# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Define VMs with static private IP addresses, vcpu, memory and vagrant-box.
    boxes = [
      {
        :name => "lpitreinamento",
        :box => "debian/buster64",
        :ram => 1024,
        :vcpu => 1,
        :ip => "192.168.29.2"
      }
    ]
  
    # Provision each of the VMs.
    boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        # Only Enable this if you are connecting to Proxy server
        # config.proxy.http    = "http://usernam:password@x.y:80"⇒ Needed if you have a proxy
        # config.proxy.https   = "http://usernam:password@x.y:80"
        # config.proxy.no_proxy = "localhost,127.0.0.1"
        # config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
        config.ssh.insert_key = false
        config.vm.box = opts[:box]
        config.vm.hostname = opts[:name]
        # config.ssh.username = 'root'
        # config.ssh.password = 'vagrant'
        # config.ssh.insert_key = 'true'
        config.vm.provider :virtualbox do |v|
          v.memory = opts[:ram]
          v.cpus = opts[:vcpu]
        end
        # config.vm.network :private_network, ip: opts[:ip]
        # config.vm.provision :file do |file|
        #    file.source     = './keys/vagrant'
        #    file.destination    = '/tmp/vagrant'
        #end
        config.vm.provision :shell, :inline => "sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; sudo systemctl restart sshd;", run: "always"
       
        config.vm.provision :shell, path: "bootstrap.sh"
        # if config.vm.hostname == 'kafkalab1'
        #   config.vm.provision :shell, :inline => "sudo -i ansible -m shell -a 'whoami' -i kafkalab1, all -u vagrant --extra-vars 'ansible_ssh_pass=vagrant' --become-user root -b", run: "always"
        #   config.vm.provision :shell, :inline => "echo 'Provisioned succesfully'"
        # end
        # config.vm.provision :ansible do |ansible|
        #   ansible.verbose = "v"
        #   ansible.playbook = "playbook.yml"
        # end
      end
    end
  end