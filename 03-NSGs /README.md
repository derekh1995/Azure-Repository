# Project 03 - Network Security Groups

derek [ ~ ]$ az group create \
> --location eastus \
> --name TRG
{
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG",
  "location": "eastus",
  "managedBy": null,
  "name": "TRG",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
derek [ ~ ]$ az network vnet create \
> --resource-group TRG \
> --name VNET1 \
> --address-prefix 10.0.0.0/16
{
  "newVNet": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/16"
      ]
    },
    "enableDdosProtection": false,
    "etag": "W/\"3ec1f1fd-17d9-4a9b-9773-a38288fbbbf9\"",
    "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1",
    "location": "eastus",
    "name": "VNET1",
    "privateEndpointVNetPolicies": "Disabled",
    "provisioningState": "Succeeded",
    "resourceGroup": "TRG",
    "resourceGuid": "a6424fda-1d3d-42a3-8f38-56dc1ffde24b",
    "subnets": [],
    "type": "Microsoft.Network/virtualNetworks",
    "virtualNetworkPeerings": []
  }
}
> derek [ ~ ]$ az network vnet subnet create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --name SUB1 \
> --address-prefix 10.0.1.0/24
{
  "addressPrefix": "10.0.1.0/24",
  "delegations": [],
  "etag": "W/\"d1b40358-431e-45ff-bd6c-a47234e12cdb\"",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1/subnets/SUB1",
  "name": "SUB1",
  "privateEndpointNetworkPolicies": "Disabled",
  "privateLinkServiceNetworkPolicies": "Enabled",
  "provisioningState": "Succeeded",
  "resourceGroup": "TRG",
  "type": "Microsoft.Network/virtualNetworks/subnets"
}
derek [ ~ ]$ az network vnet subnet create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --name SUB2 \
> --address-prefix 10.0.2.0/24
{
  "addressPrefix": "10.0.2.0/24",
  "delegations": [],
  "etag": "W/\"b32fbee8-866d-4a7c-94ed-4972b9216edf\"",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1/subnets/SUB2",
  "name": "SUB2",
  "privateEndpointNetworkPolicies": "Disabled",
  "privateLinkServiceNetworkPolicies": "Enabled",
  "provisioningState": "Succeeded",
  "resourceGroup": "TRG",
  "type": "Microsoft.Network/virtualNetworks/subnets"
}

### I started creating the rule first, but realized I hadn't made the actual NSG yet, so I cancelled and created the NSG.

derek [ ~ ]$ az network nsg rule create \
> --resource-group TRG \
> --nsg-name SUB2NSG \
> --name Allow^C
derek [ ~ ]$ az network nsg create \
> --resource-group TRG \
> --name SUB2NSG
{
  "NewNSG": {
    "defaultSecurityRules": [
      {
        "access": "Allow",
        "description": "Allow inbound traffic from all VMs in VNET",
        "destinationAddressPrefix": "VirtualNetwork",
        "destinationAddressPrefixes": [],
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Inbound",
        "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
        "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/defaultSecurityRules/AllowVnetInBound",
        "name": "AllowVnetInBound",
        "priority": 65000,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "TRG",
        "sourceAddressPrefix": "VirtualNetwork",
        "sourceAddressPrefixes": [],
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Allow",
        "description": "Allow inbound traffic from azure load balancer",
        "destinationAddressPrefix": "*",
        "destinationAddressPrefixes": [],
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Inbound",
        "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
        "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/defaultSecurityRules/AllowAzureLoadBalancerInBound",
        "name": "AllowAzureLoadBalancerInBound",
        "priority": 65001,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "TRG",
        "sourceAddressPrefix": "AzureLoadBalancer",
        "sourceAddressPrefixes": [],
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Deny",
        "description": "Deny all inbound traffic",
        "destinationAddressPrefix": "*",
        "destinationAddressPrefixes": [],
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Inbound",
        "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
        "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/defaultSecurityRules/DenyAllInBound",
        "name": "DenyAllInBound",
        "priority": 65500,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "TRG",
        "sourceAddressPrefix": "*",
        "sourceAddressPrefixes": [],
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Allow",
        "description": "Allow outbound traffic from all VMs to all VMs in VNET",
        "destinationAddressPrefix": "VirtualNetwork",
        "destinationAddressPrefixes": [],
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Outbound",
        "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
        "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/defaultSecurityRules/AllowVnetOutBound",
        "name": "AllowVnetOutBound",
        "priority": 65000,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "TRG",
        "sourceAddressPrefix": "VirtualNetwork",
        "sourceAddressPrefixes": [],
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Allow",
        "description": "Allow outbound traffic from all VMs to Internet",
        "destinationAddressPrefix": "Internet",
        "destinationAddressPrefixes": [],
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Outbound",
        "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
        "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/defaultSecurityRules/AllowInternetOutBound",
        "name": "AllowInternetOutBound",
        "priority": 65001,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "TRG",
        "sourceAddressPrefix": "*",
        "sourceAddressPrefixes": [],
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Deny",
        "description": "Deny all outbound traffic",
        "destinationAddressPrefix": "*",
        "destinationAddressPrefixes": [],
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Outbound",
        "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
        "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/defaultSecurityRules/DenyAllOutBound",
        "name": "DenyAllOutBound",
        "priority": 65500,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "TRG",
        "sourceAddressPrefix": "*",
        "sourceAddressPrefixes": [],
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      }
    ],
    "etag": "W/\"6a8b822d-fccd-4fbd-acef-1d2ea91bfb86\"",
    "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG",
    "location": "eastus",
    "name": "SUB2NSG",
    "provisioningState": "Succeeded",
    "resourceGroup": "TRG",
    "resourceGuid": "9e028327-7bd8-4725-8106-14858eab1923",
    "securityRules": [],
    "type": "Microsoft.Network/networkSecurityGroups"
  }
}

### At this point, I was able to create the rule to allow SSH and then apply it to my "SUB2" subnet.

derek [ ~ ]$ az network nsg rule create \
> --resource-group TRG \
> --nsg-name SUB2NSG \
> --name AllowSSH \
> --priority 100 \
> --direction inbound \
> --access Allow \
> --protocol TCP \
> --destination-port-range 22
{
  "access": "Allow",
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationPortRange": "22",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"6d54fad9-78ed-4147-9c99-f9f2bd3d67d6\"",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/securityRules/AllowSSH",
  "name": "AllowSSH",
  "priority": 100,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "TRG",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
derek [ ~ ]$ az network vnet subnet update \
> --resource-group TRG \
> --vnet-name VNET1 \
> --name SUB2 \
> --network-security-group SUB2NSG
{
  "addressPrefix": "10.0.2.0/24",
  "delegations": [],
  "etag": "W/\"0d353d72-3b03-446c-ad48-49e5118a794a\"",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1/subnets/SUB2",
  "name": "SUB2",
  "networkSecurityGroup": {
    "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG",
    "resourceGroup": "TRG"
  },
  "privateEndpointNetworkPolicies": "Disabled",
  "privateLinkServiceNetworkPolicies": "Enabled",
  "provisioningState": "Succeeded",
  "resourceGroup": "TRG",
  "type": "Microsoft.Network/virtualNetworks/subnets"
}

### With preparations out of the way now, I created the VMs and placed them within the subnets.

derek [ ~ ]$ az vm create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --subnet SUB1 \
> --name VM1 \
> --image Ubuntu2204 \
> --generate-ssh-keys \
> --authentication-type ssh \
> --admin-username derekadmin1 \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
SSH key files '/home/derek/.ssh/id_rsa' and '/home/derek/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Compute/virtualMachines/VM1",
  "location": "eastus",
  "macAddress": "00-0D-3A-17-6F-E6",
  "powerState": "VM running",
  "privateIpAddress": "10.0.1.4",
  "publicIpAddress": "20.127.59.148",
  "resourceGroup": "TRG"
}
derek [ ~ ]$ az vm create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --subnet SUB2 \
> --name VM2 \
> --image Ubuntu2204 \
> --generate-ssh-keys \
> --authentication-type ssh \
> --admin-username derekadmin2 \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Compute/virtualMachines/VM2",
  "location": "eastus",
  "macAddress": "7C-1E-52-1B-1B-C5",
  "powerState": "VM running",
  "privateIpAddress": "10.0.2.4",
  "publicIpAddress": "20.85.228.249",
  "resourceGroup": "TRG"
}

### Now that the VMs were created, I tested the NSG rules.

derek [ ~ ]$ ssh derekadmin1@20.127.59.148
The authenticity of host '20.127.59.148 (20.127.59.148)' can't be established.
ED25519 key fingerprint is SHA256:To6SKIsW6bDYkrMKyIOwOYONgWDl81MMpCOqq6OCSL0.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '20.127.59.148' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 23 20:41:39 UTC 2026

  System load:  0.08              Processes:             115
  Usage of /:   5.7% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ ping 10.0.2.4
PING 10.0.2.4 (10.0.2.4) 56(84) bytes of data.
64 bytes from 10.0.2.4: icmp_seq=1 ttl=64 time=6.79 ms
64 bytes from 10.0.2.4: icmp_seq=2 ttl=64 time=4.48 ms
64 bytes from 10.0.2.4: icmp_seq=3 ttl=64 time=3.20 ms
64 bytes from 10.0.2.4: icmp_seq=4 ttl=64 time=2.18 ms
64 bytes from 10.0.2.4: icmp_seq=5 ttl=64 time=1.29 ms
64 bytes from 10.0.2.4: icmp_seq=6 ttl=64 time=5.65 ms
^C
--- 10.0.2.4 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5008ms
rtt min/avg/max/mdev = 1.289/3.930/6.789/1.914 ms
derekadmin1@VM1:~$ exit
logout
Connection to 20.127.59.148 closed.

### Since my ping went through, I decided to check my SUB2NSG rules. It was exactly how I made it, but I discovered through some research that Azure default NSG rules has AllowVnetInBound (Priority 65000), which lets VMs communicate within the same VNet.

derek [ ~ ]$ az network nsg rule list \
> --resource-group TRG \
> --nsg-name SUB2NSG \
> --output table
Name      ResourceGroup    Priority    SourcePortRanges    SourceAddressPrefixes    SourceASG    Access    Protocol    Direction    DestinationPortRanges    DestinationAddressPrefixes    DestinationASG
--------  ---------------  ----------  ------------------  -----------------------  -----------  --------  ----------  -----------  -----------------------  ----------------------------  ----------------
AllowSSH  TRG              100         *                   *                        None         Allow     Tcp         Inbound      22                       *                             None

### I wanted to block ICMP traffic between VMs on the same VNet, so I made a new rule to do so. I then SSH'd back into VM1 and retried pinging. Since there was 100% packet loss, I knew my new NSG rule worked.

derek [ ~ ]$ az network nsg rule create \
> --resource-group TRG \
> --nsg-name SUB2NSG \
> --name DenyVNetInBound \
> --priority 200 \
> --direction Inbound \
> --access Deny \
> --protocol '*' \
> --source-address-prefix VirtualNetwork \
> --destination-port-range '*'
{
  "access": "Deny",
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationPortRange": "*",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"f336ceec-a630-42bb-b5be-1908b0ba26d6\"",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/networkSecurityGroups/SUB2NSG/securityRules/DenyVNetInBound",
  "name": "DenyVNetInBound",
  "priority": 200,
  "protocol": "*",
  "provisioningState": "Succeeded",
  "resourceGroup": "TRG",
  "sourceAddressPrefix": "VirtualNetwork",
  "sourceAddressPrefixes": [],
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
derek [ ~ ]$ az network nsg rule list \
> --resource-group TRG \
> --nsg-name SUB2NSG \
> --output table
Name             ResourceGroup    Priority    SourcePortRanges    SourceAddressPrefixes    SourceASG    Access    Protocol    Direction    DestinationPortRanges    DestinationAddressPrefixes    DestinationASG
---------------  ---------------  ----------  ------------------  -----------------------  -----------  --------  ----------  -----------  -----------------------  ----------------------------  ----------------
AllowSSH         TRG              100         *                   *                        None         Allow     Tcp         Inbound      22                       *                             None
DenyVNetInBound  TRG              200         *                   VirtualNetwork           None         Deny      *           Inbound      *                        *                             None
derek [ ~ ]$ ssh derekadmin1@20.127.59.148
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 23 20:53:35 UTC 2026

  System load:  0.0               Processes:             115
  Usage of /:   5.9% of 28.89GB   Users logged in:       0
  Memory usage: 4%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Thu Jul 23 20:41:42 2026 from 20.120.96.152
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ ping 10.0.2.4
PING 10.0.2.4 (10.0.2.4) 56(84) bytes of data.
^C
--- 10.0.2.4 ping statistics ---
19 packets transmitted, 0 received, 100% packet loss, time 18458ms

### From here, I tried to SSH into VM2 directly from VM1. It failed, so I had to create new SSH keys and then paste them into the known keys folder after SSHing in from Azure Cloud Shell.

derekadmin1@VM1:~$ ssh derekadmin2@10.0.2.4
The authenticity of host '10.0.2.4 (10.0.2.4)' can't be established.
ED25519 key fingerprint is SHA256:NrgJO/IEtmO0nm+jJ4BSNfu0OvpQr1racYa4ZGSsjQE.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.2.4' (ED25519) to the list of known hosts.
derekadmin2@10.0.2.4: Permission denied (publickey).
derekadmin1@VM1:~$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/derekadmin1/.ssh/id_ed25519): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/derekadmin1/.ssh/id_ed25519
Your public key has been saved in /home/derekadmin1/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:UaNjK2G17ymiIm+u8kyqjhvDZGijNZtuBXA1nQVKBSI derekadmin1@VM1
The key's randomart image is:
+--[ED25519 256]--+
|E ..=+o+o o      |
|...o oo. + .     |
| o  . o *        |
|. .  . o =       |
|.=o.  . S .      |
|*..+.  . . .     |
|+.+.  . . o      |
|+B+  . . .       |
|X@*..            |
+----[SHA256]-----+
derekadmin1@VM1:~$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFUzPVuzafhREFZVlzPIF+4K+WtUM+NJoRhAqjvssjaR derekadmin1@VM1
derekadmin1@VM1:~$ exit
logout
Connection to 20.127.59.148 closed.
derek [ ~ ]$ ssh derekadmin2@20.85.228.249
The authenticity of host '20.85.228.249 (20.85.228.249)' can't be established.
ED25519 key fingerprint is SHA256:NrgJO/IEtmO0nm+jJ4BSNfu0OvpQr1racYa4ZGSsjQE.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '20.85.228.249' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 23 21:04:12 UTC 2026

  System load:  0.08              Processes:             114
  Usage of /:   5.7% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.2.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin2@VM2:~$ nano ~/.ssh/authorized_keys
derekadmin2@VM2:~$ chmod 700 ~/.ssh
derekadmin2@VM2:~$ chmod 600 ~/.ssh/authorized_keys
derekadmin2@VM2:~$ exit
logout
Connection to 20.85.228.249 closed.
derek [ ~ ]$ ssh derekadmin1@20.127.59.148
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 23 21:08:30 UTC 2026

  System load:  0.0               Processes:             119
  Usage of /:   5.9% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Thu Jul 23 20:53:35 2026 from 20.120.96.152
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ ssh derekadmin2@10.0.2.4
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 23 21:08:37 UTC 2026

  System load:  0.0               Processes:             114
  Usage of /:   5.9% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.2.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Thu Jul 23 21:04:16 2026 from 20.120.96.152
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin2@VM2:~$ echo "Success!"
Success!
derekadmin2@VM2:~$ exit
logout
Connection to 10.0.2.4 closed.
derekadmin1@VM1:~$ exit
logout
Connection to 20.127.59.148 closed.
derek [ ~ ]$ az group delete \
> --name TRG \
> --yes

### I then deleted the resource group to conclude the project.

