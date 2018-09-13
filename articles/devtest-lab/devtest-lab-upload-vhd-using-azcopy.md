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
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="c2253-103">Upload VHD file to lab's storage account using AzCopy</span><span class="sxs-lookup"><span data-stu-id="c2253-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="c2253-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c2253-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="c2253-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span><span class="sxs-lookup"><span data-stu-id="c2253-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="c2253-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span><span class="sxs-lookup"><span data-stu-id="c2253-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="c2253-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../storage/storage-about-disks-and-vhds-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c2253-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../storage/storage-about-disks-and-vhds-linux.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="c2253-108">AzCopy is a Windows-only command-line utility.</span><span class="sxs-lookup"><span data-stu-id="c2253-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="c2253-109">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="c2253-109">Step-by-step instructions</span></span>

<span data-ttu-id="c2253-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="c2253-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="c2253-111">Get the name of the lab's storage account using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="c2253-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="c2253-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c2253-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="c2253-113">Select **More services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="c2253-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="c2253-114">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="c2253-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="c2253-115">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c2253-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="c2253-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="c2253-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="c2253-117">On the **Custom images** blade, Select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="c2253-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="c2253-118">On the **Custom image** blade, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="c2253-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="c2253-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c2253-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Upload VHD using PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="c2253-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2253-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="c2253-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span><span class="sxs-lookup"><span data-stu-id="c2253-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="c2253-123">Make note of the full URI as it is used in later steps.</span><span class="sxs-lookup"><span data-stu-id="c2253-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="c2253-124">Upload the VHD file using AzCopy:</span><span class="sxs-lookup"><span data-stu-id="c2253-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="c2253-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="c2253-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="c2253-126">Open a command window and navigate to the AzCopy installation directory.</span><span class="sxs-lookup"><span data-stu-id="c2253-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="c2253-127">Optionally, you can add the AzCopy installation location to your system path.</span><span class="sxs-lookup"><span data-stu-id="c2253-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="c2253-128">By default, AzCopy is installed to the following directory:</span><span class="sxs-lookup"><span data-stu-id="c2253-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="c2253-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span><span class="sxs-lookup"><span data-stu-id="c2253-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="c2253-130">The *vhdFileName* value needs to be in quotes.</span><span class="sxs-lookup"><span data-stu-id="c2253-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="c2253-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span><span class="sxs-lookup"><span data-stu-id="c2253-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="c2253-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2253-132">Next steps</span></span>

- [<span data-ttu-id="c2253-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c2253-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="c2253-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2253-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
