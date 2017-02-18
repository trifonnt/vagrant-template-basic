#   Collection of Vagrant VMs
# - https://github.com/tomaszguzialek/vagrant-vms

Vagrant.configure("2") do |config|
	config.vm.box = "bento/ubuntu-16.04"
	config.vm.hostname = "test-01"
	config.ssh.insert_key = true

	#config.vm.network "forwarded_port", guest: 8080, host: 8080
	#config.vm.network "forwarded_port", guest: 8020, host: 8020
	# Create a private network, which allows host-only access to the machine using a specific IP.
	#config.vm.network "private_network", ip: "192.168.33.10"

	config.vm.provider :virtualbox do |vb|
		# Display the VirtualBox GUI when booting the machine
		vb.gui = true

		# Set the VirtualBox VM name equal to the hostname
#		vb.name = config.vm.hostname.to_s

		# Use VBoxManage to customize the VM. For example to change memory:
		vb.customize ["modifyvm", :id, "--name", config.vm.hostname.to_s]
		vb.customize ["modifyvm", :id, "--memory", "1024"]
		vb.customize ["modifyvm", :id, "--vram", 128]
		vb.customize ["modifyvm", :id, "--cpus", 2]
		vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
		vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']
		vb.customize ['modifyvm', :id, '--draganddrop', 'bidirectional']
	end

	# Initial run script, executed as root
	config.vm.provision "shell", privileged: true, inline: <<-SHELL
		echo Updating apt repository
		apt-get update -y

		echo Installing JDK 8
		apt-get install -y default-jdk > /dev/null
	SHELL

	# Initial run script, executed as vagrant user
	config.vm.provision "shell", privileged: false, inline: <<-SHELL
		# echo Downloading ...
		# wget -q http://mirrors.rackhosting.com/apache/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz
	SHELL


	# Using vagrant-triggers plugin to stop <SERVICE> on halt and reload commands
	config.trigger.before :halt do
		info "Stopping service..."
		run "vagrant ssh -c 'hadoop-2.7.1/sbin/stop-yarn.sh'"
	end

	config.trigger.before :reload do
		info Stopping MR historyserver
		run "vagrant ssh -c 'hadoop-2.7.1/sbin/stop-yarn.sh'"
	end
end