# Storing Sensitive Data with Ansible Vaults
Playbooks may contain sensitive information such as credentials and keys.  This type of information should be secured using encryption.  Ansible provides the `ansible-vault` feature which can be used to encrypt files and, more commonly, variable files.  

## Creating a New Encrypted File
When creating a new encrypted file with the `create` command, you must first supply a password.  This password will be used anytime this file is accessed for read or write purposes.

```
$ ansible-vault create credentials.yml

New Vault password: ************
Confirm New Vault password: ************
```

## Adding Encryption to Existing Files
Existing files can also undergo encryption using the `encrypt` command.  As with creating new encrypted files, you must first supply a password.  This password will be used anytime this file is accessed for read or write purposes.

```
$ ansible-vault encrypt credentials.yml

New Vault password: ************
Confirm New Vault password: ************
Encryption successful
```

## Viewing an Encrypted File
To simply a view the contents of a file in a read-only mode with the `view` command, you must supply the correct password associated with the encrypted file. 

```
$ ansible-vault view credentials.yml

Vault password: ************
```

## Editing an Encrypted File
To edit the contents of a file, use the `edit` command.  You must supply the correct password associated with the encrypted file.  Once the file changes are complete and the file is saved and closed, the file will go back into an encrypted state.

```
$ ansible-vault edit credentials.yml

Vault password: ************
```

## Decrypting an Existing File
An existing file can be decrypted using the `decrypt` command.  You must supply the correct password associated with the encrypted file.  Once the file has been decrypted, it will be saved as unencrypted (plain text) data.
 
```
$ ansible-vault decrypt credentials.yml

Vault password: ************
Decryption successful
```

# Multiple Ansible Vaults
Ansible facilitates the utilization of multiple vault passwords categorized by distinct vault Ids.  This feature can be beneficial when separate vault passwords are needed for various environments, such as development, test, and production.

## Creating a New Encrypted File
To generate a new encrypted file use with `create` command (and a custom vault Id), use the `--vault-id` option along with the vault name and either a prompt (requiring password input) or path to the password file.

In the example below, we are creating for the production environment.

```
$ ansible-vault create --vault-id prod@prompt credentials_prod.yml

New vault password (prod): ************
Confirm new vault password (prod): ************
```

In the example below, we are creating for the test environment.

```
$ ansible-vault create --vault-id test@/path/to/password/file credentials_test.yml
```

In the example below, we are creating for the development environment.

```
$ ansible-vault create --vault-id dev@/path/to/password/file credentials_dev.yml
```
## Viewing an Encrypted File
To simply a view the contents of a file in a read-only mode with the `view` command (and a custom vault Id), use the `--vault-id` option along with the vault name and either a prompt (requiring password input) or path to the password file.

```
$ ansible-vault view credentials_prod.yml --vault-id prod@prompt

Vault password (prod): ************
```

## Editing an Encrypted File
To edit the contents of a file with the `edit` command (and a custom vault Id), use the `--vault-id` option along with the vault name and either a prompt (requiring password input) or path to the password file.

```
$ ansible-vault edit credentials_prod.yml --vault-id prod@prompt

Vault password (prod): ************
```

## Decrypting Existing Files
An existing files can be decrypted using the `decrypt` command (and a custom vault Id), use the `--vault-id` option along with the vault name and either a prompt (requiring password input) or path to the password file.  You must supply the correct password associated with the encrypted file.  Once the file has been decrypted, it will be saved as unencrypted (plain text) data.
 
```
$ ansible-vault decrypt credentials.yml --vault-id prod@prompt

Vault password (prod): ************
```

# Running a Playbook with Data Encrypted via an Ansible Vault
When the `ansible-vault` command has been used to encrypt data, the vault password will need to be provided whenever a playbook is run that needs access to the encrypted data. 
