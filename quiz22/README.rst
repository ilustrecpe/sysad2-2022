#######
Quiz 2.2: Ansible Playbooks
#######

Objective:

Transform this procedure_ as a playbook.

.. _procedure: https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04




================
Example Playbook
================



**Install Apache**

.. code-block:: yaml

   ---
   - hosts: all
     become: yes
     tasks:
        - name: Install apache
          apt:
            name: apache2
    
**Install MySQL Server**

          
.. code-block:: yaml

    - name: Install mysql-server
      apt:
        name: mysql-server
        update_cache: yes
 
 
 
**Install PHP**


.. code-block:: yaml


   - name: Install PHP
      apt:
        name: php
        update_cache: yes
          
**Install libapache**


.. code-block:: yaml


    - name: Install libapache
      apt:
        name: libapache2-mod-php
        update_cache: yes

**Install PHP MySQL**


.. code-block:: yaml


    - name: Install php-mysql
      apt:
        name: php-mysql
        update_cache: yes
