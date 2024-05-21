## About
This project hosts docker containerized e-commerce website hosted on a vagrant provisioned server.

## Requirements.
Make sure that you have the following installed and correctly configured:
- [VirtualBox and Vagrant](https://medium.com/@kadimasam/set-up-virtualbox-and-vagrant-on-ubuntu-22-04-9ac6b9ace94c)
- [Install ubuntu 20.04 vagrant image](https://app.vagrantup.com/geerlingguy/boxes/ubuntu2004)

## Installation instructions.
1. Clone the code repository.
2. Navigate into this code's root folder.
3. `vagrant up` : Power up the vagrant virtual machine.
4. `vagrant ssh` : Look up for the vm's ssh configurations. Update the hosts file (within the code) with the correct port number.  
5. `ansible-playbook playbook.yml` : Run ansible playbook which will in turn make several installations in the vm.

## Interacting with the application.
- Open your favourite browser in your host machine and in access the provisioned vm via `http://192.168.56.12:3000/`.
- Go ahead and add a product (note that the price field only takes a numeric input). You should also view all added products upon refreshing the page.