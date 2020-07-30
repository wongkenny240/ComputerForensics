# Nuix Processing

![Global Options](../.gitbook/assets/image%20%2824%29.png)

Workstation can be configured through Global Options \(named Preferences in macOS\). When Global Options are set, they are applied only to the current user’s profile and will persist until further changes are made. Configuration options for an individual user, such as metadata profiles, lists, and saved searches, can be saved as case options.

This window presents a list of existing profiles that have been created.

Use the “+” button to create a new profile.

Use the pencil button to edit/modify an existing profile.

Use the “-“ button to delete an existing profile.

When you create a profile, you have the capability to make it available to everyone \(local computer\), or just for a specific user.

## Data Processing Settings

![Data Processing Settings](../.gitbook/assets/image%20%2825%29.png)

Nuix Workstation offers the following options for processing evidence:

### Evidence Settings

| Options | Description |
| :--- | :--- |
| Perform Item Identification | Enables further indexing options to be performed on individual items beyond a light scan of the file system properties on the outside of items. If this option is not selected, Nuix Workstation creates an "Unknown Binary File" entry for each physical file it encounters along with only limited file system metadata. |
| Calculate processing size up-front | Enables the progress bar to display progress during the ingestion process by the physical file size of the evidence. |

| Traversal Options | Description |
| :--- | :--- |
| Full traversal | will extract all items completely according to the evidence processing settings selected below. |
| Process loose files but not their contents | allow a quick directory listing of all the files presented for ingestion without any further extraction. |
| Process loose files and forensic images but not their contents | allow forensic images to be treated like a file directory along with any loose files for ingestion without any further extraction. |

### Deleted File Recovery and Forensic Settings

| Options | Description |
| :--- | :--- |
| Recover deleted files from disk images | Recovers all deleted files from disk images. |
| Extract end-of-file slack space from disk images | Extracts the end of file slack space from disk images. |
| Smart Process Microsoft Registry files | Only sections of the Microsoft Windows Registry that are most useful for forensic investigations are processed when this option is selected. |
| Extract from mailbox slack space | Extracts deleted files from PST, OST and EDB mailboxes at a different, lower level allowing access to slack space items. It is recommended this is used in conjunction with the storing binary option. |
| Index unallocated space | This will text strip the unallocated space for text index searches. The resulting item will be the entire unallocated space when a match is found. |
| Carve file system unallocated space | Carves files from the system unallocated space. It is recommended that this setting is only used when reloading selected unallocated space items after initial processing. |

### Text Indexing Settings

| Options | Description |
| :--- | :--- |
| Analysis Language | Select the language, either English or Japanese, to be used for text indexing. Only one language can be used per the evidence store and cannot be changed when using the Reuse Evidence Store option. |
| Use stop words | By selecting this option, the stop words, or noise words, for the selected language will not be indexed. The English language stop words are: a, an, and, are, as, at, be, but, by, for, if, in, into, is, it, no, not, of, on, or, such, that, the, their, then, there, these, they, this, to, was, will and with. |
| Use stemming | When this option is set, Nuix Workstation creates a different type of text index that stores only stemmed components of words. For example, if the search word is "control", having this option enabled returns documents containing "control", "controlling", "controller", "controls" not just returning only “control”. Once set, the option is applicable to the entire case. |

For forensic E01 image, Perform Item Identification are usually selected. The checkbox essentially enables the MIME types tab. If this is not selected, Nuix will not be able to initially identify file types for classification under the Filtered Items section.

Traversal. For forensic images, I always select “process loose file and forensic images but not their contents”. This selection performs a directory listing of all files but does not perform any further analysis of file contents

Recover deleted files from disk images. I like to have this option enabled so deleted content is already identified and recovered prior to any further processing of the evidence. If I choose to do carving and indexing of unallocated space, I do that in a separate reprocessing step.

## Decryption Keys

The Decryption Keys tab enables you to manage password lists and configure keys and passwords used when processing.

![Decryption Keys](../.gitbook/assets/image%20%2834%29.png)

### Password Discovery

Password bank for decrypting files enables you to manage password lists by adding manually or importing a word list via a txt file. The password bank:

* Is done at the case level.
* Provides ingestion time decryption time of items.
* Supports the following formats:
  * Microsoft Office 2010+ \(.docx, .xlsx, .pptx\),
  * Microsoft Office pre-2010 \(.doc, .xls, .ppt\),
  * Adobe PDF documents \(.pdf\),
  * Zip archives \(.zip\),
  * 7Zip archives \(.7z\)
  * Bitlocker
  * FileVault2

The following options are displayed:

| Options | Description |
| :--- | :--- |
| Password Directory Mode | Select word-list if you want to add a word list. By default, Password Directory Mode is set to None. This must be selected each time you ingest or reload items. It is disabled by default since it is a time-consuming process. |
| Word list | When selecting word-list as the mode, the drop-down list enables you to select word-lists. It is recommended to keep .txt files for different cases. |
| Manage password lists | Enables you to add word list, password, import and export words. Add a word list, click +. To import words into the word list, click Import Words option and select a .txt file. To export, click Export Words and specify the file name and location. |

### Example of Decryption

![Export View &amp;gt; Export View to File](../.gitbook/assets/image%20%2827%29.png)

![](../.gitbook/assets/image%20%2831%29.png)

Export View &gt; Export View to File to save the word list to a csv file

![Copy the password list from the csv file to a text file ](../.gitbook/assets/image%20%2829%29.png)

Copy the password list from the csv file to a text file

![Reload Items from Source Data](../.gitbook/assets/image%20%2826%29.png)

Reload Items from Source Data

![](../.gitbook/assets/image%20%2832%29.png)

Evidence Processing Settings &gt; Decryption Keys &gt; Word list &gt; Import Words

Select our password txt file to import the word list

![](../.gitbook/assets/image%20%2830%29.png)

Select our word list in the drop down box

![](../.gitbook/assets/image%20%2828%29.png)

Wait for evidence processing to complete

![](../.gitbook/assets/image%20%2833%29.png)

Decryption Password will be shown

## Worker Script

This tab allows you to deploy the scripts \(or Java code\) prior to starting your data processing. This allows you to carry out these operations at the earliest opportunity, improves efficiency and allows for a greater level of flexibility managing your investigation workflow.

In the Worker Script tab, select the language to enter your script.

![](../.gitbook/assets/image%20%2835%29.png)

Please refer to Nuix Scription Worker script section for more details

## Pre-Filtering the Evidence

You can choose specific files or folders to add as evidence from within compound files here. Some examples include:

* Exchange Database Files \(\*.EDB\): Process only specific custodian mailboxes from within an EDB or select only a single custodian's Inbox or Calendar for processing.
* Forensic Images \(E01, L01, DD\): Process only specific folders from within an image \(Documents and Settings or Users\).
* NSF files: Selectively process-specific views from within a Lotus NSF file, instead of extracting all documents.

![](../.gitbook/assets/image%20%2836%29.png)

I deselect any volumes I do not want to include for analysis, typically only selecting the operating system volume and Unallocated Space.

## Sample Processing Settings

![From Nuix Webinar](../.gitbook/assets/image%20%2840%29.png)

Tier 1

![](../.gitbook/assets/image%20%2839%29.png)

In the ‘MIME Type Filtering’ tab deselect the following: 
|File Group|File Type|
| :--- | :--- |
|Spreadsheets |CSV files \(deselect Descendants\) |
|System Files| Microsoft Registry Decoded Data |
||Microsoft Registry Key| 
|Containers |Java Archive |
||Microsoft Registry File| 
|No Data|Inaccessible Content |
|Logs|All|

