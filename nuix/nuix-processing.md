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

| Options | Description |
| :--- | :--- |
| Perform Item Identification | Enables further indexing options to be performed on individual items beyond a light scan of the file system properties on the outside of items. If this option is not selected, Nuix Workstation creates an "Unknown Binary File" entry for each physical file it encounters along with only limited file system metadata. |
| Calculate processing size up-front | Enables the progress bar to display progress during the ingestion process by the physical file size of the evidence. |

| Traversal Options | Description |
| :--- | :--- |
| Full traversal | will extract all items completely according to the evidence processing settings selected below. |
| Process loose files but not their contents | allow a quick directory listing of all the files presented for ingestion without any further extraction. |
| Process loose files and forensic images but not their contents | allow forensic images to be treated like a file directory along with any loose files for ingestion without any further extraction. |

Deleted File Recovery and Forensic Settings

| Options | Description |
| :--- | :--- |
| Recover deleted files from disk images | Recovers all deleted files from disk images. |
| Extract end-of-file slack space from disk images | Extracts the end of file slack space from disk images. |
| Smart Process Microsoft Registry files | Only sections of the Microsoft Windows Registry that are most useful for forensic investigations are processed when this option is selected. |
| Extract from mailbox slack space | Extracts deleted files from PST, OST and EDB mailboxes at a different, lower level allowing access to slack space items. It is recommended this is used in conjunction with the storing binary option. |
| Index unallocated space | This will text strip the unallocated space for text index searches. The resulting item will be the entire unallocated space when a match is found. |
| Carve file system unallocated space | Carves files from the system unallocated space. It is recommended that this setting is only used when reloading selected unallocated space items after initial processing. |

For forensic E01 image, Perform Item Identification are usually selected. The checkbox essentially enables the MIME types tab. If this is not selected, Nuix will not be able to initially identify file types for classification under the Filtered Items section.

Traversal. For forensic images, I always select “process loose file and forensic images but not their contents”. This selection performs a directory listing of all files but does not perform any further analysis of file contents

Recover deleted files from disk images. I like to have this option enabled so deleted content is already identified and recovered prior to any further processing of the evidence. If I choose to do carving and indexing of unallocated space, I do that in a separate reprocessing step.

![Export View &amp;gt; Export View to File](../.gitbook/assets/image%20%2827%29.png)

![](../.gitbook/assets/image%20%2831%29.png)

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

Wait for evidence processing

![](../.gitbook/assets/image%20%2833%29.png)

Decryption Password will be shown

