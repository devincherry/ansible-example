VAGRANTFILE_API_VERSION = '2'.freeze

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.private_key_path = '.vagrant_ssh_private_key'
  config.ssh.insert_key = false
  config.vbguest.auto_update = true
  config.vm.network 'private_network', type: 'dhcp'
  config.vm.provider 'virtualbox' do |vb|
    vb.cpus = 1
  end

  ##############################################################################
  # NOTE:
  #
  #   - Change [configs/hosts] "vagrant_boxes" group to include the
  #     machine IP you want to test from below.
  #   - Change the relevant task(s) in [configs/vagrant.yml] to run on
  #     the "vagrant_boxes" hosts.
  ##############################################################################

  config.vm.define :ubuntu14 do |u14|
    u14.vm.box = 'ubuntu/trusty64'
    u14.vm.hostname = 'ubuntu14.04'
    u14.vm.network 'private_network', ip: '192.168.77.118'
  end

  config.vm.define :centos6 do |c6|
    c6.vm.box = 'centos/6'
    c6.vm.hostname = 'centos6-vbox'
    c6.vm.network 'private_network', ip: '192.168.77.119'
  end

  config.vm.define :centos7 do |c7|
    c7.vm.box = 'centos/7'
    c7.vm.hostname = 'centos7-vbox'
    c7.vm.network 'private_network', ip: '192.168.77.120'
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.limit = 'vagrant_boxes'
    ansible.playbook = 'configs/vagrant.yml'
    ansible.inventory_path = 'configs/hosts'
    ansible.ask_vault_pass = true
    ansible.raw_arguments = [
      '--private-key=.vagrant_ssh_private_key'
    ]
  end
end
