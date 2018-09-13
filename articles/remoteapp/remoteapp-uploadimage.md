---
title: Upload a custom image for Azure RemoteApp | Microsoft Docs
description: Learn how to upload a custom image for Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: dcf897cfb03316312613a641f1758cd4636d06b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564484"
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="7b4e9-103">Upload a custom image for Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7b4e9-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7b4e9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7b4e9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7b4e9-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span></span> <span data-ttu-id="7b4e9-107">Use these steps.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7b4e9-108">Before you start</span><span class="sxs-lookup"><span data-stu-id="7b4e9-108">Before you start</span></span>
1. <span data-ttu-id="7b4e9-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="7b4e9-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="7b4e9-110">Install the [Azure PowerShell module](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="7b4e9-110">Install the [Azure PowerShell module](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="step-by-step-on-how-to-upload-custom-image"></a><span data-ttu-id="7b4e9-111">Step by step on how to upload custom image</span><span class="sxs-lookup"><span data-stu-id="7b4e9-111">Step by step on how to upload custom image</span></span>
1. <span data-ttu-id="7b4e9-112">Open Azure Management Portal and navigate to the RemoteApp page.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-112">Open Azure Management Portal and navigate to the RemoteApp page.</span></span>
2. <span data-ttu-id="7b4e9-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span></span>
3. <span data-ttu-id="7b4e9-114">Enter a friendly name for your image and specify the storage account location.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-114">Enter a friendly name for your image and specify the storage account location.</span></span> <span data-ttu-id="7b4e9-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span></span>
4. <span data-ttu-id="7b4e9-116">When prompted, download the script to your local PC.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-116">When prompted, download the script to your local PC.</span></span>
5. <span data-ttu-id="7b4e9-117">Copy the command parameters in the text box to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-117">Copy the command parameters in the text box to your clipboard.</span></span>
6. <span data-ttu-id="7b4e9-118">Open an elevated Windows PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="7b4e9-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span></span>
8. <span data-ttu-id="7b4e9-120">Paste the copied command and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-120">Paste the copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="7b4e9-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span><span class="sxs-lookup"><span data-stu-id="7b4e9-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span></span>
9. <span data-ttu-id="7b4e9-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span></span> <span data-ttu-id="7b4e9-123">To resume an upload, run the script again using the same command line.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-123">To resume an upload, run the script again using the same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="7b4e9-124">Never modify the upload script.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-124">Never modify the upload script.</span></span> <span data-ttu-id="7b4e9-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="7b4e9-126">Common problems</span><span class="sxs-lookup"><span data-stu-id="7b4e9-126">Common problems</span></span>
* <span data-ttu-id="7b4e9-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="7b4e9-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span></span>
* <span data-ttu-id="7b4e9-129">Never alter the script, validations are there for your convenience.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-129">Never alter the script, validations are there for your convenience.</span></span>
* <span data-ttu-id="7b4e9-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span></span> <span data-ttu-id="7b4e9-131">There might be some Windows process that is preventing upload.</span><span class="sxs-lookup"><span data-stu-id="7b4e9-131">There might be some Windows process that is preventing upload.</span></span>  

