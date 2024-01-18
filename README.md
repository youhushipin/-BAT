@echo off
setlocal

REM 清理临时文件
echo Cleaning temporary files...
del /q /s %SystemRoot%\Temp\*
del /q /s %TEMP%\*

REM 清理回收站
echo Cleaning Recycle Bin...
rd /s /q %SystemDrive%\$Recycle.Bin

REM 清理系统日志
echo Cleaning system logs...
wevtutil el | foreach {wevtutil cl "$_"}

REM 清理更新缓存
echo Cleaning Windows Update cache...
net stop wuauserv
rd /s /q %SystemRoot%\SoftwareDistribution
net start wuauserv

echo Cleanup complete.
pause
exit
