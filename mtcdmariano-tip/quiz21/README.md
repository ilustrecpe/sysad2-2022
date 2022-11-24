1. How to create an Ansible Configuration
A configuration file in Ansible can be used to change some settings (ansible.cfg). Most users should be able to get by with the default settings, but there may be situations when you want to make changes. Reference documentation lists the paths that are checked for configuration files.
2. How to create an Ansible Inventory
-Creating a Custom Inventory File
-Organizing servers into groups and subgroups
-Setting up Host Aliases
-Setting up Host Variables
-Using Patterns to target execution of commands and Playbooks
How to create an Ad-hoc Ansible command with setup and shell module.
3. How to create an Ad-hoc Ansible command with setup and shell module.
$ ansible app -m file -a "path=/opt/oracle/binaries state=directory mode=0755" -i ansible_hosts -b – become-user=weblogic. mwivmapp01 | SUCCESS => { "gid": 1001, "size": 6, "uid": 1001. } mwivmapp02 | SUCCESS => { "gid": 1001,
