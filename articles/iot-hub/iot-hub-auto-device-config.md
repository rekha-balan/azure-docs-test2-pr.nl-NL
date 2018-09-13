---
title: Configure and monitor IoT devices at scale with Azure IoT Hub | Microsoft Docs
description: Use Azure IoT Hub automatic device configurations to assign a configuration to multiple devices
author: ChrisGMsft
manager: bruz
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 04/13/2018
ms.author: chrisgre
ms.openlocfilehash: 2edde122b109779794bb86752d69a5318edb9235
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858122"
---
# <a name="configure-and-monitor-iot-devices-at-scale-using-the-azure-portal"></a><span data-ttu-id="bb24f-103">Configure and monitor IoT devices at scale using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb24f-103">Configure and monitor IoT devices at scale using the Azure portal</span></span>

[!INCLUDE [iot-edge-how-to-deploy-monitor-selector](../../includes/iot-hub-auto-device-config-selector.md)]

<span data-ttu-id="bb24f-104">Automatic device management in Azure IoT Hub automates many of the repetitive and complex tasks of managing large device fleets over the entirety of their lifecycles.</span><span class="sxs-lookup"><span data-stu-id="bb24f-104">Automatic device management in Azure IoT Hub automates many of the repetitive and complex tasks of managing large device fleets over the entirety of their lifecycles.</span></span> <span data-ttu-id="bb24f-105">With automatic device management, you can target a set of devices based on their properties, define a desired configuration, and let IoT Hub update devices whenever they come into scope.</span><span class="sxs-lookup"><span data-stu-id="bb24f-105">With automatic device management, you can target a set of devices based on their properties, define a desired configuration, and let IoT Hub update devices whenever they come into scope.</span></span>  <span data-ttu-id="bb24f-106">This is performed using an automatic device configuration, which will also allow you to summarize completion and compliance, handle merging and conflicts, and roll out configurations in a phased approach.</span><span class="sxs-lookup"><span data-stu-id="bb24f-106">This is performed using an automatic device configuration, which will also allow you to summarize completion and compliance, handle merging and conflicts, and roll out configurations in a phased approach.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="bb24f-107">Automatic device configurations work by updating a set of device twins with desired properties and reporting a summary based on device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="bb24f-107">Automatic device configurations work by updating a set of device twins with desired properties and reporting a summary based on device twin reported properties.</span></span>  <span data-ttu-id="bb24f-108">It introduces a new class and JSON document called a *Configuration* which has three parts:</span><span class="sxs-lookup"><span data-stu-id="bb24f-108">It introduces a new class and JSON document called a *Configuration* which has three parts:</span></span>

* <span data-ttu-id="bb24f-109">The **target condition** defines the scope of device twins to be updated.</span><span class="sxs-lookup"><span data-stu-id="bb24f-109">The **target condition** defines the scope of device twins to be updated.</span></span> <span data-ttu-id="bb24f-110">The target condition is specified as a query on device twin tags and/or reported properties.</span><span class="sxs-lookup"><span data-stu-id="bb24f-110">The target condition is specified as a query on device twin tags and/or reported properties.</span></span>

* <span data-ttu-id="bb24f-111">The **target content** defines the desired properties to be added or updated in the targeted device twins.</span><span class="sxs-lookup"><span data-stu-id="bb24f-111">The **target content** defines the desired properties to be added or updated in the targeted device twins.</span></span> <span data-ttu-id="bb24f-112">The content includes a path to the section of desired properties to be changed.</span><span class="sxs-lookup"><span data-stu-id="bb24f-112">The content includes a path to the section of desired properties to be changed.</span></span>

* <span data-ttu-id="bb24f-113">The **metrics** define the summary counts of various configuration states such as **Success**, **In Progress**, and **Error**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-113">The **metrics** define the summary counts of various configuration states such as **Success**, **In Progress**, and **Error**.</span></span> <span data-ttu-id="bb24f-114">Custom metrics are specified as queries on device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="bb24f-114">Custom metrics are specified as queries on device twin reported properties.</span></span>  <span data-ttu-id="bb24f-115">System metrics are default metrics that measure twin update status, such as the number of device twins that are targeted and the number of twins that have been successfully updated.</span><span class="sxs-lookup"><span data-stu-id="bb24f-115">System metrics are default metrics that measure twin update status, such as the number of device twins that are targeted and the number of twins that have been successfully updated.</span></span> 

## <a name="implement-device-twins-to-configure-devices"></a><span data-ttu-id="bb24f-116">Implement device twins to configure devices</span><span class="sxs-lookup"><span data-stu-id="bb24f-116">Implement device twins to configure devices</span></span>

<span data-ttu-id="bb24f-117">Automatic device configurations require the use of device twins to synchronize state between the cloud and devices.</span><span class="sxs-lookup"><span data-stu-id="bb24f-117">Automatic device configurations require the use of device twins to synchronize state between the cloud and devices.</span></span> <span data-ttu-id="bb24f-118">Refer to [Understand and use device twins in IoT Hub](iot-hub-devguide-device-twins.md) for guidance on using device twins.</span><span class="sxs-lookup"><span data-stu-id="bb24f-118">Refer to [Understand and use device twins in IoT Hub](iot-hub-devguide-device-twins.md) for guidance on using device twins.</span></span>

## <a name="identify-devices-using-tags"></a><span data-ttu-id="bb24f-119">Identify devices using tags</span><span class="sxs-lookup"><span data-stu-id="bb24f-119">Identify devices using tags</span></span>

<span data-ttu-id="bb24f-120">Before you can create a configuration, you must specify which devices you want to affect.</span><span class="sxs-lookup"><span data-stu-id="bb24f-120">Before you can create a configuration, you must specify which devices you want to affect.</span></span> <span data-ttu-id="bb24f-121">Azure IoT Hub identifies devices using tags in the device twin.</span><span class="sxs-lookup"><span data-stu-id="bb24f-121">Azure IoT Hub identifies devices using tags in the device twin.</span></span> <span data-ttu-id="bb24f-122">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span><span class="sxs-lookup"><span data-stu-id="bb24f-122">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span></span> <span data-ttu-id="bb24f-123">For example, if you manage devices in different locations, you may add the following tags to a device twin:</span><span class="sxs-lookup"><span data-stu-id="bb24f-123">For example, if you manage devices in different locations, you may add the following tags to a device twin:</span></span>

```json
"tags": {
    "location": {
        "state": "Washington",
        "city": "Tacoma"
    }
},
```

## <a name="create-a-configuration"></a><span data-ttu-id="bb24f-124">Create a configuration</span><span class="sxs-lookup"><span data-stu-id="bb24f-124">Create a configuration</span></span>

1. <span data-ttu-id="bb24f-125">In the [Azure portal](https://portal.azure.com), go to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bb24f-125">In the [Azure portal](https://portal.azure.com), go to your IoT hub.</span></span> 

2. <span data-ttu-id="bb24f-126">Select **IoT device configuration**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-126">Select **IoT device configuration**.</span></span>

3. <span data-ttu-id="bb24f-127">Select **Add Configuration**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-127">Select **Add Configuration**.</span></span>

<span data-ttu-id="bb24f-128">There are five steps to create a configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-128">There are five steps to create a configuration.</span></span> <span data-ttu-id="bb24f-129">The following sections walk through each one.</span><span class="sxs-lookup"><span data-stu-id="bb24f-129">The following sections walk through each one.</span></span> 

### <a name="name-and-label"></a><span data-ttu-id="bb24f-130">Name and Label</span><span class="sxs-lookup"><span data-stu-id="bb24f-130">Name and Label</span></span>

1. <span data-ttu-id="bb24f-131">Give your configuration a unique name that is up to 128 lowercase letters.</span><span class="sxs-lookup"><span data-stu-id="bb24f-131">Give your configuration a unique name that is up to 128 lowercase letters.</span></span> <span data-ttu-id="bb24f-132">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span><span class="sxs-lookup"><span data-stu-id="bb24f-132">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span></span>

2. <span data-ttu-id="bb24f-133">Add labels to help track your configurations.</span><span class="sxs-lookup"><span data-stu-id="bb24f-133">Add labels to help track your configurations.</span></span> <span data-ttu-id="bb24f-134">Labels are **Name**, **Value** pairs that describe your configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-134">Labels are **Name**, **Value** pairs that describe your configuration.</span></span> <span data-ttu-id="bb24f-135">For example, `HostPlatform, Linux` or `Version, 3.0.1`.</span><span class="sxs-lookup"><span data-stu-id="bb24f-135">For example, `HostPlatform, Linux` or `Version, 3.0.1`.</span></span>

3. <span data-ttu-id="bb24f-136">Select **Next** to move to the next step.</span><span class="sxs-lookup"><span data-stu-id="bb24f-136">Select **Next** to move to the next step.</span></span> 

### <a name="specify-settings"></a><span data-ttu-id="bb24f-137">Specify Settings</span><span class="sxs-lookup"><span data-stu-id="bb24f-137">Specify Settings</span></span>

<span data-ttu-id="bb24f-138">This section specifies the target content to be set in targeted device twins.</span><span class="sxs-lookup"><span data-stu-id="bb24f-138">This section specifies the target content to be set in targeted device twins.</span></span> <span data-ttu-id="bb24f-139">There are two inputs for each set of settings.</span><span class="sxs-lookup"><span data-stu-id="bb24f-139">There are two inputs for each set of settings.</span></span> <span data-ttu-id="bb24f-140">The first is the device twin path, which is the path to the JSON section within the twin desired properties that will be set.</span><span class="sxs-lookup"><span data-stu-id="bb24f-140">The first is the device twin path, which is the path to the JSON section within the twin desired properties that will be set.</span></span>  <span data-ttu-id="bb24f-141">The second is the JSON content to be inserted in that section.</span><span class="sxs-lookup"><span data-stu-id="bb24f-141">The second is the JSON content to be inserted in that section.</span></span> <span data-ttu-id="bb24f-142">For example, set the Device Twin Path and Content to the following:</span><span class="sxs-lookup"><span data-stu-id="bb24f-142">For example, set the Device Twin Path and Content to the following:</span></span>

![Set the Device Twin Path and Content](./media/iot-hub-auto-device-config/create-configuration-full-browser.png)

<span data-ttu-id="bb24f-144">You can also set individual settings by specifying the entire path in the Device Twin Path and the value in the Content with no brackets.</span><span class="sxs-lookup"><span data-stu-id="bb24f-144">You can also set individual settings by specifying the entire path in the Device Twin Path and the value in the Content with no brackets.</span></span> <span data-ttu-id="bb24f-145">For example, set the Device Twin Path to `properties.desired.chiller-water.temperature` and set the Content to `66`.</span><span class="sxs-lookup"><span data-stu-id="bb24f-145">For example, set the Device Twin Path to `properties.desired.chiller-water.temperature` and set the Content to `66`.</span></span>

<span data-ttu-id="bb24f-146">If two or more configurations target the same Device Twin Path, the Content from the highest priority configuration will apply (priority is defined in Step 4).</span><span class="sxs-lookup"><span data-stu-id="bb24f-146">If two or more configurations target the same Device Twin Path, the Content from the highest priority configuration will apply (priority is defined in Step 4).</span></span>

<span data-ttu-id="bb24f-147">If you wish to remove a property, specify the property value to `null`.</span><span class="sxs-lookup"><span data-stu-id="bb24f-147">If you wish to remove a property, specify the property value to `null`.</span></span>

<span data-ttu-id="bb24f-148">You can add additional settings by selecting **Add Device Twin Setting**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-148">You can add additional settings by selecting **Add Device Twin Setting**.</span></span>

### <a name="specify-metrics-optional"></a><span data-ttu-id="bb24f-149">Specify Metrics (optional)</span><span class="sxs-lookup"><span data-stu-id="bb24f-149">Specify Metrics (optional)</span></span>

<span data-ttu-id="bb24f-150">Metrics provide summary counts of the various states that a device may report back as a result of applying configuration content.</span><span class="sxs-lookup"><span data-stu-id="bb24f-150">Metrics provide summary counts of the various states that a device may report back as a result of applying configuration content.</span></span> <span data-ttu-id="bb24f-151">For example, you may create a metric for pending settings changes, a metric for errors, and a metric for successful settings changes.</span><span class="sxs-lookup"><span data-stu-id="bb24f-151">For example, you may create a metric for pending settings changes, a metric for errors, and a metric for successful settings changes.</span></span>

1. <span data-ttu-id="bb24f-152">Enter a name for **Metric Name**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-152">Enter a name for **Metric Name**.</span></span>

2. <span data-ttu-id="bb24f-153">Enter a query for **Metric Criteria**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-153">Enter a query for **Metric Criteria**.</span></span>  <span data-ttu-id="bb24f-154">The query is based on device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="bb24f-154">The query is based on device twin reported properties.</span></span>  <span data-ttu-id="bb24f-155">The metric represents the number of rows returned by the query.</span><span class="sxs-lookup"><span data-stu-id="bb24f-155">The metric represents the number of rows returned by the query.</span></span>

<span data-ttu-id="bb24f-156">For example:</span><span class="sxs-lookup"><span data-stu-id="bb24f-156">For example:</span></span>

```sql
SELECT deviceId FROM devices 
  WHERE properties.reported.chillerWaterSettings.status='pending'
```

<span data-ttu-id="bb24f-157">You can include a clause that the configuration was applied, for example:</span><span class="sxs-lookup"><span data-stu-id="bb24f-157">You can include a clause that the configuration was applied, for example:</span></span> 

```sql
/* Include the double brackets. */
SELECT deviceId FROM devices 
  WHERE configurations.[[yourconfigname]].status='Applied'
```

### <a name="target-devices"></a><span data-ttu-id="bb24f-158">Target Devices</span><span class="sxs-lookup"><span data-stu-id="bb24f-158">Target Devices</span></span>

<span data-ttu-id="bb24f-159">Use the tags property from your device twins to target the specific devices that should receive this configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-159">Use the tags property from your device twins to target the specific devices that should receive this configuration.</span></span>  <span data-ttu-id="bb24f-160">You can also target devices by device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="bb24f-160">You can also target devices by device twin reported properties.</span></span>

<span data-ttu-id="bb24f-161">Since multiple configurations may target the same device, you should give each configuration a priority number.</span><span class="sxs-lookup"><span data-stu-id="bb24f-161">Since multiple configurations may target the same device, you should give each configuration a priority number.</span></span> <span data-ttu-id="bb24f-162">If there's ever a conflict, the configuration with the highest priority wins.</span><span class="sxs-lookup"><span data-stu-id="bb24f-162">If there's ever a conflict, the configuration with the highest priority wins.</span></span> 

1. <span data-ttu-id="bb24f-163">Enter a positive integer for the configuration **Priority**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-163">Enter a positive integer for the configuration **Priority**.</span></span> <span data-ttu-id="bb24f-164">The highest numerical value is considered the highest priority.</span><span class="sxs-lookup"><span data-stu-id="bb24f-164">The highest numerical value is considered the highest priority.</span></span> <span data-ttu-id="bb24f-165">If two configurations have the same priority number, the one that was created most recently wins.</span><span class="sxs-lookup"><span data-stu-id="bb24f-165">If two configurations have the same priority number, the one that was created most recently wins.</span></span> 

2. <span data-ttu-id="bb24f-166">Enter a **Target condition** to determine which devices will be targeted with this configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-166">Enter a **Target condition** to determine which devices will be targeted with this configuration.</span></span> <span data-ttu-id="bb24f-167">The condition is based on device twin tags or device twin reported properties and should match the expression format.</span><span class="sxs-lookup"><span data-stu-id="bb24f-167">The condition is based on device twin tags or device twin reported properties and should match the expression format.</span></span> <span data-ttu-id="bb24f-168">For example, `tags.environment='test'` or `properties.reported.chillerProperties.model='4000x'`.</span><span class="sxs-lookup"><span data-stu-id="bb24f-168">For example, `tags.environment='test'` or `properties.reported.chillerProperties.model='4000x'`.</span></span> <span data-ttu-id="bb24f-169">You can specify `*` to target all devices.</span><span class="sxs-lookup"><span data-stu-id="bb24f-169">You can specify `*` to target all devices.</span></span>

3. <span data-ttu-id="bb24f-170">Select **Next** to move on to the final step.</span><span class="sxs-lookup"><span data-stu-id="bb24f-170">Select **Next** to move on to the final step.</span></span>

### <a name="review-configuration"></a><span data-ttu-id="bb24f-171">Review Configuration</span><span class="sxs-lookup"><span data-stu-id="bb24f-171">Review Configuration</span></span>

<span data-ttu-id="bb24f-172">Review your configuration information, then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-172">Review your configuration information, then select **Submit**.</span></span>

## <a name="monitor-a-configuration"></a><span data-ttu-id="bb24f-173">Monitor a configuration</span><span class="sxs-lookup"><span data-stu-id="bb24f-173">Monitor a configuration</span></span>

<span data-ttu-id="bb24f-174">To view the details of a configuration and monitor the devices running it, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb24f-174">To view the details of a configuration and monitor the devices running it, use the following steps:</span></span>

1. <span data-ttu-id="bb24f-175">In the [Azure portal](https://portal.azure.com), go to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bb24f-175">In the [Azure portal](https://portal.azure.com), go to your IoT hub.</span></span> 

2. <span data-ttu-id="bb24f-176">Select **IoT device configuration**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-176">Select **IoT device configuration**.</span></span>

3. <span data-ttu-id="bb24f-177">Inspect the configuration list.</span><span class="sxs-lookup"><span data-stu-id="bb24f-177">Inspect the configuration list.</span></span> <span data-ttu-id="bb24f-178">For each configuration, you can view the following details:</span><span class="sxs-lookup"><span data-stu-id="bb24f-178">For each configuration, you can view the following details:</span></span>

   * <span data-ttu-id="bb24f-179">**ID** - the name of the configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-179">**ID** - the name of the configuration.</span></span>

   * <span data-ttu-id="bb24f-180">**Target condition** - the query used to define targeted devices.</span><span class="sxs-lookup"><span data-stu-id="bb24f-180">**Target condition** - the query used to define targeted devices.</span></span>

   * <span data-ttu-id="bb24f-181">**Priority** - the priority number assigned to the configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-181">**Priority** - the priority number assigned to the configuration.</span></span>

   * <span data-ttu-id="bb24f-182">**Creation time** - the timestamp from when the configuration was created.</span><span class="sxs-lookup"><span data-stu-id="bb24f-182">**Creation time** - the timestamp from when the configuration was created.</span></span> <span data-ttu-id="bb24f-183">This timestamp is used to break ties when two configurations have the same priority.</span><span class="sxs-lookup"><span data-stu-id="bb24f-183">This timestamp is used to break ties when two configurations have the same priority.</span></span> 

   * <span data-ttu-id="bb24f-184">**System metrics** - metrics that are calculated by IoT Hub and cannot be customized by developers.</span><span class="sxs-lookup"><span data-stu-id="bb24f-184">**System metrics** - metrics that are calculated by IoT Hub and cannot be customized by developers.</span></span> <span data-ttu-id="bb24f-185">Targeted specifies the number of device twins that match the target condition.</span><span class="sxs-lookup"><span data-stu-id="bb24f-185">Targeted specifies the number of device twins that match the target condition.</span></span> <span data-ttu-id="bb24f-186">Applies specified the number of device twins that have been modified by the configuration, which can include partial modifications in the event that a separate, higher priority configuration also made changes.</span><span class="sxs-lookup"><span data-stu-id="bb24f-186">Applies specified the number of device twins that have been modified by the configuration, which can include partial modifications in the event that a separate, higher priority configuration also made changes.</span></span> 

   * <span data-ttu-id="bb24f-187">**Custom metrics** - metrics that have been specified by the developer as queries against device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="bb24f-187">**Custom metrics** - metrics that have been specified by the developer as queries against device twin reported properties.</span></span>  <span data-ttu-id="bb24f-188">Up to five custom metrics can be defined per configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-188">Up to five custom metrics can be defined per configuration.</span></span> 
   
4. <span data-ttu-id="bb24f-189">Select the configuration that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="bb24f-189">Select the configuration that you want to monitor.</span></span>  

5. <span data-ttu-id="bb24f-190">Inspect the configuration details.</span><span class="sxs-lookup"><span data-stu-id="bb24f-190">Inspect the configuration details.</span></span> <span data-ttu-id="bb24f-191">You can use tabs to view specific details about the devices that received the configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-191">You can use tabs to view specific details about the devices that received the configuration.</span></span>

   * <span data-ttu-id="bb24f-192">**Target Condition** - the devices that match the target condition.</span><span class="sxs-lookup"><span data-stu-id="bb24f-192">**Target Condition** - the devices that match the target condition.</span></span> 

   * <span data-ttu-id="bb24f-193">**Metrics** - a list of system metrics and custom metrics.</span><span class="sxs-lookup"><span data-stu-id="bb24f-193">**Metrics** - a list of system metrics and custom metrics.</span></span>  <span data-ttu-id="bb24f-194">You can view a list of devices that are counted for each metric by selecting the metric in the drop-down and then selecting **View Devices**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-194">You can view a list of devices that are counted for each metric by selecting the metric in the drop-down and then selecting **View Devices**.</span></span>

   * <span data-ttu-id="bb24f-195">**Device Twin Settings** - the device twin settings that are set by the configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-195">**Device Twin Settings** - the device twin settings that are set by the configuration.</span></span> 

   * <span data-ttu-id="bb24f-196">**Configuration Labels** - key-value pairs used to describe a configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-196">**Configuration Labels** - key-value pairs used to describe a configuration.</span></span>  <span data-ttu-id="bb24f-197">Labels have no impact on functionality.</span><span class="sxs-lookup"><span data-stu-id="bb24f-197">Labels have no impact on functionality.</span></span> 

## <a name="modify-a-configuration"></a><span data-ttu-id="bb24f-198">Modify a configuration</span><span class="sxs-lookup"><span data-stu-id="bb24f-198">Modify a configuration</span></span>

<span data-ttu-id="bb24f-199">When you modify a configuration, the changes immediately replicate to all targeted devices.</span><span class="sxs-lookup"><span data-stu-id="bb24f-199">When you modify a configuration, the changes immediately replicate to all targeted devices.</span></span> 

<span data-ttu-id="bb24f-200">If you update the target condition, the following updates occur:</span><span class="sxs-lookup"><span data-stu-id="bb24f-200">If you update the target condition, the following updates occur:</span></span>

* <span data-ttu-id="bb24f-201">If a device twin didn't meet the old target condition, but meets the new target condition and this configuration is the highest priority for that device twin, then this configuration is applied to the device twin.</span><span class="sxs-lookup"><span data-stu-id="bb24f-201">If a device twin didn't meet the old target condition, but meets the new target condition and this configuration is the highest priority for that device twin, then this configuration is applied to the device twin.</span></span> 

* <span data-ttu-id="bb24f-202">If a device twin no longer meets the target condition, the settings from the configuration will be removed and the device twin will be modified by the next highest priority configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-202">If a device twin no longer meets the target condition, the settings from the configuration will be removed and the device twin will be modified by the next highest priority configuration.</span></span> 

* <span data-ttu-id="bb24f-203">If a device twin currently running this configuration no longer meets the target condition and doesn't meet the target condition of any other configurations, then the settings from the configuration will be removed and no other changes will be made on the twin.</span><span class="sxs-lookup"><span data-stu-id="bb24f-203">If a device twin currently running this configuration no longer meets the target condition and doesn't meet the target condition of any other configurations, then the settings from the configuration will be removed and no other changes will be made on the twin.</span></span> 

<span data-ttu-id="bb24f-204">To modify a configuration, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb24f-204">To modify a configuration, use the following steps:</span></span> 

1. <span data-ttu-id="bb24f-205">In the [Azure portal](https://portal.azure.com), go to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bb24f-205">In the [Azure portal](https://portal.azure.com), go to your IoT hub.</span></span> 

2. <span data-ttu-id="bb24f-206">Select **IoT device configuration**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-206">Select **IoT device configuration**.</span></span> 

3. <span data-ttu-id="bb24f-207">Select the configuration that you want to modify.</span><span class="sxs-lookup"><span data-stu-id="bb24f-207">Select the configuration that you want to modify.</span></span> 

4. <span data-ttu-id="bb24f-208">Make updates to the following fields:</span><span class="sxs-lookup"><span data-stu-id="bb24f-208">Make updates to the following fields:</span></span> 

   * <span data-ttu-id="bb24f-209">Target condition</span><span class="sxs-lookup"><span data-stu-id="bb24f-209">Target condition</span></span> 
   * <span data-ttu-id="bb24f-210">Labels</span><span class="sxs-lookup"><span data-stu-id="bb24f-210">Labels</span></span> 
   * <span data-ttu-id="bb24f-211">Priority</span><span class="sxs-lookup"><span data-stu-id="bb24f-211">Priority</span></span> 
   * <span data-ttu-id="bb24f-212">Metrics</span><span class="sxs-lookup"><span data-stu-id="bb24f-212">Metrics</span></span>

4. <span data-ttu-id="bb24f-213">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-213">Select **Save**.</span></span>

5. <span data-ttu-id="bb24f-214">Follow the steps in [Monitor a configuration](#monitor-a-configuration) to watch the changes roll out.</span><span class="sxs-lookup"><span data-stu-id="bb24f-214">Follow the steps in [Monitor a configuration](#monitor-a-configuration) to watch the changes roll out.</span></span> 

## <a name="delete-a-configuration"></a><span data-ttu-id="bb24f-215">Delete a configuration</span><span class="sxs-lookup"><span data-stu-id="bb24f-215">Delete a configuration</span></span>

<span data-ttu-id="bb24f-216">When you delete a configuration, any device twins take on their next highest priority configuration.</span><span class="sxs-lookup"><span data-stu-id="bb24f-216">When you delete a configuration, any device twins take on their next highest priority configuration.</span></span> <span data-ttu-id="bb24f-217">If device twins don't meet the target condition of any other configuration, then no other settings are applied.</span><span class="sxs-lookup"><span data-stu-id="bb24f-217">If device twins don't meet the target condition of any other configuration, then no other settings are applied.</span></span> 

1. <span data-ttu-id="bb24f-218">In the [Azure portal](https://portal.azure.com) go to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bb24f-218">In the [Azure portal](https://portal.azure.com) go to your IoT hub.</span></span> 

2. <span data-ttu-id="bb24f-219">Select **IoT device configuration**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-219">Select **IoT device configuration**.</span></span> 

3. <span data-ttu-id="bb24f-220">Use the checkbox to select the configuration that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="bb24f-220">Use the checkbox to select the configuration that you want to delete.</span></span> 

4. <span data-ttu-id="bb24f-221">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bb24f-221">Select **Delete**.</span></span>

5. <span data-ttu-id="bb24f-222">A prompt will ask you to confirm.</span><span class="sxs-lookup"><span data-stu-id="bb24f-222">A prompt will ask you to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb24f-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb24f-223">Next steps</span></span>

<span data-ttu-id="bb24f-224">In this article, you learned how configure and monitor IoT devices at scale.</span><span class="sxs-lookup"><span data-stu-id="bb24f-224">In this article, you learned how configure and monitor IoT devices at scale.</span></span> <span data-ttu-id="bb24f-225">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="bb24f-225">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* [<span data-ttu-id="bb24f-226">Manage your IoT Hub device identities in bulk</span><span class="sxs-lookup"><span data-stu-id="bb24f-226">Manage your IoT Hub device identities in bulk</span></span>](iot-hub-bulk-identity-mgmt.md)
* [<span data-ttu-id="bb24f-227">IoT Hub metrics</span><span class="sxs-lookup"><span data-stu-id="bb24f-227">IoT Hub metrics</span></span>](iot-hub-metrics.md)
* [<span data-ttu-id="bb24f-228">Operations monitoring</span><span class="sxs-lookup"><span data-stu-id="bb24f-228">Operations monitoring</span></span>](iot-hub-operations-monitoring.md)

<span data-ttu-id="bb24f-229">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="bb24f-229">To further explore the capabilities of IoT Hub, see:</span></span>

* [<span data-ttu-id="bb24f-230">IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="bb24f-230">IoT Hub developer guide</span></span>](iot-hub-devguide.md)
* [<span data-ttu-id="bb24f-231">Deploying AI to edge devices with Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="bb24f-231">Deploying AI to edge devices with Azure IoT Edge</span></span>](../iot-edge/tutorial-simulate-device-linux.md)

<span data-ttu-id="bb24f-232">To explore using the IoT Hub Device Provisioning Service to enable zero-touch, just-in-time provisioning, see:</span><span class="sxs-lookup"><span data-stu-id="bb24f-232">To explore using the IoT Hub Device Provisioning Service to enable zero-touch, just-in-time provisioning, see:</span></span> 

* [<span data-ttu-id="bb24f-233">Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="bb24f-233">Azure IoT Hub Device Provisioning Service</span></span>](/azure/iot-dps)
