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