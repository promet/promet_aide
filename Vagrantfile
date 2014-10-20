Vagrant.configure("2") do |config|

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true

  config.vm.box = "promet_wheezy"
  config.vm.box_url = "https://s3.amazonaws.com/promet_debian_boxes/wheezy_virtualbox.box"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", 2048]
  end

  project = 'aide'
  path = "/var/www/sites/#{project}.dev"

  config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.vm.synced_folder ".", path, :nfs => true
  config.vm.hostname = "#{project}.dev"

  config.ssh.forward_agent = true
  config.vm.network :private_network, ip: "10.33.36.11"

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe("aide")

    chef.json = {
	  :aide => {
		  :notify => "sysadmins@prometsource.com"
		}
	}
  end

end
