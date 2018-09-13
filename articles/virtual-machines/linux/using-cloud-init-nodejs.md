---
title: Using cloud-init to customize a Linux VM during creation in Azure | Microsoft Docs
description: How to use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: aa5bab547081f81f8907c0c1930ff49df968b735
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554961"
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="ae7c1-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ae7c1-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="ae7c1-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="ae7c1-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="ae7c1-106">The article requires:</span><span class="sxs-lookup"><span data-stu-id="ae7c1-106">The article requires:</span></span>

* <span data-ttu-id="ae7c1-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="ae7c1-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="ae7c1-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="ae7c1-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ae7c1-110">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="ae7c1-110">CLI versions to complete the task</span></span>
<span data-ttu-id="ae7c1-111">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="ae7c1-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ae7c1-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="ae7c1-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ae7c1-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="ae7c1-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ae7c1-114">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="ae7c1-114">Quick Commands</span></span>
<span data-ttu-id="ae7c1-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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
<span data-ttu-id="ae7c1-116">Create a resource group to launch VMs into.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="ae7c1-117">Create a Linux VM using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ae7c1-118">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="ae7c1-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="ae7c1-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="ae7c1-119">Introduction</span></span>
<span data-ttu-id="ae7c1-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="ae7c1-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="ae7c1-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="ae7c1-123">Inject scripts using cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="ae7c1-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae7c1-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="ae7c1-125">An Azure template using cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="ae7c1-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae7c1-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ae7c1-127">To inject scripts at any time after boot:</span><span class="sxs-lookup"><span data-stu-id="ae7c1-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="ae7c1-128">SSH to run commands directly</span><span class="sxs-lookup"><span data-stu-id="ae7c1-128">SSH to run commands directly</span></span>
* <span data-ttu-id="ae7c1-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span><span class="sxs-lookup"><span data-stu-id="ae7c1-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="ae7c1-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="ae7c1-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="ae7c1-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="ae7c1-133">Cloud-init availability on Azure VM quick-create image aliases:</span><span class="sxs-lookup"><span data-stu-id="ae7c1-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="ae7c1-134">Alias</span><span class="sxs-lookup"><span data-stu-id="ae7c1-134">Alias</span></span> | <span data-ttu-id="ae7c1-135">Publisher</span><span class="sxs-lookup"><span data-stu-id="ae7c1-135">Publisher</span></span> | <span data-ttu-id="ae7c1-136">Offer</span><span class="sxs-lookup"><span data-stu-id="ae7c1-136">Offer</span></span> | <span data-ttu-id="ae7c1-137">SKU</span><span class="sxs-lookup"><span data-stu-id="ae7c1-137">SKU</span></span> | <span data-ttu-id="ae7c1-138">Version</span><span class="sxs-lookup"><span data-stu-id="ae7c1-138">Version</span></span> | <span data-ttu-id="ae7c1-139">cloud-init</span><span class="sxs-lookup"><span data-stu-id="ae7c1-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="ae7c1-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae7c1-140">CentOS</span></span> |<span data-ttu-id="ae7c1-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="ae7c1-141">OpenLogic</span></span> |<span data-ttu-id="ae7c1-142">Centos</span><span class="sxs-lookup"><span data-stu-id="ae7c1-142">Centos</span></span> |<span data-ttu-id="ae7c1-143">7.2</span><span class="sxs-lookup"><span data-stu-id="ae7c1-143">7.2</span></span> |<span data-ttu-id="ae7c1-144">latest</span><span class="sxs-lookup"><span data-stu-id="ae7c1-144">latest</span></span> |<span data-ttu-id="ae7c1-145">no</span><span class="sxs-lookup"><span data-stu-id="ae7c1-145">no</span></span> |
| <span data-ttu-id="ae7c1-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ae7c1-146">CoreOS</span></span> |<span data-ttu-id="ae7c1-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ae7c1-147">CoreOS</span></span> |<span data-ttu-id="ae7c1-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ae7c1-148">CoreOS</span></span> |<span data-ttu-id="ae7c1-149">Stable</span><span class="sxs-lookup"><span data-stu-id="ae7c1-149">Stable</span></span> |<span data-ttu-id="ae7c1-150">latest</span><span class="sxs-lookup"><span data-stu-id="ae7c1-150">latest</span></span> |<span data-ttu-id="ae7c1-151">yes</span><span class="sxs-lookup"><span data-stu-id="ae7c1-151">yes</span></span> |
| <span data-ttu-id="ae7c1-152">Debian</span><span class="sxs-lookup"><span data-stu-id="ae7c1-152">Debian</span></span> |<span data-ttu-id="ae7c1-153">credativ</span><span class="sxs-lookup"><span data-stu-id="ae7c1-153">credativ</span></span> |<span data-ttu-id="ae7c1-154">Debian</span><span class="sxs-lookup"><span data-stu-id="ae7c1-154">Debian</span></span> |<span data-ttu-id="ae7c1-155">8</span><span class="sxs-lookup"><span data-stu-id="ae7c1-155">8</span></span> |<span data-ttu-id="ae7c1-156">latest</span><span class="sxs-lookup"><span data-stu-id="ae7c1-156">latest</span></span> |<span data-ttu-id="ae7c1-157">no</span><span class="sxs-lookup"><span data-stu-id="ae7c1-157">no</span></span> |
| <span data-ttu-id="ae7c1-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ae7c1-158">openSUSE</span></span> |<span data-ttu-id="ae7c1-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="ae7c1-159">SUSE</span></span> |<span data-ttu-id="ae7c1-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ae7c1-160">openSUSE</span></span> |<span data-ttu-id="ae7c1-161">13.2</span><span class="sxs-lookup"><span data-stu-id="ae7c1-161">13.2</span></span> |<span data-ttu-id="ae7c1-162">latest</span><span class="sxs-lookup"><span data-stu-id="ae7c1-162">latest</span></span> |<span data-ttu-id="ae7c1-163">no</span><span class="sxs-lookup"><span data-stu-id="ae7c1-163">no</span></span> |
| <span data-ttu-id="ae7c1-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae7c1-164">RHEL</span></span> |<span data-ttu-id="ae7c1-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="ae7c1-165">Redhat</span></span> |<span data-ttu-id="ae7c1-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae7c1-166">RHEL</span></span> |<span data-ttu-id="ae7c1-167">7.2</span><span class="sxs-lookup"><span data-stu-id="ae7c1-167">7.2</span></span> |<span data-ttu-id="ae7c1-168">latest</span><span class="sxs-lookup"><span data-stu-id="ae7c1-168">latest</span></span> |<span data-ttu-id="ae7c1-169">no</span><span class="sxs-lookup"><span data-stu-id="ae7c1-169">no</span></span> |
| <span data-ttu-id="ae7c1-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="ae7c1-170">UbuntuLTS</span></span> |<span data-ttu-id="ae7c1-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="ae7c1-171">Canonical</span></span> |<span data-ttu-id="ae7c1-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="ae7c1-172">UbuntuServer</span></span> |<span data-ttu-id="ae7c1-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="ae7c1-173">14.04.4-LTS</span></span> |<span data-ttu-id="ae7c1-174">latest</span><span class="sxs-lookup"><span data-stu-id="ae7c1-174">latest</span></span> |<span data-ttu-id="ae7c1-175">yes</span><span class="sxs-lookup"><span data-stu-id="ae7c1-175">yes</span></span> |

<span data-ttu-id="ae7c1-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="ae7c1-177">Adding a cloud-init script to the VM creation with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae7c1-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="ae7c1-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="ae7c1-179">Create a resource group to launch VMs into.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="ae7c1-180">Create a Linux VM using cloud-init to configure it during boot.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="ae7c1-181">Creating a cloud-init script to set the hostname of a Linux VM</span><span class="sxs-lookup"><span data-stu-id="ae7c1-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="ae7c1-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="ae7c1-183">We can easily set this using cloud-init with this script.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="ae7c1-184">Example cloud-init script named `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="ae7c1-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="ae7c1-186">Login and verify the hostname of the new VM.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="ae7c1-187">Creating a cloud-init script to update Linux</span><span class="sxs-lookup"><span data-stu-id="ae7c1-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="ae7c1-188">For security, you want your Ubuntu VM to update on the first boot.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="ae7c1-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="ae7c1-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span><span class="sxs-lookup"><span data-stu-id="ae7c1-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="ae7c1-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="ae7c1-192">Login and verify all packages are updated.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="ae7c1-193">Creating a cloud-init script to add a user to Linux</span><span class="sxs-lookup"><span data-stu-id="ae7c1-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="ae7c1-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="ae7c1-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="ae7c1-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span><span class="sxs-lookup"><span data-stu-id="ae7c1-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="ae7c1-197">After Linux has booted, all the listed users are created and added to the sudo group.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="ae7c1-198">Login and verify the newly created user.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="ae7c1-199">Output</span><span class="sxs-lookup"><span data-stu-id="ae7c1-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="ae7c1-200">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ae7c1-200">Next Steps</span></span>
<span data-ttu-id="ae7c1-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="ae7c1-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="ae7c1-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="ae7c1-204">With cloud-init, you would need a reboot to reset the password.</span><span class="sxs-lookup"><span data-stu-id="ae7c1-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="ae7c1-205">About virtual machine extensions and features</span><span class="sxs-lookup"><span data-stu-id="ae7c1-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="ae7c1-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="ae7c1-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

