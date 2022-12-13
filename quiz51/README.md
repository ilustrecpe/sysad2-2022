# Directory Summary

**Author:** Adrian Dave E. Ignacio

**Playbook:** Containerized (Docker) ELK Stack Installation for Ubuntu 20.04 LTS and/or CentOS 8

## Prequisites

* Ansible (installed on local machine)
* SSH (installed on both local and remote machine/s)
* Target Machine: Ubuntu 20.04 Server Edition LTS and/or CentOS 8 with 2 CPU cores and 4GB RAM

## Requirements

* configured SSH key-based authentication
* passwordless sudo on remote machines

Note: On remote machines execute ``sudo visudo`` and append the following line to enable passwordless sudo on account.

        ```
        <user> ALL=(ALL) NOPASSWD:ALL
        ```

## Declaring Values for Variables

Inside the ``config.yaml`` file are the variables used in the playbook (imported for the roles). Redeclare the values for each variable in the following format.

```
docker_host: <docker_repository for centos>

elasticsearch_image: <official_elasticsearch_image>
logstash_image: <official_logstash_image>
kibana_image: <official_kibana_image>

elasticsearch_hostname: <elasticsearh_container_name>
logstash_hostname: <logstash_container_name>
kibana: <kibana_container_name>

logstash_conf: <logstash_configuration_file, included in this playbook are two samples under files (logstash.conf=usual filebeat config; logstash.conf2 = generic telnet listener config)>
```

## Executing the Playbook

Execute ``playbook.yaml`` using the command:

```
$ ansible-playbook playbook.yaml
```

## Directory Structure

```
quiz51
├── README.md
├── ansible.cfg
├── config.yaml
├── files
│   ├── docker-ce.repo
│   ├── logstash.conf
│   └── logstash.conf2
├── inventory
├── playbook.yaml
└── roles
    ├── elk_setup
    │   ├── README.md
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    ├── installpackagecentos
    │   ├── README.md
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    ├── installpackageubuntu
    │   ├── README.md
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    ├── pipinstall
    │   ├── README.md
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    ├── pullimage
    │   ├── README.md
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    ├── stopfirewallcentos
    │   ├── README.md
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    └── stopfirewallubuntu
        ├── README.md
        ├── defaults
        │   └── main.yml
        ├── files
        ├── handlers
        │   └── main.yml
        ├── meta
        │   └── main.yml
        ├── tasks
        │   └── main.yml
        ├── templates
        ├── tests
        │   ├── inventory
        │   └── test.yml
        └── vars
            └── main.yml

65 directories, 64 files
```
