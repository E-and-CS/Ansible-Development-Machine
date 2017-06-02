# This Vagrantfile tells Vagrant how to stand up a Virtualbox machine running Ubuntu Server.
# It then tells the server to install Ansible, and then use Ansible to make system changes.
#
# You must have at least:
# * Vagrant from https://vagrantup.com
# * Virtualbox from https://virtualbox.org
# * The *SAME VERSION* extensions from Virtualbox as the version you've downloaded
#
# Install Virtualbox, then install the Extension to Virtualbox, then finally Vagrant.
# It doesn't really matter if you do Vagrant and Virtualbox the other way around, but
# you *need* the extension pack for Virtualbox, otherwise the disks won't mount.

# While it is not a requirement, I would suggest you install the following plugin for Vagrant:
# vagrant plugin install vagrant-vbguest

Vagrant.configure("2") do |config|
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/xenial64"
    ubuntu.vm.hostname = "ubuntu"
    ubuntu.vm.box_check_update = false
    ubuntu.vm.boot_timeout = 1200

    ubuntu.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
      # For some reason, the latest version of Vagrant/Virtualbox causes problems with shared drives that have options set
      vb.customize ['sharedfolder', 'add', :id, '--name', 'HostHome', '--hostpath', ENV['USERPROFILE']]
    end

    # Perform standard user account changes
    ubuntu.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "ansible_users.yml"
      ansible.install        = true
      ansible.inventory_path = "inventory"
    end

    # Mount the shared volumes and manage the links
    ubuntu.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "ansible_mounts.yml"
      ansible.install        = true
      ansible.inventory_path = "inventory"
    end
    
    # Install any extra software required
    ubuntu.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "ansible_software.yml"
      ansible.inventory_path = "inventory"
    end
  end
end