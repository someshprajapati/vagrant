# Vagrant with VirtualBox

This guide helps you set up and use [Vagrant](https://www.vagrantup.com/) with [VirtualBox](https://www.virtualbox.org/) on macOS.

---

## Prerequisites

- [VirtualBox for Mac](https://www.virtualbox.org/wiki/Downloads)
- [Homebrew](https://brew.sh/) (for installing Vagrant)

---

## Install Vagrant

```sh
brew tap hashicorp/tap
brew install hashicorp/tap/hashicorp-vagrant
```

---

## Verify Installation

```sh
vagrant --help
```

You should see output similar to:

```
Usage: vagrant [options] <command> [<args>]
    -h, --help                       Print this help.
Common commands:
  autocomplete    manages autocomplete installation on host
  box             manages boxes: installation, removal, etc.
  cloud           manages everything related to Vagrant Cloud
  destroy         stops and deletes all traces of the vagrant machine
  global-status   outputs status Vagrant environments for this user
  halt            stops the vagrant machine
  help            shows the help for a subcommand
```

---

## Common Usage

### Start a Vagrant Environment

```sh
vagrant up
```

For more options:

```sh
vagrant up --help
```

Example output:

```
Usage: vagrant up [options] [name|id]
Options:
    --[no-]provision             Enable or disable provisioning
    --provision-with x,y,z       Enable only certain provisioners, by type or by name.
    --[no-]destroy-on-error      Destroy machine if any fatal error happens (default to true)
    --[no-]parallel              Enable or disable parallelism if provider supports it
    --provider PROVIDER          Back the machine with a specific provider
    --[no-]install-provider      If possible, install the provider if it isn't installed
    --[no-]color                 Enable or disable color output
    --machine-readable           Enable machine readable output
    -v, --version                Display Vagrant version
    --debug                      Enable debug output
    --timestamp                  Enable timestamps on log output
    --debug-timestamp            Enable debug output with timestamps
    --no-tty                     Enable non-interactive output
    -h, --help                   Print this help
```

---

## Set Up Your Project

```sh
mkdir vagrant
cd vagrant
vagrant init hashicorp-education/ubuntu-24-04 --box-version 0.1.0
```

This creates a `Vagrantfile` in your directory. Example content:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp-education/ubuntu-24-04"
  config.vm.box_version = "0.1.0"
end
```

---

## Start the Environment

```sh
vagrant up --provider=virtualbox
```

You will see output as Vagrant downloads the box, imports it, and boots the VM.

---

## SSH into the VM

```sh
vagrant ssh
```

You should see a prompt inside the Ubuntu VM. To check the OS version:

```sh
lsb_release -a
```

---

## Manage the Environment Lifecycle

**Suspend** the machine (pause and save state):

```sh
vagrant suspend
```

**Resume** the machine:

```sh
vagrant resume
```

**Halt** (shut down) the machine:

```sh
vagrant halt
```

**Destroy** the machine (delete VM and data):

```sh
vagrant destroy
```

**Remove the downloaded box** (optional):

```sh
vagrant box remove hashicorp-education/ubuntu-24-04
```

---

For more information, see the [Vagrant documentation](https://www.vagrantup.com/docs/).


## Use a Specific Vagrantfile for the Multi-Node Cluster

Start the multi-node environment:

```sh
VAGRANT_VAGRANTFILE=Vagrantfile_multinode vagrant up
```

Check the status of all nodes:

```sh
VAGRANT_VAGRANTFILE=Vagrantfile_multinode vagrant status
```

SSH into a specific node:

```sh
VAGRANT_VAGRANTFILE=Vagrantfile_multinode vagrant ssh node1
```
