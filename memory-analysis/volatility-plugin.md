# Volatility Plugin

## malprocfind

```text
volatility malprocfind -f memory-image.vmem --profile=Win7SP0x86
```

The output will provide you a true or false for each check. If the check is false it means it failed the check.

The plugin will check for the following:

* PID = The right parent process ID
* Name = Process name is correct \(not misspelled\)
* Path = Process path is correct
* Priority = Right priority
* Cmdline = Command line parameters are correct
* User = Right user \(SID\)
* Session/Time = Correct Session and time started \(Most system processes run in session 0\)
* CMD = Was process spawned from the command line?
* Phollow = Does the process show signs of process hollowing?  \(Will discuss more later\)
* SPath = Looks for suspicious paths like temp directory

In addition, it will show a count of unusual processes as well as processes with no parent process.

## winesap

For detecting persistence

Volatility "winesap" Plugin:

[https://gitlab.unizar.es/rrodrigu/winesap](https://gitlab.unizar.es/rrodrigu/winesap)

## baseline

PROCESSBL A plugin that compares the running processes in 2 memory images

* can be used to detect newly started processes
* can be used to detect newly loaded DLLs

SERVICESBL A plugin that compares the services in 2 memory images

* can be used to detect modification of service configuration
* can be used to detect newly installed services

DRIVERBL A plugin that compares the kernel drivers in 2 memory images

* can be used to detect newly installed / loaded drivers

