# Running a Series of Chained Commands
Playbooks allow for multiple commands to be run in sequential order and with greater granular control.

## Running Playbooks
The `ansible-playbook` command is used to run a playbook and execute all of the respective tasks identified within the playbook.

```
$ ansible-playbook playbook1.yml
```

### Limiting Nodes
By default, the `hosts` option is used within the playbook.  However, this can be overridden and limited by using the `-l` parameter followed by the name of a group or host.

```
$ ansible-playbook -l server1 playbook1.yml
```

## Displaying Information About a Playbook

### Listing Tasks
The `--list-tasks` option can be used to list and obtain all tasks that are within a playbook without actually running the playbook nor making any changes to nodes.

```
$ ansible-playbook playbook1.yml --list-tasks
```

### Listing Hosts
The `--list-hosts` option can be used to list and obtain all hosts (nodes) that are within a playbook without actually running the playbook nor making any changes to nodes.

```
$ ansible-playbook playbook1.yml --list-hosts
```

### Listing Tags
The `--list-tags` option can be used to list and obtain all tags that are within a playbook without actually running the playbook nor making any changes to nodes.  ***Tags*** are used within a playbook to limit the execution of the play.

```
$ ansible-playbook playbook1.yml --list-hosts
```

## Controlling the Execution of a Playbook

### Starting at a Specific Task
The `--start-at-task` option can be used to define the entry point or starting point for an existing playbook.  Ansible will ignore anything that sequentially comes before this specified task and will begin execution from the specified task to the end of the playbook.

```
$ ansible-playbook playbook1.yml --start-at-task='Install Docker'
```

### Running Tasks Based on Tags
It is also possible to only execute specific tasks that are associated or identified by specific tag(s) by using the `--tags` option.  

```
$ ansible-playbook playbook1.yml --tags=postgresql,nginx
```

### Skipping Tasks Based on Tags
It is also possible to skip or not execute specific tasks that are associated or identified by specific tag(s) by using the `--skip-tags` option.  

```
$ ansible-playbook playbook1.yml --skip-tags=apache,nix-pm
```

## Playbook Structure
The playbook below represents the installation of Docker on an Ubuntu host.

```yaml
---
- hosts: all
  become: true
  vars:
    container_count: 4
    default_container_name: docker
    default_container_image: ubuntu
    default_container_command: sleep 1d

  tasks:
    - name: Install aptitude
      apt:
        name: aptitude
        state: latest
        update_cache: true

    - name: Install required system packages
      apt:
        pkg:
          - apt-transport-https
          - ca-certificates
          - curl
          - software-properties-common
          - python3-pip
          - virtualenv
          - python3-setuptools
        state: latest
        update_cache: true

    - name: Add Docker GPG apt Key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Add Docker Repository
      apt_repository:
        repo: deb https://download.docker.com/linux/ubuntu focal stable
        state: present

    - name: Update apt and install docker-ce
      apt:
        name: docker-ce
        state: latest
        update_cache: true

    - name: Install Docker Module for Python
      pip:
        name: docker

    - name: Pull default Docker image
      community.docker.docker_image:
        name: "{{ default_container_image }}"
        source: pull

    - name: Create default containers
      community.docker.docker_container:
        name: "{{ default_container_name }}{{ item }}"
        image: "{{ default_container_image }}"
        command: "{{ default_container_command }}"
        state: present
      with_sequence: count={{ container_count }}

```
