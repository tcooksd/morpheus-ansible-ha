# morpheus_ha_ansible

This is a repo of Ansible roles that allows you to provision a High Availablility Morpheus application.

## Architecture

* 2 App servers
* Odd Number Elasticsearch nodes (will support additional nodes)
  * single node implementations not supported
* Odd Number RabbitMQ nodes (will support additional nodes)
  * single node implementations not supported
* Odd Number Percona XtraDB Cluster Nodes (will support additional nodes)
  * single node implementations not supported

![alt text](https://github.com/tadamhicks/morpheus_ha_ansible/blob/master/HA.jpg "Morpheus HA Architecture Example")

### Assumptions:

* CentOS 7 only (right now)
* Entirely separated services (right now)
* A valid loadbalancer/VIP for RabbitMQ has been configured
  * Ports and server mappings for ports 5672 and 61613
* A valid loadbalancer/VIP for application tier servers has been configured
  * Ports and server mappings for ports 443 and 80

## Getting Started

The host groups for the `hosts` file are the only place that configuration needs to occur

Here is an example of a valid `hosts` file including the requisite groups:
```
[rabbit_cluster]
52.52.27.6 ansible_user=slimshady
13.56.104.200 ansible_user=slimshady
54.241.108.245 ansible_user=slimshady

[elastic_cluster]
13.56.44.24 ansible_user=slimshady
54.215.121.50 ansible_user=slimshady
13.57.169.119 ansible_user=slimshady

[db]	
52.9.94.143 ansible_user=slimshady
52.9.226.166 ansible_user=slimshady
52.8.96.0 ansible_user=slimshady

[morpheus]
13.57.66.216 ansible_user=slimshady
52.52.2.76 ansible_user=slimshady
```

Once this has been configured it is very straightforward to run the `morpheus.yml` playbook on these hosts:
```
slimshady@localhost:~$ ansible-playbook -i /path/to/hosts morpheus.yml
```# morpheus-ansible-ha
