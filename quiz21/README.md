# 1. How to create an Ansible Configuration

### Ansible Configuration Settings

Ansible supports several sources for configuring its behavior, including an ini file named |ansible.cfg|, environment variables, command-line options, playbook keywords, and variables. 

The |ansible-config utility| allows users to see all the configuration settings available, their defaults, how to set them and where their current value comes from. See ansible-config for more information.

### The configuration file

Changes can be made and used in a configuration file which will be searched for in the following order:

    ANSIBLE_CONFIG (environment variable if set)

    ansible.cfg (in the current directory)

    ~/.ansible.cfg (in the home directory)

    /etc/ansible/ansible.cfg

Ansible will process the above list and use the first file found, all others are ignored.

### Generating a sample ansible.cfg file

You can generate a fully commented-out example ansible.cfg file, for example:

    $ ansible-config init --disabled > ansible.cfg
    
You can also have a more complete file that includes existing plugins:

    $ ansible-config init --disabled -t all > ansible.cfg

You can use these as starting points to create your own ansible.cfg file.

----------

# 2. How to create an Ansible Inventory
### Step 1 — Creating a Custom Inventory File
Upon installation, Ansible creates an inventory file that is typically located at /etc/ansible/hosts. This is the default location used by Ansible when a custom inventory file is not provided with the -i option, during a playbook or command execution.

Access your home folder and create a new directory to hold your Ansible files:

    cd ~
    mkdir ansible


Move to that directory and open a new inventory file using your text editor of choice. Here, we’ll use nano:

    cd ansible
    nano inventory

A list of your nodes, with one server per line, is enough for setting up a functional inventory file. Hostnames and IP addresses are interchangeable:

    203.0.113.111
    203.0.113.112
    203.0.113.113
    server_hostname


Once you have an inventory file set up, you can use the ansible-inventory command to validate and obtain information about your Ansible inventory:

    ansible-inventory -i inventory --list

### Running Commands and Playbooks with Custom Inventories
To run Ansible commands with a custom inventory file, use the -i option as follows:

    ansible all -i inventory -m ping

This would execute the ping module on all hosts listed in your custom inventory file. Similarly, this is how you execute Ansible playbooks with a custom inventory file:

    ansible-playbook -i inventory playbook.yml


### Step 2 — Organizing Servers Into Groups and Subgroups
A host can be part of multiple groups. The following inventory file in INI format demonstrates a setup with four groups: webservers, dbservers, development, and production. You’ll notice that the servers are grouped by two different qualities: their purpose (web and database), and how they’re being used (development and production).

    [webservers]
    203.0.113.111
    203.0.113.112
    
    [dbservers]
    203.0.113.113
    server_hostname
    
    [development]
    203.0.113.111
    203.0.113.113
    
    [production]
    203.0.113.112
    server_hostname

### Step 3 — Setting Up Host Aliases
You can use aliases to name servers in a way that facilitates referencing those servers later, when running commands and playbooks.

To use an alias, include a variable named ansible_host after the alias name, containing the corresponding IP address or hostname of the server that should respond to that alias:

    ~/ansible/inventory

### Step 4 — Setting Up Host Variables
It is possible to use the inventory file to set up variables that will change Ansible’s default behavior when connecting and executing commands on your nodes. This is in fact what we did in the previous step, when setting up host aliases. The ansible_host variable tells Ansible where to find the remote nodes, in case an alias is used to refer to that server.

Inventory variables can be set per host or per group. In addition to customizing Ansible’s default settings, these variables are also accessible from your playbooks, which enables further customization for individual hosts and groups.

    server1 ansible_host=203.0.113.111 ansible_user=sammy
    server2 ansible_host=203.0.113.112 ansible_user=sammy
    server3 ansible_host=203.0.113.113 ansible_user=myuser
    server4 ansible_host=server_hostname ansible_user=myuser
    
You could also create a group to aggregate the hosts with similar settings, and then set up their variables at the group level:

    [group_a]
    server1 ansible_host=203.0.113.111 
    server2 ansible_host=203.0.113.112
    
    [group_b]
    server3 ansible_host=203.0.113.113 
    server4 ansible_host=server_hostname
    
    [group_a:vars]
    ansible_user=sammy
    
    [group_b:vars]
    ansible_user=myuser
    
### Step 5 — Using Patterns to Target Execution of Commands and Playbooks
When executing commands and playbooks with Ansible, you must provide a target. Patterns allow you to target specific hosts, groups, or subgroups in your inventory file. They’re very flexible, supporting regular expressions and wildcards.

    [webservers]
    203.0.113.111
    203.0.113.112
    
    [dbservers]
    203.0.113.113
    server_hostname
    
    [development]
    203.0.113.111
    203.0.113.113

    [production]
    203.0.113.112
    server_hostname
  
 ----------
 
# 3. How to create an Ad-hoc Ansible command with setup and shell module
An Ansible ad hoc command uses the /usr/bin/ansible command-line tool to automate a single task on one or more managed nodes. ad hoc commands are quick and easy, but they are not reusable. So why learn about ad hoc commands? ad hoc commands demonstrate the simplicity and power of Ansible. The concepts you learn here will port over directly to the playbook language.

    $ ansible [pattern] -m [module] -a "[module options]"
    
The |-a| option accepts options either through the key=value syntax or a JSON string starting with { and ending with } for more complex option structure. You can learn more about patterns and modules on other pages.

### Use cases for ad hoc tasks
ad hoc tasks can be used to reboot servers, copy files, manage packages and users, and much more. You can use any Ansible module in an ad hoc task. ad hoc tasks, like playbooks, use a declarative model, calculating and executing the actions required to reach a specified final state. They achieve a form of idempotence by checking the current state before they begin and doing nothing unless the current state is different from the specified final state.

### Rebooting servers
The default module for the ansible command-line utility is the ansible.builtin.command module. You can use an ad hoc task to call the command module and reboot all web servers in Atlanta, 10 at a time. Before Ansible can do this, you must have all servers in Atlanta listed in a group called [atlanta] in your inventory, and you must have working SSH credentials for each machine in that group. To reboot all the servers in the [atlanta] group:

    $ ansible atlanta -a "/sbin/reboot"
    
By default Ansible uses only 5 simultaneous processes. If you have more hosts than the value set for the fork count, Ansible will talk to them, but it will take a little longer. To reboot the [atlanta] servers with 10 parallel forks:

    $ ansible atlanta -a "/sbin/reboot" -f 10
    
/usr/bin/ansible will default to running from your user account. To connect as a different user:

    $ ansible atlanta -a "/sbin/reboot" -f 10 -u username
    
Rebooting probably requires privilege escalation. You can connect to the server as username and run the command as the root user by using the become keyword:

    $ ansible atlanta -a "/sbin/reboot" -f 10 -u username --become [--ask-become-pass]
    
If you add --ask-become-pass or -K, Ansible prompts you for the password to use for privilege escalation (sudo/su/pfexec/doas/etc).


### Managing files
An ad hoc task can harness the power of Ansible and SCP to transfer many files to multiple machines in parallel. To transfer a file directly to all servers in the [atlanta] group:

    $ ansible atlanta -m ansible.builtin.copy -a "src=/etc/hosts dest=/tmp/hosts"

If you plan to repeat a task like this, use the ansible.builtin.template module in a playbook. The ansible.builtin.file module allows changing ownership and permissions on files. These same options can be passed directly to the copy module as well:

    $ ansible webservers -m ansible.builtin.file -a "dest=/srv/foo/a.txt mode=600"
    $ ansible webservers -m ansible.builtin.file -a "dest=/srv/foo/b.txt mode=600 owner=mdehaan group=mdehaan"
    
The file module can also create directories, similar to mkdir -p:

    $ ansible webservers -m ansible.builtin.file -a "dest=/path/to/c mode=755 owner=mdehaan group=mdehaan state=directory"
    
As well as delete directories (recursively) and delete files:

    $ ansible webservers -m ansible.builtin.file -a "dest=/path/to/c state=absent"
    
### Managing packages
You might also use an ad hoc task to install, update, or remove packages on managed nodes using a package management module such as yum. Package management modules support common functions to install, remove, and generally manage packages. Some specific functions for a package manager might not be present in the Ansible module since they are not part of general package management.

To ensure a package is installed without updating it:

    $ ansible webservers -m ansible.builtin.yum -a "name=acme state=present"
    
To ensure a specific version of a package is installed:

    $ ansible webservers -m ansible.builtin.yum -a "name=acme-1.5 state=present"
    
To ensure a package is at the latest version:

    $ ansible webservers -m ansible.builtin.yum -a "name=acme state=latest"
    
To ensure a package is not installed:

    $ ansible webservers -m ansible.builtin.yum -a "name=acme state=absent"
    
Ansible has modules for managing packages under many platforms. If there is no module for your package manager, you can install packages using the command module or create a module for your package manager.

### Managing users and groups
You can create, manage, and remove user accounts on your managed nodes with ad hoc tasks:

    $ ansible all -m ansible.builtin.user -a "name=foo password=<crypted password here>"
    $ ansible all -m ansible.builtin.user -a "name=foo state=absent"
    
See the ansible.builtin.user module documentation for details on all of the available options, including how to manipulate groups and group membership.

### Managing services
Ensure a service is started on all webservers:

    $ ansible webservers -m ansible.builtin.service -a "name=httpd state=started"
    
Alternatively, restart a service on all webservers:

    $ ansible webservers -m ansible.builtin.service -a "name=httpd state=restarted"
    
Ensure a service is stopped:

    $ ansible webservers -m ansible.builtin.service -a "name=httpd state=stopped"
    
### Gathering facts
Facts represent discovered variables about a system. You can use facts to implement conditional execution of tasks but also just to get ad hoc information about your systems. To see all facts:

    $ ansible all -m ansible.builtin.setup
