---
# tasks file for roles/ubuntu-elastic
- name: Install prerequisites of elasticsearch
  apt:
    name:
      - openjdk-11-jdk
      - nginx
    state: latest
    update_cache: yes

- name: Get elasticsearch repo
  apt_key:
    url: "https://packages.elastic.co/GPG-KEY-elasticsearch"
    state: present

- name: Get apt-transport-https
  apt:
    name: apt-transport-https
    state: present

- name: Install elastic packages
  apt:
    name: elasticsearch
    state: present
    update_cache: yes

- name: elasticsearch port
  lineinfile:
    destfile: /etc/elasticsearch/elasticsearch.yml
    regexp: 'http.port'
    line: 'http.port: 9200'

- name: Discovery type
  lineinfile:
    destfile: /etc/elasicsearch/elasticsearch.yml
    line: 'discovery.type: single-node'

- name: Reload systemd config
  systemd: daemon_reload=yes

- name: Ensure elasticsearch running
  systemd: state=started name=elasticsearch

- name: Install kibana
  apt:
    name: kibana
    update_cache: yes

- name: Add kibana server
  lineinfile:
    destfile: /etc/kibana/kibana.yml
    regexp: 'server.host:'
    line: 'server.host: localhost'

- name: kibana port
  lineinfile:
    destfile: /etc/kibana/kibana.yml
    regexp: 'server.port'
    line: 'server.port: 5601'

- name: Run kibana
  service:
    name: kibana
    state: started

- name: Install logstash
  apt:
    name: logstash
    update_cache: yes

- name: Start logstash
  service:
    name: logstash
    state: started
