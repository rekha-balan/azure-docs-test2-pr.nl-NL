---
title: Provision Raspberry Pi to Remote Monitoring in Node.js - Azure | Microsoft Docs
description: Describes how to connect a Raspberry Pi device to the Remote Monitoring solution accelerator using an application written in Node.js.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 01/24/2018
ms.author: dobett
ms.openlocfilehash: 696bd6ec80f39e8a9f3418426a754ffc038171e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870515"
---
# <a name="connect-your-raspberry-pi-device-to-the-remote-monitoring-solution-accelerator-nodejs"></a><span data-ttu-id="6a09c-103">Connect your Raspberry Pi device to the Remote Monitoring solution accelerator (Node.js)</span><span class="sxs-lookup"><span data-stu-id="6a09c-103">Connect your Raspberry Pi device to the Remote Monitoring solution accelerator (Node.js)</span></span>

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

<span data-ttu-id="6a09c-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="6a09c-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="6a09c-105">In this tutorial, you use Node.js, which is a good option for environments with minimal resource constraints.</span><span class="sxs-lookup"><span data-stu-id="6a09c-105">In this tutorial, you use Node.js, which is a good option for environments with minimal resource constraints.</span></span>

### <a name="required-hardware"></a><span data-ttu-id="6a09c-106">Required hardware</span><span class="sxs-lookup"><span data-stu-id="6a09c-106">Required hardware</span></span>

<span data-ttu-id="6a09c-107">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6a09c-107">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="6a09c-108">[Microsoft IoT Starter Kit for Raspberry Pi 3](https://azure.microsoft.com/develop/iot/starter-kits/) or equivalent components.</span><span class="sxs-lookup"><span data-stu-id="6a09c-108">[Microsoft IoT Starter Kit for Raspberry Pi 3](https://azure.microsoft.com/develop/iot/starter-kits/) or equivalent components.</span></span> <span data-ttu-id="6a09c-109">This tutorial uses the following items from the kit:</span><span class="sxs-lookup"><span data-stu-id="6a09c-109">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="6a09c-110">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="6a09c-110">Raspberry Pi 3</span></span>
- <span data-ttu-id="6a09c-111">MicroSD Card (with NOOBS)</span><span class="sxs-lookup"><span data-stu-id="6a09c-111">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="6a09c-112">A USB Mini cable</span><span class="sxs-lookup"><span data-stu-id="6a09c-112">A USB Mini cable</span></span>
- <span data-ttu-id="6a09c-113">An Ethernet cable</span><span class="sxs-lookup"><span data-stu-id="6a09c-113">An Ethernet cable</span></span>

### <a name="required-desktop-software"></a><span data-ttu-id="6a09c-114">Required desktop software</span><span class="sxs-lookup"><span data-stu-id="6a09c-114">Required desktop software</span></span>

<span data-ttu-id="6a09c-115">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6a09c-115">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="6a09c-116">Windows does not include an SSH client.</span><span class="sxs-lookup"><span data-stu-id="6a09c-116">Windows does not include an SSH client.</span></span> <span data-ttu-id="6a09c-117">We recommend using [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="6a09c-117">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="6a09c-118">Most Linux distributions and Mac OS include the command-line SSH utility.</span><span class="sxs-lookup"><span data-stu-id="6a09c-118">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="6a09c-119">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="6a09c-119">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-raspberry-pi-software"></a><span data-ttu-id="6a09c-120">Required Raspberry Pi software</span><span class="sxs-lookup"><span data-stu-id="6a09c-120">Required Raspberry Pi software</span></span>

<span data-ttu-id="6a09c-121">If you haven't done so already, install Node.js version 4.0.0 or later on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6a09c-121">If you haven't done so already, install Node.js version 4.0.0 or later on your Raspberry Pi.</span></span> <span data-ttu-id="6a09c-122">The following steps show you how to install Node.js v6 on your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6a09c-122">The following steps show you how to install Node.js v6 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="6a09c-123">Connect to your Raspberry Pi using `ssh`.</span><span class="sxs-lookup"><span data-stu-id="6a09c-123">Connect to your Raspberry Pi using `ssh`.</span></span> <span data-ttu-id="6a09c-124">For more information, see [SSH (Secure Shell)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md) on the [Raspberry Pi website](https://www.raspberrypi.org/).</span><span class="sxs-lookup"><span data-stu-id="6a09c-124">For more information, see [SSH (Secure Shell)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md) on the [Raspberry Pi website](https://www.raspberrypi.org/).</span></span>

1. <span data-ttu-id="6a09c-125">Use the following command to update your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6a09c-125">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="6a09c-126">Use the following commands to remove any existing installation of Node.js from your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6a09c-126">Use the following commands to remove any existing installation of Node.js from your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get remove nodered -y
    sudo apt-get remove nodejs nodejs-legacy -y
    sudo apt-get remove npm  -y
    ```

1. <span data-ttu-id="6a09c-127">Use the following command to download and install Node.js v6 on your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6a09c-127">Use the following command to download and install Node.js v6 on your Raspberry Pi:</span></span>

    ```sh
    curl -sL https://deb.nodesource.com/setup_6.x | sudo bash -
    sudo apt-get install nodejs npm
    ```

1. <span data-ttu-id="6a09c-128">Use the following command to verify you have installed Node.js v6.11.4 successfully:</span><span class="sxs-lookup"><span data-stu-id="6a09c-128">Use the following command to verify you have installed Node.js v6.11.4 successfully:</span></span>

    ```sh
    node --version
    ```

## <a name="create-a-nodejs-solution"></a><span data-ttu-id="6a09c-129">Create a Node.js solution</span><span class="sxs-lookup"><span data-stu-id="6a09c-129">Create a Node.js solution</span></span>

<span data-ttu-id="6a09c-130">Complete the following steps using the `ssh` connection to your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6a09c-130">Complete the following steps using the `ssh` connection to your Raspberry Pi:</span></span>

1. <span data-ttu-id="6a09c-131">Create a folder called `remotemonitoring` in your home folder on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6a09c-131">Create a folder called `remotemonitoring` in your home folder on the Raspberry Pi.</span></span> <span data-ttu-id="6a09c-132">Navigate to this folder in your command line:</span><span class="sxs-lookup"><span data-stu-id="6a09c-132">Navigate to this folder in your command line:</span></span>

    ```sh
    cd ~
    mkdir remotemonitoring
    cd remotemonitoring
    ```

1. <span data-ttu-id="6a09c-133">To download and install the packages you need to complete the sample app, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="6a09c-133">To download and install the packages you need to complete the sample app, run the following commands:</span></span>

    ```sh
    npm install async azure-iot-device azure-iot-device-mqtt
    ```

1. <span data-ttu-id="6a09c-134">In the `remotemonitoring` folder, create a file called **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="6a09c-134">In the `remotemonitoring` folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="6a09c-135">Open this file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="6a09c-135">Open this file in a text editor.</span></span> <span data-ttu-id="6a09c-136">On the Raspberry Pi, you can use the `nano` or `vi` text editors.</span><span class="sxs-lookup"><span data-stu-id="6a09c-136">On the Raspberry Pi, you can use the `nano` or `vi` text editors.</span></span>

1. <span data-ttu-id="6a09c-137">In the **remote_monitoring.js** file, add the following `require` statements:</span><span class="sxs-lookup"><span data-stu-id="6a09c-137">In the **remote_monitoring.js** file, add the following `require` statements:</span></span>

    ```nodejs
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    var async = require('async');
    ```

1. <span data-ttu-id="6a09c-138">Add the following variable declarations after the `require` statements.</span><span class="sxs-lookup"><span data-stu-id="6a09c-138">Add the following variable declarations after the `require` statements.</span></span> <span data-ttu-id="6a09c-139">Replace the placeholder value `{device connection string}` with value you noted for the device you provisioned in the Remote Monitoring solution:</span><span class="sxs-lookup"><span data-stu-id="6a09c-139">Replace the placeholder value `{device connection string}` with value you noted for the device you provisioned in the Remote Monitoring solution:</span></span>

    ```nodejs
    var connectionString = '{device connection string}';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="6a09c-140">To define some base telemetry data, add the following variables:</span><span class="sxs-lookup"><span data-stu-id="6a09c-140">To define some base telemetry data, add the following variables:</span></span>

    ```nodejs
    var temperature = 50;
    var temperatureUnit = 'F';
    var humidity = 50;
    var humidityUnit = '%';
    var pressure = 55;
    var pressureUnit = 'psig';
    ```

1. <span data-ttu-id="6a09c-141">To define some property values, add the following variables:</span><span class="sxs-lookup"><span data-stu-id="6a09c-141">To define some property values, add the following variables:</span></span>

    ```nodejs
    var temperatureSchema = 'chiller-temperature;v1';
    var humiditySchema = 'chiller-humidity;v1';
    var pressureSchema = 'chiller-pressure;v1';
    var interval = "00:00:05";
    var deviceType = "Chiller";
    var deviceFirmware = "1.0.0";
    var deviceFirmwareUpdateStatus = "";
    var deviceLocation = "Building 44";
    var deviceLatitude = 47.638928;
    var deviceLongitude = -122.13476;
    var deviceOnline = true;
    ```

1. <span data-ttu-id="6a09c-142">Add the following variable to define the reported properties to send to the solution.</span><span class="sxs-lookup"><span data-stu-id="6a09c-142">Add the following variable to define the reported properties to send to the solution.</span></span> <span data-ttu-id="6a09c-143">These properties include metadata to describe the methods and telemetry the device uses:</span><span class="sxs-lookup"><span data-stu-id="6a09c-143">These properties include metadata to describe the methods and telemetry the device uses:</span></span>

    ```nodejs
    var reportedProperties = {
      "Protocol": "MQTT",
      "SupportedMethods": "Reboot,FirmwareUpdate,EmergencyValveRelease,IncreasePressure",
      "Telemetry": {
        "TemperatureSchema": {
          "Interval": interval,
          "MessageTemplate": "{\"temperature\":${temperature},\"temperature_unit\":\"${temperature_unit}\"}",
          "MessageSchema": {
            "Name": temperatureSchema,
            "Format": "JSON",
            "Fields": {
              "temperature": "Double",
              "temperature_unit": "Text"
            }
          }
        },
        "HumiditySchema": {
          "Interval": interval,
          "MessageTemplate": "{\"humidity\":${humidity},\"humidity_unit\":\"${humidity_unit}\"}",
          "MessageSchema": {
            "Name": humiditySchema,
            "Format": "JSON",
            "Fields": {
              "humidity": "Double",
              "humidity_unit": "Text"
            }
          }
        },
        "PressureSchema": {
          "Interval": interval,
          "MessageTemplate": "{\"pressure\":${pressure},\"pressure_unit\":\"${pressure_unit}\"}",
          "MessageSchema": {
            "Name": pressureSchema,
            "Format": "JSON",
            "Fields": {
              "pressure": "Double",
              "pressure_unit": "Text"
            }
          }
        }
      },
      "Type": deviceType,
      "Firmware": deviceFirmware,
      "FirmwareUpdateStatus": deviceFirmwareUpdateStatus,
      "Location": deviceLocation,
      "Latitude": deviceLatitude,
      "Longitude": deviceLongitude,
      "Online": deviceOnline
    }
    ```

1. <span data-ttu-id="6a09c-144">To print operation results, add the following helper function:</span><span class="sxs-lookup"><span data-stu-id="6a09c-144">To print operation results, add the following helper function:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="6a09c-145">Add the following helper function to use to randomize the telemetry values:</span><span class="sxs-lookup"><span data-stu-id="6a09c-145">Add the following helper function to use to randomize the telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="6a09c-146">Add the following generic function to handle direct method calls from the solution.</span><span class="sxs-lookup"><span data-stu-id="6a09c-146">Add the following generic function to handle direct method calls from the solution.</span></span> <span data-ttu-id="6a09c-147">The function displays information about the direct method that was invoked, but in this sample does not modify the device in any way.</span><span class="sxs-lookup"><span data-stu-id="6a09c-147">The function displays information about the direct method that was invoked, but in this sample does not modify the device in any way.</span></span> <span data-ttu-id="6a09c-148">The solution uses direct methods to act on devices:</span><span class="sxs-lookup"><span data-stu-id="6a09c-148">The solution uses direct methods to act on devices:</span></span>

    ```nodejs
    function onDirectMethod(request, response) {
      // Implement logic asynchronously here.
      console.log('Simulated ' + request.methodName);

      // Complete the response
      response.send(200, request.methodName + ' was called on the device', function (err) {
        if (err) console.error('Error sending method response :\n' + err.toString());
        else console.log('200 Response to method \'' + request.methodName + '\' sent successfully.');
      });
    }
    ```

1. <span data-ttu-id="6a09c-149">Add the following function to handle the **FirmwareUpdate** direct method calls from the solution.</span><span class="sxs-lookup"><span data-stu-id="6a09c-149">Add the following function to handle the **FirmwareUpdate** direct method calls from the solution.</span></span> <span data-ttu-id="6a09c-150">The function verifies the parameters passed in the direct method payload and then asynchronously runs a firmware update simulation:</span><span class="sxs-lookup"><span data-stu-id="6a09c-150">The function verifies the parameters passed in the direct method payload and then asynchronously runs a firmware update simulation:</span></span>

    ```node.js
    function onFirmwareUpdate(request, response) {
      // Get the requested firmware version from the JSON request body
      var firmwareVersion = request.payload.Firmware;
      var firmwareUri = request.payload.FirmwareUri;
      
      // Ensure we got a firmware values
      if (!firmwareVersion || !firmwareUri) {
        response.send(400, 'Missing firmware value', function(err) {
          if (err) console.error('Error sending method response :\n' + err.toString());
          else console.log('400 Response to method \'' + request.methodName + '\' sent successfully.');
        });
      } else {
        // Respond the cloud app for the device method
        response.send(200, 'Firmware update started.', function(err) {
          if (err) console.error('Error sending method response :\n' + err.toString());
          else {
            console.log('200 Response to method \'' + request.methodName + '\' sent successfully.');

            // Run the simulated firmware update flow
            runFirmwareUpdateFlow(firmwareVersion, firmwareUri);
          }
        });
      }
    }
    ```

1. <span data-ttu-id="6a09c-151">Add the following function to simulate a long-running firmware update flow that reports progress back to the solution:</span><span class="sxs-lookup"><span data-stu-id="6a09c-151">Add the following function to simulate a long-running firmware update flow that reports progress back to the solution:</span></span>

    ```node.js
    // Simulated firmwareUpdate flow
    function runFirmwareUpdateFlow(firmwareVersion, firmwareUri) {
      console.log('Simulating firmware update flow...');
      console.log('> Firmware version passed: ' + firmwareVersion);
      console.log('> Firmware URI passed: ' + firmwareUri);
      async.waterfall([
        function (callback) {
          console.log("Image downloading from " + firmwareUri);
          var patch = {
            FirmwareUpdateStatus: 'Downloading image..'
          };
          reportUpdateThroughTwin(patch, callback);
          sleep(10000, callback);
        },
        function (callback) {
          console.log("Downloaded, applying firmware " + firmwareVersion);
          deviceOnline = false;
          var patch = {
            FirmwareUpdateStatus: 'Applying firmware..',
            Online: false
          };
          reportUpdateThroughTwin(patch, callback);
          sleep(8000, callback);
        },
        function (callback) {
          console.log("Rebooting");
          var patch = {
            FirmwareUpdateStatus: 'Rebooting..'
          };
          reportUpdateThroughTwin(patch, callback);
          sleep(10000, callback);
        },
        function (callback) {
          console.log("Firmware updated to " + firmwareVersion);
          deviceOnline = true;
          var patch = {
            FirmwareUpdateStatus: 'Firmware updated',
            Online: true,
            Firmware: firmwareVersion
          };
          reportUpdateThroughTwin(patch, callback);
          callback(null);
        }
      ], function(err) {
        if (err) {
          console.error('Error in simulated firmware update flow: ' + err.message);
        } else {
          console.log("Completed simulated firmware update flow");
        }
      });

      // Helper function to update the twin reported properties.
      function reportUpdateThroughTwin(patch, callback) {
        console.log("Sending...");
        console.log(JSON.stringify(patch, null, 2));
        client.getTwin(function(err, twin) {
          if (!err) {
            twin.properties.reported.update(patch, function(err) {
              if (err) callback(err);
            });      
          } else {
            if (err) callback(err);
          }
        });
      }

      function sleep(milliseconds, callback) {
        console.log("Simulate a delay (milleseconds): " + milliseconds);
        setTimeout(function () {
          callback(null);
        }, milliseconds);
      }
    }
    ```

1. <span data-ttu-id="6a09c-152">Add the following code to send telemetry data to the solution.</span><span class="sxs-lookup"><span data-stu-id="6a09c-152">Add the following code to send telemetry data to the solution.</span></span> <span data-ttu-id="6a09c-153">The client app adds properties to the message to identify the message schema:</span><span class="sxs-lookup"><span data-stu-id="6a09c-153">The client app adds properties to the message to identify the message schema:</span></span>

    ```node.js
    function sendTelemetry(data, schema) {
      if (deviceOnline) {
        var d = new Date();
        var payload = JSON.stringify(data);
        var message = new Message(payload);
        message.properties.add('$$CreationTimeUtc', d.toISOString());
        message.properties.add('$$MessageSchema', schema);
        message.properties.add('$$ContentType', 'JSON');

        console.log('Sending device message data:\n' + payload);
        client.sendEvent(message, printErrorFor('send event'));
      } else {
        console.log('Offline, not sending telemetry');
      }
    }
    ```

1. <span data-ttu-id="6a09c-154">Add the following code to create a client instance:</span><span class="sxs-lookup"><span data-stu-id="6a09c-154">Add the following code to create a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="6a09c-155">Add the following code to:</span><span class="sxs-lookup"><span data-stu-id="6a09c-155">Add the following code to:</span></span>

    * <span data-ttu-id="6a09c-156">Open the connection.</span><span class="sxs-lookup"><span data-stu-id="6a09c-156">Open the connection.</span></span>
    * <span data-ttu-id="6a09c-157">Set up a handler for desired properties.</span><span class="sxs-lookup"><span data-stu-id="6a09c-157">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="6a09c-158">Send reported properties.</span><span class="sxs-lookup"><span data-stu-id="6a09c-158">Send reported properties.</span></span>
    * <span data-ttu-id="6a09c-159">Register handlers for the direct methods.</span><span class="sxs-lookup"><span data-stu-id="6a09c-159">Register handlers for the direct methods.</span></span> <span data-ttu-id="6a09c-160">The sample uses a separate handler for the firmware update direct method.</span><span class="sxs-lookup"><span data-stu-id="6a09c-160">The sample uses a separate handler for the firmware update direct method.</span></span>
    * <span data-ttu-id="6a09c-161">Start sending telemetry.</span><span class="sxs-lookup"><span data-stu-id="6a09c-161">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
      if (err) {
        printErrorFor('open')(err);
      } else {
        // Create device Twin
        client.getTwin(function (err, twin) {
          if (err) {
            console.error('Could not get device twin');
          } else {
            console.log('Device twin created');

            twin.on('properties.desired', function (delta) {
              // Handle desired properties set by solution
              console.log('Received new desired properties:');
              console.log(JSON.stringify(delta));
            });

            // Send reported properties
            twin.properties.reported.update(reportedProperties, function (err) {
              if (err) throw err;
              console.log('Twin state reported');
            });

            // Register handlers for all the method names we are interested in.
            // Consider separate handlers for each method.
            client.onDeviceMethod('Reboot', onDirectMethod);
            client.onDeviceMethod('FirmwareUpdate', onFirmwareUpdate);
            client.onDeviceMethod('EmergencyValveRelease', onDirectMethod);
            client.onDeviceMethod('IncreasePressure', onDirectMethod);
          }
        });

        // Start sending telemetry
        var sendTemperatureInterval = setInterval(function () {
          temperature += generateRandomIncrement();
          var data = {
            'temperature': temperature,
            'temperature_unit': temperatureUnit
          };
          sendTelemetry(data, temperatureSchema)
        }, 5000);

        var sendHumidityInterval = setInterval(function () {
          humidity += generateRandomIncrement();
          var data = {
            'humidity': humidity,
            'humidity_unit': humidityUnit
          };
          sendTelemetry(data, humiditySchema)
        }, 5000);

        var sendPressureInterval = setInterval(function () {
          pressure += generateRandomIncrement();
          var data = {
            'pressure': pressure,
            'pressure_unit': pressureUnit
          };
          sendTelemetry(data, pressureSchema)
        }, 5000);

        client.on('error', function (err) {
          printErrorFor('client')(err);
          if (sendTemperatureInterval) clearInterval(sendTemperatureInterval);
          if (sendHumidityInterval) clearInterval(sendHumidityInterval);
          if (sendPressureInterval) clearInterval(sendPressureInterval);
          client.close(printErrorFor('client.close'));
        });
      }
    });
    ```

1. <span data-ttu-id="6a09c-162">Save the changes to the **remote_monitoring.js** file.</span><span class="sxs-lookup"><span data-stu-id="6a09c-162">Save the changes to the **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="6a09c-163">To launch the sample application, run the following command at your command prompt on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="6a09c-163">To launch the sample application, run the following command at your command prompt on the Raspberry Pi:</span></span>

    ```sh
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]
