# Acquisition Method

## FastBloc SE

1. Make sure no devices are attached \(or only your storage device is attached\)
2. Tools &gt; FastBloc SE &gt; Write Blocked
3. Attach the target device to the system
4. In EnCase, either create a new case or open an existing one
5. Add Evidence &gt; Add Local Device
6. On the page that follows, accept the defaults and click Next. On the screen that follows, you will see a dot or Yes in the Write Blocked column, and the icon for the device will have a green box around it, both indicating a successful write block.
7. Select the write-blocked target device \(blue check\) &gt; Finish &gt; double click the evidence &gt; Acquire

```text
Write Block = writes are prevented but are cached locally to prevent Windows error messages
Write Protect =  writes are prevented, nothing is cached locally, and Windows launches error messages when writes are attempted
```

After finished acquiring &gt; Physically remove the device &gt; Stop the write-blocking software in EnCase \(Tools &gt; FastBloc SE &gt; Clear All\)

## Tableau Write Blocker

## LinEn

