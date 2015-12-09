masterIP="10.50.15.97"

Vagrant.configure("2") do |o|
	o.vm.provider "virtualbox" do |v|
		v.memory = 2048
		v.cpus = 2
	end
	
	o.vm.define "testmaster" do |testmaster|
		testmaster.vm.box = "ubuntu/trusty64"
		testmaster.vm.hostname = "testmaster.example.com"
		testmaster.vm.provision :shell, path: "PuppetMaster.sh"
		testmaster.vm.network "public_network", ip: masterIP
		testmaster.vm.provider "virtualbox" do |v|
			v.name = "testmaster"
		end
	end
	
	
	o.vm.define "proxy1" do |proxy1|
		proxy1.vm.box = "puppetlabs/centos-6.6-64-puppet-enterprise"
		proxy1.vm.hostname = "proxy1.example.com"
		proxy1.vm.network "public_network"
		proxy1.vm.provider "virtualbox" do |v|
			v.name = "proxyone"
		end
	end
	
	o.vm.define "server1" do |server1|
		server1.vm.box = "puppetlabs/centos-6.6-64-puppet-enterprise"
		server1.vm.hostname = "server1.example.com"
		server1.vm.network "public_network"
		server1.vm.provision "puppet_server" do |puppet|
		puppet.puppet_server = "testmaster.example.com"
		end
		server1.vm.provider "virtualbox" do |v|
			v.name = "serverone"
		end
	end

	
end
