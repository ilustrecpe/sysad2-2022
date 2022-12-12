---
# tasks file for roles/ubuntu-nagios
- name: Install nagios core requisites
  apt:
    name: 
      - build-essential
      - apache2
      - php
      - openssl
      - perl
      - make
      - php-gd
      - libgd-dev
      - libapache2-mod-php
      - libperl-dev
      - libssl-dev
      - daemon
      - wget
      - apache2-utils
      - unzip

- name: add group nagcmd
  group:
    name: nagcmd
    state: present

- name: add user nagios
  user:
    name: nagios
    group: nagcmd
