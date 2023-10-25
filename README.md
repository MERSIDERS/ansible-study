## Setting Up Ansible for Multiple Hosts

### Updating the Inventory File
In the `inventory.yml` file, change the `ansible_host` to the address of the desired host.

### Configuring Host Key Fingerprint
To ensure secure SSH connections, add the host key fingerprint of the hosts you plan to use to your `known_hosts` file. You can do this using the following command:

```shell
ssh-keyscan -H ip_address >> ~/.ssh/known_hosts

Scaling Up
In the playbook, we have specified the installation on a specific host from the inventory file. To perform installations on multiple remote machines, make the following adjustments:

1. In the playbook, change hosts: test to hosts: all.

2. In the inventory.yml file, add additional hosts to the hosts section. For example:

all:
  hosts:
    test:
      ansible_host: 172.16.0.71
      ansible_user: mersiders
      ansible_ssh_pass: 1
      ansible_sudo_pass: 1
    node1:
      ansible_host: 172.16.0.68
      ansible_user: mersiders
      ansible_ssh_pass: 1
      ansible_sudo_pass: 1

You can use arbitrary names like test and node1 for your hosts.
