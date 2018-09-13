---
title: Add a real device to an Azure IoT Central application | Microsoft Docs
description: As an operator, add a real device to your Azure IoT Central application.
author: sandeeppujar
ms.author: sandeepu
ms.date: 04/16/2018
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: peterpr
ms.openlocfilehash: dd68b65825c9c22453e0191d42a0fcce3b65ca64
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856047"
---
# <a name="tutorial-add-a-real-device-to-your-azure-iot-central-application"></a><span data-ttu-id="eb2dd-103">Tutorial: Add a real device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-103">Tutorial: Add a real device to your Azure IoT Central application</span></span>

<span data-ttu-id="eb2dd-104">This tutorial shows you how to add and configure a real device to your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-104">This tutorial shows you how to add and configure a real device to your Microsoft Azure IoT Central application.</span></span>

<span data-ttu-id="eb2dd-105">This tutorial is made up of two parts:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-105">This tutorial is made up of two parts:</span></span>

1. <span data-ttu-id="eb2dd-106">First, as an operator, you learn how to add and configure a real device in your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-106">First, as an operator, you learn how to add and configure a real device in your Azure IoT Central application.</span></span> <span data-ttu-id="eb2dd-107">At the end of this part, you retrieve a connection string to use in the second part.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-107">At the end of this part, you retrieve a connection string to use in the second part.</span></span>
2. <span data-ttu-id="eb2dd-108">Then, as a device developer, you learn about the code in your real device.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-108">Then, as a device developer, you learn about the code in your real device.</span></span> <span data-ttu-id="eb2dd-109">You add the connection string from the first part to the sample code.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-109">You add the connection string from the first part to the sample code.</span></span>

<span data-ttu-id="eb2dd-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-110">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb2dd-111">Add a new real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-111">Add a new real device</span></span>
> * <span data-ttu-id="eb2dd-112">Configure the new device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-112">Configure the new device</span></span>
> * <span data-ttu-id="eb2dd-113">Get connection string for real device from the application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-113">Get connection string for real device from the application</span></span>
> * <span data-ttu-id="eb2dd-114">Understand how client code maps to the application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-114">Understand how client code maps to the application</span></span>
> * <span data-ttu-id="eb2dd-115">Configure client code for the real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-115">Configure client code for the real device</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb2dd-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eb2dd-116">Prerequisites</span></span>

<span data-ttu-id="eb2dd-117">Before you begin, the builder should complete at least the first builder tutorial to create the Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-117">Before you begin, the builder should complete at least the first builder tutorial to create the Azure IoT Central application:</span></span>

* <span data-ttu-id="eb2dd-118">[Define a new device type](tutorial-define-device-type.md) (Required)</span><span class="sxs-lookup"><span data-stu-id="eb2dd-118">[Define a new device type](tutorial-define-device-type.md) (Required)</span></span>
* <span data-ttu-id="eb2dd-119">[Configure rules and actions for your device](tutorial-configure-rules.md) (Optional)</span><span class="sxs-lookup"><span data-stu-id="eb2dd-119">[Configure rules and actions for your device](tutorial-configure-rules.md) (Optional)</span></span>
* <span data-ttu-id="eb2dd-120">[Customize the operator's views](tutorial-customize-operator.md) (Optional)</span><span class="sxs-lookup"><span data-stu-id="eb2dd-120">[Customize the operator's views](tutorial-customize-operator.md) (Optional)</span></span>

## <a name="add-a-real-device"></a><span data-ttu-id="eb2dd-121">Add a real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-121">Add a real device</span></span>

<span data-ttu-id="eb2dd-122">To add a real device to your application, you use the **Connected Air Conditioner** device template you created in the [Define a new device type](tutorial-define-device-type.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-122">To add a real device to your application, you use the **Connected Air Conditioner** device template you created in the [Define a new device type](tutorial-define-device-type.md) tutorial.</span></span>

1. <span data-ttu-id="eb2dd-123">To add a new device as an operator choose **Device Explorer** in the left navigation menu:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-123">To add a new device as an operator choose **Device Explorer** in the left navigation menu:</span></span>

   ![Device explorer page showing connected air conditioner](media/tutorial-add-device/explorer.png)

   <span data-ttu-id="eb2dd-125">The **Device Explorer** shows the **Connected Air Conditioner** device template and the simulated device that was automatically created when the builder created the device template.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-125">The **Device Explorer** shows the **Connected Air Conditioner** device template and the simulated device that was automatically created when the builder created the device template.</span></span>

2. <span data-ttu-id="eb2dd-126">To start connecting a real connected air conditioner device, choose **New**, then **Real**:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-126">To start connecting a real connected air conditioner device, choose **New**, then **Real**:</span></span>

   ![Start adding a new, real connected air conditioner device](media/tutorial-add-device/newreal.png)

3. <span data-ttu-id="eb2dd-128">Optionally, you can rename your new device by choosing the device name and editing the value:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-128">Optionally, you can rename your new device by choosing the device name and editing the value:</span></span>

   ![Rename the device](media/tutorial-add-device/rename.png)

## <a name="configure-a-real-device"></a><span data-ttu-id="eb2dd-130">Configure a real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-130">Configure a real device</span></span>

<span data-ttu-id="eb2dd-131">The real device is created from the **Connected Air Conditioner** device template.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-131">The real device is created from the **Connected Air Conditioner** device template.</span></span> <span data-ttu-id="eb2dd-132">As a builder, you can use **Settings** to configure your device and set property values to record information about your device.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-132">As a builder, you can use **Settings** to configure your device and set property values to record information about your device.</span></span>

1. <span data-ttu-id="eb2dd-133">On the **Settings** page, notice that the **Set Temperature** setting status is **no update**.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-133">On the **Settings** page, notice that the **Set Temperature** setting status is **no update**.</span></span> <span data-ttu-id="eb2dd-134">It stays in this state until the real device connects and acknowledges that it has acted on the setting:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-134">It stays in this state until the real device connects and acknowledges that it has acted on the setting:</span></span>

    ![Settings show syncing](media/tutorial-add-device/settingssyncing.png)

2. <span data-ttu-id="eb2dd-136">On the **Properties** page for your new, real connected air conditioner device, set **Serial Number** to **rcac0010**, and **Firmware version** to 9.75.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-136">On the **Properties** page for your new, real connected air conditioner device, set **Serial Number** to **rcac0010**, and **Firmware version** to 9.75.</span></span> <span data-ttu-id="eb2dd-137">Then choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-137">Then choose **Save**:</span></span>

    ![Set properties for real device](media/tutorial-add-device/setproperties.png)

3. <span data-ttu-id="eb2dd-139">As a builder, you can view the **Measurements**, **Rules**, and **Dashboard** pages for your real device.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-139">As a builder, you can view the **Measurements**, **Rules**, and **Dashboard** pages for your real device.</span></span>

## <a name="get-connection-string-for-real-device-from-application"></a><span data-ttu-id="eb2dd-140">Get connection string for real device from application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-140">Get connection string for real device from application</span></span>

<span data-ttu-id="eb2dd-141">A device developer needs to embed the *connection string* for your real device in the code that runs on the device.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-141">A device developer needs to embed the *connection string* for your real device in the code that runs on the device.</span></span> <span data-ttu-id="eb2dd-142">The connection string enables the device to connect securely to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-142">The connection string enables the device to connect securely to your Azure IoT Central application.</span></span> <span data-ttu-id="eb2dd-143">Every device instance has a unique connection string.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-143">Every device instance has a unique connection string.</span></span> <span data-ttu-id="eb2dd-144">The following steps show you how to find the connection string for a device instance in your application:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-144">The following steps show you how to find the connection string for a device instance in your application:</span></span>

1. <span data-ttu-id="eb2dd-145">On the **Device** screen for your real connected air conditioner device, choose **Connect this device**:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-145">On the **Device** screen for your real connected air conditioner device, choose **Connect this device**:</span></span>

    ![Device page showing view connection information link](media/tutorial-add-device/connectionlink.png)

2. <span data-ttu-id="eb2dd-147">On the **Connect** page, copy the **Primary connection string**, and save it.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-147">On the **Connect** page, copy the **Primary connection string**, and save it.</span></span> <span data-ttu-id="eb2dd-148">You use this value in the second half of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-148">You use this value in the second half of this tutorial.</span></span> <span data-ttu-id="eb2dd-149">A device developer uses this value in the client application that runs on the device:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-149">A device developer uses this value in the client application that runs on the device:</span></span>

    ![Connection string values](media/tutorial-add-device/connectionstring.png)

## <a name="prepare-the-client-code"></a><span data-ttu-id="eb2dd-151">Prepare the client code</span><span class="sxs-lookup"><span data-stu-id="eb2dd-151">Prepare the client code</span></span>

<span data-ttu-id="eb2dd-152">The example code in this article is written in [Node.js](https://nodejs.org/) and shows just enough code to:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-152">The example code in this article is written in [Node.js](https://nodejs.org/) and shows just enough code to:</span></span>

* <span data-ttu-id="eb2dd-153">Connect as a device to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-153">Connect as a device to your Azure IoT Central application.</span></span>
* <span data-ttu-id="eb2dd-154">Send temperature telemetry as a connected air conditioner device.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-154">Send temperature telemetry as a connected air conditioner device.</span></span>
* <span data-ttu-id="eb2dd-155">Respond to an operator who uses the **Set Temperature** setting.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-155">Respond to an operator who uses the **Set Temperature** setting.</span></span>

<span data-ttu-id="eb2dd-156">The "How to" articles referenced in the [Next Steps](#next-steps) section provide more complete samples and show the use of other programming languages.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-156">The "How to" articles referenced in the [Next Steps](#next-steps) section provide more complete samples and show the use of other programming languages.</span></span> <span data-ttu-id="eb2dd-157">For more information about how devices connect to Azure IoT Central, see the [Device connectivity](concepts-connectivity.md) article.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-157">For more information about how devices connect to Azure IoT Central, see the [Device connectivity](concepts-connectivity.md) article.</span></span>

<span data-ttu-id="eb2dd-158">The following steps show how to prepare the [Node.js](https://nodejs.org/) sample:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-158">The following steps show how to prepare the [Node.js](https://nodejs.org/) sample:</span></span>

1. <span data-ttu-id="eb2dd-159">Install [Node.js](https://nodejs.org/) version 4.0.x or later in your machine.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-159">Install [Node.js](https://nodejs.org/) version 4.0.x or later in your machine.</span></span> <span data-ttu-id="eb2dd-160">Node.js is available for a wide variety of operating systems.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-160">Node.js is available for a wide variety of operating systems.</span></span>

2. <span data-ttu-id="eb2dd-161">Create a folder called `connectedairconditioner` on your machine.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-161">Create a folder called `connectedairconditioner` on your machine.</span></span>

3. <span data-ttu-id="eb2dd-162">In your command-line environment, navigate to the `connectedairconditioner` folder you created.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-162">In your command-line environment, navigate to the `connectedairconditioner` folder you created.</span></span>

4. <span data-ttu-id="eb2dd-163">To initialize your Node.js project, run the following command accepting all the defaults:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-163">To initialize your Node.js project, run the following command accepting all the defaults:</span></span>

   ```cmd/sh
   npm init
   ```

5. <span data-ttu-id="eb2dd-164">To install the necessary packages, run the following command:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-164">To install the necessary packages, run the following command:</span></span>

   ```cmd/sh
   npm install azure-iot-device azure-iot-device-mqtt --save
   ```

6. <span data-ttu-id="eb2dd-165">Using a text editor, create a file called **ConnectedAirConditioner.js** in the `connectedairconditioner` folder.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-165">Using a text editor, create a file called **ConnectedAirConditioner.js** in the `connectedairconditioner` folder.</span></span>

7. <span data-ttu-id="eb2dd-166">Add the following `require` statements at the start of the **ConnectedAirConditioner.js** file:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-166">Add the following `require` statements at the start of the **ConnectedAirConditioner.js** file:</span></span>

   ```javascript
   'use strict';

   var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
   var Message = require('azure-iot-device').Message;
   var ConnectionString = require('azure-iot-device').ConnectionString;
   ```

8. <span data-ttu-id="eb2dd-167">Add the following variable declarations to the file:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-167">Add the following variable declarations to the file:</span></span>

   ```javascript
   var connectionString = '{your device connection string}';
   var targetTemperature = 0;
   var client = clientFromConnectionString(connectionString);
   ```

   > [!NOTE]
   > <span data-ttu-id="eb2dd-168">You update the placeholder `{your device connection string}` in a later step.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-168">You update the placeholder `{your device connection string}` in a later step.</span></span>

9. <span data-ttu-id="eb2dd-169">Save the changes you have made so far, but keep the file open.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-169">Save the changes you have made so far, but keep the file open.</span></span>

## <a name="understand-how-client-code-maps-to-the-application"></a><span data-ttu-id="eb2dd-170">Understand how client code maps to the application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-170">Understand how client code maps to the application</span></span>

<span data-ttu-id="eb2dd-171">In the previous section, you created a skeleton Node.js project for an application that connects to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-171">In the previous section, you created a skeleton Node.js project for an application that connects to your Azure IoT Central application.</span></span> <span data-ttu-id="eb2dd-172">In this section, you add the code to:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-172">In this section, you add the code to:</span></span>

* <span data-ttu-id="eb2dd-173">Connect to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-173">Connect to your Azure IoT Central application.</span></span>
* <span data-ttu-id="eb2dd-174">Send telemetry to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-174">Send telemetry to your Azure IoT Central application.</span></span>
* <span data-ttu-id="eb2dd-175">Receive settings from your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-175">Receive settings from your Azure IoT Central application.</span></span>

1. <span data-ttu-id="eb2dd-176">To send temperature telemetry to your Azure IoT Central application, add the following code to the **ConnectedAirConditioner.js** file:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-176">To send temperature telemetry to your Azure IoT Central application, add the following code to the **ConnectedAirConditioner.js** file:</span></span>

   ```javascript
   // Send device telemetry.
   function sendTelemetry() {
     var temperature = targetTemperature + (Math.random() * 15);
     var data = JSON.stringify({ temperature: temperature });
     var message = new Message(data);
     client.sendEvent(message, (err, res) => console.log(`Sent message: ${message.getData()}` +
       (err ? `; error: ${err.toString()}` : '') +
       (res ? `; status: ${res.constructor.name}` : '')));
   }
   ```

   <span data-ttu-id="eb2dd-177">The name of the field in the JSON you send must match the name of the field you specified for temperature telemetry in your device template.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-177">The name of the field in the JSON you send must match the name of the field you specified for temperature telemetry in your device template.</span></span> <span data-ttu-id="eb2dd-178">In this example, the name of the field is **temperature**.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-178">In this example, the name of the field is **temperature**.</span></span>

2. <span data-ttu-id="eb2dd-179">To define the settings your device supports, such as **setTemperature**, add the following definition:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-179">To define the settings your device supports, such as **setTemperature**, add the following definition:</span></span>

   ```javascript
   // Add any settings your device supports
   // mapped to a function that is called when the setting is changed.
   var settings = {
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

3. <span data-ttu-id="eb2dd-180">To handle settings sent from Azure IoT Central, add the following function that locates and executes the appropriate device code:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-180">To handle settings sent from Azure IoT Central, add the following function that locates and executes the appropriate device code:</span></span>

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

    <span data-ttu-id="eb2dd-181">This function:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-181">This function:</span></span>

    * <span data-ttu-id="eb2dd-182">Watches for Azure IoT Central sending a desired property.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-182">Watches for Azure IoT Central sending a desired property.</span></span>
    * <span data-ttu-id="eb2dd-183">Locates the appropriate function to call to handle the setting change.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-183">Locates the appropriate function to call to handle the setting change.</span></span>
    * <span data-ttu-id="eb2dd-184">Sends an acknowledgement back to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-184">Sends an acknowledgement back to your Azure IoT Central application.</span></span>

4. <span data-ttu-id="eb2dd-185">Add the following code to complete the connection to Azure IoT Central and hook up the functions in the client code:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-185">Add the following code to complete the connection to Azure IoT Central and hook up the functions in the client code:</span></span>

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
           // Apply device settings and handle changes to device settings.
           handleSettings(twin);
         }
       });
     }
   };

   client.open(connectCallback);
   ```

5. <span data-ttu-id="eb2dd-186">Save the changes you have made so far, but keep the file open.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-186">Save the changes you have made so far, but keep the file open.</span></span>

## <a name="configure-client-code-for-the-real-device"></a><span data-ttu-id="eb2dd-187">Configure client code for the real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-187">Configure client code for the real device</span></span>

<span data-ttu-id="eb2dd-188"><!-- Add the connection string to the sample code, build, and run --> To configure your client code to connect to your Azure IoT Central application, you need to add the connection string for your real device that you noted earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-188"><!-- Add the connection string to the sample code, build, and run --> To configure your client code to connect to your Azure IoT Central application, you need to add the connection string for your real device that you noted earlier in this tutorial.</span></span>

1. <span data-ttu-id="eb2dd-189">In the **ConnectedAirConditioner.js** file, find the following line of code:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-189">In the **ConnectedAirConditioner.js** file, find the following line of code:</span></span>

   ```javascript
   var connectionString = '{your device connection string}';
   ```

2. <span data-ttu-id="eb2dd-190">Replace `{your device connection string}` with the connection string of your real device.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-190">Replace `{your device connection string}` with the connection string of your real device.</span></span> <span data-ttu-id="eb2dd-191">You made a note of the connection string at the end of the "Get connection string for real device from application" section.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-191">You made a note of the connection string at the end of the "Get connection string for real device from application" section.</span></span>

3. <span data-ttu-id="eb2dd-192">Save the changes to the **ConnectedAirConditioner.js** file.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-192">Save the changes to the **ConnectedAirConditioner.js** file.</span></span>

4. <span data-ttu-id="eb2dd-193">To run the sample, enter the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-193">To run the sample, enter the following command in your command-line environment:</span></span>

   ```cmd/sh
   node ConnectedAirConditioner.js
   ```

   > [!NOTE]
   > <span data-ttu-id="eb2dd-194">Make sure you are in the `connectedairconditioner` folder when you run this command.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-194">Make sure you are in the `connectedairconditioner` folder when you run this command.</span></span>

5. <span data-ttu-id="eb2dd-195">The application prints output to the console:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-195">The application prints output to the console:</span></span>

   ![Client application output](media/tutorial-add-device/output.png)

6. <span data-ttu-id="eb2dd-197">After about 30 seconds, you see the telemetry on the device **Measurements** page:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-197">After about 30 seconds, you see the telemetry on the device **Measurements** page:</span></span>

   ![Real telemetry](media/tutorial-add-device/realtelemetry.png)

7. <span data-ttu-id="eb2dd-199">On the **Settings** page, you can see the setting is now synchronized.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-199">On the **Settings** page, you can see the setting is now synchronized.</span></span> <span data-ttu-id="eb2dd-200">When the device first connected, it received the setting value and acknowledged the change:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-200">When the device first connected, it received the setting value and acknowledged the change:</span></span>

   ![Setting synchronized](media/tutorial-add-device/settingsynced.png)

8. <span data-ttu-id="eb2dd-202">On the **Settings** page, set the device temperature to **95** and choose **Update device**.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-202">On the **Settings** page, set the device temperature to **95** and choose **Update device**.</span></span> <span data-ttu-id="eb2dd-203">Your sample application receives and processes this change:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-203">Your sample application receives and processes this change:</span></span>

   ![Receive and process setting](media/tutorial-add-device/receivesetting.png)

   > [!NOTE]
   > <span data-ttu-id="eb2dd-205">There are two "setting update" messages.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-205">There are two "setting update" messages.</span></span> <span data-ttu-id="eb2dd-206">One when the `pending` status is sent and one when the `completed` status is sent.</span><span class="sxs-lookup"><span data-stu-id="eb2dd-206">One when the `pending` status is sent and one when the `completed` status is sent.</span></span>

1. <span data-ttu-id="eb2dd-207">On the **Measurements** page you can see that the device is sending higher temperature values:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-207">On the **Measurements** page you can see that the device is sending higher temperature values:</span></span>

    ![Temperature telemetry is now higher](media/tutorial-add-device/highertemperature.png)

## <a name="next-steps"></a><span data-ttu-id="eb2dd-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb2dd-209">Next steps</span></span>

<span data-ttu-id="eb2dd-210">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-210">In this tutorial, you learned how to:</span></span>

> [!div class="nextstepaction"]
> * <span data-ttu-id="eb2dd-211">Add a new real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-211">Add a new real device</span></span>
> * <span data-ttu-id="eb2dd-212">Configure the new device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-212">Configure the new device</span></span>
> * <span data-ttu-id="eb2dd-213">Get connection string for real device from the application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-213">Get connection string for real device from the application</span></span>
> * <span data-ttu-id="eb2dd-214">Understand how client code maps to the application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-214">Understand how client code maps to the application</span></span>
> * <span data-ttu-id="eb2dd-215">Configure client code for the real device</span><span class="sxs-lookup"><span data-stu-id="eb2dd-215">Configure client code for the real device</span></span>

<span data-ttu-id="eb2dd-216">Now that you have connected a real device to your Azure IoT Central application, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-216">Now that you have connected a real device to your Azure IoT Central application, here are the suggested next steps:</span></span>

<span data-ttu-id="eb2dd-217">As an operator, you can learn how to:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-217">As an operator, you can learn how to:</span></span>

* [<span data-ttu-id="eb2dd-218">Manage your devices</span><span class="sxs-lookup"><span data-stu-id="eb2dd-218">Manage your devices</span></span>](howto-manage-devices.md)
* [<span data-ttu-id="eb2dd-219">Use device sets</span><span class="sxs-lookup"><span data-stu-id="eb2dd-219">Use device sets</span></span>](howto-use-device-sets.md)
* [<span data-ttu-id="eb2dd-220">Create custom analytics</span><span class="sxs-lookup"><span data-stu-id="eb2dd-220">Create custom analytics</span></span>](howto-create-analytics.md)

<span data-ttu-id="eb2dd-221">As a device developer, you can learn how to:</span><span class="sxs-lookup"><span data-stu-id="eb2dd-221">As a device developer, you can learn how to:</span></span>

* [<span data-ttu-id="eb2dd-222">Prepare and connect a DevKit</span><span class="sxs-lookup"><span data-stu-id="eb2dd-222">Prepare and connect a DevKit</span></span>](howto-connect-devkit.md)
* [<span data-ttu-id="eb2dd-223">Prepare and connect a Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="eb2dd-223">Prepare and connect a Raspberry Pi</span></span>](howto-connect-raspberry-pi-python.md)
* [<span data-ttu-id="eb2dd-224">Connect a generic Node.js client to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="eb2dd-224">Connect a generic Node.js client to your Azure IoT Central application</span></span>](howto-connect-nodejs.md)