We can use service controller command (sc) to define our executable as a new service and then start it
```
C:\> net use \\[targetIP] [password] /u:[admin_user]
C:\> sc \\[targetIP] create [svcname] binpath= [command]
C:\> sc \\[targetIP] start [svcname]
```

- The downside: it runs for 30 sec, and then the system kills it 
	- because it doesent make an API call back saying that the service started successfully

## Making executable more suitable as service

- **Option A**: Use sc to start a cmd.exe, which we use to invoke another command
	- The cmd.exe lives for only 30 sec, but the command it spawns will continue running:
	`c:\> sc \\[targetIP] create [svcname] binpath= "cmd.exe /k [command]"`
- **Option B**: Use a program to wrap an executable so that it throws the API call indicating a successfull service start
	- Use ServifyThis tool, Available at http://www.inguardians.com/tools