---
title: Troubleshoot RemoteApp cloud collections - creation | Microsoft Docs
description: Learn how to troubleshoot RemoteApp cloud collection creation failures
services: remoteapp
documentationcenter: ''
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548909"
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="3fddb-103">Troubleshoot creating RemoteApp cloud collections</span><span class="sxs-lookup"><span data-stu-id="3fddb-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3fddb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="3fddb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3fddb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="3fddb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3fddb-106">If you are having problems creating a cloud collection, check out the following information.</span><span class="sxs-lookup"><span data-stu-id="3fddb-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="3fddb-107">Your image is invalid</span><span class="sxs-lookup"><span data-stu-id="3fddb-107">Your image is invalid</span></span>
<span data-ttu-id="3fddb-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="3fddb-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="3fddb-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span><span class="sxs-lookup"><span data-stu-id="3fddb-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="3fddb-110">Common errors seen in the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="3fddb-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="3fddb-111">Cloud collections often fail during creation because of you are using custom images.</span><span class="sxs-lookup"><span data-stu-id="3fddb-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="3fddb-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span><span class="sxs-lookup"><span data-stu-id="3fddb-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="3fddb-113">Ensure that the custom image you uploaded meets image requirements.</span><span class="sxs-lookup"><span data-stu-id="3fddb-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="3fddb-114">Most often the common problem is that the image was not properly syspreped.</span><span class="sxs-lookup"><span data-stu-id="3fddb-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="3fddb-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span><span class="sxs-lookup"><span data-stu-id="3fddb-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="3fddb-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span><span class="sxs-lookup"><span data-stu-id="3fddb-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="3fddb-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3fddb-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="3fddb-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span><span class="sxs-lookup"><span data-stu-id="3fddb-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="3fddb-119">If the issue persists then please contact Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="3fddb-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="3fddb-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span><span class="sxs-lookup"><span data-stu-id="3fddb-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="3fddb-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span><span class="sxs-lookup"><span data-stu-id="3fddb-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>

