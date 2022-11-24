<br>1 - How to create an Ansible Configuration.</br>
<li> Ansible is a great alternative to these options because it offers an architecture that doesn’t require special software to be installed on nodes, 
using SSH to execute the automation tasks and YAML files to define provisioning details. As such, in order to completely configure Ansible we should of course
install Ansible itself, setting up the inventory files, testing our connection, and lastly, running ad-hoc commands.</li>
<br>2 - How to create an Ansible Inventory.</br>
<li>Ansible uses an inventory file to keep track of which hosts are part of your infrastructure, and how to reach them for running commands and playbooks.
As such, in order to completely create an Ansible Inventory, we should first Create a Custom File, Organizing Servers Into Groups and Subgroups,
Setting Up Host Aliases, Setting Up Host Variables, Using Patterns to Target Execution of Commands and Playbooks.</li>
<br>3 - How to create an Ad-hoc Ansible command with setup and shell module.</br>
<li>An ad hoc command is a way of executing a single Ansible task quickly, one that you do not need to save to run again later.
In order to set up an ad-hoc in ansible, we should run the host-pattern argument, the -list-hosts, and the i code.</li>
