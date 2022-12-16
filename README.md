# Hands-on Activity 9: OpenStack Pre-requisites installation


### Objectives

Create a workflow to install OpenStack using Ansible as your Infrastructure as Code (IaC).

### Procedure

*Run a command* : `ansible-galaxy install openstack.openstack-ansible`

*Next, create inventory file and put your host*

```
[control]
node1 ansible_host=192.168.0.1

[compute]
node2 ansible_host=192.168.0.2
node3 ansible_host=192.168.0.3

[storage]
node4 ansible_host=192.168.0.4

[all:vars]
ansible_user=openstack
```


** Create a playbook file and insert**

```
- hosts: all
  become: true
  roles:
    - openstack.openstack-ansible
```

### Run the ansible code using this command:

```$ ansible-playbook -i inventory.yml install_openstack.yml```

