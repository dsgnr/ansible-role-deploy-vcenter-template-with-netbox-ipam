# Ansible Role: Deploy a new vCenter template and obtain an IP from Netbox IPAM

[![Build Status](https://travis-ci.org/dsgnr/ansible-role-deploy-vcenter-template-with-netbox-ipam.svg?branch=master)](https://travis-ci.org/dsgnr/ansible-role-deploy-vcenter-template-with-netbox-ipam)

This role obtains the latest available IP address from a Netbox IPAM instance for a specific VLAN. It clones a vCenter template and assigns the new IP address via the vCenter OS Customisation steps. It also adds both forward and reverse DNS to a Bind DNS server.

This is used for my homelab, so as your environment will differ, this may not work out of the box for you.

## Requirements

- NetBox IPAM
- Bind9 DNS Server
- vCenter with VM Templates

## Role Variables

Please see the defaults file.


## Example Playbook

    ---
    - hosts: localhost
      connection: local
      gather_facts: false
      vars:
        - domain_root: "domain.local"
        - vlan: 50
        - dns_server_ip: "10.50.3.250"
        - dns_server_fqdn: "v-dns001.domain.local"

      vars_files:
        - vault/core_db_vars.yml
        - vault/ipam_api.yml
        - vault/vm_deploy.yml
      tasks:
        - include_role:
            name: deploy-new-vm

## License

GNUv3


