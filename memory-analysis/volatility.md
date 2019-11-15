# Volatility

#### Event Log File

**Finding Event Log File in Memory**

```text
$ python vol.py -f XPSP3.vmem --profile=WinXPSP3x86 pslist | grep services`
```

```text
Volatility Foundation Volatility Framework 2.4` 
0x81d97020 services.exe 692 648 16 352 0 0 2010-12-27 21:34:32
```

```text
$ python vol.py -f XPSP3.vmem --profile=WinXPSP3x86 vadinfo -p 69
```

