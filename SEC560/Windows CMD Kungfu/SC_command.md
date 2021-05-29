## Controlling services with SC

It lets you interact with services

- To list running queries:
  `sc query`
- To list all services:
  `sc query state= all` (Notice the space=all)
- For detail on one service:
  `sc qc [service_name]`

## Stopping and starring services

- TO start a service:
  `sc start [service_name]`
- If service start_type is disabled, you first have to enable it before starting it:
  `sc config [service_name] start= demand`
- To stop a service:  
   ` sc stop [service_name]`

## Determining Service names

- determine the service name by looking at the output of:
  `sc query state= all`
