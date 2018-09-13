---
title: Capture a VM image from generalized Azure VM | Microsoft Docs
description: Learn how to capture a VM image from a generalized Azure VM created in the Resource Manager deployment model
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: afdae4a1-6dfb-47b4-902a-f327f9bfe5b4
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: cynthn
ms.openlocfilehash: 748fbf224026a1a3e5e1c4e8dac8da12c274700c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550540"
---
# <a name="how-to-capture-a-vm-image-from-a-generalized-azure-vm"></a><span data-ttu-id="74d27-103">How to capture a VM image from a generalized Azure VM</span><span class="sxs-lookup"><span data-stu-id="74d27-103">How to capture a VM image from a generalized Azure VM</span></span>
<span data-ttu-id="74d27-104">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM.</span><span class="sxs-lookup"><span data-stu-id="74d27-104">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM.</span></span> <span data-ttu-id="74d27-105">You can then use the image to create another VM.</span><span class="sxs-lookup"><span data-stu-id="74d27-105">You can then use the image to create another VM.</span></span> <span data-ttu-id="74d27-106">The image includes the OS disk and the data disks that are attached to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="74d27-106">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="74d27-107">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span><span class="sxs-lookup"><span data-stu-id="74d27-107">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="74d27-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74d27-108">Prerequisites</span></span>
* <span data-ttu-id="74d27-109">You need to have already [generalized the VM](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74d27-109">You need to have already [generalized the VM](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="74d27-110">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="74d27-110">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="74d27-111">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span><span class="sxs-lookup"><span data-stu-id="74d27-111">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="74d27-112">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md)</span><span class="sxs-lookup"><span data-stu-id="74d27-112">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md)</span></span>
* <span data-ttu-id="74d27-113">You need to have Azure PowerShell version 1.0.x or newer installed.</span><span class="sxs-lookup"><span data-stu-id="74d27-113">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="74d27-114">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for installation steps.</span><span class="sxs-lookup"><span data-stu-id="74d27-114">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for installation steps.</span></span>

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="74d27-115">Log in to Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="74d27-115">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="74d27-116">Open Azure PowerShell and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="74d27-116">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="74d27-117">A pop-up window opens for you to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="74d27-117">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="74d27-118">Get the subscription IDs for your available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="74d27-118">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="74d27-119">Set the correct subscription using the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="74d27-119">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="74d27-120">Deallocate the VM and set the state to generalized</span><span class="sxs-lookup"><span data-stu-id="74d27-120">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="74d27-121">Deallocate the VM resources.</span><span class="sxs-lookup"><span data-stu-id="74d27-121">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="74d27-122">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="74d27-122">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="74d27-123">Set the status of the virtual machine to **Generalized**.</span><span class="sxs-lookup"><span data-stu-id="74d27-123">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="74d27-124">Check the status of the VM.</span><span class="sxs-lookup"><span data-stu-id="74d27-124">Check the status of the VM.</span></span> <span data-ttu-id="74d27-125">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span><span class="sxs-lookup"><span data-stu-id="74d27-125">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="74d27-126">Create the image</span><span class="sxs-lookup"><span data-stu-id="74d27-126">Create the image</span></span>
1. <span data-ttu-id="74d27-127">Copy the virtual machine image to the destination storage container using this command.</span><span class="sxs-lookup"><span data-stu-id="74d27-127">Copy the virtual machine image to the destination storage container using this command.</span></span> <span data-ttu-id="74d27-128">The image is created in the same storage account as the original virtual machine.</span><span class="sxs-lookup"><span data-stu-id="74d27-128">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="74d27-129">The `-Path` parameter saves a copy of the JSON template locally.</span><span class="sxs-lookup"><span data-stu-id="74d27-129">The `-Path` parameter saves a copy of the JSON template locally.</span></span> <span data-ttu-id="74d27-130">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span><span class="sxs-lookup"><span data-stu-id="74d27-130">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="74d27-131">If the container doesn't exist, it is created for you.</span><span class="sxs-lookup"><span data-stu-id="74d27-131">If the container doesn't exist, it is created for you.</span></span>
   
    ```powershell
    Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
        -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
        -Path <C:\local\Filepath\Filename.json>
    ```
   
    <span data-ttu-id="74d27-132">You can get the URL of your image from the JSON file template.</span><span class="sxs-lookup"><span data-stu-id="74d27-132">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="74d27-133">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span><span class="sxs-lookup"><span data-stu-id="74d27-133">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="74d27-134">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="74d27-134">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
    <span data-ttu-id="74d27-135">You can also verify the URI in the portal.</span><span class="sxs-lookup"><span data-stu-id="74d27-135">You can also verify the URI in the portal.</span></span> <span data-ttu-id="74d27-136">The image is copied to a container named **system** in your storage account.</span><span class="sxs-lookup"><span data-stu-id="74d27-136">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="74d27-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="74d27-137">Next steps</span></span>
* <span data-ttu-id="74d27-138">Now you can [create a VM from the image](create-vm-generalized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74d27-138">Now you can [create a VM from the image](create-vm-generalized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

