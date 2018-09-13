---
title: Manage your StorSimple volume containers | Microsoft Docs
description: Explains how you can use the StorSimple Manager service volume containers page to add, modify, or delete a volume container.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: b6761e9f0747c848589b3b9087d2719710540390
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563716"
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="72200-103">Use the StorSimple Manager service to manage StorSimple volume containers</span><span class="sxs-lookup"><span data-stu-id="72200-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="72200-104">Overview</span><span class="sxs-lookup"><span data-stu-id="72200-104">Overview</span></span>
<span data-ttu-id="72200-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span><span class="sxs-lookup"><span data-stu-id="72200-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="72200-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span><span class="sxs-lookup"><span data-stu-id="72200-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="72200-107">A device can have multiple volume containers for all its volumes.</span><span class="sxs-lookup"><span data-stu-id="72200-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="72200-108">A volume container has the following attributes:</span><span class="sxs-lookup"><span data-stu-id="72200-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="72200-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span><span class="sxs-lookup"><span data-stu-id="72200-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="72200-110">A volume container may contain up to 256 StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="72200-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="72200-111">**Encryption** – An encryption key that can be defined for each volume container.</span><span class="sxs-lookup"><span data-stu-id="72200-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="72200-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span><span class="sxs-lookup"><span data-stu-id="72200-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="72200-113">A military-grade AES-256 bit key is used with the user-entered key.</span><span class="sxs-lookup"><span data-stu-id="72200-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="72200-114">To secure your data, we recommend that you always enable cloud storage encryption.</span><span class="sxs-lookup"><span data-stu-id="72200-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="72200-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span><span class="sxs-lookup"><span data-stu-id="72200-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="72200-116">All the volumes residing in a volume container share this storage account.</span><span class="sxs-lookup"><span data-stu-id="72200-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="72200-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span><span class="sxs-lookup"><span data-stu-id="72200-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="72200-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span><span class="sxs-lookup"><span data-stu-id="72200-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="72200-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span><span class="sxs-lookup"><span data-stu-id="72200-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="72200-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span><span class="sxs-lookup"><span data-stu-id="72200-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="72200-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span><span class="sxs-lookup"><span data-stu-id="72200-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![Volume containers page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="72200-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span><span class="sxs-lookup"><span data-stu-id="72200-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="72200-124">Add a volume container</span><span class="sxs-lookup"><span data-stu-id="72200-124">Add a volume container</span></span> 
* <span data-ttu-id="72200-125">Modify a volume container</span><span class="sxs-lookup"><span data-stu-id="72200-125">Modify a volume container</span></span> 
* <span data-ttu-id="72200-126">Delete a volume container</span><span class="sxs-lookup"><span data-stu-id="72200-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="72200-127">Add a volume container</span><span class="sxs-lookup"><span data-stu-id="72200-127">Add a volume container</span></span>
<span data-ttu-id="72200-128">Perform the following steps to add a volume container.</span><span class="sxs-lookup"><span data-stu-id="72200-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="72200-129">Modify a volume container</span><span class="sxs-lookup"><span data-stu-id="72200-129">Modify a volume container</span></span>
<span data-ttu-id="72200-130">Perform the following steps to modify a volume container.</span><span class="sxs-lookup"><span data-stu-id="72200-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="72200-131">Delete a volume container</span><span class="sxs-lookup"><span data-stu-id="72200-131">Delete a volume container</span></span>
<span data-ttu-id="72200-132">A volume container has volumes within it.</span><span class="sxs-lookup"><span data-stu-id="72200-132">A volume container has volumes within it.</span></span> <span data-ttu-id="72200-133">It can be deleted only if all the volumes contained in it are first deleted.</span><span class="sxs-lookup"><span data-stu-id="72200-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="72200-134">Perform the following steps to delete a volume container.</span><span class="sxs-lookup"><span data-stu-id="72200-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="72200-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="72200-135">Next steps</span></span>
* <span data-ttu-id="72200-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="72200-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="72200-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="72200-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


