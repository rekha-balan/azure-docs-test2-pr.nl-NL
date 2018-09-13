---
title: Install Updates on a StorSimple Virtual Array | Microsoft Docs
description: Describes how to use the StorSimple Virtual Array web UI to apply updates using the portal and hotfix method
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: a5d71a19cbbb3d5ef487111d77b3dd89bb2d37df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555238"
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="36869-103">Install Updates on your StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="36869-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="36869-104">Overview</span><span class="sxs-lookup"><span data-stu-id="36869-104">Overview</span></span>
<span data-ttu-id="36869-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="36869-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="36869-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span><span class="sxs-lookup"><span data-stu-id="36869-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="36869-107">Keep in mind that installing an update or hotfix restarts your device.</span><span class="sxs-lookup"><span data-stu-id="36869-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="36869-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span><span class="sxs-lookup"><span data-stu-id="36869-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="36869-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span><span class="sxs-lookup"><span data-stu-id="36869-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="36869-110">This minimizes any possibility of data corruption.</span><span class="sxs-lookup"><span data-stu-id="36869-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36869-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span><span class="sxs-lookup"><span data-stu-id="36869-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="36869-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="36869-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="36869-113">Use the local web UI</span><span class="sxs-lookup"><span data-stu-id="36869-113">Use the local web UI</span></span>
<span data-ttu-id="36869-114">There are two steps when using the local web UI:</span><span class="sxs-lookup"><span data-stu-id="36869-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="36869-115">Download the update or the hotfix</span><span class="sxs-lookup"><span data-stu-id="36869-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="36869-116">Install the update or the hotfix</span><span class="sxs-lookup"><span data-stu-id="36869-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="36869-117">Download the update or the hotfix</span><span class="sxs-lookup"><span data-stu-id="36869-117">Download the update or the hotfix</span></span>
<span data-ttu-id="36869-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="36869-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="36869-119">To download the update or the hotfix</span><span class="sxs-lookup"><span data-stu-id="36869-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="36869-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="36869-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="36869-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span><span class="sxs-lookup"><span data-stu-id="36869-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="36869-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span><span class="sxs-lookup"><span data-stu-id="36869-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="36869-123">Enter **3182061** for Update 0.3, and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="36869-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="36869-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="36869-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Search catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="36869-126">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="36869-126">Click **Add**.</span></span> <span data-ttu-id="36869-127">The update is added to the basket.</span><span class="sxs-lookup"><span data-stu-id="36869-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="36869-128">Click **View Basket**.</span><span class="sxs-lookup"><span data-stu-id="36869-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="36869-129">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="36869-129">Click **Download**.</span></span> <span data-ttu-id="36869-130">Specify or **Browse** to a local location where you want the downloads to appear.</span><span class="sxs-lookup"><span data-stu-id="36869-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="36869-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span><span class="sxs-lookup"><span data-stu-id="36869-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="36869-132">The folder can also be copied to a network share that is reachable from the device.</span><span class="sxs-lookup"><span data-stu-id="36869-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="36869-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="36869-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="36869-134">This file is used to install the update or hotfix.</span><span class="sxs-lookup"><span data-stu-id="36869-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="36869-135">Install the update or the hotfix</span><span class="sxs-lookup"><span data-stu-id="36869-135">Install the update or the hotfix</span></span>
<span data-ttu-id="36869-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span><span class="sxs-lookup"><span data-stu-id="36869-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="36869-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span><span class="sxs-lookup"><span data-stu-id="36869-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="36869-138">This procedure takes less than 2 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="36869-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="36869-139">Perform the following steps to install the update or hotfix.</span><span class="sxs-lookup"><span data-stu-id="36869-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="36869-140">To install the update or the hotfix</span><span class="sxs-lookup"><span data-stu-id="36869-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="36869-141">In the local web UI, go to **Maintenance** > **Software Update**.</span><span class="sxs-lookup"><span data-stu-id="36869-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![update device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="36869-143">In **Update file path**, enter the file name for the update or the hotfix.</span><span class="sxs-lookup"><span data-stu-id="36869-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="36869-144">You can also browse to the update or hotfix installation file if placed on a network share.</span><span class="sxs-lookup"><span data-stu-id="36869-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="36869-145">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="36869-145">Click **Apply**.</span></span>
   
    ![update device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="36869-147">A warning is displayed.</span><span class="sxs-lookup"><span data-stu-id="36869-147">A warning is displayed.</span></span> <span data-ttu-id="36869-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span><span class="sxs-lookup"><span data-stu-id="36869-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="36869-149">Click the check icon.</span><span class="sxs-lookup"><span data-stu-id="36869-149">Click the check icon.</span></span>
   
   ![update device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="36869-151">The update starts.</span><span class="sxs-lookup"><span data-stu-id="36869-151">The update starts.</span></span> <span data-ttu-id="36869-152">After the device is successfully updated, it restarts.</span><span class="sxs-lookup"><span data-stu-id="36869-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="36869-153">The local UI is not accessible in this duration.</span><span class="sxs-lookup"><span data-stu-id="36869-153">The local UI is not accessible in this duration.</span></span>
   
    ![update device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="36869-155">After the restart is complete, you are taken to the **Sign in** page.</span><span class="sxs-lookup"><span data-stu-id="36869-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="36869-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span><span class="sxs-lookup"><span data-stu-id="36869-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="36869-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="36869-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="36869-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="36869-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="36869-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span><span class="sxs-lookup"><span data-stu-id="36869-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![update device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="36869-161">Use the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="36869-161">Use the Azure classic portal</span></span>
<span data-ttu-id="36869-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="36869-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="36869-163">The portal procedure requires the user to scan, download, and then install the updates.</span><span class="sxs-lookup"><span data-stu-id="36869-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="36869-164">This procedure takes around 7 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="36869-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="36869-165">Perform the following steps to install the update or hotfix.</span><span class="sxs-lookup"><span data-stu-id="36869-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="36869-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span><span class="sxs-lookup"><span data-stu-id="36869-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="36869-167">The displayed software version should be 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="36869-167">The displayed software version should be 10.0.10288.0.</span></span>

![update device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="36869-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="36869-169">Next steps</span></span>
<span data-ttu-id="36869-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="36869-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>








