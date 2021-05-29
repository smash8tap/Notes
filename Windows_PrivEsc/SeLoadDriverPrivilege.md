# Files Needed
- Download `EOPLOADDRIVER` from [here](https://github.com/TarlogicSecurity/EoPLoadDriver/)
- Download Capcom.sys from [here](https://github.com/FuzzySecurity/Capcom-Rootkit/raw/master/Driver/Capcom.sys)
- Utility to exploit capcom.sys from [here](https://github.com/tandasat/ExploitCapcom.git)

# Compiling binaries
- Create a new project in Visual Studio 2019
![[Pasted image 20210512170801.png]]
- Get the source code from `eoploaddriver.cpp`
- Buid the soultion (we might have to remove a header)
- Do the same thing with `ExploitCamcom`
- Transfer all the three files back to hacko 
![[Pasted image 20210512174117.png]]
- Also upload a reverse shell binary
![[Pasted image 20210512174410.png]]

- Creating a new reg key with driver image path
`.\LoadDriver.exe System\CurrentControlSet\NewService C:\Users\svc-print\Document\capcom.sys`
![[Pasted image 20210512174750.png]]

- Run `.\ExploitCapcom.exe <reverse shell binary >` to get a rev shell as system
