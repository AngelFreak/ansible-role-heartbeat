Heartbeat
=========

Role that does heatbeat setup on Ubuntu based systems.
The role assumes that you have a primary, and a backup server.
The role is made for haproxy, but can be used for other usecases.

Requirements
------------

This role requires Ansible 2.2 or higher, and platform requirements are listed in the metadata file.

Role Variables
--------------
The variables that can be passed to this role and a brief description about them are as follows:

    The following veriables should be defined in the playbook:

    primary: proxyatest                   # The uname -n of the primary haproxy server
    primary_ip: 192.168.x.x            # The ip of the primary haproxy server
    backup: proxybtest                    # The uname -n of the backup haproxy server
    backup_ip: 192.168.x.x             # The ip of the backup haproxy server

    The following veriables should be defined in the defaults/main.yml

    heartbeat_password "1234"             # A password for the heartbeat auth
    interface: "eth0"                   # The network interface where heartbeat will be running on
    heartbeat_sharedip: "192.168.x.x"   # The shared ip for the heartbeat

    The following variables are optional :

    heartbeat_preferred_host:             # if wanting something different than the primary name
    heartbeat_mcast_ip: "225.0.0.1"       # multicast ip address
    auto_failback: "off|on|legacy"        # defaults to off
    autojoin: "none|other|any"            # defaults to none
    # array to add additional ressources.
    # Each item is a complete line in the haresource file :
    heartbeat_resources: [ 'linuxha1 192.168.85.3 httpd smb maid::vacuum',
                           'linuxha1 192.168.85.3/27/192.168.85.16 httpd smb' ]


Example Playbook
----------------

Installs, and configures heartbeat.

    - hosts: proxy
      roles:
        - { role: angelfreak.heartbeat, primary: proxy_01, primary_ip: 192.168.1.2, backup: proxy_02, backup_ip: 192.168.1.3 }

Dependencies
------------

None.

License
-------

Unlicens

Author Information
------------------
AngelFreak

https://github.com/AngelFreak
