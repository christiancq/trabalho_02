Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  
  config.vm.define "vm1" do |vm1|
    vm1.vm.network "private_network", ip: "192.168.1.3"
    #config.vm.provision "shell", inline: <<-SHELL
    #  sudo route add default gw 192.168.1.254
    #SHELL
  end

  config.vm.define "vm3" do |vm3|
    vm3.vm.network "private_network", ip: "10.0.0.1"
    config.vm.provision "shell", inline: <<-SHELL
      sudo route add default gw 10.0.0.254
    SHELL
  end
  
  config.vm.define "vm2" do |vm2|
    vm2.vm.network "private_network", ip: "192.168.0.254"
    config.vm.provision "shell", inline: <<-SHELL
      sudo sysctl -w net.ipv4.ip_forward=1
      sudo sysctl -p /etc/sysctl.conf
      sudo route add -net 192.168.1.0 netmask 255.255.255.0 dev eth1
      sudo route add -net 10.0.0.0 netmask 255.255.255.0 dev eth2
      sudo apt-get update 
      sudo apt-get upgrade -y
      sudo apt install tcpdump
      tcpdump -i eth1 -w output.pcap
    SHELL
  end
end
