## Display Contents of file

- `type [file]`
  - `type *.txt` or `type [file1] [file2]`
- Display output one page at a time `more [file]`
- Searching for a string within a file: `type [file] | find /i "[string]"`
- Searching for regular expressions: `type [file] | findstr [regex]`

## Environment variables

- To see all environment variables set within a shell, run: `set`

## Dir Command

- To search for a file in file system, use:
`dir /b /s [directory]\[file]`

/s: recurese subdirectories
/b: bare form of output

-  Wildcards supported with **


