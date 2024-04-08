# Definitions

The terminology used with Ansible is unique and should be defined and understood before proceeding.

- ***Ansible*** is a configuration management utility that simplifies remote server setup and maintenance.
- ***Control Machine (Node)*** - a central host machine where Ansible has been installed and configured with the ability to execute commands on remote servers.
- **Node*** - a remote target server that can be controlled by Ansible.
- ***Inventory File*** - a file that contains information about all nodes that can be affected by Ansible.  The default location of this file is usually `/etc/ansible/hosts`.
- ***Playbook*** - a file that contains tasks that can be executed on a node.
- ***Role*** - a group of playbooks and other related files which seek to accomplish a greater goal such as installing and configuring a web server.
- ***Play*** - a complete Ansible run that can consist of playbooks and roles.  Plays are included as an entry point from a single playbook.
