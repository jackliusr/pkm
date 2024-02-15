- base image
	- `Nano Server` is an ultralight Windows offering for new application development.
		- docker pull mcr.microsoft.com/windows/nanoserver:ltsc2022
	- `Server Core` is medium in size and a good option for "lifting and shifting" Windows Server apps.
		- docker pull mcr.microsoft.com/windows/servercore:ltsc2022
	- `Windows` is the largest image and has full Windows API support for workloads.
		- docker pull mcr.microsoft.com/windows:ltsc2019
	- `Windows Server` is slightly smaller than the Windows image, has full Windows API support, and allows you to use more server features.
		- docker pull mcr.microsoft.com/windows/server:ltsc2022
- Isolation
	- Hyper-V: `--isolation=hyperv`
	  https://learn.microsoft.com/en-us/virtualization/windowscontainers/manage-containers/media/container-arch-hyperv.png
	- process: `--isolation=process`
		- ("ContainerAdministrator" on Windows Server Core and "ContainerUser" on Nano Server containers, by default)
		  ![A diagram showing a container full of applications being isolated from the OS and hardware.](https://learn.microsoft.com/en-us/virtualization/windowscontainers/manage-containers/media/container-arch-process.png)
		- What gets isolated
			- file system
			- registry
			- network ports
			- process and thread ID space
			- Object Manager namespace
- binding
	- https://learn.microsoft.com/en-us/virtualization/windowscontainers/manage-containers/persistent-storage
	- `docker run -v c:\ContainerData:c:\data:RO` for read-only access
	- `docker run -v c:\ContainerData:c:\data:RW` for read-write access
	- `docker run -v c:\ContainerData:c:\data` for read-write access (default)
	- docker run -v //c/Temp/prjs/:`/test` -it mcr.microsoft.com/windows/nanoserver:ltsc2022 cmd.exe
- [SMB Global Mapping](https://learn.microsoft.com/en-us/virtualization/windowscontainers/manage-containers/persistent-storage#smb-mounts): mount a SMB share on the host, then pass directories on that share into a container
- installation: Nano Server does not support MSI and yes, Server Core does
- NOTICE: pre-pull images
- [How do I get the application exit code from a Windows command line](https://stackoverflow.com/questions/334879/how-do-i-get-the-application-exit-code-from-a-windows-command-line)
	- ``` batch
	  start /wait something.exe
	  echo %errorlevel%
	  REM error code : -1073741515
	  ```
- [Trying to port application to docker nanoserver container. Running exe fails with exit code -1073741515 (Dependency missing)](https://stackoverflow.com/questions/63688377/trying-to-port-application-to-docker-nanoserver-container-running-exe-fails-wit)
	- https://stackoverflow.com/a/64112817
- `job object`: A job object allows groups of processes to be managed as a unit. Job objects are namable, securable, sharable objects that control attributes of the processes associated with them. Operations performed on a job object affect all processes associated with the job object