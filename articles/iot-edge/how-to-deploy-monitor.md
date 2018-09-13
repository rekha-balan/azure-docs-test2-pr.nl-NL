---
title: Deploy, monitor modules for Azure IoT Edge | Microsoft Docs
description: Manage the modules that run on edge devices
keywords: ''
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/25/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 28aa2904f63a9802305d24fec1650f84e38601ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968253"
---
# <a name="deploy-and-monitor-iot-edge-modules-at-scale-using-the-azure-portal"></a><span data-ttu-id="ade14-103">Deploy and monitor IoT Edge modules at scale using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ade14-103">Deploy and monitor IoT Edge modules at scale using the Azure portal</span></span>

[!INCLUDE [iot-edge-how-to-deploy-monitor-selector](../../includes/iot-edge-how-to-deploy-monitor-selector.md)]

<span data-ttu-id="ade14-104">Azure IoT Edge enables you to move analytics to the edge and provides a cloud interface so that you can manage and monitor your IoT Edge devices without having to physically access each one.</span><span class="sxs-lookup"><span data-stu-id="ade14-104">Azure IoT Edge enables you to move analytics to the edge and provides a cloud interface so that you can manage and monitor your IoT Edge devices without having to physically access each one.</span></span> <span data-ttu-id="ade14-105">The capability to remotely manage devices is increasingly important as Internet of Things solutions are growing larger and more complex.</span><span class="sxs-lookup"><span data-stu-id="ade14-105">The capability to remotely manage devices is increasingly important as Internet of Things solutions are growing larger and more complex.</span></span> <span data-ttu-id="ade14-106">Azure IoT Edge is designed to support your business goals, no matter how many devices you add.</span><span class="sxs-lookup"><span data-stu-id="ade14-106">Azure IoT Edge is designed to support your business goals, no matter how many devices you add.</span></span>

<span data-ttu-id="ade14-107">You can manage individual devices and deploy modules to them one at a time.</span><span class="sxs-lookup"><span data-stu-id="ade14-107">You can manage individual devices and deploy modules to them one at a time.</span></span> <span data-ttu-id="ade14-108">However, if you want to make changes to devices at a large scale, you can create an **IoT Edge automatic deployment**, which is part of Automatic Device Management in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-108">However, if you want to make changes to devices at a large scale, you can create an **IoT Edge automatic deployment**, which is part of Automatic Device Management in IoT Hub.</span></span> <span data-ttu-id="ade14-109">Deployments are dynamic processes that enable you to deploy multiple modules to multiple devices at once, track the status and health of the modules, and make changes when necessary.</span><span class="sxs-lookup"><span data-stu-id="ade14-109">Deployments are dynamic processes that enable you to deploy multiple modules to multiple devices at once, track the status and health of the modules, and make changes when necessary.</span></span> 

## <a name="identify-devices-using-tags"></a><span data-ttu-id="ade14-110">Identify devices using tags</span><span class="sxs-lookup"><span data-stu-id="ade14-110">Identify devices using tags</span></span>

<span data-ttu-id="ade14-111">Before you can create a deployment, you have to be able to specify which devices you want to affect.</span><span class="sxs-lookup"><span data-stu-id="ade14-111">Before you can create a deployment, you have to be able to specify which devices you want to affect.</span></span> <span data-ttu-id="ade14-112">Azure IoT Edge identifies devices using **tags** in the device twin.</span><span class="sxs-lookup"><span data-stu-id="ade14-112">Azure IoT Edge identifies devices using **tags** in the device twin.</span></span> <span data-ttu-id="ade14-113">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span><span class="sxs-lookup"><span data-stu-id="ade14-113">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span></span> <span data-ttu-id="ade14-114">For example, if you manage a campus of smart buildings, you might add the following tags to a device:</span><span class="sxs-lookup"><span data-stu-id="ade14-114">For example, if you manage a campus of smart buildings, you might add the following tags to a device:</span></span>

```json
"tags":{
    "location":{
        "building": "20",
        "floor": "2"
    },
    "roomtype": "conference",
    "environment": "prod"
}
```

<span data-ttu-id="ade14-115">For more information about device twins and tags, see [Understand and use device twins in IoT Hub][lnk-device-twin].</span><span class="sxs-lookup"><span data-stu-id="ade14-115">For more information about device twins and tags, see [Understand and use device twins in IoT Hub][lnk-device-twin].</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="ade14-116">Create a deployment</span><span class="sxs-lookup"><span data-stu-id="ade14-116">Create a deployment</span></span>

1. <span data-ttu-id="ade14-117">In the [Azure portal][lnk-portal], go to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-117">In the [Azure portal][lnk-portal], go to your IoT hub.</span></span> 
1. <span data-ttu-id="ade14-118">Select **IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="ade14-118">Select **IoT Edge**.</span></span>
1. <span data-ttu-id="ade14-119">Select **Add IoT Edge Deployment**.</span><span class="sxs-lookup"><span data-stu-id="ade14-119">Select **Add IoT Edge Deployment**.</span></span>

<span data-ttu-id="ade14-120">There are five steps to create a deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-120">There are five steps to create a deployment.</span></span> <span data-ttu-id="ade14-121">The following sections walk through each one.</span><span class="sxs-lookup"><span data-stu-id="ade14-121">The following sections walk through each one.</span></span> 

### <a name="step-1-name-and-label"></a><span data-ttu-id="ade14-122">Step 1: Name and Label</span><span class="sxs-lookup"><span data-stu-id="ade14-122">Step 1: Name and Label</span></span>

1. <span data-ttu-id="ade14-123">Give your deployment a unique name that is up to 128 lowercase letters.</span><span class="sxs-lookup"><span data-stu-id="ade14-123">Give your deployment a unique name that is up to 128 lowercase letters.</span></span> <span data-ttu-id="ade14-124">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span><span class="sxs-lookup"><span data-stu-id="ade14-124">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span></span>
1. <span data-ttu-id="ade14-125">Add labels to help track your deployments.</span><span class="sxs-lookup"><span data-stu-id="ade14-125">Add labels to help track your deployments.</span></span> <span data-ttu-id="ade14-126">Labels are **Name**, **Value** pairs that describe your deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-126">Labels are **Name**, **Value** pairs that describe your deployment.</span></span> <span data-ttu-id="ade14-127">For example, `HostPlatform, Linux` or `Version, 3.0.1`.</span><span class="sxs-lookup"><span data-stu-id="ade14-127">For example, `HostPlatform, Linux` or `Version, 3.0.1`.</span></span>
1. <span data-ttu-id="ade14-128">Select **Next** to move to step two.</span><span class="sxs-lookup"><span data-stu-id="ade14-128">Select **Next** to move to step two.</span></span> 

### <a name="step-2-add-modules-optional"></a><span data-ttu-id="ade14-129">Step 2: Add Modules (optional)</span><span class="sxs-lookup"><span data-stu-id="ade14-129">Step 2: Add Modules (optional)</span></span>

<span data-ttu-id="ade14-130">There are two types of modules that you can add to a deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-130">There are two types of modules that you can add to a deployment.</span></span> <span data-ttu-id="ade14-131">The first is a module based off of an Azure service, like Storage Account or Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="ade14-131">The first is a module based off of an Azure service, like Storage Account or Stream Analytics.</span></span> <span data-ttu-id="ade14-132">The second is a module based off of your own code.</span><span class="sxs-lookup"><span data-stu-id="ade14-132">The second is a module based off of your own code.</span></span> <span data-ttu-id="ade14-133">You can add multiple modules of either type to a deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-133">You can add multiple modules of either type to a deployment.</span></span> 

<span data-ttu-id="ade14-134">If you create a deployment with no modules, it removes any current modules from the devices.</span><span class="sxs-lookup"><span data-stu-id="ade14-134">If you create a deployment with no modules, it removes any current modules from the devices.</span></span> 

>[!NOTE]
><span data-ttu-id="ade14-135">Azure Machine Learning and Azure Functions don't support the automated Azure service deployment yet.</span><span class="sxs-lookup"><span data-stu-id="ade14-135">Azure Machine Learning and Azure Functions don't support the automated Azure service deployment yet.</span></span> <span data-ttu-id="ade14-136">Use the custom module deployment to manually add those services to your deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-136">Use the custom module deployment to manually add those services to your deployment.</span></span> 

<span data-ttu-id="ade14-137">To add a module from Azure Stream Analytics, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ade14-137">To add a module from Azure Stream Analytics, follow these steps:</span></span>
1. <span data-ttu-id="ade14-138">In the **Deployment Modules** section of the page, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ade14-138">In the **Deployment Modules** section of the page, click **Add**.</span></span>
1. <span data-ttu-id="ade14-139">Select **Azure Stream Analytics module**.</span><span class="sxs-lookup"><span data-stu-id="ade14-139">Select **Azure Stream Analytics module**.</span></span>
1. <span data-ttu-id="ade14-140">Choose your **Subscription** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="ade14-140">Choose your **Subscription** from the drop-down menu.</span></span>
1. <span data-ttu-id="ade14-141">Choose your **Edge job** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="ade14-141">Choose your **Edge job** from the drop-down menu.</span></span>
1. <span data-ttu-id="ade14-142">Select **Save** to add your module to the deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-142">Select **Save** to add your module to the deployment.</span></span> 

<span data-ttu-id="ade14-143">To add custom code as a module, or to manually add an Azure service module, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ade14-143">To add custom code as a module, or to manually add an Azure service module, follow these steps:</span></span>
1. <span data-ttu-id="ade14-144">In the **Registry Settings** section of the page, provide the names and credentials for any private container registries that contain the module images for this deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-144">In the **Registry Settings** section of the page, provide the names and credentials for any private container registries that contain the module images for this deployment.</span></span> <span data-ttu-id="ade14-145">The Edge Agent will report error 500 if it can't find the contrainer registry credential for a docker image.</span><span class="sxs-lookup"><span data-stu-id="ade14-145">The Edge Agent will report error 500 if it can't find the contrainer registry credential for a docker image.</span></span>
1. <span data-ttu-id="ade14-146">In the **Deployment Modules** section of the page, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ade14-146">In the **Deployment Modules** section of the page, click **Add**.</span></span>
1. <span data-ttu-id="ade14-147">Select **IoT Edge Module**.</span><span class="sxs-lookup"><span data-stu-id="ade14-147">Select **IoT Edge Module**.</span></span>
1. <span data-ttu-id="ade14-148">Give your module a **Name**.</span><span class="sxs-lookup"><span data-stu-id="ade14-148">Give your module a **Name**.</span></span>
1. <span data-ttu-id="ade14-149">For the **Image URI** field, enter the container image for your module.</span><span class="sxs-lookup"><span data-stu-id="ade14-149">For the **Image URI** field, enter the container image for your module.</span></span> 
1. <span data-ttu-id="ade14-150">Specify any **Container Create Options** that should be passed to the container.</span><span class="sxs-lookup"><span data-stu-id="ade14-150">Specify any **Container Create Options** that should be passed to the container.</span></span> <span data-ttu-id="ade14-151">For more information, see [docker create][lnk-docker-create].</span><span class="sxs-lookup"><span data-stu-id="ade14-151">For more information, see [docker create][lnk-docker-create].</span></span>
1. <span data-ttu-id="ade14-152">Use the drop-down menu to select a **Restart policy**.</span><span class="sxs-lookup"><span data-stu-id="ade14-152">Use the drop-down menu to select a **Restart policy**.</span></span> <span data-ttu-id="ade14-153">Choose from the following options:</span><span class="sxs-lookup"><span data-stu-id="ade14-153">Choose from the following options:</span></span> 
   * <span data-ttu-id="ade14-154">**Always** - The module always restarts if it shuts down for any reason.</span><span class="sxs-lookup"><span data-stu-id="ade14-154">**Always** - The module always restarts if it shuts down for any reason.</span></span>
   * <span data-ttu-id="ade14-155">**Never** - The module never restarts if it shuts down for any reason.</span><span class="sxs-lookup"><span data-stu-id="ade14-155">**Never** - The module never restarts if it shuts down for any reason.</span></span>
   * <span data-ttu-id="ade14-156">**On-failed** - The module restarts if it crashes, but not if it shuts down cleanly.</span><span class="sxs-lookup"><span data-stu-id="ade14-156">**On-failed** - The module restarts if it crashes, but not if it shuts down cleanly.</span></span> 
   * <span data-ttu-id="ade14-157">**On-unhealthy** - The module restarts if it crashes or returns an unhealthy status.</span><span class="sxs-lookup"><span data-stu-id="ade14-157">**On-unhealthy** - The module restarts if it crashes or returns an unhealthy status.</span></span> <span data-ttu-id="ade14-158">It's up to each module to implement the health status function.</span><span class="sxs-lookup"><span data-stu-id="ade14-158">It's up to each module to implement the health status function.</span></span> 
1. <span data-ttu-id="ade14-159">Use the drop-down menu to select the **Desired Status** for the module.</span><span class="sxs-lookup"><span data-stu-id="ade14-159">Use the drop-down menu to select the **Desired Status** for the module.</span></span> <span data-ttu-id="ade14-160">Choose from the following options:</span><span class="sxs-lookup"><span data-stu-id="ade14-160">Choose from the following options:</span></span>
   * <span data-ttu-id="ade14-161">**Running** - This is the default option.</span><span class="sxs-lookup"><span data-stu-id="ade14-161">**Running** - This is the default option.</span></span> <span data-ttu-id="ade14-162">The module will start running immediately after being deployed.</span><span class="sxs-lookup"><span data-stu-id="ade14-162">The module will start running immediately after being deployed.</span></span>
   * <span data-ttu-id="ade14-163">**Stopped** - After being deployed, the module will remain idle until called upon to start by you or another module.</span><span class="sxs-lookup"><span data-stu-id="ade14-163">**Stopped** - After being deployed, the module will remain idle until called upon to start by you or another module.</span></span>
1. <span data-ttu-id="ade14-164">Select **Enable** if you want to add any tags or desired properties to the module twin.</span><span class="sxs-lookup"><span data-stu-id="ade14-164">Select **Enable** if you want to add any tags or desired properties to the module twin.</span></span> 
1. <span data-ttu-id="ade14-165">Enter **Environment variables** for this module.</span><span class="sxs-lookup"><span data-stu-id="ade14-165">Enter **Environment variables** for this module.</span></span> <span data-ttu-id="ade14-166">Environment variables provide supplement information to a module facilitating the configuration process.</span><span class="sxs-lookup"><span data-stu-id="ade14-166">Environment variables provide supplement information to a module facilitating the configuration process.</span></span>
1. <span data-ttu-id="ade14-167">Select **Save** to add your module to the deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-167">Select **Save** to add your module to the deployment.</span></span> 

<span data-ttu-id="ade14-168">Once you have all the modules for a deployment configured, select **Next** to move to step three.</span><span class="sxs-lookup"><span data-stu-id="ade14-168">Once you have all the modules for a deployment configured, select **Next** to move to step three.</span></span>

### <a name="step-3-specify-routes-optional"></a><span data-ttu-id="ade14-169">Step 3: Specify Routes (optional)</span><span class="sxs-lookup"><span data-stu-id="ade14-169">Step 3: Specify Routes (optional)</span></span>

<span data-ttu-id="ade14-170">Routes define how modules communicate with each other within a deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-170">Routes define how modules communicate with each other within a deployment.</span></span> <span data-ttu-id="ade14-171">By default the wizard gives you a route called **route** and defined as \**FROM /* INTO $upstream\*\*, which means that any messages output by any modules are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-171">By default the wizard gives you a route called **route** and defined as \**FROM /* INTO $upstream\*\*, which means that any messages output by any modules are sent to your IoT hub.</span></span>  

<span data-ttu-id="ade14-172">Add or update the routes with information from [Declare routes](module-composition.md#declare-routes), then select **Next** to continue to the review section.</span><span class="sxs-lookup"><span data-stu-id="ade14-172">Add or update the routes with information from [Declare routes](module-composition.md#declare-routes), then select **Next** to continue to the review section.</span></span>


### <a name="step-4-target-devices"></a><span data-ttu-id="ade14-173">Step 4: Target Devices</span><span class="sxs-lookup"><span data-stu-id="ade14-173">Step 4: Target Devices</span></span>

<span data-ttu-id="ade14-174">Use the tags property from your devices to target the specific devices that should receive this deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-174">Use the tags property from your devices to target the specific devices that should receive this deployment.</span></span> 

<span data-ttu-id="ade14-175">Since multiple deployments may target the same device, you should give each deployment a priority number.</span><span class="sxs-lookup"><span data-stu-id="ade14-175">Since multiple deployments may target the same device, you should give each deployment a priority number.</span></span> <span data-ttu-id="ade14-176">If there's ever a conflict, the deployment with the highest priority (higher values indicate higher priority) wins.</span><span class="sxs-lookup"><span data-stu-id="ade14-176">If there's ever a conflict, the deployment with the highest priority (higher values indicate higher priority) wins.</span></span> <span data-ttu-id="ade14-177">If two deployments have the same priority number, the one that was created most recently wins.</span><span class="sxs-lookup"><span data-stu-id="ade14-177">If two deployments have the same priority number, the one that was created most recently wins.</span></span> 

1. <span data-ttu-id="ade14-178">Enter a positive integer for the deployment **Priority**.</span><span class="sxs-lookup"><span data-stu-id="ade14-178">Enter a positive integer for the deployment **Priority**.</span></span> <span data-ttu-id="ade14-179">In the event that two or more deployments are targeted at the same device, the deployment with the highest numerical value for Priority will apply.</span><span class="sxs-lookup"><span data-stu-id="ade14-179">In the event that two or more deployments are targeted at the same device, the deployment with the highest numerical value for Priority will apply.</span></span>
1. <span data-ttu-id="ade14-180">Enter a **Target condition** to determine which devices will be targeted with this deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-180">Enter a **Target condition** to determine which devices will be targeted with this deployment.</span></span> <span data-ttu-id="ade14-181">The condition is based on device twin tags or device twin reported properties and should match the expression format.</span><span class="sxs-lookup"><span data-stu-id="ade14-181">The condition is based on device twin tags or device twin reported properties and should match the expression format.</span></span> <span data-ttu-id="ade14-182">For example, `tags.environment='test'` or `properties.reported.devicemodel='4000x'`.</span><span class="sxs-lookup"><span data-stu-id="ade14-182">For example, `tags.environment='test'` or `properties.reported.devicemodel='4000x'`.</span></span> 
1. <span data-ttu-id="ade14-183">Select **Next** to move on to the final step.</span><span class="sxs-lookup"><span data-stu-id="ade14-183">Select **Next** to move on to the final step.</span></span>

### <a name="step-5-review-template"></a><span data-ttu-id="ade14-184">Step 5: Review Template</span><span class="sxs-lookup"><span data-stu-id="ade14-184">Step 5: Review Template</span></span>

<span data-ttu-id="ade14-185">Review your deployment information, then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="ade14-185">Review your deployment information, then select **Submit**.</span></span>

## <a name="monitor-a-deployment"></a><span data-ttu-id="ade14-186">Monitor a deployment</span><span class="sxs-lookup"><span data-stu-id="ade14-186">Monitor a deployment</span></span>

<span data-ttu-id="ade14-187">To view the details of a deployment and monitor the devices running it, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ade14-187">To view the details of a deployment and monitor the devices running it, use the following steps:</span></span>

1. <span data-ttu-id="ade14-188">Sign in to the [Azure portal][lnk-portal] and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-188">Sign in to the [Azure portal][lnk-portal] and navigate to your IoT hub.</span></span> 
1. <span data-ttu-id="ade14-189">Select **IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="ade14-189">Select **IoT Edge**.</span></span>
1. <span data-ttu-id="ade14-190">Select **IoT Edge deployments**.</span><span class="sxs-lookup"><span data-stu-id="ade14-190">Select **IoT Edge deployments**.</span></span> 

   ![View IoT Edge deployments][1]

1. <span data-ttu-id="ade14-192">Inspect the deployment list.</span><span class="sxs-lookup"><span data-stu-id="ade14-192">Inspect the deployment list.</span></span> <span data-ttu-id="ade14-193">For each deployment, you can view the following details:</span><span class="sxs-lookup"><span data-stu-id="ade14-193">For each deployment, you can view the following details:</span></span>
   * <span data-ttu-id="ade14-194">**ID** - the name of the deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-194">**ID** - the name of the deployment.</span></span>
   * <span data-ttu-id="ade14-195">**Target condition** - the tag used to define targeted devices.</span><span class="sxs-lookup"><span data-stu-id="ade14-195">**Target condition** - the tag used to define targeted devices.</span></span>
   * <span data-ttu-id="ade14-196">**Priority** - the priority number assigned to the deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-196">**Priority** - the priority number assigned to the deployment.</span></span>
   * <span data-ttu-id="ade14-197">**System metrics** - **Targeted** specifies the number of device twins in IoT Hub that match the targeting condition, and **Applied** specifies the number of devices that have had the deployment content applied to their module twins in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-197">**System metrics** - **Targeted** specifies the number of device twins in IoT Hub that match the targeting condition, and **Applied** specifies the number of devices that have had the deployment content applied to their module twins in IoT Hub.</span></span> 
   * <span data-ttu-id="ade14-198">**Device metrics** - the number of Edge devices in the deployment reporting success or errors from the IoT Edge client runtime.</span><span class="sxs-lookup"><span data-stu-id="ade14-198">**Device metrics** - the number of Edge devices in the deployment reporting success or errors from the IoT Edge client runtime.</span></span>
   * <span data-ttu-id="ade14-199">**Creation time** - the timestamp from when the deployment was created.</span><span class="sxs-lookup"><span data-stu-id="ade14-199">**Creation time** - the timestamp from when the deployment was created.</span></span> <span data-ttu-id="ade14-200">This timestamp is used to break ties when two deployments have the same priority.</span><span class="sxs-lookup"><span data-stu-id="ade14-200">This timestamp is used to break ties when two deployments have the same priority.</span></span> 
2. <span data-ttu-id="ade14-201">Select the deployment that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="ade14-201">Select the deployment that you want to monitor.</span></span>  
3. <span data-ttu-id="ade14-202">Inspect the deployment details.</span><span class="sxs-lookup"><span data-stu-id="ade14-202">Inspect the deployment details.</span></span> <span data-ttu-id="ade14-203">You can use tabs to review the details of the deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-203">You can use tabs to review the details of the deployment.</span></span>

## <a name="modify-a-deployment"></a><span data-ttu-id="ade14-204">Modify a deployment</span><span class="sxs-lookup"><span data-stu-id="ade14-204">Modify a deployment</span></span>

<span data-ttu-id="ade14-205">When you modify a deployment, the changes immediately replicate to all targeted devices.</span><span class="sxs-lookup"><span data-stu-id="ade14-205">When you modify a deployment, the changes immediately replicate to all targeted devices.</span></span> 

<span data-ttu-id="ade14-206">If you update the target condition, the following updates occur:</span><span class="sxs-lookup"><span data-stu-id="ade14-206">If you update the target condition, the following updates occur:</span></span>
* <span data-ttu-id="ade14-207">If a device didn't meet the old target condition, but meets the new target condition and this deployment is the highest priority for that device, then this deployment is applied to the device.</span><span class="sxs-lookup"><span data-stu-id="ade14-207">If a device didn't meet the old target condition, but meets the new target condition and this deployment is the highest priority for that device, then this deployment is applied to the device.</span></span> 
* <span data-ttu-id="ade14-208">If a device currently running this deployment no longer meets the target condition, it uninstalls this deployment and takes on the next highest priority deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-208">If a device currently running this deployment no longer meets the target condition, it uninstalls this deployment and takes on the next highest priority deployment.</span></span> 
* <span data-ttu-id="ade14-209">If a device currently running this deployment no longer meets the target condition and doesn't meet the target condition of any other deployments, then no change occurs on the device.</span><span class="sxs-lookup"><span data-stu-id="ade14-209">If a device currently running this deployment no longer meets the target condition and doesn't meet the target condition of any other deployments, then no change occurs on the device.</span></span> <span data-ttu-id="ade14-210">The device continues running its current modules in their current state, but is not managed as part of this deployment anymore.</span><span class="sxs-lookup"><span data-stu-id="ade14-210">The device continues running its current modules in their current state, but is not managed as part of this deployment anymore.</span></span> <span data-ttu-id="ade14-211">Once it meets the target condition of any other deployment, it uninstalls this deployment and takes on the new one.</span><span class="sxs-lookup"><span data-stu-id="ade14-211">Once it meets the target condition of any other deployment, it uninstalls this deployment and takes on the new one.</span></span> 

<span data-ttu-id="ade14-212">To modify a deployment, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ade14-212">To modify a deployment, use the following steps:</span></span> 

1. <span data-ttu-id="ade14-213">Sign in to the [Azure portal][lnk-portal] and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-213">Sign in to the [Azure portal][lnk-portal] and navigate to your IoT hub.</span></span> 
1. <span data-ttu-id="ade14-214">Select **IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="ade14-214">Select **IoT Edge**.</span></span>
1. <span data-ttu-id="ade14-215">Select **IoT Edge deployments**.</span><span class="sxs-lookup"><span data-stu-id="ade14-215">Select **IoT Edge deployments**.</span></span> 

   ![View IoT Edge deployments][1]

1. <span data-ttu-id="ade14-217">Select the deployment that you want to modify.</span><span class="sxs-lookup"><span data-stu-id="ade14-217">Select the deployment that you want to modify.</span></span> 
1. <span data-ttu-id="ade14-218">Make updates to the following fields:</span><span class="sxs-lookup"><span data-stu-id="ade14-218">Make updates to the following fields:</span></span> 
   * <span data-ttu-id="ade14-219">Target condition</span><span class="sxs-lookup"><span data-stu-id="ade14-219">Target condition</span></span> 
   * <span data-ttu-id="ade14-220">Labels</span><span class="sxs-lookup"><span data-stu-id="ade14-220">Labels</span></span> 
   * <span data-ttu-id="ade14-221">Priority</span><span class="sxs-lookup"><span data-stu-id="ade14-221">Priority</span></span> 
1. <span data-ttu-id="ade14-222">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ade14-222">Select **Save**.</span></span>
1. <span data-ttu-id="ade14-223">Follow the steps in [Monitor a deployment][anchor-monitor] to watch the changes roll out.</span><span class="sxs-lookup"><span data-stu-id="ade14-223">Follow the steps in [Monitor a deployment][anchor-monitor] to watch the changes roll out.</span></span> 

## <a name="delete-a-deployment"></a><span data-ttu-id="ade14-224">Delete a deployment</span><span class="sxs-lookup"><span data-stu-id="ade14-224">Delete a deployment</span></span>

<span data-ttu-id="ade14-225">When you delete a deployment, any devices take on their next highest priority deployment.</span><span class="sxs-lookup"><span data-stu-id="ade14-225">When you delete a deployment, any devices take on their next highest priority deployment.</span></span> <span data-ttu-id="ade14-226">If your devices don't meet the target condition of any other deployment, then the modules are not removed when the deployment is deleted.</span><span class="sxs-lookup"><span data-stu-id="ade14-226">If your devices don't meet the target condition of any other deployment, then the modules are not removed when the deployment is deleted.</span></span> 

1. <span data-ttu-id="ade14-227">Sign in to the [Azure portal][lnk-portal] and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ade14-227">Sign in to the [Azure portal][lnk-portal] and navigate to your IoT hub.</span></span> 
1. <span data-ttu-id="ade14-228">Select **IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="ade14-228">Select **IoT Edge**.</span></span>
1. <span data-ttu-id="ade14-229">Select **IoT Edge deployments**.</span><span class="sxs-lookup"><span data-stu-id="ade14-229">Select **IoT Edge deployments**.</span></span> 

   ![View IoT Edge deployments][1]

1. <span data-ttu-id="ade14-231">Use the checkbox to select the deployment that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="ade14-231">Use the checkbox to select the deployment that you want to delete.</span></span> 
1. <span data-ttu-id="ade14-232">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ade14-232">Select **Delete**.</span></span>
1. <span data-ttu-id="ade14-233">A prompt will inform you that this action will delete this deployment and revert to the previous state for all devices.</span><span class="sxs-lookup"><span data-stu-id="ade14-233">A prompt will inform you that this action will delete this deployment and revert to the previous state for all devices.</span></span>  <span data-ttu-id="ade14-234">This means that a deployment with a lower priority will apply.</span><span class="sxs-lookup"><span data-stu-id="ade14-234">This means that a deployment with a lower priority will apply.</span></span>  <span data-ttu-id="ade14-235">If no other deployment is targeted, no modules will be removed.</span><span class="sxs-lookup"><span data-stu-id="ade14-235">If no other deployment is targeted, no modules will be removed.</span></span> <span data-ttu-id="ade14-236">If you want to remove all modules from your device, create a deployment with zero modules and deploy it to the same devices.</span><span class="sxs-lookup"><span data-stu-id="ade14-236">If you want to remove all modules from your device, create a deployment with zero modules and deploy it to the same devices.</span></span> <span data-ttu-id="ade14-237">Select **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="ade14-237">Select **Yes** to continue.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ade14-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="ade14-238">Next steps</span></span>

<span data-ttu-id="ade14-239">Learn more about [Deploying modules to Edge devices][lnk-deployments].</span><span class="sxs-lookup"><span data-stu-id="ade14-239">Learn more about [Deploying modules to Edge devices][lnk-deployments].</span></span>

<!-- Images -->
[1]: ./media/how-to-deploy-monitor/iot-edge-deployments.png

<!-- Links -->
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-portal]: https://portal.azure.com
[lnk-docker-create]: https://docs.docker.com/engine/reference/commandline/create/
[lnk-deployments]: module-deployment-monitoring.md

<!-- Anchor links -->
[anchor-monitor]: #monitor-a-deployment
