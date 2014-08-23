VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |vagrant|
  vagrant.vm.provider :virtualbox do |provider, override|
    override.vm.box     = 'trusty-server-cloudimg-amd64-vagrant-current'
    override.vm.box_url = 'http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box'
    provider.customize ["modifyvm", :id, "--ioapic", "on"]
    provider.customize ["modifyvm", :id, "--cpus", "2"]  
  end

  vagrant.vm.define 'clojuredev01' do |config|
    config.vm.network :forwarded_port, guest: 5000, host: 5000, auto_correct: false
    config.vm.network "private_network", ip: "10.100.100.10"
    config.vm.synced_folder 'app', '/opt/app', type: 'nfs'
    config.vm.provision :ansible do |ansible|
      ansible.playbook = 'ansible/development.yml'
      ansible.groups   = {'clojuredev' => ['clojuredev01'], 'vagrant_environment' => ['clojuredev01']}
      ansible.raw_arguments = '--timeout=30'
      ansible.host_key_checking = false
    end

  end

end