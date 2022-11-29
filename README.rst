
#######
Hands-on Prelim Exam
#######

Lorenz P. Laurenciano

CPE307 - CPE31S1A

Managing Enterprise Servers
 
================
Example Playbook
================



**Role 1 (python): dhcpd, **

.. code-block:: yaml

    - name: install the package, force upgrade
  apt: 
    name: python3
    state: latest
    
    - name: install the package, force reinstall to the latest version
  pip: 
    name: python3
    state: forcereinstall
    
**Role 2 bind9**

          
.. code-block:: yaml

    - name: Installing java
      apt:
        name: openjdk-8-jre
        update_cache: yes
 
 
 
**Role 3 , vsftpd**


.. code-block:: yaml

   ---

   - name: Role 3 (Change motd)
  vars:
   variable1: 'Ansible Managed node by @renzlaurennn'
  ansible.builtin.template:
    src: /root/sysad2-2022/roles/motd/files/motd.j2
    dest: /etc/motd
          
**Role 4, samba**


.. code-block:: yaml

    ---

    - name: Adding user
      vars:
        variable1: 'User_Lorenz'

      ansible.builtin.user:
        name: "{{ variable1 }}"
        
 
 **Role 4, httpd,**


.. code-block:: yaml

    ---

    - name: Adding user
      vars:
        variable1: 'User_Lorenz'

      ansible.builtin.user:
        name: "{{ variable1 }}"

**Role 4 maria**


.. code-block:: yaml

    ---

    - name: Adding user
      vars:
        variable1: 'User_Lorenz'

      ansible.builtin.user:
        name: "{{ variable1 }}"

