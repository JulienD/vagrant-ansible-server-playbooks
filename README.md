# Vagrant Ansible Node.js env.

This is a simple recipe for *vagrant* that sets up an Ubuntu virtual machine including common daemons and tools required for Node.js development.

This project aims to make spinning up a simple development environment and avoid loosing time creating virtual machines.

All the provisionning is done with `Ansible`.

## LAMP environnement

This project is designed to install all needed for web developpement on a LAMP architecture.
It will install the following on an Ubuntu 14.04 linux VM:

- Node.js
- MySQL 5.5.x
- Git

## Other environnements

The repository hosts several development environnements you can access in the other branches. Each of them are designed to answer to specific needs.

- ubuntu-14.04-lamp-dev
- ubuntu-14.04-nodejs-dev

## Requirements

- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](http://www.vagrantup.com/)
- [Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)

Preferably in their latest versions from the web sites.

## Getting started

Clone this repository to a local directory and change the name of it:

    git clone https://github.com/JulienD/vagrant-ansible-server-playbooks.git nodejs-dev-env

Go into the directory and run:

    vagrant up

This should download, run and provision the virtual machine.

If something goes wrong, have a look at `provisionning/playbook.yml`. You can re-provision the VM using at any moment when you change the configuration:

    vagrant provision

When you're done playing with the VM, you can delete it:

    vagrant destroy

## Customize the installation

Ansible tags are used to manage and group sets of actions. This mean you can choose to add specific actions in addition to the default provisionning your Vagrantfile.

    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.tags="common"
    end

In the above example, in addition to the common package, all the action in the recipe tagged with the drush tag will be executed.

For more details have a look at the file `provisionning/playbook.yml` and look for the `tags` property.

### Available tags

- common

## Why not respecting Ansible best practices

For months I've been using the classical Ansible structure management by having a separated dir for each components. This structure work really fine and is useful for sys-admin when they have to manage and maintain a lot of component, but for a local dev machine it's too much (this is my point of view).

I decided to rewrite all my development machines recipes in a flattern file way where everything is accessible at the first glance and doesn't require to navigate in dozens of sub-folders and file. KISS
