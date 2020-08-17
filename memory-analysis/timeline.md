# Timeline

## log2timeline/plaso

### psteal.py

This will produce a csv file containing all the events from an image

```text
psteal.py --source ~/cases/greendale/registrar.dd -o l2tcsv -w /tmp/registrar.csv
```

## How to create a timeline from harddrive image and memory dump with SleutKit and timeliner plugin?

### SleutKit

Extract filesystem bodyfile from .E01 file

```text
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

```text
cat Evidence1-timeliner.body >> Evidence1-bodyfile
cat Evidence1-mftparser.body >> Evidence1-bodyfile
```

Extract the combined filesystem and memory timeline

```text
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

```text
grep -a -v -i -f whitelist.txt /path/to/plaso.csv > supertimeline.csv
```

## Timeline Explorer by Eric Zimmerman

![Color legend of the timeline explorer](../.gitbook/assets/image%20%2845%29.png)

1. Load your combined csv into Timeline Explorer with &lt;Open&gt;
2. Search with the filter or power filter

![Timeline explorer](../.gitbook/assets/image%20%2844%29.png)

### Shortcut key:

Several useful shortcuts include:

CTRL-t: Tag or untag selected rows

CTRL-d: Bring up the Details window for super timelines

CTRL-C: Copy the selected cells \(with headers\) to the clipboard. Hold SHIFT to exclude the column header

## How to create a supertime line with log2timeline?

