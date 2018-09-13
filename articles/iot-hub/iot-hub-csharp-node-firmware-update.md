---
title: Device firmware update with Azure IoT Hub (.NET/Node) | Microsoft Docs
description: How to use device management on Azure IoT Hub to initiate a device firmware update. You use the Azure IoT device SDK for Node.js to implement a simulated device app and the Azure IoT service SDK for .NET to implement a service app that triggers the firmware update.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: ''
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: 7e516b95948dbd0e02964859bb71a40fe0d19ee9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550303"
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="539d1-104">Use device management to initiate a device firmware update (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="539d1-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="539d1-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="539d1-105">Introduction</span></span>
<span data-ttu-id="539d1-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span><span class="sxs-lookup"><span data-stu-id="539d1-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="539d1-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span><span class="sxs-lookup"><span data-stu-id="539d1-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="539d1-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="539d1-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="539d1-109">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="539d1-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="539d1-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="539d1-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="539d1-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span><span class="sxs-lookup"><span data-stu-id="539d1-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="539d1-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span><span class="sxs-lookup"><span data-stu-id="539d1-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="539d1-113">During each stage of the update, the device uses the reported properties to report on progress.</span><span class="sxs-lookup"><span data-stu-id="539d1-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="539d1-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span><span class="sxs-lookup"><span data-stu-id="539d1-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="539d1-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="539d1-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="539d1-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span><span class="sxs-lookup"><span data-stu-id="539d1-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="539d1-117">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="539d1-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="539d1-118">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="539d1-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="539d1-119">Node.js version 0.12.x or later,</span><span class="sxs-lookup"><span data-stu-id="539d1-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="539d1-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="539d1-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="539d1-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="539d1-121">An active Azure account.</span></span> <span data-ttu-id="539d1-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="539d1-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="539d1-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span><span class="sxs-lookup"><span data-stu-id="539d1-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="539d1-124">Trigger a remote firmware update on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="539d1-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="539d1-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span><span class="sxs-lookup"><span data-stu-id="539d1-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="539d1-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span><span class="sxs-lookup"><span data-stu-id="539d1-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="539d1-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="539d1-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="539d1-128">Name the project **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="539d1-128">Name the project **TriggerFWUpdate**.</span></span>

    ![New Visual C# Windows Classic Desktop project][img-createapp]

1. <span data-ttu-id="539d1-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="539d1-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="539d1-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="539d1-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="539d1-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="539d1-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window][img-servicenuget]
1. <span data-ttu-id="539d1-134">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="539d1-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="539d1-135">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="539d1-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="539d1-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span><span class="sxs-lookup"><span data-stu-id="539d1-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="539d1-137">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="539d1-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="539d1-138">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="539d1-138">Add the following method to the **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="539d1-139">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="539d1-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="539d1-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span><span class="sxs-lookup"><span data-stu-id="539d1-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="539d1-141">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="539d1-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="539d1-142">Run the apps</span><span class="sxs-lookup"><span data-stu-id="539d1-142">Run the apps</span></span>
<span data-ttu-id="539d1-143">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="539d1-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="539d1-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="539d1-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="539d1-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="539d1-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="539d1-146">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="539d1-146">You see the device response to the direct method in the console.</span></span>

    ![Firmware updated successfully][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="539d1-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="539d1-148">Next steps</span></span>
<span data-ttu-id="539d1-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span><span class="sxs-lookup"><span data-stu-id="539d1-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="539d1-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="539d1-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/


