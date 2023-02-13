Vagrant.configure("2") do |config|
    config.vm.box = "generic/fedora37"
    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 4
        v.customize ['modifyvm', :id, '--nested-hw-virt', 'on']
    end
    config.vm.synced_folder ".", "/home/vagrant/dev"
    config.vm.provision "shell", inline: <<-SHELL
        sudo dnf update -y
        sudo dnf install qemu -y
        sudo dnf install podman -y
        sudo dnf install golang -y
        sudo runuser -l vagrant -c "git clone https://github.com/crc-org/crc.git"
        sudo runuser -l vagrant -c "cd crc && make"
        sudo cp /home/vagrant/go/bin/crc /usr/bin/.
        sudo runuser -l vagrant -c "podman machine init"
        sudo runuser -l vagrant -c "podman machine start"
        sudo runuser -l vagrant -c "crc config set preset podman"
        sudo runuser -l vagrant -c "crc setup"
        sudo runuser -l vagrant -c "crc start"
        sudo runuser -l vagrant -c "eval $(crc podman-env)"
    SHELL
end
