# Vagrant Lab

Requirements:
 - Vagrant
 - VirtualBox
 - Linux/Mac with a user with a sh key (ssh-keygeygen)
 - Ansible (pip install ansible)

# How to

Change "192.168.1.100" to the desired local IP for the VMS

Build the Lab VMs:
```sh
vagrant up
```
Test ansible:
```
ansible activemq -m ping -i vagrant-hosts
```

# Deploy ActiveMQ
```sh

# Get the roles
git clone https://github.com/shelleg/ansible-role-activemq roles/ansible-role-activemq
git clone https://github.com/abessifi/ansible-java roles/ansible-java

# Run the playbook
ansible-playbook -i vagrant-hosts activemq_playbook.yml

# Check ActiveMQ should be running in the VM
vagrant ssh -- 'ps -ef| grep java'

# Teard down
rm -rf roles/
vagrant destroy -f
```

# Credits
Initial setup based on https://gist.github.com/gnarf/b103e77f37236ca72d8e


