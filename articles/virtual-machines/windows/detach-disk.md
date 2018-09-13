---
title: Detach a data disk from a Windows VM - Azure| Microsoft Docs
description: Learn to detach a data disk from a virtual machine in Azure using the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 0c7dc17935b720a55b998c5267fd35dfd3233fd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549484"
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a>How to detach a data disk from a Windows virtual machine
When you no longer need a data disk that's attached to a virtual machine, you can easily detach it. This removes the disk from the virtual machine, but doesn't remove it from storage. 

> [!WARNING]
> If you detach a disk it is not automatically deleted. If you have subscribed to Premium storage, you will continue to incur storage charges for the disk. For more information refer to [Pricing and Billing when using Premium Storage](../../storage/storage-premium-storage.md#pricing-and-billing). 
> 
> 

If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.  

## <a name="detach-a-data-disk-using-the-portal"></a>Detach a data disk using the portal
1. In the portal hub, select **Virtual Machines**.
2. Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.
3. In the virtual machine blade, select **Disks**.
4. At the top of the **Disks** blade, select **Edit**.
5. In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/detach-disk/detach.png) detach button.
5. After the disk has been removed, click Save on the top of the blade.
6. In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.



The disk remains in storage but is no longer attached to a virtual machine.

## <a name="detach-a-data-disk-using-powershell"></a>Detach a data disk using PowerShell
In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet. The command stores the virtual machine in the **$VirtualMachine** variable. 

The second command removes the data disk named DataDisk3 from the virtual machine. 

The final command updates the state of the virtual machine to complete the process of removing the data disk.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" 
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

For more information, see [Remove-AzureRmVMDataDisk](/powershell/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Next steps
If you want to reuse the data disk, you can just [attach it to another VM](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


