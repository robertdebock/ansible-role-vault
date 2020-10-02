# [vault](#vault)

Install Hashicorp Vault on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-vault.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-vault)|[![github](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions)|[![quality](https://img.shields.io/ansible/quality/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![downloads](https://img.shields.io/ansible/role/d/50255)](https://galaxy.ansible.com/robertdebock/vault)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-vault.svg)](https://github.com/robertdebock/ansible-role-vault/releases/)|

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

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.ca_certificates
```

For verification `molecule/resources/verify.yml` runs after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: no

  tasks:
    - name: try vault
      command: vault --version
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for vault

# The version of Vault to install.
vault_version: 1.5.0

vault_storages:
  - name: raft
    path: /root/vault/data
    node_id: node1

vault_listeners:
  - name: tcp
    address: 127.0.0.1:8200
    tls_disable: "1"

vault_api_addr: "http://127.0.0.1:8200"
vault_cluster_addr: "https://127.0.0.1:8201"
vault_ui: "true"

vault_key_shares: 5
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

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.ca_certificates
- robertdebock.core_dependencies
- robertdebock.service

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/vault.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|debian|all|
|el|7, 8|
|fedora|all|
|opensuse|all|
|ubuntu|all|

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
