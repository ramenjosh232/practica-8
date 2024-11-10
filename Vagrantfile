# Configuración de Vagrant
Vagrant.configure("2") do |config|
  
  # Configuración de la máquina virtual
  config.vm.box = "ubuntu/bionic64"  # Usamos Ubuntu 18.04 como sistema base
  
  # Configuración de red con IP estática para evitar conflictos de DHCP
  config.vm.network "private_network", ip: "192.168.56.10"

  # Configuración de hardware
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"  # Asignar 512 MB de RAM
    vb.cpus = 1        # Asignar 1 CPU
  end

  # Compartir la carpeta local con el servidor web de Apache
  config.vm.synced_folder "./web_content", "/var/www/html", SharedFoldersEnableSymlinksCreate: false
  
  # Script de aprovisionamiento para instalar Apache
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2
    echo '<!DOCTYPE html><html><body><h1>Hola Mundo</h1></body></html>' | sudo tee /var/www/html/index.html
    sudo systemctl restart apache2
  SHELL
end

