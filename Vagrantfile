Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-6.7"

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box 
  end

  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", mount_options: ['dmode=777','fmode=644']

  config.vm.provider "virtualbox" do |v|
    v.customize ['modifyvm', :id, '--paravirtprovider', 'kvm']
    v.linked_clone = true
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provision/site.yml"
  end

end
