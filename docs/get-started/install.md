
Major Linux distributions, Mac OS X and Windows should be supported.

## Requirements

- Ensure you have a fair amount of RAM (8G recommended).
- Git must be available on your host machine

**Windows:** Ensure the git executable is accessible as `git` on the command line, not as `git.exe`

## Vagrant

Vagrant is used to orchestate and coordinate the containers, but also to make a few adjustments to the
setup based on your host OS.
The ce-vm implementation does not use VirtualBox, but Docker only.

### Version
Install a recent Vagrant version from [www.vagrantup.com](https://www.vagrantup.com). 

**Linux:** Do NOT use the version from your distribution repositories; those are always outdated. Use the official version provided at [www.vagrantup.com](https://www.vagrantup.com).

You also need the 'vagrant-hostsupdater' plugin, that can be installed with:
```
vagrant plugin install vagrant-hostsupdater
```

## Docker

Docker is used as a Vagrant provider. You need a recent version of the native app from [docker.com](https://www.docker.com/community-edition#/download).

### Mac OS host

The older "boot2docker / Docker Toolbox" implementations that were using an extra VM layer using Virtualbox are not supported by ce-vm.

### Windows host

The older "boot2docker / Docker Toolbox" implementations that were using an extra VM layer using Virtualbox are not supported by ce-vm.

### Linux host

The Docker daemon can only be managed by the root user by default. As with any other Docker-based stack, this means you either have to:

- Run each and every `vagrant` command using sudo. Besides the obvious security issues, it also means that the ce-vm base will get installed 
under the root user home dir instead of yours, and that all files, including your codebase will be owned by the root user.
In practice, this is very unpractical.
- Add yourself to the "docker" group, so you can run `vagrant` commands as your standard unprivileged user - see [docs.docker.com](https://docs.docker.com/engine/installation/linux/linux-postinstall/) for details. It does solve the issue, but this poses a security risk you need to be aware of and understand. See [here for details](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface). Some users tend to just "live with it" as it is the most convenient solution, but we strongly advise you not to do this.
- The recommended solution -until it gets fixed in [vagrant](https://github.com/hashicorp/vagrant/issues/8111)- is to wrap 'docker' so it forces a sudo call. See the [tips](/tips/scripts/#vagrant-docker-sudo.sh) section for usage.


## ce-vm

There is nothing more to do. The "stack' itself will install itself when you `vagrant up` for the first time, by git cloning the main ce-vm repo from https://github.com/codeenigma/ce-vm/ as ~/.CodeEnigma/ce-vm/5.x/ce-vm-upstream on your host.
