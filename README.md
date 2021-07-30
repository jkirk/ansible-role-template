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
# The DNS-Sever where we check if the FQDN is defined before provisioning the server (default to 'localhost')
template_dns_server: 'fw.in.example.com'
```

Dependencies
------------

None. But the roles [bootstrap](https://github.com/robertdebock/ansible-role-bootstrap) and [user](https://github.com/jkirk/ansible-role-user/) are recommended before running this role.

Example Playbook
----------------

See: [bootstrap-template.yml](https://github.com/jkirk/ansible-site-template/blob/master/bootstrap-template.yml)

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
