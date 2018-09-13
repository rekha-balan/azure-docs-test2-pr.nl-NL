---
title: Get started with Azure IoT Hub device management (.NET/.NET) | Microsoft Docs
description: How to use Azure IoT Hub device management to initiate a remote device reboot. You use the Azure IoT device SDK for .NET to implement a simulated device app that includes a direct method and the Azure IoT service SDK for .NET to implement a service app that invokes the direct method.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: csharp
ms.topic: conceptual
ms.date: 09/15/2017
ms.author: dobett
ms.openlocfilehash: ed591007e6ad83dfbafe13db0bd3d8b53fc216f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866617"
---
# <a name="get-started-with-device-management-netnet"></a><span data-ttu-id="976d8-104">Get started with device management (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="976d8-104">Get started with device management (.NET/.NET)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="976d8-105">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="976d8-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="976d8-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="976d8-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>

* <span data-ttu-id="976d8-107">Create a simulated device app that contains a direct method that reboots that device.</span><span class="sxs-lookup"><span data-stu-id="976d8-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="976d8-108">Direct methods are invoked from the cloud.</span><span class="sxs-lookup"><span data-stu-id="976d8-108">Direct methods are invoked from the cloud.</span></span>

* <span data-ttu-id="976d8-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="976d8-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="976d8-110">At the end of this tutorial, you have two .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="976d8-110">At the end of this tutorial, you have two .NET console apps:</span></span>

* <span data-ttu-id="976d8-111">**SimulateManagedDevice**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span><span class="sxs-lookup"><span data-stu-id="976d8-111">**SimulateManagedDevice**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

* <span data-ttu-id="976d8-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="976d8-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="976d8-113">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="976d8-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="976d8-114">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="976d8-114">Visual Studio 2017.</span></span>

* <span data-ttu-id="976d8-115">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="976d8-115">An active Azure account.</span></span> <span data-ttu-id="976d8-116">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="976d8-116">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="976d8-117">Trigger a remote reboot on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="976d8-117">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="976d8-118">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span><span class="sxs-lookup"><span data-stu-id="976d8-118">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="976d8-119">The app uses device twin queries to discover the last reboot time for that device.</span><span class="sxs-lookup"><span data-stu-id="976d8-119">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="976d8-120">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="976d8-120">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="976d8-121">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="976d8-121">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="976d8-122">Name the project **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="976d8-122">Name the project **TriggerReboot**.</span></span>

    ![New Visual C# Windows Classic Desktop project](./media/iot-hub-csharp-csharp-device-management-get-started/createserviceapp.png)

2. <span data-ttu-id="976d8-124">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="976d8-124">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="976d8-125">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="976d8-125">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="976d8-126">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="976d8-126">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices/) NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window](./media/iot-hub-csharp-csharp-device-management-get-started/servicesdknuget.png)

4. <span data-ttu-id="976d8-128">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="976d8-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
   ```csharp
   using Microsoft.Azure.Devices;
   using Microsoft.Azure.Devices.Shared;
   ```
        
5. <span data-ttu-id="976d8-129">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="976d8-129">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="976d8-130">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the section "Create an IoT hub."</span><span class="sxs-lookup"><span data-stu-id="976d8-130">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the section "Create an IoT hub."</span></span> 
   
   ```csharp
   static RegistryManager registryManager;
   static string connString = "{iot hub connection string}";
   static ServiceClient client;
   static string targetDevice = "myDeviceId";
   ```

6. <span data-ttu-id="976d8-131">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="976d8-131">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="976d8-132">This code gets the device twin for the rebooting device and outputs the reported properties.</span><span class="sxs-lookup"><span data-stu-id="976d8-132">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
   ```csharp
   public static async Task QueryTwinRebootReported()
   {
       Twin twin = await registryManager.GetTwinAsync(targetDevice);
       Console.WriteLine(twin.Properties.Reported.ToJson());
   }
   ```
        
7. <span data-ttu-id="976d8-133">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="976d8-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="976d8-134">This code initiates the reboot on the device using a direct method.</span><span class="sxs-lookup"><span data-stu-id="976d8-134">This code initiates the reboot on the device using a direct method.</span></span>

   ```csharp
   public static async Task StartReboot()
   {
       client = ServiceClient.CreateFromConnectionString(connString);
       CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
       method.ResponseTimeout = TimeSpan.FromSeconds(30);

       CloudToDeviceMethodResult result = await 
         client.InvokeDeviceMethodAsync(targetDevice, method);

       Console.WriteLine("Invoked firmware update on device.");
   }
   ```

7. <span data-ttu-id="976d8-135">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="976d8-135">Finally, add the following lines to the **Main** method:</span></span>
   
   ```csharp
   registryManager = RegistryManager.CreateFromConnectionString(connString);
   StartReboot().Wait();
   QueryTwinRebootReported().Wait();
   Console.WriteLine("Press ENTER to exit.");
   Console.ReadLine();
   ```

8. <span data-ttu-id="976d8-136">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="976d8-136">Build the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="976d8-137">This tutorial performs only a single query for the device's reported properties.</span><span class="sxs-lookup"><span data-stu-id="976d8-137">This tutorial performs only a single query for the device's reported properties.</span></span> <span data-ttu-id="976d8-138">In production code, we recommend polling to detect changes in the reported properties.</span><span class="sxs-lookup"><span data-stu-id="976d8-138">In production code, we recommend polling to detect changes in the reported properties.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="976d8-139">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="976d8-139">Create a simulated device app</span></span>

<span data-ttu-id="976d8-140">In this section, you do the following:</span><span class="sxs-lookup"><span data-stu-id="976d8-140">In this section, you do the following:</span></span>

* <span data-ttu-id="976d8-141">Create a .NET console app that responds to a direct method called by the cloud.</span><span class="sxs-lookup"><span data-stu-id="976d8-141">Create a .NET console app that responds to a direct method called by the cloud.</span></span>

* <span data-ttu-id="976d8-142">Trigger a simulated device reboot.</span><span class="sxs-lookup"><span data-stu-id="976d8-142">Trigger a simulated device reboot.</span></span>

* <span data-ttu-id="976d8-143">Use the reported properties to enable device twin queries to identify devices and when they were last rebooted.</span><span class="sxs-lookup"><span data-stu-id="976d8-143">Use the reported properties to enable device twin queries to identify devices and when they were last rebooted.</span></span>

1. <span data-ttu-id="976d8-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="976d8-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="976d8-145">Name the project **SimulateManagedDevice**.</span><span class="sxs-lookup"><span data-stu-id="976d8-145">Name the project **SimulateManagedDevice**.</span></span>
   
    ![New Visual C# Windows Classic device app](./media/iot-hub-csharp-csharp-device-management-get-started/createdeviceapp.png)
    
2. <span data-ttu-id="976d8-147">In Solution Explorer, right-click the **SimulateManagedDevice** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="976d8-147">In Solution Explorer, right-click the **SimulateManagedDevice** project, and then click **Manage NuGet Packages...**.</span></span>

3. <span data-ttu-id="976d8-148">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices.Client**.</span><span class="sxs-lookup"><span data-stu-id="976d8-148">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices.Client**.</span></span> <span data-ttu-id="976d8-149">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="976d8-149">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="976d8-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="976d8-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window Client app](./media/iot-hub-csharp-csharp-device-management-get-started/clientsdknuget.png)
    
4. <span data-ttu-id="976d8-152">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="976d8-152">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    ```

5. <span data-ttu-id="976d8-153">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="976d8-153">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="976d8-154">Replace the placeholder value with the device connection string that you noted in the previous section.</span><span class="sxs-lookup"><span data-stu-id="976d8-154">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>

    ```csharp
    static string DeviceConnectionString = 
      "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
    static DeviceClient Client = null;
    ```
6. <span data-ttu-id="976d8-155">Add the following to implement the direct method on the device:</span><span class="sxs-lookup"><span data-stu-id="976d8-155">Add the following to implement the direct method on the device:</span></span>

   ```csharp
   static Task<MethodResponse> onReboot(MethodRequest methodRequest, object userContext)
   {
       // In a production device, you would trigger a reboot 
       //   scheduled to start after this method returns.
       // For this sample, we simulate the reboot by writing to the console
       //   and updating the reported properties.
       try
       {
           Console.WriteLine("Rebooting!");

           // Update device twin with reboot time. 
           TwinCollection reportedProperties, reboot, lastReboot;
           lastReboot = new TwinCollection();
           reboot = new TwinCollection();
           reportedProperties = new TwinCollection();
           lastReboot["lastReboot"] = DateTime.Now;
           reboot["reboot"] = lastReboot;
           reportedProperties["iothubDM"] = reboot;
           Client.UpdateReportedPropertiesAsync(reportedProperties).Wait();
       }
       catch (Exception ex)
       {
           Console.WriteLine();
           Console.WriteLine("Error in sample: {0}", ex.Message);
       }

       string result = "'Reboot started.'";
       return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
   }
   ```

7. <span data-ttu-id="976d8-156">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span><span class="sxs-lookup"><span data-stu-id="976d8-156">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>

   ```csharp
   try
   {
       Console.WriteLine("Connecting to hub");
       Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, 
         TransportType.Mqtt);

       // setup callback for "reboot" method
       Client.SetMethodHandlerAsync("reboot", onReboot, null).Wait();
       Console.WriteLine("Waiting for reboot method\n Press enter to exit.");
       Console.ReadLine();

       Console.WriteLine("Exiting...");

       // as a good practice, remove the "reboot" handler
       Client.SetMethodHandlerAsync("reboot", null, null).Wait();
       Client.CloseAsync().Wait();
   }
   catch (Exception ex)
   {
       Console.WriteLine();
       Console.WriteLine("Error in sample: {0}", ex.Message);
   }
   ```
        
8. <span data-ttu-id="976d8-157">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select the **SimulateManagedDevice** project in the dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="976d8-157">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select the **SimulateManagedDevice** project in the dropdown menu.</span></span> <span data-ttu-id="976d8-158">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="976d8-158">Build the solution.</span></span>       

> [!NOTE]
> <span data-ttu-id="976d8-159">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="976d8-159">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="976d8-160">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh680901.aspx).</span><span class="sxs-lookup"><span data-stu-id="976d8-160">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh680901.aspx).</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="976d8-161">Run the apps</span><span class="sxs-lookup"><span data-stu-id="976d8-161">Run the apps</span></span>

<span data-ttu-id="976d8-162">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="976d8-162">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="976d8-163">To run the .NET device app **SimulateManagedDevice**.</span><span class="sxs-lookup"><span data-stu-id="976d8-163">To run the .NET device app **SimulateManagedDevice**.</span></span> <span data-ttu-id="976d8-164">right-click the **SimulateManagedDevice** project, select **Debug**, and then select **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="976d8-164">right-click the **SimulateManagedDevice** project, select **Debug**, and then select **Start new instance**.</span></span> <span data-ttu-id="976d8-165">It should start listening for method calls from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="976d8-165">It should start listening for method calls from your IoT hub.</span></span> 

2. <span data-ttu-id="976d8-166">Now that the device is connected and waiting for method invocations, run the .NET **TriggerReboot** app to invoke the reboot method in the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="976d8-166">Now that the device is connected and waiting for method invocations, run the .NET **TriggerReboot** app to invoke the reboot method in the simulated device app.</span></span> <span data-ttu-id="976d8-167">To do this, right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="976d8-167">To do this, right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span> <span data-ttu-id="976d8-168">You should see "Rebooting!"</span><span class="sxs-lookup"><span data-stu-id="976d8-168">You should see "Rebooting!"</span></span> <span data-ttu-id="976d8-169">written in the **SimulatedManagedDevice** console and the reported properties of the device, which include the last reboot time,  written in the **TriggerReboot** console.</span><span class="sxs-lookup"><span data-stu-id="976d8-169">written in the **SimulatedManagedDevice** console and the reported properties of the device, which include the last reboot time,  written in the **TriggerReboot** console.</span></span>
   
    ![Service and device app run](./media/iot-hub-csharp-csharp-device-management-get-started/combinedrun.png)

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]
