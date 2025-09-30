Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"  
  config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", type: "dhcp"  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024" 
    vb.cpus = 1  
  end

  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/tmp/host_key.pub"

  config.vm.provision "shell", inline: <<-SHELL
    if [ -f /tmp/host_key.pub ]; then
      echo "SUCCESS: SSH-ключ успешно скопирован с хоста в /tmp/host_key.pub"
    else
      echo "ERROR: Не удалось скопировать SSH-ключ. Проверь, существует ли ~/.ssh/id_rsa.pub на хосте."
      exit 1
    fi

    if ! id -u devops >/dev/null 2>&1; then
      sudo useradd -m -s /bin/bash devops
      echo 'devops:password' | sudo chpasswd
      sudo usermod -aG sudo devops
    fi

    sudo mkdir -p /home/devops/.ssh
    sudo chmod 700 /home/devops/.ssh
    sudo cat /tmp/host_key.pub >> /home/devops/.ssh/authorized_keys
    sudo chown -R devops:devops /home/devops/.ssh
    sudo rm /tmp/host_key.pub

    echo "Provisioning завершён: Пользователь devops создан, SSH настроен."
SHELL
    
end