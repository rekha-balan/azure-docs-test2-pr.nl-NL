---
title: Get started with Azure IoT Hub device twins (.NET/.NET) | Microsoft Docs
description: How to use Azure IoT Hub device twins to add tags and then use an IoT Hub query. You use the Azure IoT device SDK for .NET to implement the simulated device app and the Azure IoT service SDK for .NET to implement a service app that adds the tags and runs the IoT Hub query.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: csharp
ms.topic: conceptual
ms.date: 05/15/2017
ms.author: dobett
ms.openlocfilehash: 340453448d38db66558e59edb845f2caf4454cf9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869880"
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="4b684-104">Get started with device twins (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="4b684-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="4b684-105">At the end of this tutorial, you will have these .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="4b684-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="4b684-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="4b684-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>

* <span data-ttu-id="4b684-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span><span class="sxs-lookup"><span data-stu-id="4b684-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>

* <span data-ttu-id="4b684-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span><span class="sxs-lookup"><span data-stu-id="4b684-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="4b684-109">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="4b684-109">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 

<span data-ttu-id="4b684-110">To complete this tutorial you need the following:</span><span class="sxs-lookup"><span data-stu-id="4b684-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="4b684-111">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4b684-111">Visual Studio 2017.</span></span>
* <span data-ttu-id="4b684-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="4b684-112">An active Azure account.</span></span> <span data-ttu-id="4b684-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="4b684-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="4b684-114">Create the service app</span><span class="sxs-lookup"><span data-stu-id="4b684-114">Create the service app</span></span>

<span data-ttu-id="4b684-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="4b684-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="4b684-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span><span class="sxs-lookup"><span data-stu-id="4b684-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="4b684-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="4b684-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="4b684-118">Name the project **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="4b684-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![New Visual C# Windows Classic Desktop project](./media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png)

2. <span data-ttu-id="4b684-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="4b684-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>

3. <span data-ttu-id="4b684-121">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices**.</span><span class="sxs-lookup"><span data-stu-id="4b684-121">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices**.</span></span> <span data-ttu-id="4b684-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="4b684-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="4b684-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="4b684-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices/) NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window](./media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png)

4. <span data-ttu-id="4b684-125">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="4b684-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp  
    using Microsoft.Azure.Devices;
    ```

5. <span data-ttu-id="4b684-126">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="4b684-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="4b684-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="4b684-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp  
    static RegistryManager registryManager;
    static string connectionString = "{iot hub connection string}";
    ```

6. <span data-ttu-id="4b684-128">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="4b684-128">Add the following method to the **Program** class:</span></span>

    ```csharp  
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
   
        var query = registryManager.CreateQuery(
          "SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
        var twinsInRedmond43 = await query.GetNextAsTwinAsync();
        Console.WriteLine("Devices in Redmond43: {0}", 
          string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
        query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
        var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
        Console.WriteLine("Devices in Redmond43 using cellular network: {0}", 
          string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
    }
    ```
   
    <span data-ttu-id="4b684-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span><span class="sxs-lookup"><span data-stu-id="4b684-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="4b684-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span><span class="sxs-lookup"><span data-stu-id="4b684-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="4b684-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span><span class="sxs-lookup"><span data-stu-id="4b684-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="4b684-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span><span class="sxs-lookup"><span data-stu-id="4b684-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="4b684-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span><span class="sxs-lookup"><span data-stu-id="4b684-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="4b684-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span><span class="sxs-lookup"><span data-stu-id="4b684-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>

7. <span data-ttu-id="4b684-135">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="4b684-135">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp  
    registryManager = RegistryManager.CreateFromConnectionString(connectionString);
    AddTagsAndQuery().Wait();
    Console.WriteLine("Press Enter to exit.");
    Console.ReadLine();
    ```

8. <span data-ttu-id="4b684-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span><span class="sxs-lookup"><span data-stu-id="4b684-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="4b684-137">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="4b684-137">Build the solution.</span></span>

9. <span data-ttu-id="4b684-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="4b684-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="4b684-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span><span class="sxs-lookup"><span data-stu-id="4b684-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Query results in window](./media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png)

<span data-ttu-id="4b684-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span><span class="sxs-lookup"><span data-stu-id="4b684-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="4b684-142">Create the device app</span><span class="sxs-lookup"><span data-stu-id="4b684-142">Create the device app</span></span>

<span data-ttu-id="4b684-143">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span><span class="sxs-lookup"><span data-stu-id="4b684-143">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="4b684-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="4b684-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="4b684-145">Name the project **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="4b684-145">Name the project **ReportConnectivity**.</span></span>
   
    ![New Visual C# Windows Classic device app](./media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png)
    
2. <span data-ttu-id="4b684-147">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="4b684-147">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>

3. <span data-ttu-id="4b684-148">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices.Client**.</span><span class="sxs-lookup"><span data-stu-id="4b684-148">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices.Client**.</span></span> <span data-ttu-id="4b684-149">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="4b684-149">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="4b684-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="4b684-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window Client app](./media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png)

4. <span data-ttu-id="4b684-152">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="4b684-152">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp  
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="4b684-153">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="4b684-153">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="4b684-154">Replace the placeholder value with the device connection string that you noted in the previous section.</span><span class="sxs-lookup"><span data-stu-id="4b684-154">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>

    ```csharp  
    static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;
      DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
    static DeviceClient Client = null;
    ```

6. <span data-ttu-id="4b684-155">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="4b684-155">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async void InitClient()
    {
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, 
              TransportType.Mqtt);
            Console.WriteLine("Retrieving twin");
            await Client.GetTwinAsync();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
    }
    ```

    <span data-ttu-id="4b684-156">The **Client** object exposes all the methods you require to interact with device twins from the device.</span><span class="sxs-lookup"><span data-stu-id="4b684-156">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="4b684-157">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="4b684-157">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

7. <span data-ttu-id="4b684-158">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="4b684-158">Add the following method to the **Program** class:</span></span>

    ```csharp  
    public static async void ReportConnectivity()
    {
        try
        {
            Console.WriteLine("Sending connectivity data as reported property");
            
            TwinCollection reportedProperties, connectivity;
            reportedProperties = new TwinCollection();
            connectivity = new TwinCollection();
            connectivity["type"] = "cellular";
            reportedProperties["connectivity"] = connectivity;
            await Client.UpdateReportedPropertiesAsync(reportedProperties);
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
    }
    ```

   <span data-ttu-id="4b684-159">The code above updates **myDeviceId**'s reported property with the connectivity information.</span><span class="sxs-lookup"><span data-stu-id="4b684-159">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

8. <span data-ttu-id="4b684-160">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="4b684-160">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    try
    {
        InitClient();
        ReportConnectivity();
    }
    catch (Exception ex)
    {
        Console.WriteLine();
        Console.WriteLine("Error in sample: {0}", ex.Message);
    }
    Console.WriteLine("Press Enter to exit.");
    Console.ReadLine();
    ```

9. <span data-ttu-id="4b684-161">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span><span class="sxs-lookup"><span data-stu-id="4b684-161">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="4b684-162">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="4b684-162">Build the solution.</span></span>

10. <span data-ttu-id="4b684-163">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="4b684-163">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="4b684-164">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span><span class="sxs-lookup"><span data-stu-id="4b684-164">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Run device app to report connectivity](./media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png)
       
11. <span data-ttu-id="4b684-166">Now that the device reported its connectivity information, it should appear in both queries.</span><span class="sxs-lookup"><span data-stu-id="4b684-166">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="4b684-167">Run the .NET **AddTagsAndQuery** app to run the queries again.</span><span class="sxs-lookup"><span data-stu-id="4b684-167">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="4b684-168">This time **myDeviceId** should appear in both query results.</span><span class="sxs-lookup"><span data-stu-id="4b684-168">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Device connectivity reported successfully](./media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png)

## <a name="next-steps"></a><span data-ttu-id="4b684-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b684-170">Next steps</span></span>

<span data-ttu-id="4b684-171">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="4b684-171">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="4b684-172">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span><span class="sxs-lookup"><span data-stu-id="4b684-172">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="4b684-173">You also learned how to query this information using the SQL-like IoT Hub query language.</span><span class="sxs-lookup"><span data-stu-id="4b684-173">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="4b684-174">Use the following resources to learn how to:</span><span class="sxs-lookup"><span data-stu-id="4b684-174">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="4b684-175">send telemetry from devices with the [Send telemetry from a device to an IoT hub](quickstart-send-telemetry-dotnet.md) tutorial,</span><span class="sxs-lookup"><span data-stu-id="4b684-175">send telemetry from devices with the [Send telemetry from a device to an IoT hub](quickstart-send-telemetry-dotnet.md) tutorial,</span></span>

* <span data-ttu-id="4b684-176">configure devices using device twin's desired properties with the [Use desired properties to configure devices](tutorial-device-twins.md) tutorial,</span><span class="sxs-lookup"><span data-stu-id="4b684-176">configure devices using device twin's desired properties with the [Use desired properties to configure devices](tutorial-device-twins.md) tutorial,</span></span>

* <span data-ttu-id="4b684-177">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](quickstart-control-device-node.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4b684-177">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](quickstart-control-device-node.md) tutorial.</span></span>
