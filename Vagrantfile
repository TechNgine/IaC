# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Define the box you want to use
  config.vm.box = "ubuntu/focal64" # You can choose another Ubuntu version if needed

  # Specify the VM resources
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"    # Set memory to 2 GB
    vb.cpus = 2           # Set number of CPUs to 2
    vb.customize ["createhd", "--filename", "ubuntu_disk.vdi", "--size", "10240"]
  end

  # Provisioning using a shell script
  config.vm.provision "shell", inline: <<-SHELL
    # Update the package list
    sudo apt-get update
    
    # Install Nginx, Curl, Postfix, and Dovecot
    sudo apt-get install -y nginx curl postfix dovecot-core dovecot-imapd
    
    # Create users and set passwords
    sudo useradd -m ola
    echo "ola:ola" | sudo chpasswd
    
    sudo useradd -m standard
    echo "standard:standard" | sudo chpasswd
    
    # Grant passwordless sudo privileges to user 'ola'
    echo "ola ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ola
  SHELL
end
