# Quiz 4.2: Performance Monitor

### Objectives

Follow the procedure:

Create a directory named "quiz42" in your student number directory in Quiz 1.3
Create a markdown file named "README.md" in the newly created directory with the directory summary.
Create a playbook to install **Grafana** with **Prometheu**s and **Telegraf** as agent.
Then create a Pull request and put your forked repo in the only question of this quiz (Note answer this quiz as well as create a pull request).

### Playbook

**Execute command**: ``ansible-playbook -i inventory main.yml``

**Prometheus**

```
---
- hosts: localhost
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
```

**Grafana**

```
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

# SCREENSHOT

<img width="836" alt="Screen Shot 2022-12-03 at 5 57 46 AM" src="https://user-images.githubusercontent.com/42668363/205397838-bc961a41-1edb-400c-a0df-928325f1efb7.png">
<img width="1190" alt="Screen Shot 2022-12-03 at 5 58 02 AM" src="https://user-images.githubusercontent.com/42668363/205397883-5f1de5e7-5761-44f4-a970-fe4f04e4f925.png">
<img width="1208" alt="Screen Shot 2022-12-03 at 5 58 21 AM" src="https://user-images.githubusercontent.com/42668363/205397901-2fedee4e-45ce-4c45-97d8-7a55b8850f66.png">
<img width="1201" alt="Screen Shot 2022-12-03 at 5 58 42 AM" src="https://user-images.githubusercontent.com/42668363/205397912-502137e8-a81a-4e7b-b689-6b2f005b528d.png">





