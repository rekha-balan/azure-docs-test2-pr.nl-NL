---
title: Replace chassis on StorSimple 8000 series device | Microsoft Docs
description: Describes how to remove and replace the chassis for your StorSimple primary enclosure or EBOD enclosure.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5295c5dd039b1d4746ebaaf90372932e4c3e7c26
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550066"
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="11a07-103">Replace the chassis on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="11a07-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="11a07-104">Overview</span><span class="sxs-lookup"><span data-stu-id="11a07-104">Overview</span></span>
<span data-ttu-id="11a07-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span><span class="sxs-lookup"><span data-stu-id="11a07-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="11a07-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span><span class="sxs-lookup"><span data-stu-id="11a07-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="11a07-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span><span class="sxs-lookup"><span data-stu-id="11a07-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="11a07-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span><span class="sxs-lookup"><span data-stu-id="11a07-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="11a07-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span><span class="sxs-lookup"><span data-stu-id="11a07-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11a07-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="11a07-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-chassis"></a><span data-ttu-id="11a07-111">Remove the chassis</span><span class="sxs-lookup"><span data-stu-id="11a07-111">Remove the chassis</span></span>
<span data-ttu-id="11a07-112">Perform the following steps to remove the chassis on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="11a07-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="11a07-113">To remove a chassis</span><span class="sxs-lookup"><span data-stu-id="11a07-113">To remove a chassis</span></span>
1. <span data-ttu-id="11a07-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span><span class="sxs-lookup"><span data-stu-id="11a07-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="11a07-115">Remove all the network and SAS cables, if applicable.</span><span class="sxs-lookup"><span data-stu-id="11a07-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="11a07-116">Remove the unit from the rack.</span><span class="sxs-lookup"><span data-stu-id="11a07-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="11a07-117">Remove each of the drives and note the slots from which they are removed.</span><span class="sxs-lookup"><span data-stu-id="11a07-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="11a07-118">For more information, see [Remove the disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="11a07-118">For more information, see [Remove the disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="11a07-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span><span class="sxs-lookup"><span data-stu-id="11a07-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="11a07-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="11a07-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="11a07-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span><span class="sxs-lookup"><span data-stu-id="11a07-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="11a07-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="11a07-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="11a07-123">Install the chassis</span><span class="sxs-lookup"><span data-stu-id="11a07-123">Install the chassis</span></span>
<span data-ttu-id="11a07-124">Perform the following steps to install the chassis on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="11a07-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="11a07-125">To install a chassis</span><span class="sxs-lookup"><span data-stu-id="11a07-125">To install a chassis</span></span>
1. <span data-ttu-id="11a07-126">Mount the chassis in the rack.</span><span class="sxs-lookup"><span data-stu-id="11a07-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="11a07-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="11a07-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="11a07-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span><span class="sxs-lookup"><span data-stu-id="11a07-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="11a07-129">Install the drives in the same positions and slots that they were previously installed in.</span><span class="sxs-lookup"><span data-stu-id="11a07-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="11a07-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span><span class="sxs-lookup"><span data-stu-id="11a07-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="11a07-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span><span class="sxs-lookup"><span data-stu-id="11a07-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="11a07-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="11a07-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11a07-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="11a07-133">Next steps</span></span>
<span data-ttu-id="11a07-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="11a07-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

