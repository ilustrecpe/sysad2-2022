---
- name: add grafana repositories
  copy:
    src: grafana.repo
    dest: /etc/yum.repos.d/

- name: install grafana
  yum:
    name: grafana
    state: latest
    update_cache: yes

- name: start grafana
  service:
    name: grafana-server
    state: started

- name: add prometheus repositories
  copy:
    src: prometheus.repo
    dest: /etc/yum/repos.d/

- name: install prometheus
  yum:
    name: prometheus2
    state: latest
    update_cache: yes

- name: start prometheus 
  service:
    name: prometheus
    state: started

- name: add influxdata repository
  copy:
    src: influxdp.repo
    dest: /etc/yum.repos.d/

- name: install telegraf
  yum:
    name: telegraf
    state: latest
    update_cache: yes

- name: start telegraf
  service:
    name: telegraf
    state: started
