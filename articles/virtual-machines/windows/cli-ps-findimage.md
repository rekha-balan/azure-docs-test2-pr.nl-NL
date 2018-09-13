---
title: Navigate and select Windows VM images | Microsoft Docs
description: Learn how to determine the publisher, offer, and SKU for images when creating a Windows virtual machine with the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: bb9c15ded69cbff8bd23d9aa82f5859868540259
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562693"
---
# <a name="navigate-and-select-windows-virtual-machine-images-in-azure-with-powershell"></a><span data-ttu-id="8bd2c-103">Navigate and select Windows virtual machine images in Azure with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd2c-103">Navigate and select Windows virtual machine images in Azure with PowerShell</span></span>
<span data-ttu-id="8bd2c-104">This topic describes how to find VM image publishers, offers, skus, and versions for each location into which you might deploy.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-104">This topic describes how to find VM image publishers, offers, skus, and versions for each location into which you might deploy.</span></span> <span data-ttu-id="8bd2c-105">To give an example, some commonly used Windows VM images are:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-105">To give an example, some commonly used Windows VM images are:</span></span>

## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="8bd2c-106">Table of commonly used Windows images</span><span class="sxs-lookup"><span data-stu-id="8bd2c-106">Table of commonly used Windows images</span></span>
| <span data-ttu-id="8bd2c-107">PublisherName</span><span class="sxs-lookup"><span data-stu-id="8bd2c-107">PublisherName</span></span> | <span data-ttu-id="8bd2c-108">Offer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-108">Offer</span></span> | <span data-ttu-id="8bd2c-109">Sku</span><span class="sxs-lookup"><span data-stu-id="8bd2c-109">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8bd2c-110">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="8bd2c-110">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="8bd2c-111">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="8bd2c-111">DynamicsNAV</span></span> |<span data-ttu-id="8bd2c-112">2015</span><span class="sxs-lookup"><span data-stu-id="8bd2c-112">2015</span></span> |
| <span data-ttu-id="8bd2c-113">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="8bd2c-113">MicrosoftSharePoint</span></span> |<span data-ttu-id="8bd2c-114">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-114">MicrosoftSharePointServer</span></span> |<span data-ttu-id="8bd2c-115">2013</span><span class="sxs-lookup"><span data-stu-id="8bd2c-115">2013</span></span> |
| <span data-ttu-id="8bd2c-116">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-116">MicrosoftSQLServer</span></span> |<span data-ttu-id="8bd2c-117">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="8bd2c-117">SQL2014-WS2012R2</span></span> |<span data-ttu-id="8bd2c-118">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="8bd2c-118">Enterprise-Optimized-for-DW</span></span> |
| <span data-ttu-id="8bd2c-119">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-119">MicrosoftSQLServer</span></span> |<span data-ttu-id="8bd2c-120">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="8bd2c-120">SQL2014-WS2012R2</span></span> |<span data-ttu-id="8bd2c-121">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="8bd2c-121">Enterprise-Optimized-for-OLTP</span></span> |
| <span data-ttu-id="8bd2c-122">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-122">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8bd2c-123">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-123">WindowsServer</span></span> |<span data-ttu-id="8bd2c-124">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="8bd2c-124">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="8bd2c-125">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-125">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8bd2c-126">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-126">WindowsServer</span></span> |<span data-ttu-id="8bd2c-127">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="8bd2c-127">2012-Datacenter</span></span> |
| <span data-ttu-id="8bd2c-128">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-128">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8bd2c-129">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-129">WindowsServer</span></span> |<span data-ttu-id="8bd2c-130">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="8bd2c-130">2008-R2-SP1</span></span> |
| <span data-ttu-id="8bd2c-131">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-131">MicrosoftWindowsServer</span></span> |<span data-ttu-id="8bd2c-132">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-132">WindowsServer</span></span> |<span data-ttu-id="8bd2c-133">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="8bd2c-133">Windows-Server-Technical-Preview</span></span> |
| <span data-ttu-id="8bd2c-134">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="8bd2c-134">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="8bd2c-135">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="8bd2c-135">WindowsServerEssentials</span></span> |<span data-ttu-id="8bd2c-136">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="8bd2c-136">WindowsServerEssentials</span></span> |
| <span data-ttu-id="8bd2c-137">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="8bd2c-137">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="8bd2c-138">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="8bd2c-138">WindowsServerHPCPack</span></span> |<span data-ttu-id="8bd2c-139">2012R2</span><span class="sxs-lookup"><span data-stu-id="8bd2c-139">2012R2</span></span> |

## <a name="find-azure-images-with-powershell"></a><span data-ttu-id="8bd2c-140">Find Azure images with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd2c-140">Find Azure images with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="8bd2c-141">Install and configure the [latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8bd2c-141">Install and configure the [latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8bd2c-142">If you are using Azure PowerShell modules below 1.0, you still use the following commands but you must first `Switch-AzureMode AzureResourceManager`.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-142">If you are using Azure PowerShell modules below 1.0, you still use the following commands but you must first `Switch-AzureMode AzureResourceManager`.</span></span> 
> 
> 

<span data-ttu-id="8bd2c-143">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-143">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span></span>

* <span data-ttu-id="8bd2c-144">Publisher</span><span class="sxs-lookup"><span data-stu-id="8bd2c-144">Publisher</span></span>
* <span data-ttu-id="8bd2c-145">Offer</span><span class="sxs-lookup"><span data-stu-id="8bd2c-145">Offer</span></span>
* <span data-ttu-id="8bd2c-146">SKU</span><span class="sxs-lookup"><span data-stu-id="8bd2c-146">SKU</span></span>

<span data-ttu-id="8bd2c-147">For example, these values are needed for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or with a resource group template file in which you must specify the type of virtual machine to be created.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-147">For example, these values are needed for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or with a resource group template file in which you must specify the type of virtual machine to be created.</span></span>

<span data-ttu-id="8bd2c-148">If you need to determine these values, you can navigate the images to determine these values:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-148">If you need to determine these values, you can navigate the images to determine these values:</span></span>

1. <span data-ttu-id="8bd2c-149">List the image publishers.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-149">List the image publishers.</span></span>
2. <span data-ttu-id="8bd2c-150">For a given publisher, list their offers.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-150">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="8bd2c-151">For a given offer, list their SKUs.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-151">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="8bd2c-152">First, list the publishers with the following commands:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-152">First, list the publishers with the following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="8bd2c-153">Fill in your chosen publisher name and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-153">Fill in your chosen publisher name and run the following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="8bd2c-154">Fill in your chosen offer name and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-154">Fill in your chosen offer name and run the following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="8bd2c-155">From the display of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-155">From the display of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span></span>

<span data-ttu-id="8bd2c-156">The following shows a full example:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-156">The following shows a full example:</span></span>

```powershell
PS C:\> $locName="West US"
PS C:\> Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="8bd2c-157">For the "MicrosoftWindowsServer" publisher:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-157">For the "MicrosoftWindowsServer" publisher:</span></span>

```powershell
PS C:\> $pubName="MicrosoftWindowsServer"
PS C:\> Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer

Offer
-----
WindowsServer
```

<span data-ttu-id="8bd2c-158">For the "WindowsServer" offer:</span><span class="sxs-lookup"><span data-stu-id="8bd2c-158">For the "WindowsServer" offer:</span></span>

```powershell
PS C:\> $offerName="WindowsServer"
PS C:\> Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus

Skus
----
2008-R2-SP1
2012-Datacenter
2012-R2-Datacenter
2016-Nano-Server-Technical-Previe
2016-Technical-Preview-with-Conta
Windows-Server-Technical-Preview
```

<span data-ttu-id="8bd2c-159">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-159">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd2c-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bd2c-160">Next steps</span></span>
<span data-ttu-id="8bd2c-161">Now you can choose precisely the image you want to use.</span><span class="sxs-lookup"><span data-stu-id="8bd2c-161">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="8bd2c-162">To create a virtual machine quickly by using the image information, which you just found, or to use a template with that image information, see [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8bd2c-162">To create a virtual machine quickly by using the image information, which you just found, or to use a template with that image information, see [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>