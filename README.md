# Ansible-PowerMax-interface

This ansible playbook allows for a quick way to enable and disable ports on a powermax, this includes Frontend (FA) and SRDF port (RA).
As powermax is not a linux system, and the default powermax ansible modules do not support enabling/disabling ports
, we utilize symcli to communicate with the powermax. This ansible playbook assumes you have a workign setup with symcli.
## Requirement

* symcli

## Function

Define one or more powermax in the inventoryfile.
You may call them whatever you like
make sure there is a file named pmax1.yml that matches what you name the powermax in the inventory file.
So if you name it pmax1 create a file named pmax1.yml under the host_vars

In this file specify the ip of the symcli host that can communicate with the PowerMax, this could be the same host as you run the ansible from.

If that is the case specify ansible_host: "127.0.0.1" or localhost else specify the ip of the host running symcli

If this is a remote host, make sure ssh with ssh-key authentication is setup and working.

you can specify multiple FA and RA ports to enable/disable at once
example:

```
FA_Ports:
  - "1D,25"
  - "2D,25"

RA_Ports:
  - "4E,7"
```

all these ports will be enabled or disabled in one single run depending the playbook you run:

enable-FA-ports -> will enable the FA ports
enable-RA-ports -> will enable the RA ports

## how to use

1) set all powermax with a name in the inventory file
2) create a host var file per switch with the same name you used in the inventory file.
3) make sure you define all the ports you want to enable or disable. This is per PowerMax so that you can have different ports per PowerMax if needed

 ## Executing

 
- - -
 ### manually

 ``` 
ansible-playbook playbooks/enable-FA-ports.yaml
 ```

