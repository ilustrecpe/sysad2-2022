---
- hosts: all
  become: true
  tasks:
    - name: get GPG key
      ansible.builtin.command: curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch

    - name: copy elastic
      ansible.builtin.command: echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main"

    - name: Install STACK
      apt:
        pkg:
          - apt-transport-https
          - elasticsearch
          - kibana
          - nginx
          - logstash
          - filebeat
