---
title: Use cloud-init to customize a Linux VM | Microsoft Docs
description: How to use cloud-init to customize a Linux VM during creation with the Azure CLI 2.0 Preview
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/10/2017
ms.author: iainfou
ms.openlocfilehash: a5891444757f45ba4d6223a4fbd17aad61931418
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549232"
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="fe376-103">Use cloud-init to customize a Linux VM during creation</span><span class="sxs-lookup"><span data-stu-id="fe376-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="fe376-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="fe376-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span>  <span data-ttu-id="fe376-105">The cloud-init scripts are called when you create a VM from Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fe376-105">The cloud-init scripts are called when you create a VM from Azure CLI.</span></span>  <span data-ttu-id="fe376-106">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe376-106">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fe376-107">Quick commands</span><span class="sxs-lookup"><span data-stu-id="fe376-107">Quick commands</span></span>
<span data-ttu-id="fe376-108">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span><span class="sxs-lookup"><span data-stu-id="fe376-108">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

<span data-ttu-id="fe376-109">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fe376-109">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fe376-110">The following example creates the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fe376-110">The following example creates the resource group named `myResourceGroup`:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="fe376-111">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-111">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="fe376-112">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="fe376-112">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="fe376-113">Introduction</span><span class="sxs-lookup"><span data-stu-id="fe376-113">Introduction</span></span>
<span data-ttu-id="fe376-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span><span class="sxs-lookup"><span data-stu-id="fe376-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="fe376-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span><span class="sxs-lookup"><span data-stu-id="fe376-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="fe376-116">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span><span class="sxs-lookup"><span data-stu-id="fe376-116">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="fe376-117">Inject scripts using cloud-init.</span><span class="sxs-lookup"><span data-stu-id="fe376-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="fe376-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe376-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="fe376-119">An Azure template using cloud-init.</span><span class="sxs-lookup"><span data-stu-id="fe376-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="fe376-120">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe376-120">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fe376-121">To inject scripts at any time after boot:</span><span class="sxs-lookup"><span data-stu-id="fe376-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="fe376-122">SSH to run commands directly</span><span class="sxs-lookup"><span data-stu-id="fe376-122">SSH to run commands directly</span></span>
* <span data-ttu-id="fe376-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span><span class="sxs-lookup"><span data-stu-id="fe376-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="fe376-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span><span class="sxs-lookup"><span data-stu-id="fe376-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="fe376-125">: VMAccess Extension executes a script as root in the same way using SSH can.</span><span class="sxs-lookup"><span data-stu-id="fe376-125">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="fe376-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span><span class="sxs-lookup"><span data-stu-id="fe376-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="fe376-127">Cloud-init availability on Azure VM quick-create image aliases:</span><span class="sxs-lookup"><span data-stu-id="fe376-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="fe376-128">Alias</span><span class="sxs-lookup"><span data-stu-id="fe376-128">Alias</span></span> | <span data-ttu-id="fe376-129">Publisher</span><span class="sxs-lookup"><span data-stu-id="fe376-129">Publisher</span></span> | <span data-ttu-id="fe376-130">Offer</span><span class="sxs-lookup"><span data-stu-id="fe376-130">Offer</span></span> | <span data-ttu-id="fe376-131">SKU</span><span class="sxs-lookup"><span data-stu-id="fe376-131">SKU</span></span> | <span data-ttu-id="fe376-132">Version</span><span class="sxs-lookup"><span data-stu-id="fe376-132">Version</span></span> | <span data-ttu-id="fe376-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="fe376-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="fe376-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="fe376-134">CentOS</span></span> |<span data-ttu-id="fe376-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="fe376-135">OpenLogic</span></span> |<span data-ttu-id="fe376-136">Centos</span><span class="sxs-lookup"><span data-stu-id="fe376-136">Centos</span></span> |<span data-ttu-id="fe376-137">7.2</span><span class="sxs-lookup"><span data-stu-id="fe376-137">7.2</span></span> |<span data-ttu-id="fe376-138">latest</span><span class="sxs-lookup"><span data-stu-id="fe376-138">latest</span></span> |<span data-ttu-id="fe376-139">no</span><span class="sxs-lookup"><span data-stu-id="fe376-139">no</span></span> |
| <span data-ttu-id="fe376-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="fe376-140">CoreOS</span></span> |<span data-ttu-id="fe376-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="fe376-141">CoreOS</span></span> |<span data-ttu-id="fe376-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="fe376-142">CoreOS</span></span> |<span data-ttu-id="fe376-143">Stable</span><span class="sxs-lookup"><span data-stu-id="fe376-143">Stable</span></span> |<span data-ttu-id="fe376-144">latest</span><span class="sxs-lookup"><span data-stu-id="fe376-144">latest</span></span> |<span data-ttu-id="fe376-145">yes</span><span class="sxs-lookup"><span data-stu-id="fe376-145">yes</span></span> |
| <span data-ttu-id="fe376-146">Debian</span><span class="sxs-lookup"><span data-stu-id="fe376-146">Debian</span></span> |<span data-ttu-id="fe376-147">credativ</span><span class="sxs-lookup"><span data-stu-id="fe376-147">credativ</span></span> |<span data-ttu-id="fe376-148">Debian</span><span class="sxs-lookup"><span data-stu-id="fe376-148">Debian</span></span> |<span data-ttu-id="fe376-149">8</span><span class="sxs-lookup"><span data-stu-id="fe376-149">8</span></span> |<span data-ttu-id="fe376-150">latest</span><span class="sxs-lookup"><span data-stu-id="fe376-150">latest</span></span> |<span data-ttu-id="fe376-151">no</span><span class="sxs-lookup"><span data-stu-id="fe376-151">no</span></span> |
| <span data-ttu-id="fe376-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="fe376-152">openSUSE</span></span> |<span data-ttu-id="fe376-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="fe376-153">SUSE</span></span> |<span data-ttu-id="fe376-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="fe376-154">openSUSE</span></span> |<span data-ttu-id="fe376-155">13.2</span><span class="sxs-lookup"><span data-stu-id="fe376-155">13.2</span></span> |<span data-ttu-id="fe376-156">latest</span><span class="sxs-lookup"><span data-stu-id="fe376-156">latest</span></span> |<span data-ttu-id="fe376-157">no</span><span class="sxs-lookup"><span data-stu-id="fe376-157">no</span></span> |
| <span data-ttu-id="fe376-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="fe376-158">RHEL</span></span> |<span data-ttu-id="fe376-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="fe376-159">Redhat</span></span> |<span data-ttu-id="fe376-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="fe376-160">RHEL</span></span> |<span data-ttu-id="fe376-161">7.2</span><span class="sxs-lookup"><span data-stu-id="fe376-161">7.2</span></span> |<span data-ttu-id="fe376-162">latest</span><span class="sxs-lookup"><span data-stu-id="fe376-162">latest</span></span> |<span data-ttu-id="fe376-163">no</span><span class="sxs-lookup"><span data-stu-id="fe376-163">no</span></span> |
| <span data-ttu-id="fe376-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="fe376-164">UbuntuLTS</span></span> |<span data-ttu-id="fe376-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="fe376-165">Canonical</span></span> |<span data-ttu-id="fe376-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="fe376-166">UbuntuServer</span></span> |<span data-ttu-id="fe376-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="fe376-167">14.04.4-LTS</span></span> |<span data-ttu-id="fe376-168">latest</span><span class="sxs-lookup"><span data-stu-id="fe376-168">latest</span></span> |<span data-ttu-id="fe376-169">yes</span><span class="sxs-lookup"><span data-stu-id="fe376-169">yes</span></span> |

<span data-ttu-id="fe376-170">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span><span class="sxs-lookup"><span data-stu-id="fe376-170">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="fe376-171">Add a cloud-init script to the VM creation with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fe376-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="fe376-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span><span class="sxs-lookup"><span data-stu-id="fe376-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="fe376-173">Create a resource group to launch VMs into.</span><span class="sxs-lookup"><span data-stu-id="fe376-173">Create a resource group to launch VMs into.</span></span>

<span data-ttu-id="fe376-174">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fe376-174">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fe376-175">The following example creates the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fe376-175">The following example creates the resource group named `myResourceGroup`:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="fe376-176">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-176">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="fe376-177">Create a cloud-init script to set the hostname of a Linux VM</span><span class="sxs-lookup"><span data-stu-id="fe376-177">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="fe376-178">One of the simplest and most important settings for any Linux VM would be the hostname.</span><span class="sxs-lookup"><span data-stu-id="fe376-178">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="fe376-179">We can easily set this using cloud-init with this script.</span><span class="sxs-lookup"><span data-stu-id="fe376-179">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="fe376-180">Example cloud-init script named `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="fe376-180">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="fe376-181">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span><span class="sxs-lookup"><span data-stu-id="fe376-181">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span> <span data-ttu-id="fe376-182">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-182">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --custom-data cloud-init.txt
```

<span data-ttu-id="fe376-183">Login and verify the hostname of the new VM.</span><span class="sxs-lookup"><span data-stu-id="fe376-183">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="fe376-184">Create a cloud-init script to update Linux</span><span class="sxs-lookup"><span data-stu-id="fe376-184">Create a cloud-init script to update Linux</span></span>
<span data-ttu-id="fe376-185">For security, you want your Ubuntu VM to update on the first boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-185">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="fe376-186">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span><span class="sxs-lookup"><span data-stu-id="fe376-186">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="fe376-187">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span><span class="sxs-lookup"><span data-stu-id="fe376-187">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="fe376-188">After Linux has booted, all the installed packages are updated via `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="fe376-188">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span> <span data-ttu-id="fe376-189">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-189">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="fe376-190">Login and verify all packages are updated.</span><span class="sxs-lookup"><span data-stu-id="fe376-190">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="fe376-191">Create a cloud-init script to add a user to Linux</span><span class="sxs-lookup"><span data-stu-id="fe376-191">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="fe376-192">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span><span class="sxs-lookup"><span data-stu-id="fe376-192">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="fe376-193">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span><span class="sxs-lookup"><span data-stu-id="fe376-193">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="fe376-194">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span><span class="sxs-lookup"><span data-stu-id="fe376-194">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="fe376-195">After Linux has booted, all the listed users are created and added to the sudo group.</span><span class="sxs-lookup"><span data-stu-id="fe376-195">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="fe376-196">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-196">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="fe376-197">Login and verify the newly created user.</span><span class="sxs-lookup"><span data-stu-id="fe376-197">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="fe376-198">Output</span><span class="sxs-lookup"><span data-stu-id="fe376-198">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="fe376-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe376-199">Next steps</span></span>
<span data-ttu-id="fe376-200">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span><span class="sxs-lookup"><span data-stu-id="fe376-200">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="fe376-201">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span><span class="sxs-lookup"><span data-stu-id="fe376-201">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="fe376-202">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span><span class="sxs-lookup"><span data-stu-id="fe376-202">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="fe376-203">With cloud-init, you would need a reboot to reset the password.</span><span class="sxs-lookup"><span data-stu-id="fe376-203">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="fe376-204">About virtual machine extensions and features</span><span class="sxs-lookup"><span data-stu-id="fe376-204">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="fe376-205">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="fe376-205">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

