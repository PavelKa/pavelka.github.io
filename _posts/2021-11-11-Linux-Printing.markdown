## List of printers
```console
lpstat -p -d
```
### Enable printer
```console
cupsenable HP_LaserJet_Pro_MFP_M127fn
```
### Disable printer
```console
cupsenable HP_LaserJet_Pro_MFP_M127fn
```
### Print documents
```console
lpr *
```
### Printers status
```console
lpstat -t
```
### Print not completed jobs
```console
lpstat -W not-completed | head
```
### Print all pdf documents in curret directory recursive
```console
find . -name '*.pdf' -exec lp {} \;
```