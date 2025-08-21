# HAProxy Ansible Role

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to:
* Configure a pre-existing Ubuntu instance to run [HA Proxy](https://www.haproxy.org/),
  a high-performance, open source load balancer and reverse proxy for TCP and Hypertext
  Transfer Protocol (HTTP) applications, and enable users can use HA Proxy to distribute
  workloads and improve website and application performance.

## Copyright and License
Copyright © EUMETSAT 2025.

The provided code and instructions are licensed under the MIT license. 
They are intended to automate the setup of an environment that includes 
third-party software components.
The usage and distribution terms of the resulting environment are 
subject to the individual licenses of those third-party libraries.

Users are responsible for reviewing and complying with the licenses of
all third-party components included in the environment.

Contact [EUMETSAT](http://www.eumetsat.int) for details on the usage and distribution terms.

## Usage

The step-by-step described below assume your local file system follows the 
example structure below, with `ewc-ansible-role-haproxy` being a clone of this
repository:
```
.
├── roles
│   └── ewc-ansible-role-haproxy
├── inventory.yml
└── playbook.yml
```

### 1. Specify the target host and SSH credentials
Create an inventory file to specify address/credentials that Ansible should use
to reach the virtual machine you wish to configure:
```yaml
# inventory.yml
---
ewcloud:
  hosts:
    ha_proxy:
      ansible_python_interpreter: /usr/bin/python3
      ansible_host: <add the IPV4 address of the target host>
      ansible_ssh_private_key_file: <add the path to local SSH RSA private key file>
      ansible_user: <add the username which owns the SSH RSA private key >
```
### 2. Customize the template

Create an Ansible Playbook file to load your customizations: 

```yaml
# playbook.yml
---
- name: Install HAProxy
  hosts: ha_proxy
  become: true
  become_user: root
  become_method: ansible.builtin.sudo

  roles:
    - ewc-ansible-role-haproxy
```

### 3. Apply the template

You can apply changes on the target host by running:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

## Final Environment
> ⚠️ Versions listed here refer only to those available for Ubuntu 22 packages
as of August 8th, 2025. As new security patches/features are published by their
authors, and newer Ubuntu image versions are introduced into the EWC, the 
effective versions installed in your environment might be higher.

Third-party components used in the resulting environment.

### Ubuntu 22.04 Environment

The following components will be included in the resulting environment:

| Component | Version | License | Home URL |
|------|---------|---------|--------------|
| docker-ce | 28.3 | Apache-2.0 | https://github.com/docker-archive/docker-ce |
| docker-ce-cli | 28.3 | Apache-2.0 | https://github.com/docker/cli |
| containerd.io | 1.7  | Apache-2.0 | https://github.com/containerd/containerd |
| docker-compose-plugin | 2.39 |  Apache-2.0 | https://github.com/docker/compose |
| haproxy | 2.2 |  Apache-2.0 | https://hub.docker.com/r/thingsboard/haproxy-certbot |

## Changelog
All notable changes (i.e. fixes, features and breaking changes) are documented 
in the [CHANGELOG.md](./CHANGELOG.md).

## Contributing

Thanks for taking the time to join our community and start contributing!
Please make sure to:
* Familiarize yourself with our [Code of Conduct](./CODE_OF_CONDUCT.md) before 
contributing.
* See [CONTRIBUTING.md](./CONTRIBUTING.md) for instructions on how to request 
or submit changes.

## Authors

[European Weather Cloud](http://support.europeanweather.cloud/) 
<[support@europeanweather.cloud](mailto:support@europeanweather.cloud)>
