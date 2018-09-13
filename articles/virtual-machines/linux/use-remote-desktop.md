---
title: Use Remote Desktop to a Linux VM in Azure | Microsoft Docs
description: Learn how to install and configure Remote Desktop (xrdp) to connect to a Linux VM in Azure using graphical tools
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 6d2a505ce3b1906cc30ffd8b7ade484aa415a450
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554735"
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a>Install and configure Remote Desktop to connect to a Linux VM in Azure
Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection. When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier. This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp)) for your Linux VM using the Resource Manager deployment model. You can also [perform these steps for VMs using the Classic deployment model](classic/remote-desktop.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).


## <a name="prerequisites"></a>Prerequisites
This article requires an existing Linux VM in Azure. If you need to create a VM, use one of the following methods:

- The [Azure CLI 2.0](../linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [Azure CLI 1.0](quick-create-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- The [Azure portal](../linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

You also need to be logged in to an [active Azure account](https://azure.microsoft.com/pricing/free-trial/).


## <a name="quick-commands"></a>Quick commands
If you need to quickly accomplish the task, the following section details the base commands to install and configure remote desktop on your VM. More detailed information and context for each step can be found in the rest of the document, [starting here](#install-graphical-environment-on-linux-vm).

The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM. Other distributions and desktop environments vary slightly. For example, use **yum** to install on Red Hat Enterprise Linux and configure appropriate **selinux** rules, or use **zypper** to install on SUSE.

SSH to your VM. Install the xfce desktop environment as follows:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

Install xrdp as follows:

```bash
sudo apt-get install xrdp
```

Configure xrdp to use xfce as your desktop environment as follows:

```bash
echo xfce4-session >~/.xsession
```

Restart the xrdp service:

```bash
sudo service xrdp restart
```

Set a password for your user account if currently only using SSH key for authentication:

```bash
sudo passwd ops
```

Exit the SSH session to your Linux VM. Use the Azure CLI on your local computer to create a network security group rule to allow the remote desktop traffic. Use [az network nsg rule create](/cli/azure/network/nsg/rule#create) with the Azure CLI 2.0. The following example creates a rule named `myNetworkSecurityGroupRule` within `myNetworkSecurityGroup` to allow traffic on tcp port 3389:
    
```azurecli
az network nsg rule create --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
    --protocol tcp --direction inbound --priority 1010 \
    --source-address-prefix * --source-port-range * \
    --destination-address-prefix * --destination-port-range 3389 \
    --access allow
```

Or, with the Azure CLI 1.0:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
    --protocol tcp --direction inbound --priority 1010 \
    --destination-port-range 3389 --access allow
```

Connect to your Linux VM using your remote desktop client of choice.

![Connect to xrdp using your Remote Desktop client](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/use-remote-desktop/remote-desktop-client.png)

## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Install a desktop environment on your Linux VM
Most Linux VMs in Azure do not have a desktop environment installed by default. Linux VMs are commonly managed using SSH connections rather than a desktop environment. There are various desktop environments in Linux that you can choose. Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.

The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM. Commands for other distributions vary slightly (use **yum** to install on Red Hat Enterprise Linux and configure appropriate **selinux** rules, or use **zypper** to install on SUSE, for example).

First, SSH to your VM. The following example connects to the VM named `myvm.westus.cloudapp.azure.com` with the username of `ops`:

```bash
ssh ops@myvm.westus.cloudapp.azure.com ~/.ssh/id_rsa.pub
```

If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).

Next, install xfce using `apt` as follows:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Install and configure a remote desktop server
Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections. [xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce. Install xrdp on your Ubuntu VM as follows:

```bash
sudo apt-get install xrdp
```

Tell xrdp what desktop environment to use when you start your session. Configure xrdp to use xfce as your desktop environment as follows:

```bash
echo xfce4-session >~/.xsession
```

Restart the xrdp service for the changes to take effect as follows:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Set a local user account password
If you created a password for your user account when you created your VM, skip this step. If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM. xrdp cannot accept SSH keys for authentication. The following example specifies a password for the user account `ops`:

```bash
sudo passwd ops
```

> [!NOTE]
> Specifying a password does not update your sshd configuration to permit password logins if it currently does not. From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp. If so, skip the following step on creating a network security group rule to allow remote desktop traffic.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Create a Network Security Group rule for Remote Desktop traffic
To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM. For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

The following examples create a network security group rule named `myNetworkSecurityGroupRule` to `allow` traffic on `tcp` port `3389`.

- Use [az network nsg rule create](/cli/azure/network/nsg/rule#create) with the Azure CLI 2.0:
    
    ```azurecli
    az network nsg rule create --resource-group myResourceGroup \
        --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
        --protocol tcp --direction inbound --priority 1010 \
        --source-address-prefix '*' --source-port-range '*' \
        --destination-address-prefix '*' --destination-port-range 3389 \
        --access allow
    ```

- Or, use the Azure CLI 1.0:

    ```azurecli
    azure network nsg rule create --resource-group myResourceGroup \
        --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
        --protocol tcp --direction inbound --priority 1010 \
        --destination-port-range 3389 --access allow
    ```

## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Connect your Linux VM with a Remote Desktop client
Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM. Enter the username and password for the user account on your VM as follows:

![Connect to xrdp using your Remote Desktop client](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/use-remote-desktop/remote-desktop-client.png)

After authenticating, the xfce desktop environment will load and look similar to the following example:

![xfce desktop environment through xrdp](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Troubleshoot
If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:

```bash
sudo netstat -plnt | grep rdp
```

The following example shows the VM listening on TCP port 3389 as expected:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:

```bash
sudo service xrdp restart
```

Review logs in `/var/log` on your Ubuntu VM for indications as to why the service may not be responding. You can also monitor the syslog during a remote desktop connection attempt to view any errors:

```bash
tail -f /var/log/syslog
```

Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.

If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM. Review your network security group rules to ensure that you have a rule to permit TCP on port 3389. For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="next-steps"></a>Next steps
For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).




