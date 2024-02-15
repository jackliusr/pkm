- [Comparing SSH Keys - RSA, DSA, ECDSA, or EdDSA?](https://goteleport.com/blog/comparing-ssh-keys/) **EdDSA**
- ed25519 | ed25519-sk
- [Enabling SFTP-only access on Linux](https://geraldonit.com/2018/05/02/enabling-sftp-only-access-on-linux/)
	- ``` bash
	  useradd <your sftp user> -s /sbin/nologin -m
	  passwd <your sftp user>
	  
	  sudo mkdir /var/sftp
	  sudo mkdir /var/sftp/myuser01
	  sudo chown -R root:root /var/sftp
	  chmod -R 755 /var/sftp
	  ```
	- /etc/ssh/sshd_config
	- ```
	  Match group ftp 
	       PermitTunnel no
	       AllowAgentForwarding no
	       AllowTcpForwarding no
	       X11Forwarding no
	       ForceCommand internal-sftp
	       ChrootDirectory /var/sftp/%u
	       PasswordAuthentication yes
	  
	  ```
	- issues:
		- client_loop: send disconnect: Broken pipe:  The OpenSSH SSH server's [ChrootDirectory](https://man.openbsd.org/sshd_config#ChrootDirectory) directive requires that the chroot directory and its parent directories be owned by root:
		- subsystem request failed on channel 0: might be caused by above issue