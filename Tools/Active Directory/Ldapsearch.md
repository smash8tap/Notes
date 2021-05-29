- Get domain name information
`ldapsearch -x -h $IP -s base namingcontexts`

- Get all subfolders of the base domain name obtained in previous step
`ldapsearch -x -h $IP -s sub -b "DC=htb,DC=local"`