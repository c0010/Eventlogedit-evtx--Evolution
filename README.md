# Eventlogedit-evtx--Evolution
Remove individual lines from Windows XML Event Log (EVTX) files

Support: Win7 and later

Compare with DanderSpritz,my way don't need dll injection and support more version(Server2012 and later).(It can be used to delete the setup.evtx,others need more test)

Need more test and suggestions.

The data structure and some code details are inspired by https://bbs.pediy.com/thread-219313.htm

My posts about the details:

1. [Windows XML Event Log (EVTX)单条日志清除（一）——删除思路与实例](https://3gstudent.github.io/3gstudent.github.io/Windows-XML-Event-Log-(EVTX)%E5%8D%95%E6%9D%A1%E6%97%A5%E5%BF%97%E6%B8%85%E9%99%A4-%E4%B8%80-%E5%88%A0%E9%99%A4%E6%80%9D%E8%B7%AF%E4%B8%8E%E5%AE%9E%E4%BE%8B/)
2. [Windows XML Event Log (EVTX)单条日志清除（二）——程序实现删除evtx文件的单条日志记录](https://3gstudent.github.io/3gstudent.github.io/Windows-XML-Event-Log-(EVTX)%E5%8D%95%E6%9D%A1%E6%97%A5%E5%BF%97%E6%B8%85%E9%99%A4-%E4%BA%8C-%E7%A8%8B%E5%BA%8F%E5%AE%9E%E7%8E%B0%E5%88%A0%E9%99%A4evtx%E6%96%87%E4%BB%B6%E7%9A%84%E5%8D%95%E6%9D%A1%E6%97%A5%E5%BF%97%E8%AE%B0%E5%BD%95/)
3. Windows XML Event Log (EVTX)单条日志清除（三）——通过解除文件占用删除当前系统单条日志记录
4. ...

Later I'll write translate them into English.

Note:

- WinXP and Win7,ObjectTypeNumber = 0x1c
- Win8 and later,ObjectTypeNumber = 0x1e

---

### DeleteRecordofFile.cpp

Read an evtx file(c:\\test\\Setup.evtx),then delete an event log(EventRecordID=14).

The new evtx file is saved as `c:\test\SetupNew.evtx`.

### DeleteRecordbyTerminateProcess.cpp

Kill the eventlog service's process and delete one eventlog record,then restart the Eventlog Service.

### DeleteRecordbyTerminateProcessEx.cpp

Kill the eventlog service's process and delete one eventlog record,then restart the Eventlog Service.

Use WinAPI EvtExportLog to delete the eventlog.

Note:

The EventRecordID of the events after the deleted one will not be changed.

### DeleteRecordbyGetHandle.cpp

Get specified .evtx file's handle and delete one eventlog record.

It can be used to delete the setup.evtx,others need more test.

### Setup.evtx

Number of events:15

### SetupNew.evtx

Number of events:14

You can use DeleteRecordofFile.cpp to delete the second eventlog record(EventRecordID=14) of Setup.evtx.

### SuspendorResumeTid.cpp

Suspend or resume the Eventlog Service's thread.

Use to stop or resume the system to collect logs.

