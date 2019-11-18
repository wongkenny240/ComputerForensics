# EnScript

## Enscript Help Function

![Enscript Help](../.gitbook/assets/image%20%285%29.png)

![Help Window](../.gitbook/assets/image%20%281%29.png)

![Code Example](../.gitbook/assets/image%20%284%29.png)

## Enscript Shortcut Key

* Run – F5 
* Undo – Ctrl-Z

## Entry Class

* Evidence Name: EvidenceFile\(\) 
* Unique Name: UniqueName\(\) 
* Description: Description\(\) 
* Original Path: OriginalPath\(\) 
* Size: PhysicalSize\(\) 
* Extent Count: ExtentCount\(\) 
* True Path: TruePath\(\) 
* Short Name: ShortName\(\) 
* Name: Name\(\) 
* Extension: Extension\(\) 
* Full Path: FullPath\(\) 
* Path: Path\(\) 
* IsSelected: IsSelected\(\) 
* IsDeleted: IsDeleted\(\)

## Case Class

| Name | Type | Allow Set | Description |
| :--- | :--- | :--- | :--- |
| BookmarkRoot | BookmarkClass | No | Tree of the case's bookmarks. |
| CaseFolder | String | No | Path to folder containing the .case file \(see also Path\). |
| CaseInfoRoot | CaseInfoClass | No | Top level object of the Case Information. |
| EmailFolder | String | No | Path to email folder in CaseFolder. |
| EvidenceRoot | EvidenceClass | No | Evidence in the case |
| ExportFolder | String | No | Returns the default export folder |
| GUID | GUIDClass | Yes | Globally unique identifier |
| HasBookmarkList | uint | No | Return 1 if the case has bookmark items, 0 for no items. |
| HasCaseInfoList | uint | No | Return 1 if the case has case info items, 0 for no items. |
| HasEvidenceList | uint | No | Return 1 if the case has evidence items, 0 for no items. |
| HasSecureList | uint | No | Return 1 if the case has secure storage items, 0 for no items. |
| HasTagsList | uint | No | Return 1 if the case has tags available for use, 0 for no tags. |
| HasTagViewsList | uint | No | Returns 1 if the case has tags defined, 0 for no tags. |
| Path | String | No | Path of the .case file. |
| PrimaryEvFolder | String | Yes | Returns the primary evidence cache folder |
| SecondaryEvFolder | String | Yes | Returns the secondary evidence cache folder |
| SecureStorageRoot | SecureStorageClass | No | Top level object of the secure storage tab. |
| TagCountViewRoot | TagCountViewClass | No | Allows you to loop through the TagCountViewClass objects in the case, which give you the name of each tag and the count of items which currently carry that tag. |
| TagItemRoot | TagItemClass | No | Top level object of tags list. |
| TemporaryFolder | String | No | Path to temp folder in CaseFolder. |
| UseBaseFolder | bool | Yes | Use base case folder for primary evidence cache. Overrides primary evidence folder settings |

## ItemIterator Class

```text
for (ItemIteratorClass iter(c, NOPROXY, CURRENTVIEW_SELECTED); EntryClass e = iter.GetNextEntry();){
    ProcessEntry(c, e, logfile, datestring);
}
```

Select Entry Items to loop

| Name | Value | Description |
| :--- | :--- | :--- |
| ALL | 0 | All items in the case |
| TAGGED | 1 | Tagged items |
| RESULT | 2 | Items in a named result set |
| CURRENTVIEW | 3 | Items in the current user view |
| CURRENTVIEW\_SELECTED | 4 | Selected items in the current user view |
| CURRENTFOLDER | 5 | Items in the current user folder |
| CURRENTFOLDER\_SELECTED | 6 | Selected items in the current user folder |

