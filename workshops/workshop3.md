**Institute of Systems Science  National University of Singapore**



# NICF – Agile Continuous Delivery



# Workshop 3

# Automated environment provisioning for sample application









**Copyright 2014 ThoughtWorks. The contents contained in this document may not be reproduced in any form or by any means, without the written permission of ISS and NUS, other than for the purpose for which it has been supplied.**


**Objective: To create scripts that configure a system automatically.**

**Software:**

Puppet, Vagrant

**What you will learn:**

- Basics of using Puppet to manage your infrastructure
- Basics of using Vagrant to work with virtual environments on your machine

**Setup:**

You have been provided with an ISS workstation. It has Vagrant pre-installed, along with an Ubuntu disk image.

**Instructions:**

1. Open a command prompt
2. Create a folder puppet-exercise on local machine and cd into it

d:

cd \workshops

mkdir puppet-exercise

cd puppet-exercise

1. Add web and db boxes to vagrant. Use following commands

vagrant box add web d:\boxes\lucid32.box

vagrant box add db d:\boxes\lucid32.box

1. Create a file named "Vagrantfile" in puppet-exercise folder, using your favorite text editor. This file is used by Vagrant to configure the servers that it controls. The Vagrantfile should look like this:

Vagrant.configure("2") do |config|
  config.vm.define "web" do |web|
    web.vm.box = "web"
    web.vm.hostname = "web"
  end

  config.vm.define "db" do |db|
    db.vm.box = "db"
    db.vm.hostname = "db"
  end
end

1. Start web and db servers

vagrant up

1. What output do you see? The two servers should start without errors.
2. Login into the box. You should have 2 running linux servers. Make a note of the login message.

vagrant ssh web

exit

vagrant ssh db

exit

1. Destroy the boxes

vagrant -f destroy

**Instructions to run puppet with vagrant**

1. Edit "Vagrantfile" in puppet-exercise folder. The modified file runs puppet script after starting the box. The Vagrantfile should look like this:

Vagrant.configure("2") do |config|
  config.vm.define "web" do |web|
    web.vm.box = "web"
    web.vm.hostname = "web"
    web.vm.provision "shell", inline: "apt-get update"
    web.vm.provision :puppet do |puppet|
      puppet.manifests\_path = ""
      puppet.manifest\_file = "base.pp"
    end
  end

  config.vm.define "db" do |db|
    db.vm.box = "db"
    db.vm.hostname = "db"
    db.vm.provision "shell", inline: "apt-get update"
    db.vm.provision :puppet do |puppet|
      puppet.manifests\_path = ""
      puppet.manifest\_file = "base.pp"
    end
  end
  
end

1. Create puppet configuration "base.pp". This is used by puppet to configure your servers. It should look like:

node default {
  group { "puppet":
      ensure => "present",
     }
  File { owner => 0, group => 0, mode => 0644 }
  file { '/etc/motd':
       content => "Welcome to your Vagrant-built virtual machine!
         Managed by Puppet.\n"
     }
}

1. Start the web and db servers again

vagrant up

1. Login into web

vagrant ssh web

1. You should see this welcome message on the console:

"Welcome to your Vagrant-built virtual machine!
         Managed by Puppet."

**Instruction to install a package using puppet**

1. Destroy the vagrant boxes from previous steps

vagrant -f destroy

1. Add the following code to your base.pp to install apache and sqlite3 on your servers

node 'web' inherits default {
 user { "web" :
    ensure => "present",
    managehome => true,
    comment => "Web user",
    home  => "/home/web",
    shell  => "/bin/bash",
    uid   => 1234
    }
 package { "apache2" :
    ensure => "latest"
 }
}

node 'db' inherits default {
 user { "db" :
    ensure => "present",
    managehome => true,
    comment => "DB user",
    home  => "/home/db",
    shell  => "/bin/bash",
    uid   => 1235
    }
 package { "sqlite3" :
    ensure => "latest"
 }
}

1. Bring up the boxes

vagrant up

1. Log onto each server and check that the right users have been created

vagrant ssh web

sudo su - web

exit

exit

vagrant ssh db

sudo su – db

exit

exit

1. You should see apache installed on web box and sqlite3 installed on db box.

vagrant ssh web

aptitude search apache2 | grep ^i

exit

vagrant ssh db

aptitude search sqlite3 | grep ^i

exit
