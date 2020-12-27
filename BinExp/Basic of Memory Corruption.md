## Genreal Tips
- A variables value is stored from a given memory location towards higher memory location
- Stack grows towards **lower** memory adress
## Push Instruction
push first decrements ESP by 4, then places its operand into the contents of the 32-bit location at address [ESP]

## Pop Instruction
It first moves the 4 bytes located at memory location [SP] into the specified register or memory location, and then increments SP by 4

## Load effective address
The lea instruction places the address specified by its second operand into the register specified by its first operand. Note, the contents of the memory location are not loaded, only the effective address is computed and placed into the register. This is useful for obtaining a pointer into a memory region.

## Examine (x in gdb)
- x/x <address>: prints the 4 byte content of the memory at location <address>
	![[Pasted image 20201111184754.png]]
- x/2x <adress> : prints 2 4-byte contents of the memory at location <address>
	![[Pasted image 20201111184858.png]]
