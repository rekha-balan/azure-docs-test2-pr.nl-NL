---
title: Creating an on-premises virtual machine image for the Azure Marketplace | Microsoft Docs
description: Understand and execute the steps to create an on-premises VM image and deploy to the Azure Marketplace for others to purchase.
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: db8028c5bc57760c00890725bb29a04b9a5a711b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669311"
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a>Develop an on-premises virtual machine image for the Azure Marketplace
We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol. However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.  

For on-premises development, you must download the operating system VHD of the created VM. These steps would take place as part of step 3.3, above.  

## <a name="download-a-vhd-image"></a>Download a VHD image
### <a name="locate-a-blob-url"></a>Locate a blob URL
In order to download the VHD, first locate the blob URL for the operating system disk.

Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):

1. Go to **Browse** > **VMs**, and then select the deployed VM.
2. Under **Configure**, select the **Disks** tile, which opens the Disks blade.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.
4. Copy this blob URL.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Now, delete the deployed VM without deleting the backing disks. You can also stop the VM instead of deleting it. Do not download the operating system VHD when the VM is running.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Download a VHD
After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.  

> [!NOTE]
> At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.  
> 
> 

**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**

1. Sign in to the Azure portal if you have not done so already.
2. Click the **Storage** tab.
3. Select the storage account within which the VHD is stored.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. This displays storage account properties. Select the **Containers** tab.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Select the container in which the VHD is stored. By default, when created from the portal, the VHD is stored in a vhds container.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Select the correct operating system VHD by comparing the URL to the one you saved.
7. Click **Download**.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Download a VHD by using PowerShell
In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a>Upload VHDs to an Azure storage account
If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure. This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.

### <a name="create-a-storage-account-and-container"></a>Create a storage account and container
We recommend that VHDs be uploaded into a storage account in a region in the United States. All VHDs for a single SKU should be placed in a single container within a single storage account.

To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.  

**Create a storage account from the Microsoft Azure portal**

1. Click **New**.
2. Select **Storage**.
3. Fill in the storage account name, and then select a location.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Click **Create**.
5. The blade for the created storage account should be open. If not, select **Browse** > **Storage Accounts**. On the Storage account blade, select the storage account created.
6. Select **Containers**.
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. On the Containers blade, select **Add**, and then enter a container name and the container permissions. Select **Private** for container permissions.

> [!TIP]
> We recommend that you create one container per SKU that you are planning to publish.
> 
> 

  ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Create a storage account by using PowerShell
Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Those commands assume that the current storage account context has already been set in PowerShell.   Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a>Create a storage account by using the command-line tool for Mac and Linux
> From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Create a container as follows.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Upload a VHD
After the storage account and container are created, you can upload your prepared VHDs. You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.

### <a name="upload-a-vhd-via-powershell"></a>Upload a VHD via PowerShell
Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a>Upload a VHD by using the command-line tool for Mac and Linux
With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD>

## <a name="see-also"></a>See also
* [Creating a virtual machine image for the Marketplace](marketplace-publishing-vm-image-creation.md)
* [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md)











