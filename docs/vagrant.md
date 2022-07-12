# Vagrant

Vagrant is a software packages, which allows to easily deploy reproducible development environments. This is done by setting up virtual machines using simple init files.

## Resources
* https://learn.hashicorp.com/collections/vagrant/getting-started

## Vagrantfile
To start a Vagrant environment, you need a `Vagrantfile` in the directory, where you want to start the environment. The most basic Vagrantfile looks like this
``` vagrant
# define the version of Vagrantfile to be used (this should not be changed)
Vagrant.configure("2") do | config |
  # define the virtual box to be used
  config.vm.box = "hashicorp/bionic64"
end
```
Alternatively, you can do `vagrant init hashicorp/bionic64` in the terminal, which creates a default `Vagrantfile`, which is well commented and shows additional options for the vagrant file.
To find other virtual boxes, you can check [this link](https://app.vagrantup.com/boxes/search).

## Interacting with a Vagrant environment
To start an environment simply navigate to the directory, where you placed your `Vagrantfile` and type in the termin
``` bash
vagrant up
```
To SSH into the virtual machine, you can type
``` bash
vagrant ssh
```
## Changing the Vagrantfile
If you wanted to perform some changes on the Vagrantfile, you can reload the virtual environment with those new changes by using
``` bash
vagrant reload
```

## Adding additional files to the Vagrant environment
By default, the virtual machine shares a files, which are placed in the directory, where the `Vagrantfile` is placed. To find these files you have to navigate to `/vagrant` within the virtual machine. The shared directories can be changed by additional commands in the `Vagrantfile`.

## Sharing the environment
If we want to share our environment, with anyone with a internet connection, we can use the plugin `vagrant share`.
To install the plugin we we have to install `ngrok`. Then we can install the plugin using
``` bash
vagrant plugin install vagrant-share
```
We can then share the environment using
``` bash
vagrant share
```
This outputs an URL at which our virtual machine is accessible from.

## Ending a virtual machine

 There are three different ways to stop a vagrant environment
1) `vagrant suspend`: Machines stops and current running state is preserved. The machine still uses disk space and requires addtional space to store the data of the RAM. This is mainly for quick powering down and up.
2) `vagrant halt`: Shuts down the machine, while presevering the contents of the disk and allowing to start it again.
3) `vagrant destroy`: Removes all traces of the guest machine from your system.
