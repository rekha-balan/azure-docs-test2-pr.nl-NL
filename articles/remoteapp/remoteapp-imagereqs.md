---
title: Azure RemoteApp image requirements | Microsoft Docs
description: Learn about the requirements for creating images to be used with Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554064"
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="d10cc-103">Requirements for Azure RemoteApp images</span><span class="sxs-lookup"><span data-stu-id="d10cc-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d10cc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="d10cc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d10cc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="d10cc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d10cc-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span><span class="sxs-lookup"><span data-stu-id="d10cc-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="d10cc-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="d10cc-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="d10cc-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span><span class="sxs-lookup"><span data-stu-id="d10cc-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="d10cc-109">[Check it out](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="d10cc-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="d10cc-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span><span class="sxs-lookup"><span data-stu-id="d10cc-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="d10cc-111">Custom applications don’t store data locally on the image.</span><span class="sxs-lookup"><span data-stu-id="d10cc-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="d10cc-112">These images are stateless and should only contain applications.</span><span class="sxs-lookup"><span data-stu-id="d10cc-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="d10cc-113">The image does not contain data that can be lost.</span><span class="sxs-lookup"><span data-stu-id="d10cc-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="d10cc-114">The image size should be a multiple of MBs.</span><span class="sxs-lookup"><span data-stu-id="d10cc-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="d10cc-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span><span class="sxs-lookup"><span data-stu-id="d10cc-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="d10cc-116">The image size must be 127 GB or smaller.</span><span class="sxs-lookup"><span data-stu-id="d10cc-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="d10cc-117">It must be on a VHD file (VHDX files are not currently supported).</span><span class="sxs-lookup"><span data-stu-id="d10cc-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="d10cc-118">The VHD must not be a generation 2 virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d10cc-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="d10cc-119">The VHD can be either fixed-size or dynamically expanding.</span><span class="sxs-lookup"><span data-stu-id="d10cc-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="d10cc-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span><span class="sxs-lookup"><span data-stu-id="d10cc-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="d10cc-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span><span class="sxs-lookup"><span data-stu-id="d10cc-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="d10cc-122">The GUID partition table (GPT) partition style is not supported.</span><span class="sxs-lookup"><span data-stu-id="d10cc-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="d10cc-123">The VHD must contain a single installation of Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d10cc-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="d10cc-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span><span class="sxs-lookup"><span data-stu-id="d10cc-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="d10cc-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span><span class="sxs-lookup"><span data-stu-id="d10cc-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="d10cc-126">The Remote Desktop Connection Broker role must *not* be installed.</span><span class="sxs-lookup"><span data-stu-id="d10cc-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="d10cc-127">The Encrypting File System (EFS) must be disabled.</span><span class="sxs-lookup"><span data-stu-id="d10cc-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="d10cc-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span><span class="sxs-lookup"><span data-stu-id="d10cc-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="d10cc-129">Uploading your VHD from a snapshot chain is not supported.</span><span class="sxs-lookup"><span data-stu-id="d10cc-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="d10cc-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d10cc-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

