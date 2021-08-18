# Recycle Bin

![Recycle bin behavior between Windows XP, 2003 \(Upper\) and Windows Vista, 7 \(Below\)](../.gitbook/assets/image%20%28102%29.png)

## \Recycler (Before Vista) 
When a file is placed into the Recycle Bin, Windows renames it using the following convention:
```
 D <DriveLetter><Index#>.<FileExtension>
```

* D is a fixed character and will always be present.
* <DriveLetter> refers to the volume from which the file was deleted.
* <Index#> references a count of the number of deleted files currently tracked by the Recycle Bin. This value increments with each deleted file or folder, and is cleared when the Recycle Bin is emptied and the system rebooted.
* <FileExtension> matches the original extension of the file.
