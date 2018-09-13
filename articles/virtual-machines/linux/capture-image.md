---
title: Capture a Linux VM with Azure CLI 2.0 | Microsoft Docs
description: How to capture and generalize an image of a Linux-based Azure virtual machine (VM) using managed disks created with the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/02/2017
ms.author: iainfou
ms.openlocfilehash: f0431b98aeebe4cebf8425f47c9cea1b01531c79
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563118"
---
# <a name="how-to-generalize-and-capture-a-linux-virtual-machine"></a><span data-ttu-id="d6f29-103">How to generalize and capture a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="d6f29-103">How to generalize and capture a Linux virtual machine</span></span>
<span data-ttu-id="d6f29-104">To reuse virtual machines (VMs) deployed and configured in Azure, you capture an image of the VM.</span><span class="sxs-lookup"><span data-stu-id="d6f29-104">To reuse virtual machines (VMs) deployed and configured in Azure, you capture an image of the VM.</span></span> <span data-ttu-id="d6f29-105">The process also involves generalizing the VM to remove personal account information before you deploy new VMs from the image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-105">The process also involves generalizing the VM to remove personal account information before you deploy new VMs from the image.</span></span> <span data-ttu-id="d6f29-106">This article details how to capture a VM image with the Azure CLI 2.0 for a VM using Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="d6f29-106">This article details how to capture a VM image with the Azure CLI 2.0 for a VM using Azure Managed Disks.</span></span> <span data-ttu-id="d6f29-107">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="d6f29-107">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="d6f29-108">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6f29-108">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d6f29-109">This article details how to capture a Linux VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="d6f29-109">This article details how to capture a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="d6f29-110">You can also perform these steps with the [Azure CLI 1.0](capture-image-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6f29-110">You can also perform these steps with the [Azure CLI 1.0](capture-image-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="d6f29-111">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6f29-111">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d6f29-112">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6f29-112">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  


## <a name="before-you-begin"></a><span data-ttu-id="d6f29-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d6f29-113">Before you begin</span></span>
<span data-ttu-id="d6f29-114">Ensure that you meet the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="d6f29-114">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="d6f29-115">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6f29-115">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d6f29-116">Configure the VM as needed.</span><span class="sxs-lookup"><span data-stu-id="d6f29-116">Configure the VM as needed.</span></span> <span data-ttu-id="d6f29-117">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span><span class="sxs-lookup"><span data-stu-id="d6f29-117">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 

<span data-ttu-id="d6f29-118">You also need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d6f29-118">You also need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="d6f29-119">Quick commands</span><span class="sxs-lookup"><span data-stu-id="d6f29-119">Quick commands</span></span>
<span data-ttu-id="d6f29-120">If you need to quickly accomplish the task, the following section details the base commands to capture an image of a Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="d6f29-120">If you need to quickly accomplish the task, the following section details the base commands to capture an image of a Linux VM in Azure.</span></span> <span data-ttu-id="d6f29-121">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-steps).</span><span class="sxs-lookup"><span data-stu-id="d6f29-121">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-steps).</span></span> <span data-ttu-id="d6f29-122">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="d6f29-122">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d6f29-123">Example parameter names include `myResourceGroup`, `myVM`, and `myImage`.</span><span class="sxs-lookup"><span data-stu-id="d6f29-123">Example parameter names include `myResourceGroup`, `myVM`, and `myImage`.</span></span>

1. <span data-ttu-id="d6f29-124">Deprovision your source VM:</span><span class="sxs-lookup"><span data-stu-id="d6f29-124">Deprovision your source VM:</span></span>

    ```bash
    ssh ops@myvm.westus.cloudapp.azure.com
    sudo waagent -deprovision+user -force
    exit
    ```

2. <span data-ttu-id="d6f29-125">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="d6f29-125">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="d6f29-126">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="d6f29-126">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>
   
    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="d6f29-127">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="d6f29-127">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span></span>
   
    ```azurecli
    az image create --resource-group myResourceGroup --name myImage --source myVM
    ```

5. <span data-ttu-id="d6f29-128">Create a VM from your image resource with [az vm create](/cli/azure/vm#create):</span><span class="sxs-lookup"><span data-stu-id="d6f29-128">Create a VM from your image resource with [az vm create](/cli/azure/vm#create):</span></span>

    ```azurecli
    az vm create --resource-group myResourceGroup --name myVMDeployed --image myImage
        --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub
    ```

## <a name="detailed-steps"></a><span data-ttu-id="d6f29-129">Detailed steps</span><span class="sxs-lookup"><span data-stu-id="d6f29-129">Detailed steps</span></span>
<span data-ttu-id="d6f29-130">In the following steps you deprovision an existing VM, deallocate and generalize the VM resource, then create an image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-130">In the following steps you deprovision an existing VM, deallocate and generalize the VM resource, then create an image.</span></span> <span data-ttu-id="d6f29-131">You can use this image to create VMs across any resource group within your subscription.</span><span class="sxs-lookup"><span data-stu-id="d6f29-131">You can use this image to create VMs across any resource group within your subscription.</span></span> <span data-ttu-id="d6f29-132">This process gives [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) an advantage over unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="d6f29-132">This process gives [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) an advantage over unmanaged disks.</span></span> <span data-ttu-id="d6f29-133">With unmanaged disks, you create a blob copy of the underlying virtual hard disk (VHD) and are then limited to creating VMs in the same storage account as the copied VHD blob.</span><span class="sxs-lookup"><span data-stu-id="d6f29-133">With unmanaged disks, you create a blob copy of the underlying virtual hard disk (VHD) and are then limited to creating VMs in the same storage account as the copied VHD blob.</span></span> <span data-ttu-id="d6f29-134">With managed disks, you create an image resource that can be deployed across your whole subscription.</span><span class="sxs-lookup"><span data-stu-id="d6f29-134">With managed disks, you create an image resource that can be deployed across your whole subscription.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="d6f29-135">Step 1: Remove the Azure Linux agent</span><span class="sxs-lookup"><span data-stu-id="d6f29-135">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="d6f29-136">To make the VM ready for generalizing, you deprovision the VM using the Azure VM agent to delete files and data.</span><span class="sxs-lookup"><span data-stu-id="d6f29-136">To make the VM ready for generalizing, you deprovision the VM using the Azure VM agent to delete files and data.</span></span> <span data-ttu-id="d6f29-137">Use the **waagent** command with the **deprovision** parameter on your target Linux VM.</span><span class="sxs-lookup"><span data-stu-id="d6f29-137">Use the **waagent** command with the **deprovision** parameter on your target Linux VM.</span></span> <span data-ttu-id="d6f29-138">For more information, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6f29-138">For more information, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="d6f29-139">Connect to your Linux VM using an SSH client.</span><span class="sxs-lookup"><span data-stu-id="d6f29-139">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="d6f29-140">In the SSH window, type the following command:</span><span class="sxs-lookup"><span data-stu-id="d6f29-140">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="d6f29-141">Only run this command on a VM that you intend to capture as an image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-141">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="d6f29-142">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span><span class="sxs-lookup"><span data-stu-id="d6f29-142">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="d6f29-143">Type **y** to continue.</span><span class="sxs-lookup"><span data-stu-id="d6f29-143">Type **y** to continue.</span></span> <span data-ttu-id="d6f29-144">You can add the **-force** parameter to avoid this confirmation step.</span><span class="sxs-lookup"><span data-stu-id="d6f29-144">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="d6f29-145">After the command completes, type **exit**.</span><span class="sxs-lookup"><span data-stu-id="d6f29-145">After the command completes, type **exit**.</span></span> <span data-ttu-id="d6f29-146">This step closes the SSH client.</span><span class="sxs-lookup"><span data-stu-id="d6f29-146">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="d6f29-147">Step 2: Capture the VM</span><span class="sxs-lookup"><span data-stu-id="d6f29-147">Step 2: Capture the VM</span></span>
<span data-ttu-id="d6f29-148">Use the Azure CLI 2.0 to generalize and capture the VM.</span><span class="sxs-lookup"><span data-stu-id="d6f29-148">Use the Azure CLI 2.0 to generalize and capture the VM.</span></span> <span data-ttu-id="d6f29-149">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="d6f29-149">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d6f29-150">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d6f29-150">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="d6f29-151">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="d6f29-151">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="d6f29-152">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d6f29-152">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="d6f29-153">Generalize the VM with [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="d6f29-153">Generalize the VM with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="d6f29-154">The following example generalizes the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d6f29-154">The following example generalizes the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="d6f29-155">Now create an image of the VM resource with [az image create](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="d6f29-155">Now create an image of the VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="d6f29-156">The following example creates an image named `myImage` in the resource group named `myResourceGroup` using the VM resource named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="d6f29-156">The following example creates an image named `myImage` in the resource group named `myResourceGroup` using the VM resource named `myVM`:</span></span>
   
    ```azurecli
    az image create --resource-group myResourceGroup --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d6f29-157">The image is created in the same resource group as your source VM.</span><span class="sxs-lookup"><span data-stu-id="d6f29-157">The image is created in the same resource group as your source VM.</span></span> <span data-ttu-id="d6f29-158">You can create VMs in any resource group within your subscription from this image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-158">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="d6f29-159">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span><span class="sxs-lookup"><span data-stu-id="d6f29-159">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="d6f29-160">Step 3: Create a VM from the captured image</span><span class="sxs-lookup"><span data-stu-id="d6f29-160">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="d6f29-161">Create a VM using the image you created with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d6f29-161">Create a VM using the image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d6f29-162">The following example creates a VM named `myVMDeployed` from the image named `myImage`:</span><span class="sxs-lookup"><span data-stu-id="d6f29-162">The following example creates a VM named `myVMDeployed` from the image named `myImage`:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myVMDeployed --image myImage
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="d6f29-163">With managed disks, you can create VMs from an image in any resource group within your subscription.</span><span class="sxs-lookup"><span data-stu-id="d6f29-163">With managed disks, you can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="d6f29-164">This behavior is a change from unmanaged disks where you could only create VMs in the same storage account as your source VHD.</span><span class="sxs-lookup"><span data-stu-id="d6f29-164">This behavior is a change from unmanaged disks where you could only create VMs in the same storage account as your source VHD.</span></span> <span data-ttu-id="d6f29-165">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-165">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span></span> <span data-ttu-id="d6f29-166">Use [az image list](/cli/azure/image#list) to view a list of images.</span><span class="sxs-lookup"><span data-stu-id="d6f29-166">Use [az image list](/cli/azure/image#list) to view a list of images.</span></span> <span data-ttu-id="d6f29-167">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="d6f29-167">The output is similar to the following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="d6f29-168">The following example uses **az vm create** to create a VM in a different resource group than the source image by specifying the image resource ID:</span><span class="sxs-lookup"><span data-stu-id="d6f29-168">The following example uses **az vm create** to create a VM in a different resource group than the source image by specifying the image resource ID:</span></span>

```azurecli
az vm create --resource-group myOtherResourceGroup --name myOtherVMDeployed 
    --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage"
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub
```


### <a name="verify-the-deployment"></a><span data-ttu-id="d6f29-169">Verify the deployment</span><span class="sxs-lookup"><span data-stu-id="d6f29-169">Verify the deployment</span></span>
<span data-ttu-id="d6f29-170">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span><span class="sxs-lookup"><span data-stu-id="d6f29-170">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="d6f29-171">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="d6f29-171">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM --show-details
```

## <a name="next-steps"></a><span data-ttu-id="d6f29-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6f29-172">Next steps</span></span>
<span data-ttu-id="d6f29-173">You can create multiple VMs from your source VM image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-173">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="d6f29-174">If you need to make changes to your image:</span><span class="sxs-lookup"><span data-stu-id="d6f29-174">If you need to make changes to your image:</span></span> 

- <span data-ttu-id="d6f29-175">Create a VM from your image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-175">Create a VM from your image.</span></span>
- <span data-ttu-id="d6f29-176">Make any updates or configuration changes.</span><span class="sxs-lookup"><span data-stu-id="d6f29-176">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="d6f29-177">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-177">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="d6f29-178">Use this new image for future deployments.</span><span class="sxs-lookup"><span data-stu-id="d6f29-178">Use this new image for future deployments.</span></span> <span data-ttu-id="d6f29-179">If desired, delete the original image.</span><span class="sxs-lookup"><span data-stu-id="d6f29-179">If desired, delete the original image.</span></span>

<span data-ttu-id="d6f29-180">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6f29-180">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
