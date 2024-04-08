# Checking for Connectivity 
An initial test should be run from the control machine to target nodes within the inventory file to determine the current connectivity status.  The `ping` module is a simple way to detect: (1) if proper credentials are in place; and (2) if Ansible is able to run Python scripts on the node.
## Current User
By default, Ansible uses the current user and the current user's respective security elements to establish a connection.

```
$ ansible all -m ping
```

## Different User
To connect as a different user, the `-u` parameter can be added followed by the name of the user.

```
$ ansible all -m ping -u tux
```

This can also be done when using a playbook.

```
$ ansible-playbook playbook1.yml -u tux
```

## Custom SSH Key
If an alternate SSH key is desired for establishing a connection, it can be provided using the `--private-key` option.

```
$ ansible all -m ping --private-key=~/.ssh/server_key
```

This can also be done when using a playbook.

```
$ ansbile-playbook playbook1.yml --private-key=~/.ssh/server_key
```

## Password-Based Authentication
The `--ask-pass` option can be used to prompt for password entry for the node.

```
$ ansible all -m ping --ask-pass
```

This can also be done when using a playbook.

```
$ ansbile-playbook playbook1.yml --ask-pass
```

## Using `sudo` 
If the remote user on a node is required to provide a password in order to run certain `sudo` commands, the `--ask-become-pass` option can be used.  This will prompt for the remote user's sudo password.

```
$ ansible all -m ping --ask-become-pass
```

This can also be done when using a playbook.

```
$ ansbile-playbook playbook1.yml --ask-become-pass
```
