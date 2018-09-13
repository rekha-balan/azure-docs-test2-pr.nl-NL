---
title: Connect a device using Node.js | Microsoft Docs
description: Describes how to connect a device to the Azure IoT Suite preconfigured remote monitoring solution using an application written in Node.js.
services: ''
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/20/2017
ms.author: dobett
ms.openlocfilehash: 8f45d0e86a95779d5ceeddb72638b14e0e7a80eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555721"
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="67a17-103">Connect your device to the remote monitoring preconfigured solution (Node.js)</span><span class="sxs-lookup"><span data-stu-id="67a17-103">Connect your device to the remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="67a17-104">Create a node.js sample solution</span><span class="sxs-lookup"><span data-stu-id="67a17-104">Create a node.js sample solution</span></span>

<span data-ttu-id="67a17-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span><span class="sxs-lookup"><span data-stu-id="67a17-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="67a17-106">You can run `node --version` at the command line to check the version.</span><span class="sxs-lookup"><span data-stu-id="67a17-106">You can run `node --version` at the command line to check the version.</span></span>

1. <span data-ttu-id="67a17-107">Create a folder called **RemoteMonitoring** on your development machine.</span><span class="sxs-lookup"><span data-stu-id="67a17-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="67a17-108">Navigate to this folder in your command-line environment.</span><span class="sxs-lookup"><span data-stu-id="67a17-108">Navigate to this folder in your command-line environment.</span></span>

1. <span data-ttu-id="67a17-109">Run the following commands to download and install the packages you need to complete the sample app:</span><span class="sxs-lookup"><span data-stu-id="67a17-109">Run the following commands to download and install the packages you need to complete the sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="67a17-110">In the **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="67a17-110">In the **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="67a17-111">Open this file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="67a17-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="67a17-112">In the **remote_monitoring.js** file, add the following `require` statements:</span><span class="sxs-lookup"><span data-stu-id="67a17-112">In the **remote_monitoring.js** file, add the following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="67a17-113">Add the following variable declarations after the `require` statements.</span><span class="sxs-lookup"><span data-stu-id="67a17-113">Add the following variable declarations after the `require` statements.</span></span> <span data-ttu-id="67a17-114">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="67a17-114">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="67a17-115">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span><span class="sxs-lookup"><span data-stu-id="67a17-115">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="67a17-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span><span class="sxs-lookup"><span data-stu-id="67a17-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="67a17-117">Add the following variables to define some base telemetry data:</span><span class="sxs-lookup"><span data-stu-id="67a17-117">Add the following variables to define some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="67a17-118">Add the following helper function to print operation results:</span><span class="sxs-lookup"><span data-stu-id="67a17-118">Add the following helper function to print operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="67a17-119">Add the following helper function to use to randomize the telemetry values:</span><span class="sxs-lookup"><span data-stu-id="67a17-119">Add the following helper function to use to randomize the telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="67a17-120">Add the following definition for the **DeviceInfo** object the device sends on startup:</span><span class="sxs-lookup"><span data-stu-id="67a17-120">Add the following definition for the **DeviceInfo** object the device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="67a17-121">Add the following definition for the device twin reported values.</span><span class="sxs-lookup"><span data-stu-id="67a17-121">Add the following definition for the device twin reported values.</span></span> <span data-ttu-id="67a17-122">This definition includes descriptions of the direct methods the device supports:</span><span class="sxs-lookup"><span data-stu-id="67a17-122">This definition includes descriptions of the direct methods the device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot the device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file"
        },
    }
    ```

1. <span data-ttu-id="67a17-123">Add the following function to handle the **Reboot** direct method call:</span><span class="sxs-lookup"><span data-stu-id="67a17-123">Add the following function to handle the **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete the response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="67a17-124">Add the following function to handle the **InitiateFirmwareUpdate** direct method call.</span><span class="sxs-lookup"><span data-stu-id="67a17-124">Add the following function to handle the **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="67a17-125">This direct method uses a parameter to specify the location of the firmware image to download, and initiates the firmware update on the device asynchronously:</span><span class="sxs-lookup"><span data-stu-id="67a17-125">This direct method uses a parameter to specify the location of the firmware image to download, and initiates the firmware update on the device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete the response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here to perform the firmware update asynchronously
    }
    ```

1. <span data-ttu-id="67a17-126">Add the following code to create a client instance:</span><span class="sxs-lookup"><span data-stu-id="67a17-126">Add the following code to create a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="67a17-127">Add the following code to:</span><span class="sxs-lookup"><span data-stu-id="67a17-127">Add the following code to:</span></span>

    * <span data-ttu-id="67a17-128">Open the connection.</span><span class="sxs-lookup"><span data-stu-id="67a17-128">Open the connection.</span></span>
    * <span data-ttu-id="67a17-129">Send the **DeviceInfo** object.</span><span class="sxs-lookup"><span data-stu-id="67a17-129">Send the **DeviceInfo** object.</span></span>
    * <span data-ttu-id="67a17-130">Set up a handler for desired properties.</span><span class="sxs-lookup"><span data-stu-id="67a17-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="67a17-131">Send reported properties.</span><span class="sxs-lookup"><span data-stu-id="67a17-131">Send reported properties.</span></span>
    * <span data-ttu-id="67a17-132">Register handlers for the direct methods.</span><span class="sxs-lookup"><span data-stu-id="67a17-132">Register handlers for the direct methods.</span></span>
    * <span data-ttu-id="67a17-133">Start sending telemetry.</span><span class="sxs-lookup"><span data-stu-id="67a17-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="67a17-134">Save the changes to the **remote_monitoring.js** file.</span><span class="sxs-lookup"><span data-stu-id="67a17-134">Save the changes to the **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="67a17-135">Run the following command at a command prompt to launch the sample application:</span><span class="sxs-lookup"><span data-stu-id="67a17-135">Run the following command at a command prompt to launch the sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
