Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/groovy64"
  # config.vm.network "private_network", type: "dhcp"
  config.ssh.forward_x11 = true

  # hardware configuration of the VM
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = 8192
    vb.cpus = 8
    vb.linked_clone = true
    vb.name = config.vm.hostname
  end

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get -y update
    apt-get -y upgrade
    apt-get install -y htop mininet libmnl-dev libdb-dev unzip
    apt-get install -y fish ripgrep

    # change shell to fish
    chsh -s /usr/bin/fish vagrant

    # install L4S debs
    curl -L -s -o l4s.zip https://github.com/L4STeam/linux/releases/download/testing-build/l4s-testing.zip
    unzip -j l4s.zip
    dpkg -i *deb

    # make prague the default CC
    echo 'net.ipv4.tcp_congestion_control = prague' >> /etc/sysctl.conf
    echo 'net.ipv4.tcp_ecn = 3' >> /etc/sysctl.conf

    # update grub to boot prague kernel
    sed -i'' -e 's|GRUB_DEFAULT=0|GRUB_DEFAULT="1>2"|g' /etc/default/grub
    update-grub

    # reboot
    echo Please restart via \"vagrant up\"
    shutdown -P now
  SHELL
end
