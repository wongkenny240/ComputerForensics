# Basic EnCase

## Creating a Case

* Templates: has an extension of .CaseTemplate and is stored in the Users\\Documents\EnCase\Templates folder.
* Case information items with default values
* Bookmark folders and notes
* Tag names
* Report template
* User-defined report styles
* Base Case Folder: By default, your cases will be stored in your Documents or My Documents folder.
* Primary Evidence Cache : When EnCase loads an evidence item for viewing, it parses and stores metadata associated with that evidence item. Each acquired evidence item is assigned a GUID, and a folder by that GUID name will contain the cached data associated with that evidence item.
* Secondary Evidence Cache: This location is for previously created caches
* Case Info: several fields into which you can or should enter data pertaining to the case. The fields will vary according to the template you select in Templates

## Verify Evidence

Evidence tab &gt; drop down menu &gt; Verify File Integrity &gt; File Integrity/ MD5/SHA-1 / CRC Errors

_Note: Add Evidence will automatically verify the new evidence file added to the case, also reopening the case will verify the evidence files which is not verified yet._

## Timeline view

Tree Pane &gt; Set Included &gt; Timeline view &gt; Higher Resolution or Lower Resolution

Date Types &gt; select which timestamps to be viewed

![Timeline View](../.gitbook/assets/2019-04-03-16_29_25-encase-forensic%20%282%29.png)

## Sort

First sort \(either one of the following\):

* Open sort menu from Table toolbar
* Double click the header of the column you want to sort

Second sort:

* Hold down the Shirt key &gt; double click the column header

Sort in opposite direction:

* CTRL + double click column header
* CTRL + SHIFT + double click the column header

Remove Sort:

* Remove sort in the Sort menu
* Double click

![](../.gitbook/assets/image%20%2861%29.png)

## File Types view

* Add File Type View &gt; File Types &gt; New
* Add a File Viewer Open With &gt; File Viewers &gt; New File Viewer

![View &amp;gt; File Types](../.gitbook/assets/2019-04-04-15_01_05-greenshot.png)

![New File Type](../.gitbook/assets/2019-04-04-15_01_32-greenshot.png)

## Evidence Processor

![Right Click &amp;gt; Process](../.gitbook/assets/2019-04-04-14_48_55-greenshot.png)

![Evidence Processor](../.gitbook/assets/image.png)

* Prioritization

![](../.gitbook/assets/2019-04-04-14_52_15-greenshot.png)

* Recover Folders
* Hash Analysis
* File Signatures Analysis
* Finding Email
* Finding Internet Artifacts
* Search Keywords

