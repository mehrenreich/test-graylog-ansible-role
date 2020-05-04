Vagrant.configure("2") do |config|
  config.vm.hostname = "graylog"
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", 6000]
    vb.customize ["modifyvm", :id, "--cpus", 2]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", 90]
  end

  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo '' >> /home/ubuntu/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /home/ubuntu/.ssh/authorized_keys
    SHELL
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    end
end