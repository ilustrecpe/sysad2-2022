# How to create an Ansible Configuration

##### Ansible Configuration Settings

Ansible supports several sources for configuring its behavior, including an ini file named ansible.cfg, environment variables, command-line options, playbook keywords, and variables. See Controlling how Ansible behaves: precedence rules for details on the relative precedence of each source.

The ansible-config utility allows users to see all the configuration settings available, their defaults, how to set them and where their current value comes from. See ansible-config for more information.

##### The configuration file

Changes can be made and used in a configuration file which will be searched for in the following order:

    ANSIBLE_CONFIG (environment variable if set)

    ansible.cfg (in the current directory)

    ~/.ansible.cfg (in the home directory)

    /etc/ansible/ansible.cfg

Ansible will process the above list and use the first file found, all others are ignored.

##### Generating a sample ansible.cfg file

You can generate a fully commented-out example ansible.cfg file, for example:

    $ ansible-config init --disabled > ansible.cfg

You can also have a more complete file that includes existing plugins:

    $ ansible-config init --disabled -t all > ansible.cfg

You can use these as starting points to create your own ansible.cfg file.

Click here for more: [Reference Link](https://docs.ansible.com/ansible/latest/reference_appendices/config.html)

# How to create an Ansible Inventory

##### Inventory basics: formats, hosts, and groups

You can create your inventory file in one of many formats, depending on the inventory plugins you have. The most common formats are INI and YAML. A basic INI /etc/ansible/hosts might look like this:

Sample Format:

    mail.example.com

      [webservers]

        foo.example.com

        bar.example.com

      [dbservers]

        one.example.com

        two.example.com

        three.example.com

The headings in brackets are group names, which are used in classifying hosts and deciding what hosts you are controlling at what times and for what purpose. Group names should follow the same guidelines as Creating valid variable names.

Here’s that same basic inventory file in YAML format:

Sample Format:

    all:

      hosts:

        mail.example.com:

    children:

      webservers:

        hosts:

          foo.example.com:

          bar.example.com:

      dbservers:

        hosts:

          one.example.com:

          two.example.com:

          three.example.com:

Click here for more: [Reference Link](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)

# How to create an Ad-hoc Ansible command with setup and shell module

ad hoc commands are great for tasks you repeat rarely. For example, if you want to power off all the machines in your lab for Christmas vacation, you could execute a quick one-liner in Ansible without writing a playbook. An ad hoc command looks like this:

    $ ansible [pattern] -m [module] -a "[module options]"

The -a option accepts options either through the key=value syntax or a JSON string starting with { and ending with } for more complex option structure. You can learn more about patterns and modules on other pages.

##### Use cases for ad hoc tasks

ad hoc tasks can be used to reboot servers, copy files, manage packages and users, and much more. You can use any Ansible module in an ad hoc task. ad hoc tasks, like playbooks, use a declarative model, calculating and executing the actions required to reach a specified final state. They achieve a form of idempotence by checking the current state before they begin and doing nothing unless the current state is different from the specified final state.

##### Rebooting servers

The default module for the ansible command-line utility is the ansible.builtin.command module. You can use an ad hoc task to call the command module and reboot all web servers in Atlanta, 10 at a time. Before Ansible can do this, you must have all servers in Atlanta listed in a group called [atlanta] in your inventory, and you must have working SSH credentials for each machine in that group. To reboot all the servers in the [atlanta] group:

    $ ansible atlanta -a "/sbin/reboot"

By default Ansible uses only 5 simultaneous processes. If you have more hosts than the value set for the fork count, Ansible will talk to them, but it will take a little longer. To reboot the [atlanta] servers with 10 parallel forks:

    $ ansible atlanta -a "/sbin/reboot" -f 10

/usr/bin/ansible will default to running from your user account. To connect as a different user:

    $ ansible atlanta -a "/sbin/reboot" -f 10 -u username

Rebooting probably requires privilege escalation. You can connect to the server as username and run the command as the root user by using the become keyword:

    $ ansible atlanta -a "/sbin/reboot" -f 10 -u username --become [--ask-become-pass]

If you add --ask-become-pass or -K, Ansible prompts you for the password to use for privilege escalation (sudo/su/pfexec/doas/etc).

Click here for more: [Reference Link](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html)
