# Hands-on Final Exam

### Objectives

Create an Ansible playbook that does the following with an input of a config.yaml file and structure inventory file.

4.1 Clone your prelim exam repository

4.2 Install and configure one enterprise service that can be installed in Debian,Centos and Mageia/Fedora servers

4.3 Install and configure one monitoring tool that can be installed in Debian, Centos and Mageia/Fedora servers (if it is a stack there should be option of different host)

4.4 Change Motd as "Ansible Managed by <username>"

### Playbook

**Hosts Inventory**

```
[debian]
192.168.64.14

[centos]
192.168.64.17

[mageia]
192.168.64.23
```
**To execute the ansible command type:** `ansible-playbook -i inventory playbook.yml`

## ChangeMOTD

```
- name: change message of the day
  copy:
    content: "{{ motd }} \n"
    dest: /etc/motd

- name: Disable default motd
  file:
    dest: "/etc/update-motd.d/"
    mode: "u-x,g-x,,o-x"
    state: directory
    recures: yes
```

