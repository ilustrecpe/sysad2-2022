## How to create an Ansible Configuration
- Open a terminal window on your control node.
- Create a new playbook file named playbook.yaml in any directory and open it for editing.
- Add the content to playbook.yaml.
- Run your playbook.

## How to create an Ansible Inventory
- Create a Custom Inventory File
- Organizing Servers Into Groups and Subgroups.
- Setting Up Host Aliases.
- Setting Up Host Variables.
- Using Patterns to Target Execution of Commands and Playbooks.

## How to create an Ad-hoc Ansible command with setup and shell module
- To run an ad hoc command, the command must be framed or have the following syntax.
- ansible <host-pattern> [options]
- For example. The command should be written as follows.
- ansible appserverhostgroup -m <modulename> -a <arguments to the module>
