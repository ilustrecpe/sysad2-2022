---
# tasks file for roles/centos-lamp
- name: Install httpd
  yum:
    name: httpd
    state: latest
    update_cache: yes

- name: Add httpd_index
  copy:
    content: "Apache test"
    dest: /var/www/html/index.html
    owner: root
    group: root
    mode: '0644'
    register: httpd

- name: Run httpd
  service:
    name: httpd
    state: started
  when: httpd.changed

- name: Stop firewall
  service:
    name: firewalld
    state: stopped

- name: Install mariadb
  yum:
    name: mariadb-server
    state: latest
    update_cache: yes

- name: Add mysql_index
  copy:
    content: "MySQL test"
    dest: /var/www/html/index1.html
    owner: root
    group: root
    mode: '0644'
  register: mysql

- name: Run mariadb
  service:
    name: mariadb
    state: started
  when: mysql.changed

- name: Install php
  yum:
    name: 
      - php
      - php-mysqlnd
    state: latest
    update_cache: yes

- name: Add php index
  copy:
    content: "PHP test"
    dest: /var/www/html/index2.html
    owner: root
    group: root
    mode: '0664'
  register: php

- name: Restart httpd
  service: 
    name: httpd
    state: restarted
  when: php.changed
