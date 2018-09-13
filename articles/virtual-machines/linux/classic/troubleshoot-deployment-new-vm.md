---
title: Troubleshoot Linux VM deployment-Classic | Microsoft Docs
description: Troubleshoot classic deployment issues when you create a new Linux virtual machine in Azure
services: virtual-machines-linux
documentationcenter: ''
author: JiangChen79
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: 35b8ae033425e16fb53cc3127f300e1fb919a2f2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550932"
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For the Resource Manager version of this article, see [here](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Collect audit logs
To start troubleshooting, collect the audit logs to identify the error associated with the issue.

In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors. Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.

**Upload Errors:**

**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.

**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.

**Resolution:**

To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized). To upload as generalized, remember to run -deprovision first. See [Create and Upload a Virtual Hard Disk that Contains the Linux Operating System](create-upload-vhd.md) for more information.

**Capture Errors:**

**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.

**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password. Also, the original VM is not usable because it is marked as specialized.

**Resolution:**

To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md) with the same setting as that for the OS (generalized/specialized).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Issue: Custom/ gallery/ marketplace image; allocation failure
This error arises in situations when the new VM request is sent to a cluster that either does not have available free space to accommodate the request, or cannot support the VM size being requested. It is not possible to mix different series of VMs in the same cloud service. So if you want to create a new VM of a different size than what your cloud service can support, the compute request will fail.

Depending on the constraints of the cloud service you use to create the new VM, you might encounter an error caused by one of two situations.

**Cause 1:** The cloud service is pinned to a specific cluster, or it is linked to an affinity group, and hence pinned to a specific cluster by design. So new compute resource requests in that affinity group are tried in the same cluster where the existing resources are hosted. However, the same cluster may either not support the requested VM size or have insufficient available space, resulting in an allocation error. This is true whether the new resources are created through a new cloud service or through an existing cloud service.

**Resolution 1:**

* Create a new cloud service and associate it with either a region or a region-based virtual network.
* Create a new VM in the new cloud service.
  If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.

> [!IMPORTANT]
> If you were trying to create a new VM in an existing cloud service but couldn’t, and had to create a new cloud service for your new VM, you can choose to consolidate all your VMs in the same cloud service. To do so, delete the VMs in the existing cloud service, and recapture them from their disks in the new cloud service. However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.
> 
> 

**Cause 2:** The cloud service is associated with a virtual network that is linked to an affinity group, so it is pinned to a specific cluster by design. All new compute resource requests in that affinity group are therefore tried in the same cluster where the existing resources are hosted. However, the same cluster may either not support the requested VM size or have insufficient available space, resulting in an allocation error. This is true whether the new resources are created through a new cloud service or through an existing cloud service.

**Resolution 2:**

* Create a new regional virtual network.
* Create the new VM in the new virtual network.
* [Connect your existing virtual network](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) to the new virtual network. See more about [regional virtual networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Alternatively, you can [migrate your affinity-group-based virtual network to a regional virtual network](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), and then create the new VM.

## <a name="next-steps"></a>Next steps
If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md).
