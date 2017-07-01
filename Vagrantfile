# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

# The Jenkins master

  config.vm.define "Jenkins" do |jenkins|

      jenkins.vm.hostname = 'Jenkins'
      # The jenkins master needs to run on an LTS release for the
      # geerlingguy.java role
      jenkins.vm.box = "ubuntu/xenial64"
      jenkins.vm.network :forwarded_port, guest: 8080, host: 8080
      jenkins.vm.network :private_network, ip: "10.10.10.10"
      jenkins.vm.boot_timeout = 600

      config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      config.vm.provider :virtualbox do |v|
            v.name = "Jenkins"
            v.memory = 1024
            v.cpus = 1
            v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
            v.customize ["modifyvm", :id, "--ioapic", "on"]
      end
  end


# Jenkins builders start here

  config.vm.define "Ubuntu" do |ubuntu|

      ubuntu.vm.hostname="Ubuntu"
      ubuntu.vm.box = "ubuntu/yakkety64"
      ubuntu.vm.network :private_network, ip: "10.10.10.100"
      ubuntu.vm.boot_timeout = 600

      #config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      config.vm.provider :virtualbox do |v|
            v.name = "Ubuntu"
            v.memory = 512
            v.cpus = 2
            v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
            v.customize ["modifyvm", :id, "--ioapic", "on"]
      end
  end


  config.vm.define "Debian" do |debian|

      debian.vm.hostname="Debian"
      debian.vm.box = "debian/stretch64"
      debian.vm.network :private_network, ip: "10.10.10.101"
      debian.vm.boot_timeout = 600

      #config.vm.synced_folder ".", "/vagrant", type: "rsync"

      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      config.vm.provider :virtualbox do |v|
            v.name = "Debian"
            v.memory = 512
            v.cpus = 2
            v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
            v.customize ["modifyvm", :id, "--ioapic", "on"]
      end
  end

  config.vm.define "FreeBSD" do |freebsd|

      freebsd.vm.hostname="FreeBSD"
      freebsd.vm.box = "freebsd/FreeBSD-12.0-CURRENT"
      freebsd.vm.network :private_network, ip: "10.10.10.102"
      freebsd.vm.boot_timeout = 600

      config.vm.base_mac = "080027D14C66"
      #config.vm.synced_folder ".", "/vagrant", type: "rsync"

      config.ssh.shell = "sh"
      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      config.vm.provider :virtualbox do |v|
            v.name = "FreeBSD"
            v.memory = 512
            v.cpus = 2
            v.customize ["modifyvm", :id, "--hwvirtex", "on"]
            v.customize ["modifyvm", :id, "--audio", "none"]
            v.customize ["modifyvm", :id, "--nictype1", "virtio"]
            v.customize ["modifyvm", :id, "--nictype2", "virtio"]
      end
  end

  config.vm.define "OpenBSD" do |openbsd|

      openbsd.vm.hostname="OpenBSD"
      openbsd.vm.box = "trombik/ansible-openbsd-6.0-amd64"
      openbsd.vm.network :private_network, ip: "10.10.10.103"
      openbsd.vm.boot_timeout = 600

      #config.vm.synced_folder ".", "/vagrant", type: "rsync"

      config.ssh.shell = "sh"
      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      config.vm.provider :virtualbox do |v|
            v.name = "OpenBSD"
            v.memory = 512
            v.cpus = 2
      end
  end

  config.vm.define "OpenIndiana" do |openindiana|

      #openindiana.vm.hostname="OpenIndiana"
      openindiana.vm.box = "openindiana/hipster"
      #openindiana.vm.network "private_network", ip: "10.10.10.104"
      openindiana.vm.boot_timeout = 600

      config.ssh.shell = "sh"
      config.ssh.forward_agent = true
      config.ssh.forward_x11 = true

      config.vm.provider :virtualbox do |v|
            v.name = "OpenIndiana"
            v.memory = 2048
            v.cpus = 2
      end
  end

# Ansible configuration here, add new builders to jenkins_builders

  config.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/site.yml"
            #ansible.verbose = true
            #ansible.verbose = "vvv"

            ansible.groups = {
                  "jenkins_master" => ["Jenkins"],
                  "jenkins_builders" => ["Ubuntu", "FreeBSD", "OpenBSD", "Debian", "OpenIndiana"],
            }

            ansible.host_vars = {
                  "FreeBSD" => { "ansible_python_interpreter" => "/usr/local/bin/python" },
                  "OpenBSD" => { "ansible_python_interpreter" => "/usr/local/bin/python" },
            }
  end
end
