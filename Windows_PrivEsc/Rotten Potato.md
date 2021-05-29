## The Exploit
- Get a msf shell using any meterpreter payload
![[Pasted image 20210504235902.png]]

- Check your privs with `whoami /priv` or msf's command `getprivs`

![[Pasted image 20210505000148.png]]

- We have **SeImpersonatePrivs**, Lets upload rottenpotato to the windows box
![[Pasted image 20210505000336.png]]

- Now Load `incognito` module in metasploit
![[Pasted image 20210505000505.png]]
Right now we dont have any tokens to impersonate

- Lets run rottenpotato.exe on the box
![[Pasted image 20210505000701.png]]

Boom we have NT Authority\Sytem's token
- Impersonate Token:
![[Pasted image 20210505000837.png]]

## Note

- You can use **Lonely Potato** to do this exploit without metasploit