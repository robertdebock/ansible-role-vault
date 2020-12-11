# [vault](#vault)

Install Hashicorp Vault on your system.

|Travis|GitHub|GitLab|Quality|Downloads|Version|
|------|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-vault.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-vault)|[![github](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-vault/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-vault)|[![quality](https://img.shields.io/ansible/quality/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![downloads](https://img.shields.io/ansible/role/d/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-vault.svg)](https://github.com/robertdebock/ansible-role-vault/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.vault
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.hashicorp
      hashicorp_products:
        - vault
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for vault

# The TTL parameters
vault_max_lease_ttl: 786h
vault_default_lease_ttl: 768h

# Configure clustering.
vault_disable_clustering: "True"

# The details of the cluster.
vault_cluster_name: vault-cluster

# The addresses to use.
vault_cluster_addr: "http://vault1.example.com:8201"
vault_api_addr: "http://vault2.example.com:8200"

# The plugin plugin directory.
vault_plugin_directory: /usr/local/lib/vault/plugins

# The storage backend(s) to configure.
vault_storages:
  - name: raft
    path: /vault/data
    node_id: node1
    # retry_join:
    #   - "http://vault1.example.com:8200"
    #   - "http://vault2.example.com:8200"
    #   - "/http://vault3.example.com:8200"

# Where vault should listen on.
vault_listeners:
  - name: tcp
    address: 127.0.0.1:8200
    tls_disable: "1"

# Have the web ui be made available.
vault_ui: yes

# The amount of unseal keys to hand out.
vault_key_shares: 5
# The amount of unseal keys to require.
vault_key_threshold: 3

# Once the unseal keys are known, they can be used to unseal the vault.
# The initial run on this role, displays the seal keys and token once.
# You can set them after the initial run here, but much better would be
# to use ansible-vault.
# vault_unseal_keys:
#   - "4zWxu8yVanUEkJmLOBCiZa6e5WQb+8zHcyv/HjyJKfqW"
#   - "z6zNeNnJusBA0Sf46GSf0S7iNCdx+B7QeBfhh29LHxZR"
#   - "8uEg/+mOON7qW84/Z2NKFDxht9UCWgUs7f541liP/tzU"
#   - "ai3eH6KZCpbVLFwm6Wnnc9GDGYoM7K/gJkfB8nIzkV75"
#   - "sBEBQzmx6LLRT0ty2g4GkSSestlv67MG974rZ3rNfZmK"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-vault/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-core_dependencies.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) |
| [robertdebock.hashicorp](https://galaxy.ansible.com/robertdebock/hashicorp) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-hashicorp.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-hashicorp) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-hashicorp/actions) |
| [robertdebock.vault](https://galaxy.ansible.com/robertdebock/vault) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-vault.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-vault) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/vault.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7, 8|
|debian|buster|
|fedora|32, 33|
|ubuntu|bionic, focal|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-vault) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-vault/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
