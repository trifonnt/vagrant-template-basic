# vagrant-template-basic
Basic template for Vagrant based VMs 

# Requirements
In order to run virtual machines from this project, [VirtualBox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/) are needed.

# Vagrant plugins
Plugin [vagrant-triggers](https://github.com/emyl/vagrant-triggers) is required. Pure Vagrant does not have a tear down hook to run a script before shutting down, reloading or destroying a VM.

In order to install the plugin:
```shell
vagrant plugin install vagrant-triggers
```

Plugin [vagrant-hostupdater](https://github.com/cogitatio/vagrant-hostsupdater) is optional. It updates hosts file in the host operating system with the mapping to the guest operating system. Therefore, using the hostname is possible, not only referring by IP address or setting up SSH tunnels.

In order to install the plugin:
```shell
vagrant plugin install vagrant-hostsupdater
```

Plugin [vagrant-vbox-snapshot](https://github.com/dergachev/vagrant-vbox-snapshot) is optional. It enables using VirtualBox snapshots via Vagrant.

In order to install the plugin:
```shell
vagrant plugin install vagrant-vbox-snapshot
```

# Usage
In the command line navigate to the directory where Vagrantfile is saved. In order to start the VM:
```shell
vagrant up
```
In order to connect to the VM:
```shell
vagrant ssh
```
When finished with working in the VM:
```shell
vagrant halt
```
If the VM got broken during testing, destroy it and start from scratch:
```shell
vagrant destroy
vagrant up
```
