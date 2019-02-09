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
#
# Also, if you're destroying and rebuilding this machine frequently, or building other VMs based
# on this release of Ubuntu, you could install the following plugin for Vagrant:
# vagrant plugin install vagrant-cachier

Vagrant.configure("2") do |config|
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/bionic64"
    ubuntu.vm.hostname = "ubuntu"
    ubuntu.vm.box_check_update = false
    ubuntu.vm.boot_timeout = 1200
    if Vagrant.has_plugin?("vagrant-cachier")
      ubuntu.cache.scope = :box
    end

    ubuntu.vm.provider "virtualbox" do |vb|
      #############################################################################################
      ### BASIC DETAILS
      #############################################################################################
      ##
      ## This tells Virtualbox to call the machine "Ubuntu" in the Virtualbox application and in
      ## any API calls it makes. It does not affect the hostname at all.
      vb.name = "ubuntu"
      #############################################################################################
      ### DRIVE MOUNTING
      #############################################################################################
      ##
      ## For some reason, the latest version of Vagrant/Virtualbox causes problems with shared
      ##  drives that have options set. This also means we can mount the folder "twice" - once
      ##  with permissions 0700 and the other with 0600 on files.
      ##
      vb.customize ['sharedfolder', 'add', :id, '--name', 'HostHome', '--hostpath', ENV['USERPROFILE']]
      #############################################################################################
      ### USING A GUI - COMMON OPTIONS
      #############################################################################################
      ##
      ## Uncomment these for GUI based systems. If you're doing this, also select a desktop environment
      ## ino the group_vars/all.yml file. I use Kubuntu, but you might want one of the others!
      ##
      ## Personally, when using a GUI, I like more memory and CPUs, but you might want to vary these
      ## based on your own machine
      ##
      # vb.memory = 2048
      # vb.cpus = 2
      ##
      ## This gives you more video RAM (required for modern desktop modes)
      ##
      # vb.customize ['modifyvm', :id, '--vram', '128']
      ##
      ## Optionally, turn on the option to use USB devices. If you're working "headlessly", you
      ## might need to mess around with the Virtualbox app to get the "USB Filters" sorted.
      ##
      # vb.customize ['modifyvm', :id, '--usbxhci', 'on']
      #############################################################################################
      ### USING A GUI - USING THE VIRTUALBOX APP TO RENDER THE GUI
      #############################################################################################
      ##
      ## This tells Vagrant to boot this VM in GUI mode. Leave off if you're going to use RDP to access it.
      ##
      # vb.gui = true
      ##
      ## If you are using the GUI, these settings might be useful!
      ##
      # vb.customize ['modifyvm', :id, '--monitorcount', '3']
      # vb.customize ['modifyvm', :id, '--draganddrop', 'bidirectional']
      # vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']  
      #############################################################################################
      ### USING A GUI - USING A REMOTE DESKTOP APPLICATION TO RENDER THE GUI
      #############################################################################################
      ##
      ## This is RDP mode. Settings here based on:
      ## https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm-vrde
      ##
      # vb.customize ["modifyvm", :id, "--vrde", 'on']
      # vb.customize ["modifyvm", :id, "--vrdeport", '12345']
      # vb.customize ["modifyvm", :id, "--vrdeaddress", '127.0.0.1']
    end

    # Perform standard user account changes
    ubuntu.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "ansible_users.yml"
      ansible.install_mode   = "pip"
      ansible.inventory_path = "inventory"
    end

    # Install any extra software required
    ubuntu.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "ansible_software.yml"
      ansible.inventory_path = "inventory"
    end
  end
end
