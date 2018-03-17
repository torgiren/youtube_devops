Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provider :libvirt do |libvirt|
      libvirt.memory = 256
  end
  config.vm.define "lb"
  config.vm.define "www1"
  config.vm.define "backend1"

  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ping.yml"
      ansible.groups = {
        "balanacer" => ["lb"],
        "app1:children" => ["app1_backend", "app1_frontend"],
        "app1_backend" => ["backend1", "www1"],
        "app1_frontend" => ["www1"],
        "app2:children" => ["app2_frontend"],
        "app2_frontend" => ["www1"]
      }
  end

end
