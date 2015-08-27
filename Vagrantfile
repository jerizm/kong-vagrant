# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "precise64"
  config.vm.box_url ="http://files.vagrantup.com/precise64.box"
  config.vm.synced_folder ENV["KONG_PATH"], "/kong"
  config.vm.synced_folder "/Users/jwang/Git/pgmoon", "/pgmoon"
  config.vm.synced_folder "./", "/vagrant"
  config.vm.provider :virtualbox do |vb|
     vb.memory = 2048
  end
  config.vm.network :forwarded_port, guest: 8002, host: 8002
  config.vm.network :forwarded_port, guest: 8003, host: 8003
  config.vm.provision "shell", inline: "
    apt-get update
    apt-get install wget curl tar make gcc unzip git liblua5.1-0-dev luarocks netcat lua5.1 openssl libpcre3 libpcre3-dev openjdk-7-jdk libcurl4-openssl-dev pkg-config dnsmasq -y --force-yes
    # Build dependencies for OpenResty.
    apt-get install build-essential libpcre3-dev libssl-dev libgeoip-dev

    # Install standard Nginx first so that you get the relevant service scripts installed too

    # If you want to access Postgres via Nginx
    apt-get install libpq-dev

    echo 'nameserver 10.0.2.3' >> /etc/resolv.conf
    echo 'nameserver 8.8.8.8' >> /etc/resolv.conf
    echo 'nameserver 8.8.4.4' >> /etc/resolv.conf
    /vagrant/setup.sh
    "
end
