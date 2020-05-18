Vagrant.configure("2") do |config|

  config.vm.box = "ooga04/amzn2"
  config.vm.box_version = "2.0.20190228"
  config.vm.network "private_network", ip: "192.168.240.21"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8096"
    vb.cpus = "2"
  end

  config.vm.provision :shell, :inline => <<-EOT
    sudo amazon-linux-extras install -y ansible2
    sudo ansible-playbook /vagrant/local-site.yml
  EOT

  config.vm.provision :shell, run: "always", :inline => <<-EOT
    sysctl -w vm.max_map_count=262144
    sysctl -w fs.file-max=65536
    ulimit -n 65536
    ulimit -u 65536
    sudo docker-compose -f /vagrant/docker-compose.yml up -d
  EOT

end
