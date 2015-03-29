# ansible-bootstrap-server

### What you have?
* A Debian server running somewhere
* A user account with ``sudo`` permissions

### What you need?
An extra user account with password-less SSH access, and password-less sudo permission.

### What you get?
Ansible role that does exactly what you need.

## Requirements

* Ansible >= 1.9

## Role variables

``user``: User to create on remote server.

``key``: URL to your public key(s). These keys will be uploaded to the new user account's ``.ssh/authorizer_keys`` and will be used in order to give you password-less sudo access to that account. Best thing you can do is use ``https://github.com/<username>.keys``, where ``username`` is your Github username. 

## Examples

``inventory``

        [all]
        remote.server.com

``playbook.yml``

        ---
        hosts: all
        remote_user: foo
        sudo: yes
        roles:
         - {role: 'ansible-bootstrap-server', user: bar, key: "https://github.com/stargazer.keys"}

Invoke playbook

        ansible-playbook -i inventory --ask-pass playbook.yml

You will be prompted to give the password of the ``foo`` user. When the playbook is done, the user ``bar`` will be created on the server ``remote.server.com``.
