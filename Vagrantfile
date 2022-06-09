VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'centos/7'
  #Expanding VM disk via virtual box provider (later wi will create a docker partition with Ansible)
  config.disksize.size = '100GB' 
  # Mapping folder between host and guests
  config.vm.synced_folder ".", "/home/vagrant/sync", disabled: true
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  # Update and install python3
  config.vm.provision "shell", path: "bootstrap.sh", privileged: false

 # Configure 3 CentOS-7 VMs in Loop
 N = 3
 (1..N).each do |id|
 config.vm.define "centos#{id}" do |machine|
   machine.vm.hostname = "centos#{id}"
   machine.vm.network "private_network", ip: "192.168.10.#{10+id}"

   if id == N # Wait for both VM to be up and running
     machine.vm.provision "ansible_local" do |ansible|
         # Specify python interpreter version
         ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python2.7" }
         ansible.become = true
         ansible.install_mode = "pip3"
         ansible.pip_args = "ansible==2.10.7"
         ansible.playbook = "provisioning.yml"
         ansible.galaxy_role_file = "requirements.yml"
         ansible.galaxy_roles_path = "/etc/ansible/roles"
         # Install required roles
         ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
         ansible.limit = "all"
         ansible.inventory_path = "inventory"
       end
     end
   end
  end
end
