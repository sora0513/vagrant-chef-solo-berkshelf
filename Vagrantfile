# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  require 'vagrant-vbguest' unless defined? config.vbguest
  config.vbguest.auto_update = false
  
  config.vm.box = "centos"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.1/centos65-x86_64-20131205.box"

  config.vm.define "test1" do |node|
    config.vm.box = "centos"
    node.vm.hostname = "test1"
    node.vm.network :private_network, ip:  "192.168.33.55"
  end

  config.vm.define "test2" do |node|
    config.vm.box = "centos"
    node.vm.hostname = "test2"
    node.vm.network :private_network, ip:  "192.168.33.56"
  end

  config.vm.provision :chef_solo do |chef|
   chef.log_level = :debug
    chef.run_list = [
        "recipe[yum]",
        "recipe[yum-epel]",
        "recipe[apache2]",
        "recipe[apache2::mod_php5]",
        "recipe[apache2::mod_rewrite]",
        "recipe[php]",
        "recipe[mysql::server]",
        "recipe[mysql::client]",
        "recipe[vim]",
        "recipe[git]"
    ]

    chef.json = {
        :apache => {
          :default_site_enabled => true
        },
        mysql: {
          server_root_password: "password",
          bind_address: "127.0.0.1"
        }
    }
  end
  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true
end
