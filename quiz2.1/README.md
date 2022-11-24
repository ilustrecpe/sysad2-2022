## 1.How to create an Ansible Configuration.
- You can create an ansible configuration by the ansible-config command to list list your options and change the configuration of alpine as you see fit.
It also allows you to configure by the use of environment variables. . If these environment variables are set, they will override any setting loaded from 
the configuration file.

## 2.How to create an Ansible Inventory.
- To create an inventory, make sur eyou first have Playbook. Playbook is where you write you ansible code to automate tasks and it allows you to configure your inventory.
When creating an ansible inventory file it will be located in /etc/ansible/hosts. Then you'd need to creat group and subgroup of servers in your inventory file. By 
grouping and supgrouping, you can organize your hosts or nodes. Next would be to setup their aliases and variables, we alias them so it would be better fo ryou to indicate
which nodes is which and adding variables to them so it would be easier to find these nodes.

## 3.How to create an Ad-hoc Ansible command with setup and shell module.
-First to setup, the ansible controller or machine should be able to conect to the VMs using SSH.Then to specify which node to run the command to, use host-pattern to 
execute the command on specific nodes and the command called ansible-doc -l to see all the possible modules installed in your system, you can use this command to document
nodes or modules by name, their task, and what tasks are given to them.
