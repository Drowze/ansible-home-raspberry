disk = './secondDisk.vdi'

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true 
  config.vm.network :private_network, ip: '192.168.56.2'

  config.vm.provider(:virtualbox) do |v|
  	unless File.exist?(disk)
  	  v.customize ['createhd', '--filename', disk, '--variant', 'Fixed', '--size', 12]
  	end

  	v.memory = 1024
  	v.customize ['storageattach', :id,  '--storagectl', 'SCSI', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', disk]
  end

  config.vm.provision('shell', inline: <<~SHELL
  		echo 'type=83' | sudo sfdisk /dev/sdc
  		sudo mkfs.ext4 /dev/sdc1 -F
  		mkdir -p tmp
  		sudo mount /dev/sdc1 tmp
  		mkdir tmp/Video
  		mkdir tmp/untracked
  		cp /vagrant/files/sample.mkv tmp/Video/sample.mkv
  		sudo umount tmp
  	SHELL
  )

  config.vm.provision('ansible') do |ansible|
  	ansible.playbook = 'playbook.yml'
  	ansible.inventory_path = 'hosts'
  	ansible.limit = 'all'
  end
end
