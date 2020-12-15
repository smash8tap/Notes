- **Ghost Writing**: Look for xor of register with itself in an assembly and just add push and pop instruction before that, Because that register is going to be zero, eg

```asm
.
.
.

xor eax, eax
.
.
.

```

we can add as many pust eax and pop eax instruction and that would bypass endpoint security
- **Lolbins**
-