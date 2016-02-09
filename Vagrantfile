## -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

#########################################################
# Looks for a settings file related to a given provider #
#########################################################
def load_settings(file)
  dir = File.dirname(File.expand_path(__FILE__))
  if !File.exist?("#{dir}/vagrant/#{file}.yml")
    FileUtils.mv("example.#{dir}/vagrant/#{file}.yml", "#{dir}/vagrant/#{file}.yml")
    if !File.exist?("#{dir}/vagrant/#{file}.yml")
      raise "Settings file not found! Please copy vagrant/example.#{file}.yml to vagrant/#{file}.yml and try again."
    end
  end
  YAML.load_file "#{dir}/vagrant/#{file}.yml"
end

##################################################
# Maps the ports given in the providers settings #
##################################################
def map_ports(override, settings)
  for port_mapping in settings['ports'];
    override.vm.network "forwarded_port", guest: port_mapping['guest'], host: port_mapping['host']
  end
end

############################
# Install required plugins #
############################
unless Vagrant.has_plugin?("vagrant-triggers") and Vagrant.has_plugin?("vagrant-docker-compose")
  system("vagrant plugin install vagrant-triggers")
  system("vagrant plugin install vagrant-docker-compose")
  puts "Dependencies installed, please try the command again."
  exit
end

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do | config |
  settings = load_settings 'virtualbox'
  config.vm.box = settings['box']
  config.ssh.insert_key = true
  config.vm.network "private_network", type: "dhcp"
  ports = load_settings 'ports'
  map_ports config, ports
  config.vm.provision :docker_compose
  config.vm.provider :virtualbox do | provider |
    provider.name = "livingstone"
    provider.cpus = settings['cpus']
    provider.memory = settings['memory']
  end

  config.trigger.after :up do
    run "./scripts/install-docker"
    run "./scripts/docker-compose-up"
  end

  config.trigger.after :destroy do
    run "./scripts/remove-docker-machine"
  end

end
