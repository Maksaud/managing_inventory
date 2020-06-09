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