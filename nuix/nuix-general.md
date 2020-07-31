# Nuix General

## Registry/Database Viewer Tab

The Registry/Database Viewer tab is used to review the contents of the Windows Registry and SQLite databases. To open a Registry/Database Viewer tab, select the required items in the Results pane and **right-click** to select **Show in Database Viewer**. The tab includes the following UI components:

* Evidence Tree: For Windows Registry, displays the decoded items, items in the case \(having Nuix logo\), and items not in the case \(without Nuix logo\) but you can still browse them. You can also browse other data such as ZIP files, registry hives, and view its file structure.
* For SQLite databases, you can browse the tables or indexes. You can tag the required items loaded into the case or view them in Workbench or Context tabs.
* Registry Key Values: When you select an item, the keys and values of the Windows Registry are displayed in this panel.
* Table Data: When reviewing SQLite databases, select the required table to view its content in this panel.
* SQL Query: Provides you an editor to write and execute SQL queries on the database.
* Decoder: When you select an item from the metadata view, the decoded text, binary, and image values of the item are displayed in this panel.

![Viewing Registry](../.gitbook/assets/image%20%2837%29.png)

![Viewing SQLite Database](../.gitbook/assets/image%20%2838%29.png)


Items Menu
The Items menu contains commands for editing, managing, and finding items in the case.
|Items Command| Function|
| ------------- | ------------- |
|Tags |Add and remove tags, including items in the associated family and/or duplicates. You can also remove a tag from the selected item(s), including items in the associated family and/or duplicates. Family relationships are generated when items are extracted from other items, such as a zip file or email with attachments. Documents with other items embedded within them, such as a Microsoft Word document with an embedded Excel Spreadsheet,PowerPoint Presentation, or video clip are also examples. Each of these items would be considered related and in a family.|
|Custom Metadata| Add and remove custom metadata, and apply the selected Custom Metadata template.|
|Custodian |Assign and unassign custodians with options to include associated family items.|
|Item Set |Add items to and remove items from item sets.|
|Review Job |Add items to and remove items from a Fast Review job.|
|Production Set| Enables you to: * Create a production set. * Add items to a production set based on the specified sort order. * Import and annotate document ID lists. * Renumber a production set. * Generate or delete print previews. * Apply export rules to a production set. * Remove items from a production set. * Markup Add or edit markup sets, and process bulk redaction.|
|Cluster Run | Generating clusters, adding items to an existing cluster, and removing clusters.|
|Automatic Classifier| Create Automatic Classifier, add and remove training items, build model,automatically classify items, remove automatically classified items, remove skipped items, export model, import model and delete automatic classifiers.
|Exclude Items| Exclude items from being available for further case activity using a new or existing exclusion rule. This suppresses the items within the data set, including items in the associated family and/or duplicates.|
|Delete Items| Delete all records and their descendants from the case. |
|Populate Stores| Regenerate both the binary natives store and the PDF image store with options to format the PDF images on generation.|




![](../.gitbook/assets/image%20%2843%29.png)

