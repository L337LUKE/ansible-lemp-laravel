# Ansible - LEMP on Ubuntu

This ansible playbook will provision servers with a full LEMP stack   
and more specifically to run PHP based apps.

Thre will be an optional extra soon to include;

- Node
- Mysql

<br>

## Prerequisites (packages)

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](https://www.vagrantup.com/downloads.html)
3. Install [Ansible](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-on-mac-osx)

<br>

### Running on virtual machine/host



This setup will show you how to get setup on your host machine.

```bash
# Login to your vagrant VM
vagrant ssh

```

<br>

```bash
# Install Python / ansible (you might have python already)
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get install -y ansible
``` 

<br>

Now you need to just generate an SSH key defined in your `provision.yml`

```bash
# Required for ansible to talk to login through SSH and run commands
ssh-keygen -t rsa -b 4096 -C "luke@weareadaptable.com" -f id_testapp

# Required in order to authenticate with github
ssh-keygen -t rsa -b 4096 -C "luke@weareadaptable.com" -f id_testapp_github
```

<br>

Now you should be ready to run ansible related commands, however to be sure  
check it works by running `ansible --version`.

<br>

## Before you get started

Before you jump into running playbooks straight away you need to make sure you  
have appropriately configured everything for security and to match your dev requirements.

### Ansible.cfg

You probably won't need to touch this file but in case you do refer to the [ansible docs](http://docs.ansible.com/ansible/intro_configuration.html) for info.

The only key thing to note here is that the file refers to a .vault_pass file.  
The file contains a single line which is the password to encrypt/unencrypt sensitive information.

**Never** add this to your VCS as you will effectively be giving the password to your `ansible-vault`. secured files.

<br>

### hosts

Here you need to specify the hosts you want to run which/what on.

**Finish this documentation**

<br>

### provision.yml

This file is the main entry point when you exectute the play-book, and is seperated by block  
of hosts.  These allow you to specify different groups of hosts to run everything on.

By default everything will get executed when running this playbook with the following `ansible-playbook --private-key=~/.ssh/id_testapp -i hosts provision.yml`. 

If for some reason you don't want to run everything in the playbook you can specify  
your own series of hosts to run by using something like the following

<br>

`ansible-playbook --private-key=~/.ssh/id_testapp -i hosts provision.yml`

<br>




## Running Ansible

```bash
cd ~/path/to/deploy-dist

# Check our Yaml Syntax

ansible-playbook --private-key=~/.ssh/id_testapp \
-i hosts \
--syntax-check \
provision.yml

# Run Everything!

ansible-playbook --private-key=~/.ssh/.pem \
-i hosts \
provision.yml

# Or, Limit runs by host
# In this example, we run only load_balancer tasks

ansible-playbook --private-key=~/.ssh/fideloperllc.pem \
-i hosts --limit=load_balancer \
provision.yml
```
