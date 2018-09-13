---
title: Azure Notification Hubs Secure Push
description: Learn how to send secure push notifications in Azure. Code samples written in C# using the .NET API.
documentationcenter: windows
author: ysxu
manager: erikre
editor: ''
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 585263ae1fc49770b1095cda6b7b7dfc5ab069f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671088"
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="66119-104">Azure Notification Hubs Secure Push</span><span class="sxs-lookup"><span data-stu-id="66119-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="66119-108">Overview</span><span class="sxs-lookup"><span data-stu-id="66119-108">Overview</span></span>
<span data-ttu-id="66119-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span><span class="sxs-lookup"><span data-stu-id="66119-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="66119-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span><span class="sxs-lookup"><span data-stu-id="66119-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="66119-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span><span class="sxs-lookup"><span data-stu-id="66119-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="66119-112">At a high level, the flow is as follows:</span><span class="sxs-lookup"><span data-stu-id="66119-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="66119-113">The app back-end:</span><span class="sxs-lookup"><span data-stu-id="66119-113">The app back-end:</span></span>
   * <span data-ttu-id="66119-114">Stores secure payload in back-end database.</span><span class="sxs-lookup"><span data-stu-id="66119-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="66119-115">Sends the ID of this notification to the device (no secure information is sent).</span><span class="sxs-lookup"><span data-stu-id="66119-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="66119-116">The app on the device, when receiving the notification:</span><span class="sxs-lookup"><span data-stu-id="66119-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="66119-117">The device contacts the back-end requesting the secure payload.</span><span class="sxs-lookup"><span data-stu-id="66119-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="66119-118">The app can show the payload as a notification on the device.</span><span class="sxs-lookup"><span data-stu-id="66119-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="66119-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span><span class="sxs-lookup"><span data-stu-id="66119-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="66119-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span><span class="sxs-lookup"><span data-stu-id="66119-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="66119-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span><span class="sxs-lookup"><span data-stu-id="66119-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="66119-122">The app then authenticates the user and shows the notification payload.</span><span class="sxs-lookup"><span data-stu-id="66119-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="66119-123">This Secure Push tutorial shows how to send a push notification securely.</span><span class="sxs-lookup"><span data-stu-id="66119-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="66119-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span><span class="sxs-lookup"><span data-stu-id="66119-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1. For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="66119-128">Modify the Windows Phone Project</span><span class="sxs-lookup"><span data-stu-id="66119-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="66119-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span><span class="sxs-lookup"><span data-stu-id="66119-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="66119-130">Add the following line of code at the end of the `OnLaunched()` method:</span><span class="sxs-lookup"><span data-stu-id="66119-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="66119-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span><span class="sxs-lookup"><span data-stu-id="66119-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="66119-132">Add the following `using` statements at the top of the App.xaml.cs file:</span><span class="sxs-lookup"><span data-stu-id="66119-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="66119-133">From the **File** menu in Visual Studio, click **Save All**.</span><span class="sxs-lookup"><span data-stu-id="66119-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="66119-134">Create the Push Background Component</span><span class="sxs-lookup"><span data-stu-id="66119-134">Create the Push Background Component</span></span>
<span data-ttu-id="66119-135">The next step is to create the push background component.</span><span class="sxs-lookup"><span data-stu-id="66119-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="66119-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span><span class="sxs-lookup"><span data-stu-id="66119-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="66119-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="66119-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="66119-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="66119-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="66119-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="66119-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="66119-140">Name the new class **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="66119-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="66119-141">Click **Add** to generate the class.</span><span class="sxs-lookup"><span data-stu-id="66119-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="66119-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span><span class="sxs-lookup"><span data-stu-id="66119-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store the content received from the notification so it can be retrieved from the UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="66119-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="66119-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="66119-144">On the left-hand side, click **Online**.</span><span class="sxs-lookup"><span data-stu-id="66119-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="66119-145">In the **Search** box, type **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="66119-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="66119-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="66119-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="66119-147">Complete the installation.</span><span class="sxs-lookup"><span data-stu-id="66119-147">Complete the installation.</span></span>
9. <span data-ttu-id="66119-148">Back in the NuGet **Search** box, type **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="66119-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="66119-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span><span class="sxs-lookup"><span data-stu-id="66119-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="66119-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span><span class="sxs-lookup"><span data-stu-id="66119-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="66119-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="66119-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="66119-152">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span><span class="sxs-lookup"><span data-stu-id="66119-152">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="66119-153">Under **Notifications**, set **Toast Capable** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="66119-153">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="66119-154">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span><span class="sxs-lookup"><span data-stu-id="66119-154">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="66119-155">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="66119-155">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="66119-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span><span class="sxs-lookup"><span data-stu-id="66119-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="66119-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span><span class="sxs-lookup"><span data-stu-id="66119-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="66119-158">From the **File** menu, click **Save All**.</span><span class="sxs-lookup"><span data-stu-id="66119-158">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="66119-159">Run the Application</span><span class="sxs-lookup"><span data-stu-id="66119-159">Run the Application</span></span>
<span data-ttu-id="66119-160">To run the application, do the following:</span><span class="sxs-lookup"><span data-stu-id="66119-160">To run the application, do the following:</span></span>

1. <span data-ttu-id="66119-161">In Visual Studio, run the **AppBackend** Web API application.</span><span class="sxs-lookup"><span data-stu-id="66119-161">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="66119-162">An ASP.NET web page is displayed.</span><span class="sxs-lookup"><span data-stu-id="66119-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="66119-163">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span><span class="sxs-lookup"><span data-stu-id="66119-163">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="66119-164">The Windows Phone emulator runs and loads the app automatically.</span><span class="sxs-lookup"><span data-stu-id="66119-164">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="66119-165">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span><span class="sxs-lookup"><span data-stu-id="66119-165">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="66119-166">These can be any string, but they must be the same value.</span><span class="sxs-lookup"><span data-stu-id="66119-166">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="66119-167">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span><span class="sxs-lookup"><span data-stu-id="66119-167">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="66119-168">Then click **Send push**.</span><span class="sxs-lookup"><span data-stu-id="66119-168">Then click **Send push**.</span></span>

[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png



