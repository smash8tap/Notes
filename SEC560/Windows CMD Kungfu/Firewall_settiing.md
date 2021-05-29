- Check network settings:
  `netsh /?`
- Check firewall rules
  `netsh advfirewall show allprofiles`
- Allow a given port inbound:
  `netsh advfirewall firewall add rule name="[Comment]" dir=in action=allow remoteip=[your ip] protocol=TCp localport=[port]`
- Delete rule:
  `netsh advfirewall firewall del rule name="[Comment]"`
- Disable Windows Firewall altogether:
  `netsh advfirewall set allprofiles state off`
