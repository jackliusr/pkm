- This command has to be run under the root user. #card
  card-last-interval:: 36.02
  card-repeats:: 4
  card-ease-factor:: 2.9
  card-next-schedule:: 2024-04-06T13:42:52.080Z
  card-last-reviewed:: 2024-03-01T13:42:52.080Z
  card-last-score:: 5
	- /etc/ansible/ansible.cfg
	  ``` ini
	  [defaults]
	  host_key_checking = False
	  
	  ; this section might not be needed
	  [privilege_escalation] 
	  become=True 
	  become_method=sudo 
	  become_user=root 
	  become_ask_pass=False
	  ```
	- inventory
	  
	  ``` 
	  stapp01 ansible_host=172.16.238.10 ansible_ssh_pass=Ir0nM@n ansible_user=tony
	  stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@ ansible_user=steve
	  stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n ansible_user=banner
	  ```
	- playbook
	  
	  ``` yaml
	  ---
	  - name: Update web servers
	    hosts: all
	    become: yes
	    become_method: sudo
	  
	    tasks:
	    - name: Install zip
	      yum:
	        name: zip
	        state: present
	  ```
	- apache
	  
	  ``` yaml
	  ---
	  - name: Update web servers
	    hosts: stapp01,stapp02,stapp03
	    become: yes
	    become_method: sudo 
	  
	  
	    tasks:
	    - name: install httpd
	      yum:
	        name: httpd
	        state: present
	    - name: Just force systemd to reread configs (2.4 and above)
	      ansible.builtin.systemd_service:
	        daemon_reload: true      
	    - name: Enable service httpd and ensure it is not masked
	      ansible.builtin.systemd_service:
	        name: httpd
	        enabled: true
	        state: started
	    - name: Change //var/www/html/index.html
	      ansible.builtin.file:
	        path: /var/www/html/index.html
	        owner: apache
	        group: apache
	        mode: '0755'
	        state: touch
	      
	    - name: block
	      blockinfile:
	         path: /var/www/html/index.html
	         block: |
	             Welcome to XfusionCorp!
	  
	             This is Nautilus sample file, created using Ansible!
	  
	             Please do not modify this file manually!
	  ```