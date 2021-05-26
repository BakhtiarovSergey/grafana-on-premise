Vagrant.configure("2") do |config|
  config.vm.provider :virtualbox do |v|
    v.cpus = 1
  end

  config.vm.define :grafana do |master|
    master.vm.box = "ubuntu/bionic64"
    master.vm.hostname = "grafana"
    master.vm.network :private_network, ip: "192.168.99.99"
    master.vm.provider :virtualbox do |v|
      v.memory = 3072
    end
    master.vm.provision :shell, privileged: false, inline: $commands_set
  end

  config.vm.define :node1 do |master|
    master.vm.box = "ubuntu/bionic64"
    master.vm.hostname = "node1"
    master.vm.network :private_network, ip: "192.168.99.98"
    master.vm.provider :virtualbox do |v|
      v.memory = 1024
    end
    master.vm.provision :shell, privileged: false, inline: $commands_set
  end

end

$commands_set = <<-SHELL
sudo sed -i "s/PasswordAuthentication.*/PasswordAuthentication yes/g" /etc/ssh/sshd_config
sudo systemctl restart sshd
cat /etc/os-release
uname -a
SHELL
