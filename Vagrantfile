Vagrant.configure("2") do |config|

# Webserver
  config.vm.box = "ubuntu/trusty64"
  # Virtualbox Einstellungen
  config.vm.box_check_update = false
  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "2024"
      vb.cpus = "2"
  end
  # Shellbefehle die beim Vagrant UP ausgeführt werden sollen
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
    apt-get install -y nginx
    service nginx start
  SHELL
  # Netzwerk Einstelungen
  config.vm.network "private_network", ip: "192.168.33.10"
end







