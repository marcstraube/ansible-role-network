# network

Configure the network.


## Requirements

This role requires the ```community.general``` collection. You can install it like this: 
```ansible-galaxy collection install community.general```.

This role requires root access, so either run it in a playbook with a global ```become: true```, or invoke the role in
your playbook like:

    - hosts: 'all'
      roles:
        - role: 'marcstraube.network'
          become: true


## Role variables

Available variables are listed below, along with default values (see ```defaults/main.yml```):

    network_hostname: 'arch'

The hostname for the machine.

    network_fqdn: ''

Full qualified domain name. Will default to ```{{ network_hostname }}.localdomain```

    network_ip: ''

Use this, if the hostname is available via a permanent IP address (e.g. a web server).

    network_pptp: false

Whether to install PPTP support for VPN connections.

    network_gui: false

Whether to install the nm-applet GUI tool.

    network_captive_portal: false

Whether to install support for wireless captive portals.

    network_wifi_connections: []

A list of wireless connections to set up. Possible key value pairs for items are:

* ```SSID```        The networks SSID. Required.
* ```PSK```         Pre-Shared Key (password) for the connection. Required.
* ```interface```   Name of the interface to use for the connection.
* ```permissions``` List of users that are allowed to use the connection.
* ```overwrite```   Weather to override an already existing connection. Defaults to ```false```.


    network_install_promiscuous_service: false

Install a systemd service with which you can switch your wireless card into promiscuous mode.


## Example playbook

    - hosts: 'all'
      vars:
        network_hostname: 'myhostname'
        network_wifi_connections:
        - SSID: 'MyNetwork'
          PSK: 'password'
          interface: 'wlp2s0'
          permissions:
            - 'user1'
            - 'user2'
          override: true
      roles:
        - marcstraube.network


## License

GPLv3
