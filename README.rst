

#######
Hands-on Activity 6: Install, configure, and manage enterprise services via Ansible 
#######

================
Objectives
================


Create a workflow that installs, configure, and manages enterprise services via Ansible being Infrastructure as code tool.



================
Example Playbook
================



**Role 1 (python): pip3 && python3 force unistall to reinstall to latest**

.. code-block:: yaml

    - name: install the package, force upgrade
  apt: 
    name: python3
    state: latest
    
    - name: install the package, force reinstall to the latest version
  pip: 
    name: python3
    state: forcereinstall
    
**Role 2 (Java): install open-jdk**

          
.. code-block:: yaml

    - name: Installing java
      apt:
        name: openjdk-8-jre
        update_cache: yes
 
 
 
**Role 3 (change motd): change default motd to Ansible Managed node by @renzlaurennn**


.. code-block:: yaml

   ---

   - name: Role 3 (Change motd)
  vars:
   variable1: 'Ansible Managed node by @renzlaurennn'
  ansible.builtin.template:
    src: /root/sysad2-2022/roles/motd/files/motd.j2
    dest: /etc/motd
          
**Role 4 (create_user): create a user with a variable defined in config.yaml**


.. code-block:: yaml

    ---

    - name: Adding user
      vars:
        variable1: 'User_Lorenz'

      ansible.builtin.user:
        name: "{{ variable1 }}"
