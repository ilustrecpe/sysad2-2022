[ubuntu]
192.168.1.5

[ubuntu:vars]
ansible_ssh_user=ubuntu-2010004
ansible_ssh_pass=123
 28  
2010004/quiz22/quiz22.yaml
@@ -0,0 +1,28 @@
---
- hosts: all
  become: yes
  tasks:
    - name: Install apache
      apt:
        name: apache2
        update_cache: yes

    - name: Install mysql-server
      apt:
        name: mysql-server
        update_cache: yes

    - name: Install PHP
      apt:
        name: php
        update_cache: yes

    - name: Install libapache
      apt:
        name: libapache2-mod-php
        update_cache: yes

    - name: Install php-mysql
      apt:
        name: php-mysql
        update_cache: yes
