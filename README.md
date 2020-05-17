Ansible role to bootstrap the Raspberry Pi (network and hostname)
  
# Prerequisites
- To allow ansible to use ssh pass, **sshpass** package must be installed in the manager machine.
- To run the playbook start.yml, you have to provide user and password. Please use **-u** and **--ask-pass** flags for remote user (user -> ubuntu, pass -> the one you chose). Also user **--vault-password-file** flag to decrypt the ansible-vault files.  

Example of usage:  
~~~
ansible-playbook start.yml -u ubuntu --ask-pass --ask-vault-pass
~~~

After start.yml has been run, remove the ubuntu (default) user using the **remove_default_user.yml** playbook.
To run this playbook, use ansible user and the private key associated with the public one installed.  
Also check the hosts file and set the rpi_static_ip group with the static IPs chosen (**ipv4_addr** variable).

# Variables
For each host, you have to set the following variables:  
~~~
ansible_host -> The IP given by the DHCP to the rpi (i.e. 192.168.1.55)
hostname -> The hostname you want the rpi to have (i.e. rpi.local)

ipv4_addr -> Static IP address to set to the rpi (i.e. 192.168.1.2)
ipv4_mask -> Net mask associated with the IP (i.e. /24)

#Dictionary encrypted with ansible vault giving admins user and pass. i.e:
admin_users:
   - user: mysecretuser
     pass: MyImpo$1bl€Pass!
~~~

For the group, you have to set the following variables:
~~~
ipv4_gw -> ip gateway for your local network (i.e. 192.168.1.1)

ipv4_dns1 -> first DNS for your group of rpis (i.e. 8.8.8.8)
ipv4_dns2 -> second DNS for your group of rpis (i.e. 8.8.4.4)

management_user -> user which will be used for the rest of configuration steps on remote rpis (i.e. ansible)
management_ssh_public_key -> public key used along the management_user for the rest of configuration steps on remote rpis (you have to have the private one)
~~~

Enjoy!  
/Miguel

