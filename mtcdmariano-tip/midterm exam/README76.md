---
# tasks file for roles/ubuntu-nagios2
- name: download and extract nagios
  unarchive:
    src: https://sourceforge.net/projects/nagios/files/nagios-4.x/nagios-4.4.6/nagios-4.4.6.tar.gz
    dest: /tmp
    copy: no

- name: Configure nagios 
  command: ./configure --with-nagios-group=nagcmd --with-command-group=nagcmd --with-httpd_conf=/etc/apache2/sites-enabled
  args:
    chdir: /tmp/nagios-4.4.6

- name: Complie nagios make clean
  make:
    chdir: /tmp/nagios-4.4.6
    target: clean

- name: Compile nagios make all
  make:
    chdir: /tmp/nagios-4.4.6
    target: all

- name: Compile nagios make install
  make: 
    target: install
    chdir: /tmp/nagios-4.4.6

- name: Complie nagios make install-init
  make: 
     target: install-init
     chdir: /tmp/nagios-4.4.6

- name: Compile nagios make install-config
  make:
     target: install-config
     chdir: /tmp/nagios-4.4.6

- name: Compile nagios make install-commandmode
  make:
     target: install-commandmode
     chdir: /tmp/nagios-4.4.6

- name: Install webconf
  make:
     target: install-webconf
     chdir: /tmp/nagios-4.4.6

- name: Add user account
  htpasswd:
     path: /usr/local/nagios/etc/htpasswd.users
     name: "{{user}}"
     password: "{{pass}}"

- name: a2enmod cgi
  command: a2enmod cgi

- name: Restart apache2
  service: 
      name: apache2
      state: restarted
