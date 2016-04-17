# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

# Check if you have the good Vagrant version to use docker provider...
Vagrant.require_version ">= 1.6.0"

############################
# Install required plugins #
############################
unless Vagrant.has_plugin?("vagrant-managed-servers")
  system("vagrant plugin install plugins/vagrant-managed-servers-0.8.0.dev.gem")
  puts "Dependencies installed, please try the command again."
  exit
end

Vagrant.configure("2") do |config|
  config.vm.box = "tknerr/managed-server-dummy"
  config.ssh.shell = "/bin/sh"
  config.vm.provider :managed do |managed, override|
    docker = %x[docker-machine env default]
    server = /tcp:\/\/([0-9.]+)/.match(docker)[1]
    private_key_path = /DOCKER_CERT_PATH="([^"]+)"/.match(docker)[1] + "/id_rsa"
    managed.server = server
    override.ssh.username = "docker"
    override.ssh.private_key_path = private_key_path
  end
end
