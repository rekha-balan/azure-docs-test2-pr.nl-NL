---
title: Get started with Azure IoT Hub device twins (Node) | Microsoft Docs
description: How to use Azure IoT Hub device twins to add tags and then use an IoT Hub query. You use the Azure IoT SDKs for Node.js to implement the simulated device app and a service app that adds the tags and runs the IoT Hub query.
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: ''
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 17e1ec58dcd7066992e4fc2d271db8fc5af58504
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551713"
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="7a7d6-104">Get started with device twins (Node)</span><span class="sxs-lookup"><span data-stu-id="7a7d6-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="7a7d6-105">At the end of this tutorial, you will have two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="7a7d6-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="7a7d6-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="7a7d6-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="7a7d6-109">To complete this tutorial you need the following:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="7a7d6-110">Node.js version 0.10.x or later.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7a7d6-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-111">An active Azure account.</span></span> <span data-ttu-id="7a7d6-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="7a7d6-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="7a7d6-113">Create the service app</span><span class="sxs-lookup"><span data-stu-id="7a7d6-113">Create the service app</span></span>
<span data-ttu-id="7a7d6-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="7a7d6-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reporting a cellular connection.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reporting a cellular connection.</span></span>

1. <span data-ttu-id="7a7d6-116">Create a new empty folder called **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="7a7d6-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="7a7d6-118">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7a7d6-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="7a7d6-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="7a7d6-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="7a7d6-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="7a7d6-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="7a7d6-124">After the updating the tags it calls the **queryTwins** function.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="7a7d6-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="7a7d6-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="7a7d6-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="7a7d6-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="7a7d6-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="7a7d6-130">Run the application with:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="7a7d6-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="7a7d6-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="7a7d6-133">Create the device app</span><span class="sxs-lookup"><span data-stu-id="7a7d6-133">Create the device app</span></span>
<span data-ttu-id="7a7d6-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="7a7d6-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="7a7d6-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="7a7d6-137">Create a new empty folder called **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="7a7d6-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="7a7d6-139">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7a7d6-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7a7d6-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="7a7d6-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="7a7d6-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="7a7d6-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="7a7d6-145">Run the device app</span><span class="sxs-lookup"><span data-stu-id="7a7d6-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="7a7d6-146">You should see the message `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="7a7d6-147">Now that the device reported its connectivity information, it should appear in both queries.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="7a7d6-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="7a7d6-149">This time **myDeviceId** should appear in both query results.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="7a7d6-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a7d6-150">Next steps</span></span>
<span data-ttu-id="7a7d6-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="7a7d6-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="7a7d6-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="7a7d6-154">Use the following resources to learn how to:</span><span class="sxs-lookup"><span data-stu-id="7a7d6-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="7a7d6-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="7a7d6-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="7a7d6-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="7a7d6-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="7a7d6-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a7d6-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-twin-getstarted/service1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md


