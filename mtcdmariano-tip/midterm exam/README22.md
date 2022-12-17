---
# tasks file for roles/centos-mtcdmariano
- name: Add mtcdmariano repo
  copy:
    src: mtcdmariano.repo
    dest: /etc/yum.repos.d/

- name: Install mtcdmariano
  yum:
    name: mtcdmariano
    state: latest
    update_cache: yes

- name: Run mtcdmariano
  service:
    name: mtcdmariano-server
    state: started

- name: Add prometheus repo
  copy:
    src: prometheus.repo
    dest: /etc/yum.repos.d

- name: Install prometheus
  yum:
    name: prometheus2
    state: latest
    update_cache: yes

- name: Run prometheus
  service:
    name: prometheus
    state: started

- name: Add influxdb repo
  copy: src: influxdb.repo
  dest: /etc/yum.repos.d/

- name: Install influxdb
  yum:
    name: influxdb
    state: latest
    update_cache: yes

- name: Run influxdb
  service:
    name: influxdb
    state: started
