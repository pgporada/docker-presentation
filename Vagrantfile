# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "geerlingguy/centos7"
  config.vm.network "private_network", ip: "10.1.10.11"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end
  config.vm.provision "shell", inline: <<-SHELL
    sudo hostnamectl set-hostname phils-docker-demo
    sudo timedatectl set-timezone America/Detroit

    # Curling into sh is bad practice.
    # This is for a DEMO!!!
    curl -fsSL https://get.docker.com/ | sudo sh
    sudo systemctl enable docker
    sudo systemctl start docker

    # Docker Compose
    LINK=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep "$(uname -s)-$(uname -m)" | grep browser_download_url | sed 's/"//g' | awk '{print $2}')
    echo "Installing docker-compose from ${LINK}."
    echo "This will take some time."
    sudo sh -c "curl -sL ${LINK} > /bin/docker-compose"
    sudo chmod +x /bin/docker-compose
    echo "The vagrant IP is: 10.1.10.11"
  SHELL
end
