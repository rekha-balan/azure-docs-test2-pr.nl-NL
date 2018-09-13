---
title: About images for Windows virtual machines | Microsoft Docs
description: Learn about how images are used with Windows virtual machines in Azure.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: d421cee0becabdf81d865036d0c98b12b077152b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554168"
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="2ebf8-103">About images for Windows virtual machines</span><span class="sxs-lookup"><span data-stu-id="2ebf8-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2ebf8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2ebf8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2ebf8-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="2ebf8-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="2ebf8-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2ebf8-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="2ebf8-108">Working with images</span><span class="sxs-lookup"><span data-stu-id="2ebf8-108">Working with images</span></span>

<span data-ttu-id="2ebf8-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="2ebf8-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span></span> <span data-ttu-id="2ebf8-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span></span>

<span data-ttu-id="2ebf8-112">Here are some examples that use the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-112">Here are some examples that use the Azure PowerShell module.</span></span>

* <span data-ttu-id="2ebf8-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="2ebf8-114">The resulting list could be large.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-114">The resulting list could be large.</span></span> <span data-ttu-id="2ebf8-115">The next examples show how to get a shorter list.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-115">The next examples show how to get a shorter list.</span></span>
* <span data-ttu-id="2ebf8-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="2ebf8-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="2ebf8-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="2ebf8-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span></span> <span data-ttu-id="2ebf8-119">This example also filters the output to only the label and image name.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-119">This example also filters the output to only the label and image name.</span></span>
* <span data-ttu-id="2ebf8-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="2ebf8-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="2ebf8-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="2ebf8-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="2ebf8-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span></span> <span data-ttu-id="2ebf8-123">If you don’t use the parameter, the cmdlet creates an OS image.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-123">If you don’t use the parameter, the cmdlet creates an OS image.</span></span> <span data-ttu-id="2ebf8-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span><span class="sxs-lookup"><span data-stu-id="2ebf8-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="2ebf8-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="2ebf8-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ebf8-126">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2ebf8-126">Next Steps</span></span>
<span data-ttu-id="2ebf8-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2ebf8-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span></span>
