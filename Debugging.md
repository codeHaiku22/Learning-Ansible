# Leveraging Verbosity to Identify Issues
The output verbosity can be increased when running Ansible commands and playbooks.  This allows for more information and insight to be obtained that can help to identify a problem.

## Basic Verbosity
The `-v` option can be included when running a command or playbook .

```
$ ansible-playbook playbook1.yml -v
```

## Enhanced Verbosity
If additional detail is needed, the `-vvv` option can be used to increase the level of verbosity that is shown in the output.

```
$ ansible-playbook playbook1.yml -vvv
```

## Connection Debugging
If information regarding the connection are needed, the `-vvvv` option can be used for debugging the connection, itself.

```
$ ansible-playbook playbook1.yml -vvvv
```
