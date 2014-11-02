# vertica-vagrant


This repository contains a set of [Ansible](http://docs.ansible.com/) playbooks for provisioning the virtualized [HP Vertica](http://vertica.com) instances in [VirtualBox](https://www.virtualbox.org/) using [Vagrant](https://www.vagrantup.com/).

Vertica is an columnar database from HP. Unfortunately, the installation process is somewhat cumbersome and it isn't easy to get up and running.

Disclaimer: HP Vertica is a big-data analytical platform which requires a lot resources to run at its best. The virtual instance presented here is configured to run with 4GB of memory and 2 dedicated CPUs and, therefore, is not suitable for anything beyond very simple use-cases. Virtual instance configuration can be changed in `Vagrantfile`.


## Running

In order to start the virtualized Vertica instance, you will need Anbible, Vagrant and VirtualBox installed.

Once the dependencies are satisfied, clone this Git pository:

```bash
git clone git@github.com:semberal/vertica-vagrant.git
```

Next, download the Vertica 7 Community edition from the [Vertica portal](https://my.vertica.com/community/) (you will need to create an account there) and download the Vertica community edition for Ubuntu 14.04 LTS, the latest version is 7.1.1 (as of 01/11/2014). Rename the downloaded _*.deb_ package to `vertica7.deb` and put it next to the `Vagrantfile` into the cloned repository.

As the final step, execute `vagrant up`. Now, Vagrant will boot virtual instance from the Ubuntu 14.04 LTS image, copy the _vertica7.deb_ package into the guest system and run ansible provisioner, which will configure the instance.

*Note:* `vagrant up` execution occasionally fails with a ssh _connection refused_ error, but unfortunately, I haven't figured out why, yet. If you run into such error, try to manually run `vagrant provision`, which won't recreate virtual instances, but will only run configured Vagrant provisioners (_file_ and _ansible_, in our case).

## F.A.Q.

### Is is possible to provision a multi-node Vertica cluster?

Unfortunately not. Even though would be a relatively simple change, I currently do not posses a computer with sufficient amount of memory to test it (32GB+ would be necessary).
