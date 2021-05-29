- Read a reg key:
  `reg query [keyName]`
- change a reg key:
  `reg add [keyname] /v [valuename] /t [type] /d [data]`
- Export settings to a reg file:
  `reg export [keyname] [filename.reg]`
- Import settings from a reg file:
  `reg import [filename.reg]`
- **Do any of these remotely by prepending \\[MachineName] before [KeyName]**
  - Requires admin-level SMB session
