---
title: Capture an image of a Linux VM in Azure using CLI 2.0 | Microsoft Docs
description: Capture an image of an Azure VM to use for mass deployments using the Azure CLI 2.0.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2018
ms.author: cynthn
ms.openlocfilehash: e3c451cfb04509b11821012ad9db1202ca052785
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819668"
---
# <a name="how-to-create-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="52256-103">How to create an image of a virtual machine or VHD</span><span class="sxs-lookup"><span data-stu-id="52256-103">How to create an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of the tutorial-->

<span data-ttu-id="52256-104">To create multiple copies of a virtual machine (VM) to use in Azure, capture an image of the VM or the OS VHD.</span><span class="sxs-lookup"><span data-stu-id="52256-104">To create multiple copies of a virtual machine (VM) to use in Azure, capture an image of the VM or the OS VHD.</span></span> <span data-ttu-id="52256-105">To create an image, you need remove personal account information which makes it safer to deploy multiple times.</span><span class="sxs-lookup"><span data-stu-id="52256-105">To create an image, you need remove personal account information which makes it safer to deploy multiple times.</span></span> <span data-ttu-id="52256-106">In the following steps you deprovision an existing VM, deallocate and create an image.</span><span class="sxs-lookup"><span data-stu-id="52256-106">In the following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="52256-107">You can use this image to create VMs across any resource group within your subscription.</span><span class="sxs-lookup"><span data-stu-id="52256-107">You can use this image to create VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="52256-108">If you want to create a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="52256-108">If you want to create a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="52256-109">You can also use **Packer** to create your custom configuration.</span><span class="sxs-lookup"><span data-stu-id="52256-109">You can also use **Packer** to create your custom configuration.</span></span> <span data-ttu-id="52256-110">For more information on using Packer, see [How to use Packer to create Linux virtual machine images in Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="52256-110">For more information on using Packer, see [How to use Packer to create Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="52256-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="52256-111">Before you begin</span></span>
<span data-ttu-id="52256-112">Ensure that you meet the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="52256-112">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="52256-113">You need an Azure VM created in the Resource Manager deployment model using managed disks.</span><span class="sxs-lookup"><span data-stu-id="52256-113">You need an Azure VM created in the Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="52256-114">If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md), the [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="52256-114">If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md), the [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="52256-115">Configure the VM as needed.</span><span class="sxs-lookup"><span data-stu-id="52256-115">Configure the VM as needed.</span></span> <span data-ttu-id="52256-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span><span class="sxs-lookup"><span data-stu-id="52256-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="52256-117">You also need to have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="52256-117">You also need to have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="52256-118">Quick commands</span><span class="sxs-lookup"><span data-stu-id="52256-118">Quick commands</span></span>

<span data-ttu-id="52256-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="52256-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-the-vm"></a><span data-ttu-id="52256-120">Step 1: Deprovision the VM</span><span class="sxs-lookup"><span data-stu-id="52256-120">Step 1: Deprovision the VM</span></span>
<span data-ttu-id="52256-121">You deprovision the VM, using the Azure VM agent, to delete machine specific files and data.</span><span class="sxs-lookup"><span data-stu-id="52256-121">You deprovision the VM, using the Azure VM agent, to delete machine specific files and data.</span></span> <span data-ttu-id="52256-122">Use the `waagent` command with the *-deprovision+user* parameter on your source Linux VM.</span><span class="sxs-lookup"><span data-stu-id="52256-122">Use the `waagent` command with the *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="52256-123">For more information, see the [Azure Linux Agent user guide](../extensions/agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="52256-123">For more information, see the [Azure Linux Agent user guide](../extensions/agent-linux.md).</span></span>

1. <span data-ttu-id="52256-124">Connect to your Linux VM using an SSH client.</span><span class="sxs-lookup"><span data-stu-id="52256-124">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="52256-125">In the SSH window, type the following command:</span><span class="sxs-lookup"><span data-stu-id="52256-125">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="52256-126">Only run this command on a VM that you intend to capture as an image.</span><span class="sxs-lookup"><span data-stu-id="52256-126">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="52256-127">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span><span class="sxs-lookup"><span data-stu-id="52256-127">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="52256-128">The *+user* parameter also removes the last provisioned user account.</span><span class="sxs-lookup"><span data-stu-id="52256-128">The *+user* parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="52256-129">If you want to keep account credentials in the VM, just use *-deprovision* to leave the user account in place.</span><span class="sxs-lookup"><span data-stu-id="52256-129">If you want to keep account credentials in the VM, just use *-deprovision* to leave the user account in place.</span></span>
 
3. <span data-ttu-id="52256-130">Type **y** to continue.</span><span class="sxs-lookup"><span data-stu-id="52256-130">Type **y** to continue.</span></span> <span data-ttu-id="52256-131">You can add the **-force** parameter to avoid this confirmation step.</span><span class="sxs-lookup"><span data-stu-id="52256-131">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="52256-132">After the command completes, type **exit**.</span><span class="sxs-lookup"><span data-stu-id="52256-132">After the command completes, type **exit**.</span></span> <span data-ttu-id="52256-133">This step closes the SSH client.</span><span class="sxs-lookup"><span data-stu-id="52256-133">This step closes the SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="52256-134">Step 2: Create VM image</span><span class="sxs-lookup"><span data-stu-id="52256-134">Step 2: Create VM image</span></span>
<span data-ttu-id="52256-135">Use the Azure CLI 2.0 to mark the VM as generalized and capture the image.</span><span class="sxs-lookup"><span data-stu-id="52256-135">Use the Azure CLI 2.0 to mark the VM as generalized and capture the image.</span></span> <span data-ttu-id="52256-136">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="52256-136">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="52256-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span><span class="sxs-lookup"><span data-stu-id="52256-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="52256-138">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="52256-138">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="52256-139">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="52256-139">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="52256-140">Mark the VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="52256-140">Mark the VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="52256-141">The following example marks the VM named *myVM* in the resource group named *myResourceGroup* as generalized:</span><span class="sxs-lookup"><span data-stu-id="52256-141">The following example marks the VM named *myVM* in the resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="52256-142">Now create an image of the VM resource with [az image create](/cli/azure/image#az_image_create).</span><span class="sxs-lookup"><span data-stu-id="52256-142">Now create an image of the VM resource with [az image create](/cli/azure/image#az_image_create).</span></span> <span data-ttu-id="52256-143">The following example creates an image named *myImage* in the resource group named *myResourceGroup* using the VM resource named *myVM*:</span><span class="sxs-lookup"><span data-stu-id="52256-143">The following example creates an image named *myImage* in the resource group named *myResourceGroup* using the VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="52256-144">The image is created in the same resource group as your source VM.</span><span class="sxs-lookup"><span data-stu-id="52256-144">The image is created in the same resource group as your source VM.</span></span> <span data-ttu-id="52256-145">You can create VMs in any resource group within your subscription from this image.</span><span class="sxs-lookup"><span data-stu-id="52256-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="52256-146">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span><span class="sxs-lookup"><span data-stu-id="52256-146">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span></span>
   >
   > <span data-ttu-id="52256-147">If you would like to store your image in zone-resilient storage, you need to create it in a region that supports [availability zones](../../availability-zones/az-overview.md) and include the `--zone-resilient true` parameter.</span><span class="sxs-lookup"><span data-stu-id="52256-147">If you would like to store your image in zone-resilient storage, you need to create it in a region that supports [availability zones](../../availability-zones/az-overview.md) and include the `--zone-resilient true` parameter.</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="52256-148">Step 3: Create a VM from the captured image</span><span class="sxs-lookup"><span data-stu-id="52256-148">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="52256-149">Create a VM using the image you created with [az vm create](/cli/azure/vm#az_vm_create).</span><span class="sxs-lookup"><span data-stu-id="52256-149">Create a VM using the image you created with [az vm create](/cli/azure/vm#az_vm_create).</span></span> <span data-ttu-id="52256-150">The following example creates a VM named *myVMDeployed* from the image named *myImage*:</span><span class="sxs-lookup"><span data-stu-id="52256-150">The following example creates a VM named *myVMDeployed* from the image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-the-vm-in-another-resource-group"></a><span data-ttu-id="52256-151">Creating the VM in another resource group</span><span class="sxs-lookup"><span data-stu-id="52256-151">Creating the VM in another resource group</span></span> 

<span data-ttu-id="52256-152">You can create VMs from an image in any resource group within your subscription.</span><span class="sxs-lookup"><span data-stu-id="52256-152">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="52256-153">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span><span class="sxs-lookup"><span data-stu-id="52256-153">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span></span> <span data-ttu-id="52256-154">Use [az image list](/cli/azure/image#az_image_list) to view a list of images.</span><span class="sxs-lookup"><span data-stu-id="52256-154">Use [az image list](/cli/azure/image#az_image_list) to view a list of images.</span></span> <span data-ttu-id="52256-155">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="52256-155">The output is similar to the following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="52256-156">The following example uses [az vm create](/cli/azure/vm#az_vm_create) to create a VM in a different resource group than the source image by specifying the image resource ID:</span><span class="sxs-lookup"><span data-stu-id="52256-156">The following example uses [az vm create](/cli/azure/vm#az_vm_create) to create a VM in a different resource group than the source image by specifying the image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-the-deployment"></a><span data-ttu-id="52256-157">Step 4: Verify the deployment</span><span class="sxs-lookup"><span data-stu-id="52256-157">Step 4: Verify the deployment</span></span>

<span data-ttu-id="52256-158">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span><span class="sxs-lookup"><span data-stu-id="52256-158">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="52256-159">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#az_vm_show):</span><span class="sxs-lookup"><span data-stu-id="52256-159">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#az_vm_show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="52256-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="52256-160">Next steps</span></span>
<span data-ttu-id="52256-161">You can create multiple VMs from your source VM image.</span><span class="sxs-lookup"><span data-stu-id="52256-161">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="52256-162">If you need to make changes to your image:</span><span class="sxs-lookup"><span data-stu-id="52256-162">If you need to make changes to your image:</span></span> 

- <span data-ttu-id="52256-163">Create a VM from your image.</span><span class="sxs-lookup"><span data-stu-id="52256-163">Create a VM from your image.</span></span>
- <span data-ttu-id="52256-164">Make any updates or configuration changes.</span><span class="sxs-lookup"><span data-stu-id="52256-164">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="52256-165">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span><span class="sxs-lookup"><span data-stu-id="52256-165">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="52256-166">Use this new image for future deployments.</span><span class="sxs-lookup"><span data-stu-id="52256-166">Use this new image for future deployments.</span></span> <span data-ttu-id="52256-167">If desired, delete the original image.</span><span class="sxs-lookup"><span data-stu-id="52256-167">If desired, delete the original image.</span></span>

<span data-ttu-id="52256-168">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="52256-168">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure).</span></span>
