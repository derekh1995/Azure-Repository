# Project 02 - Networking

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
derek [ ~ ]$ az vm list-skus \
> --location eastus \
> --resource-type virtualMachines \
> --output table \
> | grep Standard_D
virtualMachines  eastus       Standard_D128ads_v7       1,3      None
virtualMachines  eastus       Standard_D128alds_v7      1,3      None
virtualMachines  eastus       Standard_D128als_v7       1,3      None
virtualMachines  eastus       Standard_D128as_v7        1,3      None
virtualMachines  eastus       Standard_D128ds_v7        1,2,3    None
virtualMachines  eastus       Standard_D128lds_v7       1,2,3    None
virtualMachines  eastus       Standard_D128ls_v7        1,2,3    None
virtualMachines  eastus       Standard_D128s_v7         1,2,3    None
virtualMachines  eastus       Standard_D160ads_v7       1,3      None
virtualMachines  eastus       Standard_D160alds_v7      1,3      None
virtualMachines  eastus       Standard_D160als_v7       1,3      None
virtualMachines  eastus       Standard_D160as_v7        1,3      None
virtualMachines  eastus       Standard_D16ads_v7        1,3      None
virtualMachines  eastus       Standard_D16alds_v7       1,3      None
virtualMachines  eastus       Standard_D16als_v7        1,3      None
virtualMachines  eastus       Standard_D16as_v7         1,3      None
virtualMachines  eastus       Standard_D16ds_v7         1,2,3    None
virtualMachines  eastus       Standard_D16lds_v7        1,2,3    None
virtualMachines  eastus       Standard_D16ls_v7         1,2,3    None
virtualMachines  eastus       Standard_D16s_v7          1,2,3    None
virtualMachines  eastus       Standard_D192ds_v7        1,2,3    None
virtualMachines  eastus       Standard_D192lds_v7       1,2,3    None
virtualMachines  eastus       Standard_D192ls_v7        1,2,3    None
virtualMachines  eastus       Standard_D192s_v7         1,2,3    None
virtualMachines  eastus       Standard_D2ads_v7         1,3      None
virtualMachines  eastus       Standard_D2alds_v7        1,3      None
virtualMachines  eastus       Standard_D2als_v7         1,3      None
virtualMachines  eastus       Standard_D2as_v7          1,3      None
virtualMachines  eastus       Standard_D2ds_v7          1,2,3    None
virtualMachines  eastus       Standard_D2lds_v7         1,2,3    None
virtualMachines  eastus       Standard_D2ls_v7          1,2,3    None
virtualMachines  eastus       Standard_D2s_v7           1,2,3    None
virtualMachines  eastus       Standard_D32ads_v7        1,3      None
virtualMachines  eastus       Standard_D32alds_v7       1,3      None
virtualMachines  eastus       Standard_D32als_v7        1,3      None
virtualMachines  eastus       Standard_D32as_v7         1,3      None
virtualMachines  eastus       Standard_D32ds_v7         1,2,3    None
virtualMachines  eastus       Standard_D32lds_v7        1,2,3    None
virtualMachines  eastus       Standard_D32ls_v7         1,2,3    None
virtualMachines  eastus       Standard_D32s_v7          1,2,3    None
virtualMachines  eastus       Standard_D48ads_v7        1,3      None
virtualMachines  eastus       Standard_D48alds_v7       1,3      None
virtualMachines  eastus       Standard_D48als_v7        1,3      None
virtualMachines  eastus       Standard_D48as_v7         1,3      None
virtualMachines  eastus       Standard_D48ds_v7         1,2,3    None
virtualMachines  eastus       Standard_D48lds_v7        1,2,3    None
virtualMachines  eastus       Standard_D48ls_v7         1,2,3    None
virtualMachines  eastus       Standard_D48s_v7          1,2,3    None
virtualMachines  eastus       Standard_D4ads_v7         1,3      None
virtualMachines  eastus       Standard_D4alds_v7        1,3      None
virtualMachines  eastus       Standard_D4als_v7         1,3      None
virtualMachines  eastus       Standard_D4as_v7          1,3      None
virtualMachines  eastus       Standard_D4ds_v7          1,2,3    None
virtualMachines  eastus       Standard_D4lds_v7         1,2,3    None
virtualMachines  eastus       Standard_D4ls_v7          1,2,3    None
virtualMachines  eastus       Standard_D4s_v7           1,2,3    None
virtualMachines  eastus       Standard_D64ads_v7        1,3      None
virtualMachines  eastus       Standard_D64alds_v7       1,3      None
virtualMachines  eastus       Standard_D64als_v7        1,3      None
virtualMachines  eastus       Standard_D64as_v7         1,3      None
virtualMachines  eastus       Standard_D64ds_v7         1,2,3    None
virtualMachines  eastus       Standard_D64lds_v7        1,2,3    None
virtualMachines  eastus       Standard_D64ls_v7         1,2,3    None
virtualMachines  eastus       Standard_D64s_v7          1,2,3    None
virtualMachines  eastus       Standard_D8ads_v7         1,3      None
virtualMachines  eastus       Standard_D8alds_v7        1,3      None
virtualMachines  eastus       Standard_D8als_v7         1,3      None
virtualMachines  eastus       Standard_D8as_v7          1,3      None
virtualMachines  eastus       Standard_D8ds_v7          1,2,3    None
virtualMachines  eastus       Standard_D8lds_v7         1,2,3    None
virtualMachines  eastus       Standard_D8ls_v7          1,2,3    None
virtualMachines  eastus       Standard_D8s_v7           1,2,3    None
virtualMachines  eastus       Standard_D96ads_v7        1,3      None
virtualMachines  eastus       Standard_D96alds_v7       1,3      None
virtualMachines  eastus       Standard_D96als_v7        1,3      None
virtualMachines  eastus       Standard_D96as_v7         1,3      None
virtualMachines  eastus       Standard_D96ds_v7         1,2,3    None
virtualMachines  eastus       Standard_D96lds_v7        1,2,3    None
virtualMachines  eastus       Standard_D96ls_v7         1,2,3    None
virtualMachines  eastus       Standard_D96s_v7          1,2,3    None
virtualMachines  eastus       Standard_DC16ads_cc_v5    1,2      None
virtualMachines  eastus       Standard_DC16ads_v5       1,2      None
virtualMachines  eastus       Standard_DC16ads_v6       1,2,3    None
virtualMachines  eastus       Standard_DC16as_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC16as_v5        1,2      None
virtualMachines  eastus       Standard_DC16as_v6        1,2,3    None
virtualMachines  eastus       Standard_DC16ds_v3        1        None
virtualMachines  eastus       Standard_DC16s_v3         1        None
virtualMachines  eastus       Standard_DC1ds_v3         1        None
virtualMachines  eastus       Standard_DC1s_v3          1        None
virtualMachines  eastus       Standard_DC24ds_v3        1        None
virtualMachines  eastus       Standard_DC24s_v3         1        None
virtualMachines  eastus       Standard_DC2ads_v5        1,2      None
virtualMachines  eastus       Standard_DC2ads_v6        1,2,3    None
virtualMachines  eastus       Standard_DC2as_v5         1,2      None
virtualMachines  eastus       Standard_DC2as_v6         1,2,3    None
virtualMachines  eastus       Standard_DC2ds_v3         1        None
virtualMachines  eastus       Standard_DC2s_v3          1        None
virtualMachines  eastus       Standard_DC32ads_cc_v5    1,2      None
virtualMachines  eastus       Standard_DC32ads_v5       1,2      None
virtualMachines  eastus       Standard_DC32ads_v6       1,2,3    None
virtualMachines  eastus       Standard_DC32as_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC32as_v5        1,2      None
virtualMachines  eastus       Standard_DC32as_v6        1,2,3    None
virtualMachines  eastus       Standard_DC32ds_v3        1        None
virtualMachines  eastus       Standard_DC32s_v3         1        None
virtualMachines  eastus       Standard_DC48ads_cc_v5    1,2      None
virtualMachines  eastus       Standard_DC48ads_v5       1,2      None
virtualMachines  eastus       Standard_DC48ads_v6       1,2,3    None
virtualMachines  eastus       Standard_DC48as_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC48as_v5        1,2      None
virtualMachines  eastus       Standard_DC48as_v6        1,2,3    None
virtualMachines  eastus       Standard_DC48ds_v3        1        None
virtualMachines  eastus       Standard_DC48s_v3         1        None
virtualMachines  eastus       Standard_DC4ads_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC4ads_v5        1,2      None
virtualMachines  eastus       Standard_DC4ads_v6        1,2,3    None
virtualMachines  eastus       Standard_DC4as_cc_v5      1,2      None
virtualMachines  eastus       Standard_DC4as_v5         1,2      None
virtualMachines  eastus       Standard_DC4as_v6         1,2,3    None
virtualMachines  eastus       Standard_DC4ds_v3         1        None
virtualMachines  eastus       Standard_DC4s_v3          1        None
virtualMachines  eastus       Standard_DC64ads_cc_v5    1,2      None
virtualMachines  eastus       Standard_DC64ads_v5       1,2      None
virtualMachines  eastus       Standard_DC64ads_v6       1,2,3    None
virtualMachines  eastus       Standard_DC64as_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC64as_v5        1,2      None
virtualMachines  eastus       Standard_DC64as_v6        1,2,3    None
virtualMachines  eastus       Standard_DC8ads_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC8ads_v5        1,2      None
virtualMachines  eastus       Standard_DC8ads_v6        1,2,3    None
virtualMachines  eastus       Standard_DC8as_cc_v5      1,2      None
virtualMachines  eastus       Standard_DC8as_v5         1,2      None
virtualMachines  eastus       Standard_DC8as_v6         1,2,3    None
virtualMachines  eastus       Standard_DC8ds_v3         1        None
virtualMachines  eastus       Standard_DC8s_v3          1        None
virtualMachines  eastus       Standard_DC96ads_cc_v5    1,2      None
virtualMachines  eastus       Standard_DC96ads_v5       1,2      None
virtualMachines  eastus       Standard_DC96ads_v6       1,2,3    None
virtualMachines  eastus       Standard_DC96as_cc_v5     1,2      None
virtualMachines  eastus       Standard_DC96as_v5        1,2      None
virtualMachines  eastus       Standard_DC96as_v6        1,2,3    None
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
    "etag": "W/\"59494e19-d098-41d9-b47c-b18017837a08\"",
    "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1",
    "location": "eastus",
    "name": "VNET1",
    "privateEndpointVNetPolicies": "Disabled",
    "provisioningState": "Succeeded",
    "resourceGroup": "TRG",
    "resourceGuid": "e8766ba3-f3c4-4ab7-9a50-3cca5ea9a3ab",
    "subnets": [],
    "type": "Microsoft.Network/virtualNetworks",
    "virtualNetworkPeerings": []
  }
}
derek [ ~ ]$ az network vnet subnet create \
> --resource-group TRG \
> --vnet-name VNET1 \
> --name SUB1 \
> --address-prefix 10.0.1.0/24
{
  "addressPrefix": "10.0.1.0/24",
  "delegations": [],
  "etag": "W/\"4edec6c1-4408-41cd-b9b6-3e7b419901b2\"",
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
  "etag": "W/\"ec73ae11-9cc3-453a-9da6-818f5e2f34d2\"",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Network/virtualNetworks/VNET1/subnets/SUB2",
  "name": "SUB2",
  "privateEndpointNetworkPolicies": "Disabled",
  "privateLinkServiceNetworkPolicies": "Enabled",
  "provisioningState": "Succeeded",
  "resourceGroup": "TRG",
  "type": "Microsoft.Network/virtualNetworks/subnets"
}
derek [ ~ ]$ az vm create \
> --name VM1 \
> --resource-group TRG \
> --subnet SUB1 \
> --admin-username derekadmin1 \
> --authentication-type ssh \
> --generate-ssh-keys \
> --image Ubuntu2204 \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
incorrect usage: --subnet ID | --subnet NAME --vnet-name NAME
derek [ ~ ]$ az vm create \
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
unrecognized arguments: --subnet-name SUB1

https://aka.ms/cli_ref
Read more about the command in reference docs
derek [ ~ ]$ az vm create \
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
argument --resource-group/-g: expected one argument

Examples from command's help:
az vm create -n MyVm -g MyResourceGroup --public-ip-address-dns-name MyUniqueDnsName --image Ubuntu2204 --data-disk-sizes-gb 10 20 --size Standard_DS2_v2 --generate-ssh-keys
Create a simple Ubuntu Linux VM with a public IP address, DNS entry, two data disks (10GB and 20GB), and then generate RSA ssh key pairs.

az vm create -n MyVm -g MyResourceGroup --image Debian11 --vnet-name MyVnet --subnet subnet1 --availability-set MyAvailabilitySet --public-ip-address-dns-name MyUniqueDnsName --ssh-key-values @key-file
Create a Debian11 VM with SSH key authentication and a public DNS entry, located on an existing virtual network and availability set.

az vm create -n MyVm -g MyResourceGroup --image Ubuntu2204
Create a default Ubuntu2204 VM with automatic SSH authentication.

https://aka.ms/cli_ref
Read more about the command in reference docs
derek [ ~ ]$ az vm create \
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
SSH key files '/home/derek/.ssh/id_rsa' and '/home/derek/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Compute/virtualMachines/VM1",
  "location": "eastus",
  "macAddress": "7C-1E-52-66-A5-CF",
  "powerState": "VM running",
  "privateIpAddress": "10.0.1.4",
  "publicIpAddress": "20.51.147.79",
  "resourceGroup": "TRG"
}
derek [ ~ ]$ az vm create \
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
ERROR: the following arguments are required: --name/-n, --resource-group/-g

Examples from command's help:
az vm create -n MyVm -g MyResourceGroup --image Ubuntu2204
Create a default Ubuntu2204 VM with automatic SSH authentication.

az vm create -n MyVm -g MyResourceGroup --image RedHat:RHEL:7-RAW:7.4.2018010506
Create a default RedHat VM with automatic SSH authentication using an image URN.

az vm create -g MyResourceGroup -n MyVm --image MyImage
Create a VM from a custom managed image.

https://aka.ms/cli_ref
Read more about the command in reference docs
derek [ ~ ]$ az vm create \
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
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG/providers/Microsoft.Compute/virtualMachines/VM2",
  "location": "eastus",
  "macAddress": "00-0D-3A-12-03-14",
  "powerState": "VM running",
  "privateIpAddress": "10.0.2.4",
  "publicIpAddress": "20.42.100.157",
  "resourceGroup": "TRG"
}
derek [ ~ ]$ az vm list \
> --output table
Name    ResourceGroup    Location
------  ---------------  ----------
VM1     TRG              eastus
VM2     TRG              eastus
derek [ ~ ]$ az vm run-command invoke \
> --resource-group TRG \
> --name VM1 \
> --command-id RunShellScript \
> --scripts "id derekadmin1"
{
  "value": [
    {
      "code": "ProvisioningState/succeeded",
      "displayStatus": "Provisioning succeeded",
      "level": "Info",
      "message": "Enable succeeded: \n[stdout]\nuid=1000(derekadmin1) gid=1000(derekadmin1) groups=1000(derekadmin1),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),118(netdev),119(lxd)\n\n[stderr]\n"
    }
  ]
}
derek [ ~ ]$ az vm run-command invoke \
> --resource-group TRG \
> --name VM2 \
> --command-id RunShellScript \
> --scripts "id derekadmin2"
{
  "value": [
    {
      "code": "ProvisioningState/succeeded",
      "displayStatus": "Provisioning succeeded",
      "level": "Info",
      "message": "Enable succeeded: \n[stdout]\nuid=1000(derekadmin2) gid=1000(derekadmin2) groups=1000(derekadmin2),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),118(netdev),119(lxd)\n\n[stderr]\n"
    }
  ]
}
derek [ ~ ]$ ssh -v derekadmin1@20.51.147.79
OpenSSH_9.8p1, OpenSSL 3.3.5 30 Sep 2025
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Authenticator provider $SSH_SK_PROVIDER did not resolve; disabling
debug1: Connecting to 20.51.147.79 [20.51.147.79] port 22.
debug1: Connection established.
debug1: identity file /home/derek/.ssh/id_rsa type 0
debug1: identity file /home/derek/.ssh/id_rsa-cert type -1
debug1: identity file /home/derek/.ssh/id_ecdsa type -1
debug1: identity file /home/derek/.ssh/id_ecdsa-cert type -1
debug1: identity file /home/derek/.ssh/id_ecdsa_sk type -1
debug1: identity file /home/derek/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /home/derek/.ssh/id_ed25519 type -1
debug1: identity file /home/derek/.ssh/id_ed25519-cert type -1
debug1: identity file /home/derek/.ssh/id_ed25519_sk type -1
debug1: identity file /home/derek/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /home/derek/.ssh/id_xmss type -1
debug1: identity file /home/derek/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_9.8
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.9p1 Ubuntu-3ubuntu0.16
debug1: compat_banner: match: OpenSSH_8.9p1 Ubuntu-3ubuntu0.16 pat OpenSSH* compat 0x04000000
debug1: Authenticating to 20.51.147.79:22 as 'derekadmin1'
debug1: load_hostkeys: fopen /home/derek/.ssh/known_hosts: No such file or directory
debug1: load_hostkeys: fopen /home/derek/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: sntrup761x25519-sha512@openssh.com
debug1: kex: host key algorithm: ssh-ed25519
debug1: kex: server->client cipher: aes256-ctr MAC: hmac-sha2-512 compression: none
debug1: kex: client->server cipher: aes256-ctr MAC: hmac-sha2-512 compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: SSH2_MSG_KEX_ECDH_REPLY received
debug1: Server host key: ssh-ed25519 SHA256:svmQGJGkeL13WQGHaMBgjYRpkWHYZMkGcDJHUz0CkyI
debug1: load_hostkeys: fopen /home/derek/.ssh/known_hosts: No such file or directory
debug1: load_hostkeys: fopen /home/derek/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: hostkeys_find_by_key_hostfile: hostkeys file /home/derek/.ssh/known_hosts does not exist
debug1: hostkeys_find_by_key_hostfile: hostkeys file /home/derek/.ssh/known_hosts2 does not exist
debug1: hostkeys_find_by_key_hostfile: hostkeys file /etc/ssh/ssh_known_hosts does not exist
debug1: hostkeys_find_by_key_hostfile: hostkeys file /etc/ssh/ssh_known_hosts2 does not exist
The authenticity of host '20.51.147.79 (20.51.147.79)' can't be established.
ED25519 key fingerprint is SHA256:svmQGJGkeL13WQGHaMBgjYRpkWHYZMkGcDJHUz0CkyI.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '20.51.147.79' (ED25519) to the list of known hosts.
debug1: ssh_packet_send2_wrapped: resetting send seqnr 3
debug1: rekey out after 4294967296 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: ssh_packet_read_poll2: resetting read seqnr 3
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey in after 4294967296 blocks
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_ext_info_client_parse: server-sig-algs=<ssh-ed25519,sk-ssh-ed25519@openssh.com,ssh-rsa,rsa-sha2-256,rsa-sha2-512,ssh-dss,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com,webauthn-sk-ecdsa-sha2-nistp256@openssh.com>
debug1: kex_ext_info_check_ver: publickey-hostbound@openssh.com=<0>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey
debug1: Next authentication method: publickey
debug1: Will attempt key: /home/derek/.ssh/id_rsa RSA SHA256:Foi1wVrKyEA2nfdxrgX0eCZLzki0fmof+zyYbXGOBG4
debug1: Will attempt key: /home/derek/.ssh/id_ecdsa 
debug1: Will attempt key: /home/derek/.ssh/id_ecdsa_sk 
debug1: Will attempt key: /home/derek/.ssh/id_ed25519 
debug1: Will attempt key: /home/derek/.ssh/id_ed25519_sk 
debug1: Will attempt key: /home/derek/.ssh/id_xmss 
debug1: Offering public key: /home/derek/.ssh/id_rsa RSA SHA256:Foi1wVrKyEA2nfdxrgX0eCZLzki0fmof+zyYbXGOBG4
debug1: Server accepts key: /home/derek/.ssh/id_rsa RSA SHA256:Foi1wVrKyEA2nfdxrgX0eCZLzki0fmof+zyYbXGOBG4
Authenticated to 20.51.147.79 ([20.51.147.79]:22) using "publickey".
debug1: channel 0: new session [client-session] (inactive timeout: 0)
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: filesystem
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: client_input_hostkeys: searching /home/derek/.ssh/known_hosts for 20.51.147.79 / (none)
debug1: client_input_hostkeys: searching /home/derek/.ssh/known_hosts2 for 20.51.147.79 / (none)
debug1: client_input_hostkeys: hostkeys file /home/derek/.ssh/known_hosts2 does not exist
debug1: Remote: /home/derekadmin1/.ssh/authorized_keys:1: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug1: Remote: /home/derekadmin1/.ssh/authorized_keys:1: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
Learned new hostkey: RSA SHA256:nwze+Qy26k1e+tUXUZkk5kHBXEAZRHiIZNd3NMKw0Yk
Learned new hostkey: ECDSA SHA256:z3ncPINSdcNwD/PSodGdoeXxFwVTv69emPxn9f+zUw4
Adding new key for 20.51.147.79 to /home/derek/.ssh/known_hosts: ssh-rsa SHA256:nwze+Qy26k1e+tUXUZkk5kHBXEAZRHiIZNd3NMKw0Yk
Adding new key for 20.51.147.79 to /home/derek/.ssh/known_hosts: ecdsa-sha2-nistp256 SHA256:z3ncPINSdcNwD/PSodGdoeXxFwVTv69emPxn9f+zUw4
debug1: update_known_hosts: known hosts file /home/derek/.ssh/known_hosts2 does not exist
debug1: pledge: fork
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:19:02 UTC 2026

  System load:  0.0               Processes:             114
  Usage of /:   5.8% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ ping 10.0.2.4
PING 10.0.2.4 (10.0.2.4) 56(84) bytes of data.
64 bytes from 10.0.2.4: icmp_seq=1 ttl=64 time=1.26 ms
64 bytes from 10.0.2.4: icmp_seq=2 ttl=64 time=2.16 ms
64 bytes from 10.0.2.4: icmp_seq=3 ttl=64 time=5.02 ms
64 bytes from 10.0.2.4: icmp_seq=4 ttl=64 time=3.65 ms
64 bytes from 10.0.2.4: icmp_seq=5 ttl=64 time=1.37 ms
64 bytes from 10.0.2.4: icmp_seq=6 ttl=64 time=1.39 ms
64 bytes from 10.0.2.4: icmp_seq=7 ttl=64 time=4.93 ms
64 bytes from 10.0.2.4: icmp_seq=8 ttl=64 time=6.28 ms
64 bytes from 10.0.2.4: icmp_seq=9 ttl=64 time=17.1 ms
64 bytes from 10.0.2.4: icmp_seq=10 ttl=64 time=15.7 ms
64 bytes from 10.0.2.4: icmp_seq=11 ttl=64 time=1.88 ms
64 bytes from 10.0.2.4: icmp_seq=12 ttl=64 time=1.31 ms
64 bytes from 10.0.2.4: icmp_seq=13 ttl=64 time=1.66 ms
64 bytes from 10.0.2.4: icmp_seq=14 ttl=64 time=0.767 ms
64 bytes from 10.0.2.4: icmp_seq=15 ttl=64 time=2.28 ms
64 bytes from 10.0.2.4: icmp_seq=16 ttl=64 time=1.07 ms
64 bytes from 10.0.2.4: icmp_seq=17 ttl=64 time=1.59 ms
64 bytes from 10.0.2.4: icmp_seq=18 ttl=64 time=2.13 ms
64 bytes from 10.0.2.4: icmp_seq=19 ttl=64 time=0.894 ms
64 bytes from 10.0.2.4: icmp_seq=20 ttl=64 time=2.67 ms
64 bytes from 10.0.2.4: icmp_seq=21 ttl=64 time=5.67 ms
64 bytes from 10.0.2.4: icmp_seq=22 ttl=64 time=1.10 ms
64 bytes from 10.0.2.4: icmp_seq=23 ttl=64 time=12.5 ms
64 bytes from 10.0.2.4: icmp_seq=24 ttl=64 time=4.08 ms
64 bytes from 10.0.2.4: icmp_seq=25 ttl=64 time=0.811 ms
64 bytes from 10.0.2.4: icmp_seq=26 ttl=64 time=3.53 ms
64 bytes from 10.0.2.4: icmp_seq=27 ttl=64 time=1.44 ms
64 bytes from 10.0.2.4: icmp_seq=28 ttl=64 time=0.797 ms
64 bytes from 10.0.2.4: icmp_seq=29 ttl=64 time=0.743 ms
64 bytes from 10.0.2.4: icmp_seq=30 ttl=64 time=1.79 ms
64 bytes from 10.0.2.4: icmp_seq=31 ttl=64 time=1.24 ms
64 bytes from 10.0.2.4: icmp_seq=32 ttl=64 time=3.81 ms
64 bytes from 10.0.2.4: icmp_seq=33 ttl=64 time=6.66 ms
64 bytes from 10.0.2.4: icmp_seq=34 ttl=64 time=5.60 ms
64 bytes from 10.0.2.4: icmp_seq=35 ttl=64 time=2.37 ms
64 bytes from 10.0.2.4: icmp_seq=36 ttl=64 time=0.752 ms
64 bytes from 10.0.2.4: icmp_seq=37 ttl=64 time=3.38 ms
64 bytes from 10.0.2.4: icmp_seq=38 ttl=64 time=9.14 ms
64 bytes from 10.0.2.4: icmp_seq=39 ttl=64 time=0.836 ms
64 bytes from 10.0.2.4: icmp_seq=40 ttl=64 time=1.60 ms
64 bytes from 10.0.2.4: icmp_seq=41 ttl=64 time=10.4 ms
64 bytes from 10.0.2.4: icmp_seq=42 ttl=64 time=6.38 ms
64 bytes from 10.0.2.4: icmp_seq=43 ttl=64 time=1.53 ms
^C
--- 10.0.2.4 ping statistics ---
43 packets transmitted, 43 received, 0% packet loss, time 42208ms
rtt min/avg/max/mdev = 0.743/3.748/17.061/3.881 ms

derekadmin1@VM1:~$ exit
logout
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0
debug1: channel 0: free: client-session, nchannels 1
Connection to 20.51.147.79 closed.
Transferred: sent 5248, received 10808 bytes, in 249.1 seconds
Bytes per second: sent 21.1, received 43.4
debug1: Exit status 127
derek [ ~ ]$ ssh derekadmin2@20.42.100.157
The authenticity of host '20.42.100.157 (20.42.100.157)' can't be established.
ED25519 key fingerprint is SHA256:76Tg3qg/ue+rRfsKC3oPDFYIHk8iRuiL3Mu106soH8k.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '20.42.100.157' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:23:56 UTC 2026

  System load:  0.02              Processes:             114
  Usage of /:   5.8% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.2.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin2@VM2:~$ ping 10.0.1.4
PING 10.0.1.4 (10.0.1.4) 56(84) bytes of data.
64 bytes from 10.0.1.4: icmp_seq=1 ttl=64 time=14.9 ms
64 bytes from 10.0.1.4: icmp_seq=2 ttl=64 time=0.856 ms
64 bytes from 10.0.1.4: icmp_seq=3 ttl=64 time=8.68 ms
64 bytes from 10.0.1.4: icmp_seq=4 ttl=64 time=5.34 ms
64 bytes from 10.0.1.4: icmp_seq=5 ttl=64 time=8.03 ms
64 bytes from 10.0.1.4: icmp_seq=6 ttl=64 time=8.68 ms
64 bytes from 10.0.1.4: icmp_seq=7 ttl=64 time=4.45 ms
64 bytes from 10.0.1.4: icmp_seq=8 ttl=64 time=8.65 ms
64 bytes from 10.0.1.4: icmp_seq=9 ttl=64 time=2.35 ms
64 bytes from 10.0.1.4: icmp_seq=10 ttl=64 time=1.49 ms
^C
--- 10.0.1.4 ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 9040ms
rtt min/avg/max/mdev = 0.856/6.338/14.851/4.069 ms
derekadmin2@VM2:~$ exit
logout
Connection to 20.42.100.157 closed.

derek [ ~ ]$ ssh derekadmin1@20.51.147.79
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:30:58 UTC 2026

  System load:  0.0               Processes:             115
  Usage of /:   6.0% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Sun Jul 19 23:19:04 2026 from 20.42.18.188
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ ip route
default via 10.0.1.1 dev eth0 proto dhcp src 10.0.1.4 metric 100 
10.0.1.0/24 dev eth0 proto kernel scope link src 10.0.1.4 metric 100 
10.0.1.1 dev eth0 proto dhcp scope link src 10.0.1.4 metric 100 
168.63.129.16 via 10.0.1.1 dev eth0 proto dhcp src 10.0.1.4 metric 100 
169.254.169.254 via 10.0.1.1 dev eth0 proto dhcp src 10.0.1.4 metric 100 
derekadmin1@VM1:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 7c:1e:52:66:a5:cf brd ff:ff:ff:ff:ff:ff
    inet 10.0.1.4/24 metric 100 brd 10.0.1.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::7e1e:52ff:fe66:a5cf/64 scope link 
       valid_lft forever preferred_lft forever
3: enP30832s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 7c:1e:52:66:a5:cf brd ff:ff:ff:ff:ff:ff
    altname enp0s0
derekadmin1@VM1:~$ exit
logout
Connection to 20.51.147.79 closed.
derek [ ~ ]$ ssh derekadmin2@20.42.100.157
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:31:54 UTC 2026

  System load:  0.0               Processes:             117
  Usage of /:   6.0% of 28.89GB   Users logged in:       0
  Memory usage: 4%                IPv4 address for eth0: 10.0.2.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Sun Jul 19 23:23:58 2026 from 20.42.18.188
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin2@VM2:~$ ip route
default via 10.0.2.1 dev eth0 proto dhcp src 10.0.2.4 metric 100 
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.4 metric 100 
10.0.2.1 dev eth0 proto dhcp scope link src 10.0.2.4 metric 100 
168.63.129.16 via 10.0.2.1 dev eth0 proto dhcp src 10.0.2.4 metric 100 
169.254.169.254 via 10.0.2.1 dev eth0 proto dhcp src 10.0.2.4 metric 100 
derekadmin2@VM2:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:0d:3a:12:03:14 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.4/24 metric 100 brd 10.0.2.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::20d:3aff:fe12:314/64 scope link 
       valid_lft forever preferred_lft forever
3: enP30832s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 00:0d:3a:12:03:14 brd ff:ff:ff:ff:ff:ff
    altname enp0s0
derekadmin2@VM2:~$ exit
logout
Connection to 20.42.100.157 closed.

### I tried to transfer a file from VM1 to VM2, but the two VMs don't have each other's private keys, so I decided to save file transferring between VMs for a later project.

derek [ ~ ]$ ssh derekadmin1@20.51.147.79
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:36:56 UTC 2026

  System load:  0.0               Processes:             114
  Usage of /:   6.0% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Sun Jul 19 23:30:58 2026 from 20.42.18.188
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ nano hello.txt
derekadmin1@VM1:~$ cat hello.txt
Hello from VM1!
derekadmin1@VM1:~$ scp hello.txt derekadmin2@10.0.2.4:/home/derekadmin2
The authenticity of host '10.0.2.4 (10.0.2.4)' can't be established.
ED25519 key fingerprint is SHA256:76Tg3qg/ue+rRfsKC3oPDFYIHk8iRuiL3Mu106soH8k.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.2.4' (ED25519) to the list of known hosts.
derekadmin2@10.0.2.4: Permission denied (publickey).
lost connection
derekadmin1@VM1:~$ derekadmin1@VM1:~$ scp hello.txt derekadmin2@10.0.2.4:/home/derekadmin2
The authenticity of host '10.0.2.4 (10.0.2.4)' can't be established.
ED25519 key fingerprint is SHA256:76Tg3qg/ue+rRfsKC3oPDFYIHk8iRuiL3Mu106soH8k.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.2.4' (ED25519) to the list of known hosts.
derekadmin2@10.0.2.4: Permission denied (publickey).
lost connection
derekadmin1@VM1:~$ exit
logout
Connection to 20.51.147.79 closed.

### I used SCP to transfer files to both VMs and then SSH'd into the VMs to verify the files were successfully transferred.

derek [ ~ ]$ nano test.txt
derek [ ~ ]$ cat test.txt
Testing... Testing... 1, 2, 3.
derek [ ~ ]$ scp test.txt derekadmin1@20.51.147.79:/home/derekadmin1
test.txt                                                                                                                                                                                                                                                                                   100%   31    10.1KB/s   00:00    
derek [ ~ ]$ scp test.txt derekadmin2@20.42.100.157:/home/derekadmin2
test.txt                                                                                                                                                                                                                                                                                   100%   31     9.5KB/s   00:00    
derek [ ~ ]$ ssh derekadmin1@20.51.147.79
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:45:43 UTC 2026

  System load:  0.0               Processes:             116
  Usage of /:   6.0% of 28.89GB   Users logged in:       0
  Memory usage: 4%                IPv4 address for eth0: 10.0.1.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Sun Jul 19 23:36:56 2026 from 20.42.18.188
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin1@VM1:~$ cat test.txt
Testing... Testing... 1, 2, 3.
derekadmin1@VM1:~$ exit
logout
Connection to 20.51.147.79 closed.
derek [ ~ ]$ ssh derekadmin2@20.42.100.157
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jul 19 23:46:21 UTC 2026

  System load:  0.0               Processes:             114
  Usage of /:   6.0% of 28.89GB   Users logged in:       0
  Memory usage: 3%                IPv4 address for eth0: 10.0.2.4
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

New release '24.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Sun Jul 19 23:31:54 2026 from 20.42.18.188
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

derekadmin2@VM2:~$ cat test.txt
Testing... Testing... 1, 2, 3.
derekadmin2@VM2:~$ exit
logout
Connection to 20.42.100.157 closed.

derek [ ~ ]$ az group delete \
> --name TRG \
> --yes
derek [ ~ ]$ az group exists \
> --name TRG
false
