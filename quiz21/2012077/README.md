How to create an Ansible Configuration.
Certain settings in Ansible are adjustable via a configuration file (ansible.cfg). The stock configuration should be sufficient for most users, but there may be reasons you would want to change them.
Paths where configuration file is searched are listed in reference documentation.

How to create an Ansible Inventory.
Step 1 — Creating a Custom Inventory File. ...
Step 2 — Organizing Servers Into Groups and Subgroups. ...
Step 3 — Setting Up Host Aliases. ...
Step 4 — Setting Up Host Variables. ...
Step 5 — Using Patterns to Target Execution of Commands and Playbooks.

How to create an Ad-hoc Ansible command with setup and shell module.
$ ansible app -m file -a "path=/opt/oracle/binaries state=directory mode=0755" -i ansible_hosts -b – become-user=weblogic.
mwivmapp01 | SUCCESS => {
"gid": 1001,
"size": 6,
"uid": 1001.
}
mwivmapp02 | SUCCESS => {
"gid": 1001,
