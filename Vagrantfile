Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/groovy64"

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get -y update
    apt-get -y upgrade
    apt-get install -y htop mininet libmnl-dev libdb-dev unzip
    apt-get install -y fish ripgrep

    # change shell to fish
    chsh -s /usr/bin/fish vagrant

    # install L4S
    curl -L -s -o l4s.zip https://github.com/L4STeam/linux/releases/download/testing-build/l4s-testing.zip
    unzip -j l4s.zip
    dpkg -i *deb

    # update grub to boot L4S/Prague kernel by default
    sed -i'' -e 's|GRUB_DEFAULT=0|GRUB_DEFAULT="1>2"|g' /etc/default/grub
    update-grub

    # make L4S/Prague the default congestion controll algorithm
    echo 'net.ipv4.tcp_congestion_control = prague' >> /etc/sysctl.conf
    echo 'net.ipv4.tcp_ecn = 3' >> /etc/sysctl.conf

    # done
    shutdown -P now
  SHELL
end
