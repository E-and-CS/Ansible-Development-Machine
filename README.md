# K5 Ansible and Openstack Development Machine

This Virtual Machine Template defines how to stand up a virtual machine for certain 
activities, primarily here covering running ansible commands or python-openstackclient 
commands against K5 (but probably against any Openstack environment).

To use this, you must have [Vagrant](https://vagrantup.com) installed, 
[Virtualbox](https://virtualbox.org) installed and the Virtualbox Extension Pack (from the 
download page on the Virtualbox site) installed.

Clone this repository onto your machine somewhere, review and edit the files 
[`Vagrantfile`](https://github.com/JonTheNiceGuy/K5-Ansible-Openstack-Development-Machine/blob/master/Vagrantfile), 
and [`group_vars\all.yml`](https://github.com/JonTheNiceGuy/K5-Ansible-Openstack-Development-Machine/blob/master/group_vars/all.yml)
then run the command `vagrant up`

If you're running a Linux based OS, then you might need to change the line in the Vagrantfile
which specifies the sharedfolder (at the time of writing, that's 
[line 39](https://github.com/JonTheNiceGuy/K5-Ansible-Openstack-Development-Machine/blob/master/Vagrantfile#L39).

Hope this helps you work with Ansible and Openstack!
