- List local users:
  `net user`
- List Local groups:
  `net localgroup`
- List members of local admin group :
  `net localgroup adminstrators`
- Add a user:
  `net user [logon_name] [password] /add`
- Put the user in the local admin group:
  `net localgroup adminstrators [logon_name] /add`
- Remove a user from group:
  `nte localgroup [greoup] [logon_name] /del`
- To delete an account:
  `net user [logon_name] /del`
