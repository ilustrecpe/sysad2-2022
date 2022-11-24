## Good Day

### How to create an Ansible Configuration

##### The ansible-config utility allows users to see all the configuration settings available, their defaults, how to set them and where their current value comes from. If Ansible were to load ansible.cfg from a world-writable current working directory, it would create a serious security risk. Another user could place their own config file there, designed to make Ansible run malicious code both locally and remotely, possibly with elevated privileges. 

### How to create an Ansible Inventory.

##### Organizing servers into groups, after it add the subgroups Setting up Host Aliases. Then Setting up Host Variables, and Using Patterns to target execution of commands and Playbooks

### How to create an Ad-hoc Ansible command with setup and shell module.

##### ansible app -m file -a "path=/opt/oracle/binaries state=directory mode=0755" -i ansible_hosts -b – become-user=weblogic. mwivmapp01 | SUCCESS => { "gid": 1001, "size": 6, "uid": 1001. } mwivmapp02 | SUCCESS => { "gid": 1001,

