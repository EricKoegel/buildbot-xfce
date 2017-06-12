# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

# Jenkins builders

  config.vm.define "Ubuntu" do |ubuntu|

      ubuntu.vm.hostname="Ubuntu"
      ubuntu.vm.network "private_network", ip: "10.10.10.100"

      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      ubuntu.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/ubuntu-playbook.yml"
            ansible.inventory_path = "ansible/inventory/hosts"
            ubuntu.vm.box = "ubuntu/xenial64"
      end
  end


# The Jenkins master

  config.vm.define "Jenkins" do |jenkins|

      jenkins.vm.hostname = 'Jenkins'
      jenkins.vm.network "forwarded_port", guest: 8080, host: 8080
      jenkins.vm.network "private_network", ip: "10.10.10.10"

      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      jenkins.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/jenkins-playbook.yml"
            ansible.inventory_path = "ansible/inventory/hosts"
            jenkins.vm.box = "ubuntu/xenial64"
      end
  end

end
