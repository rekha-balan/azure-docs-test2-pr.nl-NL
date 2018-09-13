---
title: Get started with Azure IoT Hub (.NET) | Microsoft Docs
description: How to send device-to-cloud messages from a device to an Azure IoT hub using the Azure IoT SDKs for .NET. You create a simulated device app to send messages, a service app to register your device in the identity registry, and a service app to read the device-to-cloud messages from the IoT hub.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7c08fcb4b60b0244276e3e0a1bfbc91d1b81214c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554216"
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-net"></a><span data-ttu-id="c57ea-104">Connect your simulated device to your IoT hub using .NET</span><span class="sxs-lookup"><span data-stu-id="c57ea-104">Connect your simulated device to your IoT hub using .NET</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="c57ea-105">At the end of this tutorial, you have three .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="c57ea-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="c57ea-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="c57ea-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="c57ea-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="c57ea-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="c57ea-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="c57ea-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="c57ea-109">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="c57ea-109">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>
> 
> 

<span data-ttu-id="c57ea-110">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="c57ea-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c57ea-111">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c57ea-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c57ea-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="c57ea-112">An active Azure account.</span></span> <span data-ttu-id="c57ea-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="c57ea-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="c57ea-114">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c57ea-114">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="c57ea-115">Create a device identity</span><span class="sxs-lookup"><span data-stu-id="c57ea-115">Create a device identity</span></span>
<span data-ttu-id="c57ea-116">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-116">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="c57ea-117">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="c57ea-117">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="c57ea-118">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="c57ea-118">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="c57ea-119">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-119">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="c57ea-120">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="c57ea-120">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c57ea-121">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="c57ea-121">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c57ea-122">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-122">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![New Visual C# Windows Classic Desktop project][10]
2. <span data-ttu-id="c57ea-124">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-124">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="c57ea-125">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="c57ea-125">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="c57ea-126">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="c57ea-126">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window][11]
4. <span data-ttu-id="c57ea-128">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="c57ea-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="c57ea-129">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="c57ea-129">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c57ea-130">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c57ea-130">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="c57ea-131">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="c57ea-131">Add the following method to the **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="c57ea-132">This method creates a device identity with ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-132">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="c57ea-133">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span><span class="sxs-lookup"><span data-stu-id="c57ea-133">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="c57ea-134">You use this key in the simulated device app to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-134">You use this key in the simulated device app to connect to your IoT hub.</span></span>
7. <span data-ttu-id="c57ea-135">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="c57ea-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="c57ea-136">Run this application, and make a note of the device key.</span><span class="sxs-lookup"><span data-stu-id="c57ea-136">Run this application, and make a note of the device key.</span></span>
   
    ![Device key generated by the application][12]

> [!NOTE]
> <span data-ttu-id="c57ea-138">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-138">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="c57ea-139">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span><span class="sxs-lookup"><span data-stu-id="c57ea-139">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="c57ea-140">If your application needs to store other device-specific metadata, it should use an application-specific store.</span><span class="sxs-lookup"><span data-stu-id="c57ea-140">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="c57ea-141">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="c57ea-141">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="c57ea-142">Receive device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="c57ea-142">Receive device-to-cloud messages</span></span>
<span data-ttu-id="c57ea-143">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-143">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="c57ea-144">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="c57ea-144">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="c57ea-145">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span><span class="sxs-lookup"><span data-stu-id="c57ea-145">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="c57ea-146">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c57ea-146">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="c57ea-147">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c57ea-147">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="c57ea-148">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span><span class="sxs-lookup"><span data-stu-id="c57ea-148">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="c57ea-149">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span><span class="sxs-lookup"><span data-stu-id="c57ea-149">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="c57ea-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="c57ea-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c57ea-151">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="c57ea-151">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c57ea-152">Name the project **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-152">Name the project **ReadDeviceToCloudMessages**.</span></span>
   
    ![New Visual C# Windows Classic Desktop project][10a]
2. <span data-ttu-id="c57ea-154">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-154">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="c57ea-155">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="c57ea-155">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="c57ea-156">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span><span class="sxs-lookup"><span data-stu-id="c57ea-156">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="c57ea-157">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-157">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>
4. <span data-ttu-id="c57ea-158">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="c57ea-158">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.ServiceBus.Messaging;
        using System.Threading;
5. <span data-ttu-id="c57ea-159">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="c57ea-159">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c57ea-160">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span><span class="sxs-lookup"><span data-stu-id="c57ea-160">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>
   
        static string connectionString = "{iothub connection string}";
        static string iotHubD2cEndpoint = "messages/events";
        static EventHubClient eventHubClient;
6. <span data-ttu-id="c57ea-161">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="c57ea-161">Add the following method to the **Program** class:</span></span>
   
        private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
        {
            var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
            while (true)
            {
                if (ct.IsCancellationRequested) break;
                EventData eventData = await eventHubReceiver.ReceiveAsync();
                if (eventData == null) continue;
   
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
   
    <span data-ttu-id="c57ea-162">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span><span class="sxs-lookup"><span data-stu-id="c57ea-162">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="c57ea-163">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span><span class="sxs-lookup"><span data-stu-id="c57ea-163">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="c57ea-164">This filter is useful in a test environment so you can see the current set of messages.</span><span class="sxs-lookup"><span data-stu-id="c57ea-164">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="c57ea-165">In a production environment, your code should make sure that it processes all the messages.</span><span class="sxs-lookup"><span data-stu-id="c57ea-165">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="c57ea-166">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c57ea-166">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
7. <span data-ttu-id="c57ea-167">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="c57ea-167">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);
   
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
   
        CancellationTokenSource cts = new CancellationTokenSource();
   
        System.Console.CancelKeyPress += (s, e) =>
        {
          e.Cancel = true;
          cts.Cancel();
          Console.WriteLine("Exiting...");
        };
   
        var tasks = new List<Task>();
        foreach (string partition in d2cPartitions)
        {
           tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }  
        Task.WaitAll(tasks.ToArray());

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c57ea-168">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="c57ea-168">Create a simulated device app</span></span>
<span data-ttu-id="c57ea-169">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-169">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="c57ea-170">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="c57ea-170">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c57ea-171">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="c57ea-171">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c57ea-172">Name the project **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-172">Name the project **SimulatedDevice**.</span></span>
   
    ![New Visual C# Windows Classic Desktop project][10b]
2. <span data-ttu-id="c57ea-174">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-174">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="c57ea-175">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="c57ea-175">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="c57ea-176">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="c57ea-176">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>
4. <span data-ttu-id="c57ea-177">Add the following `using` statement at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="c57ea-177">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Newtonsoft.Json;
5. <span data-ttu-id="c57ea-178">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="c57ea-178">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c57ea-179">Substitute the placeholder values with the IoT hub host name you retrieved in the "Create an IoT hub" section, and the device key retrieved in the "Create a device identity" section.</span><span class="sxs-lookup"><span data-stu-id="c57ea-179">Substitute the placeholder values with the IoT hub host name you retrieved in the "Create an IoT hub" section, and the device key retrieved in the "Create a device identity" section.</span></span>
   
        static DeviceClient deviceClient;
        static string iotHubUri = "{iot hub hostname}";
        static string deviceKey = "{device key}";
6. <span data-ttu-id="c57ea-180">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="c57ea-180">Add the following method to the **Program** class:</span></span>
   
        private static async void SendDeviceToCloudMessagesAsync()
        {
            double minTemperature = 20;
            double minHumidity = 60;
            Random rand = new Random();
   
            while (true)
            {
                double currentTemperature = minTemperature + rand.NextDouble() * 15;
                double currentHumidity = minHumidity + rand.NextDouble() * 20;
   
                var telemetryDataPoint = new
                {
                    deviceId = "myFirstDevice",
                    temperature = currentTemperature,
                    humidity = currentHumidity
                };
                var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
                var message = new Message(Encoding.ASCII.GetBytes(messageString));
                message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
   
                await deviceClient.SendEventAsync(message);
                Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);
   
                await Task.Delay(1000);
            }
        }
   
    <span data-ttu-id="c57ea-181">This method sends a new device-to-cloud message every second.</span><span class="sxs-lookup"><span data-stu-id="c57ea-181">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="c57ea-182">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="c57ea-182">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>
7. <span data-ttu-id="c57ea-183">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="c57ea-183">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Simulated device\n");
        deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey), TransportType.Mqtt);
   
        SendDeviceToCloudMessagesAsync();
        Console.ReadLine();
   
   <span data-ttu-id="c57ea-184">By default, the **Create** method creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-184">By default, the **Create** method creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="c57ea-185">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span><span class="sxs-lookup"><span data-stu-id="c57ea-185">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="c57ea-186">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span><span class="sxs-lookup"><span data-stu-id="c57ea-186">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="c57ea-187">This tutorial takes you through the steps to create an IoT Hub simulated device app.</span><span class="sxs-lookup"><span data-stu-id="c57ea-187">This tutorial takes you through the steps to create an IoT Hub simulated device app.</span></span> <span data-ttu-id="c57ea-188">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span><span class="sxs-lookup"><span data-stu-id="c57ea-188">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="c57ea-189">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="c57ea-189">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c57ea-190">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="c57ea-190">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="c57ea-191">Run the apps</span><span class="sxs-lookup"><span data-stu-id="c57ea-191">Run the apps</span></span>
<span data-ttu-id="c57ea-192">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="c57ea-192">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="c57ea-193">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="c57ea-193">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="c57ea-194">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span><span class="sxs-lookup"><span data-stu-id="c57ea-194">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>
   
    ![Startup project properties][41]
2. <span data-ttu-id="c57ea-196">Press **F5** to start both apps running.</span><span class="sxs-lookup"><span data-stu-id="c57ea-196">Press **F5** to start both apps running.</span></span> <span data-ttu-id="c57ea-197">The console output from the **SimulatedDevice** app shows the messages your simulated device app sends to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-197">The console output from the **SimulatedDevice** app shows the messages your simulated device app sends to your IoT hub.</span></span> <span data-ttu-id="c57ea-198">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span><span class="sxs-lookup"><span data-stu-id="c57ea-198">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>
   
    ![Console output from apps][42]
3. <span data-ttu-id="c57ea-200">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span><span class="sxs-lookup"><span data-stu-id="c57ea-200">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![Azure portal Usage tile][43]

## <a name="next-steps"></a><span data-ttu-id="c57ea-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="c57ea-202">Next steps</span></span>
<span data-ttu-id="c57ea-203">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="c57ea-203">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="c57ea-204">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-204">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="c57ea-205">You also created an app that displays the messages received by the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c57ea-205">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="c57ea-206">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="c57ea-206">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="c57ea-207">[Connecting your device][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="c57ea-207">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="c57ea-208">[Getting started with device management][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="c57ea-208">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="c57ea-209">[Getting started with the IoT Gateway SDK][lnk-gateway-SDK]</span><span class="sxs-lookup"><span data-stu-id="c57ea-209">[Getting started with the IoT Gateway SDK][lnk-gateway-SDK]</span></span>

<span data-ttu-id="c57ea-210">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c57ea-210">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

<!-- Images. -->
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/usage.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/create-identity-csharp1.png
[10a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/create-identity-csharp2.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/create-identity-csharp3.png

<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/








