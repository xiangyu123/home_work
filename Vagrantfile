IMAGE_NAME = "luisico/centos-7.5-docker"
BOX_VERSION = "18.06.0"

Vagrant.configure("2") do |config|
    config.ssh.insert_key = true
    config.vbguest.auto_update = false
    #config.vm.network :public_network,:bridge=>'en0: Wi-Fi (AirPort)'
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    config.vm.network "forwarded_port", guest: 8083, host: 8083

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
      
    config.vm.define "docker-machine" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.box_version = BOX_VERSION
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "docker-machine"
    end
    config.vm.provision "shell", inline: <<-SHELL
      sudo yum -y install epel-release
      sudo yum clean all
      sudo yum -y install java-11-openjdk.x86_64 git python-jenkins
      git clone https://github.com/xiangyu123/Jenkins.git
      sudo cat > /etc/docker/daemon.json << EOF
{
  "registry-mirrors": [
    "https://registry.mirrors.aliyuncs.com",
    "https://euy3vpdg.mirror.aliyuncs.com"
  ]
}
EOF
      sudo systemctl restart firewalld
      sudo systemctl restart docker
    SHELL
end
