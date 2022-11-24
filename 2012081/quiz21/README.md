# Quiz 2.1

### How to create an Ansible Configuration
Ansible supports several sources for configuring its behavior, including an ini file named ansible.cfg, environment variables, command-line options, playbook keywords, and variables. See Controlling how Ansible behaves: precedence rules for details on the relative precedence of each source. The ansible-config utility allows users to see all the configuration settings available, their defaults, how to set them and where their current value comes from. See ansible-config for more information. You can generate a fully commented-out example ansible.cfg file, for example:

$ ansible-config init --disabled > ansible.cfg

You can also have a more complete file that includes existing plugins:

$ ansible-config init --disabled -t all > ansible.cfg


### How to create an Ansible Inventory.
Ansible automates tasks on managed nodes or “hosts” in your infrastructure, using a list or group of lists known as inventory. You can pass host names at the command line, but most Ansible users create inventory files. Your inventory defines the managed nodes you automate, with groups so you can run automation tasks on multiple hosts at the same time. Once your inventory is defined, you use patterns to select the hosts or groups you want Ansible to run against. The simplest inventory is a single file with a list of hosts and groups. The default location for this file is /etc/ansible/hosts. You can specify a different inventory file at the command line using the -i <path> option or in configuration using inventory.

### How to create an Ad-hoc Ansible command with setup and shell module.
ad hoc commands are great for tasks you repeat rarely. For example, if you want to power off all the machines in your lab for Christmas vacation, you could execute a quick one-liner in Ansible without writing a playbook. An ad hoc command looks like this:

$ ansible [pattern] -m [module] -a "[module options]"

The -a option accepts options either through the key=value syntax or a JSON string starting with { and ending with } for more complex option structure. You can learn more about patterns and modules on other pages.
