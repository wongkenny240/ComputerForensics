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

Sometimes you may not want to do a complete timeline that extracts events from every discovered file. To do a more targeted timelining, the -f FILTER\_FILE parameter can be used.

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

Also prefer to use docker to run log2timeline and psort as it is the latest version

Install docker from docker hub

```bash
docker pull log2timeline/plaso
```

Run it from your directory \(mount your data directory to docker container's volume \(i.e. /data\)

```bash
docker run -v </YOUR DATA DIR/>:/data log2timeline/plaso log2timeline /data/evidences.plaso /data/evidences
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

