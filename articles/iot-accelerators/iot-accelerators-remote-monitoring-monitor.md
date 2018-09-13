---
title: Monitor your IoT devices from an Azure solution tutorial | Microsoft Docs
description: In this tutorial you learn how to monitor your IoT devices using the Remote Monitoring solution accelerator.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 07/19/2018
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 1f9e5885e79e184b621ba2be7e2a8f329e31a6b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856111"
---
# <a name="tutorial-monitor-your-iot-devices"></a><span data-ttu-id="fadf0-103">Tutorial: Monitor your IoT devices</span><span class="sxs-lookup"><span data-stu-id="fadf0-103">Tutorial: Monitor your IoT devices</span></span>

<span data-ttu-id="fadf0-104">In this tutorial, you use the Remote Monitoring solution accelerator to monitor your connected IoT devices.</span><span class="sxs-lookup"><span data-stu-id="fadf0-104">In this tutorial, you use the Remote Monitoring solution accelerator to monitor your connected IoT devices.</span></span> <span data-ttu-id="fadf0-105">You use the solution dashboard to view telemetry, device information, alerts, and KPIs.</span><span class="sxs-lookup"><span data-stu-id="fadf0-105">You use the solution dashboard to view telemetry, device information, alerts, and KPIs.</span></span>

<span data-ttu-id="fadf0-106">The tutorial uses two simulated truck devices that send location, speed, and cargo temperature telemetry.</span><span class="sxs-lookup"><span data-stu-id="fadf0-106">The tutorial uses two simulated truck devices that send location, speed, and cargo temperature telemetry.</span></span> <span data-ttu-id="fadf0-107">The trucks are managed by an organization called Contoso and are connected to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="fadf0-107">The trucks are managed by an organization called Contoso and are connected to the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="fadf0-108">As a Contoso operator, you need to monitor the location and behavior of one of your trucks (truck-02) in the field.</span><span class="sxs-lookup"><span data-stu-id="fadf0-108">As a Contoso operator, you need to monitor the location and behavior of one of your trucks (truck-02) in the field.</span></span>

<span data-ttu-id="fadf0-109">In this tutorial, you:</span><span class="sxs-lookup"><span data-stu-id="fadf0-109">In this tutorial, you:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="fadf0-110">Filter the devices in the dashboard</span><span class="sxs-lookup"><span data-stu-id="fadf0-110">Filter the devices in the dashboard</span></span>
> * <span data-ttu-id="fadf0-111">View real-time telemetry</span><span class="sxs-lookup"><span data-stu-id="fadf0-111">View real-time telemetry</span></span>
> * <span data-ttu-id="fadf0-112">View device details</span><span class="sxs-lookup"><span data-stu-id="fadf0-112">View device details</span></span>
> * <span data-ttu-id="fadf0-113">View alerts from your devices</span><span class="sxs-lookup"><span data-stu-id="fadf0-113">View alerts from your devices</span></span>
> * <span data-ttu-id="fadf0-114">View the system KPIs</span><span class="sxs-lookup"><span data-stu-id="fadf0-114">View the system KPIs</span></span>

<span data-ttu-id="fadf0-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="fadf0-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [iot-accelerators-tutorial-prereqs](../../includes/iot-accelerators-tutorial-prereqs.md)]

## <a name="choose-the-devices-to-display"></a><span data-ttu-id="fadf0-116">Choose the devices to display</span><span class="sxs-lookup"><span data-stu-id="fadf0-116">Choose the devices to display</span></span>

<span data-ttu-id="fadf0-117">To select which connected devices display on the **Dashboard** page, use filters.</span><span class="sxs-lookup"><span data-stu-id="fadf0-117">To select which connected devices display on the **Dashboard** page, use filters.</span></span> <span data-ttu-id="fadf0-118">To display only the **Truck** devices, choose the built-in **Trucks** filter in the filter drop-down:</span><span class="sxs-lookup"><span data-stu-id="fadf0-118">To display only the **Truck** devices, choose the built-in **Trucks** filter in the filter drop-down:</span></span>

<span data-ttu-id="fadf0-119">[![Filter for trucks on the dashboard](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckfilter-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckfilter-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-119">[![Filter for trucks on the dashboard](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckfilter-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckfilter-expanded.png#lightbox)</span></span>

<span data-ttu-id="fadf0-120">When you apply a filter, only those devices that match the filter conditions are displayed on the map and in the telemetry panel on the **Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="fadf0-120">When you apply a filter, only those devices that match the filter conditions are displayed on the map and in the telemetry panel on the **Dashboard** page.</span></span> <span data-ttu-id="fadf0-121">You can see that there are two trucks connected to the solution accelerator, including truck-02:</span><span class="sxs-lookup"><span data-stu-id="fadf0-121">You can see that there are two trucks connected to the solution accelerator, including truck-02:</span></span>

<span data-ttu-id="fadf0-122">[![Only trucks are displayed on the map](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckmap-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckmap-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-122">[![Only trucks are displayed on the map](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckmap-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardtruckmap-expanded.png#lightbox)</span></span>

<span data-ttu-id="fadf0-123">To create, edit, and delete filters, click **Manage device groups**.</span><span class="sxs-lookup"><span data-stu-id="fadf0-123">To create, edit, and delete filters, click **Manage device groups**.</span></span>

## <a name="view-real-time-telemetry"></a><span data-ttu-id="fadf0-124">View real-time telemetry</span><span class="sxs-lookup"><span data-stu-id="fadf0-124">View real-time telemetry</span></span>

<span data-ttu-id="fadf0-125">The solution accelerator plots real-time telemetry in the chart on the **Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="fadf0-125">The solution accelerator plots real-time telemetry in the chart on the **Dashboard** page.</span></span> <span data-ttu-id="fadf0-126">The top of the telemetry chart shows available telemetry types for the devices, including truck-02, selected by the current filter.</span><span class="sxs-lookup"><span data-stu-id="fadf0-126">The top of the telemetry chart shows available telemetry types for the devices, including truck-02, selected by the current filter.</span></span> <span data-ttu-id="fadf0-127">By default, the chart is showing the latitude of the trucks and truck-02 appears to be stationary:</span><span class="sxs-lookup"><span data-stu-id="fadf0-127">By default, the chart is showing the latitude of the trucks and truck-02 appears to be stationary:</span></span>

<span data-ttu-id="fadf0-128">[![Truck telemetry types](./media/iot-accelerators-remote-monitoring-monitor/dashboardtelemetryview-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardtelemetryview-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-128">[![Truck telemetry types](./media/iot-accelerators-remote-monitoring-monitor/dashboardtelemetryview-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardtelemetryview-expanded.png#lightbox)</span></span>

<span data-ttu-id="fadf0-129">To view temperature telemetry for the trucks, click **Temperature**.</span><span class="sxs-lookup"><span data-stu-id="fadf0-129">To view temperature telemetry for the trucks, click **Temperature**.</span></span> <span data-ttu-id="fadf0-130">You can see how the temperature for truck-02 has varied over the last hour:</span><span class="sxs-lookup"><span data-stu-id="fadf0-130">You can see how the temperature for truck-02 has varied over the last hour:</span></span>

<span data-ttu-id="fadf0-131">[![Truck temperature telemetry plot](./media/iot-accelerators-remote-monitoring-monitor/dashboardselecttelemetry-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardselecttelemetry-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-131">[![Truck temperature telemetry plot](./media/iot-accelerators-remote-monitoring-monitor/dashboardselecttelemetry-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardselecttelemetry-expanded.png#lightbox)</span></span>

## <a name="view-the-map"></a><span data-ttu-id="fadf0-132">View the map</span><span class="sxs-lookup"><span data-stu-id="fadf0-132">View the map</span></span>

<span data-ttu-id="fadf0-133">The map displays information about the simulated trucks selected by the current filter.</span><span class="sxs-lookup"><span data-stu-id="fadf0-133">The map displays information about the simulated trucks selected by the current filter.</span></span> <span data-ttu-id="fadf0-134">You can zoom and pan the map to display locations in more or less detail.</span><span class="sxs-lookup"><span data-stu-id="fadf0-134">You can zoom and pan the map to display locations in more or less detail.</span></span> <span data-ttu-id="fadf0-135">The color of a device icon on the map indicates whether any **Alerts** (dark blue) or **Warnings** (red) are active for the device.</span><span class="sxs-lookup"><span data-stu-id="fadf0-135">The color of a device icon on the map indicates whether any **Alerts** (dark blue) or **Warnings** (red) are active for the device.</span></span> <span data-ttu-id="fadf0-136">A summary of the number of **Alerts** and **Warnings** is displayed to the left of the map.</span><span class="sxs-lookup"><span data-stu-id="fadf0-136">A summary of the number of **Alerts** and **Warnings** is displayed to the left of the map.</span></span>

<span data-ttu-id="fadf0-137">To view the details for truck-02, pan and zoom the map to locate it, then select the truck on the map.</span><span class="sxs-lookup"><span data-stu-id="fadf0-137">To view the details for truck-02, pan and zoom the map to locate it, then select the truck on the map.</span></span> <span data-ttu-id="fadf0-138">Then click on the device label to open the **Device details** panel.</span><span class="sxs-lookup"><span data-stu-id="fadf0-138">Then click on the device label to open the **Device details** panel.</span></span> <span data-ttu-id="fadf0-139">Device details include:</span><span class="sxs-lookup"><span data-stu-id="fadf0-139">Device details include:</span></span>

* <span data-ttu-id="fadf0-140">Recent telemetry values</span><span class="sxs-lookup"><span data-stu-id="fadf0-140">Recent telemetry values</span></span>
* <span data-ttu-id="fadf0-141">Methods the device supports</span><span class="sxs-lookup"><span data-stu-id="fadf0-141">Methods the device supports</span></span>
* <span data-ttu-id="fadf0-142">Device properties</span><span class="sxs-lookup"><span data-stu-id="fadf0-142">Device properties</span></span>

<span data-ttu-id="fadf0-143">[![View device details on the dashboard](./media/iot-accelerators-remote-monitoring-monitor/dashboarddevicedetail-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboarddevicedetail-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-143">[![View device details on the dashboard](./media/iot-accelerators-remote-monitoring-monitor/dashboarddevicedetail-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboarddevicedetail-expanded.png#lightbox)</span></span>

## <a name="view-alerts"></a><span data-ttu-id="fadf0-144">View alerts</span><span class="sxs-lookup"><span data-stu-id="fadf0-144">View alerts</span></span>

<span data-ttu-id="fadf0-145">The **Alerts** panel displays detailed information about the most recent alerts from your devices.</span><span class="sxs-lookup"><span data-stu-id="fadf0-145">The **Alerts** panel displays detailed information about the most recent alerts from your devices.</span></span> <span data-ttu-id="fadf0-146">The alerts from truck-02 indicate higher than normal cargo temperature:</span><span class="sxs-lookup"><span data-stu-id="fadf0-146">The alerts from truck-02 indicate higher than normal cargo temperature:</span></span>

<span data-ttu-id="fadf0-147">[![View device alerts on the dashboard](./media/iot-accelerators-remote-monitoring-monitor/dashboardsystemalarms-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardsystemalarms-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-147">[![View device alerts on the dashboard](./media/iot-accelerators-remote-monitoring-monitor/dashboardsystemalarms-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardsystemalarms-expanded.png#lightbox)</span></span>

<span data-ttu-id="fadf0-148">You can use a filter to adjust the time span for recent alerts.</span><span class="sxs-lookup"><span data-stu-id="fadf0-148">You can use a filter to adjust the time span for recent alerts.</span></span> <span data-ttu-id="fadf0-149">By default, the panel displays alerts from the last hour.</span><span class="sxs-lookup"><span data-stu-id="fadf0-149">By default, the panel displays alerts from the last hour.</span></span>

## <a name="view-the-system-kpis"></a><span data-ttu-id="fadf0-150">View the system KPIs</span><span class="sxs-lookup"><span data-stu-id="fadf0-150">View the system KPIs</span></span>

<span data-ttu-id="fadf0-151">The **Dashboard** page displays system KPIs calculated by the solution accelerator in the **Analytics** panel:</span><span class="sxs-lookup"><span data-stu-id="fadf0-151">The **Dashboard** page displays system KPIs calculated by the solution accelerator in the **Analytics** panel:</span></span>

<span data-ttu-id="fadf0-152">[![Dashboard KPIs](./media/iot-accelerators-remote-monitoring-monitor/dashboardkpis-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardkpis-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="fadf0-152">[![Dashboard KPIs](./media/iot-accelerators-remote-monitoring-monitor/dashboardkpis-inline.png)](./media/iot-accelerators-remote-monitoring-monitor/dashboardkpis-expanded.png#lightbox)</span></span>

<span data-ttu-id="fadf0-153">The dashboard shows three KPIs for the alerts selected by the current device and timespan filters:</span><span class="sxs-lookup"><span data-stu-id="fadf0-153">The dashboard shows three KPIs for the alerts selected by the current device and timespan filters:</span></span>

* <span data-ttu-id="fadf0-154">The number of active alerts for the rules that have triggered the most alerts.</span><span class="sxs-lookup"><span data-stu-id="fadf0-154">The number of active alerts for the rules that have triggered the most alerts.</span></span>
* <span data-ttu-id="fadf0-155">The proportion of alerts by device type.</span><span class="sxs-lookup"><span data-stu-id="fadf0-155">The proportion of alerts by device type.</span></span>
* <span data-ttu-id="fadf0-156">The percentage of alerts that are critical alerts.</span><span class="sxs-lookup"><span data-stu-id="fadf0-156">The percentage of alerts that are critical alerts.</span></span>

<span data-ttu-id="fadf0-157">For truck-02, all the alerts are warnings of higher than normal cargo temperature.</span><span class="sxs-lookup"><span data-stu-id="fadf0-157">For truck-02, all the alerts are warnings of higher than normal cargo temperature.</span></span>

<span data-ttu-id="fadf0-158">The same filters that set the time span for alerts and control which devices are displayed determine how the KPIs are aggregated.</span><span class="sxs-lookup"><span data-stu-id="fadf0-158">The same filters that set the time span for alerts and control which devices are displayed determine how the KPIs are aggregated.</span></span> <span data-ttu-id="fadf0-159">By default, the panel displays KPIs aggregated over the last hour.</span><span class="sxs-lookup"><span data-stu-id="fadf0-159">By default, the panel displays KPIs aggregated over the last hour.</span></span>

[!INCLUDE [iot-accelerators-tutorial-cleanup](../../includes/iot-accelerators-tutorial-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="fadf0-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="fadf0-160">Next steps</span></span>

<span data-ttu-id="fadf0-161">This tutorial showed you how to use the **Dashboard** page in the Remote Monitoring solution accelerator to filter and monitor the simulated trucks.</span><span class="sxs-lookup"><span data-stu-id="fadf0-161">This tutorial showed you how to use the **Dashboard** page in the Remote Monitoring solution accelerator to filter and monitor the simulated trucks.</span></span> <span data-ttu-id="fadf0-162">To learn how to use the solution accelerator to detect issues with your connected devices, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="fadf0-162">To learn how to use the solution accelerator to detect issues with your connected devices, continue to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fadf0-163">Detect issues with devices connected to your monitoring solution</span><span class="sxs-lookup"><span data-stu-id="fadf0-163">Detect issues with devices connected to your monitoring solution</span></span>](iot-accelerators-remote-monitoring-automate.md)