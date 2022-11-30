
# Quiz 3.1: Managed Information Systems Services

## Objectives

Create a playbook that installs an vsftpd server.

### vsftpd playbook

``` 
---
- hosts: all
  become: true
  tasks:
    - name: Installing vsftpd
      apt:
         name: vsftpd
         update_cache: yes

    - name: booting vsftpd
      ansible.builtin.command: systemctl enable vsftpd

    - name: launching vsftpd
      ansible.builtin.command: systemctl start vsftpd
      
      
