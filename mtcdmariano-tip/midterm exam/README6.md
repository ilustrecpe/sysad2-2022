---
- hosts: centos
  roles:
    - centos-elastic
    - centos-mtcdmariano
    - centos-lamp

- hosts: ubuntu
  roles:
    - ubuntu-elastic
    - ubuntu-nagios
    - ubuntu-nagios2
    - ubuntu-nagios3
    - ubuntu-mtcdmariano
    - ubuntu-lamp
