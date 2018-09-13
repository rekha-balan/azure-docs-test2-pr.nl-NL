---
title: Cloud-to-device messages with Azure IoT Hub (.NET) | Microsoft Docs
description: How to send cloud-to-device messages to a device from an Azure IoT hub using the Azure IoT SDKs for .NET. You modify a simulated device app to receive cloud-to-device messages and modify a back-end app to send the cloud-to-device messages.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: ''
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/08/2017
ms.author: elioda
ms.openlocfilehash: 7948383eb87fc4668ac7a0fa17f9c7a65a4e1ecd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556715"
---
# <a name="send-messages-from-the-cloud-to-your-simulated-device-with-iot-hub-net"></a><span data-ttu-id="09058-104">Send messages from the cloud to your simulated device with IoT Hub (.NET)</span><span class="sxs-lookup"><span data-stu-id="09058-104">Send messages from the cloud to your simulated device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="09058-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="09058-105">Introduction</span></span>
<span data-ttu-id="09058-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="09058-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="09058-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="09058-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="09058-108">This tutorial builds on [Get started with IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="09058-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="09058-109">It shows you how to:</span><span class="sxs-lookup"><span data-stu-id="09058-109">It shows you how to:</span></span>

* <span data-ttu-id="09058-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09058-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="09058-111">Receive cloud-to-device messages on a device.</span><span class="sxs-lookup"><span data-stu-id="09058-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="09058-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09058-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="09058-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="09058-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="09058-114">At the end of this tutorial, you run two .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="09058-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="09058-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="09058-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="09058-116">**SendCloudToDevice**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span><span class="sxs-lookup"><span data-stu-id="09058-116">**SendCloudToDevice**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="09058-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span><span class="sxs-lookup"><span data-stu-id="09058-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="09058-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="09058-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="09058-119">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="09058-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="09058-120">Visual Studio 2015 or Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="09058-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="09058-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="09058-121">An active Azure account.</span></span> <span data-ttu-id="09058-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="09058-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="09058-123">Receive messages in the simulated device app</span><span class="sxs-lookup"><span data-stu-id="09058-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="09058-124">In this section, you'll modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="09058-124">In this section, you'll modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="09058-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="09058-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="09058-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span><span class="sxs-lookup"><span data-stu-id="09058-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="09058-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span><span class="sxs-lookup"><span data-stu-id="09058-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="09058-128">When the app receives a *null*, it should continue to wait for new messages.</span><span class="sxs-lookup"><span data-stu-id="09058-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="09058-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span><span class="sxs-lookup"><span data-stu-id="09058-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="09058-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span><span class="sxs-lookup"><span data-stu-id="09058-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="09058-131">The message can be safely removed from the device queue.</span><span class="sxs-lookup"><span data-stu-id="09058-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="09058-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span><span class="sxs-lookup"><span data-stu-id="09058-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="09058-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span><span class="sxs-lookup"><span data-stu-id="09058-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="09058-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span><span class="sxs-lookup"><span data-stu-id="09058-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="09058-135">Or, the application can reject a message, which permanently removes the message from the queue.</span><span class="sxs-lookup"><span data-stu-id="09058-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="09058-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="09058-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09058-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span><span class="sxs-lookup"><span data-stu-id="09058-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="09058-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="09058-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="09058-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span><span class="sxs-lookup"><span data-stu-id="09058-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="09058-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="09058-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="09058-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span><span class="sxs-lookup"><span data-stu-id="09058-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="09058-142">For simplicity's sake, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="09058-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="09058-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="09058-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="09058-144">Send a cloud-to-device message</span><span class="sxs-lookup"><span data-stu-id="09058-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="09058-145">In this section, you write a .NET console app that sends cloud-to-device messages to the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="09058-145">In this section, you write a .NET console app that sends cloud-to-device messages to the simulated device app.</span></span>

1. <span data-ttu-id="09058-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="09058-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="09058-147">Name the project **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="09058-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![New project in Visual Studio][20]
2. <span data-ttu-id="09058-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span><span class="sxs-lookup"><span data-stu-id="09058-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="09058-150">This action opens the **Manage NuGet Packages** window.</span><span class="sxs-lookup"><span data-stu-id="09058-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="09058-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="09058-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="09058-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span><span class="sxs-lookup"><span data-stu-id="09058-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="09058-153">Add the following `using` statement at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="09058-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="09058-154">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="09058-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="09058-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="09058-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="09058-156">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="09058-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="09058-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="09058-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="09058-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="09058-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="09058-159">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="09058-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="09058-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="09058-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="09058-161">Press **F5**.</span><span class="sxs-lookup"><span data-stu-id="09058-161">Press **F5**.</span></span> <span data-ttu-id="09058-162">All three applications should start.</span><span class="sxs-lookup"><span data-stu-id="09058-162">All three applications should start.</span></span> <span data-ttu-id="09058-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="09058-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="09058-164">You should see the message being received by the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="09058-164">You should see the message being received by the simulated device app.</span></span>
   
   ![App receiving message][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="09058-166">Receive delivery feedback</span><span class="sxs-lookup"><span data-stu-id="09058-166">Receive delivery feedback</span></span>
<span data-ttu-id="09058-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span><span class="sxs-lookup"><span data-stu-id="09058-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="09058-168">This option enables the solution back end to easily inform retry or compensation logic.</span><span class="sxs-lookup"><span data-stu-id="09058-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="09058-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="09058-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="09058-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09058-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="09058-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="09058-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="09058-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span><span class="sxs-lookup"><span data-stu-id="09058-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="09058-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span><span class="sxs-lookup"><span data-stu-id="09058-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="09058-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span><span class="sxs-lookup"><span data-stu-id="09058-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="09058-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span><span class="sxs-lookup"><span data-stu-id="09058-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="09058-176">Run the apps by pressing **F5**.</span><span class="sxs-lookup"><span data-stu-id="09058-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="09058-177">You should see all three applications start.</span><span class="sxs-lookup"><span data-stu-id="09058-177">You should see all three applications start.</span></span> <span data-ttu-id="09058-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="09058-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="09058-179">You should see the message being received by the simulated device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span><span class="sxs-lookup"><span data-stu-id="09058-179">You should see the message being received by the simulated device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![App receiving message][22]

> [!NOTE]
> <span data-ttu-id="09058-181">For simplicity's sake, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="09058-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="09058-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="09058-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="09058-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="09058-183">Next steps</span></span>
<span data-ttu-id="09058-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="09058-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="09058-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="09058-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="09058-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="09058-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[IoT Hub developer guide]: iot-hub-devguide.md
[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IoT device SDKs]: iot-hub-devguide-sdks.md


