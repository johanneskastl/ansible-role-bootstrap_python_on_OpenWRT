![Ansible Lint](https://github.com/johanneskastl/ansible-role-bootstrap_python_on_OpenWRT/workflows/Ansible%20Lint/badge.svg)

bootstrap_python_on_OpenWRT
=========

Install python3 and other packages needed for managing OpenWRT via ansible

Requirements
------------

1. You need an OpenWRT device that you want to manage.
2. The device needs to have at least the gateway and DNS server set, so it has basic connectivity and can install packages.
3. You need to have SSH connectivity to the device. This can be the dropbear instance running by default and (by default) allowing root logins, even though the root user does not yet have a password.


Note for myself:
For an example VM with only one single NIC put something like this in `/etc/config/network`:
```
config interface 'lan'
        option device 'br-lan'
        option proto 'static'
        option ipaddr '192.168.1.20'
        option netmask '255.255.255.0'
        option ip6assign '60'
        option gateway '192.168.1.1'
        list dns '192.168.1.1'
```

Role Variables
--------------

None.

Dependencies
------------

None

Example Playbook
----------------

The example playbook disabling gathering of facts, which would fail as no python is installed yet. It disables `become` aka sudo or su, and hardcodes the `root` user.

    - hosts: servers
      gather_facts: 'false'
      become: 'false'
      vars:
        ansible_user: 'root'
      roles:
        - { role: 'johanneskastl.bootstrap_python_on_OpenWRT' }

You can test whether ansible is fully working by pinging the host:

```
ansible -m ping openwrt -e ansible_user=root
[WARNING]: sftp transfer mechanism failed on [openwrt]. Use ANSIBLE_DEBUG=1 to see detailed information
openwrt | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
