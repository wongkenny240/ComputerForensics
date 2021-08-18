# Recycle Bin

![Recycle bin behavior between Windows XP, 2003 \(Upper\) and Windows Vista, 7 \(Below\)](../.gitbook/assets/image%20%28102%29.png)

## \Recycler \(Before Vista\)

When a file is placed into the Recycle Bin, Windows renames it using the following convention:

```text
 D <DriveLetter><Index#>.<FileExtension>
```

* D is a fixed character and will always be present.
*  refers to the volume from which the file was deleted.
*  references a count of the number of deleted files currently tracked by the Recycle Bin. This value increments with each deleted file or folder, and is cleared when the Recycle Bin is emptied and the system rebooted.
*  matches the original extension of the file.

Each time a new file is added to the Recycle Bin, its associated metadata is stored in a hidden file named \Recycler\INFO2. The INFO2 file tracks the following information for each file currently stored in the Recycle Bin:

* Physical \(not logical\) file size
* Date and time of deletion \(stored in UTC\)
* Original file name and path

### Folder

Windows will create a directory named \Recycler \DC\#\, where \# is the current Recycle Bin index value. The original directory’s contents will be moved into this new path, but will retain their original file names and will not be tracked in the INFO2 file.

## $Recycle.Bin \(Vista and After\)

The operating system creates two files each time a file is placed in the Recycle Bin:

```text
* \$Recycle.Bin\<SID>\$I<ID_STRING>.<FileExtension>
* \$Recycle.Bin\<SID>\$R<ID_STRING>.<FileExtension>
```

*  is a six-character identifier generated for each file placed in the Recycle Bin. 
* **$R** file is a renamed copy of the “deleted” file, similar to the **DC\# file**. 
* The **$I file** takes the place of **INFO2** as the source of accompanying metadata
* $I file contains the **original name, path, and date and time deleted** for its associated $R file.

