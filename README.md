OpenWRT Config DHCP
=========

[![Role](https://img.shields.io/ansible/role/56272.svg)](https://galaxy.ansible.com/pe_pe/openwrt_config_dhcp/)
[![Quality](https://img.shields.io/ansible/quality/56272.svg)](https://galaxy.ansible.com/pe_pe/openwrt_config_dhcp/)
[![CI](https://github.com/pe-pe/ansible_role_openwrt_config_dhcp/workflows/CI/badge.svg)](https://github.com/pe-pe/ansible_role_openwrt_config_dhcp/actions)

Ansible role that configures dhcp settings of OpenWRT device (mainly those which are usually defined in `/etc/config/dhcp`).

Requirements
------------
None

Role variables
--------------
Configuration settings defined in `openwrt_config_dhcp` variable which are to be applied on OpenWRT device.
```yaml
openwrt_config_dhcp:
  interfaces:
    test: { interface: test, ignore: 0, leasetime: 6h, start: 50, limit: 100, dhcp_option: ["3,192.168.255.255"] }
  hosts:
    moon: { dns: 1, mac: "aa:bb:cc:dd:ee:ff", ip: 192.168.255.200 }
```
If `openwrt_config_dhcp` configuration variable is not present - no changes are made by role.

Dependencies
------------
This role depends on Ansible role `gekmihesg.openwrt` which allows to manage OpenWRT and derivatives with Ansible but without Python.

Example playbook using the role
-------------------------------
`./host_vars` \
`./host_vars/myrouter.yml`
```yaml
---
openwrt_config_dhcp:
  interfaces:
    lan: { interface: lan, ignore: 0, leasetime: 6h, start: 50, limit: 100, dhcp_option: ["3,192.168.255.255"] }
  hosts:
    moon: { dns: 1, mac: "aa:bb:cc:dd:ee:ff", ip: 192.168.255.200 }
```
`./inventory.ini`
```ini
[openwrt]
myrouter
```
`./roles` \
`./roles/requirements.yml`
```yaml
---
roles:
- name: gekmihesg.openwrt
- name: pe_pe.openwrt_config_dhcp
```
`./site.yml`
```yaml
---
- hosts: all
  roles:
    - role: gekmihesg.openwrt
    - role: pe_pe.openwrt_config_dhcp
```
`./ansible.cfg`
```ini
[defaults]
# Define inventory location
inventory = ./inventory.ini
# Where to put roles downloaded from galaxy and other repos
roles_path = ./roles
# Defaults to /tmp to avoid flash wear on target device
remote_tmp = /tmp
```

Example execution
-----------------
Install roles and requirements:
```
ansible-galaxy role install -r roles/requirements.yml
```
Preview changes execution would perform on inventory:
```
ansible-playbook site.yml --check --diff
```
Execute playbook on inventory:
```
ansible-playbook site.yml
```
License
-------
MIT

Author Information
------------------
PePe
