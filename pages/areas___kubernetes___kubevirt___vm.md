- Instance types and preferences
	- VirtualMachineInstancetype 
	  ``` bash
	  virtctl create instancetype --cpu 2 --memory 256Mi  #cluster
	  virtctl create instancetype --cpu 2 --memory 256Mi --namespace my-namespace
	  ```
	- VirtualMachineClusterInstancetype
	- VirtualMachine: 
	  ``` batch
	  virtctl create vm
	  ```
	- VirtualMachinePreference 
	  ``` bash
	  virtctl create preference -h
	  ```
- run strategy: Always, RerunOnFailure, Manual, Halted
- Virtual hardware
- vsock: VM Sockets (vsock) is a fast and efficient guest-host communication mechanism.
-