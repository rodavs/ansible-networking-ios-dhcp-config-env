Role Name
=========

This role deploys the isc-dhcp-server and tftpd-hpa server on Ubuntu 18.04 - 20.04 and Redhat 7  boxes to create a DHCP enviroment for providing routers default configurations.

Requirements
------------

This role used the ipaddr filter module and needs the nmcli module to function correctly

Role Variables
--------------

dhcp_server: localhost			  - Set to dhcp server as defined in the inventory file 
tftp_server: localhost			  - Set to tftp server as defined in the inventory file
tftp_dir: /var/srv/pxe/tftp		- Path for the tftp directory
dhcp_iface_name: "enp1s0" 		- Change to interface name for the dhcp server facing devices to be configured
dhcp_iface_addr: 10.0.0.1/24	- Interface IP for DHCP Server 
dhcp_network: 10.0.0.0/24		  - DHCP network definition 
tftp_iface_name: "enp1s0"		  - Change to interface name for the tftpd server facing devices to be configured
tftp_iface_addr: 10.0.0.1/24	- Interface IP for DHCP Server, change if splitting out roles on seperate hosts
tftp_network: 10.0.0.0/24	                	- TFTP network definition
PXE_Hosts:				                          - Dict of routers to be configured
  - name: Router1			                      - Router Name
    EthAddr: "00:07:7d:55:92:ba" 	          - Mac Address of the router
    IP: 10.0.0.100			                    - DHCP given ip for the router
    Bootfile: "default-ios-config-Router1"  - Bootfile make distinct for multiple devices
  - name: RouterZ                           - Router Name
    EthAddr: "00:07:7d:55:92:dd"            - Mac Address of the router
    IP: 10.0.0.101                          - DHCP given ip for the router
    Bootfile: "default-ios-config-RouterZ"  - Bootfile make distinct for multiple devices
.....

Dependencies
------------

nmcli 

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

---
- hosts: control
  gather_facts: yes
  tasks:
    - name: Include the ios-dhcp-config-env role
      include_role:
        name: ios-dhcp-config-env


License
-------

BSD

Author Information
------------------

Ryan Davis 15/11/22
