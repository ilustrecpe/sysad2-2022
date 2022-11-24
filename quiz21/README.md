# How to create an Ansible Inventory
### Step 1 — Creating a Custom Inventory File
##### Upon installation, Ansible creates an inventory file that is typically located at /etc/ansible/hosts. This is the default location used by Ansible when a custom inventory file is not provided with the -i option, during a playbook or command execution.

##### Access your home folder and create a new directory to hold your Ansible files:

------------------
###### cd ~
###### mkdir ansible
------------------

##### Move to that directory and open a new inventory file using your text editor of choice. Here, we’ll use nano:

------------------
###### cd ansible
###### nano inventory
------------------

##### A list of your nodes, with one server per line, is enough for setting up a functional inventory file. Hostnames and IP addresses are interchangeable:
------------------
###### 203.0.113.111
###### 203.0.113.112
###### 203.0.113.113
###### server_hostname
------------------

##### Once you have an inventory file set up, you can use the ansible-inventory command to validate and obtain information about your Ansible inventory:
------------------
###### ansible-inventory -i inventory --list
------------------

##### Running Commands and Playbooks with Custom Inventories
##### To run Ansible commands with a custom inventory file, use the -i option as follows:
------------------
###### ansible all -i inventory -m ping
------------------
##### This would execute the ping module on all hosts listed in your custom inventory file. Similarly, this is how you execute Ansible playbooks with a custom inventory file:
------------------
###### ansible-playbook -i inventory playbook.yml
------------------


### Step 2 — Organizing Servers Into Groups and Subgroups
##### A host can be part of multiple groups. The following inventory file in INI format demonstrates a setup with four groups: webservers, dbservers, development, and production. You’ll notice that the servers are grouped by two different qualities: their purpose (web and database), and how they’re being used (development and production).
------------------
|#####[webservers]
203.0.113.111
203.0.113.112
|fgdfg
[dbservers]
203.0.113.113
server_hostname

[development]
203.0.113.111
203.0.113.113

[production]
203.0.113.112
server_hostname
