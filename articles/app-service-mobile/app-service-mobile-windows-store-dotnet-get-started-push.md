---
title: Add push notifications to your Universal Windows Platform (UWP) app | Microsoft Docs
description: Learn how to use Azure App Service Mobile Apps and Azure Notification Hubs to send push notifications to your Universal Windows Platform (UWP) app.
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: conceptdev
manager: crdun
editor: ''
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: crdun
ms.openlocfilehash: bfbb72d6fd101932f00e12ad18ab079ec30a0d3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824558"
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="5530b-103">Add push notifications to your Windows app</span><span class="sxs-lookup"><span data-stu-id="5530b-103">Add push notifications to your Windows app</span></span>

[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="5530b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5530b-104">Overview</span></span>

<span data-ttu-id="5530b-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="5530b-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="5530b-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="5530b-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="5530b-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="5530b-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="configure-hub"></a><span data-ttu-id="5530b-108">Configure a Notification Hub</span><span class="sxs-lookup"><span data-stu-id="5530b-108">Configure a Notification Hub</span></span>

[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="5530b-109">Register your app for push notifications</span><span class="sxs-lookup"><span data-stu-id="5530b-109">Register your app for push notifications</span></span>

<span data-ttu-id="5530b-110">You need to submit your app to the Microsoft Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span><span class="sxs-lookup"><span data-stu-id="5530b-110">You need to submit your app to the Microsoft Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="5530b-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span><span class="sxs-lookup"><span data-stu-id="5530b-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Associate app with Microsoft Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="5530b-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span><span class="sxs-lookup"><span data-stu-id="5530b-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="5530b-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span><span class="sxs-lookup"><span data-stu-id="5530b-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="5530b-115">This adds the required Microsoft Store registration information to the application manifest.</span><span class="sxs-lookup"><span data-stu-id="5530b-115">This adds the required Microsoft Store registration information to the application manifest.</span></span>
4. <span data-ttu-id="5530b-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span><span class="sxs-lookup"><span data-stu-id="5530b-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="5530b-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="5530b-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="5530b-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="5530b-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Associate app with Microsoft Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="5530b-120">The client secret and package SID are important security credentials.</span><span class="sxs-lookup"><span data-stu-id="5530b-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="5530b-121">Do not share these values with anyone or distribute them with your app.</span><span class="sxs-lookup"><span data-stu-id="5530b-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="5530b-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span><span class="sxs-lookup"><span data-stu-id="5530b-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="5530b-123">Configure the backend to send push notifications</span><span class="sxs-lookup"><span data-stu-id="5530b-123">Configure the backend to send push notifications</span></span>

[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a><span data-ttu-id="5530b-124">Update the server to send push notifications</span><span class="sxs-lookup"><span data-stu-id="5530b-124">Update the server to send push notifications</span></span>

<span data-ttu-id="5530b-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="5530b-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <a name="dotnet"></a><span data-ttu-id="5530b-126">.NET backend project</span><span class="sxs-lookup"><span data-stu-id="5530b-126">.NET backend project</span></span>

1. <span data-ttu-id="5530b-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="5530b-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="5530b-128">This installs the Notification Hubs client library.</span><span class="sxs-lookup"><span data-stu-id="5530b-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="5530b-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span><span class="sxs-lookup"><span data-stu-id="5530b-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

    ```csharp
    using System.Collections.Generic;
    using Microsoft.Azure.NotificationHubs;
    using Microsoft.Azure.Mobile.Server.Config;
    ```

3. <span data-ttu-id="5530b-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="5530b-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

    ```csharp
    // Get the settings for the server project.
    HttpConfiguration config = this.Configuration;
    MobileAppSettingsDictionary settings =
        this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

    // Get the Notification Hubs credentials for the Mobile App.
    string notificationHubName = settings.NotificationHubName;
    string notificationHubConnection = settings
        .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

    // Create the notification hub client.
    NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

    // Define a WNS payload
    var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                            + item.Text + @"</text></binding></visual></toast>";
    try
    {
        // Send the push notification.
        var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

        // Write the success result to the logs.
        config.Services.GetTraceWriter().Info(result.State.ToString());
    }
    catch (System.Exception ex)
    {
        // Write the failure result to the logs.
        config.Services.GetTraceWriter()
            .Error(ex.Message, null, "Push.SendAsync Error");
    }
    ```

    <span data-ttu-id="5530b-131">This code tells the notification hub to send a push notification after a new item is insertion.</span><span class="sxs-lookup"><span data-stu-id="5530b-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>

4. <span data-ttu-id="5530b-132">Republish the server project.</span><span class="sxs-lookup"><span data-stu-id="5530b-132">Republish the server project.</span></span>

### <a name="nodejs"></a><span data-ttu-id="5530b-133">Node.js backend project</span><span class="sxs-lookup"><span data-stu-id="5530b-133">Node.js backend project</span></span>
1. <span data-ttu-id="5530b-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="5530b-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="5530b-135">Replace the existing code in the todoitem.js file with the following:</span><span class="sxs-lookup"><span data-stu-id="5530b-135">Replace the existing code in the todoitem.js file with the following:</span></span>

    ```javascript
    var azureMobileApps = require('azure-mobile-apps'),
    promises = require('azure-mobile-apps/src/utilities/promises'),
    logger = require('azure-mobile-apps/src/logger');

    var table = azureMobileApps.table();

    table.insert(function (context) {
    // For more information about the Notification Hubs JavaScript SDK,
    // see http://aka.ms/nodejshubs
    logger.info('Running TodoItem.insert');

    // Define the WNS payload that contains the new item Text.
    var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                + context.item.text + "</text></binding></visual></toast>";

    // Execute the insert.  The insert returns the results as a Promise,
    // Do the push as a post-execute action within the promise flow.
    return context.execute()
        .then(function (results) {
            // Only do the push if configured
            if (context.push) {
                // Send a WNS native toast notification.
                context.push.wns.sendToast(null, payload, function (error) {
                    if (error) {
                        logger.error('Error while sending push notification: ', error);
                    } else {
                        logger.info('Push notification sent successfully!');
                    }
                });
            }
            // Don't forget to return the results from the context.execute()
            return results;
        })
        .catch(function (error) {
            logger.error('Error while running context.execute: ', error);
        });
    });

    module.exports = table;
    ```

    <span data-ttu-id="5530b-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span><span class="sxs-lookup"><span data-stu-id="5530b-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>

3. <span data-ttu-id="5530b-137">When editing the file on your local computer, republish the server project.</span><span class="sxs-lookup"><span data-stu-id="5530b-137">When editing the file on your local computer, republish the server project.</span></span>

## <a id="update-app"></a><span data-ttu-id="5530b-138">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="5530b-138">Add push notifications to your app</span></span>
<span data-ttu-id="5530b-139">Next, your app must register for push notifications on start-up.</span><span class="sxs-lookup"><span data-stu-id="5530b-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="5530b-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span><span class="sxs-lookup"><span data-stu-id="5530b-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="5530b-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="5530b-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

    ```csharp
    using System.Threading.Tasks;
    using Windows.Networking.PushNotifications;
    ```

2. <span data-ttu-id="5530b-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="5530b-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

    ```csharp
    private async Task InitNotificationsAsync()
    {
        // Get a channel URI from WNS.
        var channel = await PushNotificationChannelManager
            .CreatePushNotificationChannelForApplicationAsync();

        // Register the channel URI with Notification Hubs.
        await App.MobileService.GetPush().RegisterAsync(channel.Uri);
    }
    ```

    <span data-ttu-id="5530b-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span><span class="sxs-lookup"><span data-stu-id="5530b-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>

3. <span data-ttu-id="5530b-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="5530b-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

    ```csharp
    protected async override void OnLaunched(LaunchActivatedEventArgs e)
    {
        await InitNotificationsAsync();

        // ...
    }
    ```

    <span data-ttu-id="5530b-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span><span class="sxs-lookup"><span data-stu-id="5530b-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>

4. <span data-ttu-id="5530b-146">Rebuild your UWP app project.</span><span class="sxs-lookup"><span data-stu-id="5530b-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="5530b-147">Your app is now ready to receive toast notifications.</span><span class="sxs-lookup"><span data-stu-id="5530b-147">Your app is now ready to receive toast notifications.</span></span>

## <a id="test"></a><span data-ttu-id="5530b-148">Test push notifications in your app</span><span class="sxs-lookup"><span data-stu-id="5530b-148">Test push notifications in your app</span></span>

[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a><span data-ttu-id="5530b-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="5530b-149">Next steps</span></span>

<span data-ttu-id="5530b-150">Learn more about push notifications:</span><span class="sxs-lookup"><span data-stu-id="5530b-150">Learn more about push notifications:</span></span>

* <span data-ttu-id="5530b-151">[How to use the managed client for Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications) Templates give you flexibility to send cross-platform pushes and localized pushes.</span><span class="sxs-lookup"><span data-stu-id="5530b-151">[How to use the managed client for Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications) Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="5530b-152">Learn how to register templates.</span><span class="sxs-lookup"><span data-stu-id="5530b-152">Learn how to register templates.</span></span>
* <span data-ttu-id="5530b-153">[Diagnose push notification issues](../notification-hubs/notification-hubs-push-notification-fixer.md) There are various reasons why notifications may get dropped or do not end up on devices.</span><span class="sxs-lookup"><span data-stu-id="5530b-153">[Diagnose push notification issues](../notification-hubs/notification-hubs-push-notification-fixer.md) There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="5530b-154">This topic shows you how to analyze and figure out the root cause of push notification failures.</span><span class="sxs-lookup"><span data-stu-id="5530b-154">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="5530b-155">Consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="5530b-155">Consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="5530b-156">[Add authentication to your app](app-service-mobile-windows-store-dotnet-get-started-users.md) Learn how to authenticate users of your app with an identity provider.</span><span class="sxs-lookup"><span data-stu-id="5530b-156">[Add authentication to your app](app-service-mobile-windows-store-dotnet-get-started-users.md) Learn how to authenticate users of your app with an identity provider.</span></span>
* <span data-ttu-id="5530b-157">[Enable offline sync for your app](app-service-mobile-windows-store-dotnet-get-started-offline-data.md) Learn how to add offline support your app using an Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="5530b-157">[Enable offline sync for your app](app-service-mobile-windows-store-dotnet-get-started-offline-data.md) Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="5530b-158">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="5530b-158">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
