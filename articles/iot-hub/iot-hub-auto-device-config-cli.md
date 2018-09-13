---
title: Configure and monitor IoT devices at scale with Azure IoT Hub (CLI) | Microsoft Docs
description: Use Azure IoT Hub automatic device configurations to assign a configuration to multiple devices
author: ChrisGMsft
manager: bruz
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 04/13/2018
ms.author: chrisgre
ms.openlocfilehash: f81ef3c231874f314d6fe023ba247a0bcff61e90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869252"
---
# <a name="configure-and-monitor-iot-devices-at-scale-using-the-azure-cli"></a><span data-ttu-id="d8a1b-103">Configure and monitor IoT devices at scale using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d8a1b-103">Configure and monitor IoT devices at scale using the Azure CLI</span></span>

[!INCLUDE [iot-edge-how-to-deploy-monitor-selector](../../includes/iot-hub-auto-device-config-selector.md)]

<span data-ttu-id="d8a1b-104">Automatic device management in Azure IoT Hub automates many of the repetitive and complex tasks of managing large device fleets over the entirety of their lifecycles.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-104">Automatic device management in Azure IoT Hub automates many of the repetitive and complex tasks of managing large device fleets over the entirety of their lifecycles.</span></span> <span data-ttu-id="d8a1b-105">With automatic device management, you can target a set of devices based on their properties, define a desired configuration, and let IoT Hub update devices whenever they come into scope.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-105">With automatic device management, you can target a set of devices based on their properties, define a desired configuration, and let IoT Hub update devices whenever they come into scope.</span></span>  <span data-ttu-id="d8a1b-106">This is performed using an automatic device configuration, which will also allow you to summarize completion and compliance, handle merging and conflicts, and roll out configurations in a phased approach.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-106">This is performed using an automatic device configuration, which will also allow you to summarize completion and compliance, handle merging and conflicts, and roll out configurations in a phased approach.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="d8a1b-107">Automatic device configurations work by updating a set of device twins with desired properties and reporting a summary based on device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-107">Automatic device configurations work by updating a set of device twins with desired properties and reporting a summary based on device twin reported properties.</span></span>  <span data-ttu-id="d8a1b-108">It introduces a new class and JSON document called a *Configuration* which has three parts:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-108">It introduces a new class and JSON document called a *Configuration* which has three parts:</span></span>

* <span data-ttu-id="d8a1b-109">The **target condition** defines the scope of device twins to be updated.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-109">The **target condition** defines the scope of device twins to be updated.</span></span> <span data-ttu-id="d8a1b-110">The target condition is specified as a query on device twin tags and/or reported properties.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-110">The target condition is specified as a query on device twin tags and/or reported properties.</span></span>

* <span data-ttu-id="d8a1b-111">The **target content** defines the desired properties to be added or updated in the targeted device twins.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-111">The **target content** defines the desired properties to be added or updated in the targeted device twins.</span></span> <span data-ttu-id="d8a1b-112">The content includes a path to the section of desired properties to be changed.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-112">The content includes a path to the section of desired properties to be changed.</span></span>

* <span data-ttu-id="d8a1b-113">The **metrics** define the summary counts of various configuration states such as **Success**, **In Progress**, and **Error**.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-113">The **metrics** define the summary counts of various configuration states such as **Success**, **In Progress**, and **Error**.</span></span> <span data-ttu-id="d8a1b-114">Custom metrics are specified as queries on device twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-114">Custom metrics are specified as queries on device twin reported properties.</span></span>  <span data-ttu-id="d8a1b-115">System metrics are default metrics that measure twin update status, such as the number of device twins that are targeted and the number of twins that have been successfully updated.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-115">System metrics are default metrics that measure twin update status, such as the number of device twins that are targeted and the number of twins that have been successfully updated.</span></span> 

## <a name="cli-prerequisites"></a><span data-ttu-id="d8a1b-116">CLI prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8a1b-116">CLI prerequisites</span></span>

* <span data-ttu-id="d8a1b-117">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-117">An [IoT hub](../iot-hub/iot-hub-create-using-cli.md) in your Azure subscription.</span></span> 
* <span data-ttu-id="d8a1b-118">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-118">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) in your environment.</span></span> <span data-ttu-id="d8a1b-119">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-119">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span></span> <span data-ttu-id="d8a1b-120">Use `az –-version` to validate.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-120">Use `az –-version` to validate.</span></span> <span data-ttu-id="d8a1b-121">This version supports az extension commands and introduces the Knack command framework.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-121">This version supports az extension commands and introduces the Knack command framework.</span></span> 
* <span data-ttu-id="d8a1b-122">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span><span class="sxs-lookup"><span data-stu-id="d8a1b-122">The [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span></span>

## <a name="implement-device-twins-to-configure-devices"></a><span data-ttu-id="d8a1b-123">Implement device twins to configure devices</span><span class="sxs-lookup"><span data-stu-id="d8a1b-123">Implement device twins to configure devices</span></span>

<span data-ttu-id="d8a1b-124">Automatic device configurations require the use of device twins to synchronize state between the cloud and devices.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-124">Automatic device configurations require the use of device twins to synchronize state between the cloud and devices.</span></span>  <span data-ttu-id="d8a1b-125">Refer to [Understand and use device twins in IoT Hub](iot-hub-devguide-device-twins.md) for guidance on using device twins.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-125">Refer to [Understand and use device twins in IoT Hub](iot-hub-devguide-device-twins.md) for guidance on using device twins.</span></span>

## <a name="identify-devices-using-tags"></a><span data-ttu-id="d8a1b-126">Identify devices using tags</span><span class="sxs-lookup"><span data-stu-id="d8a1b-126">Identify devices using tags</span></span>

<span data-ttu-id="d8a1b-127">Before you can create a configuration, you must specify which devices you want to affect.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-127">Before you can create a configuration, you must specify which devices you want to affect.</span></span> <span data-ttu-id="d8a1b-128">Azure IoT Hub identifies devices using tags in the device twin.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-128">Azure IoT Hub identifies devices using tags in the device twin.</span></span> <span data-ttu-id="d8a1b-129">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-129">Each device can have multiple tags, and you can define them any way that makes sense for your solution.</span></span> <span data-ttu-id="d8a1b-130">For example, if you manage devices in different locations, you may add the following tags to a device twin:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-130">For example, if you manage devices in different locations, you may add the following tags to a device twin:</span></span>

```json
"tags": {
    "location": {
        "state": "Washington",
        "city": "Tacoma"
    }
},
```

## <a name="define-the-target-content-and-metrics"></a><span data-ttu-id="d8a1b-131">Define the target content and metrics</span><span class="sxs-lookup"><span data-stu-id="d8a1b-131">Define the target content and metrics</span></span>

<span data-ttu-id="d8a1b-132">The target content and metric queries are specified as JSON documents that describe the device twin desired properties to be set and reported properties to be measured.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-132">The target content and metric queries are specified as JSON documents that describe the device twin desired properties to be set and reported properties to be measured.</span></span>  <span data-ttu-id="d8a1b-133">To create an automatic device configuration using Azure CLI 2.0, save the target content and metrics locally as .txt files.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-133">To create an automatic device configuration using Azure CLI 2.0, save the target content and metrics locally as .txt files.</span></span> <span data-ttu-id="d8a1b-134">You use the file paths in a later next section when you run the command to apply the configuration to your device.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-134">You use the file paths in a later next section when you run the command to apply the configuration to your device.</span></span> 

<span data-ttu-id="d8a1b-135">Here's a basic target content sample:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-135">Here's a basic target content sample:</span></span>

```json
{
  "content": {
    "deviceContent": {
      "properties.desired.chillerWaterSettings": {
        "temperature": 38,
        "pressure": 78
      }
    }
}
```

<span data-ttu-id="d8a1b-136">Here are examples of metric queries:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-136">Here are examples of metric queries:</span></span>

```json
{
  "queries": {
    "Compliant": "select deviceId from devices where configurations.[[chillersettingswashington]].status = 'Applied' AND properties.reported.chillerWaterSettings.status='current'",
    "Error": "select deviceId from devices where configurations.[[chillersettingswashington]].status = 'Applied' AND properties.reported.chillerWaterSettings.status='error'",
    "Pending": "select deviceId from devices where configurations.[[chillersettingswashington]].status = 'Applied' AND properties.reported.chillerWaterSettings.status='pending'"
  }
}
```

## <a name="create-a-configuration"></a><span data-ttu-id="d8a1b-137">Create a configuration</span><span class="sxs-lookup"><span data-stu-id="d8a1b-137">Create a configuration</span></span>

<span data-ttu-id="d8a1b-138">You configure target devices by creating a configuration that consists of the target content and metrics.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-138">You configure target devices by creating a configuration that consists of the target content and metrics.</span></span> 

<span data-ttu-id="d8a1b-139">Use the following command to create a configuration:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-139">Use the following command to create a configuration:</span></span>

```cli
   az iot hub configuration create --config-id [configuration id] \
     --labels [labels] --content [file path] --hub-name [hub name] \
     --target-condition [target query] --priority [int] \
     --metrics [metric queries]
```

* <span data-ttu-id="d8a1b-140">--**config-id** - The name of the configuration that will be created in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-140">--**config-id** - The name of the configuration that will be created in the IoT hub.</span></span> <span data-ttu-id="d8a1b-141">Give your configuration a unique name that is up to 128 lowercase letters.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-141">Give your configuration a unique name that is up to 128 lowercase letters.</span></span> <span data-ttu-id="d8a1b-142">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-142">Avoid spaces and the following invalid characters: `& ^ [ ] { } \ | " < > /`.</span></span>

* <span data-ttu-id="d8a1b-143">--**labels** - Add labels to help track your configuration.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-143">--**labels** - Add labels to help track your configuration.</span></span> <span data-ttu-id="d8a1b-144">Labels are Name, Value pairs that describe your deployment.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-144">Labels are Name, Value pairs that describe your deployment.</span></span> <span data-ttu-id="d8a1b-145">For example, `HostPlatform, Linux` or `Version, 3.0.1`</span><span class="sxs-lookup"><span data-stu-id="d8a1b-145">For example, `HostPlatform, Linux` or `Version, 3.0.1`</span></span>

* <span data-ttu-id="d8a1b-146">--**content** - Inline JSON or file path to the target content to be set as twin desired properties.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-146">--**content** - Inline JSON or file path to the target content to be set as twin desired properties.</span></span> 

* <span data-ttu-id="d8a1b-147">--**hub-name** - Name of the IoT hub in which the configuration will be created.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-147">--**hub-name** - Name of the IoT hub in which the configuration will be created.</span></span> <span data-ttu-id="d8a1b-148">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-148">The hub must be in the current subscription.</span></span> <span data-ttu-id="d8a1b-149">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="d8a1b-149">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>

* <span data-ttu-id="d8a1b-150">--**target-condition** - Enter a target condition to determine which devices will be targeted with this configuration.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-150">--**target-condition** - Enter a target condition to determine which devices will be targeted with this configuration.</span></span> <span data-ttu-id="d8a1b-151">The condition is based on device twin tags or device twin desired properties and should match the expression format.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-151">The condition is based on device twin tags or device twin desired properties and should match the expression format.</span></span> <span data-ttu-id="d8a1b-152">For example, `tags.environment='test'` or `properties.desired.devicemodel='4000x'`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-152">For example, `tags.environment='test'` or `properties.desired.devicemodel='4000x'`.</span></span> 

* <span data-ttu-id="d8a1b-153">--**priority** - A positive integer.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-153">--**priority** - A positive integer.</span></span> <span data-ttu-id="d8a1b-154">In the event that two or more configurations are targeted at the same device, the configuration with the highest numerical value for Priority will apply.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-154">In the event that two or more configurations are targeted at the same device, the configuration with the highest numerical value for Priority will apply.</span></span>

* <span data-ttu-id="d8a1b-155">--**metrics** - Filepath to the metric queries.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-155">--**metrics** - Filepath to the metric queries.</span></span> <span data-ttu-id="d8a1b-156">Metrics provide summary counts of the various states that a device may report back as a result of applying configuration content.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-156">Metrics provide summary counts of the various states that a device may report back as a result of applying configuration content.</span></span> <span data-ttu-id="d8a1b-157">For example, you may create a metric for pending settings changes, a metric for errors, and a metric for successful settings changes.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-157">For example, you may create a metric for pending settings changes, a metric for errors, and a metric for successful settings changes.</span></span> 

## <a name="monitor-a-configuration"></a><span data-ttu-id="d8a1b-158">Monitor a configuration</span><span class="sxs-lookup"><span data-stu-id="d8a1b-158">Monitor a configuration</span></span>

<span data-ttu-id="d8a1b-159">Use the following command to display the contents of a configuration:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-159">Use the following command to display the contents of a configuration:</span></span>

```cli
az iot hub configuration show --config-id [configuration id] \
  --hub-name [hub name]
```

* <span data-ttu-id="d8a1b-160">--**config-id** - The name of the configuration that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-160">--**config-id** - The name of the configuration that exists in the IoT hub.</span></span>

* <span data-ttu-id="d8a1b-161">--**hub-name** - Name of the IoT hub in which the configuration exists.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-161">--**hub-name** - Name of the IoT hub in which the configuration exists.</span></span> <span data-ttu-id="d8a1b-162">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-162">The hub must be in the current subscription.</span></span> <span data-ttu-id="d8a1b-163">Switch to the desired subscription with the command `az account set -s [subscription name]`</span><span class="sxs-lookup"><span data-stu-id="d8a1b-163">Switch to the desired subscription with the command `az account set -s [subscription name]`</span></span>

<span data-ttu-id="d8a1b-164">Inspect the configuration in the command window.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-164">Inspect the configuration in the command window.</span></span> <span data-ttu-id="d8a1b-165">The **metrics** property lists a count for each metric that is evaluated by each hub:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-165">The **metrics** property lists a count for each metric that is evaluated by each hub:</span></span>

* <span data-ttu-id="d8a1b-166">**targetedCount** - A system metric that specifies the number of device twins in IoT Hub that match the targeting condition.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-166">**targetedCount** - A system metric that specifies the number of device twins in IoT Hub that match the targeting condition.</span></span>

* <span data-ttu-id="d8a1b-167">**appliedCount** - A system metric specifies the number of devices that have had the target content applied.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-167">**appliedCount** - A system metric specifies the number of devices that have had the target content applied.</span></span>

* <span data-ttu-id="d8a1b-168">**Your custom metric** - Any metrics you have defined will be considered user metrics.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-168">**Your custom metric** - Any metrics you have defined will be considered user metrics.</span></span>

<span data-ttu-id="d8a1b-169">You can show a list of device IDs or objects for each of the metrics by using the following command:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-169">You can show a list of device IDs or objects for each of the metrics by using the following command:</span></span>

```cli
az iot hub configuration show-metric --config-id [configuration id] \
   --metric-id [metric id] --hub-name [hub name] --metric-type [type] 
```

* <span data-ttu-id="d8a1b-170">--**config-id** - The name of the deployment that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-170">--**config-id** - The name of the deployment that exists in the IoT hub.</span></span>

* <span data-ttu-id="d8a1b-171">--**metric-id** - The name of the metric for which you want to see the list of device IDs, for example `appliedCount`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-171">--**metric-id** - The name of the metric for which you want to see the list of device IDs, for example `appliedCount`.</span></span>

* <span data-ttu-id="d8a1b-172">--**hub-name** - Name of the IoT hub in which the deployment exists.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-172">--**hub-name** - Name of the IoT hub in which the deployment exists.</span></span> <span data-ttu-id="d8a1b-173">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-173">The hub must be in the current subscription.</span></span> <span data-ttu-id="d8a1b-174">Switch to the desired subscription with the command `az account set -s [subscription name]`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-174">Switch to the desired subscription with the command `az account set -s [subscription name]`.</span></span>

* <span data-ttu-id="d8a1b-175">--**metric-type** - Metric type can be `system` or `user`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-175">--**metric-type** - Metric type can be `system` or `user`.</span></span>  <span data-ttu-id="d8a1b-176">System metrics are `targetedCount` and `appliedCount`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-176">System metrics are `targetedCount` and `appliedCount`.</span></span> <span data-ttu-id="d8a1b-177">All other metrics are user metrics.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-177">All other metrics are user metrics.</span></span>

## <a name="modify-a-configuration"></a><span data-ttu-id="d8a1b-178">Modify a configuration</span><span class="sxs-lookup"><span data-stu-id="d8a1b-178">Modify a configuration</span></span>

<span data-ttu-id="d8a1b-179">When you modify a configuration, the changes immediately replicate to all targeted devices.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-179">When you modify a configuration, the changes immediately replicate to all targeted devices.</span></span> 

<span data-ttu-id="d8a1b-180">If you update the target condition, the following updates occur:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-180">If you update the target condition, the following updates occur:</span></span>

* <span data-ttu-id="d8a1b-181">If a device twin didn't meet the old target condition, but meets the new target condition and this configuration is the highest priority for that device twin, then this configuration is applied to the device twin.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-181">If a device twin didn't meet the old target condition, but meets the new target condition and this configuration is the highest priority for that device twin, then this configuration is applied to the device twin.</span></span> 

* <span data-ttu-id="d8a1b-182">If a device twin no longer meets the target condition, the settings from the configuration will be removed and the device twin will be modified by the next highest priority configuration.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-182">If a device twin no longer meets the target condition, the settings from the configuration will be removed and the device twin will be modified by the next highest priority configuration.</span></span> 

* <span data-ttu-id="d8a1b-183">If a device twin currently running this configuration no longer meets the target condition and doesn't meet the target condition of any other configurations, then the settings from the configuration will be removed and no other changes will be made on the twin.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-183">If a device twin currently running this configuration no longer meets the target condition and doesn't meet the target condition of any other configurations, then the settings from the configuration will be removed and no other changes will be made on the twin.</span></span> 

<span data-ttu-id="d8a1b-184">Use the following command to update a configuration:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-184">Use the following command to update a configuration:</span></span>

```cli
az iot hub configuration update --config-id [configuration id] \
   --hub-name [hub name] --set [property1.property2='value']
```

* <span data-ttu-id="d8a1b-185">--**config-id** - The name of the configuration that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-185">--**config-id** - The name of the configuration that exists in the IoT hub.</span></span>

* <span data-ttu-id="d8a1b-186">--**hub-name** - Name of the IoT hub in which the configuration exists.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-186">--**hub-name** - Name of the IoT hub in which the configuration exists.</span></span> <span data-ttu-id="d8a1b-187">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-187">The hub must be in the current subscription.</span></span> <span data-ttu-id="d8a1b-188">Switch to the desired subscription with the command `az account set -s [subscription name]`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-188">Switch to the desired subscription with the command `az account set -s [subscription name]`.</span></span>

* <span data-ttu-id="d8a1b-189">--**set** - Update a property in the configuration.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-189">--**set** - Update a property in the configuration.</span></span> <span data-ttu-id="d8a1b-190">You can update the following properties:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-190">You can update the following properties:</span></span>

    * <span data-ttu-id="d8a1b-191">targetCondition - for example `targetCondition=tags.location.state='Oregon'`</span><span class="sxs-lookup"><span data-stu-id="d8a1b-191">targetCondition - for example `targetCondition=tags.location.state='Oregon'`</span></span>

    * <span data-ttu-id="d8a1b-192">labels</span><span class="sxs-lookup"><span data-stu-id="d8a1b-192">labels</span></span> 

    * <span data-ttu-id="d8a1b-193">priority</span><span class="sxs-lookup"><span data-stu-id="d8a1b-193">priority</span></span>

## <a name="delete-a-configuration"></a><span data-ttu-id="d8a1b-194">Delete a configuration</span><span class="sxs-lookup"><span data-stu-id="d8a1b-194">Delete a configuration</span></span>

<span data-ttu-id="d8a1b-195">When you delete a configuration, any device twins take on their next highest priority configuration.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-195">When you delete a configuration, any device twins take on their next highest priority configuration.</span></span> <span data-ttu-id="d8a1b-196">If device twins don't meet the target condition of any other configuration, then no other settings are applied.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-196">If device twins don't meet the target condition of any other configuration, then no other settings are applied.</span></span> 

<span data-ttu-id="d8a1b-197">Use the following command to delete a configuration:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-197">Use the following command to delete a configuration:</span></span>

```cli
az iot hub configuration delete --config-id [configuration id] \
   --hub-name [hub name] 
```
* <span data-ttu-id="d8a1b-198">--**config-id** - The name of the configuration that exists in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-198">--**config-id** - The name of the configuration that exists in the IoT hub.</span></span>

* <span data-ttu-id="d8a1b-199">--**hub-name** - Name of the IoT hub in which the configuration exists.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-199">--**hub-name** - Name of the IoT hub in which the configuration exists.</span></span> <span data-ttu-id="d8a1b-200">The hub must be in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-200">The hub must be in the current subscription.</span></span> <span data-ttu-id="d8a1b-201">Switch to the desired subscription with the command `az account set -s [subscription name]`.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-201">Switch to the desired subscription with the command `az account set -s [subscription name]`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8a1b-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8a1b-202">Next steps</span></span>

<span data-ttu-id="d8a1b-203">In this article, you learned how configure and monitor IoT devices at scale.</span><span class="sxs-lookup"><span data-stu-id="d8a1b-203">In this article, you learned how configure and monitor IoT devices at scale.</span></span> <span data-ttu-id="d8a1b-204">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-204">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* [<span data-ttu-id="d8a1b-205">Manage your IoT Hub device identities in bulk</span><span class="sxs-lookup"><span data-stu-id="d8a1b-205">Manage your IoT Hub device identities in bulk</span></span>](iot-hub-bulk-identity-mgmt.md)
* [<span data-ttu-id="d8a1b-206">IoT Hub metrics</span><span class="sxs-lookup"><span data-stu-id="d8a1b-206">IoT Hub metrics</span></span>](iot-hub-metrics.md)
* [<span data-ttu-id="d8a1b-207">Operations monitoring</span><span class="sxs-lookup"><span data-stu-id="d8a1b-207">Operations monitoring</span></span>](iot-hub-operations-monitoring.md)

<span data-ttu-id="d8a1b-208">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-208">To further explore the capabilities of IoT Hub, see:</span></span>

* [<span data-ttu-id="d8a1b-209">IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="d8a1b-209">IoT Hub developer guide</span></span>](iot-hub-devguide.md)
* [<span data-ttu-id="d8a1b-210">Deploying AI to edge devices with Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="d8a1b-210">Deploying AI to edge devices with Azure IoT Edge</span></span>](../iot-edge/tutorial-simulate-device-linux.md)

<span data-ttu-id="d8a1b-211">To explore using the IoT Hub Device Provisioning Service to enable zero-touch, just-in-time provisioning, see:</span><span class="sxs-lookup"><span data-stu-id="d8a1b-211">To explore using the IoT Hub Device Provisioning Service to enable zero-touch, just-in-time provisioning, see:</span></span> 

* [<span data-ttu-id="d8a1b-212">Azure IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="d8a1b-212">Azure IoT Hub Device Provisioning Service</span></span>](/azure/iot-dps)
