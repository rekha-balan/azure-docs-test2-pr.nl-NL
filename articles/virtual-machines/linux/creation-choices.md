---
title: Different ways to create a Linux VM in Azure | Microsoft Azure
description: Learn the different ways to create a Linux virtual machine on Azure, including links to tools and tutorials for each method.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: iainfou
ms.openlocfilehash: ac74e8cef75e793c4d3aa788fabe237a68d87f77
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554295"
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="e43b9-103">Different ways to create a Linux VM</span><span class="sxs-lookup"><span data-stu-id="e43b9-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="e43b9-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span><span class="sxs-lookup"><span data-stu-id="e43b9-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="e43b9-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e43b9-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="e43b9-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e43b9-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="e43b9-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span><span class="sxs-lookup"><span data-stu-id="e43b9-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="e43b9-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="e43b9-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

<span data-ttu-id="e43b9-109">The following examples use the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e43b9-109">The following examples use the Azure CLI 2.0.</span></span> <span data-ttu-id="e43b9-110">Read each article for more details on the commands shown.</span><span class="sxs-lookup"><span data-stu-id="e43b9-110">Read each article for more details on the commands shown.</span></span> <span data-ttu-id="e43b9-111">You can also find examples on Linux creation choices using the [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e43b9-111">You can also find examples on Linux creation choices using the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

* [<span data-ttu-id="e43b9-112">Create a Linux VM using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e43b9-112">Create a Linux VM using the Azure CLI 2.0</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="e43b9-113">This example uses [az group create](/cli/azure/group#create) to create a resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e43b9-113">This example uses [az group create](/cli/azure/group#create) to create a resource group named `myResourceGroup`:</span></span> 
-    
    ```azurecli
    az group create --name myResourceGroup --location westus
    ```
    
  * <span data-ttu-id="e43b9-114">This example uses [az vm create](/cli/azure/vm#create) to create a VM named `myVM` using the latest Debian image with Azure Managed Disks and a public key named `id_rsa.pub`:</span><span class="sxs-lookup"><span data-stu-id="e43b9-114">This example uses [az vm create](/cli/azure/vm#create) to create a VM named `myVM` using the latest Debian image with Azure Managed Disks and a public key named `id_rsa.pub`:</span></span>

    ```azurecli
    az vm create \
    --image credativ:Debian:8:latest \
     --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
az vm disk attach –g myResourceGroup –-vm-name myVM –-disk myDataDisk  –-new --size-gb 5    --public-ip-address-dns-name myPublicDNS \
    --resource-group myResourceGroup \
    --location westus \
    --name myVM
    ```

    * <span data-ttu-id="e43b9-115">If you wish to use unmanaged disks, add the `--use-unmanaged-disks` flag to the above command.</span><span class="sxs-lookup"><span data-stu-id="e43b9-115">If you wish to use unmanaged disks, add the `--use-unmanaged-disks` flag to the above command.</span></span> <span data-ttu-id="e43b9-116">A storage account is created for you.</span><span class="sxs-lookup"><span data-stu-id="e43b9-116">A storage account is created for you.</span></span> <span data-ttu-id="e43b9-117">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e43b9-117">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span>

* [<span data-ttu-id="e43b9-118">Create a secured Linux VM using an Azure template</span><span class="sxs-lookup"><span data-stu-id="e43b9-118">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="e43b9-119">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM using a template stored on GitHub:</span><span class="sxs-lookup"><span data-stu-id="e43b9-119">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
    
* [<span data-ttu-id="e43b9-120">Create a complete Linux environment using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e43b9-120">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="e43b9-121">Includes creating a load balancer and multiple VMs in an availability set.</span><span class="sxs-lookup"><span data-stu-id="e43b9-121">Includes creating a load balancer and multiple VMs in an availability set.</span></span>

* [<span data-ttu-id="e43b9-122">Add a disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="e43b9-122">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  
  * <span data-ttu-id="e43b9-123">The following example uses [az vm disk attach-new](/cli/azure/vm/disk#attach-new) to add a 50 Gb managed disk to an existing VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e43b9-123">The following example uses [az vm disk attach-new](/cli/azure/vm/disk#attach-new) to add a 50 Gb managed disk to an existing VM named `myVM`:</span></span>
  
    ```azurecli
    az vm disk attach –g myResourceGroup –-vm-name myVM –-disk myDataDisk  \
    –-new --size-gb 50
    ```

## <a name="azure-portal"></a><span data-ttu-id="e43b9-124">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e43b9-124">Azure portal</span></span>
<span data-ttu-id="e43b9-125">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span><span class="sxs-lookup"><span data-stu-id="e43b9-125">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="e43b9-126">Use the Azure portal to create the VM:</span><span class="sxs-lookup"><span data-stu-id="e43b9-126">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="e43b9-127">Create a Linux VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e43b9-127">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 
* [<span data-ttu-id="e43b9-128">Attach a disk using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e43b9-128">Attach a disk using the Azure portal</span></span>](../windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="e43b9-129">Operating system and image choices</span><span class="sxs-lookup"><span data-stu-id="e43b9-129">Operating system and image choices</span></span>
<span data-ttu-id="e43b9-130">When creating a VM, you choose an image based on the operating system you want to run.</span><span class="sxs-lookup"><span data-stu-id="e43b9-130">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="e43b9-131">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span><span class="sxs-lookup"><span data-stu-id="e43b9-131">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="e43b9-132">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="e43b9-132">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="e43b9-133">Azure images</span><span class="sxs-lookup"><span data-stu-id="e43b9-133">Azure images</span></span>
<span data-ttu-id="e43b9-134">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span><span class="sxs-lookup"><span data-stu-id="e43b9-134">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="e43b9-135">List available publishers:</span><span class="sxs-lookup"><span data-stu-id="e43b9-135">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location WestUS
```

<span data-ttu-id="e43b9-136">List available products (offers) for a given publisher:</span><span class="sxs-lookup"><span data-stu-id="e43b9-136">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location WestUS
```

<span data-ttu-id="e43b9-137">List available SKUs (distro releases) of a given offer:</span><span class="sxs-lookup"><span data-stu-id="e43b9-137">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location WestUS
```

<span data-ttu-id="e43b9-138">List all available images for a given release:</span><span class="sxs-lookup"><span data-stu-id="e43b9-138">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location WestUS
```

<span data-ttu-id="e43b9-139">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e43b9-139">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e43b9-140">The **az vm create** command has aliases you can use to quickly access the more common distros and their latest releases.</span><span class="sxs-lookup"><span data-stu-id="e43b9-140">The **az vm create** command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="e43b9-141">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span><span class="sxs-lookup"><span data-stu-id="e43b9-141">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="e43b9-142">Alias</span><span class="sxs-lookup"><span data-stu-id="e43b9-142">Alias</span></span> | <span data-ttu-id="e43b9-143">Publisher</span><span class="sxs-lookup"><span data-stu-id="e43b9-143">Publisher</span></span> | <span data-ttu-id="e43b9-144">Offer</span><span class="sxs-lookup"><span data-stu-id="e43b9-144">Offer</span></span> | <span data-ttu-id="e43b9-145">SKU</span><span class="sxs-lookup"><span data-stu-id="e43b9-145">SKU</span></span> | <span data-ttu-id="e43b9-146">Version</span><span class="sxs-lookup"><span data-stu-id="e43b9-146">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="e43b9-147">CentOS</span><span class="sxs-lookup"><span data-stu-id="e43b9-147">CentOS</span></span> |<span data-ttu-id="e43b9-148">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e43b9-148">OpenLogic</span></span> |<span data-ttu-id="e43b9-149">Centos</span><span class="sxs-lookup"><span data-stu-id="e43b9-149">Centos</span></span> |<span data-ttu-id="e43b9-150">7.2</span><span class="sxs-lookup"><span data-stu-id="e43b9-150">7.2</span></span> |<span data-ttu-id="e43b9-151">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-151">latest</span></span> |
| <span data-ttu-id="e43b9-152">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e43b9-152">CoreOS</span></span> |<span data-ttu-id="e43b9-153">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e43b9-153">CoreOS</span></span> |<span data-ttu-id="e43b9-154">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e43b9-154">CoreOS</span></span> |<span data-ttu-id="e43b9-155">Stable</span><span class="sxs-lookup"><span data-stu-id="e43b9-155">Stable</span></span> |<span data-ttu-id="e43b9-156">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-156">latest</span></span> |
| <span data-ttu-id="e43b9-157">Debian</span><span class="sxs-lookup"><span data-stu-id="e43b9-157">Debian</span></span> |<span data-ttu-id="e43b9-158">credativ</span><span class="sxs-lookup"><span data-stu-id="e43b9-158">credativ</span></span> |<span data-ttu-id="e43b9-159">Debian</span><span class="sxs-lookup"><span data-stu-id="e43b9-159">Debian</span></span> |<span data-ttu-id="e43b9-160">8</span><span class="sxs-lookup"><span data-stu-id="e43b9-160">8</span></span> |<span data-ttu-id="e43b9-161">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-161">latest</span></span> |
| <span data-ttu-id="e43b9-162">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e43b9-162">openSUSE</span></span> |<span data-ttu-id="e43b9-163">SUSE</span><span class="sxs-lookup"><span data-stu-id="e43b9-163">SUSE</span></span> |<span data-ttu-id="e43b9-164">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e43b9-164">openSUSE</span></span> |<span data-ttu-id="e43b9-165">13.2</span><span class="sxs-lookup"><span data-stu-id="e43b9-165">13.2</span></span> |<span data-ttu-id="e43b9-166">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-166">latest</span></span> |
| <span data-ttu-id="e43b9-167">RHEL</span><span class="sxs-lookup"><span data-stu-id="e43b9-167">RHEL</span></span> |<span data-ttu-id="e43b9-168">Redhat</span><span class="sxs-lookup"><span data-stu-id="e43b9-168">Redhat</span></span> |<span data-ttu-id="e43b9-169">RHEL</span><span class="sxs-lookup"><span data-stu-id="e43b9-169">RHEL</span></span> |<span data-ttu-id="e43b9-170">7.2</span><span class="sxs-lookup"><span data-stu-id="e43b9-170">7.2</span></span> |<span data-ttu-id="e43b9-171">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-171">latest</span></span> |
| <span data-ttu-id="e43b9-172">SLES</span><span class="sxs-lookup"><span data-stu-id="e43b9-172">SLES</span></span> |<span data-ttu-id="e43b9-173">SLES</span><span class="sxs-lookup"><span data-stu-id="e43b9-173">SLES</span></span> |<span data-ttu-id="e43b9-174">SLES</span><span class="sxs-lookup"><span data-stu-id="e43b9-174">SLES</span></span> |<span data-ttu-id="e43b9-175">12-SP1</span><span class="sxs-lookup"><span data-stu-id="e43b9-175">12-SP1</span></span> |<span data-ttu-id="e43b9-176">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-176">latest</span></span> |
| <span data-ttu-id="e43b9-177">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="e43b9-177">UbuntuLTS</span></span> |<span data-ttu-id="e43b9-178">Canonical</span><span class="sxs-lookup"><span data-stu-id="e43b9-178">Canonical</span></span> |<span data-ttu-id="e43b9-179">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e43b9-179">UbuntuServer</span></span> |<span data-ttu-id="e43b9-180">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="e43b9-180">14.04.4-LTS</span></span> |<span data-ttu-id="e43b9-181">latest</span><span class="sxs-lookup"><span data-stu-id="e43b9-181">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="e43b9-182">Use your own image</span><span class="sxs-lookup"><span data-stu-id="e43b9-182">Use your own image</span></span>
<span data-ttu-id="e43b9-183">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span><span class="sxs-lookup"><span data-stu-id="e43b9-183">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="e43b9-184">You can also upload an image created on-premises.</span><span class="sxs-lookup"><span data-stu-id="e43b9-184">You can also upload an image created on-premises.</span></span> <span data-ttu-id="e43b9-185">For more information on supported distros and how to use your own images, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="e43b9-185">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="e43b9-186">Azure endorsed distributions</span><span class="sxs-lookup"><span data-stu-id="e43b9-186">Azure endorsed distributions</span></span>](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e43b9-187">Information for non-endorsed distributions</span><span class="sxs-lookup"><span data-stu-id="e43b9-187">Information for non-endorsed distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="e43b9-188">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e43b9-188">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
  
  * <span data-ttu-id="e43b9-189">Quick-start **az vm** example commands to capture an existing VM using unmanaged disks:</span><span class="sxs-lookup"><span data-stu-id="e43b9-189">Quick-start **az vm** example commands to capture an existing VM using unmanaged disks:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm capture --resource-group myResourceGroup --name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="e43b9-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="e43b9-190">Next steps</span></span>
* <span data-ttu-id="e43b9-191">Create a Linux VM from the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), with the [CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e43b9-191">Create a Linux VM from the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), with the [CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="e43b9-192">After creating a Linux VM, [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e43b9-192">After creating a Linux VM, [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="e43b9-193">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e43b9-193">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
