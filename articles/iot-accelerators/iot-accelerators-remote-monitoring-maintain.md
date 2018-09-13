---
title: Use alerts and fix device issues in the remote monitoring solution tutorial - Azure | Microsoft Docs
description: This tutorial shows you how to Use alerts to identify and fix issues with devices connected to the Remote Monitoring solution accelerator.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 07/19/2018
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 3138f0ebb6316e69c873a37d479ddc0279a361ef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968020"
---
# <a name="tutorial-troubleshoot-and-fix-device-issues"></a><span data-ttu-id="d790e-103">Tutorial: Troubleshoot and fix device issues</span><span class="sxs-lookup"><span data-stu-id="d790e-103">Tutorial: Troubleshoot and fix device issues</span></span>

<span data-ttu-id="d790e-104">In this tutorial, you use the Remote Monitoring solution accelerator to identify and fix issues with your connected IoT devices.</span><span class="sxs-lookup"><span data-stu-id="d790e-104">In this tutorial, you use the Remote Monitoring solution accelerator to identify and fix issues with your connected IoT devices.</span></span> <span data-ttu-id="d790e-105">You use alerts in the solution accelerator dashboard to identify issues and then run remote jobs to fix those issues.</span><span class="sxs-lookup"><span data-stu-id="d790e-105">You use alerts in the solution accelerator dashboard to identify issues and then run remote jobs to fix those issues.</span></span>

<span data-ttu-id="d790e-106">Contoso is testing a new **Prototype** device in the field.</span><span class="sxs-lookup"><span data-stu-id="d790e-106">Contoso is testing a new **Prototype** device in the field.</span></span> <span data-ttu-id="d790e-107">As a Contoso operator, you notice during testing that the **Prototype** device is unexpectedly triggering a temperature alert on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="d790e-107">As a Contoso operator, you notice during testing that the **Prototype** device is unexpectedly triggering a temperature alert on the dashboard.</span></span> <span data-ttu-id="d790e-108">You must now investigate the behavior of this faulty **Prototype** device and resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="d790e-108">You must now investigate the behavior of this faulty **Prototype** device and resolve the issue.</span></span>

<span data-ttu-id="d790e-109">In this tutorial, you:</span><span class="sxs-lookup"><span data-stu-id="d790e-109">In this tutorial, you:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="d790e-110">Investigate an alert from a device</span><span class="sxs-lookup"><span data-stu-id="d790e-110">Investigate an alert from a device</span></span>
> * <span data-ttu-id="d790e-111">Resolve the issue with the device</span><span class="sxs-lookup"><span data-stu-id="d790e-111">Resolve the issue with the device</span></span>

<span data-ttu-id="d790e-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="d790e-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [iot-accelerators-tutorial-prereqs](../../includes/iot-accelerators-tutorial-prereqs.md)]

## <a name="investigate-an-alert"></a><span data-ttu-id="d790e-113">Investigate an alert</span><span class="sxs-lookup"><span data-stu-id="d790e-113">Investigate an alert</span></span>

<span data-ttu-id="d790e-114">On the **Dashboard** page you notice there are unexpected temperature alerts coming from the rule associated with the **Prototype** devices:</span><span class="sxs-lookup"><span data-stu-id="d790e-114">On the **Dashboard** page you notice there are unexpected temperature alerts coming from the rule associated with the **Prototype** devices:</span></span>

<span data-ttu-id="d790e-115">[![Alerts showing on the dashboard](./media/iot-accelerators-remote-monitoring-maintain/dashboardalarm-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/dashboardalarm-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-115">[![Alerts showing on the dashboard](./media/iot-accelerators-remote-monitoring-maintain/dashboardalarm-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/dashboardalarm-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-116">To investigate the issue further, choose the **Explore Alert** option next to the alert:</span><span class="sxs-lookup"><span data-stu-id="d790e-116">To investigate the issue further, choose the **Explore Alert** option next to the alert:</span></span>

<span data-ttu-id="d790e-117">[![Explore alert from the dashboard](./media/iot-accelerators-remote-monitoring-maintain/dashboardexplorealarm-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/dashboardexplorealarm-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-117">[![Explore alert from the dashboard](./media/iot-accelerators-remote-monitoring-maintain/dashboardexplorealarm-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/dashboardexplorealarm-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-118">The detail view of the alert shows:</span><span class="sxs-lookup"><span data-stu-id="d790e-118">The detail view of the alert shows:</span></span>

* <span data-ttu-id="d790e-119">When the alert was triggered</span><span class="sxs-lookup"><span data-stu-id="d790e-119">When the alert was triggered</span></span>
* <span data-ttu-id="d790e-120">Status information about the devices associated with the alert</span><span class="sxs-lookup"><span data-stu-id="d790e-120">Status information about the devices associated with the alert</span></span>
* <span data-ttu-id="d790e-121">Telemetry from the devices associated with the alert</span><span class="sxs-lookup"><span data-stu-id="d790e-121">Telemetry from the devices associated with the alert</span></span>

<span data-ttu-id="d790e-122">[![Alert details](./media/iot-accelerators-remote-monitoring-maintain/maintenancealarmdetail-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancealarmdetail-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-122">[![Alert details](./media/iot-accelerators-remote-monitoring-maintain/maintenancealarmdetail-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancealarmdetail-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-123">To acknowledge the alert, select all the **Alert occurrences** and choose **Acknowledge**.</span><span class="sxs-lookup"><span data-stu-id="d790e-123">To acknowledge the alert, select all the **Alert occurrences** and choose **Acknowledge**.</span></span> <span data-ttu-id="d790e-124">This action lets other operators know that you have seen the alert and are working on it:</span><span class="sxs-lookup"><span data-stu-id="d790e-124">This action lets other operators know that you have seen the alert and are working on it:</span></span>

<span data-ttu-id="d790e-125">[![Acknowledge the alerts](./media/iot-accelerators-remote-monitoring-maintain/maintenanceacknowledge-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenanceacknowledge-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-125">[![Acknowledge the alerts](./media/iot-accelerators-remote-monitoring-maintain/maintenanceacknowledge-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenanceacknowledge-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-126">When you acknowledge the alert, the status of the occurrence changes to **Acknowledged**.</span><span class="sxs-lookup"><span data-stu-id="d790e-126">When you acknowledge the alert, the status of the occurrence changes to **Acknowledged**.</span></span>

<span data-ttu-id="d790e-127">In the list of alerted devices, you can see the **Prototype** device responsible for firing the temperature alert:</span><span class="sxs-lookup"><span data-stu-id="d790e-127">In the list of alerted devices, you can see the **Prototype** device responsible for firing the temperature alert:</span></span>

<span data-ttu-id="d790e-128">[![List the devices causing the alert](./media/iot-accelerators-remote-monitoring-maintain/maintenanceresponsibledevice-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenanceresponsibledevice-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-128">[![List the devices causing the alert](./media/iot-accelerators-remote-monitoring-maintain/maintenanceresponsibledevice-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenanceresponsibledevice-expanded.png#lightbox)</span></span>

## <a name="resolve-the-issue"></a><span data-ttu-id="d790e-129">Resolve the issue</span><span class="sxs-lookup"><span data-stu-id="d790e-129">Resolve the issue</span></span>

<span data-ttu-id="d790e-130">To resolve the issue with the **Prototype** device, you need to call the **DecreaseTemperature** method on the device.</span><span class="sxs-lookup"><span data-stu-id="d790e-130">To resolve the issue with the **Prototype** device, you need to call the **DecreaseTemperature** method on the device.</span></span>

<span data-ttu-id="d790e-131">To act on a device, select it in the list of alerted devices and then choose **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="d790e-131">To act on a device, select it in the list of alerted devices and then choose **Jobs**.</span></span> <span data-ttu-id="d790e-132">The **Prototype** device model supports six methods:</span><span class="sxs-lookup"><span data-stu-id="d790e-132">The **Prototype** device model supports six methods:</span></span>

<span data-ttu-id="d790e-133">[![View the methods the device supports](./media/iot-accelerators-remote-monitoring-maintain/maintenancemethods-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancemethods-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-133">[![View the methods the device supports](./media/iot-accelerators-remote-monitoring-maintain/maintenancemethods-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancemethods-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-134">Choose **DecreaseTemperature** and set the job name to **DecreaseTemperature**.</span><span class="sxs-lookup"><span data-stu-id="d790e-134">Choose **DecreaseTemperature** and set the job name to **DecreaseTemperature**.</span></span> <span data-ttu-id="d790e-135">Then click **Apply**:</span><span class="sxs-lookup"><span data-stu-id="d790e-135">Then click **Apply**:</span></span>

<span data-ttu-id="d790e-136">[![Create the job to decrease the temperature](./media/iot-accelerators-remote-monitoring-maintain/maintenancecreatejob-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancecreatejob-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-136">[![Create the job to decrease the temperature](./media/iot-accelerators-remote-monitoring-maintain/maintenancecreatejob-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancecreatejob-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-137">To track the status of the job, click **View job status**.</span><span class="sxs-lookup"><span data-stu-id="d790e-137">To track the status of the job, click **View job status**.</span></span> <span data-ttu-id="d790e-138">Use the **Jobs** view to track all the jobs and method calls in the solution:</span><span class="sxs-lookup"><span data-stu-id="d790e-138">Use the **Jobs** view to track all the jobs and method calls in the solution:</span></span>

<span data-ttu-id="d790e-139">[![Monitor the job to decrease the temperature](./media/iot-accelerators-remote-monitoring-maintain/maintenancerunningjob-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancerunningjob-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-139">[![Monitor the job to decrease the temperature](./media/iot-accelerators-remote-monitoring-maintain/maintenancerunningjob-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/maintenancerunningjob-expanded.png#lightbox)</span></span>

<span data-ttu-id="d790e-140">You can check that the temperature of the device has fallen by viewing the telemetry on the **Dashboard** page:</span><span class="sxs-lookup"><span data-stu-id="d790e-140">You can check that the temperature of the device has fallen by viewing the telemetry on the **Dashboard** page:</span></span>

<span data-ttu-id="d790e-141">[![View the decrease in temperature](./media/iot-accelerators-remote-monitoring-maintain/jobresult-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/jobresult-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d790e-141">[![View the decrease in temperature](./media/iot-accelerators-remote-monitoring-maintain/jobresult-inline.png)](./media/iot-accelerators-remote-monitoring-maintain/jobresult-expanded.png#lightbox)</span></span>

[!INCLUDE [iot-accelerators-tutorial-cleanup](../../includes/iot-accelerators-tutorial-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="d790e-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="d790e-142">Next steps</span></span>

<span data-ttu-id="d790e-143">This tutorial showed you how to use alerts to identify issues with your devices and how to act on those devices to resolve the issues.</span><span class="sxs-lookup"><span data-stu-id="d790e-143">This tutorial showed you how to use alerts to identify issues with your devices and how to act on those devices to resolve the issues.</span></span> <span data-ttu-id="d790e-144">To learn how to connect a physical device to your solution accelerator, continue to the how-to articles.</span><span class="sxs-lookup"><span data-stu-id="d790e-144">To learn how to connect a physical device to your solution accelerator, continue to the how-to articles.</span></span>

<span data-ttu-id="d790e-145">Now you have learned how to manage device issues, the suggested next step is to learn how to [Connect your device to the Remote Monitoring solution accelerator](iot-accelerators-connecting-devices.md).</span><span class="sxs-lookup"><span data-stu-id="d790e-145">Now you have learned how to manage device issues, the suggested next step is to learn how to [Connect your device to the Remote Monitoring solution accelerator](iot-accelerators-connecting-devices.md).</span></span>
