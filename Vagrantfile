require "yaml"
vconfig = YAML.load(File.open(File.join(File.dirname(__FILE__), "config.yaml"), File::RDONLY).read)

Vagrant.configure("2") do |config|

    config.vm.define vconfig['VAGRANT_BOX_NAME'] do |m|

        # set up basic box image
        m.vm.box = "ubuntu/trusty64"

        # set host name
        m.vm.hostname = vconfig['VAGRANT_HOST_NAME']

        # update machine configurations
        config.vm.provider "virtualbox" do |v|
            v.customize ["modifyvm", :id, "--memory", vconfig['VAGRANT_BOX_MEMORY'].to_i]
            v.customize ["modifyvm", :id, "--cpus", vconfig['VAGRANT_BOX_CORES'].to_i]
        end

        # set private network, machine will use this ip
        m.vm.network "private_network", ip: vconfig['VAGRANT_HOST_IP']

        # provision docker environment
        m.vm.provision "docker"

    end

end
