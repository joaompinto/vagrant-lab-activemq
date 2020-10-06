# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
config_yml = YAML.load_file(File.open(File.expand_path(File.dirname(__FILE__)) + "/vagrant-config.yml"))


# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config_yml[:vms].each do |name, settings|
    # use the config key as the vm identifier
    config.vm.define(name) do |vm_config|

      # Debian 8 (jessie), currently the default case
      vm_config.vm.box                   = "centos/7"


      # NOTE right place to store the project files? Overwrite /etc/puppet?
      vm_config.vm.synced_folder "./", "/vagrant"

      # assign an ip address in the hosts network
      vm_config.vm.network "private_network", ip: settings[:ip]

      vm_config.vm.hostname = settings[:hostname]

      config.vm.provider "virtualbox" do |v|
        # make sure that the name makes sense when seen in the vbox GUI
        v.name = settings[:hostname]

      end
      
      config.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
        s.inline = <<-SHELL
          echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        SHELL
      end
    end
  end
end
