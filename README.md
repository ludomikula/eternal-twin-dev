eternal-twin development environment
====================================

This vagrant setup creates a virtualbox machine based on Ubuntu Bionic x64 image and
installs all tools and software required to develop on the eternal-twin platform. 

Usage:
------
1. Download and install LATEST virtualbox from official page: https://www.virtualbox.org/wiki/Downloads
   To verify the installation, run VBoxManage from console:
      - on windows:
        "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" --version
      - on nix: VBoxManage --version
   You should see virtualbox manager version printed, eg: 6.0.0r127566

2. Download and install LATEST vagrant from official page: https://www.vagrantup.com/downloads.html
   To verify the installtion, run console:
      vagrant -v
   You should see vagrant version printed, eg: Vagrant 2.2.6
   Please not that at least version 2.2.4 is required for the required vagrant plugins to work correctly.

4. From console change your current working directory to the directory where this README is located and
   start the provisioning with command:
      vagrant up --provider virtualbox

After couple of minutes your new virtual environment will be ready.
Once the process is finished, you can login to the box using:
    vagrant ssh

Once loged in, you'll be greeted with some hints and information how to proceed further.


Useful vagrant commands:
------------------------

Start vagrant box (builds the box if it does not exist) 
```vagrant up```

Stop vagrant box (same as computer shutdown) 
```vagrant stop```

Restart system in vagrant box 
```vagrant reload```

Suspend vagrant box (same as putting computer to sleep) 
```vagrant suspend```

Resume suspended vagrant box 
```vagrant resume```

Synchronize changes made in directory where this file is located to the box 
```vagrant rsync```

Rerun provisioning without restarting the operating system inside vagrant box 
```vagrant provision```

Restart system in vagrant box and rerun provisioning 
```vagrant reload --provision```

Completely remove the virtual machine (everything inside will be deleted!) 
```vagrant destroy```


