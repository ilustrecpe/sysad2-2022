# How to create an Ansible Inventory.
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
