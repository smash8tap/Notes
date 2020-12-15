## View Network Connections
- netview: Shows shares to the current pc
- netsession: Who is currently talking with current system
- net use: who is the current system talking to

### Netstat
`netstat -naob` We can see the open TCP and UDP connection
- -a: Displays all active TCP connections and the TCP and UDP ports on which the computer is listening
-  -n: Displays active TCP connections, however, addresses and port numbers are expressed numerically and no attempt is made to determine names
-  -o: Displays active TCP connections and includes the process ID (PID) for each connection.
-  -b:  displays the executable involved in creating each connection or listening port.
- -f: shows the fully qualified domain name (when available)

### Tasklist

- `tasklist /svc`: shows services associated to a pid
- `tasklist /m <modulename>` 
- `tasklist /m /fi "pid eq [proc_id]"` 
	- /fi : filter

### Wmic
- `wmic process list full`
- `wmic process get name, parentprocessid, processid`
- `wmic process where processid=[pid] get commandline`