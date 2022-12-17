---
# tasks file for roles/ubuntu-nagios3
- name: Install nagios plugins
  unarchive: 
    src: https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
    dest: /tmp
    remote_src: yes

- name: Configure nagios plugins
  command: ./configure --with-nagios-user=nagios --with-nagios-grou=nagcmd
  args:
    chdir: /tmp/nagios-plugins-2.3.3

- name: Configure using make
  make:
    chdir: /tmp/nagios-plugins-2.3.3

- name: Configure using make install
  make: 
    target: install
    chdir: /tmp/nagios-plugins-2.3.3

- name: Enable and start nagios
  service:
    name: nagios
    enabled: yes
    state: started
