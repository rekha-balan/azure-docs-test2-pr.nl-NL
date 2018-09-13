---
title: Azure IoT device SDK for C - IoTHubClient | Microsoft Docs
description: How to use the IoTHubClient library in the Azure IoT device SDK for C to create device apps that communicate with an IoT hub.
services: iot-hub
documentationcenter: ''
author: olivierbloch
manager: timlt
editor: ''
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: 669ef16c4fe2edd4525db6f693c424f3027793f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552350"
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="ddd68-103">Azure IoT device SDK for C – more about IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="ddd68-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="ddd68-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span><span class="sxs-lookup"><span data-stu-id="ddd68-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="ddd68-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="ddd68-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span><span class="sxs-lookup"><span data-stu-id="ddd68-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="ddd68-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="ddd68-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="ddd68-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span><span class="sxs-lookup"><span data-stu-id="ddd68-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="ddd68-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span><span class="sxs-lookup"><span data-stu-id="ddd68-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="ddd68-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="ddd68-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="ddd68-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="ddd68-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span><span class="sxs-lookup"><span data-stu-id="ddd68-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="ddd68-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span><span class="sxs-lookup"><span data-stu-id="ddd68-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="ddd68-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span><span class="sxs-lookup"><span data-stu-id="ddd68-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="ddd68-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="ddd68-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="ddd68-116">The lower-level APIs</span><span class="sxs-lookup"><span data-stu-id="ddd68-116">The lower-level APIs</span></span>
<span data-ttu-id="ddd68-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span><span class="sxs-lookup"><span data-stu-id="ddd68-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="ddd68-118">For example, it explained how to initialize the library using this code.</span><span class="sxs-lookup"><span data-stu-id="ddd68-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="ddd68-119">It also described how to send events using this function call.</span><span class="sxs-lookup"><span data-stu-id="ddd68-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="ddd68-120">The article also described how to receive messages by registering a callback function.</span><span class="sxs-lookup"><span data-stu-id="ddd68-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="ddd68-121">The article also showed how to free resources using code such as the following.</span><span class="sxs-lookup"><span data-stu-id="ddd68-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="ddd68-122">However there are companion functions to each of these APIs:</span><span class="sxs-lookup"><span data-stu-id="ddd68-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="ddd68-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="ddd68-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="ddd68-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="ddd68-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="ddd68-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="ddd68-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="ddd68-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="ddd68-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="ddd68-127">These functions all include “LL” in the API name.</span><span class="sxs-lookup"><span data-stu-id="ddd68-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="ddd68-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span><span class="sxs-lookup"><span data-stu-id="ddd68-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="ddd68-129">However, the behavior of these functions is different in one important way.</span><span class="sxs-lookup"><span data-stu-id="ddd68-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="ddd68-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span><span class="sxs-lookup"><span data-stu-id="ddd68-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="ddd68-131">This thread sends events to, and receives messages from, IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="ddd68-132">No such thread is created when working with the "LL" APIs.</span><span class="sxs-lookup"><span data-stu-id="ddd68-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="ddd68-133">The creation of the background thread is a convenience to the developer.</span><span class="sxs-lookup"><span data-stu-id="ddd68-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="ddd68-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span><span class="sxs-lookup"><span data-stu-id="ddd68-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="ddd68-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span><span class="sxs-lookup"><span data-stu-id="ddd68-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="ddd68-136">To understand this better, let’s look at an example:</span><span class="sxs-lookup"><span data-stu-id="ddd68-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="ddd68-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span><span class="sxs-lookup"><span data-stu-id="ddd68-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="ddd68-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="ddd68-139">This happens in the background at the same time that the main thread is performing other work.</span><span class="sxs-lookup"><span data-stu-id="ddd68-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="ddd68-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span><span class="sxs-lookup"><span data-stu-id="ddd68-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="ddd68-141">The "LL" APIs don’t create a background thread.</span><span class="sxs-lookup"><span data-stu-id="ddd68-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="ddd68-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="ddd68-143">This is demonstrated in the following example.</span><span class="sxs-lookup"><span data-stu-id="ddd68-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="ddd68-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span><span class="sxs-lookup"><span data-stu-id="ddd68-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="ddd68-145">In that sample, we send events to IoT Hub with code such as the following:</span><span class="sxs-lookup"><span data-stu-id="ddd68-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="ddd68-146">The first three lines create the message, and the last line sends the event.</span><span class="sxs-lookup"><span data-stu-id="ddd68-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="ddd68-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span><span class="sxs-lookup"><span data-stu-id="ddd68-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="ddd68-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="ddd68-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="ddd68-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span><span class="sxs-lookup"><span data-stu-id="ddd68-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="ddd68-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="ddd68-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="ddd68-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span><span class="sxs-lookup"><span data-stu-id="ddd68-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="ddd68-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span><span class="sxs-lookup"><span data-stu-id="ddd68-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="ddd68-153">We would have registered such a callback function with code such as the following:</span><span class="sxs-lookup"><span data-stu-id="ddd68-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="ddd68-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span><span class="sxs-lookup"><span data-stu-id="ddd68-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="ddd68-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span><span class="sxs-lookup"><span data-stu-id="ddd68-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="ddd68-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span><span class="sxs-lookup"><span data-stu-id="ddd68-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="ddd68-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="ddd68-158">Note this does not also imply that all queued messages have been received.</span><span class="sxs-lookup"><span data-stu-id="ddd68-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="ddd68-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span><span class="sxs-lookup"><span data-stu-id="ddd68-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="ddd68-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span><span class="sxs-lookup"><span data-stu-id="ddd68-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="ddd68-161">A better way to deal with that is with a programmed timeout.</span><span class="sxs-lookup"><span data-stu-id="ddd68-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="ddd68-162">For example, the message callback function could reset a timer every time it’s invoked.</span><span class="sxs-lookup"><span data-stu-id="ddd68-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="ddd68-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span><span class="sxs-lookup"><span data-stu-id="ddd68-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="ddd68-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span><span class="sxs-lookup"><span data-stu-id="ddd68-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="ddd68-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span><span class="sxs-lookup"><span data-stu-id="ddd68-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="ddd68-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span><span class="sxs-lookup"><span data-stu-id="ddd68-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="ddd68-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span><span class="sxs-lookup"><span data-stu-id="ddd68-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="ddd68-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="ddd68-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span><span class="sxs-lookup"><span data-stu-id="ddd68-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="ddd68-170">Everything happens on the main thread rather than some work happening in the background.</span><span class="sxs-lookup"><span data-stu-id="ddd68-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="ddd68-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span><span class="sxs-lookup"><span data-stu-id="ddd68-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="ddd68-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span><span class="sxs-lookup"><span data-stu-id="ddd68-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="ddd68-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="ddd68-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="ddd68-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="ddd68-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="ddd68-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="ddd68-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="ddd68-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="ddd68-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="ddd68-177">The opposite is true as well.</span><span class="sxs-lookup"><span data-stu-id="ddd68-177">The opposite is true as well.</span></span> <span data-ttu-id="ddd68-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span><span class="sxs-lookup"><span data-stu-id="ddd68-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="ddd68-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span><span class="sxs-lookup"><span data-stu-id="ddd68-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="ddd68-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span><span class="sxs-lookup"><span data-stu-id="ddd68-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="ddd68-181">Property handling</span><span class="sxs-lookup"><span data-stu-id="ddd68-181">Property handling</span></span>
<span data-ttu-id="ddd68-182">So far when we've described sending data, we've been referring to the body of the message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="ddd68-183">For example, consider this code:</span><span class="sxs-lookup"><span data-stu-id="ddd68-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="ddd68-184">This example sends a message to IoT Hub with the text "Hello World."</span><span class="sxs-lookup"><span data-stu-id="ddd68-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="ddd68-185">However, IoT Hub also allows properties to be attached to each message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="ddd68-186">Properties are name/value pairs that can be attached to the message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="ddd68-187">For example, we can modify the previous code to attach a property to the message:</span><span class="sxs-lookup"><span data-stu-id="ddd68-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="ddd68-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="ddd68-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span><span class="sxs-lookup"><span data-stu-id="ddd68-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="ddd68-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span><span class="sxs-lookup"><span data-stu-id="ddd68-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="ddd68-191">With this API we can add as many properties as we like.</span><span class="sxs-lookup"><span data-stu-id="ddd68-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="ddd68-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span><span class="sxs-lookup"><span data-stu-id="ddd68-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="ddd68-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddd68-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="ddd68-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="ddd68-195">Properties can also be attached to messages received from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="ddd68-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span><span class="sxs-lookup"><span data-stu-id="ddd68-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

<span data-ttu-id="ddd68-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span><span class="sxs-lookup"><span data-stu-id="ddd68-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="ddd68-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span><span class="sxs-lookup"><span data-stu-id="ddd68-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="ddd68-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span><span class="sxs-lookup"><span data-stu-id="ddd68-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="ddd68-200">You don't have to use properties in your application.</span><span class="sxs-lookup"><span data-stu-id="ddd68-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="ddd68-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span><span class="sxs-lookup"><span data-stu-id="ddd68-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="ddd68-202">Message handling</span><span class="sxs-lookup"><span data-stu-id="ddd68-202">Message handling</span></span>
<span data-ttu-id="ddd68-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span><span class="sxs-lookup"><span data-stu-id="ddd68-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="ddd68-204">There is a return parameter of this function that deserves some additional explanation.</span><span class="sxs-lookup"><span data-stu-id="ddd68-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="ddd68-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span><span class="sxs-lookup"><span data-stu-id="ddd68-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="ddd68-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span><span class="sxs-lookup"><span data-stu-id="ddd68-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="ddd68-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span><span class="sxs-lookup"><span data-stu-id="ddd68-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="ddd68-208">Here are the options.</span><span class="sxs-lookup"><span data-stu-id="ddd68-208">Here are the options.</span></span>

* <span data-ttu-id="ddd68-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span><span class="sxs-lookup"><span data-stu-id="ddd68-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="ddd68-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="ddd68-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span><span class="sxs-lookup"><span data-stu-id="ddd68-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="ddd68-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="ddd68-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="ddd68-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span><span class="sxs-lookup"><span data-stu-id="ddd68-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="ddd68-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span><span class="sxs-lookup"><span data-stu-id="ddd68-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="ddd68-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span><span class="sxs-lookup"><span data-stu-id="ddd68-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="ddd68-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span><span class="sxs-lookup"><span data-stu-id="ddd68-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="ddd68-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span><span class="sxs-lookup"><span data-stu-id="ddd68-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="ddd68-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span><span class="sxs-lookup"><span data-stu-id="ddd68-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="ddd68-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="ddd68-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="ddd68-221">Alternate device credentials</span><span class="sxs-lookup"><span data-stu-id="ddd68-221">Alternate device credentials</span></span>
<span data-ttu-id="ddd68-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span><span class="sxs-lookup"><span data-stu-id="ddd68-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="ddd68-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ddd68-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="ddd68-224">The device connection string has a format that appears as follows:</span><span class="sxs-lookup"><span data-stu-id="ddd68-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="ddd68-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span><span class="sxs-lookup"><span data-stu-id="ddd68-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="ddd68-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span><span class="sxs-lookup"><span data-stu-id="ddd68-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="ddd68-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="ddd68-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="ddd68-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span><span class="sxs-lookup"><span data-stu-id="ddd68-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="ddd68-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span><span class="sxs-lookup"><span data-stu-id="ddd68-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="ddd68-230">This is achieved with the following code:</span><span class="sxs-lookup"><span data-stu-id="ddd68-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="ddd68-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="ddd68-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="ddd68-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span><span class="sxs-lookup"><span data-stu-id="ddd68-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="ddd68-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span><span class="sxs-lookup"><span data-stu-id="ddd68-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="ddd68-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span><span class="sxs-lookup"><span data-stu-id="ddd68-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="ddd68-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span><span class="sxs-lookup"><span data-stu-id="ddd68-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="ddd68-236">Use whichever method is convenient.</span><span class="sxs-lookup"><span data-stu-id="ddd68-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="ddd68-237">Configuration options</span><span class="sxs-lookup"><span data-stu-id="ddd68-237">Configuration options</span></span>
<span data-ttu-id="ddd68-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span><span class="sxs-lookup"><span data-stu-id="ddd68-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="ddd68-239">However, there are a few options that you can set to change how the library works.</span><span class="sxs-lookup"><span data-stu-id="ddd68-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="ddd68-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span><span class="sxs-lookup"><span data-stu-id="ddd68-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="ddd68-241">Consider this example:</span><span class="sxs-lookup"><span data-stu-id="ddd68-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="ddd68-242">There are a couple of options that are commonly used:</span><span class="sxs-lookup"><span data-stu-id="ddd68-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="ddd68-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span><span class="sxs-lookup"><span data-stu-id="ddd68-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="ddd68-244">If **false**, then messages are sent individually.</span><span class="sxs-lookup"><span data-stu-id="ddd68-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="ddd68-245">The default is **false**.</span><span class="sxs-lookup"><span data-stu-id="ddd68-245">The default is **false**.</span></span> <span data-ttu-id="ddd68-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span><span class="sxs-lookup"><span data-stu-id="ddd68-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="ddd68-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="ddd68-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="ddd68-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span><span class="sxs-lookup"><span data-stu-id="ddd68-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="ddd68-249">The batching option is important.</span><span class="sxs-lookup"><span data-stu-id="ddd68-249">The batching option is important.</span></span> <span data-ttu-id="ddd68-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="ddd68-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="ddd68-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span><span class="sxs-lookup"><span data-stu-id="ddd68-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="ddd68-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span><span class="sxs-lookup"><span data-stu-id="ddd68-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="ddd68-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span><span class="sxs-lookup"><span data-stu-id="ddd68-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="ddd68-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span><span class="sxs-lookup"><span data-stu-id="ddd68-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="ddd68-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span><span class="sxs-lookup"><span data-stu-id="ddd68-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd68-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="ddd68-256">Next steps</span></span>
<span data-ttu-id="ddd68-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="ddd68-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="ddd68-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="ddd68-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="ddd68-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="ddd68-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ddd68-260">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="ddd68-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ddd68-261">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="ddd68-261">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
