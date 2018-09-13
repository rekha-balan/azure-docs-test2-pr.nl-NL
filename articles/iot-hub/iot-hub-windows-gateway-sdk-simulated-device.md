---
title: Simulate a device with the Azure IoT Gateway SDK (Windows) | Microsoft Docs
description: How to use the Azure IoT Gateway SDK on Windows to create a simulated device that sends telemetry through a gateway to an IoT hub.
services: iot-hub
documentationcenter: ''
author: chipalost
manager: timlt
editor: ''
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: andbuc
ms.openlocfilehash: 458984f75eed3a7a3102c288798b55664afaa37d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552402"
---
# <a name="use-the-azure-iot-gateway-sdk-to-send-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="4b987-103">Use the Azure IoT Gateway SDK to send device-to-cloud messages with a simulated device (Windows)</span><span class="sxs-lookup"><span data-stu-id="4b987-103">Use the Azure IoT Gateway SDK to send device-to-cloud messages with a simulated device (Windows)</span></span>
[!INCLUDE [iot-hub-gateway-sdk-simulated-selector](../../includes/iot-hub-gateway-sdk-simulated-selector.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="4b987-104">Build and run the sample</span><span class="sxs-lookup"><span data-stu-id="4b987-104">Build and run the sample</span></span>
<span data-ttu-id="4b987-105">Before you get started, you must:</span><span class="sxs-lookup"><span data-stu-id="4b987-105">Before you get started, you must:</span></span>

* <span data-ttu-id="4b987-106">[Set up your development environment][lnk-setupdevbox] for working with the SDK on Windows.</span><span class="sxs-lookup"><span data-stu-id="4b987-106">[Set up your development environment][lnk-setupdevbox] for working with the SDK on Windows.</span></span>
* <span data-ttu-id="4b987-107">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="4b987-107">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="4b987-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="4b987-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="4b987-109">Add two devices to your IoT hub and make a note of their ids and device keys.</span><span class="sxs-lookup"><span data-stu-id="4b987-109">Add two devices to your IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="4b987-110">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span><span class="sxs-lookup"><span data-stu-id="4b987-110">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span></span>

<span data-ttu-id="4b987-111">To build the sample:</span><span class="sxs-lookup"><span data-stu-id="4b987-111">To build the sample:</span></span>

1. <span data-ttu-id="4b987-112">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span><span class="sxs-lookup"><span data-stu-id="4b987-112">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>
2. <span data-ttu-id="4b987-113">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="4b987-113">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
3. <span data-ttu-id="4b987-114">Run the **tools\\build.cmd** script.</span><span class="sxs-lookup"><span data-stu-id="4b987-114">Run the **tools\\build.cmd** script.</span></span> <span data-ttu-id="4b987-115">This script creates a Visual Studio solution file and builds the solution.</span><span class="sxs-lookup"><span data-stu-id="4b987-115">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="4b987-116">You can find the Visual Studio solution in the **build** folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="4b987-116">You can find the Visual Studio solution in the **build** folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span> <span data-ttu-id="4b987-117">Additional parameters can be given to the script to build and run unit and end to end tests.</span><span class="sxs-lookup"><span data-stu-id="4b987-117">Additional parameters can be given to the script to build and run unit and end to end tests.</span></span> <span data-ttu-id="4b987-118">These parameters are **--run-unittests** and **--run-e2e-tests** respectively.</span><span class="sxs-lookup"><span data-stu-id="4b987-118">These parameters are **--run-unittests** and **--run-e2e-tests** respectively.</span></span>

<span data-ttu-id="4b987-119">To run the sample:</span><span class="sxs-lookup"><span data-stu-id="4b987-119">To run the sample:</span></span>

<span data-ttu-id="4b987-120">In a text editor, open the file **samples\\simulated_device_cloud_upload\\src\\simulated_device_cloud_upload_win.json** in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="4b987-120">In a text editor, open the file **samples\\simulated_device_cloud_upload\\src\\simulated_device_cloud_upload_win.json** in your local copy of the **azure-iot-gateway-sdk** repository.</span></span> <span data-ttu-id="4b987-121">This file configures the modules in the sample gateway:</span><span class="sxs-lookup"><span data-stu-id="4b987-121">This file configures the modules in the sample gateway:</span></span>

* <span data-ttu-id="4b987-122">The **IoTHub** module connects to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4b987-122">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="4b987-123">You configure it to send data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4b987-123">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="4b987-124">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="4b987-124">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="4b987-125">Set the **Transport** value to one of: "HTTP", "AMQP", or "MQTT."</span><span class="sxs-lookup"><span data-stu-id="4b987-125">Set the **Transport** value to one of: "HTTP", "AMQP", or "MQTT."</span></span> <span data-ttu-id="4b987-126">Currently, only "HTTP" shares one TCP connection for all device messages.</span><span class="sxs-lookup"><span data-stu-id="4b987-126">Currently, only "HTTP" shares one TCP connection for all device messages.</span></span> <span data-ttu-id="4b987-127">If you set the value to "AMQP", or "MQTT", the gateway maintains a separate TCP connection to IoT Hub for each device.</span><span class="sxs-lookup"><span data-stu-id="4b987-127">If you set the value to "AMQP", or "MQTT", the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="4b987-128">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span><span class="sxs-lookup"><span data-stu-id="4b987-128">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="4b987-129">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span><span class="sxs-lookup"><span data-stu-id="4b987-129">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="4b987-130">The **BLE1** and **BLE2** modules are the simulated devices.</span><span class="sxs-lookup"><span data-stu-id="4b987-130">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="4b987-131">Note how the module MAC addresses match the addresses in the **mapping** module.</span><span class="sxs-lookup"><span data-stu-id="4b987-131">Note how the module MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="4b987-132">The **Logger** module logs your gateway activity to a file.</span><span class="sxs-lookup"><span data-stu-id="4b987-132">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="4b987-133">The **module path** values shown in the following example assume that you cloned the IoT Gateway SDK repository to the root of your **C:** drive.</span><span class="sxs-lookup"><span data-stu-id="4b987-133">The **module path** values shown in the following example assume that you cloned the IoT Gateway SDK repository to the root of your **C:** drive.</span></span> <span data-ttu-id="4b987-134">If you downloaded it to another location, you need to adjust the **module path** values accordingly.</span><span class="sxs-lookup"><span data-stu-id="4b987-134">If you downloaded it to another location, you need to adjust the **module path** values accordingly.</span></span>
* <span data-ttu-id="4b987-135">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span><span class="sxs-lookup"><span data-stu-id="4b987-135">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="4b987-136">It also ensures that all messages are logged by the **Logger** module.</span><span class="sxs-lookup"><span data-stu-id="4b987-136">It also ensures that all messages are logged by the **Logger** module.</span></span>

```
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

<span data-ttu-id="4b987-137">Save any changes you made to the configuration file.</span><span class="sxs-lookup"><span data-stu-id="4b987-137">Save any changes you made to the configuration file.</span></span>

<span data-ttu-id="4b987-138">To run the sample:</span><span class="sxs-lookup"><span data-stu-id="4b987-138">To run the sample:</span></span>

1. <span data-ttu-id="4b987-139">At a command prompt, navigate to the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="4b987-139">At a command prompt, navigate to the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
2. <span data-ttu-id="4b987-140">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="4b987-140">Run the following command:</span></span>
   
    ```
    build\samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="4b987-141">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span><span class="sxs-lookup"><span data-stu-id="4b987-141">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b987-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b987-142">Next steps</span></span>
<span data-ttu-id="4b987-143">If you want to gain a more advanced understanding of the IoT Gateway SDK and experiment with some code examples, visit the following developer tutorials and resources:</span><span class="sxs-lookup"><span data-stu-id="4b987-143">If you want to gain a more advanced understanding of the IoT Gateway SDK and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="4b987-144">[Send device-to-cloud messages from a physical device with the IoT Gateway SDK][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="4b987-144">[Send device-to-cloud messages from a physical device with the IoT Gateway SDK][lnk-physical-device]</span></span>
* <span data-ttu-id="4b987-145">[Azure IoT Gateway SDK][lnk-gateway-sdk]</span><span class="sxs-lookup"><span data-stu-id="4b987-145">[Azure IoT Gateway SDK][lnk-gateway-sdk]</span></span>

<span data-ttu-id="4b987-146">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="4b987-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4b987-147">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="4b987-147">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="4b987-148">[Secure your IoT solution from the ground up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="4b987-148">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-setupdevbox]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/doc/devbox_setup.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk/

[lnk-physical-device]: iot-hub-gateway-sdk-physical-device.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md
