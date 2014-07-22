# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # graphite.vm.box = "centos-6-4"
  # graphite.vm.box_url = "https://dl.dropboxusercontent.com/s/z85s74gv74m6flo/centos-6-4.box"
  # graphite.vm.box = "wheezy64"
  # graphite.vm.box_url = "https://dl.dropboxusercontent.com/s/j887m9989t2g8zj/wheezy64.box"
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  private_ip = "10.0.0.20"
  cpu = ENV['VAGRANT_CPU'] || 2
  ram = ENV['VAGRANT_MEMORY'] || 1024

  config.vm.network :private_network, ip: private_ip
  config.vm.network "public_network", bridge: "en0: Ethernet"

  config.vm.provider :virtualbox do |vm, override|
    vm.customize ["modifyvm", :id, "--memory", ram]
    vm.customize ["modifyvm", :id, "--cpus", cpu]
    #vm.gui = true # for debug
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = 'v'
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "vagrant_hosts"
    ansible.limit          = "all"
    ansible.extra_vars     = {
      target: private_ip
    }
  end
end
