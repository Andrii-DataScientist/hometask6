Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["storagectl", :id, "--name", "SATA", "--add", "sata" ]

    storages = [1,2,3,4]
    storages.each do |hw|
        to_disk = "mydisk#{hw}.vmdk"    
        unless File.exist?(to_disk)
            vb.customize [ "createmedium", "disk", "--filename", to_disk, "--format", "vmdk", "--size", 300]
        end
        vb.customize [ "storageattach", :id, "--storagectl", "SATA", "--port", "#{hw}", "--device", "0", "--type", "hdd", "--medium", to_disk]
    end
  end
  
  config.vm.provision "shell", path: "script.sh"
end