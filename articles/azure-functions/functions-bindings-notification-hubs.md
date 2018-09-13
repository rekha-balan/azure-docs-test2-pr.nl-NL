---
title: Azure Functions Notification Hub binding | Microsoft Docs
description: Understand how to use Azure Notification Hub binding in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: 7abd7b0921c029ff159935d89905d3c502aba643
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556211"
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="ebb69-104">Azure Functions Notification Hub output binding</span><span class="sxs-lookup"><span data-stu-id="ebb69-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ebb69-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ebb69-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="ebb69-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="ebb69-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="ebb69-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span><span class="sxs-lookup"><span data-stu-id="ebb69-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="ebb69-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span><span class="sxs-lookup"><span data-stu-id="ebb69-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="ebb69-109">The notifications you send can be native notifications or template notifications.</span><span class="sxs-lookup"><span data-stu-id="ebb69-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="ebb69-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span><span class="sxs-lookup"><span data-stu-id="ebb69-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="ebb69-111">A template notification can be used to target multiple platforms.</span><span class="sxs-lookup"><span data-stu-id="ebb69-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="ebb69-112">Notification hub output binding properties</span><span class="sxs-lookup"><span data-stu-id="ebb69-112">Notification hub output binding properties</span></span>
<span data-ttu-id="ebb69-113">The function.json file provides the following properties:</span><span class="sxs-lookup"><span data-stu-id="ebb69-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="ebb69-114">`name` : Variable name used in function code for the notification hub message.</span><span class="sxs-lookup"><span data-stu-id="ebb69-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="ebb69-115">`type` : must be set to *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="ebb69-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="ebb69-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span><span class="sxs-lookup"><span data-stu-id="ebb69-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="ebb69-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ebb69-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="ebb69-118">`hubName` : Name of the notification hub resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ebb69-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="ebb69-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span><span class="sxs-lookup"><span data-stu-id="ebb69-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="ebb69-120">`direction` : must be set to *"out"*.</span><span class="sxs-lookup"><span data-stu-id="ebb69-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="ebb69-121">`platform` : The platform property indicates the notification platform your notification targets.</span><span class="sxs-lookup"><span data-stu-id="ebb69-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="ebb69-122">Must be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="ebb69-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="ebb69-123">`template` : This is the default platform if the platform property is omitted from the output binding.</span><span class="sxs-lookup"><span data-stu-id="ebb69-123">`template` : This is the default platform if the platform property is omitted from the output binding.</span></span> <span data-ttu-id="ebb69-124">Template notifications can be used to target any platform configured on the Azure Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="ebb69-124">Template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="ebb69-125">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="ebb69-125">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="ebb69-126">`apns` : Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="ebb69-126">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="ebb69-127">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ebb69-127">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="ebb69-128">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="ebb69-128">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="ebb69-129">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="ebb69-129">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="ebb69-130">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="ebb69-130">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="ebb69-131">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span><span class="sxs-lookup"><span data-stu-id="ebb69-131">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="ebb69-132">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ebb69-132">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="ebb69-133">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span><span class="sxs-lookup"><span data-stu-id="ebb69-133">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="ebb69-134">Windows Phone 8.1 and later is also supported by WNS.</span><span class="sxs-lookup"><span data-stu-id="ebb69-134">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="ebb69-135">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="ebb69-135">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="ebb69-136">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebb69-136">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="ebb69-137">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span><span class="sxs-lookup"><span data-stu-id="ebb69-137">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="ebb69-138">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="ebb69-138">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="ebb69-139">Example function.json:</span><span class="sxs-lookup"><span data-stu-id="ebb69-139">Example function.json:</span></span>

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="ebb69-140">Notification hub connection string setup</span><span class="sxs-lookup"><span data-stu-id="ebb69-140">Notification hub connection string setup</span></span>
<span data-ttu-id="ebb69-141">To use a Notification hub output binding, you must configure the connection string for the hub.</span><span class="sxs-lookup"><span data-stu-id="ebb69-141">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="ebb69-142">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span><span class="sxs-lookup"><span data-stu-id="ebb69-142">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="ebb69-143">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span><span class="sxs-lookup"><span data-stu-id="ebb69-143">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="ebb69-144">This connection string provides your function access permission to send notification messages.</span><span class="sxs-lookup"><span data-stu-id="ebb69-144">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="ebb69-145">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ebb69-145">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="ebb69-146">To manually add a connection string for your hub, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ebb69-146">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="ebb69-147">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span><span class="sxs-lookup"><span data-stu-id="ebb69-147">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="ebb69-148">In the **Settings** blade, click **Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="ebb69-148">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="ebb69-149">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span><span class="sxs-lookup"><span data-stu-id="ebb69-149">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="ebb69-150">Reference your App setting string name in the output bindings.</span><span class="sxs-lookup"><span data-stu-id="ebb69-150">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="ebb69-151">Similar to **MyHubConnectionString** used in the example above.</span><span class="sxs-lookup"><span data-stu-id="ebb69-151">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="ebb69-152">APNS native notifications with C# queue triggers</span><span class="sxs-lookup"><span data-stu-id="ebb69-152">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="ebb69-153">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span><span class="sxs-lookup"><span data-stu-id="ebb69-153">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="ebb69-154">GCM native notifications with C# queue triggers</span><span class="sxs-lookup"><span data-stu-id="ebb69-154">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="ebb69-155">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span><span class="sxs-lookup"><span data-stu-id="ebb69-155">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="ebb69-156">WNS native notifications with C# queue triggers</span><span class="sxs-lookup"><span data-stu-id="ebb69-156">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="ebb69-157">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span><span class="sxs-lookup"><span data-stu-id="ebb69-157">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="ebb69-158">Template example for Node.js timer triggers</span><span class="sxs-lookup"><span data-stu-id="ebb69-158">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="ebb69-159">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span><span class="sxs-lookup"><span data-stu-id="ebb69-159">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="ebb69-160">Template example for F# timer triggers</span><span class="sxs-lookup"><span data-stu-id="ebb69-160">Template example for F# timer triggers</span></span>
<span data-ttu-id="ebb69-161">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span><span class="sxs-lookup"><span data-stu-id="ebb69-161">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="ebb69-162">Template example using an out parameter</span><span class="sxs-lookup"><span data-stu-id="ebb69-162">Template example using an out parameter</span></span>
<span data-ttu-id="ebb69-163">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span><span class="sxs-lookup"><span data-stu-id="ebb69-163">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="ebb69-164">Template example with asynchronous function</span><span class="sxs-lookup"><span data-stu-id="ebb69-164">Template example with asynchronous function</span></span>
<span data-ttu-id="ebb69-165">If you are using asynchronous code, out parameters are not allowed.</span><span class="sxs-lookup"><span data-stu-id="ebb69-165">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="ebb69-166">In this case use `IAsyncCollector` to return your template notification.</span><span class="sxs-lookup"><span data-stu-id="ebb69-166">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="ebb69-167">The following code is an asynchronous example of the code above.</span><span class="sxs-lookup"><span data-stu-id="ebb69-167">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="ebb69-168">Template example using JSON</span><span class="sxs-lookup"><span data-stu-id="ebb69-168">Template example using JSON</span></span>
<span data-ttu-id="ebb69-169">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span><span class="sxs-lookup"><span data-stu-id="ebb69-169">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="ebb69-170">Template example using Notification Hubs library types</span><span class="sxs-lookup"><span data-stu-id="ebb69-170">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="ebb69-171">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ebb69-171">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a><span data-ttu-id="ebb69-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="ebb69-172">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

