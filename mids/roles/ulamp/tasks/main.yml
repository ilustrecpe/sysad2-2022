---
# tasks file for roles/ubuntu-lamp
- name: Install apache2
  apt: 
    name: apache2
    state: latest
    update_cache: yes

- name: Add apache_index
  copy:
    content: "Apache test"
    dest: /var/www/html/index.html
    owner: root
    group: root
    mode: '0644'
  register: apache_index

- name: Restart apache2
  service:
    name: apache2
    state: restarted
    enabled: yes
  when: apache_index.changed

- name: Whitelist apache2 in ufw
  ufw:
    rule: allow
    port: '80'
    proto: tcp

- name: Install mysql
  apt:
    name: mysql-server
    state: latest
    update_cache: yes

- name: Add mysql_index
  copy:
    content: "MYSQL test"
    dest: /var/www/html/index1.html
    owner: root
    group: root
    mode: '0644'
  register: mysql_index

- name: Run MYSQL
  service:
    name: mysql
    state: started
    enabled: yes
  when: mysql_index.changed

- name: Install php
  apt:
    name:
       - php
       - php-mysql
       - libapache2-mod-php
    state: latest
    update_cache: yes

- name: Add php_index
  copy:
   content: "PHP test"
   dest: /var/www/html/index2.html
   owner: root
   group: root
   mode: '0644'
