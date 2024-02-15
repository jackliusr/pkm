- wsf.conf
	- %UserProfile%\.wslconfig vs /etc/wsl.conf
	- ``` ini
	  
	  [boot]
	  systemd=true
	  command = /bin/bash -c 'chown -v root:kvm /dev/kvm && chmod 660 /dev/kvm'
	  nestedVirtualization=true
	  
	  [wsl2]
	  kernelCommandLine = cgroup_no_v1=all
	  
	  ```