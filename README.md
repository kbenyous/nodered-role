# nodered role

## Description
Ansible role for installing and running Nodered.

It installs and  Nodered on a host, using installer script from https://github.com/node-red/node-red. It creates a 'nodered' user dedicated to running this service. it starts the service if everything is OK. It does not modify Nodered's configuration files.

## Usage
### Simple use
```(yaml)
--- 
 - hosts :myhost
   roles:
    - nodered
```

### Extra variables
| Role variable | Default value | Description |
|---------------|---------------|-------------|
|role_nodered_force_install|no (False)| Ask to always run Nodered installation script, even if Nodered was already installed |
|role_nodered_install_pi_nodes| yes (True) | Ask to install Raspberry Pi's specific nodes (for handling GPIOs, serial port, etc.)|

Example :
```(yaml)
--- 
 - hosts :myhost
   roles:
    - role: nodered
      vars:
        - role_nodered_force_install: yes
        - role_nodered_install_pi_nodes: no
```


## Requirements
Installation requires an 'admin' group on the remote host, with passwordless 'sudo' capabilities.

The installation script needs being ran by the newly created 'nodered' user. And this user needs a temporary privilege escalation. 

To enable passwordless sudo for an 'admin' group, add the following line to the /etc/sudoers config file :
```
%admin   ALL=(ALL) NOPASSWD: ALL
```

## License
MIT License