# Managing Inventory

## Creating a static Inventory managed hosts

Ansible uses an inventory to describe the systems to be managed using ansible.

Ansible takes advantage of user defined inventory to target the hosts.

In this repo, I will explain how to:

- Implement and use Ansible inventory and host files.
- Explain the format of inventory files.
- Create an inventory files that defines a alist of Linux-based managed hosts, defines groups, and assigns managed hosts to those groups.

### Inventory

- An inventory defines a collection of hosts managed by Ansible.
- Hosts can be assigned to groups.
- Groups can be managed collectively.
- Groups can contain child groups
- Hosts can be members of multiple groups.
- Variables can be set that apply to hosts and groups.

Location of the inventory:

The location is controlled by your current Ansible configuration file
- `ansible --version` should show which configuration is in use

That file specifies the location of the inventory in its [defaults] section:

```INI
[defaults]
inventory = ./inventory
```

If the configuration is not set, `/etc/ansible/hosts` will be used

### Creating an INI-formatted Inventory File

- Host groups allow you to collectively automate a set of systems.

- In the following exampe there are two groups, webservers and db_servers

```INI
[webservers]
web1.example.com
web2.example.com
192.0.2.42

[db_servers]
db1.example.com
db2.example.com
```

### Special Groups and Group Names

- Two host groups exist:
    - All includes every host in the inventory
    - ungrouped includes every host in all that is not a member of another group
- Group names should not include dashes, but underscores are fine.

### Nested groups

- Nested host groups can be added with the `:childeren` suffix.

### Ranges

- It is possible to specify ranges in the host names or IP addresses.
- Both numeric and alphabetic ranges can be specified.
- Ranges match values from [START:END]
- Groups can contain child groups
- For example.
    - 192.168.[4:7].[0:255]

## Managing Connection setting and Privilage Escilation

### Configuring Ansible

The behaviour of an Ansible installation can be customised by modifying settings in the ansible.cfg file. This will be looked for by ansible in the following places:
- ./ansible.cfg
- ~/.ansible.cfg
- /etc/ansible/ansible.cfg

### Managing settings in the cfg file

- ansible.cfg consists of several sections.
- Each section contains settings defined as key-value pairs.
- Section titles are enclosed in square brackets.
- Basic operations use two sections:

```
[defaults] sets defaults for Ansible operation.
[privilege_escalation] configures how Ansible performs privilege escalation on managed hosts.
```

### Connection settings in the cfg file

Settings to control SSH connections go on the [defaults] section

- `remote_user` specifies the user you want to use on the managed host
- `remote_port` specifies what port sshd is using on the managed host
- `ask_pass` controls whether Ansible will prompt you for the SSH password

### Privilege Escalation Settings in the Config file

Setting to control privilege escalation can go on the [privilege_escalation] section:
- `become` controls whether you will automatically use privilege escalation
- `become_user` controls what user on the managed host Ansible should become
- `become_method` controls how Ansible will become that user
- `become_ask_pass` controls whether to prompt you for a password for your become method.

### Host-Based Connection Variables

- Apply settings specific to a particular host by setting connection variables
- Place the settings in a file in the host_vars directory in the same directory as the inventory file.
- These settings override the ones in ansible.cfg
- They also have slighly different syntax naming

### Host based connection and privilege escalation variables

- `ansible_host` specifies a different IP address or hostname to use for the connection for this host instead of the one in the inventory
- `ansible_user` specifies the user you want to use on this host
- `ansible_become_user` specifies the user to become on this host
- `ansible_become_method` specifies the privilege escalation method to use for this host.