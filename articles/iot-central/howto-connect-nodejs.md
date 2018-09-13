---
title: Connect a generic Node.js client application to Azure IoT Central | Microsoft Docs
description: As an device developer, how to connect a generic Node.js device to your Azure IoT Central application.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 55ce85702804d99d806220d7f0a4ea0820975f4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968910"
---
# <a name="connect-a-generic-client-application-to-your-azure-iot-central-application-nodejs"></a><span data-ttu-id="77671-103">Connect a generic client application to your Azure IoT Central application (Node.js)</span><span class="sxs-lookup"><span data-stu-id="77671-103">Connect a generic client application to your Azure IoT Central application (Node.js)</span></span>

<span data-ttu-id="77671-104">This article describes how, as a device developer, to connect a generic Node.js application representing a physical device to your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="77671-104">This article describes how, as a device developer, to connect a generic Node.js application representing a physical device to your Microsoft Azure IoT Central application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="77671-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="77671-105">Before you begin</span></span>

<span data-ttu-id="77671-106">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="77671-106">To complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="77671-107">An Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="77671-107">An Azure IoT Central application.</span></span> <span data-ttu-id="77671-108">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="77671-108">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span></span>
1. <span data-ttu-id="77671-109">A development machine with [Node.js](https://nodejs.org/) version 4.0.0 or later installed.</span><span class="sxs-lookup"><span data-stu-id="77671-109">A development machine with [Node.js](https://nodejs.org/) version 4.0.0 or later installed.</span></span> <span data-ttu-id="77671-110">You can run `node --version` in the command line to check your version.</span><span class="sxs-lookup"><span data-stu-id="77671-110">You can run `node --version` in the command line to check your version.</span></span> <span data-ttu-id="77671-111">Node.js is available for a wide variety of operating systems.</span><span class="sxs-lookup"><span data-stu-id="77671-111">Node.js is available for a wide variety of operating systems.</span></span>

## <a name="create-a-device-template"></a><span data-ttu-id="77671-112">Create a Device Template</span><span class="sxs-lookup"><span data-stu-id="77671-112">Create a Device Template</span></span>

<span data-ttu-id="77671-113">In your Azure IoT Central application, you need a device template with the following measurements and device properties defined:</span><span class="sxs-lookup"><span data-stu-id="77671-113">In your Azure IoT Central application, you need a device template with the following measurements and device properties defined:</span></span>

### <a name="telemetry-measurements"></a><span data-ttu-id="77671-114">Telemetry measurements</span><span class="sxs-lookup"><span data-stu-id="77671-114">Telemetry measurements</span></span>

<span data-ttu-id="77671-115">Add the following telemetry in the **Measurements** page:</span><span class="sxs-lookup"><span data-stu-id="77671-115">Add the following telemetry in the **Measurements** page:</span></span>

| <span data-ttu-id="77671-116">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-116">Display Name</span></span> | <span data-ttu-id="77671-117">Field Name</span><span class="sxs-lookup"><span data-stu-id="77671-117">Field Name</span></span>  | <span data-ttu-id="77671-118">Units</span><span class="sxs-lookup"><span data-stu-id="77671-118">Units</span></span> | <span data-ttu-id="77671-119">Min</span><span class="sxs-lookup"><span data-stu-id="77671-119">Min</span></span> | <span data-ttu-id="77671-120">Max</span><span class="sxs-lookup"><span data-stu-id="77671-120">Max</span></span> | <span data-ttu-id="77671-121">Decimal Places</span><span class="sxs-lookup"><span data-stu-id="77671-121">Decimal Places</span></span> |
| ------------ | ----------- | ----- | --- | --- | -------------- |
| <span data-ttu-id="77671-122">Temperature</span><span class="sxs-lookup"><span data-stu-id="77671-122">Temperature</span></span>  | <span data-ttu-id="77671-123">temperature</span><span class="sxs-lookup"><span data-stu-id="77671-123">temperature</span></span> | <span data-ttu-id="77671-124">F</span><span class="sxs-lookup"><span data-stu-id="77671-124">F</span></span>     | <span data-ttu-id="77671-125">60</span><span class="sxs-lookup"><span data-stu-id="77671-125">60</span></span>  | <span data-ttu-id="77671-126">110</span><span class="sxs-lookup"><span data-stu-id="77671-126">110</span></span> | <span data-ttu-id="77671-127">0</span><span class="sxs-lookup"><span data-stu-id="77671-127">0</span></span>              |
| <span data-ttu-id="77671-128">Humidity</span><span class="sxs-lookup"><span data-stu-id="77671-128">Humidity</span></span>     | <span data-ttu-id="77671-129">humidity</span><span class="sxs-lookup"><span data-stu-id="77671-129">humidity</span></span>    | %     | <span data-ttu-id="77671-130">0</span><span class="sxs-lookup"><span data-stu-id="77671-130">0</span></span>   | <span data-ttu-id="77671-131">100</span><span class="sxs-lookup"><span data-stu-id="77671-131">100</span></span> | <span data-ttu-id="77671-132">0</span><span class="sxs-lookup"><span data-stu-id="77671-132">0</span></span>              |
| <span data-ttu-id="77671-133">Pressure</span><span class="sxs-lookup"><span data-stu-id="77671-133">Pressure</span></span>     | <span data-ttu-id="77671-134">pressure</span><span class="sxs-lookup"><span data-stu-id="77671-134">pressure</span></span>    | <span data-ttu-id="77671-135">kPa</span><span class="sxs-lookup"><span data-stu-id="77671-135">kPa</span></span>   | <span data-ttu-id="77671-136">80</span><span class="sxs-lookup"><span data-stu-id="77671-136">80</span></span>  | <span data-ttu-id="77671-137">110</span><span class="sxs-lookup"><span data-stu-id="77671-137">110</span></span> | <span data-ttu-id="77671-138">0</span><span class="sxs-lookup"><span data-stu-id="77671-138">0</span></span>              |

> [!NOTE]
  <span data-ttu-id="77671-139">The datatype of the telemetry measurement is double.</span><span class="sxs-lookup"><span data-stu-id="77671-139">The datatype of the telemetry measurement is double.</span></span>

<span data-ttu-id="77671-140">Enter field names exactly as shown in the table into the device template.</span><span class="sxs-lookup"><span data-stu-id="77671-140">Enter field names exactly as shown in the table into the device template.</span></span> <span data-ttu-id="77671-141">If the field names do not match, the telemetry cannot be displayed in the application.</span><span class="sxs-lookup"><span data-stu-id="77671-141">If the field names do not match, the telemetry cannot be displayed in the application.</span></span>

### <a name="state-measurements"></a><span data-ttu-id="77671-142">State measurements</span><span class="sxs-lookup"><span data-stu-id="77671-142">State measurements</span></span>

<span data-ttu-id="77671-143">Add the following state in the **Measurements** page:</span><span class="sxs-lookup"><span data-stu-id="77671-143">Add the following state in the **Measurements** page:</span></span>

| <span data-ttu-id="77671-144">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-144">Display Name</span></span> | <span data-ttu-id="77671-145">Field Name</span><span class="sxs-lookup"><span data-stu-id="77671-145">Field Name</span></span>  | <span data-ttu-id="77671-146">Value 1</span><span class="sxs-lookup"><span data-stu-id="77671-146">Value 1</span></span> | <span data-ttu-id="77671-147">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-147">Display Name</span></span> | <span data-ttu-id="77671-148">Value 2</span><span class="sxs-lookup"><span data-stu-id="77671-148">Value 2</span></span> | <span data-ttu-id="77671-149">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-149">Display Name</span></span> |
| ------------ | ----------- | --------| ------------ | ------- | ------------ | 
| <span data-ttu-id="77671-150">Fan Mode</span><span class="sxs-lookup"><span data-stu-id="77671-150">Fan Mode</span></span>     | <span data-ttu-id="77671-151">fanmode</span><span class="sxs-lookup"><span data-stu-id="77671-151">fanmode</span></span>     | <span data-ttu-id="77671-152">1</span><span class="sxs-lookup"><span data-stu-id="77671-152">1</span></span>       | <span data-ttu-id="77671-153">Running</span><span class="sxs-lookup"><span data-stu-id="77671-153">Running</span></span>      | <span data-ttu-id="77671-154">0</span><span class="sxs-lookup"><span data-stu-id="77671-154">0</span></span>       | <span data-ttu-id="77671-155">Stopped</span><span class="sxs-lookup"><span data-stu-id="77671-155">Stopped</span></span>      |

> [!NOTE]
  <span data-ttu-id="77671-156">The datatype of the State measurement is string.</span><span class="sxs-lookup"><span data-stu-id="77671-156">The datatype of the State measurement is string.</span></span>

<span data-ttu-id="77671-157">Enter field names exactly as shown in the table into the device template.</span><span class="sxs-lookup"><span data-stu-id="77671-157">Enter field names exactly as shown in the table into the device template.</span></span> <span data-ttu-id="77671-158">If the field names do not match, the state cannot be displayed in the application.</span><span class="sxs-lookup"><span data-stu-id="77671-158">If the field names do not match, the state cannot be displayed in the application.</span></span>

### <a name="event-measurements"></a><span data-ttu-id="77671-159">Event measurements</span><span class="sxs-lookup"><span data-stu-id="77671-159">Event measurements</span></span>

<span data-ttu-id="77671-160">Add the following event in the **Measurements** page:</span><span class="sxs-lookup"><span data-stu-id="77671-160">Add the following event in the **Measurements** page:</span></span>

| <span data-ttu-id="77671-161">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-161">Display Name</span></span> | <span data-ttu-id="77671-162">Field Name</span><span class="sxs-lookup"><span data-stu-id="77671-162">Field Name</span></span>  | <span data-ttu-id="77671-163">Severity</span><span class="sxs-lookup"><span data-stu-id="77671-163">Severity</span></span> |
| ------------ | ----------- | -------- |
| <span data-ttu-id="77671-164">Overheating</span><span class="sxs-lookup"><span data-stu-id="77671-164">Overheating</span></span>  | <span data-ttu-id="77671-165">overheat</span><span class="sxs-lookup"><span data-stu-id="77671-165">overheat</span></span>    | <span data-ttu-id="77671-166">Error</span><span class="sxs-lookup"><span data-stu-id="77671-166">Error</span></span>    |

> [!NOTE]
  <span data-ttu-id="77671-167">The datatype of the Event measurement is string.</span><span class="sxs-lookup"><span data-stu-id="77671-167">The datatype of the Event measurement is string.</span></span>

### <a name="device-properties"></a><span data-ttu-id="77671-168">Device properties</span><span class="sxs-lookup"><span data-stu-id="77671-168">Device properties</span></span>

<span data-ttu-id="77671-169">Add the following device properties in the **properties page**:</span><span class="sxs-lookup"><span data-stu-id="77671-169">Add the following device properties in the **properties page**:</span></span>

| <span data-ttu-id="77671-170">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-170">Display Name</span></span>        | <span data-ttu-id="77671-171">Field Name</span><span class="sxs-lookup"><span data-stu-id="77671-171">Field Name</span></span>        | <span data-ttu-id="77671-172">Data type</span><span class="sxs-lookup"><span data-stu-id="77671-172">Data type</span></span> |
| ------------------- | ----------------- | --------- |
| <span data-ttu-id="77671-173">Serial Number</span><span class="sxs-lookup"><span data-stu-id="77671-173">Serial Number</span></span>       | <span data-ttu-id="77671-174">serialNumber</span><span class="sxs-lookup"><span data-stu-id="77671-174">serialNumber</span></span>      | <span data-ttu-id="77671-175">text</span><span class="sxs-lookup"><span data-stu-id="77671-175">text</span></span>      |
| <span data-ttu-id="77671-176">Device Manufacturer</span><span class="sxs-lookup"><span data-stu-id="77671-176">Device Manufacturer</span></span> | <span data-ttu-id="77671-177">manufacturer</span><span class="sxs-lookup"><span data-stu-id="77671-177">manufacturer</span></span>      | <span data-ttu-id="77671-178">text</span><span class="sxs-lookup"><span data-stu-id="77671-178">text</span></span>      |

<span data-ttu-id="77671-179">Enter the field names exactly as shown in the table into the device template.</span><span class="sxs-lookup"><span data-stu-id="77671-179">Enter the field names exactly as shown in the table into the device template.</span></span> <span data-ttu-id="77671-180">If the field names do not match, the application cannot show the property value.</span><span class="sxs-lookup"><span data-stu-id="77671-180">If the field names do not match, the application cannot show the property value.</span></span>

### <a name="settings"></a><span data-ttu-id="77671-181">Settings</span><span class="sxs-lookup"><span data-stu-id="77671-181">Settings</span></span>

<span data-ttu-id="77671-182">Add the following **number** settings in the **settings page**:</span><span class="sxs-lookup"><span data-stu-id="77671-182">Add the following **number** settings in the **settings page**:</span></span>

| <span data-ttu-id="77671-183">Display Name</span><span class="sxs-lookup"><span data-stu-id="77671-183">Display Name</span></span>    | <span data-ttu-id="77671-184">Field Name</span><span class="sxs-lookup"><span data-stu-id="77671-184">Field Name</span></span>     | <span data-ttu-id="77671-185">Units</span><span class="sxs-lookup"><span data-stu-id="77671-185">Units</span></span> | <span data-ttu-id="77671-186">Decimals</span><span class="sxs-lookup"><span data-stu-id="77671-186">Decimals</span></span> | <span data-ttu-id="77671-187">Min</span><span class="sxs-lookup"><span data-stu-id="77671-187">Min</span></span> | <span data-ttu-id="77671-188">Max</span><span class="sxs-lookup"><span data-stu-id="77671-188">Max</span></span>  | <span data-ttu-id="77671-189">Initial</span><span class="sxs-lookup"><span data-stu-id="77671-189">Initial</span></span> |
| --------------- | -------------- | ----- | -------- | --- | ---- | ------- |
| <span data-ttu-id="77671-190">Fan Speed</span><span class="sxs-lookup"><span data-stu-id="77671-190">Fan Speed</span></span>       | <span data-ttu-id="77671-191">fanSpeed</span><span class="sxs-lookup"><span data-stu-id="77671-191">fanSpeed</span></span>       | <span data-ttu-id="77671-192">rpm</span><span class="sxs-lookup"><span data-stu-id="77671-192">rpm</span></span>   | <span data-ttu-id="77671-193">0</span><span class="sxs-lookup"><span data-stu-id="77671-193">0</span></span>        | <span data-ttu-id="77671-194">0</span><span class="sxs-lookup"><span data-stu-id="77671-194">0</span></span>   | <span data-ttu-id="77671-195">3000</span><span class="sxs-lookup"><span data-stu-id="77671-195">3000</span></span> | <span data-ttu-id="77671-196">0</span><span class="sxs-lookup"><span data-stu-id="77671-196">0</span></span>       |
| <span data-ttu-id="77671-197">Set Temperature</span><span class="sxs-lookup"><span data-stu-id="77671-197">Set Temperature</span></span> | <span data-ttu-id="77671-198">setTemperature</span><span class="sxs-lookup"><span data-stu-id="77671-198">setTemperature</span></span> | <span data-ttu-id="77671-199">F</span><span class="sxs-lookup"><span data-stu-id="77671-199">F</span></span>     | <span data-ttu-id="77671-200">0</span><span class="sxs-lookup"><span data-stu-id="77671-200">0</span></span>        | <span data-ttu-id="77671-201">20</span><span class="sxs-lookup"><span data-stu-id="77671-201">20</span></span>  | <span data-ttu-id="77671-202">200</span><span class="sxs-lookup"><span data-stu-id="77671-202">200</span></span>  | <span data-ttu-id="77671-203">80</span><span class="sxs-lookup"><span data-stu-id="77671-203">80</span></span>      |

<span data-ttu-id="77671-204">Enter field name exactly as shown in the table into the device template.</span><span class="sxs-lookup"><span data-stu-id="77671-204">Enter field name exactly as shown in the table into the device template.</span></span> <span data-ttu-id="77671-205">If the field names do not match, the device cannot receive the setting value.</span><span class="sxs-lookup"><span data-stu-id="77671-205">If the field names do not match, the device cannot receive the setting value.</span></span>

## <a name="add-a-real-device"></a><span data-ttu-id="77671-206">Add a real device</span><span class="sxs-lookup"><span data-stu-id="77671-206">Add a real device</span></span>

<span data-ttu-id="77671-207">In your Azure IoT Central application, add a real device from the device template you create and make a note of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="77671-207">In your Azure IoT Central application, add a real device from the device template you create and make a note of the device connection string.</span></span> <span data-ttu-id="77671-208">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md)</span><span class="sxs-lookup"><span data-stu-id="77671-208">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md)</span></span>

### <a name="create-a-nodejs-application"></a><span data-ttu-id="77671-209">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="77671-209">Create a Node.js application</span></span>

<span data-ttu-id="77671-210">The following steps show how to create a client application that implements the real device you added to the application.</span><span class="sxs-lookup"><span data-stu-id="77671-210">The following steps show how to create a client application that implements the real device you added to the application.</span></span>

1. <span data-ttu-id="77671-211">Create a folder called `connected-air-conditioner-adv` on your machine.</span><span class="sxs-lookup"><span data-stu-id="77671-211">Create a folder called `connected-air-conditioner-adv` on your machine.</span></span> <span data-ttu-id="77671-212">Navigate to that folder in your command-line environment.</span><span class="sxs-lookup"><span data-stu-id="77671-212">Navigate to that folder in your command-line environment.</span></span>

1. <span data-ttu-id="77671-213">To initialize your Node.js project, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="77671-213">To initialize your Node.js project, run the following commands:</span></span>

    ```cmd/sh
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="77671-214">Create a file called **connectedAirConditionerAdv.js** in the `connected-air-conditioner-adv` folder.</span><span class="sxs-lookup"><span data-stu-id="77671-214">Create a file called **connectedAirConditionerAdv.js** in the `connected-air-conditioner-adv` folder.</span></span>

1. <span data-ttu-id="77671-215">Add the following `require` statements at the start of the **connectedAirConditionerAdv.js** file:</span><span class="sxs-lookup"><span data-stu-id="77671-215">Add the following `require` statements at the start of the **connectedAirConditionerAdv.js** file:</span></span>

    ```javascript
    "use strict";

    // Use the Azure IoT device SDK for devices that connect to Azure IoT Central.
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    ```

1. <span data-ttu-id="77671-216">Add the following variable declarations to the file:</span><span class="sxs-lookup"><span data-stu-id="77671-216">Add the following variable declarations to the file:</span></span>

    ```javascript
    var connectionString = '{your device connection string}';
    var targetTemperature = 0;
    var client = clientFromConnectionString(connectionString);
    ```

    <span data-ttu-id="77671-217">Update the placeholder `{your device connection string}` with your device connection string.</span><span class="sxs-lookup"><span data-stu-id="77671-217">Update the placeholder `{your device connection string}` with your device connection string.</span></span> <span data-ttu-id="77671-218">You copied this value from the connection details page when you added your real device.</span><span class="sxs-lookup"><span data-stu-id="77671-218">You copied this value from the connection details page when you added your real device.</span></span> <span data-ttu-id="77671-219">In this sample, we initialize `targetTemperature` to zero, you can optionally take the current reading from the device or value from the device twin.</span><span class="sxs-lookup"><span data-stu-id="77671-219">In this sample, we initialize `targetTemperature` to zero, you can optionally take the current reading from the device or value from the device twin.</span></span> 

1. <span data-ttu-id="77671-220">To send telemetry, state and event measurements to your Azure IoT Central application, add the following function to the file:</span><span class="sxs-lookup"><span data-stu-id="77671-220">To send telemetry, state and event measurements to your Azure IoT Central application, add the following function to the file:</span></span>

    ```javascript
    // Send device measurements.
    function sendTelemetry() {
      var temperature = targetTemperature + (Math.random() * 15);
      var humidity = 70 + (Math.random() * 10);
      var pressure = 90 + (Math.random() * 5);
      var fanmode = 0;
      var data = JSON.stringify({ 
        temperature: temperature, 
        humidity: humidity, 
        pressure: pressure,
        fanmode: (temperature > 25) ? "1" : "0",
        overheat: (temperature > 35) ? "ER123" : undefined });
      var message = new Message(data);
      client.sendEvent(message, (err, res) => console.log(`Sent message: ${message.getData()}` +
        (err ? `; error: ${err.toString()}` : '') +
        (res ? `; status: ${res.constructor.name}` : '')));
    }
    ```

    1. <span data-ttu-id="77671-221">To send device properties to your Azure IoT Central application, add the following function to your file:</span><span class="sxs-lookup"><span data-stu-id="77671-221">To send device properties to your Azure IoT Central application, add the following function to your file:</span></span>

    ```javascript
    // Send device properties.
    function sendDeviceProperties(twin) {
      var properties = {
        serialNumber: '123-ABC',
        manufacturer: 'Contoso'
      };
      twin.properties.reported.update(properties, (err) => console.log(`Sent device properties; ` +
        (err ? `error: ${err.toString()}` : `status: success`)));
    }
    ```

1. <span data-ttu-id="77671-222">To define the settings your device responds to, add the following definition:</span><span class="sxs-lookup"><span data-stu-id="77671-222">To define the settings your device responds to, add the following definition:</span></span>

    ```javascript
    // Add any settings your device supports,
    // mapped to a function that is called when the setting is changed.
    var settings = {
      'fanSpeed': (newValue, callback) => {
          // Simulate it taking 1 second to set the fan speed.
          setTimeout(() => {
            callback(newValue, 'completed');
          }, 1000);
      },
      'setTemperature': (newValue, callback) => {
        // Simulate the temperature setting taking two steps.
        setTimeout(() => {
          targetTemperature = targetTemperature + (newValue - targetTemperature) / 2;
          callback(targetTemperature, 'pending');
          setTimeout(() => {
            targetTemperature = newValue;
            callback(targetTemperature, 'completed');
          }, 5000);
        }, 5000);
      }
    };
    ```

1. <span data-ttu-id="77671-223">To handle updated settings from your Azure IoT Central application, add the following to the file:</span><span class="sxs-lookup"><span data-stu-id="77671-223">To handle updated settings from your Azure IoT Central application, add the following to the file:</span></span>

    ```javascript
    // Handle settings changes that come from Azure IoT Central via the device twin.
    function handleSettings(twin) {
      twin.on('properties.desired', function (desiredChange) {
        for (let setting in desiredChange) {
          if (settings[setting]) {
            console.log(`Received setting: ${setting}: ${desiredChange[setting].value}`);
            settings[setting](desiredChange[setting].value, (newValue, status, message) => {
              var patch = {
                [setting]: {
                  value: newValue,
                  status: status,
                  desiredVersion: desiredChange.$version,
                  message: message
                }
              }
              twin.properties.reported.update(patch, (err) => console.log(`Sent setting update for ${setting}; ` +
                (err ? `error: ${err.toString()}` : `status: success`)));
            });
          }
        }
      });
    }
    ```

1. <span data-ttu-id="77671-224">Add the following to complete the connection to Azure IoT Central and hook up the functions in the client code:</span><span class="sxs-lookup"><span data-stu-id="77671-224">Add the following to complete the connection to Azure IoT Central and hook up the functions in the client code:</span></span>

    ```javascript
    // Handle device connection to Azure IoT Central.
    var connectCallback = (err) => {
      if (err) {
        console.log(`Device could not connect to Azure IoT Central: ${err.toString()}`);
      } else {
        console.log('Device successfully connected to Azure IoT Central');

        // Send telemetry measurements to Azure IoT Central every 1 second.
        setInterval(sendTelemetry, 1000);

        // Get device twin from Azure IoT Central.
        client.getTwin((err, twin) => {
          if (err) {
            console.log(`Error getting device twin: ${err.toString()}`);
          } else {
            // Send device properties once on device start up.
            sendDeviceProperties(twin);
            // Apply device settings and handle changes to device settings.
            handleSettings(twin);
          }
        });
      }
    };

    // Start the device (connect it to Azure IoT Central).
    client.open(connectCallback);
    ```

## <a name="run-your-nodejs-application"></a><span data-ttu-id="77671-225">Run your Node.js application</span><span class="sxs-lookup"><span data-stu-id="77671-225">Run your Node.js application</span></span>

<span data-ttu-id="77671-226">Run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="77671-226">Run the following command in your command-line environment:</span></span>

```cmd/sh
node connectedAirConditionerAdv.js
```

<span data-ttu-id="77671-227">As an operator in your Azure IoT Central application, for your real device you can:</span><span class="sxs-lookup"><span data-stu-id="77671-227">As an operator in your Azure IoT Central application, for your real device you can:</span></span>

* <span data-ttu-id="77671-228">View the telemetry on the **Measurements** page:</span><span class="sxs-lookup"><span data-stu-id="77671-228">View the telemetry on the **Measurements** page:</span></span>

    ![View telemetry](media/howto-connect-nodejs/viewtelemetry.png)

* <span data-ttu-id="77671-230">View the device property values sent from your device on the **Properties** page.</span><span class="sxs-lookup"><span data-stu-id="77671-230">View the device property values sent from your device on the **Properties** page.</span></span>

    ![View device properties](media/howto-connect-nodejs/viewproperties.png)

* <span data-ttu-id="77671-232">Set the fan speed and target temperature from the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="77671-232">Set the fan speed and target temperature from the **Settings** page.</span></span>

    ![Set fan speed](media/howto-connect-nodejs/setfanspeed.png)

## <a name="next-steps"></a><span data-ttu-id="77671-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="77671-234">Next steps</span></span>

<span data-ttu-id="77671-235">Now that you have learned how to connect a generic Node.js client to your Azure IoT Central application, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="77671-235">Now that you have learned how to connect a generic Node.js client to your Azure IoT Central application, here are the suggested next steps:</span></span>
* <span data-ttu-id="77671-236">[Prepare and connect a Raspberry Pi](howto-connect-raspberry-pi-python.md)
<!-- Next how-tos in the sequence --></span><span class="sxs-lookup"><span data-stu-id="77671-236">[Prepare and connect a Raspberry Pi](howto-connect-raspberry-pi-python.md)
<!-- Next how-tos in the sequence --></span></span>
