VAGRANTFILE_API_VERSION = "2"

### Check if required plugins are installed
unless Vagrant.has_plugin?("vagrant-bindfs")
  raise 'vagrant-bindfs plugin is missing!'
end

unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise 'vagrant-hostsupdater plugin is missing!'
end

### Configure Vagrant box
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network "private_network", ip: "192.168.100.100"
  config.vm.hostname = "wordpress-dev"

  ### Set a right amount of memory (WordPress eat a lot of resources)
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  ### Configure synced folders with bindfs
  config.vm.synced_folder "./wordpress.dev", "/vagrant-nfs", nfs: true 
  config.bindfs.bind_folder "/vagrant-nfs", "/var/www/wordpress.dev"

  ### Domain where you will reach WordPress
  config.hostsupdater.aliases = [
    "wordpress.dev"
  ]

  ### Fix for Ansible bug resulting in an encoding error
  ENV['PYTHONIOENCODING'] = "utf-8"

  ### Run Ansible provision
  config.vm.provision "ansible" do |ansible|
    ansible.limit = 'all'
    ansible.verbose = "" ### If you notice errors, add "vvv" here to activate verbose mode
    ansible.playbook = "ansible/development.yml"
    ansible.inventory_path = "ansible/hosts"
  end

  config.vm.post_up_message = "Provisioning is done. Now you can reach your WordPress instance at: http://wordpress.dev"
end
