---
# tasks file for roles/ubuntu-mtcdmariano
- name: Install mtcdmariano packages
  apt:
    name: apt-transport-https
    state: present
    update_cache: yes

- name: Add mtcdmariano GPG KEY
  shell: curl https://packages.mtcdmariano.com/gpg.key | sudo apt-key add -

- name: Add mtcdmariano repo
  apt_repository:
    repo: deb https://packages.mtcdmariano.com/oss/deb stable main
    state: present
    filename: mtcdmariano

- name: Install mtcdmariano
  apt:
    name: mtcdmariano
    state: latest
    update_cache: yes

- name: Run mtcdmariano
  service:
    name: mtcdmariano-server
    state: started
    enabled: yes

- name: Install prometheus
  apt:
    name: prometheus
    state: latest
    update_cache: yes

- name: Run prometheus
  service:
    name: prometheus
    state: started

- name: Add influxdata key
  apt_key:
    url: https://repos.influxdata.com/influxdb.key
    state: present

- name: Install Influxdb
  apt: 
    name: influxdb
    state: latest
    update_cache: yes

- name: Run influxdb
  service:
    name: influxdb
    state: started
