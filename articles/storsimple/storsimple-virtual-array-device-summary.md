---
title: StorSimple Virtual Array device summary blade | Microsoft Docs
description: Describes the device summary blade for StorSimple Device Manager and explains how to use it to monitor the health of your StorSimple Virtual Array.
services: storsimple
documentationcenter: ''
author: manuaery
manager: syadav
editor: ''
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: aa545472a3e31c64ccb5a51337333d92a64391b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551555"
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="97aa5-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="97aa5-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="97aa5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="97aa5-104">Overview</span></span>

<span data-ttu-id="97aa5-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span><span class="sxs-lookup"><span data-stu-id="97aa5-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="97aa5-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span><span class="sxs-lookup"><span data-stu-id="97aa5-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="97aa5-107">The device summary blade displays the following information:</span><span class="sxs-lookup"><span data-stu-id="97aa5-107">The device summary blade displays the following information:</span></span>

![Device dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="97aa5-109">Management</span><span class="sxs-lookup"><span data-stu-id="97aa5-109">Management</span></span>

<span data-ttu-id="97aa5-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="97aa5-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="97aa5-111">You see the management commands across the top of the blade and on the left side.</span><span class="sxs-lookup"><span data-stu-id="97aa5-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="97aa5-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span><span class="sxs-lookup"><span data-stu-id="97aa5-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="97aa5-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span><span class="sxs-lookup"><span data-stu-id="97aa5-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="97aa5-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span><span class="sxs-lookup"><span data-stu-id="97aa5-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Device essentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="97aa5-116">StorSimple device summary</span><span class="sxs-lookup"><span data-stu-id="97aa5-116">StorSimple device summary</span></span>

* <span data-ttu-id="97aa5-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span><span class="sxs-lookup"><span data-stu-id="97aa5-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="97aa5-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span><span class="sxs-lookup"><span data-stu-id="97aa5-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="97aa5-119">You can also clear the alert if the issue has been resolved.</span><span class="sxs-lookup"><span data-stu-id="97aa5-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="97aa5-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span><span class="sxs-lookup"><span data-stu-id="97aa5-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="97aa5-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span><span class="sxs-lookup"><span data-stu-id="97aa5-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="97aa5-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span><span class="sxs-lookup"><span data-stu-id="97aa5-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="97aa5-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span><span class="sxs-lookup"><span data-stu-id="97aa5-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="97aa5-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span><span class="sxs-lookup"><span data-stu-id="97aa5-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="97aa5-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span><span class="sxs-lookup"><span data-stu-id="97aa5-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="97aa5-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span><span class="sxs-lookup"><span data-stu-id="97aa5-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="97aa5-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="97aa5-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97aa5-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="97aa5-128">Next steps</span></span>
<span data-ttu-id="97aa5-129">Learn how to:</span><span class="sxs-lookup"><span data-stu-id="97aa5-129">Learn how to:</span></span>
- [<span data-ttu-id="97aa5-130">Manage shares on a StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="97aa5-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="97aa5-131">Manage volumes on a StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="97aa5-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)



