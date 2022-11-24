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
###### [webservers]
###### 203.0.113.111
###### 203.0.113.112
-
###### [dbservers]
###### 203.0.113.113
###### server_hostname
-
###### [development]
###### 203.0.113.111
###### 203.0.113.113
-
###### [production]
###### 203.0.113.112
###### server_hostname
------------------
### Step 3 — Setting Up Host Aliases
##### You can use aliases to name servers in a way that facilitates referencing those servers later, when running commands and playbooks.

##### To use an alias, include a variable named ansible_host after the alias name, containing the corresponding IP address or hostname of the server that should respond to that alias:
------------------
###### ~/ansible/inventory
------------------
### Step 4 — Setting Up Host Variables
##### It is possible to use the inventory file to set up variables that will change Ansible’s default behavior when connecting and executing commands on your nodes. This is in fact what we did in the previous step, when setting up host aliases. The ansible_host variable tells Ansible where to find the remote nodes, in case an alias is used to refer to that server.

##### Inventory variables can be set per host or per group. In addition to customizing Ansible’s default settings, these variables are also accessible from your playbooks, which enables further customization for individual hosts and groups.
------------------
###### server1 ansible_host=203.0.113.111 ansible_user=sammy
###### server2 ansible_host=203.0.113.112 ansible_user=sammy
###### server3 ansible_host=203.0.113.113 ansible_user=myuser
###### server4 ansible_host=server_hostname ansible_user=myuser
------------------
