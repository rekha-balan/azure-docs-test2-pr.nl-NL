---
title: Schedule jobs with Azure IoT Hub (.NET/.NET) | Microsoft Docs
description: How to schedule an Azure IoT Hub job to invoke a direct method on multiple devices. You use the Azure IoT device SDK for .NET to implement the simulated device apps and a service app to run the job.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 03/06/2018
ms.author: dobett
ms.openlocfilehash: eb7b4c4c6228818f78e002f4a06a000e9aa34a3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871485"
---
# <a name="schedule-and-broadcast-jobs-netnet"></a><span data-ttu-id="d14b4-104">Schedule and broadcast jobs (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="d14b4-104">Schedule and broadcast jobs (.NET/.NET)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="d14b4-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span><span class="sxs-lookup"><span data-stu-id="d14b4-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="d14b4-106">Use jobs to:</span><span class="sxs-lookup"><span data-stu-id="d14b4-106">Use jobs to:</span></span>

* <span data-ttu-id="d14b4-107">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="d14b4-107">Update desired properties</span></span>
* <span data-ttu-id="d14b4-108">Update tags</span><span class="sxs-lookup"><span data-stu-id="d14b4-108">Update tags</span></span>
* <span data-ttu-id="d14b4-109">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="d14b4-109">Invoke direct methods</span></span>

<span data-ttu-id="d14b4-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span><span class="sxs-lookup"><span data-stu-id="d14b4-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="d14b4-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span><span class="sxs-lookup"><span data-stu-id="d14b4-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="d14b4-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span><span class="sxs-lookup"><span data-stu-id="d14b4-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="d14b4-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="d14b4-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="d14b4-114">To learn more about each of these capabilities, see:</span><span class="sxs-lookup"><span data-stu-id="d14b4-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="d14b4-115">Device twin and properties: [Get started with device twins](iot-hub-csharp-csharp-twin-getstarted.md) and [Tutorial: How to use device twin properties](tutorial-device-twins.md)</span><span class="sxs-lookup"><span data-stu-id="d14b4-115">Device twin and properties: [Get started with device twins](iot-hub-csharp-csharp-twin-getstarted.md) and [Tutorial: How to use device twin properties](tutorial-device-twins.md)</span></span>

* <span data-ttu-id="d14b4-116">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](quickstart-control-device-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="d14b4-116">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](quickstart-control-device-dotnet.md)</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="d14b4-117">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="d14b4-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d14b4-118">Create a device app that implements a direct method called **LockDoor** that can be called by the back-end app.</span><span class="sxs-lookup"><span data-stu-id="d14b4-118">Create a device app that implements a direct method called **LockDoor** that can be called by the back-end app.</span></span>

* <span data-ttu-id="d14b4-119">Create a back-end app that creates a job to call the **LockDoor** direct method on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="d14b4-119">Create a back-end app that creates a job to call the **LockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="d14b4-120">Another job sends desired property updates to multiple devices.</span><span class="sxs-lookup"><span data-stu-id="d14b4-120">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="d14b4-121">At the end of this tutorial, you have two .NET (C#) console apps:</span><span class="sxs-lookup"><span data-stu-id="d14b4-121">At the end of this tutorial, you have two .NET (C#) console apps:</span></span>

<span data-ttu-id="d14b4-122">**SimulateDeviceMethods** that connects to your IoT hub and implements the **LockDoor** direct method.</span><span class="sxs-lookup"><span data-stu-id="d14b4-122">**SimulateDeviceMethods** that connects to your IoT hub and implements the **LockDoor** direct method.</span></span>

<span data-ttu-id="d14b4-123">**ScheduleJob** that uses jobs to call the **LockDoor** direct method and update the device twin desired properties on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="d14b4-123">**ScheduleJob** that uses jobs to call the **LockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="d14b4-124">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="d14b4-124">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d14b4-125">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d14b4-125">Visual Studio 2017.</span></span>
* <span data-ttu-id="d14b4-126">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="d14b4-126">An active Azure account.</span></span> <span data-ttu-id="d14b4-127">If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="d14b4-127">If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d14b4-128">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="d14b4-128">Create a simulated device app</span></span>

<span data-ttu-id="d14b4-129">In this section, you create a .NET console app that responds to a direct method called by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="d14b4-129">In this section, you create a .NET console app that responds to a direct method called by the solution back end.</span></span>

1. <span data-ttu-id="d14b4-130">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="d14b4-130">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="d14b4-131">Name the project **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-131">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![New Visual C# Windows Classic device app](./media/iot-hub-csharp-csharp-schedule-jobs/create-device-app.png)
    
2. <span data-ttu-id="d14b4-133">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-133">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>

3. <span data-ttu-id="d14b4-134">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices.Client**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-134">In the **NuGet Package Manager** window, select **Browse** and search for **Microsoft.Azure.Devices.Client**.</span></span> <span data-ttu-id="d14b4-135">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="d14b4-135">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="d14b4-136">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="d14b4-136">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window Client app](./media/iot-hub-csharp-csharp-schedule-jobs/device-app-nuget.png)

4. <span data-ttu-id="d14b4-138">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="d14b4-138">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="d14b4-139">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d14b4-139">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="d14b4-140">Replace the placeholder value with the device connection string that you noted in the previous section:</span><span class="sxs-lookup"><span data-stu-id="d14b4-140">Replace the placeholder value with the device connection string that you noted in the previous section:</span></span>

    ```csharp
    static string DeviceConnectionString = "<yourDeviceConnectionString>";
    static DeviceClient Client = null;
    ```

6. <span data-ttu-id="d14b4-141">Add the following to implement the direct method on the device:</span><span class="sxs-lookup"><span data-stu-id="d14b4-141">Add the following to implement the direct method on the device:</span></span>

    ```csharp
    static Task<MethodResponse> LockDoor(MethodRequest methodRequest, object userContext)
    {
        Console.WriteLine();
        Console.WriteLine("Locking Door!");
        Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);
            
        string result = "'Door was locked.'";
        return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
    }
    ```

7. <span data-ttu-id="d14b4-142">Add the following to implement the device twins listener on the device:</span><span class="sxs-lookup"><span data-stu-id="d14b4-142">Add the following to implement the device twins listener on the device:</span></span>

    ```csharp
    private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, 
      object userContext)
    {
        Console.WriteLine("Desired property change:");
        Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));
    }
    ```

8. <span data-ttu-id="d14b4-143">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span><span class="sxs-lookup"><span data-stu-id="d14b4-143">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```csharp
    try
    {
        Console.WriteLine("Connecting to hub");
        Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, 
          TransportType.Mqtt);

        Client.SetMethodHandlerAsync("LockDoor", LockDoor, null);
        Client.SetDesiredPropertyUpdateCallbackAsync(OnDesiredPropertyChanged, null);

        Console.WriteLine("Waiting for direct method call and device twin update\n Press enter to exit.");
        Console.ReadLine();

        Console.WriteLine("Exiting...");

        Client.SetMethodHandlerAsync("LockDoor", null, null);
        Client.CloseAsync().Wait();
    }
    catch (Exception ex)
    {
        Console.WriteLine();
        Console.WriteLine("Error in sample: {0}", ex.Message);
    }
    ```
        
9. <span data-ttu-id="d14b4-144">Save your work and build your solution.</span><span class="sxs-lookup"><span data-stu-id="d14b4-144">Save your work and build your solution.</span></span>         

> [!NOTE]
> <span data-ttu-id="d14b4-145">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="d14b4-145">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d14b4-146">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling](https://docs.microsoft.com/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="d14b4-146">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling](https://docs.microsoft.com/azure/architecture/best-practices/transient-faults).</span></span>
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="d14b4-147">Schedule jobs for calling a direct method and sending device twin updates</span><span class="sxs-lookup"><span data-stu-id="d14b4-147">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="d14b4-148">In this section, you create a .NET console app (using C#) that uses jobs to call the **LockDoor** direct method and send desired property updates to multiple devices.</span><span class="sxs-lookup"><span data-stu-id="d14b4-148">In this section, you create a .NET console app (using C#) that uses jobs to call the **LockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="d14b4-149">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="d14b4-149">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="d14b4-150">Name the project **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-150">Name the project **ScheduleJob**.</span></span>

    ![New Visual C# Windows Classic Desktop project](./media/iot-hub-csharp-csharp-schedule-jobs/createnetapp.png)

2. <span data-ttu-id="d14b4-152">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-152">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>

3. <span data-ttu-id="d14b4-153">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="d14b4-153">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="d14b4-154">This step downloads, installs, and adds a reference to the [Azure IoT service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="d14b4-154">This step downloads, installs, and adds a reference to the [Azure IoT service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices/) NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window](./media/iot-hub-csharp-csharp-schedule-jobs/servicesdknuget.png)

4. <span data-ttu-id="d14b4-156">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="d14b4-156">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

5. <span data-ttu-id="d14b4-157">Add the following `using` statement if not already present in the default statements.</span><span class="sxs-lookup"><span data-stu-id="d14b4-157">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    ```

6. <span data-ttu-id="d14b4-158">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d14b4-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="d14b4-159">Replace the placeholders with the IoT Hub connection string for the hub that you created in the previous section and the name of your device.</span><span class="sxs-lookup"><span data-stu-id="d14b4-159">Replace the placeholders with the IoT Hub connection string for the hub that you created in the previous section and the name of your device.</span></span>

    ```csharp
    static JobClient jobClient;
    static string connString = "<yourIotHubConnectionString>";
    static string deviceId = "<yourDeviceId>";
    ```

7. <span data-ttu-id="d14b4-160">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="d14b4-160">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && 
          (result.Status != JobStatus.Failed));
    }
    ```

8. <span data-ttu-id="d14b4-161">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="d14b4-161">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = 
          new CloudToDeviceMethod("LockDoor", TimeSpan.FromSeconds(5), 
          TimeSpan.FromSeconds(5));
       
        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            $"DeviceId IN ['{deviceId}']",
            directMethod,
            DateTime.UtcNow,
            (long)TimeSpan.FromMinutes(2).TotalSeconds);

        Console.WriteLine("Started Method Job");
    }
    ```

9. <span data-ttu-id="d14b4-162">Add another method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="d14b4-162">Add another method to the **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        Twin twin = new Twin(deviceId);
        twin.Tags = new TwinCollection();
        twin.Tags["Building"] = "43";
        twin.Tags["Floor"] = "3";
        twin.ETag = "*";

        twin.Properties.Desired["LocationUpdate"] = DateTime.UtcNow;

        JobResponse createJobResponse = jobClient.ScheduleTwinUpdateAsync(
            jobId,
            $"DeviceId IN ['{deviceId}']", 
            twin, 
            DateTime.UtcNow, 
            (long)TimeSpan.FromMinutes(2).TotalSeconds).Result;

        Console.WriteLine("Started Twin Update Job");
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="d14b4-163">For more information about query syntax, see [IoT Hub query language](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-query-language).</span><span class="sxs-lookup"><span data-stu-id="d14b4-163">For more information about query syntax, see [IoT Hub query language](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-query-language).</span></span>
    > 

10. <span data-ttu-id="d14b4-164">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="d14b4-164">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Press ENTER to start running jobs.");
    Console.ReadLine();

    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

11. <span data-ttu-id="d14b4-165">Save your work and build your solution.</span><span class="sxs-lookup"><span data-stu-id="d14b4-165">Save your work and build your solution.</span></span> 

## <a name="run-the-apps"></a><span data-ttu-id="d14b4-166">Run the apps</span><span class="sxs-lookup"><span data-stu-id="d14b4-166">Run the apps</span></span>

<span data-ttu-id="d14b4-167">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="d14b4-167">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="d14b4-168">In the Visual Studio Solution Explorer, right-click your solution, and then click **Build**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-168">In the Visual Studio Solution Explorer, right-click your solution, and then click **Build**.</span></span> <span data-ttu-id="d14b4-169">**Multiple startup projects**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-169">**Multiple startup projects**.</span></span> <span data-ttu-id="d14b4-170">Make sure `SimulateDeviceMethods` is at the top of the list followed by `ScheduleJob`.</span><span class="sxs-lookup"><span data-stu-id="d14b4-170">Make sure `SimulateDeviceMethods` is at the top of the list followed by `ScheduleJob`.</span></span> <span data-ttu-id="d14b4-171">Set both their actions to **Start** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-171">Set both their actions to **Start** and click **OK**.</span></span>

2. <span data-ttu-id="d14b4-172">Run the projects by clicking **Start** or go to the **Debug** menu and click **Start Debugging**.</span><span class="sxs-lookup"><span data-stu-id="d14b4-172">Run the projects by clicking **Start** or go to the **Debug** menu and click **Start Debugging**.</span></span>

3. <span data-ttu-id="d14b4-173">You see the output from both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="d14b4-173">You see the output from both device and back-end apps.</span></span>

    ![Run the apps to schedule jobs](./media/iot-hub-csharp-csharp-schedule-jobs/schedulejobs.png)

## <a name="next-steps"></a><span data-ttu-id="d14b4-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="d14b4-175">Next steps</span></span>

<span data-ttu-id="d14b4-176">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="d14b4-176">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="d14b4-177">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update](tutorial-firmware-update.md).</span><span class="sxs-lookup"><span data-stu-id="d14b4-177">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update](tutorial-firmware-update.md).</span></span>

<span data-ttu-id="d14b4-178">To learn about deploying AI to edge devices with Azure IoT Edge, see [Getting started with IoT Edge](../iot-edge/tutorial-simulate-device-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d14b4-178">To learn about deploying AI to edge devices with Azure IoT Edge, see [Getting started with IoT Edge](../iot-edge/tutorial-simulate-device-linux.md).</span></span>