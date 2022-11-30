
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
      
    
      
<img width="1041" alt="Screen Shot 2022-12-01 at 4 37 58 AM" src="https://user-images.githubusercontent.com/42668363/204903534-f30ac23f-b073-487f-b22f-2cbba8721927.png">
