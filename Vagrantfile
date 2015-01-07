# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.provider 'docker' do |d|
    d.vagrant_vagrantfile = './Vagrantfile.host'
    d.image = 'redis:latest'
  end
end
