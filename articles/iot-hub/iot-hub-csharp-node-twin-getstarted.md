---
title: Get started with Azure IoT Hub device twins (.NET/Node) | Microsoft Docs
description: How to use Azure IoT Hub device twins to add tags and then use an IoT Hub query. You use the Azure IoT device SDK for Node.js to implement the simulated device app and the Azure IoT service SDK for .NET to implement a service app that adds the tags and runs the IoT Hub query.
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: ''
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: df9001a9b8d307640c401b809904ac99c045982e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548932"
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="294c0-104">Get started with device twins (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="294c0-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="294c0-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span><span class="sxs-lookup"><span data-stu-id="294c0-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="294c0-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span><span class="sxs-lookup"><span data-stu-id="294c0-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="294c0-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span><span class="sxs-lookup"><span data-stu-id="294c0-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="294c0-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="294c0-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="294c0-109">To complete this tutorial you need the following:</span><span class="sxs-lookup"><span data-stu-id="294c0-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="294c0-110">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="294c0-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="294c0-111">Node.js version 0.10.x or later.</span><span class="sxs-lookup"><span data-stu-id="294c0-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="294c0-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="294c0-112">An active Azure account.</span></span> <span data-ttu-id="294c0-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="294c0-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="294c0-114">Create the service app</span><span class="sxs-lookup"><span data-stu-id="294c0-114">Create the service app</span></span>
<span data-ttu-id="294c0-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="294c0-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="294c0-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span><span class="sxs-lookup"><span data-stu-id="294c0-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="294c0-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="294c0-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="294c0-118">Name the project **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="294c0-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![New Visual C# Windows Classic Desktop project][img-createapp]
1. <span data-ttu-id="294c0-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="294c0-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="294c0-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="294c0-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="294c0-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="294c0-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="294c0-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="294c0-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window][img-servicenuget]
1. <span data-ttu-id="294c0-125">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="294c0-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="294c0-126">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="294c0-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="294c0-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="294c0-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="294c0-128">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="294c0-128">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="294c0-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span><span class="sxs-lookup"><span data-stu-id="294c0-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="294c0-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span><span class="sxs-lookup"><span data-stu-id="294c0-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="294c0-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span><span class="sxs-lookup"><span data-stu-id="294c0-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="294c0-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span><span class="sxs-lookup"><span data-stu-id="294c0-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="294c0-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span><span class="sxs-lookup"><span data-stu-id="294c0-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="294c0-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span><span class="sxs-lookup"><span data-stu-id="294c0-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="294c0-135">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="294c0-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="294c0-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span><span class="sxs-lookup"><span data-stu-id="294c0-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="294c0-137">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="294c0-137">Build the solution.</span></span>
1. <span data-ttu-id="294c0-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="294c0-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="294c0-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span><span class="sxs-lookup"><span data-stu-id="294c0-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Query results in window][img-addtagapp]

<span data-ttu-id="294c0-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span><span class="sxs-lookup"><span data-stu-id="294c0-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="294c0-142">Create the device app</span><span class="sxs-lookup"><span data-stu-id="294c0-142">Create the device app</span></span>
<span data-ttu-id="294c0-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span><span class="sxs-lookup"><span data-stu-id="294c0-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="294c0-144">Create a new empty folder called **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="294c0-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="294c0-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="294c0-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="294c0-146">Accept all the defaults.</span><span class="sxs-lookup"><span data-stu-id="294c0-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="294c0-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="294c0-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="294c0-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span><span class="sxs-lookup"><span data-stu-id="294c0-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="294c0-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span><span class="sxs-lookup"><span data-stu-id="294c0-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="294c0-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span><span class="sxs-lookup"><span data-stu-id="294c0-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="294c0-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span><span class="sxs-lookup"><span data-stu-id="294c0-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="294c0-152">Run the device app</span><span class="sxs-lookup"><span data-stu-id="294c0-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="294c0-153">You should see the message `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="294c0-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="294c0-154">Now that the device reported its connectivity information, it should appear in both queries.</span><span class="sxs-lookup"><span data-stu-id="294c0-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="294c0-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span><span class="sxs-lookup"><span data-stu-id="294c0-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="294c0-156">This time **myDeviceId** should appear in both query results.</span><span class="sxs-lookup"><span data-stu-id="294c0-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="294c0-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="294c0-157">Next steps</span></span>
<span data-ttu-id="294c0-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="294c0-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="294c0-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span><span class="sxs-lookup"><span data-stu-id="294c0-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="294c0-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span><span class="sxs-lookup"><span data-stu-id="294c0-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="294c0-161">Use the following resources to learn how to:</span><span class="sxs-lookup"><span data-stu-id="294c0-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="294c0-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="294c0-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="294c0-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="294c0-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="294c0-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="294c0-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md





