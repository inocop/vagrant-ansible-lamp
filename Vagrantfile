VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "bento/centos-6.7"
  config.vm.network "private_network", ip: "192.168.33.39"
  config.vm.network :forwarded_port, guest: 80, host: 8888, id: "http"
  config.vm.network :forwarded_port, guest: 443, host: 4444, id: "https"
  config.vm.hostname = "localhost.localdomain"
  config.vm.synced_folder "./src", "/var/www/html", :mount_options => ['dmode=775', 'fmode=664']
  config.vm.synced_folder "./src", "/vagrant", :mount_options => ['dmode=775', 'fmode=664']

  ### Workaround on (under vagrant v.1.8.1 & over ansible v.2)
  begin
    Vagrant.require_version(">= 1.8.2")
  rescue
    config.vm.provision "shell", inline: <<-SHELL
      echo '#!/bin/bash' > /usr/local/bin/ansible-galaxy
      echo '/usr/bin/ansible-galaxy "$@" || exit 0' >> /usr/local/bin/ansible-galaxy
      chmod 755 /usr/local/bin/ansible-galaxy
    SHELL
  end

  ### ansible run on guestOS
  #config.vm.provision "ansible_local" do |ansible|
  #  ansible.playbook = "playbooks/site.yml"
  #  ansible.inventory_path = "playbooks/hosts/guest"
  #  ansible.verbose = "vvv"
  #  ansible.install = true
  #  ansible.limit = "all"
  #end

  ### ansible run on hostOS
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/site.yml"
    ansible.inventory_path = "playbooks/hosts/host"
    ansible.verbose = "vvv"
    ansible.limit = "all"
  end
end
