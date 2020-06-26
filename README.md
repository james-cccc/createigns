Ansible Role: CreateIgns
=========

This role was put together to help assist performing Openshift 4 deployments on VMWare ESXi where static IPs are required but where DHCP is allowed to give out temporary addresses. The role creates a base64 encoded ignition file for each Red Hat CoreOS server that contains the static specific IP and network configuration as required. 

I have also started to put together another role which will not only create the new ignition files but then provision the VMs as well. I've validated that this works with an ESXi instance hosted on Packet.

https://github.com/james-cccc/ocp_modign_ova_deploy

Requirements
------------

The role expects that 'vanilla' igniton files have already been created as elements of them will be consumed. 

Role Variables
--------------

Available variables are listed below, along with example values (see vars/main.yml):

The ign directory is where the previously created 'vanilla' ignition files are, and the output directory is where you want the files that will be created to go. 
```yaml
ign_directory: /home/vagrant/ocp4
output_directory: /home/vagrant/ignition/roles/createigns/files 
``` 

The webserver host and port that hosts the bootstrap ignition file.
```yaml
webserver: 10.80.158.5:8080
``` 

Network configuration of the estate
```yaml
netmask: 255.255.255.240
cidr: 28
gateway: 10.80.158.1
dns: 10.80.158.5
domain: jftest.com
```

Openshift cluster name
```yaml
cluster_name: ocp4
```

Hostname and required IP address of the bootstrap node.
```yaml
bootstrap:
  - hostname: bootstrap.ocp4.jftest.com
    ip: 10.80.158.6
```

Hostname, IP and function (worker or master) of the required nodes in the cluster.
```yaml
nodes: 
  - hostname: master0.ocp4.jftest.com
    ip: 10.80.158.7
    function: master
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
---
- name: Generate Modified Configuration Files 
  hosts: localhost
  roles: 
   - createigns
```

License
-------

MIT License

Author Information
------------------

Thie role was created in 2020 by James Force

https://sysadm.life/
