---
title: include file
description: include file
services: storsimple
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 07/18/2018
ms.author: alkohli
ms.custom: include file
ms.openlocfilehash: a83095b8330ccf08d777e48389c17058c6d29527
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856409"
---
#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="9f8ee-103">To install updates via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9f8ee-103">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="9f8ee-104">Go to your StorSimple Device Manager and select **Devices**.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-104">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="9f8ee-105">From the list of devices connected to your service, select and click the device you want to update.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-105">From the list of devices connected to your service, select and click the device you want to update.</span></span>

2. <span data-ttu-id="9f8ee-106">Under **Settings**, click **Device updates**.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-106">Under **Settings**, click **Device updates**.</span></span>  

3. <span data-ttu-id="9f8ee-107">You see a message if the software updates are available.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="9f8ee-108">To check for updates, you can also click **Scan**.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-108">To check for updates, you can also click **Scan**.</span></span> <span data-ttu-id="9f8ee-109">Make a note of the software version you are running.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-109">Make a note of the software version you are running.</span></span> 

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-11/azupdate3m1.png)

    <span data-ttu-id="9f8ee-111">You are notified when the scan starts and completes successfully.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-111">You are notified when the scan starts and completes successfully.</span></span>
 
4. <span data-ttu-id="9f8ee-112">Once the updates are scanned, click **Download updates**.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-112">Once the updates are scanned, click **Download updates**.</span></span> <span data-ttu-id="9f8ee-113">Under **New updates**, review the release notes.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-113">Under **New updates**, review the release notes.</span></span> <span data-ttu-id="9f8ee-114">Also note that after the updates are downloaded, you need to confirm the installation.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-114">Also note that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="9f8ee-115">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-115">Click **OK**.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-11/azupdate6m.png)

    <span data-ttu-id="9f8ee-117">You are notified when the upload starts and completes successfully.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-117">You are notified when the upload starts and completes successfully.</span></span>

5. <span data-ttu-id="9f8ee-118">Under **Device updates**, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-118">Under **Device updates**, click **Install**.</span></span>

     ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-11/azupdate11m1.png)

6. <span data-ttu-id="9f8ee-120">Under **New updates**, you are warned that the update is disruptive.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-120">Under **New updates**, you are warned that the update is disruptive.</span></span> <span data-ttu-id="9f8ee-121">As virtual array is a single node device, the device restarts after it is updated.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-121">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="9f8ee-122">This disrupts any IO in progress.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-122">This disrupts any IO in progress.</span></span> <span data-ttu-id="9f8ee-123">Click **OK** to install the updates.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-123">Click **OK** to install the updates.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-11/azupdate12m.png)

    <span data-ttu-id="9f8ee-125">You are notified when the install job starts.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-125">You are notified when the install job starts.</span></span>

7.  <span data-ttu-id="9f8ee-126">After the install job completes successfully, click **View Job** link.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-126">After the install job completes successfully, click **View Job** link.</span></span> <span data-ttu-id="9f8ee-127">This action takes you to the **Install Updates** blade.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-127">This action takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="9f8ee-128">You can view detailed information about the job here.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-128">You can view detailed information about the job here.</span></span> 

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-11/azupdate16m1.png)

8. <span data-ttu-id="9f8ee-130">If you started with a virtual array running software version Update 1 (10.0.10296.0), you are now running Update 1.1 and are done.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-130">If you started with a virtual array running software version Update 1 (10.0.10296.0), you are now running Update 1.1 and are done.</span></span> <span data-ttu-id="9f8ee-131">You can skip the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-131">You can skip the remaining steps.</span></span> 

    <span data-ttu-id="9f8ee-132">If you started with a virtual array running software version Update 0.6 (10.0.10293.0), you are now updated to Update 1.0.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-132">If you started with a virtual array running software version Update 0.6 (10.0.10293.0), you are now updated to Update 1.0.</span></span> <span data-ttu-id="9f8ee-133">You see another message indicating that updates are available.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-133">You see another message indicating that updates are available.</span></span> <span data-ttu-id="9f8ee-134">Repeat steps 4-7 to install Update 1.1.</span><span class="sxs-lookup"><span data-stu-id="9f8ee-134">Repeat steps 4-7 to install Update 1.1.</span></span>

    

