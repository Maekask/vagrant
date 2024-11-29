Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 600

  config.vm.define "mart-dockerhost" do |dockerhost|
    dockerhost.vm.box = "generic/debian12"
    dockerhost.vm.network "private_network", ip: "10.10.10.130", netmask: "255.255.255.128"
    dockerhost.vm.hostname = "mart-dockerhost"
    dockerhost.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "mart-dockerhost"
    end
    dockerhost.vm.synced_folder "./docker_data", "/vagrant_data"
    dockerhost.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git
      apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
      curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
      apt-get update
      apt-get install -y docker-ce docker-ce-cli containerd.io
      systemctl enable docker
      systemctl start docker
    SHELL
  end

  config.vm.define "mart-ansible" do |ansible|
    ansible.vm.box = "generic/debian12"
    ansible.vm.network "private_network", ip: "10.10.10.131", netmask: "255.255.255.128"
    ansible.vm.hostname = "mart-ansible"
    ansible.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "mart-ANSIBLE"
    end
    ansible.vm.synced_folder "./ansible_data", "/vagrant_data"
    ansible.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git ansible sshpass yamllint ansible-lint
    SHELL
  end

  config.vm.define "mart-ubuntu" do |ubuntu|
    ubuntu.vm.box = "bento/ubuntu-24.04"
    ubuntu.vm.network "private_network", ip: "10.10.10.132", netmask: "255.255.255.128"
    ubuntu.vm.hostname = "mart-ubuntu"
    ubuntu.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "mart-UBUNTU"
    end
    ubuntu.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git
    SHELL
  end

  config.vm.define "mart-centos" do |centos|
    centos.vm.box = "generic/centos9s"
    centos.vm.network "private_network", ip: "10.10.10.133", netmask: "255.255.255.128"
    centos.vm.hostname = "mart-centos"
    centos.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "mart-CENTOS"
    end
    centos.vm.provision "shell", inline: <<-SHELL
      yum update -y
      yum install -y net-snmp net-snmp-utils tmux mc wget tree git
    SHELL
  end

  config.vm.define "mart-opensuse" do |opensuse|
    opensuse.vm.box = "bento/opensuse-leap-15"
    opensuse.vm.network "private_network", ip: "10.10.10.134", netmask: "255.255.255.128"
    opensuse.vm.hostname = "mart-opensuse"
    opensuse.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "mart-OPENSUSE"
    end
    opensuse.vm.provision "shell", inline: <<-SHELL
      zypper refresh
	  zypper update -y
      zypper install -y tmux mc wget tree git net-snmp
    SHELL
  end

end
