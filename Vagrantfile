# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "graphite" do |graphite|
    # graphite.vm.box = "centos-6-4"
    # graphite.vm.box_url = "https://dl.dropboxusercontent.com/s/z85s74gv74m6flo/centos-6-4.box"
    # graphite.vm.box = "wheezy64"
    # graphite.vm.box_url = "https://dl.dropboxusercontent.com/s/j887m9989t2g8zj/wheezy64.box"

    graphite.vm.box = "precise64"
    graphite.vm.box_url = "http://files.vagrantup.com/precise64.box"

    graphite.vm.network :private_network, ip: "10.0.0.20"

    #graphite.vm.network :public_network
    #graphite.vm.network "forwarded_port", guest: 80, host: 50080 #graphana
    #graphite.vm.network "forwarded_port", guest: 8080, host: 58080 #graphite
    #graphite.vm.network "forwarded_port", guest: 2003, host: 52003
    #graphite.vm.network "forwarded_port", guest: 8125, host: 58125, protocol: 'udp'

    graphite.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "configuration.yml"
    end
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end

end
