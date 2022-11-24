
### How to create an Ansible Configuration.

#### First, make sure you have Git, Vagrant, and VirtualBox installed. Next, create a Vagrant file that has an Ubuntu virtual machine. Then run your Ansible playbook—this will install and configure everything. Then you can deploy your application. Remember that some of the components have to be downloaded, so this may add the time the first time you deploy.

### How to create an Ansible Inventory
#### The simplest inventory is a single file with a list of hosts and groups. The default location for this file is /etc/ansible/hosts. You can specify a different inventory file at the command line using the -i <path> option or in configuration using inventory.
### Step 1 — Creating a Custom Inventory File. ...
### Step 2 — Organizing Servers Into Groups and Subgroups. ...
### Step 3 — Setting Up Host Aliases. ...
### Step 4 — Setting Up Host Variables. ...
###Step 5 — Using Patterns to Target Execution of Commands and Playbooks.

### How to create an Ad-hoc Ansible command with setup and shell module.
#### Ad hoc commands are commands which can be run individually to perform quick functions. These commands need not be performed later.For example, you have to reboot all your company servers. For this, you will run the Adhoc commands from ‘/usr/bin/ansible’.These ad-hoc commands are not used for configuration management and deployment, because these commands are of one time usage.ansible-playbook is used for configuration management and deployment.
