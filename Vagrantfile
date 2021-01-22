Vagrant.configure("2") do |config|
  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 1
    v.name = "Grafana_for_TDG_bionic"
  end

  config.vm.define :grafana do |master|
    master.vm.box = "ubuntu/bionic64"
    master.vm.hostname = "grafana"
    master.vm.network :private_network, ip: "192.168.99.99"
    master.vm.provision :shell, privileged: false, inline: $commands_set
  end

end

$commands_set = <<-SHELL
sudo sed -i "s/PasswordAuthentication.*/PasswordAuthentication yes/g" /etc/ssh/sshd_config
sudo systemctl restart sshd
cat /etc/os-release
uname -a
SHELL
