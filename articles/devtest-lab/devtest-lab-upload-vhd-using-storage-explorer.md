---
title: Upload VHD file to Azure DevTest Labs using Microsoft Azure Storage Explorer | Microsoft Docs
description: Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: efa97577bc1b97a8950786d909442901a1970fdd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551983"
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a>Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines. This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account. Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file. For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../storage/storage-about-disks-and-vhds-linux.md)

## <a name="step-by-step-instructions"></a>Step-by-step instructions

The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).

1. Get the name of the lab's storage account using the Azure portal:

    1. Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Select **More services**, and then select **DevTest Labs** from the list.
    
    1. From the list of labs, select the desired lab.  
    
    1. On the lab's blade, select **Configuration**. 
    
    1. On the lab **Configuration** blade, select **Custom images (VHDs)**.
    
    1. On the **Custom images** blade, Select **+Add**. 
    
    1. On the **Custom image** blade, select **VHD**.
    
    1. On the **VHD** blade, select **Upload a VHD using PowerShell**.
    
        ![Upload VHD using PowerShell][0]
    
    1. The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet. The first parameter (*Destination*) contains the storage account name for the lab in the following format:
    
        https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/... 

    1. Make note of the storage account name as it is used in later steps.
    
1. Connect to an Azure subscription account using Storage Explorer.

    > [!TIP] 
    > 
    > Storage Explorer supports several connection options. This section illustrates connecting to a storage account associated with your Azure subscription. To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Open Storage Explorer.
    
    1. In Storage Explorer, select **Azure Account settings**. 
    
        ![Azure account settings][1]
    
    1. The left pane displays the Microsoft accounts you've logged in to. To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.
    
        ![Add an account][2]
    
    1. Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account. Select the Azure subscriptions with which you want to work, and then select **Apply**. (Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)
    
        ![Select Azure subscriptions][3]
    
    1. The left pane displays the storage accounts associated with the selected Azure subscriptions.
    
        ![Selected Azure subscriptions][4]

1. Locate the lab's storage account:

    1. In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.
    
    1. Under the subscription's node, expand **Storage Accounts**.

    1. Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.
    
    1. Expand the **Blob Containers** node.
    
    1. Select the uploads blob container to display its contents in the right pane.
        
        ![Upload directory][5]

1. Upload the VHD file using Storage Explorer:

    1. In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account. On the blob editor toolbar, select **Upload** 
        
        ![Upload button][6]
    
    1. From the **Upload** drop-down menu, select **Upload files...**.
    
    1. On the **Upload files** dialog, select the ellipsis.
        
        ![Select file][8]  

    1. On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.
    
    1. When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.
    
    1. Select **Upload**.

        ![Select file][9]  
    
    1. The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload). The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed. 

        ![Upload-file status][10]  

## <a name="next-steps"></a>Next steps

- [Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal](devtest-lab-create-template.md)
- [Create a custom image in Azure DevTest Labs from a VHD file using PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png










