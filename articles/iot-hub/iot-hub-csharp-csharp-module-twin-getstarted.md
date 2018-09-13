---
title: Get started with Azure IoT Hub module identity and module twin (.NET) | Microsoft Docs
description: Learn how to create module identity and update module twin using IoT SDKs for .NET.
author: chrissie926
ms.service: iot-hub
services: iot-hub
ms.devlang: csharp
ms.topic: conceptual
ms.date: 04/26/2018
ms.author: menchi
ms.openlocfilehash: 7ff867bc29e81e47a4bf66173ce3056792f2f445
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969247"
---
# <a name="get-started-with-iot-hub-module-identity-and-module-twin-using-net-back-end-and-net-device"></a><span data-ttu-id="6647f-103">Get started with IoT Hub module identity and module twin using .NET back end and .NET device</span><span class="sxs-lookup"><span data-stu-id="6647f-103">Get started with IoT Hub module identity and module twin using .NET back end and .NET device</span></span>

> [!NOTE]
> <span data-ttu-id="6647f-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span><span class="sxs-lookup"><span data-stu-id="6647f-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span></span> <span data-ttu-id="6647f-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span><span class="sxs-lookup"><span data-stu-id="6647f-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span></span> <span data-ttu-id="6647f-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span><span class="sxs-lookup"><span data-stu-id="6647f-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span></span>

<span data-ttu-id="6647f-107">At the end of this tutorial, you have two .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="6647f-107">At the end of this tutorial, you have two .NET console apps:</span></span>

* <span data-ttu-id="6647f-108">**CreateIdentities**, which creates a device identity, a module identity and associated security key to connect your device and module clients.</span><span class="sxs-lookup"><span data-stu-id="6647f-108">**CreateIdentities**, which creates a device identity, a module identity and associated security key to connect your device and module clients.</span></span>

* <span data-ttu-id="6647f-109">**UpdateModuleTwinReportedProperties**, which sends updated module twin reported properties to your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6647f-109">**UpdateModuleTwinReportedProperties**, which sends updated module twin reported properties to your IoT Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="6647f-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs](iot-hub-devguide-sdks.md).</span><span class="sxs-lookup"><span data-stu-id="6647f-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs](iot-hub-devguide-sdks.md).</span></span>

<span data-ttu-id="6647f-111">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="6647f-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6647f-112">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6647f-112">Visual Studio 2017.</span></span>

* <span data-ttu-id="6647f-113">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="6647f-113">An active Azure account.</span></span> <span data-ttu-id="6647f-114">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="6647f-114">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="6647f-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6647f-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-create-module-identity-csharp](../../includes/iot-hub-get-started-create-module-identity-csharp.md)]


## <a name="update-the-module-twin-using-net-device-sdk"></a><span data-ttu-id="6647f-116">Update the module twin using .NET device SDK</span><span class="sxs-lookup"><span data-stu-id="6647f-116">Update the module twin using .NET device SDK</span></span>

<span data-ttu-id="6647f-117">In this section, you create a .NET console app on your simulated device that updates the module twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="6647f-117">In this section, you create a .NET console app on your simulated device that updates the module twin reported properties.</span></span>

1. <span data-ttu-id="6647f-118">**Create a Visual Studio project:** In Visual Studio, add a Visual C# Windows Classic Desktop project to the existing solution by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="6647f-118">**Create a Visual Studio project:** In Visual Studio, add a Visual C# Windows Classic Desktop project to the existing solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="6647f-119">Make sure the .NET Framework version is 4.6.1 or later.</span><span class="sxs-lookup"><span data-stu-id="6647f-119">Make sure the .NET Framework version is 4.6.1 or later.</span></span> <span data-ttu-id="6647f-120">Name the project **UpdateModuleTwinReportedProperties**.</span><span class="sxs-lookup"><span data-stu-id="6647f-120">Name the project **UpdateModuleTwinReportedProperties**.</span></span>

    ![Create a visual studio project](./media/iot-hub-csharp-csharp-module-twin-getstarted/update-twins-csharp1.JPG)

2. <span data-ttu-id="6647f-122">**Install the latest Azure IoT Hub .NET device SDK:** Module identity and module twin is in public preview.</span><span class="sxs-lookup"><span data-stu-id="6647f-122">**Install the latest Azure IoT Hub .NET device SDK:** Module identity and module twin is in public preview.</span></span> <span data-ttu-id="6647f-123">It's only availble in the IoT Hub prerelease device SDKs.</span><span class="sxs-lookup"><span data-stu-id="6647f-123">It's only availble in the IoT Hub prerelease device SDKs.</span></span> <span data-ttu-id="6647f-124">In Visual Studio, open tools > Nuget package manager > manage Nuget packages for solution.</span><span class="sxs-lookup"><span data-stu-id="6647f-124">In Visual Studio, open tools > Nuget package manager > manage Nuget packages for solution.</span></span> <span data-ttu-id="6647f-125">Search Microsoft.Azure.Devices.Client.</span><span class="sxs-lookup"><span data-stu-id="6647f-125">Search Microsoft.Azure.Devices.Client.</span></span> <span data-ttu-id="6647f-126">Make sure you've checked include prerelease check box.</span><span class="sxs-lookup"><span data-stu-id="6647f-126">Make sure you've checked include prerelease check box.</span></span> <span data-ttu-id="6647f-127">Select the latest version and install.</span><span class="sxs-lookup"><span data-stu-id="6647f-127">Select the latest version and install.</span></span> <span data-ttu-id="6647f-128">Now you have access to all the module features.</span><span class="sxs-lookup"><span data-stu-id="6647f-128">Now you have access to all the module features.</span></span> 

    ![Install Azure IoT Hub .NET service SDK V1.16.0-preview-005](./media/iot-hub-csharp-csharp-module-twin-getstarted/install-sdk.png)

3. <span data-ttu-id="6647f-130">**Get your module connection string** -- now if you login to [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6647f-130">**Get your module connection string** -- now if you login to [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="6647f-131">Navigate to your IoT Hub and click IoT Devices.</span><span class="sxs-lookup"><span data-stu-id="6647f-131">Navigate to your IoT Hub and click IoT Devices.</span></span> <span data-ttu-id="6647f-132">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span><span class="sxs-lookup"><span data-stu-id="6647f-132">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span></span> <span data-ttu-id="6647f-133">Copy the module connection string.</span><span class="sxs-lookup"><span data-stu-id="6647f-133">Copy the module connection string.</span></span> <span data-ttu-id="6647f-134">It is needed in the next step.</span><span class="sxs-lookup"><span data-stu-id="6647f-134">It is needed in the next step.</span></span>

    ![Azure portal module detail](./media/iot-hub-csharp-csharp-module-twin-getstarted/module-detail.JPG)

4. <span data-ttu-id="6647f-136">**Create UpdateModuleTwinReportedProperties console app**</span><span class="sxs-lookup"><span data-stu-id="6647f-136">**Create UpdateModuleTwinReportedProperties console app**</span></span>

    <span data-ttu-id="6647f-137">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="6647f-137">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    using System.Threading.Tasks;
    using Newtonsoft.Json;
    ```

    <span data-ttu-id="6647f-138">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="6647f-138">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="6647f-139">Replace the placeholder value with the module connection string.</span><span class="sxs-lookup"><span data-stu-id="6647f-139">Replace the placeholder value with the module connection string.</span></span>

    ```csharp
    private const string ModuleConnectionString = 
      "<Your module connection string>";
    private static ModuleClient Client = null;
    static void ConnectionStatusChangeHandler(ConnectionStatus status, 
      ConnectionStatusChangeReason reason)
    {
        Console.WriteLine("Connection Status Changed to {0}; the reason is {1}", 
          status, reason);
    }
    ```

    <span data-ttu-id="6647f-140">Add the following method **OnDesiredPropertyChanged** to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="6647f-140">Add the following method **OnDesiredPropertyChanged** to the **Program** class:</span></span>

    ```csharp
    private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, 
      object userContext)
        {
            Console.WriteLine("desired property change:");
            Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));
            Console.WriteLine("Sending current time as reported property");
            TwinCollection reportedProperties = new TwinCollection
            {
                ["DateTimeLastDesiredPropertyChangeReceived"] = DateTime.Now
            };

            await Client.UpdateReportedPropertiesAsync(reportedProperties).ConfigureAwait(false);
        }
    ```

    <span data-ttu-id="6647f-141">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="6647f-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    static void Main(string[] args)
    {
        Microsoft.Azure.Devices.Client.TransportType transport = 
          Microsoft.Azure.Devices.Client.TransportType.Amqp;

        try
        {
            Client = 
              ModuleClient.CreateFromConnectionString(ModuleConnectionString, transport);
            Client.SetConnectionStatusChangesHandler(ConnectionStatusChangeHandler);
            Client.SetDesiredPropertyUpdateCallbackAsync(OnDesiredPropertyChanged, null).Wait();

            Console.WriteLine("Retrieving twin");
            var twinTask = Client.GetTwinAsync();
            twinTask.Wait();
            var twin = twinTask.Result;
            Console.WriteLine(JsonConvert.SerializeObject(twin.Properties)); 

            Console.WriteLine("Sending app start time as reported property");
            TwinCollection reportedProperties = new TwinCollection();
            reportedProperties["DateTimeLastAppLaunch"] = DateTime.Now;

            Client.UpdateReportedPropertiesAsync(reportedProperties);
        }
        catch (AggregateException ex)
        {
            Console.WriteLine("Error in sample: {0}", ex);
        }

        Console.WriteLine("Waiting for Events.  Press enter to exit...");
        Console.ReadLine();
        Client.CloseAsync().Wait();
    }
    ```

    <span data-ttu-id="6647f-142">This code sample shows you how to retrieve the module twin and update reported properties with AMQP protocol.</span><span class="sxs-lookup"><span data-stu-id="6647f-142">This code sample shows you how to retrieve the module twin and update reported properties with AMQP protocol.</span></span> <span data-ttu-id="6647f-143">In public preview, we only support AMQP for module twin operations.</span><span class="sxs-lookup"><span data-stu-id="6647f-143">In public preview, we only support AMQP for module twin operations.</span></span>

5. <span data-ttu-id="6647f-144">In addition to the above **Main** method, you can add below code block to send event to IoT Hub from your module:</span><span class="sxs-lookup"><span data-stu-id="6647f-144">In addition to the above **Main** method, you can add below code block to send event to IoT Hub from your module:</span></span>

    ```csharp
    Byte[] bytes = new Byte[2];
    bytes[0] = 0;
    bytes[1] = 1;
    var sendEventsTask = Client.SendEventAsync(new Message(bytes));
    sendEventsTask.Wait();
    Console.WriteLine("Event sent to IoT Hub.");
    ```

## <a name="run-the-apps"></a><span data-ttu-id="6647f-145">Run the apps</span><span class="sxs-lookup"><span data-stu-id="6647f-145">Run the apps</span></span>

<span data-ttu-id="6647f-146">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="6647f-146">You are now ready to run the apps.</span></span> <span data-ttu-id="6647f-147">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="6647f-147">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="6647f-148">Select **Multiple startup projects**, and then select **Start** as the action for the console app.</span><span class="sxs-lookup"><span data-stu-id="6647f-148">Select **Multiple startup projects**, and then select **Start** as the action for the console app.</span></span> <span data-ttu-id="6647f-149">And then press F5 to start the app.</span><span class="sxs-lookup"><span data-stu-id="6647f-149">And then press F5 to start the app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6647f-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="6647f-150">Next steps</span></span>

<span data-ttu-id="6647f-151">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="6647f-151">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* [<span data-ttu-id="6647f-152">Getting started with device management</span><span class="sxs-lookup"><span data-stu-id="6647f-152">Getting started with device management</span></span>](iot-hub-node-node-device-management-get-started.md)
* [<span data-ttu-id="6647f-153">Getting started with IoT Edge</span><span class="sxs-lookup"><span data-stu-id="6647f-153">Getting started with IoT Edge</span></span>](../iot-edge/tutorial-simulate-device-linux.md)