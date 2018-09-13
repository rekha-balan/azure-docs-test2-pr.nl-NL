---
title: Get started with preconfigured solutions | Microsoft Docs
description: Follow this tutorial to learn how to deploy an Azure IoT Suite preconfigured solution.
services: iot-suite
ms.service: iot-suite
author: dominicbetts
ms.topic: conceptual
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 0c499d5f4d1d6256294e25921cef1fb0dfed0c05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868830"
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="74c53-103">Get started with the preconfigured solutions</span><span class="sxs-lookup"><span data-stu-id="74c53-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="74c53-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span><span class="sxs-lookup"><span data-stu-id="74c53-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="74c53-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="74c53-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span><span class="sxs-lookup"><span data-stu-id="74c53-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="74c53-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="74c53-108">It also walks you through the basic features of the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="74c53-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="74c53-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Remote monitoring preconfigured solution dashboard][img-dashboard]

<span data-ttu-id="74c53-111">To complete this tutorial, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="74c53-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="74c53-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="74c53-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="74c53-113">For details, see [Azure Free Trial][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="74c53-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="74c53-114">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="74c53-114">Scenario overview</span></span>

<span data-ttu-id="74c53-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span><span class="sxs-lookup"><span data-stu-id="74c53-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="74c53-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span><span class="sxs-lookup"><span data-stu-id="74c53-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="74c53-117">The following sections show you how to:</span><span class="sxs-lookup"><span data-stu-id="74c53-117">The following sections show you how to:</span></span>

* <span data-ttu-id="74c53-118">Identify the devices sending unexpected temperature values.</span><span class="sxs-lookup"><span data-stu-id="74c53-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="74c53-119">Configure these devices to send more detailed telemetry.</span><span class="sxs-lookup"><span data-stu-id="74c53-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="74c53-120">Fix the problem by updating the firmware on these devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="74c53-121">Verify that your action has resolved the issue.</span><span class="sxs-lookup"><span data-stu-id="74c53-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="74c53-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="74c53-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="74c53-123">You do not need physical access to the devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="74c53-124">View the solution dashboard</span><span class="sxs-lookup"><span data-stu-id="74c53-124">View the solution dashboard</span></span>

<span data-ttu-id="74c53-125">The solution dashboard enables you to manage the deployed solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="74c53-126">For example, you can view telemetry, add devices, and configure rules.</span><span class="sxs-lookup"><span data-stu-id="74c53-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="74c53-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span><span class="sxs-lookup"><span data-stu-id="74c53-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Launch the preconfigured solution][img-launch-solution]

1. <span data-ttu-id="74c53-129">By default, the solution portal shows the *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="74c53-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="74c53-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span><span class="sxs-lookup"><span data-stu-id="74c53-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Remote monitoring preconfigured solution dashboard][img-menu]

<span data-ttu-id="74c53-132">The dashboard displays the following information:</span><span class="sxs-lookup"><span data-stu-id="74c53-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="74c53-133">A map that displays the location of each device connected to the solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="74c53-134">When you first run the solution, there are 25 simulated devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="74c53-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span><span class="sxs-lookup"><span data-stu-id="74c53-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="74c53-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span><span class="sxs-lookup"><span data-stu-id="74c53-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="74c53-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span><span class="sxs-lookup"><span data-stu-id="74c53-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="74c53-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span><span class="sxs-lookup"><span data-stu-id="74c53-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="74c53-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="74c53-140">A **Jobs** panel that displays information about scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="74c53-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="74c53-141">You can schedule your own jobs on **Management jobs** page.</span><span class="sxs-lookup"><span data-stu-id="74c53-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="74c53-142">View alarms</span><span class="sxs-lookup"><span data-stu-id="74c53-142">View alarms</span></span>

<span data-ttu-id="74c53-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span><span class="sxs-lookup"><span data-stu-id="74c53-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![TODO Alarm history on the solution dashboard][img-alarms]

> [!NOTE]
> <span data-ttu-id="74c53-145">These alarms are generated by a rule that is included in the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="74c53-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span><span class="sxs-lookup"><span data-stu-id="74c53-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="74c53-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="74c53-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="74c53-148">View devices</span><span class="sxs-lookup"><span data-stu-id="74c53-148">View devices</span></span>

<span data-ttu-id="74c53-149">The *devices* list shows all the registered devices in the solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="74c53-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="74c53-151">You can filter and sort the list of devices in the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="74c53-152">You can also customize the columns shown in the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="74c53-153">Choose **Devices** to show the device list for this solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![View the device list in the solution portal][img-devicelist]

1. <span data-ttu-id="74c53-155">The device list initially shows 25 simulated devices created by the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="74c53-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="74c53-156">You can add additional simulated and physical devices to the solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="74c53-157">To view the details of a device, choose a device in the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-157">To view the details of a device, choose a device in the device list.</span></span>

   ![View the device details in the solution portal][img-devicedetails]

<span data-ttu-id="74c53-159">The **Device Details** panel contains six sections:</span><span class="sxs-lookup"><span data-stu-id="74c53-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="74c53-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span><span class="sxs-lookup"><span data-stu-id="74c53-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="74c53-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="74c53-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="74c53-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span><span class="sxs-lookup"><span data-stu-id="74c53-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="74c53-163">You can display tag values in the device list and use tag values to filter the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="74c53-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span><span class="sxs-lookup"><span data-stu-id="74c53-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="74c53-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span><span class="sxs-lookup"><span data-stu-id="74c53-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="74c53-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span><span class="sxs-lookup"><span data-stu-id="74c53-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="74c53-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span><span class="sxs-lookup"><span data-stu-id="74c53-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="74c53-168">Filter the device list</span><span class="sxs-lookup"><span data-stu-id="74c53-168">Filter the device list</span></span>

<span data-ttu-id="74c53-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span><span class="sxs-lookup"><span data-stu-id="74c53-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="74c53-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span><span class="sxs-lookup"><span data-stu-id="74c53-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="74c53-171">You can also [create your own filters](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="74c53-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="74c53-172">Choose **Open saved filter** to display a list of available filters.</span><span class="sxs-lookup"><span data-stu-id="74c53-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="74c53-173">Then choose **Unhealthy devices** to apply the filter:</span><span class="sxs-lookup"><span data-stu-id="74c53-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Display the list of filters][img-unhealthy-filter]

1. <span data-ttu-id="74c53-175">The device list now shows only devices with a mean temperature value greater than 60.</span><span class="sxs-lookup"><span data-stu-id="74c53-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![View the filtered device list showing unhealthy devices][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="74c53-177">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="74c53-177">Update desired properties</span></span>

<span data-ttu-id="74c53-178">You have now identified a set of devices that may need remediation.</span><span class="sxs-lookup"><span data-stu-id="74c53-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="74c53-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span><span class="sxs-lookup"><span data-stu-id="74c53-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="74c53-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="74c53-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="74c53-181">You can push this configuration change to your remote devices from the solution portal.</span><span class="sxs-lookup"><span data-stu-id="74c53-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="74c53-182">You can make the change once, evaluate the impact, and then act on the results.</span><span class="sxs-lookup"><span data-stu-id="74c53-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="74c53-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="74c53-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span><span class="sxs-lookup"><span data-stu-id="74c53-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="74c53-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span><span class="sxs-lookup"><span data-stu-id="74c53-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="74c53-186">Call the job **Change telemetry interval**.</span><span class="sxs-lookup"><span data-stu-id="74c53-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="74c53-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span><span class="sxs-lookup"><span data-stu-id="74c53-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="74c53-188">Choose **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="74c53-188">Choose **Schedule**.</span></span>

    ![Change the TelemetryInterval property to five seconds][img-change-interval]

1. <span data-ttu-id="74c53-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="74c53-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="74c53-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span><span class="sxs-lookup"><span data-stu-id="74c53-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="74c53-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span><span class="sxs-lookup"><span data-stu-id="74c53-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="74c53-193">The devices retrieve this value from the device twin and update their behavior.</span><span class="sxs-lookup"><span data-stu-id="74c53-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="74c53-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span><span class="sxs-lookup"><span data-stu-id="74c53-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="74c53-195">Invoke methods</span><span class="sxs-lookup"><span data-stu-id="74c53-195">Invoke methods</span></span>

<span data-ttu-id="74c53-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span><span class="sxs-lookup"><span data-stu-id="74c53-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![View the reported firmware version for the unhealthy devices][img-old-firmware]

<span data-ttu-id="74c53-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span><span class="sxs-lookup"><span data-stu-id="74c53-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="74c53-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span><span class="sxs-lookup"><span data-stu-id="74c53-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="74c53-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span><span class="sxs-lookup"><span data-stu-id="74c53-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="74c53-201">Choose **Open saved filter** to display a list of available filters.</span><span class="sxs-lookup"><span data-stu-id="74c53-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="74c53-202">Then choose **Old firmware devices** to apply the filter:</span><span class="sxs-lookup"><span data-stu-id="74c53-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Display the list of filters][img-old-filter]

1. <span data-ttu-id="74c53-204">The device list now shows only devices with old firmware versions.</span><span class="sxs-lookup"><span data-stu-id="74c53-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="74c53-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span><span class="sxs-lookup"><span data-stu-id="74c53-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![View the filtered device list showing old devices][img-filtered-old-list]

1. <span data-ttu-id="74c53-207">Choose **Job Scheduler**, then **Invoke Method**.</span><span class="sxs-lookup"><span data-stu-id="74c53-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="74c53-208">Set **Job Name** to **Firmware update to version 2.0**.</span><span class="sxs-lookup"><span data-stu-id="74c53-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="74c53-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span><span class="sxs-lookup"><span data-stu-id="74c53-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="74c53-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="74c53-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="74c53-211">Choose **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="74c53-211">Choose **Schedule**.</span></span> <span data-ttu-id="74c53-212">The default is for the job to run now.</span><span class="sxs-lookup"><span data-stu-id="74c53-212">The default is for the job to run now.</span></span>

    ![Create job to update the firmware of the selected devices][img-method-update]

> [!NOTE]
> <span data-ttu-id="74c53-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span><span class="sxs-lookup"><span data-stu-id="74c53-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="74c53-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span><span class="sxs-lookup"><span data-stu-id="74c53-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="74c53-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span><span class="sxs-lookup"><span data-stu-id="74c53-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="74c53-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span><span class="sxs-lookup"><span data-stu-id="74c53-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="74c53-218">Choose the **Refresh** icon to update the information in the device and job lists:</span><span class="sxs-lookup"><span data-stu-id="74c53-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="74c53-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="74c53-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="74c53-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span><span class="sxs-lookup"><span data-stu-id="74c53-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="74c53-221">Scenario review</span><span class="sxs-lookup"><span data-stu-id="74c53-221">Scenario review</span></span>

<span data-ttu-id="74c53-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span><span class="sxs-lookup"><span data-stu-id="74c53-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="74c53-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="74c53-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="74c53-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="74c53-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="74c53-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span><span class="sxs-lookup"><span data-stu-id="74c53-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filter showing that all devices have up-to-date firmware][img-updated]

![Filter showing that all devices are healthy][img-healthy]

## <a name="other-features"></a><span data-ttu-id="74c53-229">Other features</span><span class="sxs-lookup"><span data-stu-id="74c53-229">Other features</span></span>

<span data-ttu-id="74c53-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span><span class="sxs-lookup"><span data-stu-id="74c53-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="74c53-231">Customize columns</span><span class="sxs-lookup"><span data-stu-id="74c53-231">Customize columns</span></span>

<span data-ttu-id="74c53-232">You can customize the information shown in the device list by choosing **Column editor**.</span><span class="sxs-lookup"><span data-stu-id="74c53-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="74c53-233">You can add and remove columns that display reported property and tag values.</span><span class="sxs-lookup"><span data-stu-id="74c53-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="74c53-234">You can also reorder and rename columns:</span><span class="sxs-lookup"><span data-stu-id="74c53-234">You can also reorder and rename columns:</span></span>

   ![Column editor ion the device list][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="74c53-236">Customize the device icon</span><span class="sxs-lookup"><span data-stu-id="74c53-236">Customize the device icon</span></span>

<span data-ttu-id="74c53-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span><span class="sxs-lookup"><span data-stu-id="74c53-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="74c53-238">Choose the pencil icon to open the **Edit image** panel for a device:</span><span class="sxs-lookup"><span data-stu-id="74c53-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Open device image editor][img-startimageedit]

1. <span data-ttu-id="74c53-240">Either upload a new image or use one of the existing images and then choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="74c53-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Edit device image editor][img-imageedit]

1. <span data-ttu-id="74c53-242">The image you selected now displays in the **Icon** column for the device.</span><span class="sxs-lookup"><span data-stu-id="74c53-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="74c53-243">The image is stored in blob storage.</span><span class="sxs-lookup"><span data-stu-id="74c53-243">The image is stored in blob storage.</span></span> <span data-ttu-id="74c53-244">A tag in the device twin contains a link to the image in blob storage.</span><span class="sxs-lookup"><span data-stu-id="74c53-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="74c53-245">Add a device</span><span class="sxs-lookup"><span data-stu-id="74c53-245">Add a device</span></span>

<span data-ttu-id="74c53-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="74c53-247">These devices are *simulated devices* running in an Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="74c53-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="74c53-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="74c53-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="74c53-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="74c53-250">The following steps show you how to add a simulated device to the solution:</span><span class="sxs-lookup"><span data-stu-id="74c53-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="74c53-251">Navigate back to the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="74c53-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="74c53-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Add a device to the preconfigured solution][img-adddevice]

1. <span data-ttu-id="74c53-254">Choose **Add New** on the **Simulated Device** tile.</span><span class="sxs-lookup"><span data-stu-id="74c53-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Set new device details in dashboard][img-addnew]

   <span data-ttu-id="74c53-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span><span class="sxs-lookup"><span data-stu-id="74c53-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="74c53-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="74c53-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="74c53-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="74c53-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="74c53-259">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="74c53-259">Choose **Create**.</span></span>

   ![Save a new device][img-definedevice]

1. <span data-ttu-id="74c53-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="74c53-262">You can view your device **Running** in the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-262">You can view your device **Running** in the device list.</span></span>

    ![View new device in device list][img-runningnew]

1. <span data-ttu-id="74c53-264">You can also view the simulated telemetry from your new device on the dashboard:</span><span class="sxs-lookup"><span data-stu-id="74c53-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![View telemetry from new device][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="74c53-266">Disable and delete a device</span><span class="sxs-lookup"><span data-stu-id="74c53-266">Disable and delete a device</span></span>

<span data-ttu-id="74c53-267">You can disable a device, and after it is disabled you can remove it:</span><span class="sxs-lookup"><span data-stu-id="74c53-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Disable and remove a device][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="74c53-269">Add a rule</span><span class="sxs-lookup"><span data-stu-id="74c53-269">Add a rule</span></span>

<span data-ttu-id="74c53-270">There are no rules for the new device you just added.</span><span class="sxs-lookup"><span data-stu-id="74c53-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="74c53-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span><span class="sxs-lookup"><span data-stu-id="74c53-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="74c53-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span><span class="sxs-lookup"><span data-stu-id="74c53-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="74c53-273">Navigate back to the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="74c53-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span><span class="sxs-lookup"><span data-stu-id="74c53-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="74c53-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span><span class="sxs-lookup"><span data-stu-id="74c53-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Add a device rule][img-adddevicerule]

1. <span data-ttu-id="74c53-277">To save your changes, choose **Save and View Rules**.</span><span class="sxs-lookup"><span data-stu-id="74c53-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="74c53-278">Choose **Commands** in the device details pane for the new device.</span><span class="sxs-lookup"><span data-stu-id="74c53-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Add a device rule][img-adddevicerule2]

1. <span data-ttu-id="74c53-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span><span class="sxs-lookup"><span data-stu-id="74c53-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="74c53-281">Then choose **Send Command**:</span><span class="sxs-lookup"><span data-stu-id="74c53-281">Then choose **Send Command**:</span></span>

    ![Add a device rule][img-adddevicerule3]

1. <span data-ttu-id="74c53-283">Navigate back to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74c53-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="74c53-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span><span class="sxs-lookup"><span data-stu-id="74c53-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Add a device rule][img-adddevicerule4]

1. <span data-ttu-id="74c53-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span><span class="sxs-lookup"><span data-stu-id="74c53-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![List device rules][img-rules]

1. <span data-ttu-id="74c53-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span><span class="sxs-lookup"><span data-stu-id="74c53-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![List device actions][img-actions]

> [!NOTE]
> <span data-ttu-id="74c53-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="74c53-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="74c53-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="74c53-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="74c53-292">Manage filters</span><span class="sxs-lookup"><span data-stu-id="74c53-292">Manage filters</span></span>

<span data-ttu-id="74c53-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span><span class="sxs-lookup"><span data-stu-id="74c53-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="74c53-294">To create a filter:</span><span class="sxs-lookup"><span data-stu-id="74c53-294">To create a filter:</span></span>

1. <span data-ttu-id="74c53-295">Choose the edit filter icon above the list of devices:</span><span class="sxs-lookup"><span data-stu-id="74c53-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Open the filter editor][img-editfiltericon]

1. <span data-ttu-id="74c53-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span><span class="sxs-lookup"><span data-stu-id="74c53-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="74c53-298">You can add multiple clauses to refine your filter.</span><span class="sxs-lookup"><span data-stu-id="74c53-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="74c53-299">Choose **Filter** to apply the filter:</span><span class="sxs-lookup"><span data-stu-id="74c53-299">Choose **Filter** to apply the filter:</span></span>

    ![Create a filter][img-filtereditor]

1. <span data-ttu-id="74c53-301">In this example, the list is filtered by manufacturer and model number:</span><span class="sxs-lookup"><span data-stu-id="74c53-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Filtered list][img-filterelist]

1. <span data-ttu-id="74c53-303">To save your filter with a custom name, choose the **Save as** icon:</span><span class="sxs-lookup"><span data-stu-id="74c53-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Save a filter][img-savefilter]

1. <span data-ttu-id="74c53-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span><span class="sxs-lookup"><span data-stu-id="74c53-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Open a filter][img-openfilter]

<span data-ttu-id="74c53-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span><span class="sxs-lookup"><span data-stu-id="74c53-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="74c53-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="74c53-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="74c53-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span><span class="sxs-lookup"><span data-stu-id="74c53-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="74c53-310">Commands</span><span class="sxs-lookup"><span data-stu-id="74c53-310">Commands</span></span>

<span data-ttu-id="74c53-311">From the **Device Details** panel, you can send commands to the device.</span><span class="sxs-lookup"><span data-stu-id="74c53-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="74c53-312">When a device first starts, it sends information about the commands it supports to the solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="74c53-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="74c53-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="74c53-314">Choose **Commands** in the **Device Details** panel for the selected device:</span><span class="sxs-lookup"><span data-stu-id="74c53-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Device commands in dashboard][img-devicecommands]

1. <span data-ttu-id="74c53-316">Select **PingDevice** from the command list.</span><span class="sxs-lookup"><span data-stu-id="74c53-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="74c53-317">Choose **Send Command**.</span><span class="sxs-lookup"><span data-stu-id="74c53-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="74c53-318">You can see the status of the command in the command history.</span><span class="sxs-lookup"><span data-stu-id="74c53-318">You can see the status of the command in the command history.</span></span>

   ![Command status in dashboard][img-pingcommand]

<span data-ttu-id="74c53-320">The solution tracks the status of each command it sends.</span><span class="sxs-lookup"><span data-stu-id="74c53-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="74c53-321">Initially the result is **Pending**.</span><span class="sxs-lookup"><span data-stu-id="74c53-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="74c53-322">When the device reports that it has executed the command, the result is set to **Success**.</span><span class="sxs-lookup"><span data-stu-id="74c53-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="74c53-323">Behind the scenes</span><span class="sxs-lookup"><span data-stu-id="74c53-323">Behind the scenes</span></span>

<span data-ttu-id="74c53-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span><span class="sxs-lookup"><span data-stu-id="74c53-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="74c53-325">You can view these resources in the Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="74c53-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="74c53-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="74c53-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Preconfigured solution in the Azure portal][img-portal]

<span data-ttu-id="74c53-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="74c53-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="74c53-329">You can also view the source code for the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="74c53-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="74c53-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="74c53-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74c53-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="74c53-332">The **Simulator** folder contains the source code for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="74c53-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="74c53-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span><span class="sxs-lookup"><span data-stu-id="74c53-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="74c53-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="74c53-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="74c53-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="74c53-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="74c53-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span><span class="sxs-lookup"><span data-stu-id="74c53-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74c53-337">Next Steps</span><span class="sxs-lookup"><span data-stu-id="74c53-337">Next Steps</span></span>

<span data-ttu-id="74c53-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="74c53-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="74c53-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="74c53-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="74c53-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="74c53-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="74c53-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="74c53-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-v1-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-v1-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-v1-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-v1-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-v1-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-v1-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-v1-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-v1-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-v1-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-v1-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-v1-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-v1-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-v1-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-v1-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-v1-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-v1-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-v1-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-v1-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-v1-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-v1-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-v1-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-v1-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-v1-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-v1-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-v1-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-v1-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-v1-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-v1-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-v1-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-v1-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-v1-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-v1-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-v1-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-v1-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-v1-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-v1-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-v1-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-v1-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-v1-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-v1-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-v1-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-v1-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-v1-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-v1-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-v1-connecting-devices.md
[lnk-permissions]: iot-suite-v1-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-v1-faq.md