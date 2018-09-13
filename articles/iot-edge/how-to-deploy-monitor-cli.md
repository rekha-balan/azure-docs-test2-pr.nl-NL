---
title: Deploy and monitor modules for Azure IoT Edge (CLI) | Microsoft Docs
description: Manage the modules that run on edge devices
keywords: ''
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 07/25/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: b90c26eaa36c906dda904106b104c3dbf04a55ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968032"
---
# <a name="deploy-and-monitor-iot-edge-modules-at-scale-using-the-azure-cli"></a><span data-ttu-id="8b4fa-103">Deploy and monitor IoT Edge modules at scale using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b4fa-103">Deploy and monitor IoT Edge modules at scale using the Azure CLI</span></span>

[!INCLUDE [iot-edge-how-to-deploy-monitor-selector](../../includes/iot-edge-how-to-deploy-monitor-selector.md)]

<span data-ttu-id="8b4fa-104">Azure IoT Edge enables you to move analytics to the edge and provides a cloud interface so that you can manage and monitor your IoT Edge devices without having to physically access each one.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-104">Azure IoT Edge enables you to move analytics to the edge and provides a cloud interface so that you can manage and monitor your IoT Edge devices without having to physically access each one.</span></span> <span data-ttu-id="8b4fa-105">The capability to remotely manage devices is increasingly important as Internet of Things solutions are growing larger and more complex.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-105">The capability to remotely manage devices is increasingly important as Internet of Things solutions are growing larger and more complex.</span></span> <span data-ttu-id="8b4fa-106">Azure IoT Edge is designed to support your business goals, no matter how many devices you add.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-106">Azure IoT Edge is designed to support your business goals, no matter how many devices you add.</span></span>

<span data-ttu-id="8b4fa-107">You can manage individual devices and deploy modules to them one at a time.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-107">You can manage individual devices and deploy modules to them one at a time.</span></span> <span data-ttu-id="8b4fa-108">However, if you want to make changes to devices at a large scale, you can create an **IoT Edge automatic deployment**, which is part of Automatic Device Management in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-108">However, if you want to make changes to devices at a large scale, you can create an **IoT Edge automatic deployment**, which is part of Automatic Device Management in IoT Hub.</span></span> <span data-ttu-id="8b4fa-109">Deployments are dynamic processes that enable you to deploy multiple modules to multiple devices at once, track the status and health of the modules, and make changes when necessary.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-109">Deployments are dynamic processes that enable you to deploy multiple modules to multiple devices at once, track the status and health of the modules, and make changes when necessary.</span></span> 

<span data-ttu-id="8b4fa-110">In this article, you set up Azure CLI 2.0 and the IoT extension.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-110">In this article, you set up Azure CLI 2.0 and the IoT extension.</span></span> <span data-ttu-id="8b4fa-111">Then you learn how to deploy modules to a set of IoT Edge devices and monitor the progress using the available CLI commands.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-111">Then you learn how to deploy modules to a set of IoT Edge devices and monitor the progress using the available CLI commands.</span></span>

## <a name="cli-prerequisites"></a><span data-ttu-id="8b4fa-112">CLI Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b4fa-112">CLI Prerequisites</span></span>

* <span data-ttu-id="8b4fa-113">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-113">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span></span> 
* <span data-ttu-id="8b4fa-114">[IoT Edge devices](how-to-register-device-cli.md) with the IoT Edge runtime installed.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-114">[IoT Edge devices](how-to-register-device-cli.md) with the IoT Edge runtime installed.</span></span>
* <span data-ttu-id="8b4fa-115">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-115">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span></span> <span data-ttu-id="8b4fa-116">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-116">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span></span> <span data-ttu-id="8b4fa-117">Use `az –-version` to validate.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-117">Use `az –-version` to validate.</span></span> <span data-ttu-id="8b4fa-118">This version supports az extension commands and introduces the Knack command framework.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-118">This version supports az extension commands and introduces the Knack command framework.</span></span> 
* <span data-ttu-id="8b4fa-119">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span><span class="sxs-lookup"><span data-stu-id="8b4fa-119">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span></span>

## <a name="configure-a-deployment-manifest"></a><span data-ttu-id="8b4fa-120">Configure a deployment manifest</span><span class="sxs-lookup"><span data-stu-id="8b4fa-120">Configure a deployment manifest</span></span>

<span data-ttu-id="8b4fa-121">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-121">A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins.</span></span> <span data-ttu-id="8b4fa-122">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span><span class="sxs-lookup"><span data-stu-id="8b4fa-122">For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](module-composition.md).</span></span>

<span data-ttu-id="8b4fa-123">To deploy modules using Azure CLI 2.0, save the deployment manifest locally as a .txt file.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-123">To deploy modules using Azure CLI 2.0, save the deployment manifest locally as a .txt file.</span></span> <span data-ttu-id="8b4fa-124">You will use the file path in the next section when you run the command to apply the configuration to your device.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-124">You will use the file path in the next section when you run the command to apply the configuration to your device.</span></span> 

<span data-ttu-id="8b4fa-125">Here's a basic deployment manifest with one module as an example:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-125">Here's a basic deployment manifest with one module as an example:</span></span>

   ```json
   {
        "content": {
         "modulesContent": {
           "$edgeAgent": {
             "properties.desired": {
               "schemaVersion": "1.0",
               "runtime": {
                 "type": "docker",
                 "settings": {
                   "minDockerVersion": "v1.25",
                   "loggingOptions": "",
                   "registryCredentials": {
                     "registryName": {
                       "username": "",
                       "password": "",
                       "address": ""
                     }
                   }
               },
               "systemModules": {
                 "edgeAgent": {
                   "type": "docker",
                   "settings": {
                     "image": "mcr.microsoft.com/azureiotedge-agent:1.0",
                     "createOptions": "{}"
                   }
                 },
                 "edgeHub": {
                   "type": "docker",
                   "status": "running",
                   "restartPolicy": "always",
                   "settings": {
                     "image": "mcr.microsoft.com/azureiotedge-hub:1.0",
                     "createOptions": "{}"
                   }
                 }
               },
               "modules": {
                 "tempSensor": {
                   "version": "1.0",
                   "type": "docker",
                   "status": "running",
                   "restartPolicy": "always",
                   "settings": {
                     "image": "mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0",
                     "createOptions": "{}"
                   }
                 }
               }
             }
           },
           "$edgeHub": {
             "properties.desired": {
               "schemaVersion": "1.0",
               "routes": {
                   "route": "FROM /* INTO $upstream"
               },
               "storeAndForwardConfiguration": {
                 "timeToLiveSecs": 7200
               }
             }
           },
           "tempSensor": {
             "properties.desired": {}
           }
         }
       }
   }
   ```


## <a name="identify-devices-using-tags"></a><span data-ttu-id="8b4fa-126">Identify devices using tags</span><span class="sxs-lookup"><span data-stu-id="8b4fa-126">Identify devices using tags</span></span>

<span data-ttu-id="8b4fa-127">Before you can create a deployment, you have to be able to specify which devices you want to affect.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-127">Before you can create a deployment, you have to be able to specify which devices you want to affect.</span></span> <span data-ttu-id="8b4fa-128">Azure IoT Edge identifies devices using **tags** in the device twin.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-128">Azure IoT Edge identifies devices using **tags** in the device twin.</span></span> <span data-ttu-id="8b4fa-129">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-129">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span></span> <span data-ttu-id="8b4fa-130">For example, if you manage a campus of smart buildings, you might add the following tags to a device:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-130">For example, if you manage a campus of smart buildings, you might add the following tags to a device:</span></span>

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

<span data-ttu-id="8b4fa-131">For more information about device twins and tags, see [Understand and use device twins in IoT Hub][lnk-device-twin].</span><span class="sxs-lookup"><span data-stu-id="8b4fa-131">For more information about device twins and tags, see [Understand and use device twins in IoT Hub][lnk-device-twin].</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="8b4fa-132">Create a deployment</span><span class="sxs-lookup"><span data-stu-id="8b4fa-132">Create a deployment</span></span>

<span data-ttu-id="8b4fa-133">You deploy modules to your target devices by creating a deployment that consists of the deployment manifest as well as other parameters.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-133">You deploy modules to your target devices by creating a deployment that consists of the deployment manifest as well as other parameters.</span></span> 

<span data-ttu-id="8b4fa-134">Use the following command to create a deployment:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-134">Use the following command to create a deployment:</span></span>

   ```cli
   az iot edge deployment create --deployment-id [deployment id] --labels [labels] --content [file path] --hub-name [hub name] --target-condition [target query] --priority [int]
   ```

* <span data-ttu-id="8b4fa-135">**--deployment-id** - The name of the deployment that will be created in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-135">**--deployment-id** - The name of the deployment that will be created in the IoT hub.</span></span> <span data-ttu-id="8b4fa-136">Give your deployment a unique name that is up to 128 lowercase letters.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-136">Give your deployment a unique name that is up to 128 lowercase letters.</span></span> <span data-ttu-id="8b4fa-137">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-137">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span></span>
* <span data-ttu-id="8b4fa-138">**--labels** - Add labels to help track your deployments.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-138">**--labels** - Add labels to help track your deployments.</span></span> <span data-ttu-id="8b4fa-139">Labels are Name, Value pairs that describe your deployment.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-139">Labels are Name, Value pairs that describe your deployment.</span></span> <span data-ttu-id="8b4fa-140">For example, `HostPlatform, Linux` or `Version, 3.0.1`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-140">For example, `HostPlatform, Linux` or `Version, 3.0.1`</span></span>
* <span data-ttu-id="8b4fa-141">**--content** - Filepath to the deployment manifest JSON.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-141">**--content** - Filepath to the deployment manifest JSON.</span></span> 
* <span data-ttu-id="8b4fa-142">**--hub-name** - Name of the IoT hub in which the deployment will be created.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-142">**--hub-name** - Name of the IoT hub in which the deployment will be created.</span></span> <span data-ttu-id="8b4fa-143">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-143">The hub must be in the current subscription.</span></span> <span data-ttu-id="8b4fa-144">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-144">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>
* <span data-ttu-id="8b4fa-145">**--target-condition** - Enter a target condition to determine which devices will be targeted with this deployment.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-145">**--target-condition** - Enter a target condition to determine which devices will be targeted with this deployment.</span></span> <span data-ttu-id="8b4fa-146">The condition is based on device twin tags or device twin reported properties and should match the expression format.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-146">The condition is based on device twin tags or device twin reported properties and should match the expression format.</span></span> <span data-ttu-id="8b4fa-147">For example, `tags.environment='test'` or `properties.reported.devicemodel='4000x'`.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-147">For example, `tags.environment='test'` or `properties.reported.devicemodel='4000x'`.</span></span> 
* <span data-ttu-id="8b4fa-148">**--priority** - A positive integer.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-148">**--priority** - A positive integer.</span></span> <span data-ttu-id="8b4fa-149">In the event that two or more deployments are targeted at the same device, the deployment with the highest numerical value for Priority will apply.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-149">In the event that two or more deployments are targeted at the same device, the deployment with the highest numerical value for Priority will apply.</span></span>

## <a name="monitor-a-deployment"></a><span data-ttu-id="8b4fa-150">Monitor a deployment</span><span class="sxs-lookup"><span data-stu-id="8b4fa-150">Monitor a deployment</span></span>

<span data-ttu-id="8b4fa-151">Use the following command to display the contents of a deployment:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-151">Use the following command to display the contents of a deployment:</span></span>

   ```cli
az iot edge deployment show --deployment-id [deployment id] --hub-name [hub name]
   ```
* <span data-ttu-id="8b4fa-152">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-152">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span></span>
* <span data-ttu-id="8b4fa-153">**--hub-name** - Name of the IoT hub in which the deployment exists.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-153">**--hub-name** - Name of the IoT hub in which the deployment exists.</span></span> <span data-ttu-id="8b4fa-154">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-154">The hub must be in the current subscription.</span></span> <span data-ttu-id="8b4fa-155">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-155">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>

<span data-ttu-id="8b4fa-156">Inspect the deployment in the command window.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-156">Inspect the deployment in the command window.</span></span> <span data-ttu-id="8b4fa-157">The **metrics** property lists a count for each metric that is evaluated by each hub:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-157">The **metrics** property lists a count for each metric that is evaluated by each hub:</span></span>
* <span data-ttu-id="8b4fa-158">**targetedCount** - A system metric that specifies the number of device twins in IoT Hub that match the targeting condition.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-158">**targetedCount** - A system metric that specifies the number of device twins in IoT Hub that match the targeting condition.</span></span>
* <span data-ttu-id="8b4fa-159">**appliedCount** - A system metric specifies the number of devices that have had the deployment content applied to their module twins in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-159">**appliedCount** - A system metric specifies the number of devices that have had the deployment content applied to their module twins in IoT Hub.</span></span>
* <span data-ttu-id="8b4fa-160">**reportedSuccessfulCount** - A device metric that specifies the number of Edge devices in the deployment reporting success from the IoT Edge client runtime.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-160">**reportedSuccessfulCount** - A device metric that specifies the number of Edge devices in the deployment reporting success from the IoT Edge client runtime.</span></span>
* <span data-ttu-id="8b4fa-161">**reportedFailedCount** - A device metric that specifies the number of Edge devices in the deployment reporting failure from the IoT Edge client runtime.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-161">**reportedFailedCount** - A device metric that specifies the number of Edge devices in the deployment reporting failure from the IoT Edge client runtime.</span></span>

<span data-ttu-id="8b4fa-162">You can show a list of device IDs or objects for each of the metrics by using the following command:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-162">You can show a list of device IDs or objects for each of the metrics by using the following command:</span></span>

   ```cli
az iot edge deployment show-metric --deployment-id [deployment id] --metric-id [metric id] --hub-name [hub name] 
   ```

* <span data-ttu-id="8b4fa-163">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-163">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span></span>
* <span data-ttu-id="8b4fa-164">**--metric-id** - The name of the metric for which you want to see the list of device IDs, for example `reportedFailedCount`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-164">**--metric-id** - The name of the metric for which you want to see the list of device IDs, for example `reportedFailedCount`</span></span>
* <span data-ttu-id="8b4fa-165">**--hub-name** - Name of the IoT hub in which the deployment exists.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-165">**--hub-name** - Name of the IoT hub in which the deployment exists.</span></span> <span data-ttu-id="8b4fa-166">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-166">The hub must be in the current subscription.</span></span> <span data-ttu-id="8b4fa-167">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-167">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>

## <a name="modify-a-deployment"></a><span data-ttu-id="8b4fa-168">Modify a deployment</span><span class="sxs-lookup"><span data-stu-id="8b4fa-168">Modify a deployment</span></span>

<span data-ttu-id="8b4fa-169">When you modify a deployment, the changes immediately replicate to all targeted devices.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-169">When you modify a deployment, the changes immediately replicate to all targeted devices.</span></span> 

<span data-ttu-id="8b4fa-170">If you update the target condition, the following updates occur:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-170">If you update the target condition, the following updates occur:</span></span>
* <span data-ttu-id="8b4fa-171">If a device didn't meet the old target condition, but meets the new target condition and this deployment is the highest priority for that device, then this deployment is applied to the device.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-171">If a device didn't meet the old target condition, but meets the new target condition and this deployment is the highest priority for that device, then this deployment is applied to the device.</span></span> 
* <span data-ttu-id="8b4fa-172">If a device currently running this deployment no longer meets the target condition, it uninstalls this deployment and takes on the next highest priority deployment.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-172">If a device currently running this deployment no longer meets the target condition, it uninstalls this deployment and takes on the next highest priority deployment.</span></span> 
* <span data-ttu-id="8b4fa-173">If a device currently running this deployment no longer meets the target condition and doesn't meet the target condition of any other deployments, then no change occurs on the device.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-173">If a device currently running this deployment no longer meets the target condition and doesn't meet the target condition of any other deployments, then no change occurs on the device.</span></span> <span data-ttu-id="8b4fa-174">The device continues running its current modules in their current state, but is not managed as part of this deployment anymore.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-174">The device continues running its current modules in their current state, but is not managed as part of this deployment anymore.</span></span> <span data-ttu-id="8b4fa-175">Once it meets the target condition of any other deployment, it uninstalls this deployment and takes on the new one.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-175">Once it meets the target condition of any other deployment, it uninstalls this deployment and takes on the new one.</span></span> 

<span data-ttu-id="8b4fa-176">Use the following command to update a deployment:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-176">Use the following command to update a deployment:</span></span>

   ```cli
az iot edge deployment update --deployment-id [deployment id] --hub-name [hub name] --set [property1.property2='value']
   ```
* <span data-ttu-id="8b4fa-177">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-177">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span></span>
* <span data-ttu-id="8b4fa-178">**--hub-name** - Name of the IoT hub in which the deployment exists.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-178">**--hub-name** - Name of the IoT hub in which the deployment exists.</span></span> <span data-ttu-id="8b4fa-179">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-179">The hub must be in the current subscription.</span></span> <span data-ttu-id="8b4fa-180">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-180">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>
* <span data-ttu-id="8b4fa-181">**--set** - Update a property in the deployment.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-181">**--set** - Update a property in the deployment.</span></span> <span data-ttu-id="8b4fa-182">You can update the following properties:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-182">You can update the following properties:</span></span>
    * <span data-ttu-id="8b4fa-183">targetCondition - for example `targetCondition=tags.location.state='Oregon'`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-183">targetCondition - for example `targetCondition=tags.location.state='Oregon'`</span></span>
    * <span data-ttu-id="8b4fa-184">labels</span><span class="sxs-lookup"><span data-stu-id="8b4fa-184">labels</span></span> 
    * <span data-ttu-id="8b4fa-185">priority</span><span class="sxs-lookup"><span data-stu-id="8b4fa-185">priority</span></span>


## <a name="delete-a-deployment"></a><span data-ttu-id="8b4fa-186">Delete a deployment</span><span class="sxs-lookup"><span data-stu-id="8b4fa-186">Delete a deployment</span></span>

<span data-ttu-id="8b4fa-187">When you delete a deployment, any devices take on their next highest priority deployment.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-187">When you delete a deployment, any devices take on their next highest priority deployment.</span></span> <span data-ttu-id="8b4fa-188">If your devices don't meet the target condition of any other deployment, then the modules are not removed when the deployment is deleted.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-188">If your devices don't meet the target condition of any other deployment, then the modules are not removed when the deployment is deleted.</span></span> 

<span data-ttu-id="8b4fa-189">Use the following command to delete a deployment:</span><span class="sxs-lookup"><span data-stu-id="8b4fa-189">Use the following command to delete a deployment:</span></span>

   ```cli
az iot edge deployment delete --deployment-id [deployment id] --hub-name [hub name] 
   ```
* <span data-ttu-id="8b4fa-190">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-190">**--deployment-id** - The name of the deployment that exists in the IoT hub.</span></span>
* <span data-ttu-id="8b4fa-191">**--hub-name** - Name of the IoT hub in which the deployment exists.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-191">**--hub-name** - Name of the IoT hub in which the deployment exists.</span></span> <span data-ttu-id="8b4fa-192">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="8b4fa-192">The hub must be in the current subscription.</span></span> <span data-ttu-id="8b4fa-193">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="8b4fa-193">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b4fa-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b4fa-194">Next steps</span></span>

<span data-ttu-id="8b4fa-195">Learn more about [Deploying modules to Edge devices][lnk-deployments].</span><span class="sxs-lookup"><span data-stu-id="8b4fa-195">Learn more about [Deploying modules to Edge devices][lnk-deployments].</span></span>

<!-- Images -->
[1]: ./media/how-to-deploy-monitor/iot-edge-deployments.png

<!-- Links -->
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-portal]: https://portal.azure.com
[lnk-docker-create]: https://docs.docker.com/engine/reference/commandline/create/
[lnk-deployments]: module-deployment-monitoring.md

<!-- Anchor links -->
[anchor-monitor]: #monitor-a-deployment
