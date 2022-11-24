## ANSIBLE CONFIGURATION

### Configuration file.

* Certain settings in Ansible are adjustable via a configuration file (ansible.cfg). The stock configuration should be sufficient for most users, but there may be reasons you would want to change them. Paths where configuration file is searched are listed in reference documentation.

### Getting the latest configuration

* If installing Ansible from a package manager, the latest ansible.cfg file should be present in /etc/ansible, possibly as a .rpmnew file (or other) as appropriate in the case of updates. If you installed Ansible from pip or from source, you may want to create this file in order to override default settings in Ansible. An example file is available on GitHub. For more details and a full listing of available configurations go to configuration_settings. Starting with Ansible version 2.4, you can use the ansible-config command line utility to list your available options and inspect the current values. For in-depth details, see Ansible Configuration Settings.

### Environmental configuration

* Ansible also allows configuration of settings using environment variables. If these environment variables are set, they will override any setting loaded from the configuration file. You can get a full listing of available environment variables from Ansible Configuration Settings.

### Command line options

* Not all configuration options are present in the command line, just the ones deemed most useful or common. Settings in the command line will override those passed through the configuration file and the environment. The full list of options available is in ansible-playbook and ansible.

## ANSIBLE INVENTORY
### Inventory basics: formats, hosts, and groups
* You can create your inventory file in one of many formats, depending on the inventory plugins you have. The most common formats are INI and YAML. A basic INI /etc/ansible/hosts might look like this:

![1](https://user-images.githubusercontent.com/118405022/203676089-3e771ea4-6b19-449a-ac3e-23a6dbfe3bf7.JPG)

* The headings in brackets are group names, which are used in classifying hosts and deciding what hosts you are controlling at what times and for what purpose. Group names should follow the same guidelines as Creating valid variable names. Here’s that same basic inventory file in YAML format:

![2](https://user-images.githubusercontent.com/118405022/203676222-20e64ea6-051e-4877-935a-64be78905988.JPG)

### Default Groups
* Even if you do not define any groups in your inventory file, Ansible creates two default groups: all and ungrouped. The all group contains every host. The ungrouped group contains all hosts that don’t have another group aside from all. Every host will always belong to at least 2 groups (all and ungrouped or all and some other group). For example, in the basic inventory above, the host mail.example.com belongs to the all group and the ungrouped group; the host two.example.com belongs to the all group and the dbservers group. Though all and ungrouped are always present, they can be implicit and not appear in group listings like group_names

### Hosts in multiple groups
* You can (and probably will) put each host in more than one group. For example a production webserver in a datacenter in Atlanta might be included in groups called [prod] and [atlanta] and [webservers]. You can create groups that track:

    What - An application, stack or microservice (for example, database servers, web servers, and so on).

    Where - A datacenter or region, to talk to local DNS, storage, and so on (for example, east, west).

    When - The development stage, to avoid testing on production resources (for example, prod, test).
* Extending the previous YAML inventory to include what, when, and where would look like this:

![3](https://user-images.githubusercontent.com/118405022/203676613-d9126757-2abf-4935-91b1-4cbbb6d38992.JPG)

## AD HOC
### Why use ad hoc commands?

* ad hoc commands are great for tasks you repeat rarely. For example, if you want to power off all the machines in your lab for Christmas vacation, you could execute a quick one-liner in Ansible without writing a playbook. An ad hoc command looks like this:

      $ ansible [pattern] -m [module] -a "[module options]"

* The -a option accepts options either through the key=value syntax or a JSON string starting with { and ending with } for more complex option structure. You can learn more about patterns and modules on other pages.
Use cases for ad hoc tasks

* ad hoc tasks can be used to reboot servers, copy files, manage packages and users, and much more. You can use any Ansible module in an ad hoc task. ad hoc tasks, like playbooks, use a declarative model, calculating and executing the actions required to reach a specified final state. They achieve a form of idempotence by checking the current state before they begin and doing nothing unless the current state is different from the specified final state.
Rebooting servers

* The default module for the ansible command-line utility is the ansible.builtin.command module. You can use an ad hoc task to call the command module and reboot all web servers in Atlanta, 10 at a time. Before Ansible can do this, you must have all servers in Atlanta listed in a group called [atlanta] in your inventory, and you must have working SSH credentials for each machine in that group. To reboot all the servers in the [atlanta] group:

      $ ansible atlanta -a "/sbin/reboot"

* By default Ansible uses only 5 simultaneous processes. If you have more hosts than the value set for the fork count, Ansible will talk to them, but it will take a little longer. To reboot the [atlanta] servers with 10 parallel forks:

      $ ansible atlanta -a "/sbin/reboot" -f 10

* /usr/bin/ansible will default to running from your user account. To connect as a different user:

      $ ansible atlanta -a "/sbin/reboot" -f 10 -u username

* Rebooting probably requires privilege escalation. You can connect to the server as username and run the command as the root user by using the become keyword:

      $ ansible atlanta -a "/sbin/reboot" -f 10 -u username --become [--ask-become-pass]

* If you add --ask-become-pass or -K, Ansible prompts you for the password to use for privilege escalation (sudo/su/pfexec/doas/etc).

#### So far all our examples have used the default ‘command’ module. To use a different module, pass -m for module name. For example, to use the ansible.builtin.shell module:

      $ ansible raleigh -m ansible.builtin.shell -a 'echo $TERM'

* When running any command with the Ansible ad hoc CLI (as opposed to Playbooks), pay particular attention to shell quoting rules, so the local shell retains the variable and passes it to Ansible. For example, using double rather than single quotes in the above example would evaluate the variable on the box you were on.
### Managing files

* An ad hoc task can harness the power of Ansible and SCP to transfer many files to multiple machines in parallel. To transfer a file directly to all servers in the [atlanta] group:

      $ ansible atlanta -m ansible.builtin.copy -a "src=/etc/hosts dest=/tmp/hosts"

* If you plan to repeat a task like this, use the ansible.builtin.template module in a playbook.

* The ansible.builtin.file module allows changing ownership and permissions on files. These same options can be passed directly to the copy module as well:

      $ ansible webservers -m ansible.builtin.file -a "dest=/srv/foo/a.txt mode=600"
      $ ansible webservers -m ansible.builtin.file -a "dest=/srv/foo/b.txt mode=600 owner=mdehaan group=mdehaan"

* The file module can also create directories, similar to mkdir -p:

      $ ansible webservers -m ansible.builtin.file -a "dest=/path/to/c mode=755 owner=mdehaan group=mdehaan state=directory"

* As well as delete directories (recursively) and delete files:

      $ ansible webservers -m ansible.builtin.file -a "dest=/path/to/c state=absent"

### Managing packages

* You might also use an ad hoc task to install, update, or remove packages on managed nodes using a package management module such as yum. Package management modules support common functions to install, remove, and generally manage packages. Some specific functions for a package manager might not be present in the Ansible module since they are not part of general package management.

* To ensure a package is installed without updating it:

      $ ansible webservers -m ansible.builtin.yum -a "name=acme state=present"

* To ensure a specific version of a package is installed:

      $ ansible webservers -m ansible.builtin.yum -a "name=acme-1.5 state=present"

* To ensure a package is at the latest version:

      $ ansible webservers -m ansible.builtin.yum -a "name=acme state=latest"

* To ensure a package is not installed:

      $ ansible webservers -m ansible.builtin.yum -a "name=acme state=absent"

* Ansible has modules for managing packages under many platforms. If there is no module for your package manager, you can install packages using the command module or create a module for your package manager.
Managing users and groups

* You can create, manage, and remove user accounts on your managed nodes with ad hoc tasks:

      $ ansible all -m ansible.builtin.user -a "name=foo password=<crypted password here>"

      $ ansible all -m ansible.builtin.user -a "name=foo state=absent"

### See the ansible.builtin.user module documentation for details on all of the available options, including how to manipulate groups and group membership.
Managing services

* Ensure a service is started on all webservers:

      $ ansible webservers -m ansible.builtin.service -a "name=httpd state=started"

* Alternatively, restart a service on all webservers:

      $ ansible webservers -m ansible.builtin.service -a "name=httpd state=restarted"

* Ensure a service is stopped:

      $ ansible webservers -m ansible.builtin.service -a "name=httpd state=stopped"

### Gathering facts

* Facts represent discovered variables about a system. You can use facts to implement conditional execution of tasks but also just to get ad hoc information about your systems. To see all facts:

* $ ansible all -m ansible.builtin.setup

* You can also filter this output to display only certain facts, see the ansible.builtin.setup module documentation for details.
Patterns and ad-hoc commands

* See the patterns documentation for details on all of the available options, including how to limit using patterns in ad-hoc commands.

#### Now that you understand the basic elements of Ansible execution, you are ready to learn to automate repetitive tasks using Ansible Playbooks.
