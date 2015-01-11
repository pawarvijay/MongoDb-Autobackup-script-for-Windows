@echo off

REM Create a file name for the database output which contains the date and time. Replace any characters which might cause an issue.
set filename=database Date_%date%_Time_%time%
set filename=%filename:/=-%
set filename=%filename: =__%
set filename=%filename:.=_%
set filename=%filename::=-%

REM Export the database

echo Running backup "%filename%"
C:\Users\sony\Desktop\mongodb-win32-i386-2.6.6\bin\mongodump --out --nojournal C:\database_backups\%filename%

REM ZIP the backup directory
REM echo Running backup "%filename%"
REM "c:\Program Files\7-Zip\7z.exe" a -tzip "%filename%.zip" "%filename%"

REM Delete the backup directory (leave the ZIP file). The /q tag makes sure we don't get prompted for questions 
REM echo Deleting original backup directory "%filename%"

REM rmdir "%filename%" /s /q

FORFILES /p C:\database_backups /S /D -3 /C "cmd /c IF @isdir == TRUE RMDIR /S /Q @path"

echo BACKUP COMPLETE

