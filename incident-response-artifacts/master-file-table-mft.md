# Master File Table \(MFT\)

## Overview

* Each Each NTFS volume will contain its own MFT \(named $MFT stored within the volume root\)
* NTFS metadata files such as the $MFT are not accessible via Windows Explorer or other standard application programming interface \(API\) file-access methods. 
* Each entries is 1,024 byte
* The first 16 MFT entries are reserved for essential NTFS artifacts

## Important elements of an entry

* Record type - Specifies whether a given entry represents a file or directory.
* Record \# - An integer used to identify a given MFT entry. Record numbers grow sequentially as new entries are added.
* Parent record \# - The record number of the parent directory. Each MFT entry only tracks the record number of its immediate parent, rather than its full path on disk. 
* Active/Inactive flag - MFT entries for deleted files or directories are marked “Inactive.” NTFS will automatically reclaim and replace inactive entries with new active entries to keep the MFT from growing indefinitely.
* Attributes - Each MFT entry contains a number of “attributes” that contain metadata about a file—everything from timestamps to the physical location of the file’s contents on disk.

  Important Attributes included the following:

  * $STANDARD\_INFORMATION
  * $FILENAME
  * $DATA.

![](../.gitbook/assets/image%20%2873%29.png)

## MFT

* Collect the MFT and analyze the file timestamps

![](../.gitbook/assets/image%20%2894%29.png)

* Use MFT2CSV to convert MFT file into .csv file
* Choose the MFT file to be converted
* Select the appropriate time zone
* Set the output path
* Click start processing to proceed the conversion process

![](../.gitbook/assets/image%20%2895%29.png)

* Open the converted file using text editor or Excel

![](../.gitbook/assets/image%20%2898%29.png)

## $USNJRNL

* Choose the $J file of $USNJRNL file to be converted
* Select the appropriate time zone
* Select process output options
* Click start processing to proceed the conversion process

![](../.gitbook/assets/image%20%2897%29.png)

* Open Excel and then select Get Data through import

![](../.gitbook/assets/image%20%2896%29.png)

## $LogFiles

* Choose the $LogFile and the previous processed MFT.csv file
* Select the appropriate time zone
* Click start processing to proceed the convertion process

