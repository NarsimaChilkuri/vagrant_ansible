node_count = 2

ansible_master_os = "centos/7"
ansible_slave_os = "centos/7"

Vagrant.configure("2") do |config|
  config.vm.define "ansible-master" do |ansible|
    ansible.vm.box = ansible_master_os
    ansible.vm.hostname = "ansible-master.com"
    ansible.vm.network "private_network", ip: "173.42.42.100"
    ansible.vm.provision :shell, path: "entrypoint_scripts/install_ansible.sh", run: 'always'
    ansible.vm.provider "virtualbox" do |v|
      v.name = "ansible-server"
      v.memory = 1024
      v.cpus = 1
      v.customize ["modifyvm", :id, "--audio", "none"]
    end
  end

  (1..node_count).each do |i|
    config.vm.define "ansible-slave#{i}" do |workernode|
      workernode.vm.box = ansible_slave_os
      workernode.vm.hostname = "ansible-slave#{i}.com"
      workernode.vm.network "private_network", ip: "173.42.42.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "ansible-slave#{i}"
        v.memory = 1024
        v.cpus = 1
        v.customize ["modifyvm", :id, "--audio", "none"]
      end
    end
  end
end
