---

- name: Adding user
  vars:
   variable1: 'User_Thadeus'

  ansible.builtin.user:
    name: "{{ variable1 }}"
