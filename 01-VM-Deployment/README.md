# Project 01 - Create resource group and VM, establish SSH connection, delete VM and resource group.

## Resource Group Creation

### Upon connecting to Azure CLI, the first thing I did was create a resource group. I had previously tried using variables for the name/location (i.e. "export RESOURCE_GROUP_NAME=TRG$RANDOM_ID"), but I was encountering issues, so I opted to use literals instead of variables.

derek [ ~ ]$ az group create \
> --name TRG1.0 \
> --location eastus2
{
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG1.0",
  "location": "eastus2",
  "managedBy": null,
  "name": "TRG1.0",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}

## VM Creation

### Then, I set the VM image to the latest Ubuntu 22.04 image.

derek [ ~ ]$ export vm_image="Canonical:0001-com-ubuntu-minimal-jammy:minimal-22_04-lts-gen2:latest"

### I attempted to create a VM

derek [ ~ ]$ az vm create \
> --resource-group TRG1.0 \
> --name TVM1 \
> --image $vm_image \
> --admin-username operator \
> --assign-identity \
> --generate-ssh-keys \
> --public-ip-sku Standard
ERROR: the following arguments are required: --name/-n, --resource-group/-g

### The VM image failed, because I didn't use capital letters when setting its value earlier. Therefore, I reset the value correctly and verified it was accepted.

derek [ ~ ]$ echo $VM_IMAGE

derek [ ~ ]$ export VM_IMAGE="Canonical:0001-com-ubuntu-minimal-jammy:minimal-22_04-lts-gen2:latest"
derek [ ~ ]$ echo $VM_IMAGE
Canonical:0001-com-ubuntu-minimal-jammy:minimal-22_04-lts-gen2:latest

### Then I could reattempt VM creation

derek [ ~ ]$ az vm create \
> --resource-group TRG1.0 \
> --name TVM1 \
> --image $VM_IMAGE \
> --admin-username operator \
> --assign-identity \
> --generate-ssh-keys \
> --public-ip-sku Standard

### The SSH keys were generated, but then I got a long error which had the below notifcation that the VM size was not available in my location.

Exception Details:      (SkuNotAvailable) The requested VM size for resource 'Following SKUs have failed for Capacity Restrictions: Standard_D2s_v5' is currently not available in location 'eastus2'. Please try another size or deploy to a different location or different zone. See https://aka.ms/azureskunotavailable for details.
        Code: SkuNotAvailable
        Message: The requested VM size for resource 'Following SKUs have failed for Capacity Restrictions: Standard_D2s_v5' is currently not available in location 'eastus2'. Please try another size or deploy to a different location or different zone. See https://aka.ms/azureskunotavailable for details.

### Next, I checked the available Standard_B VM sizes in eastus2 with grep. I searched for Standard_B because they're generally the cheapest sizes.

derek [ ~ ]$ az vm list-skus \
> --location eastus2 \
> --resource-type virtualMachines \
> --output table
> | grep Standard_B

### There were no Standard_B VMs available, so I checked Standard_D next. Since there were no Bs, Ds are the next cheapest.

derek [ ~ ]$ az vm list-skus \
> --location eastus2 \
> --resource-type virtualMachines \
> --output table
> | grep Standard_D

### There were a ton of available Standard_D VM sizes available, so I chose Standard_D2s_v7. Success.

derek [ ~ ]$ az vm create \
> --resource-group TRG1.0 \
> --name TVM1 \
> --image $VM_IMAGE \
> --admin-username operator \
> --assign-identity \
> --generate-ssh-keys \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
No access was given yet to the 'TVM1', because '--scope' was not provided. You should setup by creating a role assignment, e.g. 'az role assignment create --assignee <principal-id> --role contributor -g TRG1.0' would let it access the current resource group. To get the pricipal id, run 'az vm show -g TRG1.0 -n TVM1 --query "identity.principalId" -otsv'
{
  "fqdns": "",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG1.0/providers/Microsoft.Compute/virtualMachines/TVM1",
  "identity": {
    "systemAssignedIdentity": "96789677-4c09-4c53-a126-030455a82302",
    "userAssignedIdentities": {}
  },
  "location": "eastus2",
  "macAddress": "7C-1E-52-F4-7B-B0",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.242.53.242",
  "resourceGroup": "TRG1.0"
}

## SSH

### I attempted to SSH into the VM, but was denied.

derek [ ~ ]$ ssh operator@20.242.53.242
The authenticity of host '20.242.53.242 (20.242.53.242)' can't be established.
ED25519 key fingerprint is SHA256:GePBONJbXV9WdgHOlhrb8Y7ZZR9n90yLKBbDIX4/Te4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '20.242.53.242' (ED25519) to the list of known hosts.
operator@20.242.53.242: Permission denied (publickey).
'

### I attempted troubleshooting for about 45 minutes using various different commands (e.g. verbose ssh, az vm run-command invoke w/ the command "id operator", etc.), but ultimately could not SSH into the machine. It turned out that the admin-username "operator" was not actually being created on with the VM, so SSHing into the machine was impossible. So, I deleted the VM and verified its deletion.

derek [ ~ ]$ az vm delete \
> --resource-group TRG1.0 \
> --name TVM1
Are you sure you want to perform this operation? (y/n): y
derek [ ~ ]$ az vm show \
> --resource-group TRG1.0 \
> --name TVM1
(ResourceNotFound) The Resource 'Microsoft.Compute/virtualMachines/TVM1' under resource group 'TRG1.0' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix
Code: ResourceNotFound
Message: The Resource 'Microsoft.Compute/virtualMachines/TVM1' under resource group 'TRG1.0' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix

### However, I wanted to try one more thing, so I verified the group still exists, and then tried spinning up a new VM with more specific admin username and different image.

derek [ ~ ]$ az group show \
> --name TRG1.0
{
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG1.0",
  "location": "eastus2",
  "managedBy": null,
  "name": "TRG1.0",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}

derek [ ~ ]$ az vm create \
> --resource-group TRG1.0 \
> --name TVM2 \
> --image Ubuntu2204 \
> --admin-username derekadmin \
> --authentication-type ssh \
> --generate-ssh-keys \
> --public-ip-sku Standard \
> --size Standard_D2s_v7
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG1.0/providers/Microsoft.Compute/virtualMachines/TVM2",
  "location": "eastus2",
  "macAddress": "7C-1E-52-A3-FC-72",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "20.242.80.113",
  "resourceGroup": "TRG1.0"

### I then checked to see if the admin username was created. The admin-username was finally appearing.

  derek [ ~ ]$ az vm run-command invoke \
  --resource-group TRG1.0 \
  --name TVM2 \
  --command-id RunShellScript \
  --scripts "id derekadmin"
{
  "value": [
    {
      "code": "ProvisioningState/succeeded",
      "displayStatus": "Provisioning succeeded",
      "level": "Info",
      "message": "Enable succeeded: \n[stdout]\nuid=1000(derekadmin) gid=1000(derekadmin) groups=1000(derekadmin),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),118(netdev),119(lxd)\n\n[stderr]\n"
    }
  ]
}

### I then successfully SSH'd into the new derekadmin account.

derek [ ~ ]$ ssh -v -i ~/.ssh/id_rsa derekadmin@20.242.80.113
OpenSSH_9.8p1, OpenSSL 3.3.5 30 Sep 2025
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Authenticator provider $SSH_SK_PROVIDER did not resolve; disabling
debug1: Connecting to 20.242.80.113 [20.242.80.113] port 22.
debug1: Connection established.
debug1: identity file /home/derek/.ssh/id_rsa type 0
debug1: identity file /home/derek/.ssh/id_rsa-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_9.8
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.9p1 Ubuntu-3ubuntu0.16
debug1: compat_banner: match: OpenSSH_8.9p1 Ubuntu-3ubuntu0.16 pat OpenSSH* compat 0x04000000
debug1: Authenticating to 20.242.80.113:22 as 'derekadmin'
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
debug1: Server host key: ssh-ed25519 SHA256:Dq8VMGfodGSLd4ADAjxcf0VFJRsmM9dm02JECw/2PFo
debug1: load_hostkeys: fopen /home/derek/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: hostkeys_find_by_key_hostfile: hostkeys file /home/derek/.ssh/known_hosts2 does not exist
debug1: hostkeys_find_by_key_hostfile: hostkeys file /etc/ssh/ssh_known_hosts does not exist
debug1: hostkeys_find_by_key_hostfile: hostkeys file /etc/ssh/ssh_known_hosts2 does not exist
The authenticity of host '20.242.80.113 (20.242.80.113)' can't be established.
ED25519 key fingerprint is SHA256:Dq8VMGfodGSLd4ADAjxcf0VFJRsmM9dm02JECw/2PFo.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added '20.242.80.113' (ED25519) to the list of known hosts.
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
debug1: Will attempt key: /home/derek/.ssh/id_rsa RSA SHA256:Jm2gf4AEnrS7VRlC4ylvr2Yq/oCD09qhsGHCtXPq2BQ explicit
debug1: Offering public key: /home/derek/.ssh/id_rsa RSA SHA256:Jm2gf4AEnrS7VRlC4ylvr2Yq/oCD09qhsGHCtXPq2BQ explicit
debug1: Server accepts key: /home/derek/.ssh/id_rsa RSA SHA256:Jm2gf4AEnrS7VRlC4ylvr2Yq/oCD09qhsGHCtXPq2BQ explicit
Authenticated to 20.242.80.113 ([20.242.80.113]:22) using "publickey".
debug1: channel 0: new session [client-session] (inactive timeout: 0)
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: filesystem
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: client_input_hostkeys: searching /home/derek/.ssh/known_hosts for 20.242.80.113 / (none)
debug1: client_input_hostkeys: searching /home/derek/.ssh/known_hosts2 for 20.242.80.113 / (none)
debug1: client_input_hostkeys: hostkeys file /home/derek/.ssh/known_hosts2 does not exist
debug1: Remote: /home/derekadmin/.ssh/authorized_keys:1: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug1: Remote: /home/derekadmin/.ssh/authorized_keys:1: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
Learned new hostkey: RSA SHA256:/74HjMd2/0PBf3llLDJHCSMdV8X7ria2rzbp7u9QCZo
Learned new hostkey: ECDSA SHA256:Yc+IzSZ0PtGgN+yvKSt2HPxYTkJPzaoDlaOPcqbj9ns
Adding new key for 20.242.80.113 to /home/derek/.ssh/known_hosts: ssh-rsa SHA256:/74HjMd2/0PBf3llLDJHCSMdV8X7ria2rzbp7u9QCZo
Adding new key for 20.242.80.113 to /home/derek/.ssh/known_hosts: ecdsa-sha2-nistp256 SHA256:Yc+IzSZ0PtGgN+yvKSt2HPxYTkJPzaoDlaOPcqbj9ns
debug1: update_known_hosts: known hosts file /home/derek/.ssh/known_hosts2 does not exist
debug1: pledge: fork
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1062-azure x86_64)
'

## Cleaning Up

### Since I was able to successfully SSH into the VM, I decided to exit the SSH conncection, delete my VM and resource group, and verify that all resources have been torn down so as to not incur any unnecessary costs.

derek [ ~ ]$ az vm delete \
> --name TVM2 \
> --resource-group TRG1.0
Are you sure you want to perform this operation? (y/n): y
derek [ ~ ]$ az vm show \
> --name TVM2 \
> --resource-group TRG1.0
(ResourceNotFound) The Resource 'Microsoft.Compute/virtualMachines/TVM2' under resource group 'TRG1.0' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix
Code: ResourceNotFound
Message: The Resource 'Microsoft.Compute/virtualMachines/TVM2' under resource group 'TRG1.0' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix
derek [ ~ ]$ az vm show \
> --name TVM1 \
> --resource-group TRG1.0
(ResourceNotFound) The Resource 'Microsoft.Compute/virtualMachines/TVM1' under resource group 'TRG1.0' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix
Code: ResourceNotFound
Message: The Resource 'Microsoft.Compute/virtualMachines/TVM1' under resource group 'TRG1.0' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix
derek [ ~ ]$ az group show \
> --name TRG1.0
{
  "id": "/subscriptions/1e6d5cc3-adf2-41f8-80a6-4652d5464072/resourceGroups/TRG1.0",
  "location": "eastus2",
  "managedBy": null,
  "name": "TRG1.0",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
derek [ ~ ]$ az group delete \
> --name TRG1.0
Are you sure you want to perform this operation? (y/n): y 
derek [ ~ ]$ az group show \
> --name TRG1.0
(ResourceGroupNotFound) Resource group 'TRG1.0' could not be found.
##Code: ResourceGroupNotFound
Message: Resource group 'TRG1.0' could not be found.
