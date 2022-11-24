Create an Ansible playbook that does the following with an input of a config.yaml file

Role 1 (python):

1. Installs the latest python3 and pip3

2. use pip3 as default pip 

3. use python3 as default python 

Role 2 (Java)

1. Install Java open-jdk

Role 3 (Change motd)

1. Create Motd containing the text defined by a variable defined in config.yaml file and if there is no variable input the default motd is "Ansible Managed node by (your user name)"

Role 4 (Create user)

1. Create a user with a variable defined in config.yaml
