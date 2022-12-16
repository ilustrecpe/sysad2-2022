# Hands-on Activity 8: Containerization

### Objectives

Create a Dockerfile and form a workflow using Ansible as Infrastructure as Code (IaC) to enable Continuous Delivery process.

### Playbook

```
- name: Docker Installation
  service: 
    name: Docker
    state: started
    enabled: yes

- name: web server
  docker_imgae:
    name: newdeveloper/apache-php
    state: present
    source: pull

- name: db server
  docker_image:
    name: mysql/mysql-server:latest
    state: present
    source: pull
 ```
 
 
