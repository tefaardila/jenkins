Vagrant.configure("2") do |config|
  
  config.vm.define "backend" do |backend|
  
    backend.vm.box = "hashicorp/bionic64"
    backend.vm.hostname = "backend"
    
    backend.vm.provider "virtualbox" do |vb|
      vb.memory = "8192"
      vb.cpus = 4
    end
    
    backend.vm.provision "file", source: "public-proyect.pem", destination: "/home/vagrant"

    backend.vm.network "private_network", ip: "192.168.33.11"
    backend.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "192.168.33.11"
    backend.vm.network "forwarded_port", guest: 443, host: 443, host_ip: "192.168.33.11"
    


    backend.vm.provision "A", type: "ansible_local" do |ansible|
      ansible.playbook = "playbooks/backend.yml"
    end
    
    backend.vm.provision "B", after: "A", type: "ansible_local" do |ansible|
      ansible.playbook = "playbooks/d-backend.yml"
    end

    backend.vm.provision "C", after: "B", type: "ansible_local" do |ansible|
      ansible.playbook = "jenkins/jenkins.yml"
    end

    # backend.vm.provision "D", after: "C", type: "ansible_local" do |ansible|
    #   ansible.playbook = "playbooks/ngrok.yml"
    # end

  end

  # config.vm.define "nexus" do |nexus|
  
  #   nexus.vm.box = "hashicorp/bionic64"
  #   nexus.vm.hostname = "nexus"
    
  #   nexus.vm.provider "virtualbox" do |vb|
  #     vb.memory = "8192"
  #     vb.cpus = 4
  #   end
    
    
  #   nexus.vm.network "private_network", ip: "192.168.33.12"
  #   nexus.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "192.168.33.12"
  #   nexus.vm.network "forwarded_port", guest: 443, host: 443, host_ip: "192.168.33.12"
    

  #   nexus.vm.provision "A", type: "ansible_local" do |ansible|
  #     ansible.playbook = "playbooks/nexus.yml"
  #   end


  # end


  

  
  
end
