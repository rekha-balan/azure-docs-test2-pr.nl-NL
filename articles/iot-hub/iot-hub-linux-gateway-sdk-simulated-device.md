---
title: Simulate a device with the Azure IoT Gateway SDK (Linux) | Microsoft Docs
description: How to use the Azure IoT Gateway SDK on Linux to create a simulated device that sends telemetry through a gateway to an IoT hub.
services: iot-hub
documentationcenter: ''
author: chipalost
manager: timlt
editor: ''
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/08/2017
ms.author: andbuc
ms.openlocfilehash: f6e3d0bfd45cb5cd133d77bcb23113c3f419450c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550003"
---
# <a name="use-the-azure-iot-gateway-sdk-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="f568d-103">Use the Azure IoT Gateway SDK to send device-to-cloud messages with a simulated device (Linux)</span><span class="sxs-lookup"><span data-stu-id="f568d-103">Use the Azure IoT Gateway SDK to send device-to-cloud messages with a simulated device (Linux)</span></span>
[!INCLUDE [iot-hub-gateway-sdk-simulated-selector](../../includes/iot-hub-gateway-sdk-simulated-selector.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="f568d-104">Build and run the sample</span><span class="sxs-lookup"><span data-stu-id="f568d-104">Build and run the sample</span></span>
<span data-ttu-id="f568d-105">Before you get started, you must:</span><span class="sxs-lookup"><span data-stu-id="f568d-105">Before you get started, you must:</span></span>

* <span data-ttu-id="f568d-106">[Set up your development environment][lnk-setupdevbox] for working with the SDK on Linux.</span><span class="sxs-lookup"><span data-stu-id="f568d-106">[Set up your development environment][lnk-setupdevbox] for working with the SDK on Linux.</span></span>
* <span data-ttu-id="f568d-107">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you will need the name of your hub to complete this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="f568d-107">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you will need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="f568d-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="f568d-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="f568d-109">Add two devices to your IoT hub and make a note of their ids and device keys.</span><span class="sxs-lookup"><span data-stu-id="f568d-109">Add two devices to your IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="f568d-110">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span><span class="sxs-lookup"><span data-stu-id="f568d-110">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span></span>

<span data-ttu-id="f568d-111">To build the sample:</span><span class="sxs-lookup"><span data-stu-id="f568d-111">To build the sample:</span></span>

1. <span data-ttu-id="f568d-112">Open a shell.</span><span class="sxs-lookup"><span data-stu-id="f568d-112">Open a shell.</span></span>
2. <span data-ttu-id="f568d-113">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="f568d-113">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
3. <span data-ttu-id="f568d-114">Run the **tools/build.sh** script.</span><span class="sxs-lookup"><span data-stu-id="f568d-114">Run the **tools/build.sh** script.</span></span> <span data-ttu-id="f568d-115">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **azure-iot-gateway-sdk** repository and generate a makefile.</span><span class="sxs-lookup"><span data-stu-id="f568d-115">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **azure-iot-gateway-sdk** repository and generate a makefile.</span></span> <span data-ttu-id="f568d-116">The script then builds the solution, skipping unit tests and end to end tests.</span><span class="sxs-lookup"><span data-stu-id="f568d-116">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="f568d-117">Add the **--run-unittests** parameter if you want to build and run the unit tests.</span><span class="sxs-lookup"><span data-stu-id="f568d-117">Add the **--run-unittests** parameter if you want to build and run the unit tests.</span></span> <span data-ttu-id="f568d-118">Add the **--run-e2e-tests** if you want to build and run the end to end tests.</span><span class="sxs-lookup"><span data-stu-id="f568d-118">Add the **--run-e2e-tests** if you want to build and run the end to end tests.</span></span> 

> [!NOTE]
> <span data-ttu-id="f568d-119">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="f568d-119">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
> 
> 

<span data-ttu-id="f568d-120">To run the sample:</span><span class="sxs-lookup"><span data-stu-id="f568d-120">To run the sample:</span></span>

<span data-ttu-id="f568d-121">In a text editor, open the file **samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json** in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="f568d-121">In a text editor, open the file **samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json** in your local copy of the **azure-iot-gateway-sdk** repository.</span></span> <span data-ttu-id="f568d-122">This file configures the modules in the sample gateway:</span><span class="sxs-lookup"><span data-stu-id="f568d-122">This file configures the modules in the sample gateway:</span></span>

* <span data-ttu-id="f568d-123">The **IoTHub** module connects to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f568d-123">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="f568d-124">You must configure it to send data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f568d-124">You must configure it to send data to your IoT hub.</span></span> <span data-ttu-id="f568d-125">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="f568d-125">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="f568d-126">Set the **Transport** value to one of: "HTTP", "AMQP", or "MQTT".</span><span class="sxs-lookup"><span data-stu-id="f568d-126">Set the **Transport** value to one of: "HTTP", "AMQP", or "MQTT".</span></span> <span data-ttu-id="f568d-127">Note that currently, only "HTTP" will share one TCP connection for all device messages.</span><span class="sxs-lookup"><span data-stu-id="f568d-127">Note that currently, only "HTTP" will share one TCP connection for all device messages.</span></span> <span data-ttu-id="f568d-128">If you set the value to "AMQP", or "MQTT", the gateway will maintain a separate TCP connection to IoT Hub for each device.</span><span class="sxs-lookup"><span data-stu-id="f568d-128">If you set the value to "AMQP", or "MQTT", the gateway will maintain a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="f568d-129">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span><span class="sxs-lookup"><span data-stu-id="f568d-129">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="f568d-130">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span><span class="sxs-lookup"><span data-stu-id="f568d-130">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="f568d-131">The **BLE1** and **BLE2** modules are the simulated devices.</span><span class="sxs-lookup"><span data-stu-id="f568d-131">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="f568d-132">Note how their MAC addresses match those in the **mapping** module.</span><span class="sxs-lookup"><span data-stu-id="f568d-132">Note how their MAC addresses match those in the **mapping** module.</span></span>
* <span data-ttu-id="f568d-133">The **Logger** module logs your gateway activity to a file.</span><span class="sxs-lookup"><span data-stu-id="f568d-133">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="f568d-134">The **module path** values shown below assume that you will run the sample from the root of your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="f568d-134">The **module path** values shown below assume that you will run the sample from the root of your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
* <span data-ttu-id="f568d-135">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span><span class="sxs-lookup"><span data-stu-id="f568d-135">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="f568d-136">It also ensures that all messages are logged by the **Logger** module.</span><span class="sxs-lookup"><span data-stu-id="f568d-136">It also ensures that all messages are logged by the **Logger** module.</span></span>

```
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
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
              "module.path": "./modules/identitymap/libidentity_map.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

<span data-ttu-id="f568d-137">Save any changes you made to the configuration file.</span><span class="sxs-lookup"><span data-stu-id="f568d-137">Save any changes you made to the configuration file.</span></span>

<span data-ttu-id="f568d-138">To run the sample:</span><span class="sxs-lookup"><span data-stu-id="f568d-138">To run the sample:</span></span>

1. <span data-ttu-id="f568d-139">In your shell, navigate to the **azure-iot-gateway-sdk/build** folder.</span><span class="sxs-lookup"><span data-stu-id="f568d-139">In your shell, navigate to the **azure-iot-gateway-sdk/build** folder.</span></span>
2. <span data-ttu-id="f568d-140">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="f568d-140">Run the following command:</span></span>
   
    ```
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ./../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="f568d-141">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span><span class="sxs-lookup"><span data-stu-id="f568d-141">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f568d-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="f568d-142">Next steps</span></span>
<span data-ttu-id="f568d-143">If you want to gain a more advanced understanding of the IoT Gateway SDK and experiment with some code examples, visit the following developer tutorials and resources:</span><span class="sxs-lookup"><span data-stu-id="f568d-143">If you want to gain a more advanced understanding of the IoT Gateway SDK and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="f568d-144">[Send device-to-cloud messages from a physical device with the IoT Gateway SDK][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="f568d-144">[Send device-to-cloud messages from a physical device with the IoT Gateway SDK][lnk-physical-device]</span></span>
* <span data-ttu-id="f568d-145">[Azure IoT Gateway SDK][lnk-gateway-sdk]</span><span class="sxs-lookup"><span data-stu-id="f568d-145">[Azure IoT Gateway SDK][lnk-gateway-sdk]</span></span>

<span data-ttu-id="f568d-146">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="f568d-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f568d-147">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="f568d-147">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="f568d-148">[Secure your IoT solution from the ground up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="f568d-148">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-setupdevbox]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/doc/devbox_setup.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk/

[lnk-physical-device]: iot-hub-gateway-sdk-physical-device.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-create-hub]: iot-hub-create-through-portal.md
