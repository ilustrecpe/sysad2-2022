---
# tasks file for roles/centos-elastic
- name: Install prerequisites of elasticsearch
  yum:
    name: java-11-openjdk-devel
    state: present
    update_cache: yes

- name: Install elasticsearch repo
  yum_repository:
    name: Elastic_7.x_repo
    baseurl: https://artifacts.elastic.co/packages/7.x/yum
    gpgcheck: yes
    gpgkey: https://artifacts.elastic.co/GPG-KEY-elasticsearch
    enabled: yes
    description: Elastic 7.x repo

- name: Add elasticsearch key
  rpm_key:
    key: https://artifacts.elastic.co/GPG-KEY-elasticsearch
    state: present

- name: elasticsearch port
  lineinfile:
    destfile: /etc/elasticsearch/elasticsearch.yml
    regexp: 'http.port:'
    line: 'https.port: 9200'

- name: Run elasticsearch
  service:
    name: elasticsearch
    state: started

- name: Install logstash repo
  yum_repository:
    name: Elastic repository for 7.x packages
    baseurl: https://artifacts.elastic.co/packages/7.x/yum
    gpgcheck: yes
    gpgkey: https://artifacts.elastic.co/GPG-KEY-elasticsearch
    enabled: yes
    description: Elastic 7.x packages repo

- name: Install logstash
  yum:
    name: logstash
    state: present
    update_cache: yes

- name: logstash host
  lineinfile:
    destfile: /etc/logstash/logstash.yml
    regexp: 'http.host:'
    line: 'http.host: 127.0.0.1'

- name: Run logstash
  service:
    name: logstash
    state: started

- name: Install kibana repo
  yum_repository:
    name: Kibana 7.x packages
    baseurl: https://artifacts.elastic.co/packages/7.x/yum
    gpgcheck: yes
    gpgkey: https://artifacts.elastic.co/GPG-KEY-elasticsearch
    enabled: yes
    description: Kibana-7.x

- name: Install kibana
  yum:
    name: kibana
    state: present
    update_cache: yes

- name: kibana host
  lineinfile:
    destfile: /etc/kibana/kibana.yml
    regexp: 'server.host:'
    line: 'server.host: 0.0.0.0'

- name: kibana port
  lineinfile:
    destfile: /etc/kibana/kibana.yml
    regexp: 'server.port:'
    line: 'server.port: 5601'

- name: Run kibana
  service:
    name: kibana
    state: started
