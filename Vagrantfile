# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"
  config.ssh.forward_x11 = true


  #config.vm.network "private_network", ip: "192.168.254.21"

  config.vm.provider 'virtualbox' do |v, override|
    v.customize ["modifyvm", :id, "--nictype1", "virtio"]
    v.memory = 1024
  end
  config.vm.network "forwarded_port", guest: 5901, host: 5901, host_ip: "127.0.0.1", protocol: "tcp"
  config.vm.network "forwarded_port", guest: 5901, host: 5901, host_ip: "127.0.0.1", protocol: "udp"


  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end

#  if Vagrant.has_plugin?("vagrant-cachier")
#    config.cache.scope = :box
#    config.cache.synced_folder_opts = {
#      type: :nfs,
#      mount_options: ['rw', 'vers=3', 'tcp', 'nolock']
#    }
#    config.cache.enable :pip
#  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.yum_proxy.http     = "http://10.0.2.2:3128/"
    config.git_proxy.http     = "http://10.0.2.2:3128/"
    config.proxy.no_proxy = "localhost,127.0.0.1,.example.com"
  end
end
