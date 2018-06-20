## General overview

The stack is at heart a Debian-based sets of containers, using Nginx, PHP-FPM and MySQL.

There's a loose matching between a "service" and a "container" - although this not strictly true from a technical point of view,
and some containers actually bundle several processes together - and we refer to either term indifferently in this documentation.

## Networking

A 'named' network will be created by Vagrant at startup, and your /etc/hosts file is updated accordingly by the hostupdaters plugin.

This avoids conflicts with other docker-based solutions and allows for the use of 'preset' IPs: this is to overcome some limitations on Mac OS X and ensure - by adding some loopback aliases - that we don't have to rely on clumsy port forwarding and a project behaves consistently on all platforms.

The default network is 192.168.57.0/24, while the domain name is ce-vm.local, but this is configurable.
 
## Services/containers

The following services are currently available.

### Mandatory services

Those services can not be 'disabled', as the others depends on them, and will be created even if they're not present 
in the 'service' list of your config.yml file.

- [Log](services/log): a centralized syslog, using [Frontail](https://github.com/mthenw/frontail) as the UI.
- [Dashboard](services/dashboard): a dashboard page, containing links to other services and useful information.

### Core services

Those services are the most commonly used ones, and are enabled by default when generating a new project from [http://ce-vm.codeenigma.net](http://ce-vm.codeenigma.net). 
You can however disable them in your config.yml file - provided you know what you're doing !

- [NGINX](services/nginx): the Nginx webserver.
- [PHP-FPM](services/fpm): the php interpreter for the webserver
- [PHP-CLI](services/cli): the main 'cli' container, to run php commands (composer, drush, console, ...) via ssh.
- [MySQL](services/mysql): MySQL Community Edition

### Optional services

- [HAProxy](services/haproxy): a Proxy/Load Balancer to replicate more complex setup
- [Memcached](services/memcached): Memcached instance
- [MkDocs](services/mkdocs): Documentation generator
- [NightwatchJS](services/nightwatch): Browser automated testing
- [Redis](services/redis): Redis instance
- [Apache Solr](services/solr): Solr search indexing
- [SonarQube](services/sonar): Static code analysis