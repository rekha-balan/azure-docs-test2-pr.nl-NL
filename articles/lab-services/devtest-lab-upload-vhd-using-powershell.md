---
title: Upload VHD file to Azure DevTest Labs using PowerShell | Microsoft Docs
description: Upload VHD file to lab's storage account using PowerShell
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: ea2687c61239e893f46dfa12c5b822a51823e1f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864570"
---
# <a name="upload-vhd-file-to-labs-storage-account-using-powershell"></a>Upload VHD file to lab's storage account using PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines. The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account. Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file. For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Step-by-step instructions

The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell. 

1. Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Select **All services**, and then select **DevTest Labs** from the list.

1. From the list of labs, select the desired lab.  

1. On the lab's blade, select **Configuration**. 

1. On the lab **Configuration** blade, select **Custom images (VHDs)**.

1. On the **Custom images** blade, Select **+Add**. 

1. On the **Custom image** blade, select **VHD**.

1. On the **VHD** blade, select **Upload a VHD using PowerShell**.

    ![Upload VHD using PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.

1. Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.

1. At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).

> [!WARNING] 
> 
> The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.

## <a name="next-steps"></a>Next steps

- [Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal](devtest-lab-create-template.md)
- [Create a custom image in Azure DevTest Labs from a VHD file using PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
