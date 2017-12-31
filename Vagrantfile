Vagrant.configure("2") do |config|
  config.vm.box = "envimation/ubuntu-xenial"
  config.ssh.forward_agent = true
  config.vm.network "public_network"
  config.vm.network "forwarded_port", guest: 34197, host: 34197, protocol: "udp"
  config.vm.network "forwarded_port", guest: 27015, host: 27015

  config.vm.provider "virtualbox" do |vb|
    vb.name = "Factorio"
    vb.gui = true
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y \
	  apt-transport-https \
      ca-certificates \
      curl \
      software-properties-common
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"
	apt-get update
	sudo apt-get install -y \
	  docker-ce \
	  git \
	  wget \
	  nano
	curl -sSL https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
	chmod 755 /usr/local/bin/docker-compose
	mkdir -p /vagrant/factorio
	chown vagrant:vagrant /vagrant/factorio
	cd /vagrant
	docker-compose up -d
  SHELL
end
