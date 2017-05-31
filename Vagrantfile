# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "xenial64"
  config.vm.box_url = "http://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"

  config.vm.network :private_network, ip: "192.168.33.15"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--name", "MyCoolApp", "--memory", "1024"]
  end

  # Shared folder from the host machine to the guest machine. Uncomment the line
  # below to enable it.
  #config.vm.synced_folder "../../../my-cool-app", "/webapps/mycoolapp/my-cool-app"

  # 16.04 first requires that you install Python
  # before you can run ansible
  config.vm.provision "shell" do |s|
    s.inline = "apt-get install -y python"
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.host_key_checking = false
    ansible.verbose = "vv"
  end
end