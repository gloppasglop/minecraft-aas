# -*- mode: ruby -*-
# vi: set ft=ruby :


# This is your exoscale configuration
private_key_path = "~/.ssh/macveltiexo"

# exoscale's Vagrant boxes: https://www.exoscale.ch/open-cloud/templates/
vagrant_box_name = "coreos_exo"
exoscale_service_offering_id = "b6e9d1e8-89fc-4db3-aaa4-9b4c5b1d0844" # Micro - 4096 MB
exoscale_keypair='macveltiexo'

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"



Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
#  config.vm.hostname = hostname
  config.vm.box = vagrant_box_name
  
  config.vm.provider :cloudstack do |cloudstack, override|
#    cloudstack.api_key = exoscale_api_key
#    cloudstack.secret_key = exoscale_secret_key
    cloudstack.service_offering_id = exoscale_service_offering_id
    cloudstack.keypair = exoscale_keypair
 #   cloudstack.user_data = user_data
    override.ssh.username = "core"
    cloudstack.zone='ch-gva-2'
    override.ssh.private_key_path = private_key_path
  end

  etcd_nodes = ['node1','node2','node3']

  user_data = File.open('user-data.txt').read

  etcd_nodes.each do |node|
      config.vm.define node do |c|
          c.vm.hostname = node
          c.vm.provider :cloudstack do |cloudstack, override|
              cloudstack.display_name = node
              cloudstack.security_group_names = ['default','coreos']
              cloudstack.user_data = user_data
#              override.ssh.username = "core"
#              override.ssh.private_key_path = private_key_path
          end
      end
  end


end
