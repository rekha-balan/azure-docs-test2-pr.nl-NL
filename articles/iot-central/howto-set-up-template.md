---
title: Set up a device template in an Azure IoT Central application | Microsoft Docs
description: Learn how to set up a device template with measurements, settings, properties, rules, and a dashboard.
author: viv-liu
ms.author: viviali
ms.date: 04/16/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: dafa58c5356c89351ab0eb711e4095b767aee1ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856648"
---
# <a name="set-up-a-device-template"></a><span data-ttu-id="a379e-103">Set up a device template</span><span class="sxs-lookup"><span data-stu-id="a379e-103">Set up a device template</span></span>

<span data-ttu-id="a379e-104">A device template is a blueprint that defines the characteristics and behaviors of a type of device that connects to a Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="a379e-104">A device template is a blueprint that defines the characteristics and behaviors of a type of device that connects to a Microsoft Azure IoT Central application.</span></span>

<span data-ttu-id="a379e-105">For example, a builder can create a device template for an IoT-connected fan that has:</span><span class="sxs-lookup"><span data-stu-id="a379e-105">For example, a builder can create a device template for an IoT-connected fan that has:</span></span>

- <span data-ttu-id="a379e-106">Temperature telemetry measurement</span><span class="sxs-lookup"><span data-stu-id="a379e-106">Temperature telemetry measurement</span></span>

- <span data-ttu-id="a379e-107">Fan motor error event measurement</span><span class="sxs-lookup"><span data-stu-id="a379e-107">Fan motor error event measurement</span></span>

- <span data-ttu-id="a379e-108">Fan operating state measurement</span><span class="sxs-lookup"><span data-stu-id="a379e-108">Fan operating state measurement</span></span>

- <span data-ttu-id="a379e-109">Fan speed setting</span><span class="sxs-lookup"><span data-stu-id="a379e-109">Fan speed setting</span></span>

- <span data-ttu-id="a379e-110">Location property</span><span class="sxs-lookup"><span data-stu-id="a379e-110">Location property</span></span>

- <span data-ttu-id="a379e-111">Rules that send alerts</span><span class="sxs-lookup"><span data-stu-id="a379e-111">Rules that send alerts</span></span>

- <span data-ttu-id="a379e-112">Dashboard that gives you an overall view of the device</span><span class="sxs-lookup"><span data-stu-id="a379e-112">Dashboard that gives you an overall view of the device</span></span>

<span data-ttu-id="a379e-113">From this device template, an operator can create and connect real fan devices with names such as **fan-1** and **fan-2**.</span><span class="sxs-lookup"><span data-stu-id="a379e-113">From this device template, an operator can create and connect real fan devices with names such as **fan-1** and **fan-2**.</span></span> <span data-ttu-id="a379e-114">All these fans have measurements, settings, properties, rules, and a dashboard that users of your application can monitor and manage.</span><span class="sxs-lookup"><span data-stu-id="a379e-114">All these fans have measurements, settings, properties, rules, and a dashboard that users of your application can monitor and manage.</span></span>

> [!NOTE]
> <span data-ttu-id="a379e-115">Only builders and administrators can create, edit, and delete device templates.</span><span class="sxs-lookup"><span data-stu-id="a379e-115">Only builders and administrators can create, edit, and delete device templates.</span></span> <span data-ttu-id="a379e-116">Any user can create devices on the **Device Explorer** page from existing device templates.</span><span class="sxs-lookup"><span data-stu-id="a379e-116">Any user can create devices on the **Device Explorer** page from existing device templates.</span></span>

## <a name="create-a-device-template"></a><span data-ttu-id="a379e-117">Create a device template</span><span class="sxs-lookup"><span data-stu-id="a379e-117">Create a device template</span></span>

1. <span data-ttu-id="a379e-118">Go to the **Application Builder** page.</span><span class="sxs-lookup"><span data-stu-id="a379e-118">Go to the **Application Builder** page.</span></span>

2. <span data-ttu-id="a379e-119">To create a blank template, select **Create Device Template**, and then select **Custom**.</span><span class="sxs-lookup"><span data-stu-id="a379e-119">To create a blank template, select **Create Device Template**, and then select **Custom**.</span></span>

3. <span data-ttu-id="a379e-120">Enter a name for your new device template and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="a379e-120">Enter a name for your new device template and select **Create**.</span></span>

   ![Device details page with "Refrigerator" as the template name](./media/howto-set-up-template/devicedetailspage.png)

4. <span data-ttu-id="a379e-122">Now you’re on the **Device Details** page of a new simulated device.</span><span class="sxs-lookup"><span data-stu-id="a379e-122">Now you’re on the **Device Details** page of a new simulated device.</span></span> <span data-ttu-id="a379e-123">A simulated device is automatically created for you when you create a device template.</span><span class="sxs-lookup"><span data-stu-id="a379e-123">A simulated device is automatically created for you when you create a device template.</span></span> <span data-ttu-id="a379e-124">It reports data and can be controlled just like a real device.</span><span class="sxs-lookup"><span data-stu-id="a379e-124">It reports data and can be controlled just like a real device.</span></span>

<span data-ttu-id="a379e-125">Now look at each of the tabs on the **Device Details** page.</span><span class="sxs-lookup"><span data-stu-id="a379e-125">Now look at each of the tabs on the **Device Details** page.</span></span>

## <a name="measurements"></a><span data-ttu-id="a379e-126">Measurements</span><span class="sxs-lookup"><span data-stu-id="a379e-126">Measurements</span></span>

<span data-ttu-id="a379e-127">Measurements are the data that comes from your device.</span><span class="sxs-lookup"><span data-stu-id="a379e-127">Measurements are the data that comes from your device.</span></span> <span data-ttu-id="a379e-128">You can add multiple measurements to your device template to match the capabilities of your device.</span><span class="sxs-lookup"><span data-stu-id="a379e-128">You can add multiple measurements to your device template to match the capabilities of your device.</span></span>

- <span data-ttu-id="a379e-129">**Telemetry** measurements are the numerical data points that your device collects over time.</span><span class="sxs-lookup"><span data-stu-id="a379e-129">**Telemetry** measurements are the numerical data points that your device collects over time.</span></span> <span data-ttu-id="a379e-130">They're represented as a continuous stream.</span><span class="sxs-lookup"><span data-stu-id="a379e-130">They're represented as a continuous stream.</span></span> <span data-ttu-id="a379e-131">An example is temperature.</span><span class="sxs-lookup"><span data-stu-id="a379e-131">An example is temperature.</span></span>
- <span data-ttu-id="a379e-132">**Event** measurements are point-in-time data that represents something of significance on the device.</span><span class="sxs-lookup"><span data-stu-id="a379e-132">**Event** measurements are point-in-time data that represents something of significance on the device.</span></span> <span data-ttu-id="a379e-133">A severity level represents the importance of an event.</span><span class="sxs-lookup"><span data-stu-id="a379e-133">A severity level represents the importance of an event.</span></span> <span data-ttu-id="a379e-134">An example is a fan motor error.</span><span class="sxs-lookup"><span data-stu-id="a379e-134">An example is a fan motor error.</span></span>
- <span data-ttu-id="a379e-135">**State** measurements represent the state of the device or its components over a period of time.</span><span class="sxs-lookup"><span data-stu-id="a379e-135">**State** measurements represent the state of the device or its components over a period of time.</span></span> <span data-ttu-id="a379e-136">For example, a fan mode can be defined as having **Operating** and **Stopped** as the two possible states.</span><span class="sxs-lookup"><span data-stu-id="a379e-136">For example, a fan mode can be defined as having **Operating** and **Stopped** as the two possible states.</span></span>

### <a name="create-a-telemetry-measurement"></a><span data-ttu-id="a379e-137">Create a telemetry measurement</span><span class="sxs-lookup"><span data-stu-id="a379e-137">Create a telemetry measurement</span></span>
<span data-ttu-id="a379e-138">To add a new telemetry measurement, select **Edit Template**, and then click the **+ New Measurement** button.</span><span class="sxs-lookup"><span data-stu-id="a379e-138">To add a new telemetry measurement, select **Edit Template**, and then click the **+ New Measurement** button.</span></span> <span data-ttu-id="a379e-139">Select **Telemetry** as the measurement type, and enter the details on the **Create Telemetry** form.</span><span class="sxs-lookup"><span data-stu-id="a379e-139">Select **Telemetry** as the measurement type, and enter the details on the **Create Telemetry** form.</span></span>

> [!NOTE]
> <span data-ttu-id="a379e-140">When a real device is connected, pay attention to the name of the measurement that the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-140">When a real device is connected, pay attention to the name of the measurement that the device reports.</span></span> <span data-ttu-id="a379e-141">The name must exactly match the **Field Name** entry for a measurement.</span><span class="sxs-lookup"><span data-stu-id="a379e-141">The name must exactly match the **Field Name** entry for a measurement.</span></span>

<span data-ttu-id="a379e-142">For example, you can add a new temperature telemetry measurement:</span><span class="sxs-lookup"><span data-stu-id="a379e-142">For example, you can add a new temperature telemetry measurement:</span></span>

!["Create Telemetry" form with details for temperature measurement](./media/howto-set-up-template/measurementsform.png)

<span data-ttu-id="a379e-144">After you select **Done**, the **Temperature** measurement appears in the list of measurements.</span><span class="sxs-lookup"><span data-stu-id="a379e-144">After you select **Done**, the **Temperature** measurement appears in the list of measurements.</span></span> <span data-ttu-id="a379e-145">An operator can see the visualization of the temperature data that the device is collecting.</span><span class="sxs-lookup"><span data-stu-id="a379e-145">An operator can see the visualization of the temperature data that the device is collecting.</span></span>

![Measurement graph](./media/howto-set-up-template/measurementsgraph.png)

### <a name="create-an-event-measurement"></a><span data-ttu-id="a379e-147">Create an event measurement</span><span class="sxs-lookup"><span data-stu-id="a379e-147">Create an event measurement</span></span>
<span data-ttu-id="a379e-148">To add a new event measurement, select **Edit Template**, and then click the **+ New Measurement** button.</span><span class="sxs-lookup"><span data-stu-id="a379e-148">To add a new event measurement, select **Edit Template**, and then click the **+ New Measurement** button.</span></span> <span data-ttu-id="a379e-149">Select **Event** as the measurement type, and enter the details on the **Create Event** form.</span><span class="sxs-lookup"><span data-stu-id="a379e-149">Select **Event** as the measurement type, and enter the details on the **Create Event** form.</span></span>

<span data-ttu-id="a379e-150">Provide the **Display Name**, **Field Name**, and **Severity** details for the event.</span><span class="sxs-lookup"><span data-stu-id="a379e-150">Provide the **Display Name**, **Field Name**, and **Severity** details for the event.</span></span> <span data-ttu-id="a379e-151">You can choose from the three available levels of severity: **Error**, **Warning**, and **Information**.</span><span class="sxs-lookup"><span data-stu-id="a379e-151">You can choose from the three available levels of severity: **Error**, **Warning**, and **Information**.</span></span>  

<span data-ttu-id="a379e-152">For example, you can add a new **Fan Motor Error** event.</span><span class="sxs-lookup"><span data-stu-id="a379e-152">For example, you can add a new **Fan Motor Error** event.</span></span>

!["Create Event" form with details for a fan motor event](./media/howto-set-up-template/eventmeasurementsform.png)

<span data-ttu-id="a379e-154">After you select **Done**, the **Fan Motor Error** measurement appears in the list of measurements.</span><span class="sxs-lookup"><span data-stu-id="a379e-154">After you select **Done**, the **Fan Motor Error** measurement appears in the list of measurements.</span></span> <span data-ttu-id="a379e-155">An operator can see the visualization of the event data that the device is sending.</span><span class="sxs-lookup"><span data-stu-id="a379e-155">An operator can see the visualization of the event data that the device is sending.</span></span>

![Event measurement chart](./media/howto-set-up-template/eventmeasurementschart.png)

<span data-ttu-id="a379e-157">To view more details about the event, select the event icon on the chart:</span><span class="sxs-lookup"><span data-stu-id="a379e-157">To view more details about the event, select the event icon on the chart:</span></span>

![Details for the "Fan Motor Error" event](./media/howto-set-up-template/eventmeasurementsdetail.png)


### <a name="create-a-state-measurement"></a><span data-ttu-id="a379e-159">Create a state measurement</span><span class="sxs-lookup"><span data-stu-id="a379e-159">Create a state measurement</span></span>
<span data-ttu-id="a379e-160">To add a new state measurement, select **Edit Template**, and then click the **+ New Measurement** button.</span><span class="sxs-lookup"><span data-stu-id="a379e-160">To add a new state measurement, select **Edit Template**, and then click the **+ New Measurement** button.</span></span> <span data-ttu-id="a379e-161">Select **State** as the measurement type, and enter the details on the **Create State** form.</span><span class="sxs-lookup"><span data-stu-id="a379e-161">Select **State** as the measurement type, and enter the details on the **Create State** form.</span></span>

<span data-ttu-id="a379e-162">Provide the details for **Display Name**, **Field Name**, and **Values** of the state.</span><span class="sxs-lookup"><span data-stu-id="a379e-162">Provide the details for **Display Name**, **Field Name**, and **Values** of the state.</span></span> <span data-ttu-id="a379e-163">Each value can also have a display name that will be used when the value appears in charts and tables.</span><span class="sxs-lookup"><span data-stu-id="a379e-163">Each value can also have a display name that will be used when the value appears in charts and tables.</span></span>

<span data-ttu-id="a379e-164">For example, you can add a new **Fan Mode** state that has two possible values that the device can send, **Operating** and **Stopped**.</span><span class="sxs-lookup"><span data-stu-id="a379e-164">For example, you can add a new **Fan Mode** state that has two possible values that the device can send, **Operating** and **Stopped**.</span></span>

!["Edit State" form with details for fan mode](./media/howto-set-up-template/statemeasurementsform.png)

<span data-ttu-id="a379e-166">After you select **Done**, the **Fan Mode** state measurement appears in the list of measurements.</span><span class="sxs-lookup"><span data-stu-id="a379e-166">After you select **Done**, the **Fan Mode** state measurement appears in the list of measurements.</span></span> <span data-ttu-id="a379e-167">The operator can see the visualization of the state data that the device is sending.</span><span class="sxs-lookup"><span data-stu-id="a379e-167">The operator can see the visualization of the state data that the device is sending.</span></span>

![State measurement chart](./media/howto-set-up-template/statemeasurementschart.png)

<span data-ttu-id="a379e-169">If the device sends too many data points in a small duration, the state measurement appears with a different visual, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="a379e-169">If the device sends too many data points in a small duration, the state measurement appears with a different visual, as shown in the following screenshot.</span></span> <span data-ttu-id="a379e-170">If you click on the chart, all the data points within that time period are displayed in a chronological order.</span><span class="sxs-lookup"><span data-stu-id="a379e-170">If you click on the chart, all the data points within that time period are displayed in a chronological order.</span></span> <span data-ttu-id="a379e-171">You can also narrow down the time range to see the measurement plotted on the chart.</span><span class="sxs-lookup"><span data-stu-id="a379e-171">You can also narrow down the time range to see the measurement plotted on the chart.</span></span>

![Details for the "Static Fan Mode" state measurement](./media/howto-set-up-template/statemeasurementsdetail.png)


## <a name="settings"></a><span data-ttu-id="a379e-173">Settings</span><span class="sxs-lookup"><span data-stu-id="a379e-173">Settings</span></span>

<span data-ttu-id="a379e-174">Settings control a device.</span><span class="sxs-lookup"><span data-stu-id="a379e-174">Settings control a device.</span></span> <span data-ttu-id="a379e-175">They enable operators of your application to provide inputs to the device.</span><span class="sxs-lookup"><span data-stu-id="a379e-175">They enable operators of your application to provide inputs to the device.</span></span> <span data-ttu-id="a379e-176">You can add multiple settings to your device template that appear as tiles on the **Settings** tab for operators to use.</span><span class="sxs-lookup"><span data-stu-id="a379e-176">You can add multiple settings to your device template that appear as tiles on the **Settings** tab for operators to use.</span></span> <span data-ttu-id="a379e-177">You can add six types of settings: number, text, date, toggle, pick list, and section label.</span><span class="sxs-lookup"><span data-stu-id="a379e-177">You can add six types of settings: number, text, date, toggle, pick list, and section label.</span></span>

> [!NOTE]
> <span data-ttu-id="a379e-178">When a real device is connected, pay attention to the name of the setting that the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-178">When a real device is connected, pay attention to the name of the setting that the device reports.</span></span> <span data-ttu-id="a379e-179">The name must exactly match the **Field Name** entry for a setting.</span><span class="sxs-lookup"><span data-stu-id="a379e-179">The name must exactly match the **Field Name** entry for a setting.</span></span>

<span data-ttu-id="a379e-180">Settings can be in one of three states.</span><span class="sxs-lookup"><span data-stu-id="a379e-180">Settings can be in one of three states.</span></span> <span data-ttu-id="a379e-181">The device reports these states.</span><span class="sxs-lookup"><span data-stu-id="a379e-181">The device reports these states.</span></span>

- <span data-ttu-id="a379e-182">**Synced**: The device has changed to reflect the setting value.</span><span class="sxs-lookup"><span data-stu-id="a379e-182">**Synced**: The device has changed to reflect the setting value.</span></span>

- <span data-ttu-id="a379e-183">**Pending**: The device is currently changing to the setting value.</span><span class="sxs-lookup"><span data-stu-id="a379e-183">**Pending**: The device is currently changing to the setting value.</span></span>

- <span data-ttu-id="a379e-184">**Error**: The device has returned an error.</span><span class="sxs-lookup"><span data-stu-id="a379e-184">**Error**: The device has returned an error.</span></span>

<span data-ttu-id="a379e-185">For example, you can add a new fan speed setting by selecting **Edit Template** and entering in the new setting:</span><span class="sxs-lookup"><span data-stu-id="a379e-185">For example, you can add a new fan speed setting by selecting **Edit Template** and entering in the new setting:</span></span>

!["Configure Number" form with details for speed settings](./media/howto-set-up-template/settingsform.png)

<span data-ttu-id="a379e-187">After you select **Save**, the **Fan Speed** setting appears as a tile and is ready to be used to change the fan speed of the device.</span><span class="sxs-lookup"><span data-stu-id="a379e-187">After you select **Save**, the **Fan Speed** setting appears as a tile and is ready to be used to change the fan speed of the device.</span></span>

<span data-ttu-id="a379e-188">After you create a tile, you can try out your new setting.</span><span class="sxs-lookup"><span data-stu-id="a379e-188">After you create a tile, you can try out your new setting.</span></span> <span data-ttu-id="a379e-189">First, select **Done** at the upper-right part of the screen.</span><span class="sxs-lookup"><span data-stu-id="a379e-189">First, select **Done** at the upper-right part of the screen.</span></span>

!["Settings" tab with the "Design Mode" switch for the tile](./media/howto-set-up-template/settingstile.png)

## <a name="properties"></a><span data-ttu-id="a379e-191">Properties</span><span class="sxs-lookup"><span data-stu-id="a379e-191">Properties</span></span>

<span data-ttu-id="a379e-192">Properties are the device metadata that's associated with the device, such as device location and serial number.</span><span class="sxs-lookup"><span data-stu-id="a379e-192">Properties are the device metadata that's associated with the device, such as device location and serial number.</span></span> <span data-ttu-id="a379e-193">You can add multiple properties to your device template that appear as tiles on the **Properties** tab. An operator can specify the values for properties when they create a device, and they can edit these values at any time.</span><span class="sxs-lookup"><span data-stu-id="a379e-193">You can add multiple properties to your device template that appear as tiles on the **Properties** tab. An operator can specify the values for properties when they create a device, and they can edit these values at any time.</span></span> <span data-ttu-id="a379e-194">You can add six types of properties: number, text, date, toggle, device property, and label.</span><span class="sxs-lookup"><span data-stu-id="a379e-194">You can add six types of properties: number, text, date, toggle, device property, and label.</span></span>

<span data-ttu-id="a379e-195">There are two categories of properties:</span><span class="sxs-lookup"><span data-stu-id="a379e-195">There are two categories of properties:</span></span>

- <span data-ttu-id="a379e-196">**Device** properties that the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-196">**Device** properties that the device reports.</span></span>
- <span data-ttu-id="a379e-197">**Application** properties that are stored purely in the application.</span><span class="sxs-lookup"><span data-stu-id="a379e-197">**Application** properties that are stored purely in the application.</span></span> <span data-ttu-id="a379e-198">The device doesn't recognize application properties.</span><span class="sxs-lookup"><span data-stu-id="a379e-198">The device doesn't recognize application properties.</span></span>

> [!NOTE]
> <span data-ttu-id="a379e-199">For device properties, when a real device is connected, pay attention to the name of the property that the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-199">For device properties, when a real device is connected, pay attention to the name of the property that the device reports.</span></span> <span data-ttu-id="a379e-200">The name must exactly match the **Field Name** entry for the property.</span><span class="sxs-lookup"><span data-stu-id="a379e-200">The name must exactly match the **Field Name** entry for the property.</span></span> <span data-ttu-id="a379e-201">For application properties, the field name can be anything you want, as long as the name is unique in the device template.</span><span class="sxs-lookup"><span data-stu-id="a379e-201">For application properties, the field name can be anything you want, as long as the name is unique in the device template.</span></span>

<span data-ttu-id="a379e-202">For example, you can add device location as a new property by selecting **Edit Template** and entering in the new property:</span><span class="sxs-lookup"><span data-stu-id="a379e-202">For example, you can add device location as a new property by selecting **Edit Template** and entering in the new property:</span></span>

!["Configure Text" form on the "Properties" tab](./media/howto-set-up-template/propertiesform.png)

<span data-ttu-id="a379e-204">After you select **Save**, device location appears as a tile:</span><span class="sxs-lookup"><span data-stu-id="a379e-204">After you select **Save**, device location appears as a tile:</span></span>

![Location tile](./media/howto-set-up-template/propertiestile.png)

<span data-ttu-id="a379e-206">After you create a tile, you can change the property value.</span><span class="sxs-lookup"><span data-stu-id="a379e-206">After you create a tile, you can change the property value.</span></span> <span data-ttu-id="a379e-207">First, select **Done** in the upper-right part of the screen.</span><span class="sxs-lookup"><span data-stu-id="a379e-207">First, select **Done** in the upper-right part of the screen.</span></span>

### <a name="create-a-location-property-through-azure-maps"></a><span data-ttu-id="a379e-208">Create a location property through Azure Maps</span><span class="sxs-lookup"><span data-stu-id="a379e-208">Create a location property through Azure Maps</span></span>
<span data-ttu-id="a379e-209">You can give geographic context to your location data in Azure IoT Central and map any latitude and longitude coordinates of a street address.</span><span class="sxs-lookup"><span data-stu-id="a379e-209">You can give geographic context to your location data in Azure IoT Central and map any latitude and longitude coordinates of a street address.</span></span> <span data-ttu-id="a379e-210">Or you can simply map latitude and longitude coordinates.</span><span class="sxs-lookup"><span data-stu-id="a379e-210">Or you can simply map latitude and longitude coordinates.</span></span> <span data-ttu-id="a379e-211">Azure Maps enables this capability in IoT Central.</span><span class="sxs-lookup"><span data-stu-id="a379e-211">Azure Maps enables this capability in IoT Central.</span></span>

<span data-ttu-id="a379e-212">You can add two types of location properties:</span><span class="sxs-lookup"><span data-stu-id="a379e-212">You can add two types of location properties:</span></span>
- <span data-ttu-id="a379e-213">**Location as an application property**, which is stored purely in the application.</span><span class="sxs-lookup"><span data-stu-id="a379e-213">**Location as an application property**, which is stored purely in the application.</span></span> <span data-ttu-id="a379e-214">The device doesn't recognize application properties.</span><span class="sxs-lookup"><span data-stu-id="a379e-214">The device doesn't recognize application properties.</span></span>
- <span data-ttu-id="a379e-215">**Location as a device property**, which the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-215">**Location as a device property**, which the device reports.</span></span>

#### <a name="add-location-as-an-application-property"></a><span data-ttu-id="a379e-216">Add location as an application property</span><span class="sxs-lookup"><span data-stu-id="a379e-216">Add location as an application property</span></span> 
<span data-ttu-id="a379e-217">You can create a location property as an application property by using Azure Maps in your IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="a379e-217">You can create a location property as an application property by using Azure Maps in your IoT Central application.</span></span> <span data-ttu-id="a379e-218">For example, you can add the device installation address.</span><span class="sxs-lookup"><span data-stu-id="a379e-218">For example, you can add the device installation address.</span></span> 

1. <span data-ttu-id="a379e-219">On the **Properties** tab, select **Edit Template**.</span><span class="sxs-lookup"><span data-stu-id="a379e-219">On the **Properties** tab, select **Edit Template**.</span></span>

   !["Properties" tab with design mode turned on](./media/howto-set-up-template/locationcloudproperty1.png)

2. <span data-ttu-id="a379e-221">In the library, select **Location**.</span><span class="sxs-lookup"><span data-stu-id="a379e-221">In the library, select **Location**.</span></span>
3. <span data-ttu-id="a379e-222">Configure **Display Name**, **Field Name**, and (optionally) **Initial Value** for the location.</span><span class="sxs-lookup"><span data-stu-id="a379e-222">Configure **Display Name**, **Field Name**, and (optionally) **Initial Value** for the location.</span></span> 

   !["Configure Location" form with details for location](./media/howto-set-up-template/locationcloudproperty2.png)

   <span data-ttu-id="a379e-224">There are two supported formats to add a location:</span><span class="sxs-lookup"><span data-stu-id="a379e-224">There are two supported formats to add a location:</span></span>
   - <span data-ttu-id="a379e-225">**Location as an address**</span><span class="sxs-lookup"><span data-stu-id="a379e-225">**Location as an address**</span></span>
   - <span data-ttu-id="a379e-226">**Location as coordinates**</span><span class="sxs-lookup"><span data-stu-id="a379e-226">**Location as coordinates**</span></span> 

4. <span data-ttu-id="a379e-227">Select **Save** and **Done**.</span><span class="sxs-lookup"><span data-stu-id="a379e-227">Select **Save** and **Done**.</span></span> 

   ![Location property with installation address added](./media/howto-set-up-template/locationcloudproperty3.png)

<span data-ttu-id="a379e-229">Now an operator can update the location value in the location field form.</span><span class="sxs-lookup"><span data-stu-id="a379e-229">Now an operator can update the location value in the location field form.</span></span> 

#### <a name="add-location-as-a-device-property"></a><span data-ttu-id="a379e-230">Add location as a device property</span><span class="sxs-lookup"><span data-stu-id="a379e-230">Add location as a device property</span></span> 

<span data-ttu-id="a379e-231">You can create a location property as a device property that the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-231">You can create a location property as a device property that the device reports.</span></span> <span data-ttu-id="a379e-232">For example, if you want to track the device location:</span><span class="sxs-lookup"><span data-stu-id="a379e-232">For example, if you want to track the device location:</span></span>

1. <span data-ttu-id="a379e-233">On the **Properties** tab, select **Edit Template**.</span><span class="sxs-lookup"><span data-stu-id="a379e-233">On the **Properties** tab, select **Edit Template**.</span></span>

   !["Properties" tab with design mode turned on](./media/howto-set-up-template/locationdeviceproperty1.png)

2. <span data-ttu-id="a379e-235">Select **Device Property** from the library.</span><span class="sxs-lookup"><span data-stu-id="a379e-235">Select **Device Property** from the library.</span></span>
3. <span data-ttu-id="a379e-236">Configure the display name and field name, and select **Location** as the data type.</span><span class="sxs-lookup"><span data-stu-id="a379e-236">Configure the display name and field name, and select **Location** as the data type.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="a379e-237">The field name must exactly match the name of the property that the device reports.</span><span class="sxs-lookup"><span data-stu-id="a379e-237">The field name must exactly match the name of the property that the device reports.</span></span> 

   !["Configure Device Properties" form with details for location](./media/howto-set-up-template/locationdeviceproperty2.png)

<span data-ttu-id="a379e-239">Now that you've configured your location property, you can [add a map to visualize the location in the device dashboard](#add-an-azure-maps-location-in-the-dashboard).</span><span class="sxs-lookup"><span data-stu-id="a379e-239">Now that you've configured your location property, you can [add a map to visualize the location in the device dashboard](#add-an-azure-maps-location-in-the-dashboard).</span></span>

## <a name="commands"></a><span data-ttu-id="a379e-240">Commands</span><span class="sxs-lookup"><span data-stu-id="a379e-240">Commands</span></span>

<span data-ttu-id="a379e-241">Commands are used to remotely manage a device.</span><span class="sxs-lookup"><span data-stu-id="a379e-241">Commands are used to remotely manage a device.</span></span> <span data-ttu-id="a379e-242">They enable operators of your application to instantly run commands on the device.</span><span class="sxs-lookup"><span data-stu-id="a379e-242">They enable operators of your application to instantly run commands on the device.</span></span> <span data-ttu-id="a379e-243">You can add multiple commands to your device template that appear as tiles on the **Commands** tab for operators to use.</span><span class="sxs-lookup"><span data-stu-id="a379e-243">You can add multiple commands to your device template that appear as tiles on the **Commands** tab for operators to use.</span></span> <span data-ttu-id="a379e-244">As the builder of the device, you have the flexibility to define commands according to your requirements.</span><span class="sxs-lookup"><span data-stu-id="a379e-244">As the builder of the device, you have the flexibility to define commands according to your requirements.</span></span>

<span data-ttu-id="a379e-245">How is a command different from a setting?</span><span class="sxs-lookup"><span data-stu-id="a379e-245">How is a command different from a setting?</span></span> 

* <span data-ttu-id="a379e-246">**Setting**: A setting is a configuration that you want to apply to a device, and you want the device to persist that configuration until you change it.</span><span class="sxs-lookup"><span data-stu-id="a379e-246">**Setting**: A setting is a configuration that you want to apply to a device, and you want the device to persist that configuration until you change it.</span></span> <span data-ttu-id="a379e-247">For example, you want to set the temperature of your freezer, and you want that setting even when the freezer restarts.</span><span class="sxs-lookup"><span data-stu-id="a379e-247">For example, you want to set the temperature of your freezer, and you want that setting even when the freezer restarts.</span></span> 

* <span data-ttu-id="a379e-248">**Command**: You use commands to instantly run a command on the device remotely from IoT Central.</span><span class="sxs-lookup"><span data-stu-id="a379e-248">**Command**: You use commands to instantly run a command on the device remotely from IoT Central.</span></span> <span data-ttu-id="a379e-249">If a device isn't connected, the command times out and fails.</span><span class="sxs-lookup"><span data-stu-id="a379e-249">If a device isn't connected, the command times out and fails.</span></span> <span data-ttu-id="a379e-250">For example, you want to restart a device.</span><span class="sxs-lookup"><span data-stu-id="a379e-250">For example, you want to restart a device.</span></span>  

<span data-ttu-id="a379e-251">When you run a command, it can be in one of three states, depending on whether the device received the command.</span><span class="sxs-lookup"><span data-stu-id="a379e-251">When you run a command, it can be in one of three states, depending on whether the device received the command.</span></span>

<span data-ttu-id="a379e-252">For example, you can add a new **Echo** command by selecting **Editing Template**, then clicking **+ New Command**, and entering in the new command:</span><span class="sxs-lookup"><span data-stu-id="a379e-252">For example, you can add a new **Echo** command by selecting **Editing Template**, then clicking **+ New Command**, and entering in the new command:</span></span>

!["Configure Command" form with details for echo](./media/howto-set-up-template/commandsecho.png)

<span data-ttu-id="a379e-254">After you select **Save** and **Done**,  the **Echo** command appears as a tile and is ready to be used to echo the device.</span><span class="sxs-lookup"><span data-stu-id="a379e-254">After you select **Save** and **Done**,  the **Echo** command appears as a tile and is ready to be used to echo the device.</span></span>

<span data-ttu-id="a379e-255">After you create a tile, you can try out your new command.</span><span class="sxs-lookup"><span data-stu-id="a379e-255">After you create a tile, you can try out your new command.</span></span>

## <a name="rules"></a><span data-ttu-id="a379e-256">Rules</span><span class="sxs-lookup"><span data-stu-id="a379e-256">Rules</span></span>

<span data-ttu-id="a379e-257">Rules enable operators to monitor devices in near real time.</span><span class="sxs-lookup"><span data-stu-id="a379e-257">Rules enable operators to monitor devices in near real time.</span></span> <span data-ttu-id="a379e-258">Rules automatically invoke actions such as sending an email when the rule is triggered.</span><span class="sxs-lookup"><span data-stu-id="a379e-258">Rules automatically invoke actions such as sending an email when the rule is triggered.</span></span> <span data-ttu-id="a379e-259">One type of rule is available today:</span><span class="sxs-lookup"><span data-stu-id="a379e-259">One type of rule is available today:</span></span>

- <span data-ttu-id="a379e-260">**Telemetry rule**, which is triggered when the selected device telemetry crosses a specified threshold.</span><span class="sxs-lookup"><span data-stu-id="a379e-260">**Telemetry rule**, which is triggered when the selected device telemetry crosses a specified threshold.</span></span> <span data-ttu-id="a379e-261">[Learn more about telemetry rules](howto-create-telemetry-rules.md).</span><span class="sxs-lookup"><span data-stu-id="a379e-261">[Learn more about telemetry rules](howto-create-telemetry-rules.md).</span></span>

## <a name="dashboard"></a><span data-ttu-id="a379e-262">Dashboard</span><span class="sxs-lookup"><span data-stu-id="a379e-262">Dashboard</span></span>

<span data-ttu-id="a379e-263">The dashboard is where an operator can go to see information about a device.</span><span class="sxs-lookup"><span data-stu-id="a379e-263">The dashboard is where an operator can go to see information about a device.</span></span> <span data-ttu-id="a379e-264">As a builder, you can add tiles on this page to help operators understand how the device is behaving.</span><span class="sxs-lookup"><span data-stu-id="a379e-264">As a builder, you can add tiles on this page to help operators understand how the device is behaving.</span></span> <span data-ttu-id="a379e-265">You can add multiple dashboard tiles to your device template.</span><span class="sxs-lookup"><span data-stu-id="a379e-265">You can add multiple dashboard tiles to your device template.</span></span> <span data-ttu-id="a379e-266">You can add six types of dashboard tiles: image, line chart, bar chart, KPI, settings and properties, and label.</span><span class="sxs-lookup"><span data-stu-id="a379e-266">You can add six types of dashboard tiles: image, line chart, bar chart, KPI, settings and properties, and label.</span></span>

<span data-ttu-id="a379e-267">For example, you can add a **Settings and Properties** tile to show a selection of the current values of settings and properties by selecting **Edit Template** and the tile from the Library:</span><span class="sxs-lookup"><span data-stu-id="a379e-267">For example, you can add a **Settings and Properties** tile to show a selection of the current values of settings and properties by selecting **Edit Template** and the tile from the Library:</span></span>

!["Configure Device Details" form with details for settings and properties](./media/howto-set-up-template/dashboardsettingsandpropertiesform.png)

<span data-ttu-id="a379e-269">Now when an operator views the dashboard, they can see this tile that displays the properties and settings of the device:</span><span class="sxs-lookup"><span data-stu-id="a379e-269">Now when an operator views the dashboard, they can see this tile that displays the properties and settings of the device:</span></span>

!["Dashboard" tab with displayed settings and properties for the tile](./media/howto-set-up-template/dashboardtile.png)

### <a name="add-an-azure-maps-location-in-the-dashboard"></a><span data-ttu-id="a379e-271">Add an Azure Maps location in the dashboard</span><span class="sxs-lookup"><span data-stu-id="a379e-271">Add an Azure Maps location in the dashboard</span></span>

<span data-ttu-id="a379e-272">If you configured a location property earlier in [Create a location property through Azure Maps](#create-a-location-property-through-azure-maps), you can visualize the location by using a map in your device dashboard.</span><span class="sxs-lookup"><span data-stu-id="a379e-272">If you configured a location property earlier in [Create a location property through Azure Maps](#create-a-location-property-through-azure-maps), you can visualize the location by using a map in your device dashboard.</span></span>

1. <span data-ttu-id="a379e-273">On the **Dashboard** tab, select **Edit Template**.</span><span class="sxs-lookup"><span data-stu-id="a379e-273">On the **Dashboard** tab, select **Edit Template**.</span></span>

   !["Dashboard" tab with design mode turned on](./media/howto-set-up-template/locationcloudproperty4map.png)

2. <span data-ttu-id="a379e-275">On the device dashboard, select **Map** from the library.</span><span class="sxs-lookup"><span data-stu-id="a379e-275">On the device dashboard, select **Map** from the library.</span></span> 
3. <span data-ttu-id="a379e-276">Give it a title and choose the location property that you previously configured as part of your device properties.</span><span class="sxs-lookup"><span data-stu-id="a379e-276">Give it a title and choose the location property that you previously configured as part of your device properties.</span></span>

   !["Configure Map" form with details for title and properties](./media/howto-set-up-template/locationcloudproperty5map.png)

4. <span data-ttu-id="a379e-278">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a379e-278">Select **Save**.</span></span> <span data-ttu-id="a379e-279">The map tile now displays the location that you selected.</span><span class="sxs-lookup"><span data-stu-id="a379e-279">The map tile now displays the location that you selected.</span></span> 

   ![Map tile with selected location](./media/howto-set-up-template/locationcloudproperty6map.png) 

<span data-ttu-id="a379e-281">You can resize the map to your desired size.</span><span class="sxs-lookup"><span data-stu-id="a379e-281">You can resize the map to your desired size.</span></span>

<span data-ttu-id="a379e-282">Now when an operator views the dashboard, they can see all the dashboard tiles that you've configured, including a location map.</span><span class="sxs-lookup"><span data-stu-id="a379e-282">Now when an operator views the dashboard, they can see all the dashboard tiles that you've configured, including a location map.</span></span>

![Tiles on the dashboard](./media/howto-set-up-template/locationcloudproperty7map.png) 

## <a name="next-steps"></a><span data-ttu-id="a379e-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="a379e-284">Next steps</span></span>

<span data-ttu-id="a379e-285">Now that you've learned how to set up a device template in your Azure IoT Central application, you can:</span><span class="sxs-lookup"><span data-stu-id="a379e-285">Now that you've learned how to set up a device template in your Azure IoT Central application, you can:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a379e-286">Create a new device template version</span><span class="sxs-lookup"><span data-stu-id="a379e-286">Create a new device template version</span></span>](howto-version-devicetemplate.md)
