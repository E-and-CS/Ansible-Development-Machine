# This is a work in progress

This means that if you find something wrong in here, please let me know! Create
issues in the github repo, or even better, make changes in your own fork and
raise pull requests!

If you're stuck, I'm *MORE* than happy to receive emails asking for help! Please
let me know what you need!!

# K5 Ansible and Openstack Development Machine

This provisions a Vagrant machine, running (eventually) an Ubuntu 18.04 Machine
(optionally with a desktop environment) in Virtualbox, but including the
`openstack` command and the ability to use Ansible against the K5 OpenStack
environment. More recent versions also now include the `az` command for working
with the Microsoft Azure platform.

To use this, you must have [Vagrant](https://vagrantup.com) installed,
[Virtualbox](https://virtualbox.org) installed and it is recommended that you
have the Virtualbox Extension Pack (from the download page on the Virtualbox
site) installed.

It adds a user account with your credentials (provided you configure them in
`group_vars\all\credentials.yml`), and can optionally use a caching proxy
(such as `apt-cachier-ng`) if you have one in your network.

This build mounts two directories - /HostHome and /HostHomeExec - against the
host machine's user home directory. I personally create the following links
in the machine:

* `/HostHome/Standard_Build/dotfiles/ssh` to `$HOME/.ssh`
* `/HostHomeExec/Standard_Build/bin` to `$HOME/bin`

This means that for the files that shouldn't have the exec bits set (SSH keys,
etc.) I can use the /HostHome path for them, but for the paths that do require
exec bits (like scripts), then they can be executed at will.

## Exercise for the reader

* Without changes, the standard build gives you an Ubuntu Server build. If you
tweak the group_vars/all/vars.yml and configure the value `DesktopEnvironment`
with one of the options there (`ubuntu-desktop`, `kubuntu-desktop`,
`lubuntu-desktop`, `xubuntu-desktop` or `ubuntu-mate-desktop`) then these will
install official flavours of Ubuntu into your Virtual Machine (note, these will)
take a LONG time to install.
