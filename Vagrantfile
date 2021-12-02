# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  #config.vm.network "forwarded_port", guest: 80, host: 8888, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"\
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL

   	setenforce 0
	sudo su
 	echo '-find and print names of all soft-links on your VM;'
	find / -type l -print > sym-links.txt
	find / -type l | wc -l	
	
	echo '-find and print count of block and character devices;'
	find / -type b -o -type c | wc -l 

	echo '-find all folders with Sticky bit;' 
	find / -type d -perm -1000 -exec ls -lbd {} +

	echo '-make soft link for /etc/hostname in /tmp folder'
	ln -s /etc/hostname /tmp/mylink
	find /tmp -type l

	echo '-create user testuser'
	sudo useradd testuser
	less /etc/passwd

	echo 'create file in home directory testuser_data owned by testuser'
	sudo runuser testuser
	echo 'I Love DevOps' > /home/testuser/testuser_data.txt
	find / -name testuser_data.txt 2>/dev/null

   SHELL
end
