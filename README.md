# Grafana, Graphite & StatsD with Ansible

This playbook let you easily setup [Grafana](http://grafana.org/), [Graphite](http://graphite.readthedocs.org/en/latest/) and [StatsD](https://github.com/etsy/statsd/).
You can use it to provison a dedicated server or even a virtual machine using the VagrantFile and Virtualbox

It uses [Ansible](http://www.ansible.com/) as a provisionner, make sure to install Ansible it before.

What gets installed with this playbook:

*  PostgreSQL
*  NginX webserver/reverse proxy
*  Python, Pip & VirtualEnv
*  NodeJS
*  Memcached
*  ElasticSearch
*  StatsD
*  Grahite with its components:
	* [Carbon](https://github.com/graphite-project/carbon)
	* [Whisper](https://github.com/graphite-project/whisper)
	* [The Graphite webapp](https://github.com/graphite-project/graphite-web)
* And finally [Grafana](http://grafana.org/)


## Running it

You shoud **configure** your install by modifying the variables in the _graphite.yml_, see the section *Configure your Grafana/Graphite install* below.

### Using Vagrant
If you want to install Grafana/Graphite on a VM using Vagrant, you need to install [Vagrant](http://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/) first.

Then hit:
```
$ vagrant up --provision
```

### Configure your Grafana/Graphite install

Many configuration options are present in the _graphite.yml_ file, you sould take a deep look at it.
**You should at least change**:
- _graphite.secret_key_ : Generate a new one from [here](http://www.miniwebtool.com/django-secret-key-generator/))
- _grafana.nginx_htpasswd_ : Generate your own login/password from [here](http://htpasswd.i-connector.com/))

## Misc

### Different OSes

By default, the Vagrant box runs Ubuntu 12.04, but the playbook supports Debian 7 and CentOS 6.4 as well! To try those out, uncomment the appropriate lines in the Vagrantfile and comment out the Debian lines.

### Known issues

* On CentOS, the firewall is completely closed by default (at least on the box I tried it with). So you have to manually open the relevant port (80) using `iptables`, or if you're not concerned about security (because you're running it locally through Vagrant), you can always flush the firewall with `iptables -F`.


## Thanks

This project is originally based on

- Graphite install repository from [DandyDev](https://github.com/DandyDev) that you can find [here](https://github.com/DandyDev/graphite-statsd-ansible-vagrant)
- Graphana Ainsible role from [Torkelo](https://github.com/torkelo) that you can find [here]([grafana](https://github.com/torkelo/grafana).

Many thanks to them.
