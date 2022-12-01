


# Hands-on Activity 6: Install, configure, and manage enterprise services via Ansible 



### Objectives



Create a workflow that installs, configure, and manages enterprise services via Ansible being Infrastructure as code tool.

---

### Tux and sysstat


the ``tux`` and ``sysstat`` that are included in configuration is linux utilities packages.


---

### Command to execute the playbook activity-6.yml

``$ ansible-playbook -u tux -b activity-6.yml``


### Example Playbook



**All Roles: Installing several packages in one playbook activity-6.yml**



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
          
          
          
<img width="1719" alt="Screen Shot 2022-12-01 at 6 08 57 AM" src="https://user-images.githubusercontent.com/42668363/204919292-53a4882b-501e-4c75-ae2b-cafbf1a27cce.png">


