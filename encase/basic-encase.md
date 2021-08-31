# Basic EnCase

## Creating a Case

![](../.gitbook/assets/image%20%28112%29.png)

* **Templates**: has an extension of .CaseTemplate and is stored in the Users\Documents\EnCase\Templates folder.
* Case information items with default values
* Bookmark folders and notes
* Tag names
* Report template
* User-defined report styles
* **Base Case Folder**: By default, your cases will be stored in your Documents or My Documents folder.
* **Primary Evidence Cache** : When EnCase loads an evidence item for viewing, it parses and stores metadata associated with that evidence item. Each acquired evidence item is assigned a GUID, and a folder by that GUID name will contain the cached data associated with that evidence item.
* **Secondary Evidence Cache**: This location is for previously created caches
* **Case Info**: several fields into which you can or should enter data pertaining to the case. The fields will vary according to the template you select in Templates

### EnCase Folder Structure

* EnCase creates subfolders called Email, Export, Tags, and Temp. 
* User need to manually created Evidence and EvidenceCache.

![](../.gitbook/assets/image%20%28113%29.png)

## EnCase View

Placeholder

## Verify Evidence

Evidence tab &gt; drop down menu &gt; Verify File Integrity &gt; File Integrity/ MD5/SHA-1 / CRC Errors

_Note: Add Evidence will automatically verify the new evidence file added to the case, also reopening the case will verify the evidence files which is not verified yet._

## Timeline view

Tree Pane &gt; Set Included &gt; Timeline view &gt; Higher Resolution or Lower Resolution

Date Types &gt; select which timestamps to be viewed

![Timeline View](../.gitbook/assets/2019-04-03-16_29_25-encase-forensic%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29.png)

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

## Gallery view

* See images -&gt; Set Include Folders button in the Tree pane, you can direct the content of the Table pane
* EnCase displays images based on the file extension. After the file signature analysis has been completed, the files will display based on their file header information.

## Disk view

* Evidence tab -&gt; Place the cursor on device -&gt; Device -&gt; Disk View
* By default, you see a series of colored square blocks, each representing one sector. If you would prefer that each block represent a cluster, simply click the check box next to View Clusters on the toolbar for this view. 
* Blue blocks are allocated sectors or clusters. 
* The gray blocks with the raised bump in the center are unallocated sectors or clusters. 
* Go to a sector by typing in the sector number -&gt; Go To feature from its menu on the Disk View toolbar

![](../.gitbook/assets/image%20%2865%29.png)

## File Types view

* Add File Type View &gt; File Types &gt; New
* Add a File Viewer Open With &gt; File Viewers &gt; New File Viewer

![View &amp;gt; File Types](../.gitbook/assets/2019-04-04-15_01_05-greenshot.png)

![New File Type](../.gitbook/assets/2019-04-04-15_01_32-greenshot.png)

## Evidence Processor

![Right Click &amp;gt; Process](../.gitbook/assets/2019-04-04-14_48_55-greenshot.png)

![Evidence Processor](../.gitbook/assets/image.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Task</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Prioritization</td>
      <td style="text-align:left">
        <p>Prioritisation option</p>
        <p>
          <img src="../.gitbook/assets/image (125).png" alt/>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Recover folders</td>
      <td style="text-align:left">
        <p>Recover files that have been deleted or corrupted on FAT and NTFS volumes</p>
        <p><em>Note: When you turn on the Recover folder structure of NTFS 3.0 files option, recovery will take longer, but will reconstruct (folder tree); if you left that unchecked, all found folders will be grouped together without tree structure.</em>
        </p>
        <p>
          <img src="../.gitbook/assets/image (114).png" alt/>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">File signature analysis</td>
      <td style="text-align:left">Determine if the extension of a file has been altered and whether or not
        the extension matches the file type as specified by the file&#x2019;s header</td>
    </tr>
    <tr>
      <td style="text-align:left">Protected file analysis</td>
      <td style="text-align:left">Identify encrypted and password-protected files with the Passware Encryption
        Analyzer</td>
    </tr>
    <tr>
      <td style="text-align:left">Thumbnail creation</td>
      <td style="text-align:left">Creates image thumbnails for faster display in the EnCase&#xAE; GUI</td>
    </tr>
    <tr>
      <td style="text-align:left">Hash analysis</td>
      <td style="text-align:left">Generate MD5 and/or SHA1 hash values for files and compare against your
        case Hash Library</td>
    </tr>
    <tr>
      <td style="text-align:left">Expand compound files</td>
      <td style="text-align:left">Expand compound and compressed files, such as ZIP, RAR, GZIP, TAR, THUMBS.DB,
        CLOOP, and BZIP2</td>
    </tr>
    <tr>
      <td style="text-align:left">Find email</td>
      <td style="text-align:left">Extract individual messages from e-mail archive files, such as PST (Microsoft&#xAE;
        Outlook), NSF (Lotus&#xAE; Notes), DBX (Microsoft&#xAE; Outlook Express),
        EDB (Microsoft&#xAE; Exchange), AOL, MBOX, and EMLX (Macintosh).</td>
    </tr>
    <tr>
      <td style="text-align:left">Find Internet artifacts</td>
      <td style="text-align:left">Collect Internet-related artifacts, such as browser histories and cached
        web pages. You also have the option to search unallocated space for the
        Internet artifacts.</td>
    </tr>
    <tr>
      <td style="text-align:left">Search for keywords</td>
      <td style="text-align:left">Search raw (not transcript) text for specific keywords.</td>
    </tr>
    <tr>
      <td style="text-align:left">Index text and metadata</td>
      <td style="text-align:left">Create an index for when you need to search for keywords in compound files
        (Microsoft Office 2007 and 2010) and across large amounts of data. You
        can adjust the parameters for index creation, such as the minimum word
        length to index and whether to use a noise file (which does not index specific
        and common words).</td>
    </tr>
    <tr>
      <td style="text-align:left">System Info Parser</td>
      <td style="text-align:left">
        <p>Report on the core system information for Linux and Windows, including:</p>
        <ul>
          <li>User activity (Linux only)</li>
          <li>Operating system</li>
          <li>Hardware</li>
          <li>Software</li>
          <li>Accounts/users</li>
          <li>Network information</li>
          <li>Shared/mapped drives</li>
          <li>USB Devices</li>
          <li>Network Shares</li>
        </ul>
        <p>Advanced : Windows Registry</p>
        <ul>
          <li>Time zone setting</li>
          <li>Auto start</li>
          <li>Hardware</li>
          <li>User activity</li>
          <li>User defined keys</li>
          <li>Network Shares</li>
          <li>Other AutoRuns</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Windows Artifact Parser</td>
      <td style="text-align:left">
        <p>Report on Windows artifacts, including</p>
        <ul>
          <li>Link files</li>
          <li>Recycle Bin files</li>
          <li>MFT (NTFS Master File Table) transactions</li>
        </ul>
        <p>Option: All or selected files, and/or unallocated clusters</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Snapshot (Live preview of devices only)</td>
      <td style="text-align:left">Running processes, open ports, logged on users, etc.</td>
    </tr>
  </tbody>
</table>

## File Signature Analysis

### Create a new file signatures

![View &amp;gt; File Types](../.gitbook/assets/image%20%28116%29.png)

![Click New on the File Types table toolbar](../.gitbook/assets/image%20%28117%29.png)

![Change the extensions or Description of the file types](../.gitbook/assets/image%20%28115%29.png)

### Running File Signature Analysis against Selected Files

* Blue check the specific files you want to run signature analysis on.
* Click Entries. In the dropdown menu, click Hash\Sig Selected. The Hash\Sig Selected dialog displays.
* Select Verify file signatures to run signature analysis.
* Click OK and refresh the device after running

![Entries &amp;gt; Hash\Sig Selected](../.gitbook/assets/image%20%28118%29.png)

### File Signature Analysis

| extension | header | Header in Table | Extension | Signature | Signature Analysis |
| :--- | :--- | :--- | :--- | :--- | :--- |
| picture.jpg | FF D8 FF E0 | Known | Known and matches | JPEG Image Standard | Match |
| picture.dll | FF D8 FF E0 | Known | Known and incorrect | JPEG Image Standard | Alias |
| anyfile.zza | FF D6 FE FF | Unknown | Unknown |  | Unknown |
| picture.jpg | D8 D8 FF E0 | Unknown | Known and doesn't match |  | Bad Signature |

* Search for different types of results with filter
* Find Entries by Signature
* The results will be in Result tab

## Hash Analysis

### Creating hash libraries and hash sets

* Before you can create any hash sets from within EnCase, you must first create a hash library container, which is a folder containing a series of file-based, database-like structures into which EnCase will store hash sets. 

![Create a folder](../.gitbook/assets/image%20%28124%29.png)

* Tools -&gt; Manage Hash Libraries 

![Tools &amp;gt; Manage hash library](../.gitbook/assets/image%20%28119%29.png)

* Manage hash libraries -&gt; new hash library 

![New hash library &amp;gt; Select the folder \(container\) you created](../.gitbook/assets/image%20%28122%29.png)

* Importing legacy hash sets into EnCase

 

![Importing legacy EnCase hash sets](../.gitbook/assets/image%20%28123%29.png)

### Adding hash values to the hash sets and library

* Query the hash libraries for a MD5 hash
* Manage Hash Library -&gt; Query 

![Manage Hash Library &amp;gt; Query](../.gitbook/assets/image%20%28120%29.png)

* Add to hash library -&gt; Right Click New Hash Set

 

![Add to Hash Library &amp;gt; Right click New Hash Set](../.gitbook/assets/image%20%28121%29.png)

### Using hash values to identify/exclude files

* Entries -&gt; Hash\Sig Selected
* Find Entries by Hash Category -&gt; Result tab

### Hash Analysis Summary

* Creating a Hash Library
  * Tools &gt; Manage Hash Library
  * New button
  * Browse for a folder -&gt; click OK
* Import hash sets from another library
  * Tools &gt; Manage Hash Library
  * Click Import from the toolbar
* Creating a Hash Set
  * Tools &gt; Manage Hash Library
  * click New Hash Set. The Create Hash Set dialog appears
* Adding Hash Values to a Hash Set
  * Hash the item by right click item Entries -&gt; Hash\Sig Selected
  * Right click Entries -&gt; Add to hash library
  * Choose the hash library to add to
  * Select one existing hash sets or create new hash set by right clicking
  * Select Fields

![Add to hash library](../.gitbook/assets/image%20%28126%29.png)

* Adding Hash Values to a Hash Set from Results

