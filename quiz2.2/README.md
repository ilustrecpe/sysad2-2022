
### DIRECTORY CONTENT ###
A "LAMP" stack is a collection of open source applications that are commonly deployed together to allow a server to run dynamic websites and PHP-coded web applications. This word is an abbreviation for the Apache web server and the Linux operating system. PHP processes dynamic content, and a MySQL database stores the site's data.

ANSIBLE.CFG
-Contains the ansible configuration, passed here is the inventory file to specify managed nodes
and HOST_KEY_CHECKING=False since SSH credentials were used

INVENTORY
-Contains the managed node's IP address and SSH credentials  

QUIZ 2.2.YAML
-Contains the playbook command for package automation

### ANSIBLE AUTOMATION FOR INSTALLING PACKAGES ###

List of Packages Installed:
-Apache2
-mysql-server
-PHP
-libapache2-mod-php
-php-mysql

