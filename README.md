Solr Configuration as Master
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-solr-master/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-solr-master.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-solr-master)
## Summary

This role:
  - Configures Solr on Centos 7, Ubuntu or Windows host to be master.

Requirements
------------
  - Minimal Version of the ansible for installation: 2.5
  - **Java 8** [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-java.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-java)
  - **Solr installed** [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-solr-standalone.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-solr-standalone)
  - **Supported OS**:
    - CentOS
      - 7
    - Ubuntu
    - Windows
      - "Windows Server 2008"
      - "Windows Server 2008 R2"
      - "Windows Server 2012"
      - "Windows Server 2012 R2"
      - "Windows Server 2016"
      - "Windows 7"
      - "Windows 8.1"
      - "Windows 10"

[Prepared Windows System](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html)

## Role Variables
  - `solr_version` - matches available version on https://archive.apache.org/dist/lucene/solr/. Tested versions 5.3-7.1.x
    default: `7.1.0`
  - `override_dest_main_path` - root directory to store solr folder
    default: `/opt`
    default: `C:\Solr`
  - `override_dest_solr_path` - solr folder path
    default: `{{ dest_main_path }}/solr-{{ solr_version }}`
    default: `{{ dest_main_path }}\\solr-{{ solr_version }}`
  - `overrride_solr_configset_path` - solr configset folder path
    default: `{{ dest_solr_path }}/server/solr/configsets`
    default: `{{ dest_solr_path }}\\server\\solr\\configsets`
  - `solr_service_name` - solr service name
    default: `solr`
  - `solr_with_systemd` - to run solr as a service
    default: `True`
  - `configset_list` - list of configset directories
    default: `- default`
  - `auto_populate_configset_list` - get all configset directories automatically
    default: `True`

Example Inventory
----------------
[solr-master]
solr.example.com

[solrwin-master]
solrwin.example.com

[solrwin-master:vars]
ansible_user=admin
ansible_password=password
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore

Example Playbook
----------------

```yml
- name: Configure Solr as master
  hosts: solr-master
  roles:
    - role: lean_delivery.java
    - role: lean_delivery.solr_standalone
    - role: lean_delivery.solr_master
```

License
-------

Apache

Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
