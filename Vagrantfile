VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |vagrant|

  vagrant.vm.provider "vmware_fusion" do |provider, v|
    v.vm.box = "vmware-trusty64"
    v.vm.box_url = "http://s3-us-west-2.amazonaws.com/technolo-g/vagrant-boxes/ubuntu/vmware-trusty64.box"
  end

  vagrant.vm.provider :virtualbox do |provider, override|
    override.vm.box     = 'trusty-server-cloudimg-amd64-vagrant-current'
    override.vm.box_url = 'http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box'
    provider.customize ["modifyvm", :id, "--ioapic", "on"]
    #provider.customize ["modifyvm", :id, "--cpus", "2"]  
  end

  vagrant.vm.define 'clojuredev01' do |config|
    config.vm.network :forwarded_port, guest: 5000, host: 5000, auto_correct: false
    config.vm.provision :ansible do |ansible|
      ansible.playbook = 'ansible/development.yml'
      ansible.groups   = {'clojuredev' => ['clojuredev01'], 'vagrant_environment' => ['clojuredev01']}
      ansible.raw_arguments = '--timeout=30'
      ansible.host_key_checking = false
    end

  end

end