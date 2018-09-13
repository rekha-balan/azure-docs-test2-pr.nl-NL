---
title: Capture an Azure Linux VM to use as a template | Microsoft Docs
description: Learn how to capture and generalize an image of a Linux-based Azure virtual machine (VM) created with the Azure Resource Manager deployment model.
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
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 82ed205b0be7be346fdf5f4776361c903e193780
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556646"
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="3492e-103">Capture a Linux virtual machine running on Azure</span><span class="sxs-lookup"><span data-stu-id="3492e-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="3492e-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="3492e-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="3492e-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="3492e-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="3492e-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span><span class="sxs-lookup"><span data-stu-id="3492e-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="3492e-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="3492e-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="3492e-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3492e-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="3492e-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="3492e-110">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-110">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="3492e-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span><span class="sxs-lookup"><span data-stu-id="3492e-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="3492e-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3492e-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="3492e-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3492e-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="3492e-115">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="3492e-115">CLI versions to complete the task</span></span>
<span data-ttu-id="3492e-116">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="3492e-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="3492e-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="3492e-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3492e-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="3492e-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3492e-119">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3492e-119">Before you begin</span></span>
<span data-ttu-id="3492e-120">Ensure that you meet the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="3492e-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="3492e-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
  
    <span data-ttu-id="3492e-122">Configure the VM as needed.</span><span class="sxs-lookup"><span data-stu-id="3492e-122">Configure the VM as needed.</span></span> <span data-ttu-id="3492e-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span><span class="sxs-lookup"><span data-stu-id="3492e-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="3492e-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span><span class="sxs-lookup"><span data-stu-id="3492e-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="3492e-125">Step 1: Remove the Azure Linux agent</span><span class="sxs-lookup"><span data-stu-id="3492e-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="3492e-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="3492e-127">This command deletes files and data to make the VM ready for generalizing.</span><span class="sxs-lookup"><span data-stu-id="3492e-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="3492e-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="3492e-129">Connect to your Linux VM using an SSH client.</span><span class="sxs-lookup"><span data-stu-id="3492e-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="3492e-130">In the SSH window, type the following command:</span><span class="sxs-lookup"><span data-stu-id="3492e-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="3492e-131">Only run this command on a VM that you intend to capture as an image.</span><span class="sxs-lookup"><span data-stu-id="3492e-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="3492e-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span><span class="sxs-lookup"><span data-stu-id="3492e-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="3492e-133">Type **y** to continue.</span><span class="sxs-lookup"><span data-stu-id="3492e-133">Type **y** to continue.</span></span> <span data-ttu-id="3492e-134">You can add the **-force** parameter to avoid this confirmation step.</span><span class="sxs-lookup"><span data-stu-id="3492e-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="3492e-135">After the command completes, type **exit**.</span><span class="sxs-lookup"><span data-stu-id="3492e-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="3492e-136">This step closes the SSH client.</span><span class="sxs-lookup"><span data-stu-id="3492e-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="3492e-137">Step 2: Capture the VM</span><span class="sxs-lookup"><span data-stu-id="3492e-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="3492e-138">Use the Azure CLI to generalize and capture the VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="3492e-139">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="3492e-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3492e-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span><span class="sxs-lookup"><span data-stu-id="3492e-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="3492e-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="3492e-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="3492e-142">Make sure you are in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="3492e-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="3492e-143">Shut down the VM that you already deprovisioned by using the following command:</span><span class="sxs-lookup"><span data-stu-id="3492e-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="3492e-144">Generalize the VM with the following command:</span><span class="sxs-lookup"><span data-stu-id="3492e-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="3492e-145">Now run the **azure vm capture** command, which captures the VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="3492e-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="3492e-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="3492e-147">The image VHD files get created by default in the same storage account that the original VM used.</span><span class="sxs-lookup"><span data-stu-id="3492e-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="3492e-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span><span class="sxs-lookup"><span data-stu-id="3492e-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="3492e-149">To find the location of a captured image, open the JSON template in a text editor.</span><span class="sxs-lookup"><span data-stu-id="3492e-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="3492e-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span><span class="sxs-lookup"><span data-stu-id="3492e-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="3492e-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="3492e-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="3492e-152">Step 3: Create a VM from the captured image</span><span class="sxs-lookup"><span data-stu-id="3492e-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="3492e-153">Now use the image with a template to create a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="3492e-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="3492e-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="3492e-155">Create network resources</span><span class="sxs-lookup"><span data-stu-id="3492e-155">Create network resources</span></span>
<span data-ttu-id="3492e-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="3492e-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span><span class="sxs-lookup"><span data-stu-id="3492e-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="3492e-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span><span class="sxs-lookup"><span data-stu-id="3492e-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="3492e-159">Get the Id of the NIC</span><span class="sxs-lookup"><span data-stu-id="3492e-159">Get the Id of the NIC</span></span>
<span data-ttu-id="3492e-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span><span class="sxs-lookup"><span data-stu-id="3492e-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="3492e-161">Obtain it by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3492e-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="3492e-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="3492e-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="3492e-163">Create a VM</span><span class="sxs-lookup"><span data-stu-id="3492e-163">Create a VM</span></span>
<span data-ttu-id="3492e-164">Now run the following command to create your VM from the captured VM image.</span><span class="sxs-lookup"><span data-stu-id="3492e-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="3492e-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span><span class="sxs-lookup"><span data-stu-id="3492e-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="3492e-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span><span class="sxs-lookup"><span data-stu-id="3492e-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="3492e-167">The following sample shows what you see for a successful deployment:</span><span class="sxs-lookup"><span data-stu-id="3492e-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-the-deployment"></a><span data-ttu-id="3492e-168">Verify the deployment</span><span class="sxs-lookup"><span data-stu-id="3492e-168">Verify the deployment</span></span>
<span data-ttu-id="3492e-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="3492e-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3492e-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="3492e-171">The public IP address is listed in the command output.</span><span class="sxs-lookup"><span data-stu-id="3492e-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="3492e-172">By default you connect to the Linux VM by SSH on port 22.</span><span class="sxs-lookup"><span data-stu-id="3492e-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="3492e-173">Create additional VMs</span><span class="sxs-lookup"><span data-stu-id="3492e-173">Create additional VMs</span></span>
<span data-ttu-id="3492e-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="3492e-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="3492e-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span><span class="sxs-lookup"><span data-stu-id="3492e-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="3492e-176">Use the captured template</span><span class="sxs-lookup"><span data-stu-id="3492e-176">Use the captured template</span></span>
<span data-ttu-id="3492e-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span><span class="sxs-lookup"><span data-stu-id="3492e-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="3492e-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span><span class="sxs-lookup"><span data-stu-id="3492e-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="3492e-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span><span class="sxs-lookup"><span data-stu-id="3492e-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="3492e-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="3492e-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="3492e-181">Create a NIC in either the same or a different virtual network.</span><span class="sxs-lookup"><span data-stu-id="3492e-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="3492e-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span><span class="sxs-lookup"><span data-stu-id="3492e-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="3492e-183">Use a quickstart template</span><span class="sxs-lookup"><span data-stu-id="3492e-183">Use a quickstart template</span></span>
<span data-ttu-id="3492e-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span><span class="sxs-lookup"><span data-stu-id="3492e-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="3492e-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="3492e-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="3492e-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span><span class="sxs-lookup"><span data-stu-id="3492e-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="3492e-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="3492e-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="3492e-188">Use the azure vm create command</span><span class="sxs-lookup"><span data-stu-id="3492e-188">Use the azure vm create command</span></span>
<span data-ttu-id="3492e-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span><span class="sxs-lookup"><span data-stu-id="3492e-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="3492e-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span><span class="sxs-lookup"><span data-stu-id="3492e-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="3492e-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="3492e-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span><span class="sxs-lookup"><span data-stu-id="3492e-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="3492e-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span><span class="sxs-lookup"><span data-stu-id="3492e-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="3492e-194">Before running **azure vm create** with the image, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="3492e-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="3492e-195">Create a resource group, or identify an existing resource group for the deployment.</span><span class="sxs-lookup"><span data-stu-id="3492e-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="3492e-196">Create a public IP address resource and a NIC resource for the new VM.</span><span class="sxs-lookup"><span data-stu-id="3492e-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="3492e-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="3492e-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="3492e-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span><span class="sxs-lookup"><span data-stu-id="3492e-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="3492e-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span><span class="sxs-lookup"><span data-stu-id="3492e-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="3492e-200">In this example, a size Standard_A1 VM is created in the East US region.</span><span class="sxs-lookup"><span data-stu-id="3492e-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="3492e-201">For additional command options, run `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="3492e-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3492e-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="3492e-202">Next steps</span></span>
<span data-ttu-id="3492e-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3492e-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

