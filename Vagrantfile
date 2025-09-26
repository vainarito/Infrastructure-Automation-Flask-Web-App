Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"  
  config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", type: "dhcp"  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024" 
    vb.cpus = 1  
  end
end