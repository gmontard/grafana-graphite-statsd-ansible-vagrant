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


## Setup

Before running this playbook you need to configure a few things, mostly **for your own security**.
All the configuration variables are held under the _graphite.yml_ file, I suggest you to take a look at each of them.

Here the most important one for Graphite:
- _graphite.secret_key_ : This is the django secret signin key, generate your own [here](http://www.miniwebtool.com/django-secret-key-generator/)
- _graphite.nginx_server_name_ : The domain or IP address on which you will access graphite
- _graphite.nginx_htpasswd_ : The .htaccess content, you can generate one from [here](http://htpasswd.i-connector.com/)
- _graphite.nginx_enable_ssl_ : Wherever or not you want to use SSL, I **strongly** advise you to do so if you don't your credential to be sent in clear mode
- _graphite.nginx_ssl_cert_ : If you enable the SSL you need an SSL certificate (.crt or .pem), use the name of it here and put it inside the /files/ssl directroy
- _nginx_ssl_key_ : If you enable the SSL you need an SSL certificate (.key), use the name of it here and put it inside the /ssl directroy

Here the most important one for Grafana:
- _grafana_version_ : The version of Grafana to use, check for the latest one
- _grafana_nginx_server_name_ : The domain or IP address on which you will access grafana
- _grafana_nginx_htpasswd_ : The .htaccess content, you can generate one from [here](http://htpasswd.i-connector.com/)
- _grafana_nginx_enable_ssl_ : Wherever or not you want to use SSL, I **strongly** advise you to do so if you don't your credential to be sent in clear mode
- _grafana_nginx_ssl_cert_ : If you enable the SSL you need an SSL certificate (.crt or .pem), use the name of it here and put it inside the /files/ssl directroy
- _grafana_nginx_ssl_key_ : If you enable the SSL you need an SSL certificate (.key), use the name of it here and put it inside the /ssl directroy

Then you will be able to access:
- **StatsD**: http://your_box_ip_or_domain:8125
- **Graphite**: http://graphite.nginx_server_name:8082
- **Grafana**: http://grafana_nginx_server_name


## Running it with Vagrant

If you want to install Grafana/Graphite on a VM using Vagrant, you need to install [Vagrant](http://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/) first.

Then hit:
```
$ vagrant up --provision
```

## Deploying with Ansible

Before running the command below you need to add the ip of your target server into the _ansible_hosts_ file
```
$ ansible-playbook -v -i ansible_hosts playbook.yml -e target=servers
```

## Generating an SSL Certificate

If you don't own a valid SSL certificate you can still generate a self signed on:
```
$ cd files/ssl ; openssl req -x509 -newkey rsa:2048 -keyout ssl_certif.pem -out ssl_certif.pem -days 365 -nodes
```


## Misc

### Different OSes

By default, the Vagrant box runs Ubuntu 12.04, but the playbook supports Debian 7 and CentOS 6.4 as well! To try those out, uncomment the appropriate lines in the Vagrantfile and comment out the Debian lines.

### Known issues

* On CentOS, the firewall is completely closed by default (at least on the box I tried it with). So you have to manually open the relevant port (80) using `iptables`, or if you're not concerned about security (because you're running it locally through Vagrant), you can always flush the firewall with `iptables -F`.


## Thanks

This project is originally based on

- Graphite install repository from [DandyDev](https://github.com/DandyDev) that you can find [here](https://github.com/DandyDev/graphite-statsd-ansible-vagrant)
- Grafana Ainsible role from [Bobrik](https://github.com/bobrik) that you can find [here](https://github.com/bobrik/ansible-grafana)

Many thanks to them.
