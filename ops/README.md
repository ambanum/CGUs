# CGUs-ops

Recipes to setup infrastructure and deploy CGUs app

> Recettes pour mettre en place l'infrastructure et déployer l'application CGUs

## Requirements

- Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

### [For developement only] Additionals dependencies

To test the changes without impacting the production server, a Vagrantfile is provided to test the changes locally in a virtual machine. VirtualBox and Vagrant are therefore required.

- Install [VirtualBox](https://www.vagrantup.com/docs/installation/)
- Install [Vagrant](https://www.vagrantup.com/docs/installation/)

## Usage

To avoid making changes on the production server by mistake, by default all commands will only affect the vagrant developement VM. Note that the VM need to be started before with `vagrant up`.\
To execute commands on the production server you should specify it by adding the option `-i inventories/production.yml` to the following commands:

- To setup a phoenix server:
```
ansible-playbook ops/site.yml
```

- To setup infrastructure only:
```
ansible-playbook ops/infra.yml
```

- To setup `CGUs` app only:
```
ansible-playbook ops/app.yml
```

Some useful options can be used to:
- see what changed with `--diff`
- simulate execution with `--check`
- see what will be changed with `--check --diff`

### Tags

Some tags are available to refine what will happen, use them with `-t`:
 - `setup`: to only setup system dependencies required by the app (cloning repo, installing app dependencies, all config files, and so on…)
 - `start`: to start the app
 - `stop`: to stop the app
 - `restart`: to restart the app
 - `update`: to update the app (pull code, install dependencies and restart app)

For example, you can update `CGUs` by running:
```
ansible-playbook ops/app.yml -t update
```