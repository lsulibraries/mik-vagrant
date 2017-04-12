# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.post_up_message = "
MIK SHOULD NOW BE INSTALLED ON YOUR BOX.

LOGIN to the box: 
    vagrant ssh

CHANGE DIRECTORY to the location of the MIK executable:
    cd /vagrant/mik

Then RUN a sample mik conversion:
    php mik --config mik-sample-data/hnoc-delcroix/hnoc-delcroix_config.ini 

OUTPUT: 

Frome the /vagrant/mik location in the box, you should be able
to list the contents of MIK's output directory:
    ll mik-sample-data/hnoc-delcroix/output/

LOCAL_DIRECTORY means the directory in which you ran `vagrant up`, 
where this Vagrantfile lives.

Files in LOCAL_DIRECTORY are available on the box under /vagrant/.

From your local machine, you should be able to use normal filesystem
tools to create/access/edit/delete files at LOCAL_DIRECTORY/mik/.

HELP: 

For most MIK questions, visit https://github.com/marcusbarnes/mik
For trouble with Vagrant, be sure you've installed the latest version,
and check https://www.vagrantup.com/.
For trouble with this fork of MIK, or this box, open an issue at 
https://github.com/lsulibraries/mik.

"

  config.vm.provision "shell", inline: <<-SHELL
    MHOME=/vagrant
    sudo apt-get update
    sudo apt-get -y install php5-cli default-jre zip git emacs
    git clone https://github.com/lsulibraries/mik $MHOME/mik
    git clone https://github.com/lsulibraries/mik-sample-data $MHOME/mik/mik-sample-data
    git config core.filemode false
    cd $MHOME/mik &&  curl -sS https://getcomposer.org/installer | php
    cd $MHOME/mik &&  php composer.phar install
    cd $MHOME && curl -OL https://sourceforge.net/projects/saxon/files/Saxon-HE/9.7/SaxonHE9-7-0-18J.zip/download
    cd $MHOME && unzip download
    mv $MHOME/saxon9he.jar $MHOME/mik
SHELL
end
