
Vagrant.configure("2") do |config|

  servers = [
    {
      :hostname => "Server1",
      :box => "bento/ubuntu-22.04",
      :ip => "192.168.56.2",
      :ssh_port => "2200"
    },
    {
      :hostname => "Server2",
      :box => "bento/ubuntu-22.04",
      :ip => "192.168.56.3",
      :ssh_port => "2201"
    },
    {
      :hostname => "Server3",
      :box => "bento/ubuntu-22.04",
      :ip => "192.168.56.4",
      :ssh_port => "2202"
    }
  ]

  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
      node.vm.synced_folder "../data", "/home/vagrant/data"
      node.vm.provision "file", source: "copiedfile.txt", destination: "/home/vagrant/copiedfile.txt"

      config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", 2048]
        vb.customize ["modifyvm", :id, "--cpus", 2]
      end

    end

  end

end