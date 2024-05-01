# ss
SS labs
Vagrant:-
Vagrant.configure("2") do |config|
  # Configuration for Ubuntu VMs
  (1..3).each do |i|
    config.vm.define "ubuntu#{i}" do |ubuntu|
      ubuntu.vm.box = "generic/ubuntu2004"
      ubuntu.vm.hostname = "ubuntu#{i}"
      ubuntu.vm.network "private_network", ip: "192.168.56.#{i + 10}"
      ubuntu.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        sudo apt-get install -y apache2
      SHELL
    end
  end
  
  # Configuration for CentOS VMs
  (1..2).each do |i|
    config.vm.define "centos#{i}" do |centos|
      centos.vm.box = "generic/centos8"
      centos.vm.hostname = "centos#{i}"
      centos.vm.network "private_network", ip: "192.168.56.#{i + 20}"
      centos.vm.provision "shell", inline: <<-SHELL
        sudo yum install -y httpd
        sudo systemctl start httpd
        sudo systemctl enable httpd
      SHELL
    end
  end
end
