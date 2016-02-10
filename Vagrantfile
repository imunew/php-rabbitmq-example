# -*- coding: utf-8 -*-
# -*- mode: ruby; -*-
# -*- coding: utf-8; -*-
# vi: set ft=ruby; :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = 'centos65'

  config.vm.box_url = 'https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box'
  #config.vm.box_url = 'https://github.com/2creatives/vagrant-centos/releases/download/v6.5.1/centos65-x86_64-20131205.box'

  config.vm.network :private_network, ip: '192.168.101.11'
  config.vm.network :forwarded_port, guest: 443, host: 8443, auto_correct: true

  if ENV['USE_NFS']
    config.vm.synced_folder './', '/apps', :nfs => true
  else
    config.vm.synced_folder './', '/apps', :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777','fmode=777']
  end

  config.vm.provider :virtualbox do |vb|

    unless defined? config.vbguest
      require 'vagrant-vbguest'
      config.vbguest.auto_update = false
    end

    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ['modifyvm', :id, '--memory', '1024']

    # やたらネットワークが遅い現象の対策 (ipv6絡み)
    # see https://github.com/mitchellh/vagrant/issues/1172
    vb.customize ['modifyvm', :id, '--natdnsproxy1', 'off']
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']

  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook       = 'ansible/vagrant.yml'
    ansible.inventory_path = 'ansible/vagrant'
    ansible.limit          = 'all'
    ansible.verbose        = true
  end
end
