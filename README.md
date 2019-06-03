nodejs role
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-nodejs/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-nodejs.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-nodejs)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-nodejs/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-nodejs/pipelines)
[![Galaxy](https://img.shields.io/badge/galaxy-lean__delivery.nodejs-blue.svg)](https://galaxy.ansible.com/lean_delivery/nodejs)
![Ansible](https://img.shields.io/ansible/role/d/32264.svg)
![Ansible](https://img.shields.io/badge/dynamic/json.svg?label=min_ansible_version&url=https%3A%2F%2Fgalaxy.ansible.com%2Fapi%2Fv1%2Froles%2F32264%2F&query=$.min_ansible_version)

Summary
-------

This role:
  - installs Node.js on EL and Ubuntu.
  - make preparation and install Node.js packages globally.

Requirements
------------

- Version of the ansible for installation: 2.5
- **Supported OS**
  - EL
    - 6
    - 7
  - Ubuntu
    - 16.04
    - 18.04

Role Variables
--------------

- required
  - `nodejs_branch` -  is used to select main nodejs branch to be installed.  
  default value is `8`.
  - `nodejs_version` - version of node.js.  
  default value is `8*`

- defaults
  - `nodejs_apt_key` - GPG-key for APT repositories  
  default value is `https://deb.nodesource.com/gpgkey/nodesource.gpg.key`
  - `nodejs_apt_url` - path to nodejs APT repository  
  default value is `deb https://deb.nodesource.com/node_{{ nodejs_branch }}.x {{ ansible_distribution_release }} main`
  - `nodejs_transport` - RedHat distribution transport  
  default value is `  {{ ansible_distribution_major_version is version('7', '<') | ternary('http','https') }}`
  - `nodejs_rpm_key` - GPG-key for RPM repositories  
  default value is `{{ nodejs_transport }}://rpm.nodesource.com/pub/el/NODESOURCE-GPG-SIGNING-KEY-EL`
  - `nodejs_yum_url` - path to nodejs RPM repository  
  - `build_tools` - to compile and install native addons from npm you may also need build tools.  
  default value is `false`.
  - `npm_global_user` - global packages owner.  
  default value is `""` (global packages are not installed).
  - `npm_global_group` - global packages group.  
  default value is `""` (global packages are not installed).
  - `npm_global_directory` - global installation directory.  
  default value is `/usr/local/lib/npm`.
  - `npm_global_packages` - a list of npm packages with a name and a version.  
  default value is `[]`.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- name: "Install node.js on remote hosts"
  hosts: servers

  vars:
    nodejs_branch: 10
    nodejs_version: 10.15.3
    build_tools: true
    npm_global_user: user
    npm_global_group: user
    npm_global_directory: /home/user/.local
    npm_global_packages:
      - lodash
      - name: express
        version: 4.16.0

  roles:
    - role: ansible-role-nodejs
```

Inventory example
-----------------

    [servers]
    127.0.0.1

Install nodejs role
-------------------

```bash
$ ansible-playbook playbook.yml -i inventory
```

License
-------

Apache

Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
