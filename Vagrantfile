# Vagrantfile

Vagrant_API_Version ="2"

Vagrant.configure(Vagrant_API_Version) do |config|

  #haproxy-server
  config.vm.define:"haproxy-server" do |cfg|
     cfg.vm.box = "centos/7"
	 cfg.vm.provider:virtualbox do |vb|
	   vb.name="haproxy-server"
	   vb.customize ["modifyvm", :id, "--cpus",1]
	   vb.customize ["modifyvm", :id, "--memory",1024]
	 end
	 cfg.vm.host_name="haproxy-server"
	 cfg.vm.synced_folder ".", "/vagrant", disabled: true
	 cfg.vm.network "public_network", ip: "192.168.1.11"
	 cfg.vm.network "forwarded_port", guest: 22, host: 19211, auto_correct: false, id: "ssh"
	 cfg.vm.provision "shell", path: "bash_ssh_conf_CentOS.sh"
  end
  
  #web-server01	 
  config.vm.define:"web-server01" do |cfg|
     cfg.vm.box = "centos/7"
	 cfg.vm.provider:virtualbox do |vb|
	   vb.name="web-server01"
	   vb.customize ["modifyvm", :id, "--cpus",1]
	   vb.customize ["modifyvm", :id, "--memory",1024]
	 end
	 cfg.vm.host_name="web-server01"
	 cfg.vm.synced_folder ".", "/vagrant", disabled: true
	 cfg.vm.network "public_network", ip: "192.168.1.12"
	 cfg.vm.network "forwarded_port", guest: 22, host: 19212, auto_correct: false, id: "ssh"
	 cfg.vm.provision "shell", path: "bash_ssh_conf_CentOS.sh"
  end
  
  #web-server02	 
  config.vm.define:"web-server02" do |cfg|
     cfg.vm.box = "centos/7"
	 cfg.vm.provider:virtualbox do |vb|
	   vb.name="web-server02"
	   vb.customize ["modifyvm", :id, "--cpus",1]
	   vb.customize ["modifyvm", :id, "--memory",1024]
	 end
	 cfg.vm.host_name="web-server02"
	 cfg.vm.synced_folder ".", "/vagrant", disabled: true
	 cfg.vm.network "public_network", ip: "192.168.1.13"
	 cfg.vm.network "forwarded_port", guest: 22, host: 19213, auto_correct: false, id: "ssh"
	 cfg.vm.provision "shell", path: "bash_ssh_conf_CentOS.sh"
  end
  
  #Ansible-Server
  config.vm.define:"ansible-server" do |cfg|
     cfg.vm.box = "centos/7"
	 cfg.vm.provider:virtualbox do |vb|
	   vb.name="Ansible-Server"
	 end
	 cfg.vm.host_name="ansible-server"
	 cfg.vm.synced_folder ".", "/vagrant", disabled: true
	 cfg.vm.network "public_network", ip: "192.168.1.10"
	 cfg.vm.network "forwarded_port", guest: 22, host: 19210, auto_correct: false, id: "ssh"
	 cfg.vm.provision "shell", path: "bootstrap.sh"
	 cfg.vm.provision "file", source: "Ansible_env_ready.yml", destination: "Ansible_env_ready.yml"
	 cfg.vm.provision "shell", inline: "ansible-playbook Ansible_env_ready.yml"
	 cfg.vm.provision "file", source: "Auto_known_host.yml", destination: "Auto_known_host.yml"
	 cfg.vm.provision "shell", inline: "ansible-playbook Auto_known_host.yml", privileged: false
	 cfg.vm.provision "file", source: "Auto_authorized_keys.yml", destination: "Auto_authorized_keys.yml"
	 cfg.vm.provision "shell", inline: "ansible-playbook Auto_authorized_keys.yml --extra-vars 'ansible_ssh_pass=vagrant'", privileged: false
	 cfg.vm.provision "file", source: "httpd_install.zip", destination: "httpd_install.zip"
	 cfg.vm.provision "shell", inline: "yum -y install unzip"
	 cfg.vm.provision "shell", inline: "unzip httpd_install.zip", privileged: false
	 cfg.vm.provision "shell", inline: "ansible-playbook httpd_install/Configure_httpd.yml", privileged: false
	 cfg.vm.provision "file", source: "haproxy.cfg", destination: "haproxy.cfg"
	 cfg.vm.provision "file", source: "haproxy_install.yml", destination: "haproxy_install.yml"
	 cfg.vm.provision "shell", inline: "ansible-playbook haproxy_install.yml", privileged: false
  end
  
end