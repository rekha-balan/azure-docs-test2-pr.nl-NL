---
title: Manage your virtual machines by using Azure PowerShell | Microsoft Docs
description: Learn commands that you can use to automate tasks in managing your virtual machines.
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: 44235e32b7cf5b2be90f6d460ac22d7c0350f894
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540633"
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="9980b-103">Manage your virtual machines by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9980b-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="9980b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9980b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9980b-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="9980b-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9980b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="9980b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9980b-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9980b-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="9980b-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9980b-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9980b-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span><span class="sxs-lookup"><span data-stu-id="9980b-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="9980b-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="9980b-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="9980b-111">How to use the example commands</span><span class="sxs-lookup"><span data-stu-id="9980b-111">How to use the example commands</span></span>
<span data-ttu-id="9980b-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="9980b-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="9980b-113">The < and > symbols indicate text you need to replace.</span><span class="sxs-lookup"><span data-stu-id="9980b-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="9980b-114">When you replace the text, remove the symbols but leave the quote marks in place.</span><span class="sxs-lookup"><span data-stu-id="9980b-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="9980b-115">Get a VM</span><span class="sxs-lookup"><span data-stu-id="9980b-115">Get a VM</span></span>
<span data-ttu-id="9980b-116">This is a basic task you'll use often.</span><span class="sxs-lookup"><span data-stu-id="9980b-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="9980b-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span><span class="sxs-lookup"><span data-stu-id="9980b-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="9980b-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span><span class="sxs-lookup"><span data-stu-id="9980b-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="9980b-119">To store the output in a $vm variable, run:</span><span class="sxs-lookup"><span data-stu-id="9980b-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="9980b-120">Log on to a Windows-based VM</span><span class="sxs-lookup"><span data-stu-id="9980b-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="9980b-121">Run these commands:</span><span class="sxs-lookup"><span data-stu-id="9980b-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="9980b-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span><span class="sxs-lookup"><span data-stu-id="9980b-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="9980b-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span><span class="sxs-lookup"><span data-stu-id="9980b-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="9980b-124">Stop a VM</span><span class="sxs-lookup"><span data-stu-id="9980b-124">Stop a VM</span></span>
<span data-ttu-id="9980b-125">Run this command:</span><span class="sxs-lookup"><span data-stu-id="9980b-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="9980b-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span><span class="sxs-lookup"><span data-stu-id="9980b-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="9980b-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span><span class="sxs-lookup"><span data-stu-id="9980b-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="9980b-128">Start a VM</span><span class="sxs-lookup"><span data-stu-id="9980b-128">Start a VM</span></span>
<span data-ttu-id="9980b-129">Run this command:</span><span class="sxs-lookup"><span data-stu-id="9980b-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="9980b-130">Attach a data disk</span><span class="sxs-lookup"><span data-stu-id="9980b-130">Attach a data disk</span></span>
<span data-ttu-id="9980b-131">This task requires a few steps.</span><span class="sxs-lookup"><span data-stu-id="9980b-131">This task requires a few steps.</span></span> <span data-ttu-id="9980b-132">First, you use the \*\*\*\*Add-AzureDataDisk\*\*\*\* cmdlet to add the disk to the $vm object.</span><span class="sxs-lookup"><span data-stu-id="9980b-132">First, you use the \*\*\*\*Add-AzureDataDisk\*\*\*\* cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="9980b-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span><span class="sxs-lookup"><span data-stu-id="9980b-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="9980b-134">You'll also need to decide whether to attach a new disk or one that contains data.</span><span class="sxs-lookup"><span data-stu-id="9980b-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="9980b-135">For a new disk, the command creates the .vhd file and attaches it.</span><span class="sxs-lookup"><span data-stu-id="9980b-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="9980b-136">To attach a new disk, run this command:</span><span class="sxs-lookup"><span data-stu-id="9980b-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="9980b-137">To attach an existing data disk, run this command:</span><span class="sxs-lookup"><span data-stu-id="9980b-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="9980b-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span><span class="sxs-lookup"><span data-stu-id="9980b-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="9980b-139">Create a Windows-based VM</span><span class="sxs-lookup"><span data-stu-id="9980b-139">Create a Windows-based VM</span></span>
<span data-ttu-id="9980b-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9980b-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="9980b-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span><span class="sxs-lookup"><span data-stu-id="9980b-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="9980b-142">With Active Directory domain membership.</span><span class="sxs-lookup"><span data-stu-id="9980b-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="9980b-143">With additional disks.</span><span class="sxs-lookup"><span data-stu-id="9980b-143">With additional disks.</span></span>
* <span data-ttu-id="9980b-144">As a member of an existing load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="9980b-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="9980b-145">With a static IP address.</span><span class="sxs-lookup"><span data-stu-id="9980b-145">With a static IP address.</span></span>

