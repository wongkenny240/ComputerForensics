# Prefetch

Prefetch file path

```text
%SystemRoot%\Prefetch
```

File name

* Boot Prefetch: NTOSBOOT-B00DFAAD.pf
* Application prefetch: - .pf

Example: CALC.EXE-AC08706A.pf

The hash is a hash of the file’s path. In this example, CALC.EXE is located in C:\Windows\System32. If it were copied to another location \(like the Desktop\) and executed, a new .pf file would be created reflecting a hash of the new path

## Boot prefetching vs. application prefetching

### Boot Prefetching

* Boot related files are scattered or fragmented on storage 
* Slow boot 
* Monitors up to 120 seconds at system boot time by Prefetcher 
* Monitor the file you use for booting and save the results to a file 
* Speed up booting with prefetched files 

### Application Prefetching

* Cache manager monitors the first 10 seconds of application initial launch 
* Monitor the file used for 10 seconds and save the result as a file 
* Faster initial execution speed with prefetch files when rerunning prefetched applications 
* The maximum number of files is 128. 
* Automatically delete unused files when the limit is exceeded

## Information that can be obtained from the prefetch file

* Application name 
* Application Execution Count 
* Application's last run time \(FILETIME, 64-Bit Timestmamp\) 
* Reference list \(path to DLL, SDB, NLS, INI, etc. required for execution\) 
* Integrated analysis using file system time information \(creation, modification, access time\) 
* Automatic prefetch file generation when malicious code is executed 
* Boot-prefetch file detects malware loaded at boot 
* List of loaded libraries and files can be checked from the reference list

## Prefetch File Analysis Tool

### WinPrefetchView – Nirsoft

{% embed url="http://www.nirsoft.net/utils/win\_prefetch\_view.html" %}

![](../.gitbook/assets/image%20%2814%29.png)

### PrefetchForensics – Mark Woan

{% embed url="https://github.com/woanware/woanware.github.io/blob/master/forensics/prefetchforensics.md" %}



### APFA\(Advanced Prefetch File Analyzer\) – ASH368

{% embed url="http://www.ash368.com/" %}



### Windows Prefetch Parser – TZWorks

{% embed url="https://www.tzworks.net/prototype\_page.php?proto\_id=1" %}



## Prefetch Registry Key

```text
HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters
```

EnablePrefetcher Key:

```text
0 = Disabled
1 = Application prefetching enabled
2 = Boot prefetching enabled (default on Windows 2003 only)
3 = Application and Boot prefetching enabled (default)
```

Task Scheduler calls Windows Disk Defragmenter every three \(3\) days When idle, lists of files and directories referenced during boot process and application startups is processed

* The processed result is stored in Layout.ini in the Prefetch directory, and is subsequently passed to the Disk Defragmenter, instructing it to re-order those files into sequential positions on the physical hard drive

