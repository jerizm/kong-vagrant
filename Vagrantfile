# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "precise64"
  config.vm.box_url ="http://files.vagrantup.com/precise64.box"
  config.vm.synced_folder "../kong", "/kong"
  config.vm.synced_folder "./", "/kong/dev"
  config.vm.provider :virtualbox do |vb|
     vb.memory = 2048
  end
  config.vm.network :forwarded_port, guest: 8000, host: 8000
  config.vm.network :forwarded_port, guest: 8001, host: 8001
  config.vm.provision "shell", inline: "
    apt-get update
    apt-get install wget curl tar make gcc unzip git liblua5.1-0-dev luarocks netcat lua5.1 openssl libpcre3 libpcre3-dev libcurl4-openssl-dev pkg-config dnsmasq -y --force-yes
    # Build dependencies for OpenResty.
    apt-get install build-essential libpcre3-dev libssl-dev libgeoip-dev

    # If you want to access Postgres via Nginx
    apt-get install libpq-dev

    echo 'nameserver 10.0.2.3' >> /etc/resolv.conf
    echo 'nameserver 8.8.8.8' >> /etc/resolv.conf
    echo 'nameserver 8.8.4.4' >> /etc/resolv.conf
    /kong/dev/setup.sh
    "
end
