## Sysinternal's Psexec
- Freely available from Microsoft Sysinternals 
- MS Psexec creates a service on the remote machine and leaves it behind after disconnecting
-  You have to delete the service with `sc` command

`psexec \\[target IP] [-d] [-u user] [-p password] command`
-  Will use existing user's creds if no -u and -p provided
- By default stdin and stdout sent from/to psexec
- `-d` run detached (in background, no interaction with stdin or stdout )

## Metasploit psexec module

- Makes smbsession with the target box
- Writes rev shell code on the target box
- creates the service to run the code
- starts the service
- deltes the service and code