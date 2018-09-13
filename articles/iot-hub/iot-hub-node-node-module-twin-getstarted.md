---
title: Get started with Azure IoT Hub module identity and module twin (Node.js) | Microsoft Docs
description: Learn how to create module identity and update module twin using IoT SDKs for Node.js.
author: chrissie926
manager: ''
ms.service: iot-hub
services: iot-hub
ms.devlang: node
ms.topic: conceptual
ms.date: 04/26/2018
ms.author: menchi
ms.openlocfilehash: fa77e117b8045be4ef0566e388c4e8df08c95fe2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864691"
---
# <a name="get-started-with-iot-hub-module-identity-and-module-twin-using-nodejs-back-end-and-nodejs-device"></a><span data-ttu-id="e5efa-103">Get started with IoT Hub module identity and module twin using Node.js back end and Node.js device</span><span class="sxs-lookup"><span data-stu-id="e5efa-103">Get started with IoT Hub module identity and module twin using Node.js back end and Node.js device</span></span>

> [!NOTE]
> <span data-ttu-id="e5efa-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span><span class="sxs-lookup"><span data-stu-id="e5efa-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span></span> <span data-ttu-id="e5efa-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span><span class="sxs-lookup"><span data-stu-id="e5efa-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span></span> <span data-ttu-id="e5efa-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span><span class="sxs-lookup"><span data-stu-id="e5efa-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span></span>

<span data-ttu-id="e5efa-107">At the end of this tutorial, you have two Node.js apps:</span><span class="sxs-lookup"><span data-stu-id="e5efa-107">At the end of this tutorial, you have two Node.js apps:</span></span>

* <span data-ttu-id="e5efa-108">**CreateIdentities**, which creates a device identity, a module identity and associated security key to connect your device and module clients.</span><span class="sxs-lookup"><span data-stu-id="e5efa-108">**CreateIdentities**, which creates a device identity, a module identity and associated security key to connect your device and module clients.</span></span>
* <span data-ttu-id="e5efa-109">**UpdateModuleTwinReportedProperties**, which sends updated module twin reported properties to your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e5efa-109">**UpdateModuleTwinReportedProperties**, which sends updated module twin reported properties to your IoT Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e5efa-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="e5efa-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="e5efa-111">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="e5efa-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e5efa-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="e5efa-112">An active Azure account.</span></span> <span data-ttu-id="e5efa-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="e5efa-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>
* <span data-ttu-id="e5efa-114">An IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e5efa-114">An IoT Hub.</span></span>
* <span data-ttu-id="e5efa-115">Install the latest [Node.js SDK](https://github.com/Azure/azure-iot-sdk-node).</span><span class="sxs-lookup"><span data-stu-id="e5efa-115">Install the latest [Node.js SDK](https://github.com/Azure/azure-iot-sdk-node).</span></span>


<span data-ttu-id="e5efa-116">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e5efa-116">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity-and-a-module-identity-in-iot-hub"></a><span data-ttu-id="e5efa-117">Create a device identity and a module identity in IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e5efa-117">Create a device identity and a module identity in IoT Hub</span></span>

<span data-ttu-id="e5efa-118">In this section, you create a Node.js app that creates a device identity and a module identity in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e5efa-118">In this section, you create a Node.js app that creates a device identity and a module identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="e5efa-119">A device or module cannot connect to IoT hub unless it has an entry in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="e5efa-119">A device or module cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="e5efa-120">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="e5efa-120">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="e5efa-121">When you run this console app, it generates a unique ID and key for both device and module.</span><span class="sxs-lookup"><span data-stu-id="e5efa-121">When you run this console app, it generates a unique ID and key for both device and module.</span></span> <span data-ttu-id="e5efa-122">Your device and module use these values to identify itself when it sends device-to-cloud messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e5efa-122">Your device and module use these values to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="e5efa-123">The IDs are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e5efa-123">The IDs are case-sensitive.</span></span>

1.  <span data-ttu-id="e5efa-124">Create a directory to hold your code.</span><span class="sxs-lookup"><span data-stu-id="e5efa-124">Create a directory to hold your code.</span></span>
2. <span data-ttu-id="e5efa-125">Inside of that directory, first run **npm init -y** to create an empty package.json with defaults.</span><span class="sxs-lookup"><span data-stu-id="e5efa-125">Inside of that directory, first run **npm init -y** to create an empty package.json with defaults.</span></span> <span data-ttu-id="e5efa-126">This is the project file for your code.</span><span class="sxs-lookup"><span data-stu-id="e5efa-126">This is the project file for your code.</span></span>
3. <span data-ttu-id="e5efa-127">Run **npm install -S azure-iothub@modules-preview** to install the service SDK inside the **node_modules** subdirectory.</span><span class="sxs-lookup"><span data-stu-id="e5efa-127">Run **npm install -S azure-iothub@modules-preview** to install the service SDK inside the **node_modules** subdirectory.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="e5efa-128">The subdirectory name node_modules uses the word module to mean "a node library".</span><span class="sxs-lookup"><span data-stu-id="e5efa-128">The subdirectory name node_modules uses the word module to mean "a node library".</span></span> <span data-ttu-id="e5efa-129">The term here has nothing to do with IoT Hub modules.</span><span class="sxs-lookup"><span data-stu-id="e5efa-129">The term here has nothing to do with IoT Hub modules.</span></span>

4. <span data-ttu-id="e5efa-130">Create the following .js file in your directory.</span><span class="sxs-lookup"><span data-stu-id="e5efa-130">Create the following .js file in your directory.</span></span> <span data-ttu-id="e5efa-131">Call it **add.js**.</span><span class="sxs-lookup"><span data-stu-id="e5efa-131">Call it **add.js**.</span></span> <span data-ttu-id="e5efa-132">Copy and paste your hub connection string and hub name.</span><span class="sxs-lookup"><span data-stu-id="e5efa-132">Copy and paste your hub connection string and hub name.</span></span>

    ```javascript
    var Registry = require('azure-iothub').Registry;
    var uuid = require('uuid');
    // Copy/paste your connection string and hub name here
    var serviceConnectionString = '<hub connection string from portal>';
    var hubName = '<hub name>.azure-devices.net';
    // Create an instance of the IoTHub registry
    var registry = Registry.fromConnectionString(serviceConnectionString);
    // Insert your device ID and moduleId here.
    var deviceId = 'myFirstDevice';
    var moduleId = 'myFirstModule';
    // Create your device as a SAS authentication device
    var primaryKey = new Buffer(uuid.v4()).toString('base64');
    var secondaryKey = new Buffer(uuid.v4()).toString('base64');
    var deviceDescription = {
      deviceId: deviceId,
      status: 'enabled',
      authentication: {
        type: 'sas',
        symmetricKey: {
          primaryKey: primaryKey,
          secondaryKey: secondaryKey
        }
      }
    };

    // First, create a device identity
    registry.create(deviceDescription, function(err) {
      if (err) {
        console.log('Error creating device identity: ' + err);
        process.exit(1);
      }
      console.log('device connection string = "HostName=' + hubName + ';DeviceId=' + deviceId + ';SharedAccessKey=' + primaryKey + '"');

    // Then add a module to that device
      registry.addModule({ deviceId: deviceId, moduleId: moduleId }, function(err) {
        if (err) {
          console.log('Error creating module identity: ' + err);
          process.exit(1);
        }

    // Finally, retrieve the module details from the hub so we can construct the connection string
        registry.getModule(deviceId, moduleId, function(err, foundModule) {
          if (err) {
            console.log('Error getting module back from hub: ' + err);
            process.exit(1);
          }
          console.log('module connection string = "HostName=' + hubName + ';DeviceId=' + foundModule.deviceId + ';ModuleId='+foundModule.moduleId+';SharedAccessKey=' + foundModule.authentication.symmetricKey.primaryKey + '"');
          process.exit(0);
        });
      });
    });

    ```

<span data-ttu-id="e5efa-133">This app creates a device identity with ID **myFirstDevice** and a module identity with ID **myFirstModule** under device **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="e5efa-133">This app creates a device identity with ID **myFirstDevice** and a module identity with ID **myFirstModule** under device **myFirstDevice**.</span></span> <span data-ttu-id="e5efa-134">(If that module ID already exists in the identity registry, the code simply retrieves the existing module information.) The app then displays the primary key for that identity.</span><span class="sxs-lookup"><span data-stu-id="e5efa-134">(If that module ID already exists in the identity registry, the code simply retrieves the existing module information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="e5efa-135">You use this key in the simulated module app to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e5efa-135">You use this key in the simulated module app to connect to your IoT hub.</span></span>

5. <span data-ttu-id="e5efa-136">Run this using node add.js.</span><span class="sxs-lookup"><span data-stu-id="e5efa-136">Run this using node add.js.</span></span> <span data-ttu-id="e5efa-137">It will give you a connection string for your device identity and another one for your module identity.</span><span class="sxs-lookup"><span data-stu-id="e5efa-137">It will give you a connection string for your device identity and another one for your module identity.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e5efa-138">The IoT Hub identity registry only stores device and module identities to enable secure access to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e5efa-138">The IoT Hub identity registry only stores device and module identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="e5efa-139">The identity registry stores device IDs and keys to use as security credentials.</span><span class="sxs-lookup"><span data-stu-id="e5efa-139">The identity registry stores device IDs and keys to use as security credentials.</span></span> <span data-ttu-id="e5efa-140">The identity registry also stores an enabled/disabled flag for each device that you can use to disable access for that device.</span><span class="sxs-lookup"><span data-stu-id="e5efa-140">The identity registry also stores an enabled/disabled flag for each device that you can use to disable access for that device.</span></span> <span data-ttu-id="e5efa-141">If your application needs to store other device-specific metadata, it should use an application-specific store.</span><span class="sxs-lookup"><span data-stu-id="e5efa-141">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="e5efa-142">There is no enabled/disabled flag for module identities.</span><span class="sxs-lookup"><span data-stu-id="e5efa-142">There is no enabled/disabled flag for module identities.</span></span> <span data-ttu-id="e5efa-143">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="e5efa-143">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="update-the-module-twin-using-nodejs-device-sdk"></a><span data-ttu-id="e5efa-144">Update the module twin using Node.js device SDK</span><span class="sxs-lookup"><span data-stu-id="e5efa-144">Update the module twin using Node.js device SDK</span></span>

<span data-ttu-id="e5efa-145">In this section, you create a Node.js app on your simulated device that updates the module twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="e5efa-145">In this section, you create a Node.js app on your simulated device that updates the module twin reported properties.</span></span>

1. <span data-ttu-id="e5efa-146">**Get your module connection string** -- now if you login to [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="e5efa-146">**Get your module connection string** -- now if you login to [Azure portal][lnk-portal].</span></span> <span data-ttu-id="e5efa-147">Navigate to your IoT Hub and click IoT Devices.</span><span class="sxs-lookup"><span data-stu-id="e5efa-147">Navigate to your IoT Hub and click IoT Devices.</span></span> <span data-ttu-id="e5efa-148">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span><span class="sxs-lookup"><span data-stu-id="e5efa-148">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span></span> <span data-ttu-id="e5efa-149">Copy the module connection string.</span><span class="sxs-lookup"><span data-stu-id="e5efa-149">Copy the module connection string.</span></span> <span data-ttu-id="e5efa-150">It is needed in the next step.</span><span class="sxs-lookup"><span data-stu-id="e5efa-150">It is needed in the next step.</span></span>

    ![Azure portal module detail][15]

2. <span data-ttu-id="e5efa-152">Similar to you did in the step above, create a directory for your device code and use NPM to initialize it and install the device SDK (**npm install -S azure-iot-device-amqp@modules-preview**).</span><span class="sxs-lookup"><span data-stu-id="e5efa-152">Similar to you did in the step above, create a directory for your device code and use NPM to initialize it and install the device SDK (**npm install -S azure-iot-device-amqp@modules-preview**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e5efa-153">The npm install command may feel slow.</span><span class="sxs-lookup"><span data-stu-id="e5efa-153">The npm install command may feel slow.</span></span> <span data-ttu-id="e5efa-154">Be patient, it's pulling down lots of code from the package repository.</span><span class="sxs-lookup"><span data-stu-id="e5efa-154">Be patient, it's pulling down lots of code from the package repository.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5efa-155">If you see an error that says npm ERR!</span><span class="sxs-lookup"><span data-stu-id="e5efa-155">If you see an error that says npm ERR!</span></span> <span data-ttu-id="e5efa-156">registry error parsing json, this is safe to ignore.</span><span class="sxs-lookup"><span data-stu-id="e5efa-156">registry error parsing json, this is safe to ignore.</span></span> <span data-ttu-id="e5efa-157">If you see an error that says npm ERR!</span><span class="sxs-lookup"><span data-stu-id="e5efa-157">If you see an error that says npm ERR!</span></span> <span data-ttu-id="e5efa-158">registry error parsing json, this is safe to ignore.</span><span class="sxs-lookup"><span data-stu-id="e5efa-158">registry error parsing json, this is safe to ignore.</span></span>

3. <span data-ttu-id="e5efa-159">Create a file called twin.js.</span><span class="sxs-lookup"><span data-stu-id="e5efa-159">Create a file called twin.js.</span></span> <span data-ttu-id="e5efa-160">Copy and paste your module identity string.</span><span class="sxs-lookup"><span data-stu-id="e5efa-160">Copy and paste your module identity string.</span></span>

    ```javascript
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-amqp').Amqp;
    // Copy/paste your module connection string here.
    var connectionString = '<insert module connection string here>';
    // Create a client using the Amqp protocol.
    var client = Client.fromConnectionString(connectionString, Protocol);
    client.on('error', function (err) {
      console.error(err.message);
    });
    // connect to the hub
    client.open(function(err) {
      if (err) {
        console.error('error connecting to hub: ' + err);
        process.exit(1);
      }
      console.log('client opened');
    // Create device Twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('error getting twin: ' + err);
          process.exit(1);
        }
    // Output the current properties
        console.log('twin contents:');
        console.log(twin.properties);
    // Add a handler for desired property changes
        twin.on('properties.desired', function(delta) {
            console.log('new desired properties received:');
            console.log(JSON.stringify(delta));
        });
    // create a patch to send to the hub
        var patch = {
          updateTime: new Date().toString(),
          firmwareVersion:'1.2.1',
          weather:{
            temperature: 72,
            humidity: 17
          }
        };
    // send the patch
        twin.properties.reported.update(patch, function(err) {
          if (err) throw err;
          console.log('twin state reported');
        });
      });
    });
    ```

2. <span data-ttu-id="e5efa-161">Now, run this using the command **node twin.js**.</span><span class="sxs-lookup"><span data-stu-id="e5efa-161">Now, run this using the command **node twin.js**.</span></span>

    ```
    F:\temp\module_twin>node twin.js
    client opened
    twin contents:
    { reported: { update: [Function: update], '$version': 1 },
      desired: { '$version': 1 } }
    new desired properties received:
    {"$version":1}
    twin state reported
    ```

## <a name="next-steps"></a><span data-ttu-id="e5efa-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5efa-162">Next steps</span></span>

<span data-ttu-id="e5efa-163">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="e5efa-163">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="e5efa-164">[Getting started with device management][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="e5efa-164">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="e5efa-165">[Getting started with IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="e5efa-165">[Getting started with IoT Edge][lnk-iot-edge]</span></span>


<!-- Images. -->
[15]: ./media\iot-hub-csharp-csharp-module-twin-getstarted/module-detail.JPG
<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/