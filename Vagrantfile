Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.dns.tld= "hdp"
  VagrantDNS::Config.listen = [ [:udp, "127.0.0.1", 5300] , [:udp, "192.168.5.1", 53] ]

#  config.hostmanager.enabled = true
#  config.hostmanager.manage_guest = true
#  config.hostmanager.manage_host = false
  config.vm.provision :ansible do |a|
    a.playbook = "ansible/playbook.yml"
  end

  config.vm.define "mgmt" do |child|
		child.vm.hostname = "mgmt"
    child.vm.network "private_network", ip: "192.168.5.2"
    child.vm.provider :vmware_fusion do |v|
      v.vmx["memsize"] = "1024"
      v.vmx["numvcpus"] = "2"
    end
    config.vm.provision :ansible do |a|
      a.playbook = "ansible/ambari.yml"
    end
  end

  config.vm.define "master-01" do |child|
		child.vm.hostname = "master-01"
    child.vm.network "private_network", ip: "192.168.5.3"
    child.vm.provider :vmware_fusion do |v|
      v.vmx["memsize"] = "512"
    end
  end

  config.vm.define "master-02" do |child|
		child.vm.hostname = "master-02"
    child.vm.network "private_network", ip: "192.168.5.4"
    child.vm.provider :vmware_fusion do |v|
      v.vmx["memsize"] = "512"
    end
  end

  config.vm.define "master-03" do |child|
		child.vm.hostname = "master-03"
    child.vm.network "private_network", ip: "192.168.5.5"
    child.vm.provider :vmware_fusion do |v|
      v.vmx["memsize"] = "512"
    end
  end

  config.vm.define "edge-01" do |child|
		child.vm.hostname = "edge-01"
    child.vm.network "private_network", ip: "192.168.5.8"
    child.vm.provider :vmware_fusion do |v|
      v.vmx["memsize"] = "512"
    end
  end

  (1..2).each do |i| 
    config.vm.define "node-0#{i}" do |child|
			child.vm.hostname = "node-0#{i}"
      child.vm.network "private_network", ip: "192.168.5.1#{i}"
      child.vm.provider :vmware_fusion do |v|
        v.vmx["memsize"] = "512"
      end
    end
  end

end
