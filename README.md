nodejs role
===========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-nodejs/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-nodejs.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-nodejs)

## Summary

This role:
  - installs Node.js on EL and Ubuntu.
  - make preparation and install Node.js packages globally.

## Requirements

- Version of the ansible for installation: 2.5
- **Supported OS**
  - EL
    - 6
    - 7
  - Ubuntu
    - 16.04
    - 18.04

## Role Variables

- required
  - `nodejs_version`
  Version of node.js. Default value is `8`.

- defaults
  - `build_tools`
  To compile and install native addons from npm you may also need build tools. Default value is `False`.
  - `npm_global_user`
  Global packages owner. Default value is `""` (global packages are not installed).
  - `npm_global_group`
  Global packages group. Default value is `""` (global packages are not installed).
  - `npm_global_directory`
  Global installation directory. Default value is `/usr/local/lib/npm`.
  - `npm_global_packages`
  A list of npm packages with a name and a version. Default value is `[]`.

## Dependencies

None.

## Example Playbook

```yaml
- name: "Install node.js on remote hosts"
  hosts: servers

  vars:
    nodejs_version: 10
    build_tools: True
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

## Inventory example

    [servers]
    127.0.0.1

## Install nodejs role

```bash
$ ansible-playbook playbook.yml -i inventory
```

## License

Apache

## Author Information

authors:
  - Lean Delivery Team <team@lean-delivery.com>
