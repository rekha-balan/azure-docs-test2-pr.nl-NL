---
title: Use Azure IoT Hub direct methods (.NET/Node) | Microsoft Docs
description: How to use Azure IoT Hub direct methods. You use the Azure IoT device SDK for Node.js to implement a simulated device app that includes a direct method and the Azure IoT service SDK for .NET to implement a service app that invokes the direct method.
services: iot-hub
documentationcenter: ''
author: nberdy
manager: timlt
editor: ''
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: 9ae295c0cc4f069828b677efa0edd638622bf1a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564639"
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="1c063-104">Use direct methods (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="1c063-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="1c063-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span><span class="sxs-lookup"><span data-stu-id="1c063-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="1c063-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span><span class="sxs-lookup"><span data-stu-id="1c063-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="1c063-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span><span class="sxs-lookup"><span data-stu-id="1c063-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="1c063-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span><span class="sxs-lookup"><span data-stu-id="1c063-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="1c063-109">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="1c063-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="1c063-110">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1c063-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1c063-111">Node.js version 0.10.x or later.</span><span class="sxs-lookup"><span data-stu-id="1c063-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="1c063-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="1c063-112">An active Azure account.</span></span> <span data-ttu-id="1c063-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="1c063-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1c063-114">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="1c063-114">Create a simulated device app</span></span>
<span data-ttu-id="1c063-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="1c063-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="1c063-116">Create a new empty folder called **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="1c063-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="1c063-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="1c063-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="1c063-118">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="1c063-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1c063-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span><span class="sxs-lookup"><span data-stu-id="1c063-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1c063-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="1c063-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="1c063-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="1c063-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="1c063-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span><span class="sxs-lookup"><span data-stu-id="1c063-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="1c063-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="1c063-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="1c063-124">Add the following function to implement the direct method on the device:</span><span class="sxs-lookup"><span data-stu-id="1c063-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="1c063-125">Open the connection to your IoT hub and initialize the method listener:</span><span class="sxs-lookup"><span data-stu-id="1c063-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="1c063-126">Save and close the **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="1c063-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="1c063-127">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="1c063-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1c063-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1c063-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="1c063-129">Call a direct method on a device</span><span class="sxs-lookup"><span data-stu-id="1c063-129">Call a direct method on a device</span></span>
<span data-ttu-id="1c063-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span><span class="sxs-lookup"><span data-stu-id="1c063-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="1c063-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="1c063-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="1c063-132">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="1c063-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="1c063-133">Name the project **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="1c063-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![New Visual C# Windows Classic Desktop project][10]
2. <span data-ttu-id="1c063-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="1c063-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="1c063-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="1c063-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="1c063-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="1c063-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Package Manager window][11]

4. <span data-ttu-id="1c063-139">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="1c063-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="1c063-140">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="1c063-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="1c063-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="1c063-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="1c063-142">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="1c063-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="1c063-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span><span class="sxs-lookup"><span data-stu-id="1c063-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="1c063-144">Then, it writes the response provided by the device on the console.</span><span class="sxs-lookup"><span data-stu-id="1c063-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="1c063-145">Note how it is possible to specify a timeout value for the device to respond.</span><span class="sxs-lookup"><span data-stu-id="1c063-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="1c063-146">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="1c063-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="1c063-147">Run the applications</span><span class="sxs-lookup"><span data-stu-id="1c063-147">Run the applications</span></span>
<span data-ttu-id="1c063-148">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="1c063-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="1c063-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="1c063-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="1c063-150">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="1c063-150">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="1c063-151">Wait for the simulated device to open:  ![][7]</span><span class="sxs-lookup"><span data-stu-id="1c063-151">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="1c063-152">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="1c063-152">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="1c063-153">You should see the device response written in the console.</span><span class="sxs-lookup"><span data-stu-id="1c063-153">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="1c063-154">The device then reacts to the method by printing this message:</span><span class="sxs-lookup"><span data-stu-id="1c063-154">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="1c063-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c063-155">Next steps</span></span>
<span data-ttu-id="1c063-156">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="1c063-156">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="1c063-157">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span><span class="sxs-lookup"><span data-stu-id="1c063-157">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="1c063-158">You also created an app that invokes methods on the device and displays the response from the device.</span><span class="sxs-lookup"><span data-stu-id="1c063-158">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="1c063-159">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="1c063-159">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="1c063-160">[Get started with IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="1c063-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="1c063-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="1c063-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="1c063-162">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c063-162">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Get started with IoT Hub]: iot-hub-node-node-getstarted.md





