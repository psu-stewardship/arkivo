# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "debian74-puppet"
  # config.vm.box_url = "http://domain.com/path/to/above.box"

  config.vm.define "arkivo" do |arkivo|
    arkivo.vm.network "forwarded_port", guest: 6379, host: 6379

    arkivo.vm.provision "puppet" do |puppet|
      puppet.manifests_path = "puppet/manifests"
      puppet.module_path = "puppet/modules"
      puppet.manifest_file  = "arkivo.pp"
    end
  end

  config.vm.define "scholarsphere" do |ss|

    ss.vm.network "forwarded_port", guest: 3000, host: 6080
    ss.vm.network "forwarded_port", guest: 6379, host: 6079
    ss.vm.network "forwarded_port", guest: 8983, host: 6083

    ss.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
    end

    ss.vm.provision "puppet" do |puppet|
      puppet.manifests_path = "puppet/manifests"
      puppet.module_path = "puppet/modules"
      puppet.manifest_file  = "scholarsphere.pp"
    end
  end
end
