# kvm
<pre>
kvm builder tools
--------------------------------------------------------------
This tool will use libvirt and virt-install to provision kvm nodes on Linux.
This code was built and tested on Ubuntu 18.04.
The base images are downloaded from Ubuntu cloud using img files.
The images are configured via cloud-init and a generated cdrom iso.

Variables:
key variables are:
DISTRO:...(xenial|bionic) (default: xenial)
SWAPSIZE:.(GB) (default: 2)
DATASIZE:.(GB) (default: 0)
RAM:......(MB) (default: 2048)
VCPUS:....(COUNT) (default: 2)
NAME:.....fqdn (REQUIRED) 
NET:......(static|dhcp) (default: static)
ROOTSIZE:.(GB) (default: size of image)

Targets
help    --> This help
list    --> List currently defined libvirt nodes
targets --> Produce this listing
stats   --> Display variable info
clean   --> Clean
sources --> Build sources directory
base    --> Build qcow2 base images
image   --> libvirt node images
disks   --> Create node disks
rootfs  --> Create node rootfs disk
swap    --> Create node swap disk
data    --> Create node data disk
Delete  --> Delete node
node    --> Create node
cluster --> Create a gluster cluster

Tasks:

Build a node using defaults:
==============================
make -e NAME=some-node-fqdn node

Build a node with a data disk of 8 gb
==============================
make -e NAME=fqdn DATASIZE=8 node

Build a node from distro xenial
==============================
make -e NAME=fqdn DISTRO=xenial node

Delete a node
==============================
make -e NAME=fqdn Delete

Create a cluster
==============================
make -e PREFIX=gl COUNT=6 cluster

<pre>
This will create $COUNT number of nodes.  
The ip-addresses are assigned as static 
and must be declared in DNS, or at 
least /etc/hosts.  The hostname patterns 
are defined as ${PREFIX}${%02d COUNT}.${DOMAIN}  
</pre>

Delete a cluster
==============================
make cluster-delete

<pre>
This relies on the presence of the "./hosts" 
file in the workspace, and uses that to 
define the hostnames to delete.
</pre>

