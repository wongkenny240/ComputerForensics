# Timeline

## Plaso

* log2timeline is a command line tool to extract events from individual files, recursing a directory \(e.g. mount point\) or storage media image or device. log2timeline creates a plaso storage file which can be analyzed with the pinfo and psort tools.
* psort is a command line tool to post-process plaso storage files. It allows you to filter, sort and run automatic analysis on the contents of plaso storage files.
* psteal is a command line tool that combines the functionality of log2timeline and psort.

![Plaso tools](../.gitbook/assets/image%20%2874%29.png)

### psteal.py

This will produce a csv file containing all the events from an image

```python
psteal.py --source ~/cases/greendale/registrar.dd -o l2tcsv -w /tmp/registrar.csv
```

### log2timeline \(1st step\)

```text
log2timeline.py [-z TIMEZONE] [-f filterfile] [--parsers PARSER_LIST] -i[-o OFFSET] [--vss] [.plaso dump] [image file] ["FILTER"]
```

Sometimes you may not want to do a complete timeline that extracts events from every discovered file. To do a more targeted timelining, the **-f FILTER\_FILE** parameter can be used.

I usually use the filter\_windows.yaml to shorten the loading time for all windows image

### psort \(2nd step\)

```text
psort.py [-a] [-o FORMAT] [-w OUTPUTFILE] [-z TIMEZONE] STORAGE_FILE FILTER
```

I usually use the date filter to filter away the irrelevant date in this step

```text
psort.py -o l2tcsv -w registrar.csv registrar.plaso "date > '2010-01-01' and date < '2020-01-01'"
```

To see a list of support format

```text
psort.py -o list
```

#### Docker

Also we can use docker to run log2timeline and psort as it is the latest version and we don't need to bother with the dependencies

Install docker from docker hub

```bash
docker pull log2timeline/plaso
```

Run it from your directory \(mount your data directory to docker container's volume \(i.e. /data\)

```bash
docker run -v </YOUR DATA DIR/>:/data log2timeline/plaso log2timeline /data/evidences.plaso /data/evidences/<evidence file name>
```

### Timeline Explorer / Elasticsearch \(3rd step\)

#### Upload to elasticsearch via commandline

```text
psteal.py -o elastic --server 127.0.0.1 --port 9200 --index_name [index name] --source [image file] -w [plaso storage file]
```

#### Output as csv

When output with csv, we can open it with Eric Zimmermen's Timeline Explorer \(see below\)

## Timeline Explorer by Eric Zimmerman

![Color legend of the timeline explorer](../.gitbook/assets/image%20%2845%29.png)

1. Load your combined csv into Timeline Explorer with &lt;Open&gt;
2. Search with the filter or power filter

![Timeline explorer](../.gitbook/assets/image%20%2846%29%20%281%29.png)

### Shortcut key

Several useful shortcuts include:

CTRL-t: Tag or untag selected rows

CTRL-d: Bring up the Details window for super timelines

CTRL-C: Copy the selected cells \(with headers\) to the clipboard. Hold SHIFT to exclude the column header

## Timesketch

1. Install timesketch using docker. The detailed steps in [https://github.com/google/timesketch/blob/master/docs/Installation.md](https://github.com/google/timesketch/blob/master/docs/Installation.md)
2. Create a case after logging in [https://127.0.0.1:5000](https://127.0.0.1:5000)
3. Upload data using timesketch api


#### Upload data with Python

importing python libraries

```python
from timesketch_api_client import client
from timesketch_import_client import importer
```

connect to your timesketch server with your server ip, username and password

```python
 ts = client.TimesketchApi(SERVER_LOCATION, USERNAME, PASSWORD)
 my_sketch = ts.get_sketch(SKETCH_ID)
```

code to enumerate sketch

```python
sketches = ts_client.list_sketches()
for i, sketch in enumerate(sketches):
  print('[{0:d}] {1:s}'.format(i, sketch.name))
```

Output
```
[0] MUSCTF 2019
[1] The Greendale incident - 2019
[2] The Greendale investigation
```

set target sketch
```python
my_sketch = sketches[0]
```

use a streamer to upload the data to the server

```python
  with importer.ImportStreamer() as streamer:
    streamer.set_sketch(my_sketch)
    streamer.set_timestamp_description('Web Log')
    streamer.set_timeline_name('excel_import')
    streamer.set_message_format_string(
        '{What:s} resulted in {Results:s}, pointed from {URL:s}')

    streamer.add_data_frame(frame)
```

#### Search queries for timesketch

{% embed url="https://blog.compass-security.com/2019/03/windows-forensics-with-plaso/" caption="" %}

#### File Download Capabilities

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| Mail Attachements | NO | There is just no parser for mail attachments but this is a case where analysts are usually well off with a commercial forensic suite. |
| Skype History | YES | parser:”skype” |
| Browser Artifacts | YES | source\_short:”WEBHIST” |
| Downloads | YES | parser:”firefox\_downloads” OR parser:”msiecf”  Note that msiecf contains general browsing artifacts and is not limited to file downloads only. |
| ADS Zone.Identifier | NO |  |
| Open/Save MRU | CLAIMED | MRU parsers pose to be some sort of jungle yet. Plaso has a total of six different MRU list parsers\[5\].  Unfortunately, it is not documented which one parses which artifact. Even though they have different names, it is hard to guess which artifact they get and one definitely cannot get around digging into the source code.  However, empirical tests of the six MRU list parsers did not include the NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU registry items that contains the Open/Save MRU artifacts. |

#### Program Execution Analysis

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| UserAssist | YES | parser:”userassist” |
| Last-VisitedMRU | YES | “\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU” OR “\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU” |
| SystemBoot Autostart Progs. | YES | parser:”windows\_run” |
| SystemBoot Autostart Svcs. | YES | parser:”windows\_services” |
| AppCompatCache/  Shimcache | PARTIAL | parser:”appcompatcache”  The parser gets the executable which is the most important artifact. However, the shimcache would also include other information such as file size, last modification time,last update time as well as the execution flag. The parser would need to be improved to get the supplement information as well. |
| RecentApps | YES | “\Software\Microsoft\Windows\CurrentVersion\Search\RecentApps” |
| Prefetch | YES | parser:”prefetch” |
| LastCommands Executed | YES | “\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU” OR “\Software\Microsoft\Windows\CurrentVersion\Explorer\Policies\RunMRU” parser:”mrulist\_string” AND “\CurrentVersion\Explorer\RunMRU” |
| Amcache.hive / RecentFile-Cache.bcf | PARTIAL | parser:”amcache”  This parser was run against a Windows 10 image and it was not capable to parse events. This parser is likely to be buggy. In general, event parsing seems to be tricky as we noticed event parser to fail for various reasons. |
| SRUM | CLAIMED | parser:”srum”  Make sure to configure the SRUM artifact files in your filter.conf file. With our setup, log2timeline had troubles to extract the /Windows/System32/SRU folder from the image and Plaso failed to properly parse it. Thus, manually extracting the folder and running the parser will yield results. |
| BAM/DAM | YES | “\Services\bam\UserSettings\” OR “\Services\dam\UserSettings\” |

#### **Deleted Files or File Knowledge**

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
|  |  |  |
| Thumbnails | NO | log2timeline/Plaso is a tool designed to extract meta information from files. Thus, it will collect timestamps from images but for analyzing media artifacts such as pictures, music or video it is recommended to rely on a commercial forensics suite. |
| Thumbcache | NO | See above. |
| WordWheelQuery | YES | “\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery”&gt;br&gt; parser:”mrulistex\_string” AND “\WordWheelQuery” |
| RecycleBin | YES | parser:”recycle\_bin” |

#### Network Activity and Physical Locations

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| Network History | YES | parser:”networks” |
| Shares, offline caching | YES | “\Services\lanmanserver\Shares” |
| MappedDrives | YES | parser:”winreg/network\_drives” |
| WLANEvent Log | YES | parser:”winevtx” AND \(event\_identifier:”11000″ OR event\_identifier:”8001″ OR event\_identifier:”8002″ OR event\_identifier:”8003″ OR event\_identifier:”6100″\) |

#### **File/Folder Opening**

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| UserAssist | YES | parser:”userassist” |
| Last-VisitedMRU | YES | “\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU” OR “\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU” |
| SystemBoot Autostart Progs. | YES | parser:”windows\_run” |
| SystemBoot Autostart Svcs. | YES | parser:”windows\_services” |
| AppCompatCache/  Shimcache | PARTIAL | parser:”appcompatcache”  The parser gets the executable which is the most important artifact. However, the shimcache would also include other information such as file size, last modification time,last update time as well as the execution flag. The parser would need to be improved to get the supplement information as well. |
| RecentApps | YES | “\Software\Microsoft\Windows\CurrentVersion\Search\RecentApps” |
| Prefetch | YES | parser:”prefetch” |
| LastCommands Executed | YES | “\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU” OR “\Software\Microsoft\Windows\CurrentVersion\Explorer\Policies\RunMRU” parser:”mrulist\_string” AND “\CurrentVersion\Explorer\RunMRU” |
| Amcache.hive / RecentFile-Cache.bcf | PARTIAL | parser:”amcache”  This parser was run against a Windows 10 image and it was not capable to parse events. This parser is likely to be buggy. In general, event parsing seems to be tricky as we noticed event parser to fail for various reasons. |
| SRUM | CLAIMED | parser:”srum”  Make sure to configure the SRUM artifact files in your filter.conf file. With our setup, log2timeline had troubles to extract the /Windows/System32/SRU folder from the image and Plaso failed to properly parse it. Thus, manually extracting the folder and running the parser will yield results. |
| BAM/DAM | YES | “\Services\bam\UserSettings\” OR “\Services\dam\UserSettings\” |

#### Account Usage

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| RDP | YES | parser:”winevtx” AND \(event\_identifier:”4778″ OR event\_identifier:”4779″\) |
| ServiceEvents | YES | parser:”winevtx” AND \(event\_identifier:”7034″ OR event\_identifier:”7035″ OR event\_identifier:”7036″ OR event\_identifier:”7040″  OR event\_identifier:”7045″ event\_identifier:”4097″\) |
| LogonTypes | YES | parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;2/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;3/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;4/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;5/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;7/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;8/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;9/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;10/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;11/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;12/” parser:”winevtx” AND event\_identifier:”4624″ AND xml\_string:”/LogonType\”\&gt;13/” |
| AuthenticationEvents | YES | parser:”winevtx” AND \(event\_identifier:”4776″ OR event\_identifier:”4768″ OR event\_identifier:”4769″ OR event\_identifier:”4771″\) |
| Success/FailLogons | YES | parser:”winevtx” AND \(event\_identifier:”4624″ OR event\_identifier:”4625″ OR event\_identifier:”4634″ OR event\_identifier:”4647″ OR event\_identifier:”4648″ OR event\_identifier:”4672″ OR event\_identifier:”4720″\) |

#### External Devices, Storage

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| IDs, First/LastTime Use | PARTIAL | parser:”windows\_usb\_devices”parser:”windows\_usbstor\_devices”but the connection times are missing.  These parsers get some information out of the registry such as which USB devices were connected. But the parsers do not analyze the setupapi.dev.log file which also includes some information. Currently, the the Plaso parser give some information about USB stick usage but this definitely needs improvement. |
| User | YES | ListGUIDs: “SYSTEM\MountedDevices” Users:”\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2″ |
| PnPEvents | YES | parser:”winevtx” AND event\_identifier:”20001″ |
| SerialNumbers | NO |  |
| DriveLetters and Vol. Names | NO |  |
| AuditRemovable Storage | YES | parser:”winevtx” AND event\_identifier:”4663″ |

#### Browser Usage

| Topic | Supported | Timesketch and Kibana Queries, Notes |
| :--- | :--- | :--- |
| SearchTerms | YES | source\_short:”webhist” parser:”opera\_typed\_history” OR parser:”file\_history” OR parser:”safari\_history” OR parser:”chrome\_27\_history” OR parser:”chrome\_8\_history” OR parser:”firefox\_history”  Mind that queries need some fine tuning with the URL search parameter i.e. AND “search” AND “q=” |
| History | YES | source\_short:”webhist” |
| Cookies | YES | parser:”binary\_cookies” OR parser:”chrome\_cookies” OR parser:”firefox\_cookies” OR parser:”msie\_webcache” |
| Cache | YES | Query:parser:”chrome\_cache” OR parser:”firefox\_cache” OR parser:”msie\_webcache” |
| Flash& Super Cookies | NO | No parser but not very relevant |
| SessionRestore | NO | No parser but would be nice to have one |

#### Python code for searching on TimeSketch with jupyter notebook

import the necessary libraries for searching
```python
# Import some things we'll need
from timesketch_api_client import config
from timesketch_api_client import search
import pandas as pd

```


First way of searching is to use the explore function

```python
ts_results = ctf.explore(
    <query_str>, 
    return_fields='*', # * means return all fields 
    as_pandas=True)

```

Second way of searching

```python
search_obj = search.Search(ctf)

date_chip = search.DateRangeChip()
date_chip.start_time = '2019-02-25T00:00:00'
date_chip.end_time = '2019-03-04T23:59:59'

search_obj.query_string = 'TeamViewer'
search_obj.add_chip(date_chip)
search_obj.return_fields = '*'

ts_results = search_obj.table

```

DateRangeClip object is used to control the date range of the output of the query

## How to create a timeline from harddrive image and memory dump with SleutKit and Volatility's timeliner plugin?

### SleutKit

Extract filesystem bodyfile from .E01 file

```bash
fls -r -m /Evidence1.E01 > Evidence1-bodyfile
```

### Volatility

Run the timeliner plugin against image file

```text
vol.py -f /path/to/image.001 --profile=<profile> timeliner --output=body > Evidence1-timeliner.body
```

Run the mftparser volatility plugin

```text
vol.py -f /path/to/image.001 --profile=<profile> mftparser --output=body > Evidence1-mftparser.body
```

Combine the memory timeline and mftparser timeline to the filesytem bodyfile

```bash
cat Evidence1-timeliner.body >> Evidence1-bodyfile
cat Evidence1-mftparser.body >> Evidence1-bodyfile
```

Extract the combined filesystem and memory timeline

```bash
mactime -d -b Evidence1-bodyfile [date start e.g. 20xx-xx-xx]..[date end] > Evidence1-mactime-timeline.csv
```

Apply whitelist

```text
Temporary\ Internet \Files
PrivacIE
Content.IE5
IETldCache
ACPI
MSIE\ Cache\ File
THREAD
\(\$FILE\_NAME \)
DLL\ LOADTIME
```

```bash
grep -a -v -i -f whitelist.txt /path/to/plaso.csv > supertimeline.csv
```

## How to create a supertime line with log2timeline?

