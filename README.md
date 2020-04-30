# Infrastructure Generator

This repository will help you to build your infrastructure of virtual machines for testing, development or production.

The built infrastructure will be a set of virtual machines with full network connectivity.  
Each VM will have an own IP address and hostname and will see others machines in the cluster (by IP or hostname).  
On every VM there will be added user with sudo privileges, created private and public key for him, and sent the public key for the rest set of machines in the cluster.  
Therefore, in each single machine the user will be available to connect to other VMs using SSH key authentication.

## Vagrant

You can use Vagrant to build your infrastructure for testing or development purpose.  

In order to do so, you must firstly download and install Vagrant and VirtualBox:  
- Vagrant - enables users to create and configure lightweight development environments  
  https://www.vagrantup.com/
- VirtualBox - hosted hypervisor for x86 virtualization  
  https://www.virtualbox.org/
  
**Note**: if you are Linux / MacOS user you may want to have changed <code>vagrant</code> directory to your own:
```bash
$ sudo chown -R $USER: ~/.vagrant.d
```

If you have Vagrant and VirtualBox downloaded you can now set up your cluster.   
To do so, open the <code>vagrant/Vagrantfile</code> file and prepare your configuration.  
The example configuration is:
```ruby
# OS which will be installed on VMs (all available images on https://app.vagrantup.com/boxes/search)
IMAGE_NAME = "centos/7"

# On every machine there will be added user with sudo privileges with this name
ADMIN_USERNAME = "admin"

# Password for the user above
ADMIN_PASSWORD = "12345"

# Description of the cluster.
# Each element here is a single virtual machine.
# Each VM is a pair of hostname and set of features:
# - IP address
# - number of CPUs
# - Memory (in MB) 
CLUSTER = {
    "node-master" => {
        :ip => "192.168.33.101",
        :cpus => 2,
        :mem => 4096
    },
    "node-slave" => {
        :ip => "192.168.33.102",
        :cpus => 2,
        :mem => 4096
    }
}
```

To get the infrastructure ready just type:
```bash
$ cd infrastructure\vagrant
$ vagrant up
```

Now, you can connect to any of the VM by the IP address using user and password defined in the infrastructure configuration.

If later you want to destroy your infrastructure type:
```bash
$ vagrant destroy -f
```
