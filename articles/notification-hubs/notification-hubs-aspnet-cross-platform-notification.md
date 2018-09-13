---
title: Send cross-platform notifications to users with Notification Hubs (ASP.NET)
description: Learn how to use Notification Hubs templates to send, in a single request, a platform-agnostic notification that targets all platforms.
services: notification-hubs
documentationcenter: ''
author: ysxu
manager: erikre
editor: ''
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 0cc620324c75ed6ffee26fe442014d61673ba1e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564127"
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="28d6d-103">Send cross-platform notifications to users with Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="28d6d-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="28d6d-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span><span class="sxs-lookup"><span data-stu-id="28d6d-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="28d6d-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span><span class="sxs-lookup"><span data-stu-id="28d6d-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="28d6d-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span><span class="sxs-lookup"><span data-stu-id="28d6d-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="28d6d-107">This simplifies sending cross-platform notifications.</span><span class="sxs-lookup"><span data-stu-id="28d6d-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="28d6d-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span><span class="sxs-lookup"><span data-stu-id="28d6d-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="28d6d-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span><span class="sxs-lookup"><span data-stu-id="28d6d-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>

> [!NOTE]
> <span data-ttu-id="28d6d-110">Notification Hubs allows a device to register multiple templates with the same tag.</span><span class="sxs-lookup"><span data-stu-id="28d6d-110">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="28d6d-111">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span><span class="sxs-lookup"><span data-stu-id="28d6d-111">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="28d6d-112">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span><span class="sxs-lookup"><span data-stu-id="28d6d-112">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="28d6d-113">Complete the following steps to send cross-platform notifications using templates:</span><span class="sxs-lookup"><span data-stu-id="28d6d-113">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="28d6d-114">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span><span class="sxs-lookup"><span data-stu-id="28d6d-114">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="28d6d-115">Locate the block of code in the **Post** method that creates a new registration replace the `switch` content with the following code:</span><span class="sxs-lookup"><span data-stu-id="28d6d-115">Locate the block of code in the **Post** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    <span data-ttu-id="28d6d-116">This code calls the platform-specific method to create a template registration instead of a native registration.</span><span class="sxs-lookup"><span data-stu-id="28d6d-116">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="28d6d-117">Existing registrations need not be modified because template registrations derive from native registrations.</span><span class="sxs-lookup"><span data-stu-id="28d6d-117">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="28d6d-118">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span><span class="sxs-lookup"><span data-stu-id="28d6d-118">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="28d6d-119">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span><span class="sxs-lookup"><span data-stu-id="28d6d-119">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="28d6d-120">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span><span class="sxs-lookup"><span data-stu-id="28d6d-120">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="28d6d-121">Re-publish your WebApi back-end project.</span><span class="sxs-lookup"><span data-stu-id="28d6d-121">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="28d6d-122">Run the client app again and verify that registration succeeds.</span><span class="sxs-lookup"><span data-stu-id="28d6d-122">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="28d6d-123">(Optional) Deploy the client app to a second device, then run the app.</span><span class="sxs-lookup"><span data-stu-id="28d6d-123">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="28d6d-124">Note that a notification is displayed on each device.</span><span class="sxs-lookup"><span data-stu-id="28d6d-124">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28d6d-125">Next Steps</span><span class="sxs-lookup"><span data-stu-id="28d6d-125">Next Steps</span></span>
<span data-ttu-id="28d6d-126">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span><span class="sxs-lookup"><span data-stu-id="28d6d-126">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="28d6d-127">**[Use Notification Hubs to send breaking news]**</span><span class="sxs-lookup"><span data-stu-id="28d6d-127">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="28d6d-128">Demonstrates another scenario for using templates</span><span class="sxs-lookup"><span data-stu-id="28d6d-128">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="28d6d-129">**[Azure Notification Hubs Overview][Templates]**</span><span class="sxs-lookup"><span data-stu-id="28d6d-129">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="28d6d-130">Overview topic has more detailed information on templates.</span><span class="sxs-lookup"><span data-stu-id="28d6d-130">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
