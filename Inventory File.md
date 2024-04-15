# Keeping Inventory of Nodes
Ansible typically installs with a default inventory file.  However, customer inventory files can also be used.  Ansible also supports inventory scripts that can be used to generate dynamic inventory files.
## Default Inventory File
By default, the inventory file is located at `/etc/ansible/hosts` and does not need to specified when running Ansible commands and playbooks.

```
$ ansible all -m ping
```

```
$ ansible-playbook playbook1.yml 
```
## Custom Inventory File
The `-i` parameter can be used to reference a custom inventory file when running Ansible commands and playbooks.

```
$ ansible all -m ping -i custom_inventory_file
```

This can also be done when using a playbook.

```
$ ansible-playbook playbook1.yml -i custom_inventory_file
```

## Inventory File Structure

### INI Format
The typical inventory file is written in the "ini" format and contains groups and nodes.  This is a simpler format to maintain and is preferred by me.

```ini
## file: /etc/ansible/hosts

email.example.com
server57 ansible_host=192.168.2.57 ansible_user=supertux    #Host alias and variable

[appservers]
windows2023.example.com
redhat.example.com

[webservers]
apache.example.com
nginx.example.com

[dbservers]
mssql-ubuntu.example.com
postgresql-debian.example.com

[apt-packages-group]                                        #Collection of groups
webservers
dbservers

[group_a]
server1 ansible_host=192.168.68.11                          #Host aliases
server2 ansible_host=fedora.example.com                     #Host aliases

[group_a:vars]
ansible_user=tux                                            #Host variables
```

### YAML Format
The inventory file can also be represented in the "yaml" format and contains groups and nodes.

```yaml
## file: /etc/ansible/hosts

all:
  hosts:
    email.example.com:
  children:
    appservers:
      hosts:
        windows2023.example.com:
        redhat.example.com:
    webservers:
      hosts:
        apache.example.com:
        nginx.example.com:    
    dbservers:
      hosts:
        mssql-ubuntu.example.com:
        postgresql-debian.example.com:
    apt-packages-group:    #Collection of groups
      children:
        webservers:
        dbservers:
```

