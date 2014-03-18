# Presto Playbook

A [Ansible](ttp://www.ansible.com/home) playbook for [Presto](http://prestodb.io/).


## Inventory example

```
[presto_coordinator]
coordinator_host

[presto_worker]
worker_host[01:10]

[presto_server:children]
presto_coordinator
presto_worker

[presto_client]
some_nice_server
```

## Playbook example

```yaml
---
- hosts: presto_server
  sudo: yes
  vars:
    presto__xmx: 16G
    presto__hive_metastore: "metastore host"
    presto__coordinator_group: "presto_coordinator"
    presto__version: "0.61"
  roles:
    - { role: presto/server", tags: ['presto_server'] }

- hosts: presto_client
  sudo: yes
  vars:
    presto__version: "0.61"
  roles:
    - { role: presto/client", tags: ['presto_client'] }
```

## Parameter

see defaults/main.yml
