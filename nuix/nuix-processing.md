# Nuix Processing

![Global Options](../.gitbook/assets/image%20%2824%29.png)

Workstation can be configured through Global Options \(named Preferences in macOS\). When Global Options are set, they are applied only to the current user’s profile and will persist until further changes are made. Configuration options for an individual user, such as metadata profiles, lists, and saved searches, can be saved as case options.

This window presents a list of existing profiles that have been created. 

Use the “+” button to create a new profile.

Use the pencil button to edit/modify an existing profile. 

Use the “-“ button to delete an existing profile. 

When you create a profile, you have the capability to make it available to everyone \(local computer\), or just for a specific user.

Data Processing Settings

![Data Processing Settings](../.gitbook/assets/image%20%2825%29.png)

Nuix Workstation offers the following options for processing evidence: 
|Options | Description|
| ------------- | ------------- |
|Perform Item Identification |Enables further indexing options to be performed on individual items beyond a light scan of the file system properties on the outside of items. If this option is not selected, Nuix Workstation creates an "Unknown Binary File" entry for each physical file it encounters along with only limited file system metadata. |
|Calculate processing size up-front |Enables the progress bar to display progress during the ingestion process by the physical file size of the evidence. |

|Traversal Options| Description
| ------------- | ------------- |
| Full traversal| will extract all items completely according to the evidence processing settings selected below.|
|Process loose files but not their contents| allow a quick directory listing of all the files presented for ingestion without any further extraction.
|Process loose files and forensic images but not their contents| allow forensic images to be treated like a file directory along with any loose files for ingestion without any further extraction.|



