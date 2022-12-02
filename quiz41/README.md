# Quiz 4.1: Availability Monitor

### Follow the procedure:

Create a directory named "quiz41" in your student number directory in Quiz 1.3
Create a markdown file named "README.md" in the newly created directory with the directory summary.
Create playbook to install Nagios Core.
Then create a Pull request and put your forked repo in the only question of this quiz (Note answer this quiz as well as create a pull request).

### Execute command

``` ansible-playbook activity-41.yml ```

### PLAYBOOK NAGIOS CORE

```
---
- hosts: localhost
  become: true
  tasks:
    - name: Downloading dependencies
      apt:
        pkg:
         - autoconf
         - gcc
         - libc6
         - libmcrypt-dev
         - make
         - libssl-dev
         - wget
         - bc
         - gawk
         - dc
         - build-essential
         - snmp
         - libnet-snmp-perl
         - gettext
         - unzip
         - unzip
         - php
         - libapache2-mod-php7.4
         - openssl
        state: latest
        update_cache: yes

    - name: Download Nagios Core
      ansible.builtin.get_url:
            url: https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.4.6.tar.gz
            dest: /tmp/nagioscore-nagios-4.4.6.tar.gz
            mode: '0440'

    - name: Extract
      ansible.builtin.unarchive:
         src: /tmp/nagioscore-nagios-4.4.6.tar.gz
         dest: /tmp/
         remote_src: yes

    - name: Configure
      ansible.builtin.command: ./configure
      args:
        chdir: /tmp/nagioscore-nagios-4.4.6

    - name: Compile
      ansible.builtin.command: "{{ item }}"
      args:
        chdir: /tmp/nagioscore-nagios-4.4.6
      with_items:
          - make all
          - make install-groups-users
          - make install
          - make install-daemoninit
```

# SCREENSHOT

<img width="1566" alt="Screen Shot 2022-12-03 at 3 49 00 AM" src="https://user-images.githubusercontent.com/42668363/205374467-772bda62-a257-4c15-b20a-ef4867d07f28.png">
