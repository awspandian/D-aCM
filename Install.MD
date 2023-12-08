Steps to Install Ansible Belwo

using Python install ansible
# https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

using core install ansible
#  https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html

EXECUTE BELOW COMMANDS IN ALL NODES:
# Create one new user # (comman to Ansible machines)
$ sudo useradd ansible
$ sudo passwd ansible

# Provide sudoer permissions (like root user)
$ sudo visudo
ansible ALL=(ALL) NOPASSWD: ALL

# Activate Password Authentication YES
$ vi /etc/ssh/sshd_config
PasswordAuthentication yes (Might be default value NO, change to YES)

# Restart sshd service
$ sudo systemctl restart sshd

# Switch to Ansible user
$ sudo su - ansible

// Only in Controller Node
# Generate a new KEY-PAIR using SSH  
$ ssh-keygen

# Copy Public Key (Authorized Keys) into Managed Nodes
$ ssh-copy-id ansible@<Private-IP>

# Install Python on the instance
$ sudo yum install python3 -y
$ python3 --version
$ sudo yum install python3-pip –y

# Install Ansible
$ pip3 install ansible --user
$ ansible --version


# by default ansible will check teh ansible.cfg in /ect/ansible/ansible.cfg location; if required can change as need.
 
$ sudo mkdir /etc/ansible

$ sudo vi /etc/ansible/ansible.cfg

[defaults]
inventory = /etc/ansible/hosts
sudo_user = ansible
:wq (save and quit) 

# https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html

## Ansible automates tasks on managed nodes or “hosts” in your infrastructure, using a list or group of lists known as inventory. You can pass host names at the command line, but most Ansible users create inventory files. Your inventory defines the managed nodes you automate, with groups so you can run automation tasks on multiple hosts at the same time. Once your inventory is defined, you use patterns to select the hosts or groups you want Ansible to run against.

## The simplest inventory is a single file with a list of hosts and groups. The default location for this file is /etc/ansible/hosts. You can specify a different inventory file at the command line using the -i <path> option or in configuration using inventory.

$ sudo vi /etc/ansible/hosts


[atlanta]
host1
host2

[raleigh]
host2
host3

[southeast:children]
atlanta
raleigh

[southeast:vars]
some_server=foo.southeast.example.com
halon_system_timeout=30
self_destruct_countdown=60
escape_pods=2

[usa:children]
southeast
northeast
southwest
northwe
:wq

$ ansible all --list-hosts

