# Prefetch

Prefetch file path

```
%SystemRoot%\Prefetch
```

File name

* Boot Prefetch: NTOSBOOT-B00DFAAD.pf

* Application prefetch: <filename>-<filepath hash> .pf

Example: CALC.EXE-AC08706A.pf

The hash is a hash of the file’s path. In this example, CALC.EXE is located in C:\Windows\System32. If it were copied to another location (like the Desktop) and executed, a new .pf file would be created reflecting a hash of the new path

### Boot prefetching vs. application prefetching 
#### Boot Prefetching 
* Boot related files are scattered or fragmented on storage 
* Slow boot 
* Monitors up to 120 seconds at system boot time by Prefetcher 
* Monitor the file you use for booting and save the results to a file 
* Speed up booting with prefetched files 
#### Application Prefetching 
* Cache manager monitors the first 10 seconds of application initial launch 
* Monitor the file used for 10 seconds and save the result as a file 
* Faster initial execution speed with prefetch files when rerunning prefetched applications 
* The maximum number of files is 128. 
* Automatically delete unused files when the limit is exceeded

### Information that can be obtained from the prefetch file 
* Application name 
* Application Execution Count 
* Application's last run time (FILETIME, 64-Bit Timestmamp) 
* Reference list (path to DLL, SDB, NLS, INI, etc. required for execution) 
* Integrated analysis using file system time information (creation, modification, access time) 
* Automatic prefetch file generation when malicious code is executed 
* Boot-prefetch file detects malware loaded at boot 
* List of loaded libraries and files can be checked from the reference list

