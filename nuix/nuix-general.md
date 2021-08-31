# Nuix General

![](../.gitbook/assets/image%20%28101%29.png)

## Registry/Database Viewer Tab

The Registry/Database Viewer tab is used to review the contents of the **Windows Registry** and **SQLite databases**. To open a Registry/Database Viewer tab, select the required items in the Results pane and **right-click** to select **Show in Database Viewer**. The tab includes the following UI components:

* Evidence Tree: For Windows Registry, displays the decoded items, items in the case \(having Nuix logo\), and items not in the case \(without Nuix logo\) but you can still browse them. You can also browse other data such as ZIP files, registry hives, and view its file structure.
* For SQLite databases, you can browse the tables or indexes. You can tag the required items loaded into the case or view them in Workbench or Context tabs.
* Registry Key Values: When you select an item, the keys and values of the Windows Registry are displayed in this panel.
* Table Data: When reviewing SQLite databases, select the required table to view its content in this panel.
* SQL Query: Provides you an editor to write and execute SQL queries on the database.
* Decoder: When you select an item from the metadata view, the decoded text, binary, and image values of the item are displayed in this panel.

![Viewing Registry](../.gitbook/assets/image%20%2837%29.png)

![Viewing SQLite Database](../.gitbook/assets/image%20%2838%29.png)

## Items Menu

![Delete Items](../.gitbook/assets/image%20%2843%29.png)

Items Menu The Items menu contains commands for editing, managing, and finding items in the case.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Items Command</th>
      <th style="text-align:left">Function</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Tags</td>
      <td style="text-align:left">Add and remove tags, including items in the associated family and/or duplicates.
        You can also remove a tag from the selected item(s), including items in
        the associated family and/or duplicates. Family relationships are generated
        when items are extracted from other items, such as a zip file or email
        with attachments. Documents with other items embedded within them, such
        as a Microsoft Word document with an embedded Excel Spreadsheet,PowerPoint
        Presentation, or video clip are also examples. Each of these items would
        be considered related and in a family.</td>
    </tr>
    <tr>
      <td style="text-align:left">Custom Metadata</td>
      <td style="text-align:left">Add and remove custom metadata, and apply the selected Custom Metadata
        template.</td>
    </tr>
    <tr>
      <td style="text-align:left">Custodian</td>
      <td style="text-align:left">Assign and unassign custodians with options to include associated family
        items.</td>
    </tr>
    <tr>
      <td style="text-align:left">Item Set</td>
      <td style="text-align:left">Add items to and remove items from item sets.</td>
    </tr>
    <tr>
      <td style="text-align:left">Review Job</td>
      <td style="text-align:left">Add items to and remove items from a Fast Review job.</td>
    </tr>
    <tr>
      <td style="text-align:left">Production Set</td>
      <td style="text-align:left">
        <p>Enables you to:</p>
        <p><em>Create a production set.</em>
        </p>
        <p>Add items to a production set based on the specified sort order.</p>
        <p><em>Import and annotate document ID lists.</em>
        </p>
        <p>Renumber a production set.</p>
        <p><em>Generate or delete print previews.</em>
        </p>
        <p>Apply export rules to a production set.</p>
        <p><em>Remove items from a production set.</em>
        </p>
        <p>Markup Add or edit markup sets, and process bulk redaction.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Cluster Run</td>
      <td style="text-align:left">Generating clusters, adding items to an existing cluster, and removing
        clusters.</td>
    </tr>
    <tr>
      <td style="text-align:left">Automatic Classifier</td>
      <td style="text-align:left">Create Automatic Classifier, add and remove training items, build model,automatically
        classify items, remove automatically classified items, remove skipped items,
        export model, import model and delete automatic classifiers.</td>
    </tr>
    <tr>
      <td style="text-align:left">Exclude Items</td>
      <td style="text-align:left">Exclude items from being available for further case activity using a new
        or existing exclusion rule. This suppresses the items within the data set,
        including items in the associated family and/or duplicates.</td>
    </tr>
    <tr>
      <td style="text-align:left">Delete Items</td>
      <td style="text-align:left">Delete all records and their descendants from the case.</td>
    </tr>
    <tr>
      <td style="text-align:left">Populate Stores</td>
      <td style="text-align:left">Regenerate both the binary natives store and the PDF image store with
        options to format the PDF images on generation.</td>
    </tr>
  </tbody>
</table>

