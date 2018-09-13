---
title: Get started with Azure Notification Hubs for Windows Universal Platform Apps | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to push notifications to a Windows Universal Platform application.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 0d6aa9367b0b35ed8058466a36b6961052f58a55
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554617"
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="c0966-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span><span class="sxs-lookup"><span data-stu-id="c0966-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c0966-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c0966-104">Overview</span></span>
<span data-ttu-id="c0966-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span><span class="sxs-lookup"><span data-stu-id="c0966-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="c0966-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="c0966-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="c0966-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span><span class="sxs-lookup"><span data-stu-id="c0966-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0966-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c0966-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="c0966-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="c0966-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0966-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c0966-110">Prerequisites</span></span>
<span data-ttu-id="c0966-111">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="c0966-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="c0966-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span><span class="sxs-lookup"><span data-stu-id="c0966-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="c0966-113">Universal Windows App Development Tools installed</span><span class="sxs-lookup"><span data-stu-id="c0966-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="c0966-114">An active Azure account</span><span class="sxs-lookup"><span data-stu-id="c0966-114">An active Azure account</span></span> <br/><span data-ttu-id="c0966-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="c0966-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c0966-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="c0966-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="c0966-117">An active Windows Store account</span><span class="sxs-lookup"><span data-stu-id="c0966-117">An active Windows Store account</span></span>

<span data-ttu-id="c0966-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span><span class="sxs-lookup"><span data-stu-id="c0966-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="c0966-119">Register your app for the Windows Store</span><span class="sxs-lookup"><span data-stu-id="c0966-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="c0966-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span><span class="sxs-lookup"><span data-stu-id="c0966-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="c0966-121">You must then configure your notification hub to integrate with WNS.</span><span class="sxs-lookup"><span data-stu-id="c0966-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="c0966-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span><span class="sxs-lookup"><span data-stu-id="c0966-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>
2. <span data-ttu-id="c0966-123">Type a name for your app and click **Reserve app name**.</span><span class="sxs-lookup"><span data-stu-id="c0966-123">Type a name for your app and click **Reserve app name**.</span></span>
   
       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hubs-win8-app-name.png)
   
       This creates a new Windows Store registration for your app.
3. <span data-ttu-id="c0966-124">In Visual Studio, create a new Visual C# Store Apps project by using the **Blank App** template and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0966-124">In Visual Studio, create a new Visual C# Store Apps project by using the **Blank App** template and click **OK**.</span></span>
   
       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-windows-universal-app.png)
4. <span data-ttu-id="c0966-125">Accept the defaults for the target and minimum platform versions.</span><span class="sxs-lookup"><span data-stu-id="c0966-125">Accept the defaults for the target and minimum platform versions.</span></span>
5. <span data-ttu-id="c0966-126">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span><span class="sxs-lookup"><span data-stu-id="c0966-126">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span>
   
       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-associate-win8-app.png)

       The **Associate Your App with the Windows Store** wizard appears.

1. <span data-ttu-id="c0966-127">In the wizard, click **Sign in** and then sign in with your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="c0966-127">In the wizard, click **Sign in** and then sign in with your Microsoft account.</span></span>
2. <span data-ttu-id="c0966-128">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span><span class="sxs-lookup"><span data-stu-id="c0966-128">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span>
   
       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-associate-app-name.png)
   
       This adds the required Windows Store registration information to the application manifest.
3. <span data-ttu-id="c0966-129">Back on the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?LinkID=266582) page for your new app, click **Services**, click **Push notifications**, and then click **Live Services site** under **Windows Push Notification Services (WNS) and Microsoft Azure Mobile Apps**.</span><span class="sxs-lookup"><span data-stu-id="c0966-129">Back on the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?LinkID=266582) page for your new app, click **Services**, click **Push notifications**, and then click **Live Services site** under **Windows Push Notification Services (WNS) and Microsoft Azure Mobile Apps**.</span></span>
   
       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hubs-uwp-app-live-services.png)
4. <span data-ttu-id="c0966-130">On the registration page for your app, make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span><span class="sxs-lookup"><span data-stu-id="c0966-130">On the registration page for your app, make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>
   
       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hubs-uwp-app-push-auth.png)

     > [AZURE.WARNING]
    <span data-ttu-id="c0966-131">The application secret and package SID are important security credentials.</span><span class="sxs-lookup"><span data-stu-id="c0966-131">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="c0966-132">Do not share these values with anyone or distribute them with your app.</span><span class="sxs-lookup"><span data-stu-id="c0966-132">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="c0966-133">Configure your notification hub</span><span class="sxs-lookup"><span data-stu-id="c0966-133">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="c0966-134">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span><span class="sxs-lookup"><span data-stu-id="c0966-134">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="c0966-135">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span><span class="sxs-lookup"><span data-stu-id="c0966-135">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="c0966-136">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span><span class="sxs-lookup"><span data-stu-id="c0966-136">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="c0966-137">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span><span class="sxs-lookup"><span data-stu-id="c0966-137">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="c0966-138">Connect your app to the notification hub</span><span class="sxs-lookup"><span data-stu-id="c0966-138">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="c0966-139">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c0966-139">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="c0966-140">This displays the **Manage NuGet Packages** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c0966-140">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="c0966-141">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="c0966-141">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="c0966-142">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span><span class="sxs-lookup"><span data-stu-id="c0966-142">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="c0966-143">Open the App.xaml.cs project file and add the following `using` statements.</span><span class="sxs-lookup"><span data-stu-id="c0966-143">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="c0966-144">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="c0966-144">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="c0966-145">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="c0966-145">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c0966-146">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c0966-146">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="c0966-147">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span><span class="sxs-lookup"><span data-stu-id="c0966-147">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="c0966-148">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span><span class="sxs-lookup"><span data-stu-id="c0966-148">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="c0966-149">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span><span class="sxs-lookup"><span data-stu-id="c0966-149">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="c0966-150">Press the **F5** key to run the app.</span><span class="sxs-lookup"><span data-stu-id="c0966-150">Press the **F5** key to run the app.</span></span> <span data-ttu-id="c0966-151">A pop-up dialog that contains the registration key is displayed.</span><span class="sxs-lookup"><span data-stu-id="c0966-151">A pop-up dialog that contains the registration key is displayed.</span></span>
   
       ![][19]

<span data-ttu-id="c0966-152">Your app is now ready to receive toast notifications.</span><span class="sxs-lookup"><span data-stu-id="c0966-152">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="c0966-153">Send notifications</span><span class="sxs-lookup"><span data-stu-id="c0966-153">Send notifications</span></span>
<span data-ttu-id="c0966-154">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span><span class="sxs-lookup"><span data-stu-id="c0966-154">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="c0966-155">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span><span class="sxs-lookup"><span data-stu-id="c0966-155">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="c0966-156">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span><span class="sxs-lookup"><span data-stu-id="c0966-156">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="c0966-157">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span><span class="sxs-lookup"><span data-stu-id="c0966-157">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="c0966-158">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span><span class="sxs-lookup"><span data-stu-id="c0966-158">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="c0966-159">However, the following approaches can be used for sending notifications:</span><span class="sxs-lookup"><span data-stu-id="c0966-159">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="c0966-160">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0966-160">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="c0966-161">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="c0966-161">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="c0966-162">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c0966-162">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="c0966-163">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="c0966-163">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="c0966-164">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="c0966-164">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="c0966-165">(Optional) Send notifications from a console app</span><span class="sxs-lookup"><span data-stu-id="c0966-165">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="c0966-166">To send notifications by using a .NET console application follow these steps.</span><span class="sxs-lookup"><span data-stu-id="c0966-166">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="c0966-167">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0966-167">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![][13]
   
    <span data-ttu-id="c0966-168">This adds a new Visual C# console application to the solution.</span><span class="sxs-lookup"><span data-stu-id="c0966-168">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="c0966-169">You can also do this in a separate solution.</span><span class="sxs-lookup"><span data-stu-id="c0966-169">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="c0966-170">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="c0966-170">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="c0966-171">This displays the Package Manager Console in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0966-171">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="c0966-172">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="c0966-172">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="c0966-173">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span><span class="sxs-lookup"><span data-stu-id="c0966-173">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="c0966-174">Open the Program.cs file and add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="c0966-174">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="c0966-175">In the **Program** class, add the following method:</span><span class="sxs-lookup"><span data-stu-id="c0966-175">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="c0966-176">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span><span class="sxs-lookup"><span data-stu-id="c0966-176">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="c0966-177">The listen-access string does not have permissions to send notifications.</span><span class="sxs-lookup"><span data-stu-id="c0966-177">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="c0966-178">Add the following lines in the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="c0966-178">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="c0966-179">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span><span class="sxs-lookup"><span data-stu-id="c0966-179">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="c0966-180">Then press the **F5** key to run the application.</span><span class="sxs-lookup"><span data-stu-id="c0966-180">Then press the **F5** key to run the application.</span></span>
   
       ![][14]
   
    <span data-ttu-id="c0966-181">You will receive a toast notification on all registered devices.</span><span class="sxs-lookup"><span data-stu-id="c0966-181">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="c0966-182">Clicking or tapping the toast banner loads the app.</span><span class="sxs-lookup"><span data-stu-id="c0966-182">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="c0966-183">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span><span class="sxs-lookup"><span data-stu-id="c0966-183">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0966-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0966-184">Next steps</span></span>
<span data-ttu-id="c0966-185">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span><span class="sxs-lookup"><span data-stu-id="c0966-185">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="c0966-186">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span><span class="sxs-lookup"><span data-stu-id="c0966-186">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="c0966-187">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span><span class="sxs-lookup"><span data-stu-id="c0966-187">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="c0966-188">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span><span class="sxs-lookup"><span data-stu-id="c0966-188">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="c0966-189">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0966-189">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx













