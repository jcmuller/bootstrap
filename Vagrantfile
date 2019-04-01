Vagrant.configure('2') do |config|
  config.vm.box = 'generic/ubuntu1810'
  config.vm.synced_folder '.', '/vagrant'

  config.vm.provider 'virtualbox' do |vb|
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end

  config.vm.provision 'shell', inline: <<-SHELL
    apt-get update
    apt-get install -y ansible
  SHELL

  config.vm.provision 'ansible_local', install: false do |ansible|
    ansible.playbook_command = 'ansible-playbook -vvv -e secrets_tarball=/vagrant/secrets.tar.gz'
    ansible.playbook = 'provision.yml'
  end
end
