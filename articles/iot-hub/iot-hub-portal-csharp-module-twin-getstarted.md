---
title: Get started with Azure IoT Hub module identity and module twin (portal and .NET) | Microsoft Docs
description: Learn how to create module identity and update module twin using the portal and .NET.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: csharp
ms.topic: conceptual
ms.date: 04/26/2018
ms.author: dobett
ms.openlocfilehash: 3de08d9e4a45b842fc921436f855831afb6b9ce0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866258"
---
# <a name="get-started-with-iot-hub-module-identity-and-module-twin-using-the-portal-and-net-device"></a><span data-ttu-id="325f2-103">Get started with IoT Hub module identity and module twin using the portal and .NET device</span><span class="sxs-lookup"><span data-stu-id="325f2-103">Get started with IoT Hub module identity and module twin using the portal and .NET device</span></span>

> [!NOTE]
> <span data-ttu-id="325f2-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span><span class="sxs-lookup"><span data-stu-id="325f2-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span></span> <span data-ttu-id="325f2-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span><span class="sxs-lookup"><span data-stu-id="325f2-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span></span> <span data-ttu-id="325f2-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span><span class="sxs-lookup"><span data-stu-id="325f2-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span></span>

<span data-ttu-id="325f2-107">In this tutorial, you will learn</span><span class="sxs-lookup"><span data-stu-id="325f2-107">In this tutorial, you will learn</span></span> 
1. <span data-ttu-id="325f2-108">how to create a module identity in the portal.</span><span class="sxs-lookup"><span data-stu-id="325f2-108">how to create a module identity in the portal.</span></span> 
2. <span data-ttu-id="325f2-109">how to use .NET device SDK update the module twin from your device.</span><span class="sxs-lookup"><span data-stu-id="325f2-109">how to use .NET device SDK update the module twin from your device.</span></span>

> [!NOTE]
> <span data-ttu-id="325f2-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="325f2-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="325f2-111">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="325f2-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="325f2-112">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="325f2-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="325f2-113">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="325f2-113">An active Azure account.</span></span> <span data-ttu-id="325f2-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="325f2-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

## <a name="create-a-device-identity-in-the-portal"></a><span data-ttu-id="325f2-115">Create a device identity in the portal</span><span class="sxs-lookup"><span data-stu-id="325f2-115">Create a device identity in the portal</span></span>

<span data-ttu-id="325f2-116">Now you have your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="325f2-116">Now you have your IoT Hub.</span></span> <span data-ttu-id="325f2-117">Open [portal](https://portal.azure.com) and navigate to your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="325f2-117">Open [portal](https://portal.azure.com) and navigate to your IoT Hub.</span></span> <span data-ttu-id="325f2-118">Click on IoT Devices, and then click add to create a device identity.</span><span class="sxs-lookup"><span data-stu-id="325f2-118">Click on IoT Devices, and then click add to create a device identity.</span></span> <span data-ttu-id="325f2-119">Name it **MyFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="325f2-119">Name it **MyFirstDevice**.</span></span> 

![Create device identity][8]

<span data-ttu-id="325f2-121">After save, in your device identity list, you can see MyFirstDevice identity is successfuly created.</span><span class="sxs-lookup"><span data-stu-id="325f2-121">After save, in your device identity list, you can see MyFirstDevice identity is successfuly created.</span></span>

![Device id created][11]

<span data-ttu-id="325f2-123">Now click on the row.</span><span class="sxs-lookup"><span data-stu-id="325f2-123">Now click on the row.</span></span> <span data-ttu-id="325f2-124">You will see device details.</span><span class="sxs-lookup"><span data-stu-id="325f2-124">You will see device details.</span></span>

![Device details][10]

## <a name="create-a-module-identity-in-the-portal"></a><span data-ttu-id="325f2-126">Create a module identity in the portal</span><span class="sxs-lookup"><span data-stu-id="325f2-126">Create a module identity in the portal</span></span>

<span data-ttu-id="325f2-127">Within one device identity, you can create up to 20 module identities.</span><span class="sxs-lookup"><span data-stu-id="325f2-127">Within one device identity, you can create up to 20 module identities.</span></span> <span data-ttu-id="325f2-128">Click the **Add Module Identity** button on top to create your first module identity called **myFirstModule**.</span><span class="sxs-lookup"><span data-stu-id="325f2-128">Click the **Add Module Identity** button on top to create your first module identity called **myFirstModule**.</span></span> 

![Device details][9]

<span data-ttu-id="325f2-130">Save and click the just created module identity.</span><span class="sxs-lookup"><span data-stu-id="325f2-130">Save and click the just created module identity.</span></span> <span data-ttu-id="325f2-131">You can see the module identity details.</span><span class="sxs-lookup"><span data-stu-id="325f2-131">You can see the module identity details.</span></span> <span data-ttu-id="325f2-132">Save the connect string - primary key.</span><span class="sxs-lookup"><span data-stu-id="325f2-132">Save the connect string - primary key.</span></span> <span data-ttu-id="325f2-133">It will be used in the next section where you set up your module on the device.</span><span class="sxs-lookup"><span data-stu-id="325f2-133">It will be used in the next section where you set up your module on the device.</span></span>

![Device details][12]

## <a name="update-the-module-twin-using-net-device-sdk"></a><span data-ttu-id="325f2-135">Update the module twin using .NET device SDK</span><span class="sxs-lookup"><span data-stu-id="325f2-135">Update the module twin using .NET device SDK</span></span>

<span data-ttu-id="325f2-136">You've successfully created the module identity in your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="325f2-136">You've successfully created the module identity in your IoT Hub.</span></span> <span data-ttu-id="325f2-137">Let's try to communicate to the cloud from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="325f2-137">Let's try to communicate to the cloud from your simulated device.</span></span> <span data-ttu-id="325f2-138">Once a module identity is created, a module twin is implicitly created in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="325f2-138">Once a module identity is created, a module twin is implicitly created in IoT Hub.</span></span> <span data-ttu-id="325f2-139">In this section, you will create a .NET console app on your simulated device that updates the module twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="325f2-139">In this section, you will create a .NET console app on your simulated device that updates the module twin reported properties.</span></span>

1. <span data-ttu-id="325f2-140">**Create a Visual Studio project** - In Visual Studio, add a Visual C# Windows Classic Desktop project to the existing solution by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="325f2-140">**Create a Visual Studio project** - In Visual Studio, add a Visual C# Windows Classic Desktop project to the existing solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="325f2-141">Make sure the .NET Framework version is 4.6.1 or later.</span><span class="sxs-lookup"><span data-stu-id="325f2-141">Make sure the .NET Framework version is 4.6.1 or later.</span></span> <span data-ttu-id="325f2-142">Name the project **UpdateModuleTwinReportedProperties**.</span><span class="sxs-lookup"><span data-stu-id="325f2-142">Name the project **UpdateModuleTwinReportedProperties**.</span></span>

    ![Create a visual studio project][13]

2. <span data-ttu-id="325f2-144">**Install the latest Azure IoT Hub .NET device SDK** - Module identity and module twin is in public preview.</span><span class="sxs-lookup"><span data-stu-id="325f2-144">**Install the latest Azure IoT Hub .NET device SDK** - Module identity and module twin is in public preview.</span></span> <span data-ttu-id="325f2-145">It's only availble in the IoT Hub prerelease device SDKs.</span><span class="sxs-lookup"><span data-stu-id="325f2-145">It's only availble in the IoT Hub prerelease device SDKs.</span></span> <span data-ttu-id="325f2-146">In Visual Studio, open tools > Nuget package manager > manage Nuget packages for solution.</span><span class="sxs-lookup"><span data-stu-id="325f2-146">In Visual Studio, open tools > Nuget package manager > manage Nuget packages for solution.</span></span> <span data-ttu-id="325f2-147">Search Microsoft.Azure.Devices.Client.</span><span class="sxs-lookup"><span data-stu-id="325f2-147">Search Microsoft.Azure.Devices.Client.</span></span> <span data-ttu-id="325f2-148">Make sure you've checked include prerelease check box.</span><span class="sxs-lookup"><span data-stu-id="325f2-148">Make sure you've checked include prerelease check box.</span></span> <span data-ttu-id="325f2-149">Select the latest version and install.</span><span class="sxs-lookup"><span data-stu-id="325f2-149">Select the latest version and install.</span></span> <span data-ttu-id="325f2-150">Now you have access to all the module features.</span><span class="sxs-lookup"><span data-stu-id="325f2-150">Now you have access to all the module features.</span></span> 

    ![Install Azure IoT Hub .NET service SDK V1.16.0-preview-005][14]

3. <span data-ttu-id="325f2-152">**Get your module connection string** -- now if you login to [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="325f2-152">**Get your module connection string** -- now if you login to [Azure portal][lnk-portal].</span></span> <span data-ttu-id="325f2-153">Navigate to your IoT Hub and click IoT Devices.</span><span class="sxs-lookup"><span data-stu-id="325f2-153">Navigate to your IoT Hub and click IoT Devices.</span></span> <span data-ttu-id="325f2-154">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span><span class="sxs-lookup"><span data-stu-id="325f2-154">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span></span> <span data-ttu-id="325f2-155">Copy the module connection string.</span><span class="sxs-lookup"><span data-stu-id="325f2-155">Copy the module connection string.</span></span> <span data-ttu-id="325f2-156">It is needed in the next step.</span><span class="sxs-lookup"><span data-stu-id="325f2-156">It is needed in the next step.</span></span>

    ![Azure portal module detail][15]

4. <span data-ttu-id="325f2-158">**Create UpdateModuleTwinReportedProperties console app** Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="325f2-158">**Create UpdateModuleTwinReportedProperties console app** Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    ```

    <span data-ttu-id="325f2-159">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="325f2-159">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="325f2-160">Replace the placeholder value with the module connection string.</span><span class="sxs-lookup"><span data-stu-id="325f2-160">Replace the placeholder value with the module connection string.</span></span>

    ```csharp
    private const string ModuleConnectionString = "<Your module connection string>";
    private static ModuleClient Client = null;
    ```

    <span data-ttu-id="325f2-161">Add the following method **OnDesiredPropertyChanged** to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="325f2-161">Add the following method **OnDesiredPropertyChanged** to the **Program** class:</span></span>

    ```csharp
    private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
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

    <span data-ttu-id="325f2-162">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="325f2-162">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    static void Main(string[] args)
    {
        Microsoft.Azure.Devices.Client.TransportType transport = Microsoft.Azure.Devices.Client.TransportType.Amqp;

        try
        {
            Client = ModuleClient.CreateFromConnectionString(ModuleConnectionString, transport);
            Client.SetConnectionStatusChangesHandler(ConnectionStatusChangeHandler);
            Client.SetDesiredPropertyUpdateCallbackAsync(OnDesiredPropertyChanged, null).Wait();

            Console.WriteLine("Retrieving twin");
            var twinTask = Client.GetTwinAsync();
            twinTask.Wait();
            var twin = twinTask.Result;
            Console.WriteLine(JsonConvert.SerializeObject(twin));

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
        Console.ReadKey();
        Client.CloseAsync().Wait();
    }
    
    private static void ConnectionStatusChangeHandler(ConnectionStatus status, ConnectionStatusChangeReason reason)
    {
        Console.WriteLine($"Status {status} changed: {reason}");
    }
    ```

    <span data-ttu-id="325f2-163">This code sample shows you how to retrieve the module twin and update reported properties with AMQP protocol.</span><span class="sxs-lookup"><span data-stu-id="325f2-163">This code sample shows you how to retrieve the module twin and update reported properties with AMQP protocol.</span></span> <span data-ttu-id="325f2-164">In public preview, we only support AMQP for module twin operations.</span><span class="sxs-lookup"><span data-stu-id="325f2-164">In public preview, we only support AMQP for module twin operations.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="325f2-165">Run the apps</span><span class="sxs-lookup"><span data-stu-id="325f2-165">Run the apps</span></span>

<span data-ttu-id="325f2-166">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="325f2-166">You are now ready to run the apps.</span></span> <span data-ttu-id="325f2-167">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="325f2-167">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="325f2-168">Select **Multiple startup projects**, and then select **Start** as the action for the console app.</span><span class="sxs-lookup"><span data-stu-id="325f2-168">Select **Multiple startup projects**, and then select **Start** as the action for the console app.</span></span> <span data-ttu-id="325f2-169">And then press F5 to start both apps running.</span><span class="sxs-lookup"><span data-stu-id="325f2-169">And then press F5 to start both apps running.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="325f2-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="325f2-170">Next steps</span></span>

<span data-ttu-id="325f2-171">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="325f2-171">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="325f2-172">[Get started with IoT Hub module identity and module twin using .NET backup and .NET device][lnk-csharp-csharp-getstarted]</span><span class="sxs-lookup"><span data-stu-id="325f2-172">[Get started with IoT Hub module identity and module twin using .NET backup and .NET device][lnk-csharp-csharp-getstarted]</span></span>
* <span data-ttu-id="325f2-173">[Getting started with IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="325f2-173">[Getting started with IoT Edge][lnk-iot-edge]</span></span>


<!-- Images. -->
[8]:./media\iot-hub-portal-csharp-module-twin-getstarted/create-device-id.JPG
[9]:./media\iot-hub-portal-csharp-module-twin-getstarted/create-module-id.JPG
[10]:./media\iot-hub-portal-csharp-module-twin-getstarted/device-details.JPG
[11]:./media\iot-hub-portal-csharp-module-twin-getstarted/device-id-created.JPG
[12]:./media\iot-hub-portal-csharp-module-twin-getstarted/module-details.JPG
[13]: ./media\iot-hub-csharp-csharp-module-twin-getstarted/update-twins-csharp1.JPG
[14]: ./media\iot-hub-csharp-csharp-module-twin-getstarted/install-sdk.png
[15]: ./media\iot-hub-csharp-csharp-module-twin-getstarted/module-detail.JPG
<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-csharp-csharp-getstarted]: iot-hub-csharp-csharp-module-twin-getstarted.md
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
