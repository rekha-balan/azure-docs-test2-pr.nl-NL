---
title: Deploy Azure IoT Edge modules (portal) | Microsoft Docs
description: Use the Azure portal to deploy modules to an IoT Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/06/2018
ms.topic: conceptual
ms.reviewer: menchi
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 83f199c49209210ec577017534f93e36d05bd70a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856011"
---
# <a name="deploy-azure-iot-edge-modules-from-the-azure-portal"></a><span data-ttu-id="77541-103">Deploy Azure IoT Edge modules from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="77541-103">Deploy Azure IoT Edge modules from the Azure portal</span></span>

<span data-ttu-id="77541-104">Once you create IoT Edge modules with your business logic, you want to deploy them to your devices to operate at the edge.</span><span class="sxs-lookup"><span data-stu-id="77541-104">Once you create IoT Edge modules with your business logic, you want to deploy them to your devices to operate at the edge.</span></span> <span data-ttu-id="77541-105">If you have multiple modules that work together to collect and process data, you can deploy them all at once and declare the routing rules that connect them.</span><span class="sxs-lookup"><span data-stu-id="77541-105">If you have multiple modules that work together to collect and process data, you can deploy them all at once and declare the routing rules that connect them.</span></span> 

<span data-ttu-id="77541-106">This article shows how the Azure portal guides you through creating a deployment manifest and pushing the deployment to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="77541-106">This article shows how the Azure portal guides you through creating a deployment manifest and pushing the deployment to an IoT Edge device.</span></span> <span data-ttu-id="77541-107">For information about creating a deployment that targets multiple devices based on their shared tags, see [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="77541-107">For information about creating a deployment that targets multiple devices based on their shared tags, see [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77541-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77541-108">Prerequisites</span></span>

* <span data-ttu-id="77541-109">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="77541-109">An [IoT hub](../iot-hub/iot-hub-create-through-portal.md) in your Azure subscription.</span></span> 
* <span data-ttu-id="77541-110">An [IoT Edge device](how-to-register-device-portal.md) with the IoT Edge runtime installed.</span><span class="sxs-lookup"><span data-stu-id="77541-110">An [IoT Edge device](how-to-register-device-portal.md) with the IoT Edge runtime installed.</span></span> 

## <a name="select-your-device"></a><span data-ttu-id="77541-111">Select your device</span><span class="sxs-lookup"><span data-stu-id="77541-111">Select your device</span></span>

1. <span data-ttu-id="77541-112">Sign in to the [Azure portal](https://portal.azure.com) and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="77541-112">Sign in to the [Azure portal](https://portal.azure.com) and navigate to your IoT hub.</span></span>
2. <span data-ttu-id="77541-113">Select **IoT Edge** from the menu.</span><span class="sxs-lookup"><span data-stu-id="77541-113">Select **IoT Edge** from the menu.</span></span>
3. <span data-ttu-id="77541-114">Click on the ID of the target device from the list of devices.</span><span class="sxs-lookup"><span data-stu-id="77541-114">Click on the ID of the target device from the list of devices.</span></span> 
4. <span data-ttu-id="77541-115">Select **Set Modules**.</span><span class="sxs-lookup"><span data-stu-id="77541-115">Select **Set Modules**.</span></span>

## <a name="configure-a-deployment-manifest"></a><span data-ttu-id="77541-116">Configure a deployment manifest</span><span class="sxs-lookup"><span data-stu-id="77541-116">Configure a deployment manifest</span></span>

<span data-ttu-id="77541-117">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span><span class="sxs-lookup"><span data-stu-id="77541-117">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span></span> <span data-ttu-id="77541-118">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span><span class="sxs-lookup"><span data-stu-id="77541-118">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span></span>

<span data-ttu-id="77541-119">The Azure portal has a wizard that walks you through creating the deployment manifest, instead of building the JSON document manually.</span><span class="sxs-lookup"><span data-stu-id="77541-119">The Azure portal has a wizard that walks you through creating the deployment manifest, instead of building the JSON document manually.</span></span> <span data-ttu-id="77541-120">It has three steps: **Add modules**, **Specify routes**, and **Review deployment**.</span><span class="sxs-lookup"><span data-stu-id="77541-120">It has three steps: **Add modules**, **Specify routes**, and **Review deployment**.</span></span> 

### <a name="add-modules"></a><span data-ttu-id="77541-121">Add modules</span><span class="sxs-lookup"><span data-stu-id="77541-121">Add modules</span></span>

1. <span data-ttu-id="77541-122">In the **Registry settings** section of the page, provide the credentials to access any private container registries that contain your module images.</span><span class="sxs-lookup"><span data-stu-id="77541-122">In the **Registry settings** section of the page, provide the credentials to access any private container registries that contain your module images.</span></span> 
2. <span data-ttu-id="77541-123">In the **Deployment modules** section of the page, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="77541-123">In the **Deployment modules** section of the page, select **Add**.</span></span> 
3. <span data-ttu-id="77541-124">Look at the types of modules from the drop-down list:</span><span class="sxs-lookup"><span data-stu-id="77541-124">Look at the types of modules from the drop-down list:</span></span> 
   * <span data-ttu-id="77541-125">**IoT Edge Module** - the default option.</span><span class="sxs-lookup"><span data-stu-id="77541-125">**IoT Edge Module** - the default option.</span></span>
   * <span data-ttu-id="77541-126">**Azure Stream Analytics Module** - only modules generated from an Azure Stream Analytics workload.</span><span class="sxs-lookup"><span data-stu-id="77541-126">**Azure Stream Analytics Module** - only modules generated from an Azure Stream Analytics workload.</span></span> 
4. <span data-ttu-id="77541-127">Select the **IoT Edge Module**.</span><span class="sxs-lookup"><span data-stu-id="77541-127">Select the **IoT Edge Module**.</span></span>
5. <span data-ttu-id="77541-128">Provide a name for the module, then specify the container image.</span><span class="sxs-lookup"><span data-stu-id="77541-128">Provide a name for the module, then specify the container image.</span></span> <span data-ttu-id="77541-129">For example:</span><span class="sxs-lookup"><span data-stu-id="77541-129">For example:</span></span> 
   * <span data-ttu-id="77541-130">**Name** - tempSensor</span><span class="sxs-lookup"><span data-stu-id="77541-130">**Name** - tempSensor</span></span>
   * <span data-ttu-id="77541-131">**Image URI** - mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0</span><span class="sxs-lookup"><span data-stu-id="77541-131">**Image URI** - mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0</span></span>
6. <span data-ttu-id="77541-132">Fill out the optional fields if necessary.</span><span class="sxs-lookup"><span data-stu-id="77541-132">Fill out the optional fields if necessary.</span></span> <span data-ttu-id="77541-133">For more information about container create options, restart policy, and desired status see [EdgeAgent desired properties](module-edgeagent-edgehub.md#edgeagent-desired-properties).</span><span class="sxs-lookup"><span data-stu-id="77541-133">For more information about container create options, restart policy, and desired status see [EdgeAgent desired properties](module-edgeagent-edgehub.md#edgeagent-desired-properties).</span></span> <span data-ttu-id="77541-134">For more information about the module twin see [Define or update desired properties](module-composition.md#define-or-update-desired-properties).</span><span class="sxs-lookup"><span data-stu-id="77541-134">For more information about the module twin see [Define or update desired properties](module-composition.md#define-or-update-desired-properties).</span></span>
7. <span data-ttu-id="77541-135">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="77541-135">Select **Save**.</span></span>
8. <span data-ttu-id="77541-136">Repeat steps 2-6 to add additional modules to your deployment.</span><span class="sxs-lookup"><span data-stu-id="77541-136">Repeat steps 2-6 to add additional modules to your deployment.</span></span> 
9. <span data-ttu-id="77541-137">Select **Next** to continue to the routes section.</span><span class="sxs-lookup"><span data-stu-id="77541-137">Select **Next** to continue to the routes section.</span></span>

### <a name="specify-routes"></a><span data-ttu-id="77541-138">Specify routes</span><span class="sxs-lookup"><span data-stu-id="77541-138">Specify routes</span></span>

<span data-ttu-id="77541-139">By default the wizard gives you a route called **route** and defined as \**FROM /* INTO $upstream\*\*, which means that any messages output by any modules are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="77541-139">By default the wizard gives you a route called **route** and defined as \**FROM /* INTO $upstream\*\*, which means that any messages output by any modules are sent to your IoT hub.</span></span>  

<span data-ttu-id="77541-140">Add or update the routes with information from [Declare routes](module-composition.md#declare-routes), then select **Next** to continue to the review section.</span><span class="sxs-lookup"><span data-stu-id="77541-140">Add or update the routes with information from [Declare routes](module-composition.md#declare-routes), then select **Next** to continue to the review section.</span></span>

### <a name="review-deployment"></a><span data-ttu-id="77541-141">Review deployment</span><span class="sxs-lookup"><span data-stu-id="77541-141">Review deployment</span></span>

<span data-ttu-id="77541-142">The review section shows you the JSON deployment manifest that was created based on your selections in the previous two sections.</span><span class="sxs-lookup"><span data-stu-id="77541-142">The review section shows you the JSON deployment manifest that was created based on your selections in the previous two sections.</span></span> <span data-ttu-id="77541-143">Note that there are two modules declared that you didn't add: **$edgeAgent** and **$edgeHub**.</span><span class="sxs-lookup"><span data-stu-id="77541-143">Note that there are two modules declared that you didn't add: **$edgeAgent** and **$edgeHub**.</span></span> <span data-ttu-id="77541-144">These two modules make up the [IoT Edge runtime](iot-edge-runtime.md) and are required defaults in every deployment.</span><span class="sxs-lookup"><span data-stu-id="77541-144">These two modules make up the [IoT Edge runtime](iot-edge-runtime.md) and are required defaults in every deployment.</span></span> 

<span data-ttu-id="77541-145">Review your deployment information, then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="77541-145">Review your deployment information, then select **Submit**.</span></span> 

## <a name="view-modules-on-your-device"></a><span data-ttu-id="77541-146">View modules on your device</span><span class="sxs-lookup"><span data-stu-id="77541-146">View modules on your device</span></span>

<span data-ttu-id="77541-147">Once you've deployed modules to your device, you can view all of them in the **Device details** page of the portal.</span><span class="sxs-lookup"><span data-stu-id="77541-147">Once you've deployed modules to your device, you can view all of them in the **Device details** page of the portal.</span></span> <span data-ttu-id="77541-148">This page displays the name of each deployed module, as well as useful information like the deployment status and exit code.</span><span class="sxs-lookup"><span data-stu-id="77541-148">This page displays the name of each deployed module, as well as useful information like the deployment status and exit code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="77541-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="77541-149">Next steps</span></span>

<span data-ttu-id="77541-150">Learn how to [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="77541-150">Learn how to [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md)</span></span>
