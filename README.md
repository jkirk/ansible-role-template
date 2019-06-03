template
========

A ansible role to do the necessary things for a template VM.

Requirements
------------

A template VM is usually created on our Proxmox-Cluster via [grml-debootstrap](https://github.com/grml/grml-debootstrap).

The template VM needs the following characteristics:

* The network must be configured
* Public key authentication for the user `root` must be deployed or password authentication for `root` via ssh must be enabled
* The hostname needs to contain `template-debian-`.
* The FQDN needs to be resolvable

Role Variables
--------------

This variable can defined in the playbook:

```yaml
# The DNS-Sever where we check if the FQDN is defined before provisioning the server.
dns_server: fw.in.example.com
```

Dependencies
------------

None. But the roles [bootstrap](https://github.com/robertdebock/ansible-role-bootstrap) and [user](https://github.com/jkirk/ansible-role-user/) are recommended before running this role.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

`bootstrap-template.yml`:

```yaml
---
# This playbook prepares template VM to be managed by Ansible.
#
# Example:
#
#   ansible-playbook -u root bootstrap-template.yml

- name: Prepare template VM to be managed by Ansible
  hosts: all
  become: false
  gather_facts: false
  vars:
    dns_server: fw.in.example.com
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
