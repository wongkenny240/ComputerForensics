# Timeline

## log2timeline/plaso

### psteal.py

This will produce a csv file containing all the events from an image

```text
psteal.py --source ~/cases/greendale/registrar.dd -o l2tcsv -w /tmp/registrar.csv
```


## SleutKit

```text
fls -r -m /Evidence1.E01 > Evidence1-bodyfile
```

## Volatility

Run the timeliner plugin against image file

```text
volatility -f /path/to/image.001 --profile=<profile> timeliner --output=body > Evidence1-timeliner.body
```
