Role Name
=========

Containerized Elasticsearch+Fluentd+Kibana+Nginx installation


Requirements
------------

A detailed description of the prerequisites you can find in .travis.yml

- the role is tested on Linux Ubuntu 16.04
- Docker daemon is running & listening socket localhost:2375
- Ansible version >= 2.6 installed
- docker-compose == 1.9 (newer versions could work unstable with the Ansible docker-related modules)
- sudo sysctl -w vm.max_map_count = 262144 # to run Elasticsearch 6.4

Role Variables
--------------

Kibana default HTTP auth credentials: admin / admin

To change the defaults you should define the next environment variables before the role launching:

HTTP_AUTH_LOGIN
HTTP_AUTH_PASS



Example Playbook
----------------

The testing playbook & inventory are placed in tests directory. So to run you should fire the command:

ansible-playbook tests/test.yml -i tests/inventory --connection=local --become


License
-------

BSD

Author Information
------------------

The detailed projects' specification see in TODO file
