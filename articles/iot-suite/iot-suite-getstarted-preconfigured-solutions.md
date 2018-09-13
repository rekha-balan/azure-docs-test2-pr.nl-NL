---
title: Get started with preconfigured solutions | Microsoft Docs
description: Follow this tutorial to learn how to deploy an Azure IoT Suite preconfigured solution.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: dobett
ms.openlocfilehash: 67f5a1e909fa354cf38b600efb638aa3c11a0e61
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555389"
---
# <a name="tutorial-get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="5652c-103">Tutorial: Get started with the preconfigured solutions</span><span class="sxs-lookup"><span data-stu-id="5652c-103">Tutorial: Get started with the preconfigured solutions</span></span>
## <a name="introduction"></a><span data-ttu-id="5652c-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="5652c-104">Introduction</span></span>
<span data-ttu-id="5652c-105">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span><span class="sxs-lookup"><span data-stu-id="5652c-105">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="5652c-106">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-106">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="5652c-107">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span><span class="sxs-lookup"><span data-stu-id="5652c-107">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="5652c-108">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-108">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5652c-109">It also walks you through the basic features of the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-109">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="5652c-110">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="5652c-110">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Remote monitoring preconfigured solution dashboard][img-dashboard]

<span data-ttu-id="5652c-112">To complete this tutorial, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5652c-112">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5652c-113">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="5652c-113">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5652c-114">For details, see [Azure Free Trial][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="5652c-114">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="5652c-115">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="5652c-115">Scenario overview</span></span>

<span data-ttu-id="5652c-116">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span><span class="sxs-lookup"><span data-stu-id="5652c-116">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="5652c-117">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span><span class="sxs-lookup"><span data-stu-id="5652c-117">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="5652c-118">The following sections show you how to:</span><span class="sxs-lookup"><span data-stu-id="5652c-118">The following sections show you how to:</span></span>

* <span data-ttu-id="5652c-119">Identify the devices sending unexpected temperature values.</span><span class="sxs-lookup"><span data-stu-id="5652c-119">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="5652c-120">Configure these devices to send more detailed telemetry.</span><span class="sxs-lookup"><span data-stu-id="5652c-120">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="5652c-121">Fix the problem by updating the firmware on these devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-121">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="5652c-122">Verify that your action has resolved the issue.</span><span class="sxs-lookup"><span data-stu-id="5652c-122">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="5652c-123">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="5652c-123">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="5652c-124">You do not need physical access to the devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-124">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="5652c-125">View the solution dashboard</span><span class="sxs-lookup"><span data-stu-id="5652c-125">View the solution dashboard</span></span>

<span data-ttu-id="5652c-126">The solution dashboard enables you to manage the deployed solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-126">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="5652c-127">For example, you can view telemetry, add devices, and configure rules.</span><span class="sxs-lookup"><span data-stu-id="5652c-127">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="5652c-128">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span><span class="sxs-lookup"><span data-stu-id="5652c-128">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Launch the preconfigured solution][img-launch-solution]

1. <span data-ttu-id="5652c-130">By default, the solution portal shows the *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="5652c-130">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="5652c-131">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span><span class="sxs-lookup"><span data-stu-id="5652c-131">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Remote monitoring preconfigured solution dashboard][img-menu]

<span data-ttu-id="5652c-133">The dashboard displays the following information:</span><span class="sxs-lookup"><span data-stu-id="5652c-133">The dashboard displays the following information:</span></span>

* <span data-ttu-id="5652c-134">A map that displays the location of each device connected to the solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-134">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="5652c-135">When you first run the solution, there are 25 simulated devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-135">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="5652c-136">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span><span class="sxs-lookup"><span data-stu-id="5652c-136">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="5652c-137">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span><span class="sxs-lookup"><span data-stu-id="5652c-137">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="5652c-138">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span><span class="sxs-lookup"><span data-stu-id="5652c-138">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="5652c-139">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span><span class="sxs-lookup"><span data-stu-id="5652c-139">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="5652c-140">You can define your own alarms in addition to the examples created by the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-140">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="5652c-141">A **Jobs** panel that displays information about scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="5652c-141">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="5652c-142">You can schedule your own jobs on **Management jobs** page.</span><span class="sxs-lookup"><span data-stu-id="5652c-142">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="5652c-143">View alarms</span><span class="sxs-lookup"><span data-stu-id="5652c-143">View alarms</span></span>

<span data-ttu-id="5652c-144">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span><span class="sxs-lookup"><span data-stu-id="5652c-144">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![TODO Alarm history on the solution dashboard][img-alarms]

> [!NOTE]
> <span data-ttu-id="5652c-146">These alarms are generated by a rule that is included in the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-146">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="5652c-147">This rule generates an alert when the temperature value sent by a device exceeds 60.</span><span class="sxs-lookup"><span data-stu-id="5652c-147">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="5652c-148">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="5652c-148">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="5652c-149">View devices</span><span class="sxs-lookup"><span data-stu-id="5652c-149">View devices</span></span>

<span data-ttu-id="5652c-150">The *devices* list shows all the registered devices in the solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-150">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="5652c-151">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-151">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="5652c-152">You can filter and sort the list of devices in the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-152">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="5652c-153">You can also customize the columns shown in the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-153">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="5652c-154">Choose **Devices** to show the device list for this solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-154">Choose **Devices** to show the device list for this solution.</span></span>

   ![View the device list in the solution portal][img-devicelist]

1. <span data-ttu-id="5652c-156">The device list initially shows 25 simulated devices created by the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="5652c-156">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="5652c-157">You can add additional simulated and physical devices to the solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-157">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="5652c-158">To view the details of a device, choose a device in the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-158">To view the details of a device, choose a device in the device list.</span></span>

   ![View the device details in the solution portal][img-devicedetails]

<span data-ttu-id="5652c-160">The **Device Details** panel contains six sections:</span><span class="sxs-lookup"><span data-stu-id="5652c-160">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="5652c-161">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span><span class="sxs-lookup"><span data-stu-id="5652c-161">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="5652c-162">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="5652c-162">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="5652c-163">The **Device Twin - Tags** section enables you to edit tag values for the device.</span><span class="sxs-lookup"><span data-stu-id="5652c-163">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="5652c-164">You can display tag values in the device list and use tag values to filter the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-164">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="5652c-165">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span><span class="sxs-lookup"><span data-stu-id="5652c-165">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="5652c-166">The **Device Twin - Reported Properties** section shows property values sent from the device.</span><span class="sxs-lookup"><span data-stu-id="5652c-166">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="5652c-167">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span><span class="sxs-lookup"><span data-stu-id="5652c-167">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="5652c-168">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span><span class="sxs-lookup"><span data-stu-id="5652c-168">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="5652c-169">Filter the device list</span><span class="sxs-lookup"><span data-stu-id="5652c-169">Filter the device list</span></span>

<span data-ttu-id="5652c-170">You can use a filter to display only those devices that are sending unexpected temperature values.</span><span class="sxs-lookup"><span data-stu-id="5652c-170">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="5652c-171">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span><span class="sxs-lookup"><span data-stu-id="5652c-171">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="5652c-172">You can also [create your own filters](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="5652c-172">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="5652c-173">Choose **Open saved filter** to display a list of available filters.</span><span class="sxs-lookup"><span data-stu-id="5652c-173">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="5652c-174">Then choose **Unhealthy devices** to apply the filter:</span><span class="sxs-lookup"><span data-stu-id="5652c-174">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Display the list of filters][img-unhealthy-filter]

1. <span data-ttu-id="5652c-176">The device list now shows only devices with a mean temperature value greater than 60.</span><span class="sxs-lookup"><span data-stu-id="5652c-176">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![View the filtered device list showing unhealthy devices][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="5652c-178">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="5652c-178">Update desired properties</span></span>

<span data-ttu-id="5652c-179">You have now identified a set of devices that may need remediation.</span><span class="sxs-lookup"><span data-stu-id="5652c-179">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="5652c-180">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span><span class="sxs-lookup"><span data-stu-id="5652c-180">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="5652c-181">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="5652c-181">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="5652c-182">You can push this configuration change to your remote devices from the solution portal.</span><span class="sxs-lookup"><span data-stu-id="5652c-182">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="5652c-183">You can make the change once, evaluate the impact, and then act on the results.</span><span class="sxs-lookup"><span data-stu-id="5652c-183">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="5652c-184">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-184">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="5652c-185">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span><span class="sxs-lookup"><span data-stu-id="5652c-185">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="5652c-186">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span><span class="sxs-lookup"><span data-stu-id="5652c-186">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="5652c-187">Call the job **Change telemetry interval**.</span><span class="sxs-lookup"><span data-stu-id="5652c-187">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="5652c-188">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span><span class="sxs-lookup"><span data-stu-id="5652c-188">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="5652c-189">Choose **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="5652c-189">Choose **Schedule**.</span></span>

    ![Change the TelemetryInterval property to five seconds][img-change-interval]

1. <span data-ttu-id="5652c-191">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="5652c-191">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5652c-192">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span><span class="sxs-lookup"><span data-stu-id="5652c-192">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="5652c-193">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span><span class="sxs-lookup"><span data-stu-id="5652c-193">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="5652c-194">The devices retrieve this value from the device twin and update their behavior.</span><span class="sxs-lookup"><span data-stu-id="5652c-194">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="5652c-195">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span><span class="sxs-lookup"><span data-stu-id="5652c-195">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="5652c-196">Invoke methods</span><span class="sxs-lookup"><span data-stu-id="5652c-196">Invoke methods</span></span>

<span data-ttu-id="5652c-197">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span><span class="sxs-lookup"><span data-stu-id="5652c-197">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![View the reported firmware version for the unhealthy devices][img-old-firmware]

<span data-ttu-id="5652c-199">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span><span class="sxs-lookup"><span data-stu-id="5652c-199">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="5652c-200">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span><span class="sxs-lookup"><span data-stu-id="5652c-200">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="5652c-201">From the portal, you can then remotely update all the devices still running old firmware versions:</span><span class="sxs-lookup"><span data-stu-id="5652c-201">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="5652c-202">Choose **Open saved filter** to display a list of available filters.</span><span class="sxs-lookup"><span data-stu-id="5652c-202">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="5652c-203">Then choose **Old firmware devices** to apply the filter:</span><span class="sxs-lookup"><span data-stu-id="5652c-203">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Display the list of filters][img-old-filter]

1. <span data-ttu-id="5652c-205">The device list now shows only devices with old firmware versions.</span><span class="sxs-lookup"><span data-stu-id="5652c-205">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="5652c-206">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span><span class="sxs-lookup"><span data-stu-id="5652c-206">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![View the filtered device list showing old devices][img-filtered-old-list]

1. <span data-ttu-id="5652c-208">Choose **Job Scheduler**, then **Invoke Method**.</span><span class="sxs-lookup"><span data-stu-id="5652c-208">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="5652c-209">Set **Job Name** to **Firmware update to version 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5652c-209">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="5652c-210">Choose **InitiateFirmwareUpdate** as the **Method**.</span><span class="sxs-lookup"><span data-stu-id="5652c-210">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="5652c-211">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="5652c-211">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="5652c-212">Choose **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="5652c-212">Choose **Schedule**.</span></span> <span data-ttu-id="5652c-213">The default is for the job to run now.</span><span class="sxs-lookup"><span data-stu-id="5652c-213">The default is for the job to run now.</span></span>

    ![Create job to update the firmware of the selected devices][img-method-update]

> [!NOTE]
> <span data-ttu-id="5652c-215">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span><span class="sxs-lookup"><span data-stu-id="5652c-215">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="5652c-216">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span><span class="sxs-lookup"><span data-stu-id="5652c-216">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="5652c-217">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span><span class="sxs-lookup"><span data-stu-id="5652c-217">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="5652c-218">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span><span class="sxs-lookup"><span data-stu-id="5652c-218">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="5652c-219">Choose the **Refresh** icon to update the information in the device and job lists:</span><span class="sxs-lookup"><span data-stu-id="5652c-219">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="5652c-220">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="5652c-220">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="5652c-221">In a production environment, you can schedule jobs to run during a designated maintenance window.</span><span class="sxs-lookup"><span data-stu-id="5652c-221">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="5652c-222">Scenario review</span><span class="sxs-lookup"><span data-stu-id="5652c-222">Scenario review</span></span>

<span data-ttu-id="5652c-223">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span><span class="sxs-lookup"><span data-stu-id="5652c-223">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="5652c-224">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="5652c-224">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="5652c-225">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-225">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="5652c-226">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-226">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="5652c-227">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span><span class="sxs-lookup"><span data-stu-id="5652c-227">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filter showing that all devices have up-to-date firmware][img-updated]

![Filter showing that all devices are healthy][img-healthy]

## <a name="other-features"></a><span data-ttu-id="5652c-230">Other features</span><span class="sxs-lookup"><span data-stu-id="5652c-230">Other features</span></span>

<span data-ttu-id="5652c-231">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span><span class="sxs-lookup"><span data-stu-id="5652c-231">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="5652c-232">Customize columns</span><span class="sxs-lookup"><span data-stu-id="5652c-232">Customize columns</span></span>

<span data-ttu-id="5652c-233">You can customize the information shown in the device list by choosing **Column editor**.</span><span class="sxs-lookup"><span data-stu-id="5652c-233">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="5652c-234">You can add and remove columns that display reported property and tag values.</span><span class="sxs-lookup"><span data-stu-id="5652c-234">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="5652c-235">You can also reorder and rename columns:</span><span class="sxs-lookup"><span data-stu-id="5652c-235">You can also reorder and rename columns:</span></span>

   ![Column editor ion the device list][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="5652c-237">Customize the device icon</span><span class="sxs-lookup"><span data-stu-id="5652c-237">Customize the device icon</span></span>

<span data-ttu-id="5652c-238">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span><span class="sxs-lookup"><span data-stu-id="5652c-238">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="5652c-239">Choose the pencil icon to open the **Edit image** panel for a device:</span><span class="sxs-lookup"><span data-stu-id="5652c-239">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Open device image editor][img-startimageedit]

1. <span data-ttu-id="5652c-241">Either upload a new image or use one of the existing images and then choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="5652c-241">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Edit device image editor][img-imageedit]

1. <span data-ttu-id="5652c-243">The image you selected now displays in the **Icon** column for the device.</span><span class="sxs-lookup"><span data-stu-id="5652c-243">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="5652c-244">The image is stored in blob storage.</span><span class="sxs-lookup"><span data-stu-id="5652c-244">The image is stored in blob storage.</span></span> <span data-ttu-id="5652c-245">A tag in the device twin contains a link to the image in blob storage.</span><span class="sxs-lookup"><span data-stu-id="5652c-245">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="5652c-246">Add a device</span><span class="sxs-lookup"><span data-stu-id="5652c-246">Add a device</span></span>

<span data-ttu-id="5652c-247">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-247">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="5652c-248">These devices are *simulated devices* running in an Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="5652c-248">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="5652c-249">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-249">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="5652c-250">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5652c-250">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="5652c-251">The following steps show you how to add a simulated device to the solution:</span><span class="sxs-lookup"><span data-stu-id="5652c-251">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="5652c-252">Navigate back to the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-252">Navigate back to the device list.</span></span>

1. <span data-ttu-id="5652c-253">To add a device, choose **+ Add A Device** in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="5652c-253">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Add a device to the preconfigured solution][img-adddevice]

1. <span data-ttu-id="5652c-255">Choose **Add New** on the **Simulated Device** tile.</span><span class="sxs-lookup"><span data-stu-id="5652c-255">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Set new device details in dashboard][img-addnew]

   <span data-ttu-id="5652c-257">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span><span class="sxs-lookup"><span data-stu-id="5652c-257">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="5652c-258">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="5652c-258">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="5652c-259">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="5652c-259">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="5652c-260">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="5652c-260">Choose **Create**.</span></span>

   ![Save a new device][img-definedevice]

1. <span data-ttu-id="5652c-262">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-262">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="5652c-263">You can view your device **Running** in the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-263">You can view your device **Running** in the device list.</span></span>

    ![View new device in device list][img-runningnew]

1. <span data-ttu-id="5652c-265">You can also view the simulated telemetry from your new device on the dashboard:</span><span class="sxs-lookup"><span data-stu-id="5652c-265">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![View telemetry from new device][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="5652c-267">Disable and delete a device</span><span class="sxs-lookup"><span data-stu-id="5652c-267">Disable and delete a device</span></span>

<span data-ttu-id="5652c-268">You can disable a device, and after it is disabled you can remove it:</span><span class="sxs-lookup"><span data-stu-id="5652c-268">You can disable a device, and after it is disabled you can remove it:</span></span>

![Disable and remove a device][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="5652c-270">Add a rule</span><span class="sxs-lookup"><span data-stu-id="5652c-270">Add a rule</span></span>

<span data-ttu-id="5652c-271">There are no rules for the new device you just added.</span><span class="sxs-lookup"><span data-stu-id="5652c-271">There are no rules for the new device you just added.</span></span> <span data-ttu-id="5652c-272">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span><span class="sxs-lookup"><span data-stu-id="5652c-272">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="5652c-273">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span><span class="sxs-lookup"><span data-stu-id="5652c-273">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="5652c-274">Navigate back to the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-274">Navigate back to the device list.</span></span>

1. <span data-ttu-id="5652c-275">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span><span class="sxs-lookup"><span data-stu-id="5652c-275">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="5652c-276">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span><span class="sxs-lookup"><span data-stu-id="5652c-276">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Add a device rule][img-adddevicerule]

1. <span data-ttu-id="5652c-278">To save your changes, choose **Save and View Rules**.</span><span class="sxs-lookup"><span data-stu-id="5652c-278">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="5652c-279">Choose **Commands** in the device details pane for the new device.</span><span class="sxs-lookup"><span data-stu-id="5652c-279">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Add a device rule][img-adddevicerule2]

1. <span data-ttu-id="5652c-281">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span><span class="sxs-lookup"><span data-stu-id="5652c-281">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="5652c-282">Then choose **Send Command**:</span><span class="sxs-lookup"><span data-stu-id="5652c-282">Then choose **Send Command**:</span></span>

    ![Add a device rule][img-adddevicerule3]

1. <span data-ttu-id="5652c-284">Navigate back to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="5652c-284">Navigate back to the dashboard.</span></span> <span data-ttu-id="5652c-285">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span><span class="sxs-lookup"><span data-stu-id="5652c-285">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Add a device rule][img-adddevicerule4]

1. <span data-ttu-id="5652c-287">You can review and edit all your rules on the **Rules** page of the dashboard:</span><span class="sxs-lookup"><span data-stu-id="5652c-287">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![List device rules][img-rules]

1. <span data-ttu-id="5652c-289">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span><span class="sxs-lookup"><span data-stu-id="5652c-289">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![List device actions][img-actions]

> [!NOTE]
> <span data-ttu-id="5652c-291">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="5652c-291">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="5652c-292">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="5652c-292">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="5652c-293">Manage filters</span><span class="sxs-lookup"><span data-stu-id="5652c-293">Manage filters</span></span>

<span data-ttu-id="5652c-294">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span><span class="sxs-lookup"><span data-stu-id="5652c-294">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="5652c-295">To create a filter:</span><span class="sxs-lookup"><span data-stu-id="5652c-295">To create a filter:</span></span>

1. <span data-ttu-id="5652c-296">Choose the edit filter icon above the list of devices:</span><span class="sxs-lookup"><span data-stu-id="5652c-296">Choose the edit filter icon above the list of devices:</span></span>

    ![Open the filter editor][img-editfiltericon]

1. <span data-ttu-id="5652c-298">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span><span class="sxs-lookup"><span data-stu-id="5652c-298">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="5652c-299">You can add multiple clauses to refine your filter.</span><span class="sxs-lookup"><span data-stu-id="5652c-299">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="5652c-300">Choose **Filter** to apply the filter:</span><span class="sxs-lookup"><span data-stu-id="5652c-300">Choose **Filter** to apply the filter:</span></span>

    ![Create a filter][img-filtereditor]

1. <span data-ttu-id="5652c-302">In this example, the list is filtered by manufacturer and model number:</span><span class="sxs-lookup"><span data-stu-id="5652c-302">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Filtered list][img-filterelist]

1. <span data-ttu-id="5652c-304">To save your filter with a custom name, choose the **Save as** icon:</span><span class="sxs-lookup"><span data-stu-id="5652c-304">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Save a filter][img-savefilter]

1. <span data-ttu-id="5652c-306">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span><span class="sxs-lookup"><span data-stu-id="5652c-306">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Open a filter][img-openfilter]

<span data-ttu-id="5652c-308">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span><span class="sxs-lookup"><span data-stu-id="5652c-308">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="5652c-309">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="5652c-309">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="5652c-310">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span><span class="sxs-lookup"><span data-stu-id="5652c-310">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="5652c-311">Commands</span><span class="sxs-lookup"><span data-stu-id="5652c-311">Commands</span></span>

<span data-ttu-id="5652c-312">From the **Device Details** panel, you can send commands to the device.</span><span class="sxs-lookup"><span data-stu-id="5652c-312">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="5652c-313">When a device first starts, it sends information about the commands it supports to the solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-313">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="5652c-314">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="5652c-314">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="5652c-315">Choose **Commands** in the **Device Details** panel for the selected device:</span><span class="sxs-lookup"><span data-stu-id="5652c-315">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Device commands in dashboard][img-devicecommands]

1. <span data-ttu-id="5652c-317">Select **PingDevice** from the command list.</span><span class="sxs-lookup"><span data-stu-id="5652c-317">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="5652c-318">Choose **Send Command**.</span><span class="sxs-lookup"><span data-stu-id="5652c-318">Choose **Send Command**.</span></span>

1. <span data-ttu-id="5652c-319">You can see the status of the command in the command history.</span><span class="sxs-lookup"><span data-stu-id="5652c-319">You can see the status of the command in the command history.</span></span>

   ![Command status in dashboard][img-pingcommand]

<span data-ttu-id="5652c-321">The solution tracks the status of each command it sends.</span><span class="sxs-lookup"><span data-stu-id="5652c-321">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="5652c-322">Initially the result is **Pending**.</span><span class="sxs-lookup"><span data-stu-id="5652c-322">Initially the result is **Pending**.</span></span> <span data-ttu-id="5652c-323">When the device reports that it has executed the command, the result is set to **Success**.</span><span class="sxs-lookup"><span data-stu-id="5652c-323">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="5652c-324">Behind the scenes</span><span class="sxs-lookup"><span data-stu-id="5652c-324">Behind the scenes</span></span>

<span data-ttu-id="5652c-325">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span><span class="sxs-lookup"><span data-stu-id="5652c-325">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="5652c-326">You can view these resources in the Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="5652c-326">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="5652c-327">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="5652c-327">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Preconfigured solution in the Azure portal][img-portal]

<span data-ttu-id="5652c-329">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="5652c-329">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="5652c-330">You can also view the source code for the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-330">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="5652c-331">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="5652c-331">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="5652c-332">The **DeviceAdministration** folder contains the source code for the dashboard.</span><span class="sxs-lookup"><span data-stu-id="5652c-332">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="5652c-333">The **Simulator** folder contains the source code for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="5652c-333">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="5652c-334">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span><span class="sxs-lookup"><span data-stu-id="5652c-334">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="5652c-335">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="5652c-335">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="5652c-336">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="5652c-336">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="5652c-337">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span><span class="sxs-lookup"><span data-stu-id="5652c-337">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5652c-338">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5652c-338">Next Steps</span></span>

<span data-ttu-id="5652c-339">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="5652c-339">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="5652c-340">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="5652c-340">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="5652c-341">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="5652c-341">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="5652c-342">[Permissions on the azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="5652c-342">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md








































