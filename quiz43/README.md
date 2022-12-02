# Quiz 4.3: Log Monitor

### Objectives

Follow the procedure:

Create a directory named "quiz43" in your student number directory in Quiz 1.3
Create a markdown file named "README.md" in the newly created directory with the directory summary.
Create playbook to install Elastic Stack.
Then create a Pull request and put your forked repo in the only question of this quiz (Note answer this quiz as well as create a pull request).

### playbook

```
---
- hosts: localhost
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
      - filebeat
      - nginx
    update_cache: yes
```

# Screenshot
<img width="599" alt="Screen Shot 2022-12-03 at 7 08 33 AM" src="https://user-images.githubusercontent.com/42668363/205404437-cc6840ec-a882-43c0-ad2d-0e86d3c8d9e0.png">
