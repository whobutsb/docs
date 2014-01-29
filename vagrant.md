#Vagrant

__Documentation__
- http://docs.vagrantup.com/v2

Start up Vagrant in a directory
    
    vagrant init 

VagrantFile - configuration file 

    VAGRANTFILE_API_VERSION = "2"
    Vagrant.configure(VAGRANTFILE_API_VERSION) do |config

      # Every Vagrant virtual environment requires a box to build off of.
      config.vm.box = "precise32"  

      #Runs the bootstrap.sh script on boot
      config.vm.provision :shell, :path => "bootstrap.sh"

      #Port forwards localhost 4567 to look at guest host 80
      #View apache pages at: localhost:4567
      config.vm.network :forwarded_port, host: 4567, guest: 80

      #Setup synced directories
      #create: true creates the folder if it doesn't exist
      config.vm.synced_folder "/Users/stevebarbera/Desktop/", "/steve", create: true
      #setup Virtual Box Parameters
      config.vm.provider "virtualbox" do |v|
        #Name of the VBox Template
        v.name = "Vagrant Tutorial"
        #How much memory the VBox has
        v.memory = 512
      end
    end