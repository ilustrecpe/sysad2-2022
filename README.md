
#######
Hands-on Prelim Exam
#######

Lorenz P. Laurenciano

CPE307 - CPE31S1A

Managing Enterprise Servers
 
================
Example Playbook
================


   ---
**Role 1 (python)**


   

    - name: install python3 the package
      apt:
        name: python3
        state: latest

    
    
  ---    
**Role 2**

  
  
    - name: Installing java
      apt:
        name: openjdk-8-jre
        update_cache: yes
 
 
 
 
---
**Role 3**

   

 
    - name: Role 3 (Change motd)
    vars:
     variable1: 'Ansible Managed node by @renzlaurennn'
    ansible.builtin.template:
      src: /root/sysad2-2022/roles/motd/files/motd.j2
      dest: /etc/motd
          

---
**Role 4**


    

    - name: Adding user
      vars:
        variable1: 'User_Lorenz'

      ansible.builtin.user:
        name: "{{ variable1 }}"
        
 
 
 
 ## SCREENSHOT
 <img width="1579" alt="Screen Shot 2022-12-01 at 5 44 11 AM" src="https://user-images.githubusercontent.com/42668363/204915459-9fb7b1cd-c50b-460b-8e6b-ecf94f3d7c93.png">
 <img width="1588" alt="Screen Shot 2022-12-01 at 5 43 54 AM" src="https://user-images.githubusercontent.com/42668363/204915515-c6bad2c1-ea89-4a48-b196-746e06cc78a3.png">

 

