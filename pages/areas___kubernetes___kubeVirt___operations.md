- Live Migration
	- ``` yaml
	  apiVersion: kubevirt.io/v1
	  kind: VirtualMachineInstanceMigration
	  metadata:
	    name: migration-job
	  spec:
	    vmiName: vmi-fedora
	  ```
	- ``` bash
	      virtctl migrate vmi-fedora
	      virtctl migration-cancel vmi-fedora
	  ```
	- migration strategy: pre-copy, post-copy, auto-converge
- hotplug network interface