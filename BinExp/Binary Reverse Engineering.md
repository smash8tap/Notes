## Basic Structure of an assembly program

![[Pasted image 20201225212808.png]]

## File Identification

- `file <executable>` command looks at the metadata of the file to determine what file type it is
![[Pasted image 20201225213200.png]]
	-	`statically` or `dynamically linked`, which refers to how the binary finds various symbols. `Dynamically linked` means the shared objects referenced for functions like `C` need to be present on the box you are running the executable on, otherwise the executable will fail
	- `stripped` whether the binary has had all of its strings, function names, debugging information, and other such important information taken away

## Readelf

`Readelf` provides information on `ELF` executables. Using `readelf -a <executable>` will display:

-   File headers
-   Program headers
-   Section headers
-   Symbols
-   Relocations (if present)
-   Dynamic sections (if present)
-   Version sections (if present)
-   Architecture-specific information

**Section Headers **
-   `.text` – Stores the executable code (defined by the program above)
-   `.data` – Stores the initialised variables (defined by the program above)
-   `.symtab` – An object file's symbol table which holds information needed to locate and relocate a program's symbolic definitions and symbolic references
-   `.strtab` – String table sections hold null-terminated character sequences, commonly called strings
-   `.shstrtab` – Holds section names

## Section Information
![[Pasted image 20201225214030.png]]
- `Type` – Specifies the type of section
	- `NULL` – An inactive header
	-   `PROGBITS` – Sections defined by the program itself (programmable bits)
	- `SYMTAB` – Identifies sections that are symbol tables. With enough of these, the binary will be statically linked, not dynamically.
- `Addr`- The  starting address of the section as if it was in running memory (RAM). (Notice the `.text` `Addr` is the same as the `Entry Point Address` of the executable)
	- `00000000` – The section will never get loaded into RAM
- `off` - The offset within the executable from the starting point of the file `0`. Notice the final two hexadecimal characters for the `.data` and `.text` section are the same as the last two for the `Addr` – `00` and `00`.
- `Size` – The size of the sections referenced
- `ES` – Some sections hold a table of fixed-size entries, such as a symbol table. For such a section, this member gives the size in bytes of each entry.
- `flg` – Flags which show the attributes of the section, whether it is executable, allocable, writeable, etc.
- `Lk` – Whether the section links to another section; this executable has the value `4` meaning it links to the section `.strtab`
- `Inf` – One greater than the symbol table index of the last local symbol, binding to `STB_LOCAL` (to keep the symbols inside the `.symtab` section only visible inside this file)
- `Al` – Section alignment: if there are certain size values inside various sections, the alignment may be required to be a certain value
	-   `0` or `1` means there are no alignment requirements