> Written with [StackEdit](https://stackedit.io/).

## Installing Atom Packages off Company Network
Sometimes the GUI from Atom to install new packages doesn't work fine. Therefore you must use the `apm` (Atom Package Management) command:
```bash
$ apm install package-name
```
Open the Windows CMD console as administrator.
## Updating Atom Packages off Company Network
Sometimes the GUI from Atom to install new packages doesn't work fine. Therefore you must use the `apm` (Atom Package Management) command:
```bash
$ apm update package-name
```
Open the Windows CMD console as administrator.

### [Opening same directory in Multiple Windows?](https://discuss.atom.io/t/opening-same-directory-in-multiple-windows/16523)

How to open two Atom windows on the same project. In that way, you can execute a long code in one Atom instance and continue developing code on the other instance. 

you need to use the command `atom -n project-folder-locaton`. For example:
```
C:\Users\T93KQI0>atom -n C:\Users\T93KQI0\Documents\Projects\Geospatial-Analysis
``
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMzg4MjEyNSwxNDgyMTY0OTUsLTExNT
E4NTg4NzEsNDcwMzg3NDc3XX0=
-->