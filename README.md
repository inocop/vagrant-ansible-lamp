## Software version

### VirtualBox
version 5.0.14

### ansible
```
$ ansible --version
ansible 2.0.0.2
```

### Vagarant
```
$ vagrant --version
Vagrant 1.8.1
```

### Vagarant plugin
```
$ vagrant plugin install vagrant-vbguest
```

## Start (ansible run on hostOS)
```
$ git clone https://github.com/inocop/vagrant-ansible-lamp.git
$ cd vagrant-ansible-lamp
$ vagrant up
```

## Start (ansible run on guestOS)
```
$ git clone https://github.com/inocop/vagrant-ansible-lamp.git
$ cd vagrant-ansible-lamp
$ vi Vagrantfile
  ## ansible run on guestOS
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbooks/site.yml"
    ansible.inventory_path = "playbooks/hosts/guest"
    ansible.verbose = "vvv"
    ansible.install = true
    ansible.limit = "all"
  end

  #### ansible run on hostOS
  #config.vm.provision "ansible" do |ansible|
  #  ansible.playbook = "playbooks/site.yml"
  #  ansible.inventory_path = "playbooks/hosts/host"
  #  ansible.verbose = "vvv"
  #  ansible.limit = "all"
  #end
$ vagrant up
```

## Author
inocop

## License
MIT
