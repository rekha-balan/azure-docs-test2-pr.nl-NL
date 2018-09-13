---
title: VM restarting or resizing issues in Azure | Microsoft Docs
description: Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: ''
author: Deland-Han
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b648b000e82b540c611658f369b15d6fe7f52121
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564059"
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a>Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure
When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure. This error results when the cluster or region either does not have resources available or cannot support the requested VM size.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Collect activity logs
To start troubleshooting, collect the activity logs to identify the error associated with the issue. The following links contain detailed information on the process:

[View deployment operations](../../azure-resource-manager/resource-manager-deployment-operations.md)

[View activity logs to manage Azure resources](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Issue: Error when starting a stopped VM
You try to start a stopped VM but get an allocation failure.

### <a name="cause"></a>Cause
The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service. However, the cluster does not have free space available to fulfill the request.

### <a name="resolution"></a>Resolution
* Stop all the VMs in the availability set, and then restart each VM.
  
  1. Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.
  2. After all the VMs stop, select each of the stopped VMs and click Start.
* Retry the restart request at a later time.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Issue: Error when resizing an existing VM
You try to resize an existing VM but get an allocation failure.

### <a name="cause"></a>Cause
The request to resize the VM has to be attempted at the original cluster that hosts the cloud service. However, the cluster does not support the requested VM size.

### <a name="resolution"></a>Resolution
* Retry the request using a smaller VM size.
* If the size of the requested VM cannot be changed：
  
  1. Stop all the VMs in the availability set.
     
     * Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.
  2. After all the VMs stop, resize the desired VM to a larger size.
  3. Select the resized VM and click **Start**, and then start each of the stopped VMs.

## <a name="next-steps"></a>Next steps
If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

