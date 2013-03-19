# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  config.vm.hostname = "zazu"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network
  
  # SSH key
  # config.ssh.private_key_path = "~/.ssh/id_rsa"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../", "/home/vagrant/app"
  config.vm.synced_folder "~/.ssh", "/home/vagrant/.ssh"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  config.vm.provider :virtualbox do |vb|
     # Use VBoxManage to customize the VM. For example to change memory:
     vb.customize ["modifyvm", :id, "--memory", "1024"]
  end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision :chef_solo do |chef|
    chef.add_recipe "git"
    chef.add_recipe "nodejs::install_from_source"
    #chef.add_recipe "nodejs::npm"
    chef.add_recipe "python"
    chef.add_recipe "vim"
  
    #   # You may also specify custom JSON attributes:
    #   chef.json = { :mysql_password => "foo" }
  end

  # install ctags
  config.vm.provision :shell, :inline => "apt-get install ctags"

  # run pos install steps
  # config.vm.provision :shell, :inline => "/home/vagrant/postinstall.sh"

  # configure environment
  config.vm.provision :shell, :inline => "su vagrant -c \"test ! -d ~/.termrc && git clone git://github.com/michalbachowski/termrc.git ~/.termrc && cd ~/.termrc && /bin/bash init.sh\""
  
  # configure vim
  config.vm.provision :shell, :inline => "su vagrant -c \"test ! -d ~/.termrc && git clone git://github.com/michalbachowski/vimper.git ~/.vimper && cd ~/.vimper && python bootstrap.py\""
  
end