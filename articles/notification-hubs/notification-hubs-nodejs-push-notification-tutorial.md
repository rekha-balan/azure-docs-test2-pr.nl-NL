---
title: Sending push notifications with Azure Notification Hubs and Node.js
description: Learn how to use Notification Hubs to send push notifications from a Node.js application.
keywords: push notification,push notifications,node.js push,ios push
services: notification-hubs
documentationcenter: nodejs
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 49ee6b7fabe78c2328a2a772347c612ad38cfe7a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775937"
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="3e101-104">Sending push notifications with Azure Notification Hubs and Node.js</span><span class="sxs-lookup"><span data-stu-id="3e101-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="3e101-105">Overview</span><span class="sxs-lookup"><span data-stu-id="3e101-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3e101-106">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="3e101-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3e101-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="3e101-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3e101-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="3e101-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="3e101-109">This guide shows you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="3e101-109">This guide shows you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="3e101-110">The scenarios covered include sending push notifications to applications on the following platforms:</span><span class="sxs-lookup"><span data-stu-id="3e101-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="3e101-111">Android</span><span class="sxs-lookup"><span data-stu-id="3e101-111">Android</span></span>
* <span data-ttu-id="3e101-112">iOS</span><span class="sxs-lookup"><span data-stu-id="3e101-112">iOS</span></span>
* <span data-ttu-id="3e101-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3e101-113">Windows Phone</span></span>
* <span data-ttu-id="3e101-114">Universal Windows Platform</span><span class="sxs-lookup"><span data-stu-id="3e101-114">Universal Windows Platform</span></span> 

<span data-ttu-id="3e101-115">For more information on notification hubs, see the [Next Steps](#next) section.</span><span class="sxs-lookup"><span data-stu-id="3e101-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="3e101-116">What are Notification Hubs?</span><span class="sxs-lookup"><span data-stu-id="3e101-116">What are Notification Hubs?</span></span>
<span data-ttu-id="3e101-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span><span class="sxs-lookup"><span data-stu-id="3e101-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="3e101-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="3e101-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="3e101-119">Create a Node.js Application</span><span class="sxs-lookup"><span data-stu-id="3e101-119">Create a Node.js Application</span></span>
<span data-ttu-id="3e101-120">The first step in this tutorial is creating a new blank Node.js application.</span><span class="sxs-lookup"><span data-stu-id="3e101-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="3e101-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix][webmatrix].</span><span class="sxs-lookup"><span data-stu-id="3e101-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix][webmatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="3e101-122">Configure Your Application to Use Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="3e101-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="3e101-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span><span class="sxs-lookup"><span data-stu-id="3e101-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="3e101-124">Use Node Package Manager (NPM) to obtain the package</span><span class="sxs-lookup"><span data-stu-id="3e101-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="3e101-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span><span class="sxs-lookup"><span data-stu-id="3e101-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="3e101-126">Type **npm install azure-sb** in the command window.</span><span class="sxs-lookup"><span data-stu-id="3e101-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="3e101-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="3e101-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="3e101-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="3e101-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3e101-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="3e101-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="3e101-130">Import the module</span><span class="sxs-lookup"><span data-stu-id="3e101-130">Import the module</span></span>
<span data-ttu-id="3e101-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span><span class="sxs-lookup"><span data-stu-id="3e101-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="set-up-an-azure-notification-hub-connection"></a><span data-ttu-id="3e101-132">Set up an Azure Notification Hub connection</span><span class="sxs-lookup"><span data-stu-id="3e101-132">Set up an Azure Notification Hub connection</span></span>
<span data-ttu-id="3e101-133">The **NotificationHubService** object lets you work with notification hubs.</span><span class="sxs-lookup"><span data-stu-id="3e101-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="3e101-134">The following code creates a **NotificationHubService** object for the notification hub named **hubname**.</span><span class="sxs-lookup"><span data-stu-id="3e101-134">The following code creates a **NotificationHubService** object for the notification hub named **hubname**.</span></span> <span data-ttu-id="3e101-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span><span class="sxs-lookup"><span data-stu-id="3e101-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="3e101-136">The connection **connectionstring** value can be obtained from the [Azure portal] by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="3e101-136">The connection **connectionstring** value can be obtained from the [Azure portal] by performing the following steps:</span></span>

1. <span data-ttu-id="3e101-137">In the left navigation pane, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="3e101-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="3e101-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span><span class="sxs-lookup"><span data-stu-id="3e101-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="3e101-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="3e101-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="3e101-140">Select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="3e101-140">Select **Settings**.</span></span>
4. <span data-ttu-id="3e101-141">Click on **Access Policies**.</span><span class="sxs-lookup"><span data-stu-id="3e101-141">Click on **Access Policies**.</span></span> <span data-ttu-id="3e101-142">You see both shared and full access connection strings.</span><span class="sxs-lookup"><span data-stu-id="3e101-142">You see both shared and full access connection strings.</span></span>

![Azure portal - Notification Hubs](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="3e101-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3e101-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="3e101-145">General architecture</span><span class="sxs-lookup"><span data-stu-id="3e101-145">General architecture</span></span>
<span data-ttu-id="3e101-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span><span class="sxs-lookup"><span data-stu-id="3e101-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="3e101-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="3e101-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="3e101-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="3e101-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="3e101-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="3e101-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="3e101-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="3e101-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="3e101-151">How to: Send push notifications to Android applications</span><span class="sxs-lookup"><span data-stu-id="3e101-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="3e101-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span><span class="sxs-lookup"><span data-stu-id="3e101-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="3e101-153">The **send** method accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3e101-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3e101-154">**Tags** - the tag identifier.</span><span class="sxs-lookup"><span data-stu-id="3e101-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3e101-155">If no tag is provided, the notification is sent to all clients.</span><span class="sxs-lookup"><span data-stu-id="3e101-155">If no tag is provided, the notification is sent to all clients.</span></span>
* <span data-ttu-id="3e101-156">**Payload** - the message's JSON or raw string payload.</span><span class="sxs-lookup"><span data-stu-id="3e101-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="3e101-157">**Callback** - the callback function.</span><span class="sxs-lookup"><span data-stu-id="3e101-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="3e101-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span><span class="sxs-lookup"><span data-stu-id="3e101-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="3e101-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span><span class="sxs-lookup"><span data-stu-id="3e101-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="3e101-160">How to: Send push notifications to iOS applications</span><span class="sxs-lookup"><span data-stu-id="3e101-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="3e101-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span><span class="sxs-lookup"><span data-stu-id="3e101-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="3e101-162">The **send** method accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3e101-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3e101-163">**Tags** - the tag identifier.</span><span class="sxs-lookup"><span data-stu-id="3e101-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3e101-164">If no tag is provided, the notification is sent to all clients.</span><span class="sxs-lookup"><span data-stu-id="3e101-164">If no tag is provided, the notification is sent to all clients.</span></span>
* <span data-ttu-id="3e101-165">**Payload** - the message's JSON or string payload.</span><span class="sxs-lookup"><span data-stu-id="3e101-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="3e101-166">**Callback** - the callback function.</span><span class="sxs-lookup"><span data-stu-id="3e101-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="3e101-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span><span class="sxs-lookup"><span data-stu-id="3e101-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="3e101-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span><span class="sxs-lookup"><span data-stu-id="3e101-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="3e101-169">How to: Send push notifications to Windows Phone applications</span><span class="sxs-lookup"><span data-stu-id="3e101-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="3e101-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span><span class="sxs-lookup"><span data-stu-id="3e101-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="3e101-171">The **send** method accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3e101-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3e101-172">**Tags** - the tag identifier.</span><span class="sxs-lookup"><span data-stu-id="3e101-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3e101-173">If no tag is provided, the notification is sent to all clients.</span><span class="sxs-lookup"><span data-stu-id="3e101-173">If no tag is provided, the notification is sent to all clients.</span></span>
* <span data-ttu-id="3e101-174">**Payload** - the message's XML payload.</span><span class="sxs-lookup"><span data-stu-id="3e101-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="3e101-175">**TargetName** - `toast` for toast notifications.</span><span class="sxs-lookup"><span data-stu-id="3e101-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="3e101-176">`token` for tile notifications.</span><span class="sxs-lookup"><span data-stu-id="3e101-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="3e101-177">**NotificationClass** - The priority of the notification.</span><span class="sxs-lookup"><span data-stu-id="3e101-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="3e101-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span><span class="sxs-lookup"><span data-stu-id="3e101-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="3e101-179">**Options** - optional request headers.</span><span class="sxs-lookup"><span data-stu-id="3e101-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="3e101-180">**Callback** - the callback function.</span><span class="sxs-lookup"><span data-stu-id="3e101-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="3e101-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="3e101-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="3e101-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span><span class="sxs-lookup"><span data-stu-id="3e101-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="3e101-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span><span class="sxs-lookup"><span data-stu-id="3e101-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="3e101-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span><span class="sxs-lookup"><span data-stu-id="3e101-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="3e101-185">The **send** method accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3e101-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3e101-186">**Tags** - the tag identifier.</span><span class="sxs-lookup"><span data-stu-id="3e101-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3e101-187">If no tag is provided, the notification is sent to all registered clients.</span><span class="sxs-lookup"><span data-stu-id="3e101-187">If no tag is provided, the notification is sent to all registered clients.</span></span>
* <span data-ttu-id="3e101-188">**Payload** - the XML message payload.</span><span class="sxs-lookup"><span data-stu-id="3e101-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="3e101-189">**Type** - the notification type.</span><span class="sxs-lookup"><span data-stu-id="3e101-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="3e101-190">**Options** - optional request headers.</span><span class="sxs-lookup"><span data-stu-id="3e101-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="3e101-191">**Callback** - the callback function.</span><span class="sxs-lookup"><span data-stu-id="3e101-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="3e101-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e101-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="3e101-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span><span class="sxs-lookup"><span data-stu-id="3e101-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="3e101-194">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3e101-194">Next Steps</span></span>
<span data-ttu-id="3e101-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span><span class="sxs-lookup"><span data-stu-id="3e101-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="3e101-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span><span class="sxs-lookup"><span data-stu-id="3e101-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="3e101-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e101-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="3e101-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span><span class="sxs-lookup"><span data-stu-id="3e101-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs
[webmatrix]: https://docs.microsoft.com/aspnet/web-pages/videos/introduction/create-a-website-using-webmatrix
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com
