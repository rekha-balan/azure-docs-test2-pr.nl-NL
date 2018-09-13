---
title: StorSimple Virtual Array web UI administration | Microsoft Docs
description: Describes how to perform basic device administration tasks through the StorSimple Virtual Array web UI.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 989e7b697f9b527df549fb32be18edd1d3c8d224
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804484"
---
# <a name="use-the-web-ui-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="8bf33-103">Use the Web UI to administer your StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="8bf33-103">Use the Web UI to administer your StorSimple Virtual Array</span></span>
![setup process flow](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="8bf33-105">Overview</span><span class="sxs-lookup"><span data-stu-id="8bf33-105">Overview</span></span>
<span data-ttu-id="8bf33-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span><span class="sxs-lookup"><span data-stu-id="8bf33-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="8bf33-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="8bf33-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span></span> <span data-ttu-id="8bf33-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span><span class="sxs-lookup"><span data-stu-id="8bf33-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span></span> <span data-ttu-id="8bf33-109">This article focuses on the tasks that you can perform using the web UI.</span><span class="sxs-lookup"><span data-stu-id="8bf33-109">This article focuses on the tasks that you can perform using the web UI.</span></span>

<span data-ttu-id="8bf33-110">This article includes the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="8bf33-110">This article includes the following tutorials:</span></span>

* <span data-ttu-id="8bf33-111">Get the service data encryption key</span><span class="sxs-lookup"><span data-stu-id="8bf33-111">Get the service data encryption key</span></span>
* <span data-ttu-id="8bf33-112">Troubleshoot web UI setup errors</span><span class="sxs-lookup"><span data-stu-id="8bf33-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="8bf33-113">Generate a log package</span><span class="sxs-lookup"><span data-stu-id="8bf33-113">Generate a log package</span></span>
* <span data-ttu-id="8bf33-114">Shut down or restart your device</span><span class="sxs-lookup"><span data-stu-id="8bf33-114">Shut down or restart your device</span></span>

## <a name="get-the-service-data-encryption-key"></a><span data-ttu-id="8bf33-115">Get the service data encryption key</span><span class="sxs-lookup"><span data-stu-id="8bf33-115">Get the service data encryption key</span></span>
<span data-ttu-id="8bf33-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="8bf33-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span></span> <span data-ttu-id="8bf33-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="8bf33-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span></span>

<span data-ttu-id="8bf33-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span><span class="sxs-lookup"><span data-stu-id="8bf33-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span></span>

#### <a name="to-get-the-service-data-encryption-key"></a><span data-ttu-id="8bf33-119">To get the service data encryption key</span><span class="sxs-lookup"><span data-stu-id="8bf33-119">To get the service data encryption key</span></span>
1. <span data-ttu-id="8bf33-120">Connect to the local web UI.</span><span class="sxs-lookup"><span data-stu-id="8bf33-120">Connect to the local web UI.</span></span> <span data-ttu-id="8bf33-121">Go to **Configuration** > **Cloud Settings**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-121">Go to **Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="8bf33-122">At the bottom of the page, click **Get service data encryption key**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-122">At the bottom of the page, click **Get service data encryption key**.</span></span> <span data-ttu-id="8bf33-123">A key will appear.</span><span class="sxs-lookup"><span data-stu-id="8bf33-123">A key will appear.</span></span> <span data-ttu-id="8bf33-124">Copy and save this key.</span><span class="sxs-lookup"><span data-stu-id="8bf33-124">Copy and save this key.</span></span>
   
    ![get service data encryption key 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="8bf33-126">Troubleshoot web UI setup errors</span><span class="sxs-lookup"><span data-stu-id="8bf33-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="8bf33-127">In some instances when you configure the device through the local web UI, you might run into errors.</span><span class="sxs-lookup"><span data-stu-id="8bf33-127">In some instances when you configure the device through the local web UI, you might run into errors.</span></span> <span data-ttu-id="8bf33-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span><span class="sxs-lookup"><span data-stu-id="8bf33-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span></span>

#### <a name="to-run-the-diagnostic-tests"></a><span data-ttu-id="8bf33-129">To run the diagnostic tests</span><span class="sxs-lookup"><span data-stu-id="8bf33-129">To run the diagnostic tests</span></span>
1. <span data-ttu-id="8bf33-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![run diagnostics 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="8bf33-132">At the bottom of the page, click **Run Diagnostic Tests**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-132">At the bottom of the page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="8bf33-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span><span class="sxs-lookup"><span data-stu-id="8bf33-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="8bf33-134">You will be notified that the device is running tests.</span><span class="sxs-lookup"><span data-stu-id="8bf33-134">You will be notified that the device is running tests.</span></span>
3. <span data-ttu-id="8bf33-135">After the tests have completed, the results will be displayed.</span><span class="sxs-lookup"><span data-stu-id="8bf33-135">After the tests have completed, the results will be displayed.</span></span> <span data-ttu-id="8bf33-136">The following example shows the results of diagnostic tests.</span><span class="sxs-lookup"><span data-stu-id="8bf33-136">The following example shows the results of diagnostic tests.</span></span> <span data-ttu-id="8bf33-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span><span class="sxs-lookup"><span data-stu-id="8bf33-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span></span> <span data-ttu-id="8bf33-138">All the other tests for network settings, DNS server, and time settings were successful.</span><span class="sxs-lookup"><span data-stu-id="8bf33-138">All the other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![run diagnostics 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="8bf33-140">Generate a log package</span><span class="sxs-lookup"><span data-stu-id="8bf33-140">Generate a log package</span></span>
<span data-ttu-id="8bf33-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span><span class="sxs-lookup"><span data-stu-id="8bf33-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="8bf33-142">In this release, a log package can be generated via the local web UI.</span><span class="sxs-lookup"><span data-stu-id="8bf33-142">In this release, a log package can be generated via the local web UI.</span></span>

#### <a name="to-generate-the-log-package"></a><span data-ttu-id="8bf33-143">To generate the log package</span><span class="sxs-lookup"><span data-stu-id="8bf33-143">To generate the log package</span></span>
1. <span data-ttu-id="8bf33-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span></span>
   
    ![generate log package 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="8bf33-146">At the bottom of the page, click **Create log package**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-146">At the bottom of the page, click **Create log package**.</span></span> <span data-ttu-id="8bf33-147">A package of the system logs will be created.</span><span class="sxs-lookup"><span data-stu-id="8bf33-147">A package of the system logs will be created.</span></span> <span data-ttu-id="8bf33-148">This will take a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="8bf33-148">This will take a couple of minutes.</span></span>
   
    ![generate log package 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="8bf33-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span><span class="sxs-lookup"><span data-stu-id="8bf33-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span></span>
   
    ![generate log package 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="8bf33-152">Click **Download log package**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-152">Click **Download log package**.</span></span> <span data-ttu-id="8bf33-153">A zipped package will be downloaded on your system.</span><span class="sxs-lookup"><span data-stu-id="8bf33-153">A zipped package will be downloaded on your system.</span></span>
   
    ![generate log package 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="8bf33-155">You can unzip the downloaded log package and view the system log files.</span><span class="sxs-lookup"><span data-stu-id="8bf33-155">You can unzip the downloaded log package and view the system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="8bf33-156">Shut down and restart your device</span><span class="sxs-lookup"><span data-stu-id="8bf33-156">Shut down and restart your device</span></span>
<span data-ttu-id="8bf33-157">You can shut down or restart your virtual device using the local web UI.</span><span class="sxs-lookup"><span data-stu-id="8bf33-157">You can shut down or restart your virtual device using the local web UI.</span></span> <span data-ttu-id="8bf33-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span><span class="sxs-lookup"><span data-stu-id="8bf33-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span></span> <span data-ttu-id="8bf33-159">This will minimize any possibility of data corruption.</span><span class="sxs-lookup"><span data-stu-id="8bf33-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="to-shut-down-your-virtual-device"></a><span data-ttu-id="8bf33-160">To shut down your virtual device</span><span class="sxs-lookup"><span data-stu-id="8bf33-160">To shut down your virtual device</span></span>
1. <span data-ttu-id="8bf33-161">In the local web UI, go to **Maintenance** > **Power settings**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-161">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="8bf33-162">At the bottom of the page, click **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-162">At the bottom of the page, click **Shutdown**.</span></span>
   
    ![device shutdown 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="8bf33-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span><span class="sxs-lookup"><span data-stu-id="8bf33-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="8bf33-165">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="8bf33-165">Click the check icon</span></span> ![check icon](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="8bf33-167">.</span><span class="sxs-lookup"><span data-stu-id="8bf33-167">.</span></span>
   
    ![device shutdown warning](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="8bf33-169">You will be notified that the shutdown has been initiated.</span><span class="sxs-lookup"><span data-stu-id="8bf33-169">You will be notified that the shutdown has been initiated.</span></span>
   
    ![device shutdown started](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="8bf33-171">The device will now shut down.</span><span class="sxs-lookup"><span data-stu-id="8bf33-171">The device will now shut down.</span></span> <span data-ttu-id="8bf33-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="8bf33-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span></span>

#### <a name="to-restart-your-virtual-device"></a><span data-ttu-id="8bf33-173">To restart your virtual device</span><span class="sxs-lookup"><span data-stu-id="8bf33-173">To restart your virtual device</span></span>
1. <span data-ttu-id="8bf33-174">In the local web UI, go to **Maintenance** > **Power settings**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-174">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="8bf33-175">At the bottom of the page, click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="8bf33-175">At the bottom of the page, click **Restart**.</span></span>
   
    ![device restart](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="8bf33-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span><span class="sxs-lookup"><span data-stu-id="8bf33-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="8bf33-178">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="8bf33-178">Click the check icon</span></span> ![check icon](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="8bf33-180">.</span><span class="sxs-lookup"><span data-stu-id="8bf33-180">.</span></span>
   
    ![restart warning](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="8bf33-182">You will be notified that the restart has been initiated.</span><span class="sxs-lookup"><span data-stu-id="8bf33-182">You will be notified that the restart has been initiated.</span></span>
   
    ![restart initiated](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="8bf33-184">While the restart is in progress, you will lose the connection to the UI.</span><span class="sxs-lookup"><span data-stu-id="8bf33-184">While the restart is in progress, you will lose the connection to the UI.</span></span> <span data-ttu-id="8bf33-185">You can monitor the restart by refreshing the UI periodically.</span><span class="sxs-lookup"><span data-stu-id="8bf33-185">You can monitor the restart by refreshing the UI periodically.</span></span> <span data-ttu-id="8bf33-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="8bf33-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bf33-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bf33-187">Next steps</span></span>
<span data-ttu-id="8bf33-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8bf33-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

