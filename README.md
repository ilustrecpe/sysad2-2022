# Hands-on Midterm Exam

### Objectives

Create an Ansible playbook that does the following with an input of a config.yaml file and arranged Inventory file:

4.1 Install and configure Elastic Stack in separate  hosts (Elastic Search, Kibana, Logstash)

4.2 Install Nagios in one host

4.3 Install Grafana,Prometheus and Influxdb in seperate hosts (Influxdb,Grafana,Prometheus)

4.4 Install Lamp Stack in seperate hosts (Httpd + Php,Mariadb)


### arranged group inventory file in each hosts configuration

```
[servers]
elasticstack ansible_host=192.168.64.14
nagios ansible_host=127.0.0.1
## Grafana, prometheus, and influxdb
gratheusflux ansible_host= 192.168.64.255
lampstack ansible_host= 10.0.0.4

[all:vars]
ansible_python_interpreter=/usr/bin/python3 
```

### Roles Playbook

**Installing ELK**

```
---
- hosts: elasticstack
  become: true
- name: Downloading dependencies
  apt:
    name: apt-transport-https
    update_cache: yes

- name: Getting KEY
  ansible.builtin.apt_key:
    url: https://artifacts.elastic.co/GPG-KEY-elasticsearch
    state: present

- name: Adding to repo list
  ansible.builtin.apt_repository:
    repo: deb https://artifacts.elastic.co/packages/8.x/apt stable main
    state: present

- name: Installing ELK STACK
  apt:
    pkg:
      - elasticsearch
      - kibana
      - logstash
    update_cache: yes
```
**Install Grafana, promotheus, and influxdb**

```
---
- hosts: gratheusflux
  roles:
    - cloudalchemy.prometheus
  vars:
    prometheus_targets:
     node:
      - targets:
        - localhost:9100
        - demo.cloudalchemy.org:9100
        labels:
         env: demosite


- name: Installing dependencies
  apt:
    pkg:
      - apt-transport-https
      - software-properties-common
      - wget

- name: Grafana KEY
  ansible.builtin.apt_key:
    url: https://apt.grafana.com/gpg.key
    state: present

- name: Adding to repo
  ansible.builtin.apt_repository:
    repo: deb https://apt.grafana.com stable main
    state: present

- name: Install Grafana
  apt:
    name: grafana
    update_cache: yes
```

**Installing lampstack**

```
---
- hosts: lampstack
- name: Installing lamp stack
  apt:
    pkg:
    - apache2
    - mysql-server
    - php
    - libapache2-mod-php
    - php-mysql
  update_cache: yes
  
  - name: Getting apt key
    ansible.builtin.apt_key:
    url: https://repos.influxdata.com/influxdb.key
    state: present

- name: Adding to repository
  ansible.builtin.apt_repository:
    repo: deb https://repos.influxdata.com/ubuntu bionic stable
    state: present

- name: Installing influxdb
  apt:
    name: influxdb
    update_cache: yes
```

**Installing NagiOS**

```
---
- hosts: nagios
- name: Downloading Prerequisites
  apt:
    pkg:
    - autoconf
    - gcc
    - libc6
    - libmcrypt-dev
    - make
    - libssl-dev
    - wget
    - bc
    - gawk
    - dc
    - build-essential
    - snmp
    - libnet-snmp-perl
    - gettext
    - unzip
    - apache2
    - php
    - libapache2-mod-php7.4
    - libgd-dev
    - openssl
    update_cache: yes

- name: Downloading Source from Nagios repo
  ansible.builtin.get_url:
    url: https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.4.6.tar.gz
    dest: /tmp/nagioscore-nagios-4.4.6.tar.gz
    mode: '0440'

- name: Unarchiving 
  ansible.builtin.unarchive:
    src: /tmp/nagioscore-nagios-4.4.6.tar.gz
    dest: /tmp/
    remote_src: yes

- name: Configuring Nagios
  ansible.builtin.command: sudo ./configure --with-https-conf=/etc/apache2/sites-enabled
  args:
    chdir: /tmp/nagioscore-nagios-4.4.6

- name: Compiling Nagios
  ansible.builtin.command: "{{ item }}"
  args:
    chdir: /tmp/nagioscore-nagios-4.4.6
  with_items:
    - make clean
    - make all
    - make install-groups-users
    - make install
    - make install-daemoninit
    - make install-commandmode
    - make install-config
    - make install-webconf
---
- name: adding web server to group
  ansible.builtin.user:
    name: www-data
    group: nagios

- name: Installing apache config files
  ansible.builtin.command: "{{ item }}"
  args:
    chdir: /tmp/nagioscore-nagios-4.4.6
  with_items:
    - a2enmod rewrite
    - a2enmod cgi

- name: Downloading Plugin Source
  ansible.builtin.get_url:
    url: https://github.com/nagios-plugins/nagios-plugins/archive/release-2.3.3.tar.gz
    dest: /tmp/nagios-plugins-release-2.3.3.tar.gz
    mode: '0440'

- name: Unarchiving plugins
  ansible.builtin.unarchive:
    src: /tmp/nagios-plugins-release-2.3.3.tar.gz
    dest: /tmp/
    remote_src: yes

- name: Compiling nagios plugins
  ansible.builtin.command: "{{ item }}"
  args:
    chdir: /tmp/nagios-plugins-release-2.3.3
  with_items:
    - ./tools/setup
    - ./configure
    - make
    - make install
```
