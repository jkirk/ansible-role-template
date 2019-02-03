template
========

A ansible role to do the necessary things for a template VM.

Requirements
------------

A template VM is usually created on our Proxmox-Cluster via [grml-debootstrap](https://github.com/grml/grml-debootstrap).

The network must be configured and public key authentication for the user
`root` must be deployed or the password authentication for root via ssh must be enabled.

The hostname of the template VM needs to be `template-debian-stretch`.

After that the template VM is cloned and Ansible should handle the configuration.

To use this role you need a working DNS-Server where FQDN of the final server is configured.

Role Variables
--------------

`group_vars/all`:

```yaml
dns_server: fw.in.example.com
```

Dependencies
------------

None. But the roles [bootstrap](https://github.com/robertdebock/ansible-role-bootstrap) and [user](https://github.com/jkirk/ansible-role-user/) are recommended before and [Oefenweb.hostname](https://github.com/Oefenweb/ansible-hostname.git) is recommended after running this role.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

`bootstrap-template.yml`:

```yaml
---
# This playbook prepares the system to be managed by Ansible.
#
# Example:
#
#   ansible-playbook -u root bootstrap.yml

- name: Prepare system to be managed by Ansible
  hosts: all
  become: false
  gather_facts: false
  roles:
    - robertdebock.bootstrap
    - { role: jkirk.user, users: [ 'jane_doe', 'john_doe' ], groupname: 'sysadmin', admin: True }
    - jkirk.template
    - Oefenweb.hostname
```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
