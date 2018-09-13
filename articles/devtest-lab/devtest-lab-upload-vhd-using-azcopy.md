---
title: Upload VHD file to Azure DevTest Labs using AzCopy | Microsoft Docs
description: Upload VHD file to lab's storage account using AzCopy
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
ms.openlocfilehash: 65e355e48af3b1b5a69405a9f4342bc7b242fd8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552108"
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a>Upload VHD file to lab's storage account using AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines. The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account. Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file. For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../storage/storage-about-disks-and-vhds-linux.md)

> [!NOTE] 
>  
> AzCopy is a Windows-only command-line utility.

## <a name="step-by-step-instructions"></a>Step-by-step instructions

The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy). 

1. Get the name of the lab's storage account using the Azure portal:

1. Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Select **More services**, and then select **DevTest Labs** from the list.

1. From the list of labs, select the desired lab.  

1. On the lab's blade, select **Configuration**. 

1. On the lab **Configuration** blade, select **Custom images (VHDs)**.

1. On the **Custom images** blade, Select **+Add**. 

1. On the **Custom image** blade, select **VHD**.

1. On the **VHD** blade, select **Upload a VHD using PowerShell**.

    ![Upload VHD using PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet. The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Make note of the full URI as it is used in later steps.

1. Upload the VHD file using AzCopy:
 
1. [Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).

1. Open a command window and navigate to the AzCopy installation directory. Optionally, you can add the AzCopy installation location to your system path. By default, AzCopy is installed to the following directory:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Using the storage account key and blob container URI, run the following command at the command prompt. The *vhdFileName* value needs to be in quotes. The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Next steps

- [Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal](devtest-lab-create-template.md)
- [Create a custom image in Azure DevTest Labs from a VHD file using PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)