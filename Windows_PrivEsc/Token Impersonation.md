# Windows 
- Some privs can override permissions set on an object
- some privs assigned to users are only available in an High IL Process (Elevated shell)
- whoam /priv will list your privs

# Windows Access Tokens
- Its assigned to user when he first logs in
- Used to verify if you can want to perform certain tasks that requires adequate privs
- Upon creation of a process or theread, a copy of token is assigned to them

# SeDebugPrivilege
- Allows user to attach a debugger to any process
- Allows read/write access to memory and change properties of any process ( including Local System, admin )
- Allows to inject code into privileged process 
- Create a new process and set the parent process a privileged process (github psgetsystem )

# SeRestorePrivilege
- Allows to restore files and registry keys
- API Calls use
	- CreateFile()
	- RegCreateKeyEx()
- Can write files anywhere, overwrite files

# SeBackupPrivilege
- "Allows to acess files"
- Backup SAM database using reg save
- Members of "Backup Operators" can logon locally on a DC and backup NTDS.dit, for eg. "wbadmin.exe" or "diskshadow.exe" to make backup using normal user with SeBackup Priv

# SeTakeOwnership Privilege
- Allows to take ownership of any scurable object in the system
- Once gained ownership, same techniques as in SeRestorePriv

# SeCreateToken Privilege
- Allows a process to create an access token by calling token-creating API
- Create custom token will all privs and group memberships
- Use the token without impersonating Seimpersonate 
- **Does not work on Win10>=1809 and Win 2019**
	- But using anonymous authentication ID we can still use it

# SeLoadDrive Priv
- By default given to printer in DCs
- load a malicious driver

# SeImpersonate and SeAssignPrimary Token Priv

- Allows to impersonate any access Token
- Normally assigned too "service users", admins, local system 
- SeImpersonate
	- Impersonate a client after authentication
- SeAssignPrimary Token
	- Assign the primary token of a process
- Use **Rotten Potato** to impersonate tokens
- **Juicy Potato** 