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

You need to open (Windows) the CMD terminal.

you need to use the command `atom -n project-folder-location`. For example:
```
C:\Users\T93KQI0>atom -n C:\Users\T93KQI0\Documents\Projects\Geospatial-Analysis
```
### [How To Customize Script Console Of Atom Editor](http://www.rebellionrider.com/how-to-customize-script-console-of-atom-editor/)

This is to change font size, color and other characteristics on the Script Console to run code on Atom. The original font size is too small and white. 

Here there CSS colors you can use: [css_colors](https://www.w3schools.com/cssref/css_colors.asp)

### Atom not showing folders ignored by `.gitignore` in editor

- [https://stackoverflow.com/questions/24079976/how-to-hide-pyc-files-in-atom-editor/24728871#24728871](https://stackoverflow.com/questions/24079976/how-to-hide-pyc-files-in-atom-editor/24728871#24728871)
- [https://github.com/atom/atom/issues/3429](https://github.com/atom/atom/issues/3429)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1Nzc2NzMxMSwxNzQyMzY1MzQsLTE4Mz
A1ODA2NTcsNjM4ODkwNjczLDE0ODIxNjQ5NSwtMTE1MTg1ODg3
MSw0NzAzODc0NzddfQ==
-->