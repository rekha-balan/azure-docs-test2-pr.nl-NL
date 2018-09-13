---
title: Sending push notifications with Azure Notification Hubs on Windows Phone | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.
services: notification-hubs
documentationcenter: windows
keywords: push notification,push notification,windows phone push
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: bd963d263c4e83077edb21946847f78d8448a516
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553575"
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="81f7a-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span><span class="sxs-lookup"><span data-stu-id="81f7a-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="81f7a-105">Overview</span><span class="sxs-lookup"><span data-stu-id="81f7a-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="81f7a-106">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="81f7a-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="81f7a-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="81f7a-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="81f7a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="81f7a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="81f7a-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span><span class="sxs-lookup"><span data-stu-id="81f7a-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="81f7a-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span><span class="sxs-lookup"><span data-stu-id="81f7a-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="81f7a-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="81f7a-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="81f7a-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span><span class="sxs-lookup"><span data-stu-id="81f7a-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="81f7a-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span><span class="sxs-lookup"><span data-stu-id="81f7a-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="81f7a-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span><span class="sxs-lookup"><span data-stu-id="81f7a-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="81f7a-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="81f7a-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81f7a-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="81f7a-116">Prerequisites</span></span>
<span data-ttu-id="81f7a-117">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="81f7a-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="81f7a-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span><span class="sxs-lookup"><span data-stu-id="81f7a-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="81f7a-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span><span class="sxs-lookup"><span data-stu-id="81f7a-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="81f7a-120">Create your notification hub</span><span class="sxs-lookup"><span data-stu-id="81f7a-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="81f7a-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span><span class="sxs-lookup"><span data-stu-id="81f7a-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure Portal - Enable unathenticated push notifications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="81f7a-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="81f7a-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="81f7a-124">This tutorial uses MPNS in unauthenticated mode.</span><span class="sxs-lookup"><span data-stu-id="81f7a-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="81f7a-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span><span class="sxs-lookup"><span data-stu-id="81f7a-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="81f7a-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span><span class="sxs-lookup"><span data-stu-id="81f7a-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="81f7a-127">Connecting your app to the notification hub</span><span class="sxs-lookup"><span data-stu-id="81f7a-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="81f7a-128">In Visual Studio, create a new Windows Phone 8 application.</span><span class="sxs-lookup"><span data-stu-id="81f7a-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="81f7a-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span><span class="sxs-lookup"><span data-stu-id="81f7a-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - New Project - Blank App - Windows Phone Silverlight][11]
2. <span data-ttu-id="81f7a-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="81f7a-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="81f7a-132">This displays the **Manage NuGet Packages** dialog box.</span><span class="sxs-lookup"><span data-stu-id="81f7a-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="81f7a-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="81f7a-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio - NuGet Package Manager][20]
   
    <span data-ttu-id="81f7a-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span><span class="sxs-lookup"><span data-stu-id="81f7a-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="81f7a-136">Open the file App.xaml.cs and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="81f7a-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="81f7a-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="81f7a-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="81f7a-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span><span class="sxs-lookup"><span data-stu-id="81f7a-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="81f7a-139">If there isn't one there, create a new entry with that name.</span><span class="sxs-lookup"><span data-stu-id="81f7a-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="81f7a-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="81f7a-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="81f7a-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="81f7a-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="81f7a-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span><span class="sxs-lookup"><span data-stu-id="81f7a-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="81f7a-143">This tutorial sends a toast notification to the device.</span><span class="sxs-lookup"><span data-stu-id="81f7a-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="81f7a-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span><span class="sxs-lookup"><span data-stu-id="81f7a-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="81f7a-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="81f7a-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="81f7a-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span><span class="sxs-lookup"><span data-stu-id="81f7a-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="81f7a-147">Press the `F5` key to run the app.</span><span class="sxs-lookup"><span data-stu-id="81f7a-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="81f7a-148">A registration message is displayed in the app.</span><span class="sxs-lookup"><span data-stu-id="81f7a-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="81f7a-149">Close the app.</span><span class="sxs-lookup"><span data-stu-id="81f7a-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="81f7a-150">To receive a toast push notification, the application must not be running in the foreground.</span><span class="sxs-lookup"><span data-stu-id="81f7a-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="81f7a-151">Send push notifications from your backend</span><span class="sxs-lookup"><span data-stu-id="81f7a-151">Send push notifications from your backend</span></span>
<span data-ttu-id="81f7a-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span><span class="sxs-lookup"><span data-stu-id="81f7a-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="81f7a-153">In this tutorial, you send push notifications using a .NET console application.</span><span class="sxs-lookup"><span data-stu-id="81f7a-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="81f7a-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="81f7a-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="81f7a-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="81f7a-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="81f7a-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="81f7a-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="81f7a-157">This adds a new Visual C# console application to the solution.</span><span class="sxs-lookup"><span data-stu-id="81f7a-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="81f7a-158">You can also do this in a separate solution.</span><span class="sxs-lookup"><span data-stu-id="81f7a-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="81f7a-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="81f7a-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="81f7a-160">This displays the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="81f7a-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="81f7a-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="81f7a-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="81f7a-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span><span class="sxs-lookup"><span data-stu-id="81f7a-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="81f7a-163">Open the `Program.cs` file and add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="81f7a-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="81f7a-164">In the `Program` class, add the following method:</span><span class="sxs-lookup"><span data-stu-id="81f7a-164">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="81f7a-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span><span class="sxs-lookup"><span data-stu-id="81f7a-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="81f7a-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span><span class="sxs-lookup"><span data-stu-id="81f7a-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="81f7a-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span><span class="sxs-lookup"><span data-stu-id="81f7a-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="81f7a-168">The listen-access string does not have permissions to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="81f7a-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="81f7a-169">Add the following line in your `Main` method:</span><span class="sxs-lookup"><span data-stu-id="81f7a-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="81f7a-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span><span class="sxs-lookup"><span data-stu-id="81f7a-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="81f7a-171">You will receive a toast push notification.</span><span class="sxs-lookup"><span data-stu-id="81f7a-171">You will receive a toast push notification.</span></span> <span data-ttu-id="81f7a-172">Tapping the toast banner loads the app.</span><span class="sxs-lookup"><span data-stu-id="81f7a-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="81f7a-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span><span class="sxs-lookup"><span data-stu-id="81f7a-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81f7a-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="81f7a-174">Next steps</span></span>
<span data-ttu-id="81f7a-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span><span class="sxs-lookup"><span data-stu-id="81f7a-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="81f7a-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span><span class="sxs-lookup"><span data-stu-id="81f7a-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="81f7a-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span><span class="sxs-lookup"><span data-stu-id="81f7a-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="81f7a-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span><span class="sxs-lookup"><span data-stu-id="81f7a-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp









