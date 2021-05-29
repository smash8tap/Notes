- WMIC = Windows Management Instrumentation Control Command
	- Built in to WinXP pro through Windows10
- Can be used to interact with various aspects of a system
	- processes, services, startup and more
- Runs against local system by default
	- Or can be invoked to take action on a target
- To make it run a program on a target immediately, use:
`C:\> wmic /node:[targetIP] /user:[admin_user] /password:[password] process call create [command]`

- Use `/node:@[filename]` to run a command on all target machines listed on per line in filename

**Wmic doesent creates log entries**

## Interacting with Process with WMIC

- List the processes on target:
`C:\> wmic /node:[targetIP] /user:[admin_user] /password:[password] process list brief`
- Kill a process on a target by PID:
`C:\> wmic /node:[targetIP] /user:[admin_user] /password:[password] process where processid="[PID]" delete`
- Kill process on a target by name with:
`C:\> wmic /node:[targetIP] /user:[admin_user] /password:[password] process where name="[name]" delete`