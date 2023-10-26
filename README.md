## Setting Up Ansible for Multiple Hosts

### Updating the Inventory File
In the `inventory.yml` file, change the `ansible_host` to the address of the desired host.

### Configuring Host Key Fingerprint
To ensure secure SSH connections, add the host key fingerprint of the hosts you plan to use to your `known_hosts` file. You can do this using the following command:

```shell
ssh-keyscan -H ip_address >> ~/.ssh/known_hosts
```
Scaling Up
In the playbook, we have specified the installation on a specific host from the inventory file. To perform installations on multiple remote machines, make the following adjustments:

1. In the playbook, change hosts: test to hosts: all.

2. In the inventory.yml file, add additional hosts to the hosts section. For example:
```shell
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
```
You can use arbitrary names like test and node1 for your hosts.


The command to run:
```shell
ansible-playbook -i inventory.yml proxy-ipv4-kiev.yml
```

### Control Task Execution
Using vars.yml to Control Task Execution.
The vars.yml file is designed to allow users to control which tasks are executed in the playbook. It contains variables that determine whether a task should be executed or skipped. To configure the vars.yml file, follow these steps:
1. Open the vars.yml file in a text editor.
2. In vars.yml, you will find a set of variables with corresponding task names, for example:
```shell
enable_disable_tasks:
  disable_ipv6: true
  set_timezone: true
  update_packages: true
  install_nginx: true
```
3. To enable a task, set the corresponding variable to true. To disable a task, set it to false.
4. Save the vars.yml file after making your changes.
Now, when you run your playbook, it will check the values in vars.yml to determine which tasks to execute. If a variable is set to true, the corresponding task will be executed; if set to false, the task will be skipped.
