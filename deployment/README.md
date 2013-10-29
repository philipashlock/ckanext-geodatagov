Packaging data.gov 
==================

### Vagrant

If you're developing with Vagrant. First install Virtualbox and Vagrant:

Download and install the lastest version of Virtualbox
https://www.virtualbox.org/wiki/Downloads

Download and install the latest version of Vagrant
http://downloads.vagrantup.com/

### Ansible
If you're using Vagrant, still continue on with the directions for Ansible. Vagrant will use the Ansible for provisioning. 

Make sure pip is installed on your system
http://www.pip-installer.org/en/latest/installing.html

Install ansible on your local machine (probably ok to do this globally)

```
pip install ansible
```

Have a bare centos box that you have ssh login too. We shall assume this machines ipaddress is 192.168.19.98

Make a hosts file (eg /etc/ansible/hosts) that has the following entry. For Vagrant, you can just put the hosts file in the same place as your Vagrantfile and the ip address of the hosts file should match the ip address in your Vagrantfile. 

```
[build]
192.168.19.98
```

Run the ansible playbook

```
ansible-playbook datagov-buildserver.yml
```

You may have to supply connection parameters to ansible-playbook i.e private-key or password to connect.  See ansible-playbook --help

To run ansible with your Vagrant machine you'll need to supply some additional parameters. Try:

```
ansible-playbook -i hosts datagov-buildserver.yml -u vagrant -k --ask-pass --sudo -c paramiko
```

You are asked to supply ckan version and iteration. The ckan version refers to the github release, eg for the release-datagov branch of CKAN on github you would enter 'datagov' as the release. 

This should do everything and the rpm is in /var/www/


