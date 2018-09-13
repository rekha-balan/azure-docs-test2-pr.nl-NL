---
title: Attach a data disk to a Linux VM | Microsoft Docs
description: How to attach new or existing data disk to a Linux VM in the Azure portal using the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 23ef6f16c1e104e559d29790a13e554a36ab8054
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555194"
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a>How to attach a data disk to a Linux VM in the Azure portal
This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal. You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). You can choose to use either Azure Managed Disks or unmanaged disks. Managed disks are handled by the Azure platform and do not require any preparation or location to store them. Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits). For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).

Before you attach disks to your VM, review these tips:

* The size of the virtual machine controls how many data disks you can attach. For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* To use Premium storage, you need a DS-series or GS-series virtual machine. You can use both Premium and Standard disks with these virtual machines. Premium storage is available in certain regions. For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Disks attached to virtual machines are actually .vhd files stored in Azure. For details, see [About disks and VHDs for virtual machines](../../storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-the-virtual-machine"></a>Find the virtual machine
1. Sign in to the [Azure portal](https://portal.azure.com/).
2. On the Hub menu, click **Virtual Machines**.
3. Select the virtual machine from the list.
4. To the Virtual machines blade, in **Essentials**, click **Disks**.
   
    ![Open disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/find-disk-settings.png)

Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Use Azure Managed Disks

### <a name="attach-a-new-disk"></a>Attach a new disk

1. On the **Disks** blade, click **+ Add data disk**.
2. Click the drop-down menu for **Name** and select **Create disk**:

    ![Create Azure managed disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/create-new-md.png)

3. Enter a name for your managed disk. Review the default settings, update as necessary, and then click **Create**.
   
   ![Review disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/create-new-md-settings.png)

4. Click **Save** to create the managed disk and update the VM configuration:

   ![Save new Azure Managed Disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/confirm-create-new-md.png)

5. After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**. As managed disks are a top-level resource, the disk appears at the root of the resource group:

   ![Azure Managed Disk in resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Attach an existing disk
1. On the **Disks** blade, click **+ Add data disk**.
2. Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription. Select the managed disk to attach:

   ![Attach existing Azure Managed Disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/select-existing-md.png)

3. Click **Save** to attach the existing managed disk and update the VM configuration:
   
   ![Save Azure Managed Disk updates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/confirm-attach-existing-md.png)

4. After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.

## <a name="use-unmanaged-disks"></a>Use unmanaged disks

### <a name="attach-a-new-disk"></a>Attach a new disk

1. On the **Disks** blade, click **+ Add data disk**.
2. Review the default settings, update as necessary, and then click **OK**.
   
   ![Review disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/attach-new.png)
3. After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.

### <a name="attach-an-existing-disk"></a>Attach an existing disk
1. On the **Disks** blade, click **+ Add data disk**.
2. Under **Attach existing disk**, click **VHD File**.
   
   ![Attach existing disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/attach-existing.png)
3. Under **Storage accounts**, select the account and container that holds the .vhd file.
   
   ![Find VHD location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/find-storage-container.png)
4. Select the .vhd file.
5. Under **Attach existing disk**, the file you just selected is listed under **VHD File**. Click **OK**.
6. After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.


## <a name="next-steps"></a>Next steps
After the disk is added, you need to prepare it for use. For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).










