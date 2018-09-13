---
title: Different ways to create a Linux VM | Microsoft Docs
description: Learn the different ways to create a Linux virtual machine on Azure, including links to tools and tutorials for each method.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: ''
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: iainfou
ms.openlocfilehash: a48fedc0148d1a2ff3ea4fb7711dbc78a1cf458f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554717"
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="4d514-103">Different ways to create a Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="4d514-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="4d514-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span><span class="sxs-lookup"><span data-stu-id="4d514-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="4d514-105">This article summarizes these differences and examples for creating your Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="4d514-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="4d514-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4d514-106">Azure CLI</span></span>
<span data-ttu-id="4d514-107">You can create VMs in Azure using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="4d514-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="4d514-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="4d514-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4d514-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="4d514-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="4d514-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span><span class="sxs-lookup"><span data-stu-id="4d514-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="4d514-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4d514-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="4d514-112">The following tutorials provide examples on using the Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="4d514-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="4d514-113">Read each article for more details on the CLI quick-start commands shown:</span><span class="sxs-lookup"><span data-stu-id="4d514-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="4d514-114">Create a Linux VM from the Azure CLI for dev and test</span><span class="sxs-lookup"><span data-stu-id="4d514-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="4d514-115">The following example creates a CoreOS VM using a public key named `azure_id_rsa.pub`:</span><span class="sxs-lookup"><span data-stu-id="4d514-115">The following example creates a CoreOS VM using a public key named `azure_id_rsa.pub`:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="4d514-116">Create a secured Linux VM using an Azure template</span><span class="sxs-lookup"><span data-stu-id="4d514-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="4d514-117">The following example creates a VM using a template stored on GitHub:</span><span class="sxs-lookup"><span data-stu-id="4d514-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location WestUS 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="4d514-118">Create a complete Linux environment using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4d514-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="4d514-119">Includes creating a load balancer and multiple VMs in an availability set.</span><span class="sxs-lookup"><span data-stu-id="4d514-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="4d514-120">Add a disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="4d514-120">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="4d514-121">The following example adds a 5Gb disk to an existing VM named `TestVM`:</span><span class="sxs-lookup"><span data-stu-id="4d514-121">The following example adds a 5Gb disk to an existing VM named `TestVM`:</span></span>
    
    ```azurecli
    azure vm disk attach-new --resource-group myResourceGroup  --vm-name myVM \
      --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="4d514-122">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4d514-122">Azure portal</span></span>
<span data-ttu-id="4d514-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span><span class="sxs-lookup"><span data-stu-id="4d514-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="4d514-124">Use the Azure portal to create the VM:</span><span class="sxs-lookup"><span data-stu-id="4d514-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="4d514-125">Create a Linux VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4d514-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 
* [<span data-ttu-id="4d514-126">Attach a disk using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4d514-126">Attach a disk using the Azure portal</span></span>](../windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="4d514-127">Operating system and image choices</span><span class="sxs-lookup"><span data-stu-id="4d514-127">Operating system and image choices</span></span>
<span data-ttu-id="4d514-128">When creating a VM, you choose an image based on the operating system you want to run.</span><span class="sxs-lookup"><span data-stu-id="4d514-128">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="4d514-129">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span><span class="sxs-lookup"><span data-stu-id="4d514-129">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="4d514-130">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="4d514-130">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="4d514-131">Azure images</span><span class="sxs-lookup"><span data-stu-id="4d514-131">Azure images</span></span>
<span data-ttu-id="4d514-132">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span><span class="sxs-lookup"><span data-stu-id="4d514-132">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="4d514-133">List available publishers as follows:</span><span class="sxs-lookup"><span data-stu-id="4d514-133">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location WestUS
```

<span data-ttu-id="4d514-134">List available products (offers) for a given publisher as follows:</span><span class="sxs-lookup"><span data-stu-id="4d514-134">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location WestUS --publisher Canonical
```

<span data-ttu-id="4d514-135">List available SKUs (distro releases) of a given offer as follows:</span><span class="sxs-lookup"><span data-stu-id="4d514-135">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location WestUS --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="4d514-136">List all available images for a given release follows:</span><span class="sxs-lookup"><span data-stu-id="4d514-136">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location WestUS --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="4d514-137">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d514-137">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4d514-138">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span><span class="sxs-lookup"><span data-stu-id="4d514-138">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="4d514-139">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span><span class="sxs-lookup"><span data-stu-id="4d514-139">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="4d514-140">Alias</span><span class="sxs-lookup"><span data-stu-id="4d514-140">Alias</span></span> | <span data-ttu-id="4d514-141">Publisher</span><span class="sxs-lookup"><span data-stu-id="4d514-141">Publisher</span></span> | <span data-ttu-id="4d514-142">Offer</span><span class="sxs-lookup"><span data-stu-id="4d514-142">Offer</span></span> | <span data-ttu-id="4d514-143">SKU</span><span class="sxs-lookup"><span data-stu-id="4d514-143">SKU</span></span> | <span data-ttu-id="4d514-144">Version</span><span class="sxs-lookup"><span data-stu-id="4d514-144">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4d514-145">CentOS</span><span class="sxs-lookup"><span data-stu-id="4d514-145">CentOS</span></span> |<span data-ttu-id="4d514-146">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4d514-146">OpenLogic</span></span> |<span data-ttu-id="4d514-147">Centos</span><span class="sxs-lookup"><span data-stu-id="4d514-147">Centos</span></span> |<span data-ttu-id="4d514-148">7.2</span><span class="sxs-lookup"><span data-stu-id="4d514-148">7.2</span></span> |<span data-ttu-id="4d514-149">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-149">latest</span></span> |
| <span data-ttu-id="4d514-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4d514-150">CoreOS</span></span> |<span data-ttu-id="4d514-151">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4d514-151">CoreOS</span></span> |<span data-ttu-id="4d514-152">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4d514-152">CoreOS</span></span> |<span data-ttu-id="4d514-153">Stable</span><span class="sxs-lookup"><span data-stu-id="4d514-153">Stable</span></span> |<span data-ttu-id="4d514-154">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-154">latest</span></span> |
| <span data-ttu-id="4d514-155">Debian</span><span class="sxs-lookup"><span data-stu-id="4d514-155">Debian</span></span> |<span data-ttu-id="4d514-156">credativ</span><span class="sxs-lookup"><span data-stu-id="4d514-156">credativ</span></span> |<span data-ttu-id="4d514-157">Debian</span><span class="sxs-lookup"><span data-stu-id="4d514-157">Debian</span></span> |<span data-ttu-id="4d514-158">8</span><span class="sxs-lookup"><span data-stu-id="4d514-158">8</span></span> |<span data-ttu-id="4d514-159">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-159">latest</span></span> |
| <span data-ttu-id="4d514-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4d514-160">openSUSE</span></span> |<span data-ttu-id="4d514-161">SUSE</span><span class="sxs-lookup"><span data-stu-id="4d514-161">SUSE</span></span> |<span data-ttu-id="4d514-162">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4d514-162">openSUSE</span></span> |<span data-ttu-id="4d514-163">13.2</span><span class="sxs-lookup"><span data-stu-id="4d514-163">13.2</span></span> |<span data-ttu-id="4d514-164">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-164">latest</span></span> |
| <span data-ttu-id="4d514-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="4d514-165">RHEL</span></span> |<span data-ttu-id="4d514-166">Redhat</span><span class="sxs-lookup"><span data-stu-id="4d514-166">Redhat</span></span> |<span data-ttu-id="4d514-167">RHEL</span><span class="sxs-lookup"><span data-stu-id="4d514-167">RHEL</span></span> |<span data-ttu-id="4d514-168">7.2</span><span class="sxs-lookup"><span data-stu-id="4d514-168">7.2</span></span> |<span data-ttu-id="4d514-169">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-169">latest</span></span> |
| <span data-ttu-id="4d514-170">SLES</span><span class="sxs-lookup"><span data-stu-id="4d514-170">SLES</span></span> |<span data-ttu-id="4d514-171">SLES</span><span class="sxs-lookup"><span data-stu-id="4d514-171">SLES</span></span> |<span data-ttu-id="4d514-172">SLES</span><span class="sxs-lookup"><span data-stu-id="4d514-172">SLES</span></span> |<span data-ttu-id="4d514-173">12-SP1</span><span class="sxs-lookup"><span data-stu-id="4d514-173">12-SP1</span></span> |<span data-ttu-id="4d514-174">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-174">latest</span></span> |
| <span data-ttu-id="4d514-175">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="4d514-175">UbuntuLTS</span></span> |<span data-ttu-id="4d514-176">Canonical</span><span class="sxs-lookup"><span data-stu-id="4d514-176">Canonical</span></span> |<span data-ttu-id="4d514-177">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="4d514-177">UbuntuServer</span></span> |<span data-ttu-id="4d514-178">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="4d514-178">14.04.4-LTS</span></span> |<span data-ttu-id="4d514-179">latest</span><span class="sxs-lookup"><span data-stu-id="4d514-179">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="4d514-180">Use your own image</span><span class="sxs-lookup"><span data-stu-id="4d514-180">Use your own image</span></span>
<span data-ttu-id="4d514-181">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span><span class="sxs-lookup"><span data-stu-id="4d514-181">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="4d514-182">You can also upload an image created on-premises.</span><span class="sxs-lookup"><span data-stu-id="4d514-182">You can also upload an image created on-premises.</span></span> <span data-ttu-id="4d514-183">For more information on supported distros and how to use your own images, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="4d514-183">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="4d514-184">Azure endorsed distributions</span><span class="sxs-lookup"><span data-stu-id="4d514-184">Azure endorsed distributions</span></span>](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4d514-185">Information for non-endorsed distributions</span><span class="sxs-lookup"><span data-stu-id="4d514-185">Information for non-endorsed distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4d514-186">Upload and create a Linux VM from custom disk image</span><span class="sxs-lookup"><span data-stu-id="4d514-186">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="4d514-187">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d514-187">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
  
  * <span data-ttu-id="4d514-188">Quick-start example commands to capture an existing VM:</span><span class="sxs-lookup"><span data-stu-id="4d514-188">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="4d514-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d514-189">Next steps</span></span>
* <span data-ttu-id="4d514-190">Create a Linux VM from the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), with the [CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d514-190">Create a Linux VM from the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), with the [CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="4d514-191">After creating a Linux VM, [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d514-191">After creating a Linux VM, [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="4d514-192">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4d514-192">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

