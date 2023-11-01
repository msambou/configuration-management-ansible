# Configuration Management using Ansible

## Create 3 VMS
- Master VM
- vm1
- vm2

## VM Specification
- Ubuntu Server 22.04
- Standard_B1ms (1 vcpu, 2 Gib RAM)
- Use password authentication

## Commands to run after first login

  sudo apt update
  
## Configure Master VM
SSH into the master VM and run the following commands:

  ssh-keygen

When asked to "Enter file in which to save the key", hit the enter key.
When asked for a passphrase, hit the enter key.

## Copy SSH Key to the VM Fleet (VM1 and VM2)

  cat .ssh/id_rsa.pub

Copy the contents of the above command. We will paste these into the authorized_keys file in vms 1 and 2

## Configure VMs 1 and 2
SSH into vm1 and generate a new SSH Key

  sudo apt update
  ssh-keygen

Open the authorized_keys file

  nano .ssh/authorized_keys

Paste the public key you copied from the master vm into this file.
Save the file by running CTRL + O and exit the editor by running CTRL + X
Repeat the above steps for vm2.

## Install Ansible on the Master VM

  sudo apt install ansible

## Check the version of Python running on vms 1 and 2

  python3 --version

The output of the above command should be Python 3.10.12

## Use Ansible to update the version of Python to 3.11.x

### Create an Inventory File

  mkdir ansible
  cd ansible
  nano inventory.ini

Paste the following into the file:

  [servers]
  server1 ansible_host=<vm1-ip-address> ansible_user=<your-server-username>
  server2 ansible_host=<vm2-ip-address> ansible_user=<your-server-username>
  
  
  