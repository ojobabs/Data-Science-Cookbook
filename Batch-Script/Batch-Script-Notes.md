> Written with [StackEdit](https://stackedit.io/).

# Batch Scripting Notes

- [Difference between Batch and Bash files](https://stackoverflow.com/questions/5079180/difference-between-batch-and-bash-files)
- [Batch Script Tutorial](https://www.tutorialspoint.com/batch_script/index.htm)
- [How-to-write-a-batch-script-on-windows](https://www.howtogeek.com/263177/how-to-write-a-batch-script-on-windows/)
- [How to Create a Batch File to Run Python Script](https://datatofish.com/batch-python-script/)
- [Auto-Compressing Files with a Scheduled Batch Using 7-Zip](http://www.iron-automation.com/2018/07/automatically-compressing-files-with-a-scheduled-batch-using-7-zip/)
- [Batch-file-to-copy-files-from-one-folder-to-another-folder](https://stackoverflow.com/questions/986447/batch-file-to-copy-files-from-one-folder-to-another-folder)
- [Generate a Backup File with Timestamp using a Batch Script](https://datatofish.com/backup-file-timestamp/)
- [How to schedule a Batch File to run automatically in Windows 10](https://www.thewindowsclub.com/how-to-schedule-batch-file-run-automatically-windows-7)
- [How To Delete Files Older Than X Days in Windows 10](https://winaero.com/blog/delete-files-older-x-days/)

I used the above references to write a backup batch script for a Windows virtual machine:

> **Note**: Avoid using the option "Run with the highest privileges" when using Windows task scheduler. Otherwise, the system cannot open shared drives linke this one `X:\CDSA Data Management\ESRI\backup\%BackupName_1%.zip`. 

```batch
@echo off

:: run backup.py to export geodatabase as XML document
"C:\Program Files\ArcGIS\Pro\bin\Python\envs\arcgispro-py3\python.exe" "C:\Users\T93KQI0\Documents\Projects\Geospatial-Analysis\src\backup.py"

:: Compress XML document
"C:\Program Files\7zip\7za" a -tzip "C:\Users\T93KQI0\Documents\ArcGIS\Projects\testproject02\testproject02_ExportXMLWorks1.zip" "C:\Users\T93KQI0\Documents\ArcGIS\Projects\testproject02\testproject02_ExportXMLWorks1.xml" -mx5

:: Copy on shared folder outside VIZ compressed XML document and ArcGIS project file

for /f "delims=" %%a in ('wmic OS Get localdatetime ^| find "."') do set DateTime=%%a

set Yr=%DateTime:~0,4%
set Mon=%DateTime:~4,2%
set Day=%DateTime:~6,2%
set Hr=%DateTime:~8,2%
set Min=%DateTime:~10,2%
set Sec=%DateTime:~12,2%

set BackupName_1= testproject02_ExportXMLWorks1_%Yr%-%Mon%-%Day%_%Hr%-%Min%-%Sec%
set BackupName_2= testproject02_%Yr%-%Mon%-%Day%_%Hr%-%Min%-%Sec%

copy "C:\Users\T93KQI0\Documents\ArcGIS\Projects\testproject02\testproject02_ExportXMLWorks1.zip" "X:\CDSA Data Management\ESRI\backup\%BackupName_1%.zip"
copy "C:\Users\T93KQI0\Documents\ArcGIS\Projects\testproject02\testproject02.aprx" "X:\CDSA Data Management\ESRI\backup\%BackupName_2%.aprx"

:: Retention policy: delete all files older than one month

ForFiles /p "X:\CDSA Data Management\ESRI\backup" /s /d -30 /c "cmd /c del @file"
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTY3NTczNTIsNzAzODA4MjQ1LDE2Mj
YzMTUyMzEsMTAyNDMzMzU1OCwtNTg2MTgxOTE3XX0=
-->