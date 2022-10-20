#Atividade Vagrant 
#Tiago Norato

# -*- mode: ruby -*-
# vi: set ft=ruby :

$script_ubuntu = <<-EOF
sudo apt update
sudo apt install vim -y
sudo apt install net-tools -y
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce -y
EOF

$script_Win = <<-EOF
Install-Module -Name PSWindowsUpdate -S
Get-WindowsUpdate
EOF

$script_centos = <<-EOF
sudo yum check-update
curl -fsSL https://get.docker.com/ | sh
sudo systemctl status docker
sudo systemctl enable docker
sudo usermod -aG docker $(whoami)
EOF

$script_Fedora = <<-EOF
dnf -y update vs dnf -y upgrade
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager \
--add-repo \
https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf -y install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo docker run hello-world
EOF

Vagrant.configure("2") do |config|
  config.vm.define "ubuntu-18" do |ubuntu_18|
  ubuntu_18.vm.box = "hashicorp/bionic64"
  ubuntu_18.vm.network "private_network", ip: "10.0.0.20"
  ubuntu_18.vm.provider "hyperv" do |hv|
    hv.vmname = "ubuntu-18"
    hv.memory = "1024"
    hv.cpus   = "1"
  ubuntu_18.vm.provision "shell", inline: $script_ubuntu
  end
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "windows-10" do |windows_10|
  windows_10.vm.box = "gusztavvargadr/windows-10"
  windows_10.vm.network "private_network", ip: "10.0.0.10"
  windows_10.vm.provider "hyperv" do |hv|
    hv.vmname = "windows-10"
    hv.memory = "2048"
    hv.cpus   = "2"
  windows_10.vm.provision "shell", inline: $script_Win
  end
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "centos-7" do |centos_7|
  centos_7.vm.box = "centos/7"
  centos_7.vm.network "private_network", ip: "10.0.0.30"
  centos_7.vm.provider "hyperv" do |hv|
    hv.vmname = "centos-7"
    hv.memory = "1024"
    hv.cpus   = "1"
  centos_7.vm.provision "shell", inline: $script_centos
  end
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "fedora-28" do |fedora_28|
  fedora_28.vm.box = "generic/fedora28"
  fedora_28.vm.provider "hyperv" do |hv|
    hv.vmname = "fedora-28"
    hv.memory = "1024"
    hv.cpus   = "1"
  fedora_28.vm.provision "shell", inline: $script_Fedora
  end
  end
end