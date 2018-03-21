# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "dockerenv"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "2"
  end
  config.vm.synced_folder "playbook","/home/vagrant/playbook",:mount_options => ['dmode=775','fmode=664']
  config.vm.provision "shell", inline: $script
end

$script = <<END
    if ! [`which ansible`]; then
        yum -y install epel-release
        yum -y install ansible
    fi

    ansible-playbook -i /home/vagrant/playbook/hosts-development /home/vagrant/playbook/site.yml
END
