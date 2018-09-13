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
ms.openlocfilehash: 42bf7218598793608a49f9dc2ffba1fb8e11ff13
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660738"
---
# <a name="use-the-web-ui-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="42f7a-103">Use the Web UI to administer your StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="42f7a-103">Use the Web UI to administer your StorSimple Virtual Array</span></span>
![setup process flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="42f7a-105">Overview</span><span class="sxs-lookup"><span data-stu-id="42f7a-105">Overview</span></span>
<span data-ttu-id="42f7a-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span><span class="sxs-lookup"><span data-stu-id="42f7a-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="42f7a-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="42f7a-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span></span> <span data-ttu-id="42f7a-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span><span class="sxs-lookup"><span data-stu-id="42f7a-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span></span> <span data-ttu-id="42f7a-109">This article focuses on the tasks that you can perform using the web UI.</span><span class="sxs-lookup"><span data-stu-id="42f7a-109">This article focuses on the tasks that you can perform using the web UI.</span></span>

<span data-ttu-id="42f7a-110">This article includes the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="42f7a-110">This article includes the following tutorials:</span></span>

* <span data-ttu-id="42f7a-111">Get the service data encryption key</span><span class="sxs-lookup"><span data-stu-id="42f7a-111">Get the service data encryption key</span></span>
* <span data-ttu-id="42f7a-112">Troubleshoot web UI setup errors</span><span class="sxs-lookup"><span data-stu-id="42f7a-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="42f7a-113">Generate a log package</span><span class="sxs-lookup"><span data-stu-id="42f7a-113">Generate a log package</span></span>
* <span data-ttu-id="42f7a-114">Shut down or restart your device</span><span class="sxs-lookup"><span data-stu-id="42f7a-114">Shut down or restart your device</span></span>

## <a name="get-the-service-data-encryption-key"></a><span data-ttu-id="42f7a-115">Get the service data encryption key</span><span class="sxs-lookup"><span data-stu-id="42f7a-115">Get the service data encryption key</span></span>
<span data-ttu-id="42f7a-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="42f7a-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span></span> <span data-ttu-id="42f7a-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="42f7a-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span></span>

<span data-ttu-id="42f7a-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span><span class="sxs-lookup"><span data-stu-id="42f7a-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span></span>

#### <a name="to-get-the-service-data-encryption-key"></a><span data-ttu-id="42f7a-119">To get the service data encryption key</span><span class="sxs-lookup"><span data-stu-id="42f7a-119">To get the service data encryption key</span></span>
1. <span data-ttu-id="42f7a-120">Connect to the local web UI.</span><span class="sxs-lookup"><span data-stu-id="42f7a-120">Connect to the local web UI.</span></span> <span data-ttu-id="42f7a-121">Go to **Configuration** > **Cloud Settings**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-121">Go to **Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="42f7a-122">At the bottom of the page, click **Get service data encryption key**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-122">At the bottom of the page, click **Get service data encryption key**.</span></span> <span data-ttu-id="42f7a-123">A key will appear.</span><span class="sxs-lookup"><span data-stu-id="42f7a-123">A key will appear.</span></span> <span data-ttu-id="42f7a-124">Copy and save this key.</span><span class="sxs-lookup"><span data-stu-id="42f7a-124">Copy and save this key.</span></span>
   
    ![get service data encryption key 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="42f7a-126">Troubleshoot web UI setup errors</span><span class="sxs-lookup"><span data-stu-id="42f7a-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="42f7a-127">In some instances when you configure the device through the local web UI, you might run into errors.</span><span class="sxs-lookup"><span data-stu-id="42f7a-127">In some instances when you configure the device through the local web UI, you might run into errors.</span></span> <span data-ttu-id="42f7a-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span><span class="sxs-lookup"><span data-stu-id="42f7a-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span></span>

#### <a name="to-run-the-diagnostic-tests"></a><span data-ttu-id="42f7a-129">To run the diagnostic tests</span><span class="sxs-lookup"><span data-stu-id="42f7a-129">To run the diagnostic tests</span></span>
1. <span data-ttu-id="42f7a-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![run diagnostics 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="42f7a-132">At the bottom of the page, click **Run Diagnostic Tests**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-132">At the bottom of the page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="42f7a-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span><span class="sxs-lookup"><span data-stu-id="42f7a-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="42f7a-134">You will be notified that the device is running tests.</span><span class="sxs-lookup"><span data-stu-id="42f7a-134">You will be notified that the device is running tests.</span></span>
3. <span data-ttu-id="42f7a-135">After the tests have completed, the results will be displayed.</span><span class="sxs-lookup"><span data-stu-id="42f7a-135">After the tests have completed, the results will be displayed.</span></span> <span data-ttu-id="42f7a-136">The following example shows the results of diagnostic tests.</span><span class="sxs-lookup"><span data-stu-id="42f7a-136">The following example shows the results of diagnostic tests.</span></span> <span data-ttu-id="42f7a-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span><span class="sxs-lookup"><span data-stu-id="42f7a-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span></span> <span data-ttu-id="42f7a-138">All the other tests for network settings, DNS server, and time settings were successful.</span><span class="sxs-lookup"><span data-stu-id="42f7a-138">All the other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![run diagnostics 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="42f7a-140">Generate a log package</span><span class="sxs-lookup"><span data-stu-id="42f7a-140">Generate a log package</span></span>
<span data-ttu-id="42f7a-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span><span class="sxs-lookup"><span data-stu-id="42f7a-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="42f7a-142">In this release, a log package can be generated via the local web UI.</span><span class="sxs-lookup"><span data-stu-id="42f7a-142">In this release, a log package can be generated via the local web UI.</span></span>

#### <a name="to-generate-the-log-package"></a><span data-ttu-id="42f7a-143">To generate the log package</span><span class="sxs-lookup"><span data-stu-id="42f7a-143">To generate the log package</span></span>
1. <span data-ttu-id="42f7a-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span></span>
   
    ![generate log package 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="42f7a-146">At the bottom of the page, click **Create log package**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-146">At the bottom of the page, click **Create log package**.</span></span> <span data-ttu-id="42f7a-147">A package of the system logs will be created.</span><span class="sxs-lookup"><span data-stu-id="42f7a-147">A package of the system logs will be created.</span></span> <span data-ttu-id="42f7a-148">This will take a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="42f7a-148">This will take a couple of minutes.</span></span>
   
    ![generate log package 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="42f7a-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span><span class="sxs-lookup"><span data-stu-id="42f7a-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span></span>
   
    ![generate log package 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="42f7a-152">Click **Download log package**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-152">Click **Download log package**.</span></span> <span data-ttu-id="42f7a-153">A zipped package will be downloaded on your system.</span><span class="sxs-lookup"><span data-stu-id="42f7a-153">A zipped package will be downloaded on your system.</span></span>
   
    ![generate log package 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="42f7a-155">You can unzip the downloaded log package and view the system log files.</span><span class="sxs-lookup"><span data-stu-id="42f7a-155">You can unzip the downloaded log package and view the system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="42f7a-156">Shut down and restart your device</span><span class="sxs-lookup"><span data-stu-id="42f7a-156">Shut down and restart your device</span></span>
<span data-ttu-id="42f7a-157">You can shut down or restart your virtual device using the local web UI.</span><span class="sxs-lookup"><span data-stu-id="42f7a-157">You can shut down or restart your virtual device using the local web UI.</span></span> <span data-ttu-id="42f7a-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span><span class="sxs-lookup"><span data-stu-id="42f7a-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span></span> <span data-ttu-id="42f7a-159">This will minimize any possibility of data corruption.</span><span class="sxs-lookup"><span data-stu-id="42f7a-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="to-shut-down-your-virtual-device"></a><span data-ttu-id="42f7a-160">To shut down your virtual device</span><span class="sxs-lookup"><span data-stu-id="42f7a-160">To shut down your virtual device</span></span>
1. <span data-ttu-id="42f7a-161">In the local web UI, go to **Maintenance** > **Power settings**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-161">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="42f7a-162">At the bottom of the page, click **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-162">At the bottom of the page, click **Shutdown**.</span></span>
   
    ![device shutdown 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="42f7a-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span><span class="sxs-lookup"><span data-stu-id="42f7a-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="42f7a-165">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="42f7a-165">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="42f7a-167">.</span><span class="sxs-lookup"><span data-stu-id="42f7a-167">.</span></span>
   
    ![device shutdown warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="42f7a-169">You will be notified that the shutdown has been initiated.</span><span class="sxs-lookup"><span data-stu-id="42f7a-169">You will be notified that the shutdown has been initiated.</span></span>
   
    ![device shutdown started](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="42f7a-171">The device will now shut down.</span><span class="sxs-lookup"><span data-stu-id="42f7a-171">The device will now shut down.</span></span> <span data-ttu-id="42f7a-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="42f7a-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span></span>

#### <a name="to-restart-your-virtual-device"></a><span data-ttu-id="42f7a-173">To restart your virtual device</span><span class="sxs-lookup"><span data-stu-id="42f7a-173">To restart your virtual device</span></span>
1. <span data-ttu-id="42f7a-174">In the local web UI, go to **Maintenance** > **Power settings**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-174">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="42f7a-175">At the bottom of the page, click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="42f7a-175">At the bottom of the page, click **Restart**.</span></span>
   
    ![device restart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="42f7a-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span><span class="sxs-lookup"><span data-stu-id="42f7a-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="42f7a-178">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="42f7a-178">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="42f7a-180">.</span><span class="sxs-lookup"><span data-stu-id="42f7a-180">.</span></span>
   
    ![restart warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="42f7a-182">You will be notified that the restart has been initiated.</span><span class="sxs-lookup"><span data-stu-id="42f7a-182">You will be notified that the restart has been initiated.</span></span>
   
    ![restart initiated](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="42f7a-184">While the restart is in progress, you will lose the connection to the UI.</span><span class="sxs-lookup"><span data-stu-id="42f7a-184">While the restart is in progress, you will lose the connection to the UI.</span></span> <span data-ttu-id="42f7a-185">You can monitor the restart by refreshing the UI periodically.</span><span class="sxs-lookup"><span data-stu-id="42f7a-185">You can monitor the restart by refreshing the UI periodically.</span></span> <span data-ttu-id="42f7a-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="42f7a-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f7a-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="42f7a-187">Next steps</span></span>
<span data-ttu-id="42f7a-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="42f7a-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

















