
# Quiz 2.2: Ansible Playbooks


### Objective:

Transform this [procedure](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04) as a playbook 


### Example Playbook


**Install Apache**
```

   ---
   - hosts: all
     become: yes
     tasks:
        - name: Install apache
          apt:
            name: apache2
```

**Install MySQL Server**

```

    - name: Install mysql-server
      apt:
        name: mysql-server
        update_cache: yes
 
 
**Install PHP**


```
   - name: Install PHP
      apt:
        name: php
        update_cache: yes
          


```
    - name: Install libapache
      apt:
        name: libapache2-mod-php
        update_cache: yes
```


**Install PHP MySQL**




    - name: Install php-mysql
      apt:
        name: php-mysql
        update_cache: yes
        
        

## SCREENSHOTS

<img width="1229" alt="procedure1" src="https://user-images.githubusercontent.com/42668363/204908828-b8adfdcc-d35a-4d6c-a6ec-0fe9906f3359.png">



<img width="1229" alt="procedure2" src="https://user-images.githubusercontent.com/42668363/204908863-92775477-c548-45a4-ac16-85055395530a.png">

