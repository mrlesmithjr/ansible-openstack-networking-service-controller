<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-openstack-networking-service-controller](#ansible-openstack-networking-service-controller)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
    - [Ansible Roles](#ansible-roles)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-openstack-networking-service-controller

An [Ansible](https://www.ansible.com) role to install/configure
[OpenStack Networking Service Controller](https://docs.openstack.org/ocata/install-guide-ubuntu/neutron-controller-install.html)

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-openstack-networking-service-controller

# Defines Neutron DB info
openstack_networking_service_controller_db_info:
  db: 'neutron'
  user: 'neutron'
  pass: 'neutron'
  host: 'localhost'

# keystone_authtoken
openstack_networking_service_controller_keystone_authtoken:
  auth_type: 'password'
  auth_uri: '{{ openstack_networking_service_controller_keystone_service_endpoint_url }}:5000'
  auth_url: '{{ openstack_networking_service_controller_keystone_service_endpoint_url }}:35357'
  memcached_servers: '{{ openstack_networking_service_controller_memcached_servers }}'
  password: "{{ openstack_networking_service_controller_neutron_user_info['password'] }}"
  project_domain_name: "{{ openstack_networking_service_controller_neutron_user_info['domain_id'] }}"
  project_name: "{{ openstack_networking_service_controller_neutron_user_info['project'] }}"
  user_domain_name: "{{ openstack_networking_service_controller_neutron_user_info['domain_id'] }}"
  username: "{{ openstack_networking_service_controller_neutron_user_info['name'] }}"

# Defines the default Keystone endpoint url
# Do not append the port or api version
openstack_networking_service_controller_keystone_service_endpoint_url: 'http://{{ inventory_hostname }}'

openstack_networking_service_controller_keystone_service_endpoint_region: 'RegionOne'

# Define memcached servers
openstack_networking_service_controller_memcached_servers:
  - 127.0.0.1

# Define a suitable secret for the metadata proxy.
openstack_networking_service_controller_metadata_secret: []

# Define the metadata host
openstack_networking_service_controller_nova_metadata_ip: '127.0.0.1'

# Neutron info
## Define Neutron user info
openstack_networking_service_controller_neutron_user_info:
  description: 'Neutron user'
  domain_id: 'default'
  enabled: true
  name: 'neutron'
  # Generate with openssl rand -hex 10
  password: '{{ openstack_networking_service_controller_neutron_user_pass }}'
  project: 'service'
  role: 'admin'
  state: 'present'

## Define Neutron user password
openstack_networking_service_controller_neutron_user_pass: []

# Nova info
openstack_networking_service_controller_nova:
  auth_type: 'password'
  auth_url: '{{ openstack_networking_service_controller_keystone_service_endpoint_url }}:35357'
  password: "{{ openstack_networking_service_controller_nova_user_info['password'] }}"
  project_domain_name: "{{ openstack_networking_service_controller_nova_user_info['domain_id'] }}"
  project_name: "{{ openstack_networking_service_controller_nova_user_info['project'] }}"
  user_domain_name: "{{ openstack_networking_service_controller_nova_user_info['domain_id'] }}"
  username: "{{ openstack_networking_service_controller_nova_user_info['name'] }}"

## Define Nova user info
openstack_networking_service_controller_nova_user_info:
  description: 'Nova user'
  domain_id: 'default'
  enabled: true
  name: 'nova'
  # Generate with openssl rand -hex 10
  password: '{{ openstack_networking_service_controller_nova_user_pass }}'
  project: 'service'
  role: 'admin'
  state: 'present'

## Define Nova user password
openstack_networking_service_controller_nova_user_pass: []

# Provider network info
openstack_networking_service_controller_provider_interface: 'enp0s9'

# RabbitMQ connection info
openstack_networking_service_controller_rabbit_host: 'localhost'
openstack_networking_service_controller_rabbit_pass: 'openstack'
openstack_networking_service_controller_rabbit_user: 'openstack'
```

## Dependencies

### Ansible Roles

The following [Ansible](https://www.ansible.com) roles are required as part of
this role.

-   [ansible-chrony](https://github.com/mrlesmithjr/ansible-chrony)
-   [ansible-config-interfaces](https://github.com/mrlesmithjr/ansible-config-interfaces)
-   [ansible-etc-hosts](https://github.com/mrlesmithjr/ansible-etc-hosts)
-   [ansible-memcached](https://github.com/mrlesmithjr/ansible-memcached)
-   [ansible-mysql](https://github.com/mrlesmithjr/ansible-mysql)
-   [ansible-openstack-base](https://github.com/mrlesmithjr/ansible-openstack-base)
-   [ansible-openstack-compute-service-controller](https://github.com/mrlesmithjr/ansible-openstack-compute-service-controller)
-   [ansible-openstack-identity-service](https://github.com/mrlesmithjr/ansible-openstack-identity-service)
-   [ansible-openstack-image-service](https://github.com/mrlesmithjr/ansible-openstack-image-service)
-   [ansible-openstack-openrc](https://github.com/mrlesmithjr/ansible-openstack-openrc)
-   [ansible-rabbitmq](https://github.com/mrlesmithjr/ansible-rabbitmq)

The above roles can be installed using `ansible-galaxy` along with [requirements.yml](./requirements.yml):

```bash
ansible-galaxy install -r requirements.yml
```

## Example Playbook

[Example Playbook](./playbook.yml)

## License

MIT

## Author Information

Larry Smith Jr.

-   [@mrlesmithjr](https://www.twitter.com/mrlesmithjr)
-   [EverythingShouldBeVirtual](http://www.everythingshouldbevirtual.com)
-   mrlesmithjr [at] gmail.com
