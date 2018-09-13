---
title: Create an Azure RemoteApp image | Microsoft Docs
description: Learn about the options available for creating images for Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f2decec5385ffab59a441cdc28da80371b579df7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661075"
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="85589-103">Create an Azure RemoteApp image</span><span class="sxs-lookup"><span data-stu-id="85589-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="85589-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="85589-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="85589-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="85589-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="85589-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span><span class="sxs-lookup"><span data-stu-id="85589-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="85589-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span><span class="sxs-lookup"><span data-stu-id="85589-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="85589-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span><span class="sxs-lookup"><span data-stu-id="85589-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="85589-109">You have several options for creating or using images.</span><span class="sxs-lookup"><span data-stu-id="85589-109">You have several options for creating or using images.</span></span> <span data-ttu-id="85589-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span><span class="sxs-lookup"><span data-stu-id="85589-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="85589-111">How you get that is where things get interesting.</span><span class="sxs-lookup"><span data-stu-id="85589-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="85589-112">You have the following options when it comes to images:</span><span class="sxs-lookup"><span data-stu-id="85589-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="85589-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="85589-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="85589-114">This is good for line-of-business apps that require custom settings.</span><span class="sxs-lookup"><span data-stu-id="85589-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="85589-115">You can customize the image to work for the app.</span><span class="sxs-lookup"><span data-stu-id="85589-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="85589-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="85589-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="85589-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span><span class="sxs-lookup"><span data-stu-id="85589-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="85589-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span><span class="sxs-lookup"><span data-stu-id="85589-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="85589-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span><span class="sxs-lookup"><span data-stu-id="85589-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="85589-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span><span class="sxs-lookup"><span data-stu-id="85589-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="85589-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="85589-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="85589-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span><span class="sxs-lookup"><span data-stu-id="85589-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

