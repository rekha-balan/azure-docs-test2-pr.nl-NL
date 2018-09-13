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
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="24827-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="24827-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="24827-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span><span class="sxs-lookup"><span data-stu-id="24827-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="24827-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span><span class="sxs-lookup"><span data-stu-id="24827-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="24827-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp)) for your Linux VM using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="24827-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp)) for your Linux VM using the Resource Manager deployment model.</span></span> <span data-ttu-id="24827-107">You can also [perform these steps for VMs using the Classic deployment model](classic/remote-desktop.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24827-107">You can also [perform these steps for VMs using the Classic deployment model](classic/remote-desktop.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="24827-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="24827-108">Prerequisites</span></span>
<span data-ttu-id="24827-109">This article requires an existing Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="24827-109">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="24827-110">If you need to create a VM, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="24827-110">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="24827-111">The [Azure CLI 2.0](../linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [Azure CLI 1.0](quick-create-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="24827-111">The [Azure CLI 2.0](../linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [Azure CLI 1.0](quick-create-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
- <span data-ttu-id="24827-112">The [Azure portal](../linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="24827-112">The [Azure portal](../linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

<span data-ttu-id="24827-113">You also need to be logged in to an [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24827-113">You also need to be logged in to an [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="24827-114">Quick commands</span><span class="sxs-lookup"><span data-stu-id="24827-114">Quick commands</span></span>
<span data-ttu-id="24827-115">If you need to quickly accomplish the task, the following section details the base commands to install and configure remote desktop on your VM.</span><span class="sxs-lookup"><span data-stu-id="24827-115">If you need to quickly accomplish the task, the following section details the base commands to install and configure remote desktop on your VM.</span></span> <span data-ttu-id="24827-116">More detailed information and context for each step can be found in the rest of the document, [starting here](#install-graphical-environment-on-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="24827-116">More detailed information and context for each step can be found in the rest of the document, [starting here](#install-graphical-environment-on-linux-vm).</span></span>

<span data-ttu-id="24827-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="24827-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="24827-118">Other distributions and desktop environments vary slightly.</span><span class="sxs-lookup"><span data-stu-id="24827-118">Other distributions and desktop environments vary slightly.</span></span> <span data-ttu-id="24827-119">For example, use **yum** to install on Red Hat Enterprise Linux and configure appropriate **selinux** rules, or use **zypper** to install on SUSE.</span><span class="sxs-lookup"><span data-stu-id="24827-119">For example, use **yum** to install on Red Hat Enterprise Linux and configure appropriate **selinux** rules, or use **zypper** to install on SUSE.</span></span>

<span data-ttu-id="24827-120">SSH to your VM.</span><span class="sxs-lookup"><span data-stu-id="24827-120">SSH to your VM.</span></span> <span data-ttu-id="24827-121">Install the xfce desktop environment as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-121">Install the xfce desktop environment as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

<span data-ttu-id="24827-122">Install xrdp as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-122">Install xrdp as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="24827-123">Configure xrdp to use xfce as your desktop environment as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-123">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="24827-124">Restart the xrdp service:</span><span class="sxs-lookup"><span data-stu-id="24827-124">Restart the xrdp service:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="24827-125">Set a password for your user account if currently only using SSH key for authentication:</span><span class="sxs-lookup"><span data-stu-id="24827-125">Set a password for your user account if currently only using SSH key for authentication:</span></span>

```bash
sudo passwd ops
```

<span data-ttu-id="24827-126">Exit the SSH session to your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="24827-126">Exit the SSH session to your Linux VM.</span></span> <span data-ttu-id="24827-127">Use the Azure CLI on your local computer to create a network security group rule to allow the remote desktop traffic.</span><span class="sxs-lookup"><span data-stu-id="24827-127">Use the Azure CLI on your local computer to create a network security group rule to allow the remote desktop traffic.</span></span> <span data-ttu-id="24827-128">Use [az network nsg rule create](/cli/azure/network/nsg/rule#create) with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="24827-128">Use [az network nsg rule create](/cli/azure/network/nsg/rule#create) with the Azure CLI 2.0.</span></span> <span data-ttu-id="24827-129">The following example creates a rule named `myNetworkSecurityGroupRule` within `myNetworkSecurityGroup` to allow traffic on tcp port 3389:</span><span class="sxs-lookup"><span data-stu-id="24827-129">The following example creates a rule named `myNetworkSecurityGroupRule` within `myNetworkSecurityGroup` to allow traffic on tcp port 3389:</span></span>
    
```azurecli
az network nsg rule create --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
    --protocol tcp --direction inbound --priority 1010 \
    --source-address-prefix * --source-port-range * \
    --destination-address-prefix * --destination-port-range 3389 \
    --access allow
```

<span data-ttu-id="24827-130">Or, with the Azure CLI 1.0:</span><span class="sxs-lookup"><span data-stu-id="24827-130">Or, with the Azure CLI 1.0:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
    --protocol tcp --direction inbound --priority 1010 \
    --destination-port-range 3389 --access allow
```

<span data-ttu-id="24827-131">Connect to your Linux VM using your remote desktop client of choice.</span><span class="sxs-lookup"><span data-stu-id="24827-131">Connect to your Linux VM using your remote desktop client of choice.</span></span>

![Connect to xrdp using your Remote Desktop client](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/use-remote-desktop/remote-desktop-client.png)

## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="24827-133">Install a desktop environment on your Linux VM</span><span class="sxs-lookup"><span data-stu-id="24827-133">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="24827-134">Most Linux VMs in Azure do not have a desktop environment installed by default.</span><span class="sxs-lookup"><span data-stu-id="24827-134">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="24827-135">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span><span class="sxs-lookup"><span data-stu-id="24827-135">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="24827-136">There are various desktop environments in Linux that you can choose.</span><span class="sxs-lookup"><span data-stu-id="24827-136">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="24827-137">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span><span class="sxs-lookup"><span data-stu-id="24827-137">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="24827-138">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="24827-138">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="24827-139">Commands for other distributions vary slightly (use **yum** to install on Red Hat Enterprise Linux and configure appropriate **selinux** rules, or use **zypper** to install on SUSE, for example).</span><span class="sxs-lookup"><span data-stu-id="24827-139">Commands for other distributions vary slightly (use **yum** to install on Red Hat Enterprise Linux and configure appropriate **selinux** rules, or use **zypper** to install on SUSE, for example).</span></span>

<span data-ttu-id="24827-140">First, SSH to your VM.</span><span class="sxs-lookup"><span data-stu-id="24827-140">First, SSH to your VM.</span></span> <span data-ttu-id="24827-141">The following example connects to the VM named `myvm.westus.cloudapp.azure.com` with the username of `ops`:</span><span class="sxs-lookup"><span data-stu-id="24827-141">The following example connects to the VM named `myvm.westus.cloudapp.azure.com` with the username of `ops`:</span></span>

```bash
ssh ops@myvm.westus.cloudapp.azure.com ~/.ssh/id_rsa.pub
```

<span data-ttu-id="24827-142">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="24827-142">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="24827-143">Next, install xfce using `apt` as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-143">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="24827-144">Install and configure a remote desktop server</span><span class="sxs-lookup"><span data-stu-id="24827-144">Install and configure a remote desktop server</span></span>
<span data-ttu-id="24827-145">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span><span class="sxs-lookup"><span data-stu-id="24827-145">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="24827-146">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span><span class="sxs-lookup"><span data-stu-id="24827-146">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="24827-147">Install xrdp on your Ubuntu VM as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-147">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="24827-148">Tell xrdp what desktop environment to use when you start your session.</span><span class="sxs-lookup"><span data-stu-id="24827-148">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="24827-149">Configure xrdp to use xfce as your desktop environment as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-149">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="24827-150">Restart the xrdp service for the changes to take effect as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-150">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="24827-151">Set a local user account password</span><span class="sxs-lookup"><span data-stu-id="24827-151">Set a local user account password</span></span>
<span data-ttu-id="24827-152">If you created a password for your user account when you created your VM, skip this step.</span><span class="sxs-lookup"><span data-stu-id="24827-152">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="24827-153">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span><span class="sxs-lookup"><span data-stu-id="24827-153">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="24827-154">xrdp cannot accept SSH keys for authentication.</span><span class="sxs-lookup"><span data-stu-id="24827-154">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="24827-155">The following example specifies a password for the user account `ops`:</span><span class="sxs-lookup"><span data-stu-id="24827-155">The following example specifies a password for the user account `ops`:</span></span>

```bash
sudo passwd ops
```

> [!NOTE]
> <span data-ttu-id="24827-156">Specifying a password does not update your sshd configuration to permit password logins if it currently does not.</span><span class="sxs-lookup"><span data-stu-id="24827-156">Specifying a password does not update your sshd configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="24827-157">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span><span class="sxs-lookup"><span data-stu-id="24827-157">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="24827-158">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span><span class="sxs-lookup"><span data-stu-id="24827-158">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="24827-159">Create a Network Security Group rule for Remote Desktop traffic</span><span class="sxs-lookup"><span data-stu-id="24827-159">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="24827-160">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span><span class="sxs-lookup"><span data-stu-id="24827-160">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="24827-161">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="24827-161">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="24827-162">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24827-162">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="24827-163">The following examples create a network security group rule named `myNetworkSecurityGroupRule` to `allow` traffic on `tcp` port `3389`.</span><span class="sxs-lookup"><span data-stu-id="24827-163">The following examples create a network security group rule named `myNetworkSecurityGroupRule` to `allow` traffic on `tcp` port `3389`.</span></span>

- <span data-ttu-id="24827-164">Use [az network nsg rule create](/cli/azure/network/nsg/rule#create) with the Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="24827-164">Use [az network nsg rule create](/cli/azure/network/nsg/rule#create) with the Azure CLI 2.0:</span></span>
    
    ```azurecli
    az network nsg rule create --resource-group myResourceGroup \
        --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
        --protocol tcp --direction inbound --priority 1010 \
        --source-address-prefix '*' --source-port-range '*' \
        --destination-address-prefix '*' --destination-port-range 3389 \
        --access allow
    ```

- <span data-ttu-id="24827-165">Or, use the Azure CLI 1.0:</span><span class="sxs-lookup"><span data-stu-id="24827-165">Or, use the Azure CLI 1.0:</span></span>

    ```azurecli
    azure network nsg rule create --resource-group myResourceGroup \
        --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
        --protocol tcp --direction inbound --priority 1010 \
        --destination-port-range 3389 --access allow
    ```

## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="24827-166">Connect your Linux VM with a Remote Desktop client</span><span class="sxs-lookup"><span data-stu-id="24827-166">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="24827-167">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="24827-167">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="24827-168">Enter the username and password for the user account on your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-168">Enter the username and password for the user account on your VM as follows:</span></span>

![Connect to xrdp using your Remote Desktop client](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="24827-170">After authenticating, the xfce desktop environment will load and look similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="24827-170">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![xfce desktop environment through xrdp](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="24827-172">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="24827-172">Troubleshoot</span></span>
<span data-ttu-id="24827-173">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-173">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="24827-174">The following example shows the VM listening on TCP port 3389 as expected:</span><span class="sxs-lookup"><span data-stu-id="24827-174">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="24827-175">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span><span class="sxs-lookup"><span data-stu-id="24827-175">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="24827-176">Review logs in `/var/log` on your Ubuntu VM for indications as to why the service may not be responding.</span><span class="sxs-lookup"><span data-stu-id="24827-176">Review logs in `/var/log` on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="24827-177">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span><span class="sxs-lookup"><span data-stu-id="24827-177">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="24827-178">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span><span class="sxs-lookup"><span data-stu-id="24827-178">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="24827-179">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span><span class="sxs-lookup"><span data-stu-id="24827-179">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="24827-180">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span><span class="sxs-lookup"><span data-stu-id="24827-180">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="24827-181">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24827-181">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="24827-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="24827-182">Next steps</span></span>
<span data-ttu-id="24827-183">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24827-183">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="24827-184">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24827-184">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>




