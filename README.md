[![Build Status](https://travis-ci.com/ironreality/docker-efk.svg?branch=master)](https://travis-ci.com/ironreality/docker-efk)

Role Name
=========

Containerized Elasticsearch+Fluentd+Kibana+Nginx installation

The Kibana URL: http://localhost
Kibana default login / pass: admin / admin


The detailed projects' specification see in TODO file


Requirements
------------

- the role is tested on Linux Ubuntu 16.04 via Vagrant & on Ubuntu 14.04 via TravisCI
- Docker daemon is running & listening socket localhost:2375
- Ansible version >= 2.6 installed
- docker-compose == 1.9 (newer versions can work unstable with the Ansible docker-related modules)
- sudo sysctl -w vm.max_map_count = 262144 # to run Elasticsearch 6.4

**A detailed description of the pre-configuration steps you can find in the Vagrantfile or in .travis.yml**


Role Variables
--------------

**Kibana default HTTP auth credentials: admin / admin**

To change the defaults you should define the next environment variables before the role launching:

- HTTP_AUTH_LOGIN
- HTTP_AUTH_PASS


Example Playbook
----------------

The testing playbook & inventory are placed in tests directory. So to run you should fire the command:

```
cd <repo_directory>
ansible-playbook tests/test.yml -i tests/inventory --connection=local --become
```

or you can test the role with Vagrant - you need to have Vagrant+VirtualBox installed in such case:
```
cd <repo_directory>
vagrant up
```


License
-------

BSD

Author Information
------------------

(c) Vadym Surzhyk aka Yamato
