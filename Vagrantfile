Vagrant.configure("2") do |config|
  config.vm.define "grafana" do |grafana|
    grafana.vm.box = "generic/ubuntu2004"
    grafana.vm.network "forwarded_port", guest: 3000, host: 3000
    grafana.vm.network "private_network", ip: "192.168.56.30"

    grafana.vm.provision "shell", inline: "apt-get install -y docker.io"
    grafana.vm.provision "shell", inline: "gpasswd -a vagrant docker"
    grafana.vm.provision "shell", inline: "docker run -d -p 3000:3000 --name=grafana -e 'GF_SERVER_ROOT_URL=http://localhost:3000' -e 'GF_SECURITY_ADMIN_PASSWORD=secret' grafana/grafana"
    grafana.vm.provision "shell", inline: "docker ps"
  end
  config.vm.define "prometheus" do |prometheus|
    prometheus.vm.box = "generic/ubuntu2004"
    prometheus.vm.network "forwarded_port", guest: 9090, host: 9090
    prometheus.vm.network "forwarded_port", guest: 9100, host: 9100
    prometheus.vm.network "private_network", ip: "192.168.56.31"

    prometheus.vm.provision "shell", inline: "apt-get install -y prometheus prometheus-node-exporter"
    prometheus.vm.provision "shell", inline: "systemctl status prometheus"
    prometheus.vm.provision "shell", inline: "systemctl status prometheus-node-exporter"
  end
end
