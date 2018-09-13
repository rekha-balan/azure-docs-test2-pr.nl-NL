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
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Manage your virtual machines by using Azure PowerShell
> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets. This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.

> [!NOTE]
> If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).
> 
> 

## <a name="how-to-use-the-example-commands"></a>How to use the example commands
You'll need to replace some of the text in the commands with text that's appropriate for your environment. The < and > symbols indicate text you need to replace. When you replace the text, remove the symbols but leave the quote marks in place.

## <a name="get-a-vm"></a>Get a VM
This is a basic task you'll use often. Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.

To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

To store the output in a $vm variable, run:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a>Log on to a Windows-based VM
Run these commands:

> [!NOTE]
> You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch
> 
> 

## <a name="stop-a-vm"></a>Stop a VM
Run this command:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service. <br><br> If you use the StayProvisioned parameter, you'll still be billed for the VM.
> 
> 

## <a name="start-a-vm"></a>Start a VM
Run this command:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Attach a data disk
This task requires a few steps. First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object. Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.

You'll also need to decide whether to attach a new disk or one that contains data. For a new disk, the command creates the .vhd file and attaches it.

To attach a new disk, run this command:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

To attach an existing data disk, run this command:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

To attach data disks from an existing .vhd file in blob storage, run this command:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Create a Windows-based VM
To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md). This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:

* With Active Directory domain membership.
* With additional disks.
* As a member of an existing load-balanced set.
* With a static IP address.

