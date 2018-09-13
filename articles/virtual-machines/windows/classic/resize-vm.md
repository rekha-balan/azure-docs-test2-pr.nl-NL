---
title: Resize a Windows VM in the classic deployment model - Azure | Microsoft Docs
description: Resize a Windows virtual machine created in the classic deployment model, using Azure Powershell.
services: virtual-machines-windows
documentationcenter: ''
author: Drewm3
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 35e0807f95490660ef40fd401007f4c0d482c7b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551464"
---
# <a name="resize-a-windows-vm-created-in-the-classic-deployment-model"></a><span data-ttu-id="c2063-103">Resize a Windows VM created in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="c2063-103">Resize a Windows VM created in the classic deployment model</span></span>
<span data-ttu-id="c2063-104">This article shows you how to resize a Windows VM, created in the classic deployment model using Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="c2063-104">This article shows you how to resize a Windows VM, created in the classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="c2063-105">When considering the ability to resize a VM, there are two concepts which control the range of sizes available to resize the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c2063-105">When considering the ability to resize a VM, there are two concepts which control the range of sizes available to resize the virtual machine.</span></span> <span data-ttu-id="c2063-106">The first concept is the region in which your VM is deployed.</span><span class="sxs-lookup"><span data-stu-id="c2063-106">The first concept is the region in which your VM is deployed.</span></span> <span data-ttu-id="c2063-107">The list of VM sizes available in region is under the Services tab of the Azure Regions web page.</span><span class="sxs-lookup"><span data-stu-id="c2063-107">The list of VM sizes available in region is under the Services tab of the Azure Regions web page.</span></span> <span data-ttu-id="c2063-108">The second concept is the physical hardware currently hosting your VM.</span><span class="sxs-lookup"><span data-stu-id="c2063-108">The second concept is the physical hardware currently hosting your VM.</span></span> <span data-ttu-id="c2063-109">The physical servers hosting VMs are grouped together in clusters of common physical hardware.</span><span class="sxs-lookup"><span data-stu-id="c2063-109">The physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="c2063-110">The method of changing a VM size differs depending on if the desired new VM size is supported by the hardware cluster currently hosting the VM.</span><span class="sxs-lookup"><span data-stu-id="c2063-110">The method of changing a VM size differs depending on if the desired new VM size is supported by the hardware cluster currently hosting the VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c2063-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c2063-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c2063-112">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="c2063-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c2063-113">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="c2063-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c2063-114">You can also [resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2063-114">You can also [resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="c2063-115">Add your account</span><span class="sxs-lookup"><span data-stu-id="c2063-115">Add your account</span></span>
<span data-ttu-id="c2063-116">You must configure Azure PowerShell to work with classic Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c2063-116">You must configure Azure PowerShell to work with classic Azure resources.</span></span> <span data-ttu-id="c2063-117">Follow the steps below to configure Azure PowerShell to manage classic resources.</span><span class="sxs-lookup"><span data-stu-id="c2063-117">Follow the steps below to configure Azure PowerShell to manage classic resources.</span></span>

1. <span data-ttu-id="c2063-118">At the PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c2063-118">At the PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="c2063-119">Type in the email address associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="c2063-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="c2063-120">Type in the password for your account.</span><span class="sxs-lookup"><span data-stu-id="c2063-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="c2063-121">Click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="c2063-121">Click **Sign in**.</span></span> 

## <a name="resize-in-the-same-hardware-cluster"></a><span data-ttu-id="c2063-122">Resize in the same hardware cluster</span><span class="sxs-lookup"><span data-stu-id="c2063-122">Resize in the same hardware cluster</span></span>
<span data-ttu-id="c2063-123">To resize a VM to a size available in the hardware cluster hosting the VM, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="c2063-123">To resize a VM to a size available in the hardware cluster hosting the VM, perform the following steps.</span></span>

1. <span data-ttu-id="c2063-124">Run the following PowerShell command to list the VM sizes available in the hardware cluster hosting the cloud service which contains the VM.</span><span class="sxs-lookup"><span data-stu-id="c2063-124">Run the following PowerShell command to list the VM sizes available in the hardware cluster hosting the cloud service which contains the VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="c2063-125">Run the following commands to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="c2063-125">Run the following commands to resize the VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="c2063-126">Resize on a new hardware cluster</span><span class="sxs-lookup"><span data-stu-id="c2063-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="c2063-127">To resize a VM to a size not available in the hardware cluster hosting the VM, the cloud service and all VMs in the cloud service must be recreated.</span><span class="sxs-lookup"><span data-stu-id="c2063-127">To resize a VM to a size not available in the hardware cluster hosting the VM, the cloud service and all VMs in the cloud service must be recreated.</span></span> <span data-ttu-id="c2063-128">Each cloud service is hosted on a single hardware cluster so all VMs in the cloud service must be a size that is supported on a hardware cluster.</span><span class="sxs-lookup"><span data-stu-id="c2063-128">Each cloud service is hosted on a single hardware cluster so all VMs in the cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="c2063-129">The following steps will describe how to resize a VM by deleting and then recreating the cloud service.</span><span class="sxs-lookup"><span data-stu-id="c2063-129">The following steps will describe how to resize a VM by deleting and then recreating the cloud service.</span></span>

1. <span data-ttu-id="c2063-130">Run the following PowerShell command to list the VM sizes available in the region.</span><span class="sxs-lookup"><span data-stu-id="c2063-130">Run the following PowerShell command to list the VM sizes available in the region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="c2063-131">Make note of all configuration settings for each VM in the cloud service which contains the VM to be resized.</span><span class="sxs-lookup"><span data-stu-id="c2063-131">Make note of all configuration settings for each VM in the cloud service which contains the VM to be resized.</span></span> 
3. <span data-ttu-id="c2063-132">Delete all VMs in the cloud service selecting the option to retain the disks for each VM.</span><span class="sxs-lookup"><span data-stu-id="c2063-132">Delete all VMs in the cloud service selecting the option to retain the disks for each VM.</span></span>
4. <span data-ttu-id="c2063-133">Recreate the VM to be resized using the desired VM size.</span><span class="sxs-lookup"><span data-stu-id="c2063-133">Recreate the VM to be resized using the desired VM size.</span></span>
5. <span data-ttu-id="c2063-134">Recreate all other VMs which were in the cloud service using a VM size available in the hardware cluster now hosting the cloud service.</span><span class="sxs-lookup"><span data-stu-id="c2063-134">Recreate all other VMs which were in the cloud service using a VM size available in the hardware cluster now hosting the cloud service.</span></span>

<span data-ttu-id="c2063-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="c2063-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c2063-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2063-136">Next steps</span></span>
* <span data-ttu-id="c2063-137">[Resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2063-137">[Resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

