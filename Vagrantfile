Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  box = "ubuntu/mantic64"

  if Vagrant::Util::Platform.darwin? 
    box = "bento/ubuntu-22.04-arm64"
  else
    config.vm.provision "shell", inline: "sudo apt-get update && sudo apt-get install -y virtualbox-guest-x11"
  end

  config.vm.box = box
  config.vm.network "forwarded_port", guest: 80, host: 8081
  config.vm.box_download_insecure = true
  config.vm.hostname = "utn-devops.localhost"
  config.vm.boot_timeout = 1000
  config.vm.provider "virtualbox" do |vb|
    v.name = "utn-devops-vagrant-ubuntu"
    vb.memory = "2048"
  end

  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "vmware_desktop" do |vm|
    vm.memory = "2048"
  end

  config.vm.provision "file", source: "Configs/devops.site.conf", destination: "/tmp/devops.site.conf"
  config.vm.provision :shell, path: "Vagrant.bootstrap.sh", run: "always"

end
