# Project 02 - Networking (Creating VNet and subnets, verifying ICMP communication between two VMs, practice with file transferring, etc.)

## Provisioning Resources and Setting up the Network

### I created the resource group to begin.

> derek [ ~ ]$ az group create \
> --location eastus \
> --name TRG
> {
>  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG",
>  "location": "eastus",
>  "managedBy": null,
>  "name": "TRG",
>  "properties": {
>    "provisioningState": "Succeeded"
>  },
>  "tags": null,
>  "type": "Microsoft.Resources/resourceGroups"
> }

### I searched for available Standard_D VM sizes preemptively, just to verify that my preferred size was available.

> derek [ ~ ]$ az vm list-skus \
> --location eastus \
> --resource-type virtualMachines \
> --output table \
> | grep Standard_D

### I began creating the VNet and, subsequently, two subnets under that VNet.

> derek [ ~ ]$ az network vnet create \
> --resource-group TRG \
> --name VNET1 \
> --address-prefix 10.0.0.0/16
> {
>   "newVNet": {
>     "addressSpace": {
>       "addressPrefixes": [
>         "10.0.0.0/16"
>       ]
>     },
>     "enableDdosProtection": false,
>     "etag": "W/\"59494e19-d098-41d9-b47c-b18017837a08\"",
>     "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1",
>     "location": "eastus",
>     "name": "VNET1",
>     "privateEndpointVNetPolicies": "Disabled",
>     "provisioningState": "Succeeded",
>     "resourceGroup": "TRG",
>     "resourceGuid": "e8766ba3-f3c4-4ab7-9a50-3cca5ea9a3ab",
>     "subnets": [],
>     "type": "Microsoft.Network/virtualNetworks",
>     "virtualNetworkPeerings": []
>   }
> }

> derek [ ~ ]$ az network vnet subnet create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --name SUB1 \
> --address-prefix 10.0.1.0/24
> {
>   "addressPrefix": "10.0.1.0/24",
>   "delegations": [],
>   "etag": "W/\"4edec6c1-4408-41cd-b9b6-3e7b419901b2\"",
>   "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1/subnets/SUB1",
>   "name": "SUB1",
>   "privateEndpointNetworkPolicies": "Disabled",
>   "privateLinkServiceNetworkPolicies": "Enabled",
>   "provisioningState": "Succeeded",
>   "resourceGroup": "TRG",
>   "type": "Microsoft.Network/virtualNetworks/subnets"
> }

> derek [ ~ ]$ az network vnet subnet create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --name SUB2 \
> --address-prefix 10.0.2.0/24
> {
>   "addressPrefix": "10.0.2.0/24",
>   "delegations": [],
>   "etag": "W/\"ec73ae11-9cc3-453a-9da6-818f5e2f34d2\"",
>   "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1/subnets/SUB2",
>   "name": "SUB2",
>   "privateEndpointNetworkPolicies": "Disabled",
>   "privateLinkServiceNetworkPolicies": "Enabled",
>   "provisioningState": "Succeeded",
>   "resourceGroup": "TRG",
>   "type": "Microsoft.Network/virtualNetworks/subnets"
> }
> 
### After the network was ready, I created two VMs -- one in each subnet. It took me a few tries to use the correct syntax.
> 
> derek [ ~ ]$ az vm create \
> --name VM1 \
> --resource-group TRG \
> --subnet SUB1 \
> --admin-username derekadmin1 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --image Ubuntu2204 \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
>
> incorrect usage: --subnet ID | --subnet NAME --vnet-name NAME
> 
> derek [ ~ ]$ az vm create \
> --name VM1 \
> --resource-group TRG \
> --vnet-name VNET1 \
> --subnet-name SUB1 \
> --admin-username derekadmin1 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --image Ubuntu2204 \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
>
> unrecognized arguments: --subnet-name SUB1
> 
> https://aka.ms/cli_ref
> Read more about the command in reference docs
> 
> derek [ ~ ]$ az vm create \
> --name VM1 \
> --resource-group \
> --vnet-name VNET1 \
> --subnet SUB1 \
> --image Ubuntu2204 \
> --admin-username derekadmin1 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
>
> argument --resource-group/-g: expected one argument
> 
> Examples from command's help:
> az vm create -n MyVm -g MyResourceGroup --public-ip-address-dns-name MyUniqueDnsName --image Ubuntu2204 --data-disk-sizes-gb 10 20 --size Standard_DS2_v2 --generate-ssh-keys
> Create a simple Ubuntu Linux VM with a public IP address, DNS entry, two data disks (10GB and 20GB), and then generate RSA ssh key pairs.
> 
> az vm create -n MyVm -g MyResourceGroup --image Debian11 --vnet-name MyVnet --subnet subnet1 --availability-set MyAvailabilitySet --public-ip-address-dns-name MyUniqueDnsName --ssh-key-values @key-file
> Create a Debian11 VM with SSH key authentication and a public DNS entry, located on an existing virtual network and availability set.
> 
> az vm create -n MyVm -g MyResourceGroup --image Ubuntu2204
> Create a default Ubuntu2204 VM with automatic SSH authentication.
> 
> https://aka.ms/cli_ref
> Read more about the command in reference docs
> 
> derek [ ~ ]$ az vm create \
> --name VM1 \
> --resource-group TRG \
> --vnet-name VNET1 \
> --subnet SUB1 \
> --image Ubuntu2204 \
> --admin-username derekadmin1 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
> 
> SSH key files '/home/derek/.ssh/id_rsa' and '/home/derek/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
> Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
> {
>   "fqdns": "",
>   "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Compute/virtualMachines/VM1",
>   "location": "eastus",
>   "macAddress": "7C-1E-52-66-A5-CF",
>   "powerState": "VM running",
>   "privateIpAddress": "10.0.1.4",
>   "publicIpAddress": "20.51.147.79",
>   "resourceGroup": "TRG"
> }

> derek [ ~ ]$ az vm create \
> --name VM1 \
> --resource-group TRG \
> --vnet-name VNET1 \
> --subnet SUB2 \
> --image Ubuntu2204 \
> --admin-username derekadmin2 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
>
> ERROR: the following arguments are required: --name/-n, --resource-group/-g
> 
> Examples from command's help:
> az vm create -n MyVm -g MyResourceGroup --image Ubuntu2204
> Create a default Ubuntu2204 VM with automatic SSH authentication.
> 
> az vm create -n MyVm -g MyResourceGroup --image RedHat:RHEL:7-RAW:7.4.2018010506
> Create a default RedHat VM with automatic SSH authentication using an image URN.
> 
> az vm create -g MyResourceGroup -n MyVm --image MyImage
> Create a VM from a custom managed image.
> 
> https://aka.ms/cli_ref
> Read more about the command in reference docs
> 
> derek [ ~ ]$ az vm create \
> --name VM2 \
> --resource-group TRG \
> --vnet-name VNET1 \
> --subnet SUB2 \
> --image Ubuntu2204 \
> --admin-username derekadmin2 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
> 
> Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
> {
>   "fqdns": "",
>   "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Compute/virtualMachines/VM2",
>   "location": "eastus",
>   "macAddress": "00-0D-3A-12-03-14",
>   "powerState": "VM running",
>   "privateIpAddress": "10.0.2.4",
>   "publicIpAddress": "20.42.100.157",
>   "resourceGroup": "TRG"
> }

## Validation of Builds

### After I created the VMs, I did some quick verifications to make sure the VMs and their associated accounts were successfully created. I did this by listing the VMs and then having the VMs run id commands as root to check their status.

> derek [ ~ ]$ az vm list \
> --output table
> 
> Name    ResourceGroup    Location
> ------  ---------------  ----------
> VM1     TRG              eastus
> VM2     TRG              eastus
> 
> derek [ ~ ]$ az vm run-command invoke \
> --resource-group TRG \
> --name VM1 \
> --command-id RunShellScript \
> --scripts "id derekadmin1"
>
> {
>   "value": [
>     {
>       "code": "ProvisioningState/succeeded",
>       "displayStatus": "Provisioning succeeded",
>       "level": "Info",
>       "message": "Enable succeeded: \n[stdout]\nuid=1000(derekadmin1) gid=1000(derekadmin1) groups=1000(derekadmin1),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),118(netdev),119(lxd)\n\n[stderr]\n"
>     }
>   ]
> }
> 
> derek [ ~ ]$ az vm run-command invoke \
> --resource-group TRG \
> --name VM2 \
> --command-id RunShellScript \
> --scripts "id derekadmin2"
>
> {
>   "value": [
>     {
>       "code": "ProvisioningState/succeeded",
>       "displayStatus": "Provisioning succeeded",
>       "level": "Info",
>       "message": "Enable succeeded: \n[stdout]\nuid=1000(derekadmin2) gid=1000(derekadmin2) groups=1000(derekadmin2),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),118(netdev),119(lxd)\n\n[stderr]\n"
>     }
>   ]
> }

## SSHing into Machines and Pinging

### After verifying the VMs and accounts were good, I ran a verbose SSH into derekadmin1. The SSH was successful, but using -v was unnecessary and just flooded my terminal with information I didn't need. Upon entering VM1, I began to ping VM2 via its private IP. After communicating with VM2, I exited the VM.

> derek [ ~ ]$ ssh -v derekadmin1@20.51.147.79

> derekadmin1@VM1:~$ ping 10.0.2.4
>
> PING 10.0.2.4 (10.0.2.4) 56(84) bytes of data.
> 64 bytes from 10.0.2.4: icmp_seq=1 ttl=64 time=1.26 ms
> 64 bytes from 10.0.2.4: icmp_seq=2 ttl=64 time=2.16 ms
> 64 bytes from 10.0.2.4: icmp_seq=3 ttl=64 time=5.02 ms
> 64 bytes from 10.0.2.4: icmp_seq=4 ttl=64 time=3.65 ms
> 64 bytes from 10.0.2.4: icmp_seq=5 ttl=64 time=1.37 ms
> 64 bytes from 10.0.2.4: icmp_seq=6 ttl=64 time=1.39 ms
> 64 bytes from 10.0.2.4: icmp_seq=7 ttl=64 time=4.93 ms
> 64 bytes from 10.0.2.4: icmp_seq=8 ttl=64 time=6.28 ms
> 64 bytes from 10.0.2.4: icmp_seq=9 ttl=64 time=17.1 ms
> 64 bytes from 10.0.2.4: icmp_seq=10 ttl=64 time=15.7 ms
> 64 bytes from 10.0.2.4: icmp_seq=11 ttl=64 time=1.88 ms
> 64 bytes from 10.0.2.4: icmp_seq=12 ttl=64 time=1.31 ms
> 64 bytes from 10.0.2.4: icmp_seq=13 ttl=64 time=1.66 ms
> 64 bytes from 10.0.2.4: icmp_seq=14 ttl=64 time=0.767 ms
> 64 bytes from 10.0.2.4: icmp_seq=15 ttl=64 time=2.28 ms
> 64 bytes from 10.0.2.4: icmp_seq=16 ttl=64 time=1.07 ms
> 64 bytes from 10.0.2.4: icmp_seq=17 ttl=64 time=1.59 ms
> 64 bytes from 10.0.2.4: icmp_seq=18 ttl=64 time=2.13 ms
> 64 bytes from 10.0.2.4: icmp_seq=19 ttl=64 time=0.894 ms
> 64 bytes from 10.0.2.4: icmp_seq=20 ttl=64 time=2.67 ms
> 64 bytes from 10.0.2.4: icmp_seq=21 ttl=64 time=5.67 ms
> 64 bytes from 10.0.2.4: icmp_seq=22 ttl=64 time=1.10 ms
> 64 bytes from 10.0.2.4: icmp_seq=23 ttl=64 time=12.5 ms
> 64 bytes from 10.0.2.4: icmp_seq=24 ttl=64 time=4.08 ms
> 64 bytes from 10.0.2.4: icmp_seq=25 ttl=64 time=0.811 ms
> 64 bytes from 10.0.2.4: icmp_seq=26 ttl=64 time=3.53 ms
> 64 bytes from 10.0.2.4: icmp_seq=27 ttl=64 time=1.44 ms
> 64 bytes from 10.0.2.4: icmp_seq=28 ttl=64 time=0.797 ms
> 64 bytes from 10.0.2.4: icmp_seq=29 ttl=64 time=0.743 ms
> 64 bytes from 10.0.2.4: icmp_seq=30 ttl=64 time=1.79 ms
> 64 bytes from 10.0.2.4: icmp_seq=31 ttl=64 time=1.24 ms
> 64 bytes from 10.0.2.4: icmp_seq=32 ttl=64 time=3.81 ms
> 64 bytes from 10.0.2.4: icmp_seq=33 ttl=64 time=6.66 ms
> 64 bytes from 10.0.2.4: icmp_seq=34 ttl=64 time=5.60 ms
> 64 bytes from 10.0.2.4: icmp_seq=35 ttl=64 time=2.37 ms
> 64 bytes from 10.0.2.4: icmp_seq=36 ttl=64 time=0.752 ms
> 64 bytes from 10.0.2.4: icmp_seq=37 ttl=64 time=3.38 ms
> 64 bytes from 10.0.2.4: icmp_seq=38 ttl=64 time=9.14 ms
> 64 bytes from 10.0.2.4: icmp_seq=39 ttl=64 time=0.836 ms
> 64 bytes from 10.0.2.4: icmp_seq=40 ttl=64 time=1.60 ms
> 64 bytes from 10.0.2.4: icmp_seq=41 ttl=64 time=10.4 ms
> 64 bytes from 10.0.2.4: icmp_seq=42 ttl=64 time=6.38 ms
> 64 bytes from 10.0.2.4: icmp_seq=43 ttl=64 time=1.53 ms
> ^C
> --- 10.0.2.4 ping statistics ---
> 43 packets transmitted, 43 received, 0% packet loss, time 42208ms
> rtt min/avg/max/mdev = 0.743/3.748/17.061/3.881 ms
> 
> derekadmin1@VM1:~$ exit
>
> logout
> debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
> debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0
> debug1: channel 0: free: client-session, nchannels 1
> Connection to 20.51.147.79 closed.
> Transferred: sent 5248, received 10808 bytes, in 249.1 seconds
> Bytes per second: sent 21.1, received 43.4
> debug1: Exit status 127

### After exiting VM1, I SSH'd into VM2 to verify that I could ping VM1. Upon verification, I exited VM2.

> derek [ ~ ]$ ssh derekadmin2@20.42.100.157
> 
> 
> derekadmin2@VM2:~$ ping 10.0.1.4
>
> PING 10.0.1.4 (10.0.1.4) 56(84) bytes of data.
> 64 bytes from 10.0.1.4: icmp_seq=1 ttl=64 time=14.9 ms
> 64 bytes from 10.0.1.4: icmp_seq=2 ttl=64 time=0.856 ms
> 64 bytes from 10.0.1.4: icmp_seq=3 ttl=64 time=8.68 ms
> 64 bytes from 10.0.1.4: icmp_seq=4 ttl=64 time=5.34 ms
> 64 bytes from 10.0.1.4: icmp_seq=5 ttl=64 time=8.03 ms
> 64 bytes from 10.0.1.4: icmp_seq=6 ttl=64 time=8.68 ms
> 64 bytes from 10.0.1.4: icmp_seq=7 ttl=64 time=4.45 ms
> 64 bytes from 10.0.1.4: icmp_seq=8 ttl=64 time=8.65 ms
> 64 bytes from 10.0.1.4: icmp_seq=9 ttl=64 time=2.35 ms
> 64 bytes from 10.0.1.4: icmp_seq=10 ttl=64 time=1.49 ms
> ^C
> --- 10.0.1.4 ping statistics ---
> 10 packets transmitted, 10 received, 0% packet loss, time 9040ms
> rtt min/avg/max/mdev = 0.856/6.338/14.851/4.069 ms
>
> derekadmin2@VM2:~$ exit
>
> logout
> Connection to 20.42.100.157 closed.

## Network Verification

### I SSH'd into both VMs again to verify the network.

> derek [ ~ ]$ ssh derekadmin1@20.51.147.79
> 
> derekadmin1@VM1:~$ ip route
>
> default via 10.0.1.1 dev eth0 proto dhcp src 10.0.1.4 metric 100 
> 10.0.1.0/24 dev eth0 proto kernel scope link src 10.0.1.4 metric 100 
> 10.0.1.1 dev eth0 proto dhcp scope link src 10.0.1.4 metric 100 
> 168.63.129.16 via 10.0.1.1 dev eth0 proto dhcp src 10.0.1.4 metric 100 
> 169.254.169.254 via 10.0.1.1 dev eth0 proto dhcp src 10.0.1.4 metric 100 
>
> derekadmin1@VM1:~$ ip addr
>
> 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
>     link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
>     inet 127.0.0.1/8 scope host lo
>        valid_lft forever preferred_lft forever
>     inet6 ::1/128 scope host 
>        valid_lft forever preferred_lft forever
> 2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
>     link/ether 7c:1e:52:66:a5:cf brd ff:ff:ff:ff:ff:ff
>     inet 10.0.1.4/24 metric 100 brd 10.0.1.255 scope global eth0
>        valid_lft forever preferred_lft forever
>     inet6 fe80::7e1e:52ff:fe66:a5cf/64 scope link 
>        valid_lft forever preferred_lft forever
> 3: enP30832s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
>     link/ether 7c:1e:52:66:a5:cf brd ff:ff:ff:ff:ff:ff
>     altname enp0s0
> 
> derekadmin1@VM1:~$ exit
>
> logout
> Connection to 20.51.147.79 closed.
>
> derek [ ~ ]$ ssh derekadmin2@20.42.100.157
>
> derekadmin2@VM2:~$ ip route
>
> default via 10.0.2.1 dev eth0 proto dhcp src 10.0.2.4 metric 100
> 10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.4 metric 100
> 10.0.2.1 dev eth0 proto dhcp scope link src 10.0.2.4 metric 100
> 168.63.129.16 via 10.0.2.1 dev eth0 proto dhcp src 10.0.2.4 metric 100
> 169.254.169.254 via 10.0.2.1 dev eth0 proto dhcp src 10.0.2.4 metric 100
>
> derekadmin2@VM2:~$ ip addr
> 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
>     link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
>     inet 127.0.0.1/8 scope host lo
>        valid_lft forever preferred_lft forever
>     inet6 ::1/128 scope host 
>        valid_lft forever preferred_lft forever
> 2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
>     link/ether 00:0d:3a:12:03:14 brd ff:ff:ff:ff:ff:ff
>     inet 10.0.2.4/24 metric 100 brd 10.0.2.255 scope global eth0
>        valid_lft forever preferred_lft forever
>     inet6 fe80::20d:3aff:fe12:314/64 scope link 
>        valid_lft forever preferred_lft forever
> 3: enP30832s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
>     link/ether 00:0d:3a:12:03:14 brd ff:ff:ff:ff:ff:ff
>     altname enp0s0
>
> derekadmin2@VM2:~$ exit
>
> logout
> Connection to 20.42.100.157 closed.

## SCP File Transfers

### I tried to transfer a file from VM1 to VM2, but the two VMs don't have each other's keys, and it was getting late, so I decided to save file transferring between VMs for a later project.

> derek [ ~ ]$ ssh derekadmin1@20.51.147.79
> 
> derekadmin1@VM1:~$ nano hello.txt
>
> derekadmin1@VM1:~$ cat hello.txt
> Hello from VM1!
>
> derekadmin1@VM1:~$ scp hello.txt derekadmin2@10.0.2.4:/home/derekadmin2
>
> The authenticity of host '10.0.2.4 (10.0.2.4)' can't be established.
> ED25519 key fingerprint is SHA256:76Tg3qg/ue+rRfsKC3oPDFYIHk8iRuiL3Mu106soH8k.
> This key is not known by any other names
> Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
> Warning: Permanently added '10.0.2.4' (ED25519) to the list of known hosts.
> derekadmin2@10.0.2.4: Permission denied (publickey).
> lost connection
>
> derekadmin1@VM1:~$ exit
>
> logout
> Connection to 20.51.147.79 closed.

### I still wanted to get some experience with testing file transfers, so I used SCP to transfer files to both VMs from Azure CLI and then SSH'd into the VMs to verify the files were successfully transferred.

> derek [ ~ ]$ nano test.txt
>
> derek [ ~ ]$ cat test.txt
>
> Testing... Testing... 1, 2, 3.
>
> derek [ ~ ]$ scp test.txt derekadmin1@20.51.147.79:/home/derekadmin1
>
> test.txt                                                                                                                                                                                                                                                                    >                100%   31    10.1KB/s   00:00    
>
> derek [ ~ ]$ scp test.txt derekadmin2@20.42.100.157:/home/derekadmin2
>
> test.txt                                                                                                                                                                                                                                                                    >                100%   31     9.5KB/s   00:00    
>
> derek [ ~ ]$ ssh derekadmin1@20.51.147.79
>
> derekadmin1@VM1:~$ cat test.txt
>
> Testing... Testing... 1, 2, 3.
>
> derekadmin1@VM1:~$ exit
>
> logout
> Connection to 20.51.147.79 closed.
>
> derek [ ~ ]$ ssh derekadmin2@20.42.100.157
>
> derekadmin2@VM2:~$ cat test.txt
>
> Testing... Testing... 1, 2, 3.
>
> derekadmin2@VM2:~$ exit
>
> logout
> Connection to 20.42.100.157 closed.

## Clean-up

### After verifying the files were transferred, I concluded my project, deleted the resource group, and verified it was deleted.

> derek [ ~ ]$ az group delete \
> --name TRG \
> --yes
>
> derek [ ~ ]$ az group exists \
> --name TRG
> 
> false
