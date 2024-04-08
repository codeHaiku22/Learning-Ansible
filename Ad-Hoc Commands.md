# Issuing Commands "On the Fly"
Not everything has to be pre-determined and pre-scripted within playbooks.  Commands can also be issued immediately and manually using the CLI.

## Commands
A command can be issued on a node by using the `-a` parameter followed immediately by the desired command, itself (within quotes)

```
$ ansible all -a 'uname -a'
```

## Modules
It run an Ansible module, use the `-m` parameter.  In the example below, the `htop` package is being installed on server1 (as defined in the inventory file).

```
$ ansible server1 -m apt -a 'htop'
```

## Dry Run
It is even possible to perform a "dry run" before making any changes on a node.  This can be done by using the `--check` option.

```
$ ansible server1 -m apt -a 'htop' --check
```
