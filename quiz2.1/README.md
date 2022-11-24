# How to create an Ansible Configuration
  - After installing the ansible on Alpine, type "ansible --version" to see the directory of the config command. The default directory of the ansible configuration is in /etc/ansible/ansible.cfg. If the ansible is installed using pip, the config file would be none, but you can type "ansible-config init --disabled > ansible.cfg" to generate a sample file.

# How to create an Ansible Inventory
  - Upon installation of ansible, you can check the ansible version by typing "ansible --version" to see the default location of the inventory. Ansible creates an inventory file which is usually located at /etc/ansible/host. To create an ansible inventory, create a new directory to put the inventory. After that you can use a text edtior like vim or nano to create the inventory. The common formats used in inventory are .ini and .yaml.

# How to create an Ad-hoc Ansible command with setup and shell module
  - 
