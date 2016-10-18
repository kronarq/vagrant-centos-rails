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
  config.vm.box = "centos/7"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # Customize the amount of memory on the VM:
    vb.cpus = "2"

    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    yum update -y
    yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel epel-release mariadb-server mariadb-devel
    yum install -y nodejs

    sudo -S -u vagrant -i /bin/bash -l -c 'git clone git://github.com/sstephenson/rbenv.git /home/vagrant/.rbenv'
    sudo -S -u vagrant -i /bin/bash -l -c 'git clone git://github.com/sstephenson/ruby-build.git /home/vagrant/.rbenv/plugins/ruby-build'

    echo 'export PATH="/home/vagrant/.rbenv/bin:/home/vagrant/.rbenv/plugins/ruby-build/bin:$PATH"' >> /home/vagrant/.bash_profile
    echo 'export MAKEFLAGS="-j $(nproc --all)"' >> /home/vagrant/.bash_profile
    echo 'eval "$(rbenv init -)"' >> /home/vagrant/.bash_profile

    sudo -S -u vagrant -i /bin/bash -l -c '/home/vagrant/.rbenv/bin/rbenv install -v 2.3.1'
    sudo -S -u vagrant -i /bin/bash -l -c '/home/vagrant/.rbenv/bin/rbenv global 2.3.1'
    sudo -S -u vagrant -i /bin/bash -l -c 'ruby -v'
    sudo -S -u vagrant -i /bin/bash -l -c 'echo "gem: --no-document" > /home/vagrant/.gemrc'
    sudo -S -u vagrant -i /bin/bash -l -c 'gem install bundler'
    sudo -S -u vagrant -i /bin/bash -l -c 'gem install rails'
    sudo -S -u vagrant -i /bin/bash -l -c '/home/vagrant/.rbenv/bin/rbenv rehash'

    sudo -S -u vagrant -i /bin/bash -l -c 'export MAKEFLAGS="-j 2"; cd /vagrant/rails/rails-devise/; bundle update'
    sudo -S -u vagrant -i /bin/bash -l -c 'cd /vagrant/rails/rails-devise/; rake db:migrate'

    sudo -S -u vagrant -i /bin/bash -l -c 'cd /vagrant/rails/rails-devise/; rails s -d'

    echo; echo "-----------------------"; echo "WARNING!"; echo "This is inherently insecure only run behind a firewall."; echo "Do not open to the internet!"; echo "-----------------------"; echo;

    echo; echo "-----------------------"; echo "Connect to server at:"; ifconfig | grep "inet " | grep -v "10.0.2.15" | grep -v "127.0.0.1" | awk '{print "http://" $2 ":3000"}'; echo "-----------------------"; echo;
  SHELL

end
