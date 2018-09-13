---
title: Upload VHD file to Azure DevTest Labs using PowerShell | Microsoft Docs
description: Upload VHD file to lab's storage account using PowerShell
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
ms.openlocfilehash: fb9847f42466b613350d44614369d58120b24f27
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555171"
---
# <a name="upload-vhd-file-to-labs-storage-account-using-powershell"></a><span data-ttu-id="3c20a-103">Upload VHD file to lab's storage account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c20a-103">Upload VHD file to lab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="3c20a-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3c20a-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="3c20a-105">The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account.</span><span class="sxs-lookup"><span data-stu-id="3c20a-105">The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="3c20a-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span><span class="sxs-lookup"><span data-stu-id="3c20a-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="3c20a-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../storage/storage-about-disks-and-vhds-linux.md)</span><span class="sxs-lookup"><span data-stu-id="3c20a-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../storage/storage-about-disks-and-vhds-linux.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="3c20a-108">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="3c20a-108">Step-by-step instructions</span></span>

<span data-ttu-id="3c20a-109">The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c20a-109">The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="3c20a-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3c20a-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="3c20a-111">Select **More services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="3c20a-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="3c20a-112">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="3c20a-112">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="3c20a-113">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3c20a-113">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="3c20a-114">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="3c20a-114">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="3c20a-115">On the **Custom images** blade, Select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="3c20a-115">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="3c20a-116">On the **Custom image** blade, select **VHD**.</span><span class="sxs-lookup"><span data-stu-id="3c20a-116">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="3c20a-117">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3c20a-117">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Upload VHD using PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="3c20a-119">On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.</span><span class="sxs-lookup"><span data-stu-id="3c20a-119">On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.</span></span>

1. <span data-ttu-id="3c20a-120">Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.</span><span class="sxs-lookup"><span data-stu-id="3c20a-120">Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.</span></span>

1. <span data-ttu-id="3c20a-121">At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).</span><span class="sxs-lookup"><span data-stu-id="3c20a-121">At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="3c20a-122">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span><span class="sxs-lookup"><span data-stu-id="3c20a-122">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c20a-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c20a-123">Next steps</span></span>

- [<span data-ttu-id="3c20a-124">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3c20a-124">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="3c20a-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c20a-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

