

#######
Hands-on Activity 6: Install, configure, and manage enterprise services via Ansible 
#######

================
Objectives
================


Create a workflow that installs, configure, and manages enterprise services via Ansible being Infrastructure as code tool.


================
Tux and sysstat
================


the ``tux`` and ``sysstat`` that are included in configuration is linux utilities packages.



================
Command to run the playbook main.yml
================

``$ ansible-playbook -u tux -b main.yml``

================
Example Playbook
================



**All Roles: Installing several packages in one playbook main.yml


.. code-block:: yaml

    ---
    - hosts: all
     tasks:
      - name: Package installation
        dnf:
          name:
            - sysstat
            - httpd
            - mariadb-server
            - vsftpd
            - samba
          state: latest
