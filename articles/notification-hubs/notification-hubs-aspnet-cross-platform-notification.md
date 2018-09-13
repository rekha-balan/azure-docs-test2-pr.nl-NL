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
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a>Send cross-platform notifications to users with Notification Hubs
In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user. In that tutorial, multiple requests were required to send a notification to each supported client platform. Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications. This simplifies sending cross-platform notifications. This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms. For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].

> [!NOTE]
> Notification Hubs allows a device to register multiple templates with the same tag. In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template. This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.
> 
> 

Complete the following steps to send cross-platform notifications using templates:

1. In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.
2. Locate the block of code in the **Post** method that creates a new registration replace the `switch` content with the following code:
   
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
   
    This code calls the platform-specific method to create a template registration instead of a native registration. Existing registrations need not be modified because template registrations derive from native registrations.
3. In the **Notifications** controller, replace the **sendNotification** method with the following code:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    This code sends a notification to all platforms at the same time and without having to specify a native payload. Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.
4. Re-publish your WebApi back-end project.
5. Run the client app again and verify that registration succeeds.
6. (Optional) Deploy the client app to a second device, then run the app.
   
    Note that a notification is displayed on each device.

## <a name="next-steps"></a>Next Steps
Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:

* **[Use Notification Hubs to send breaking news]** <br/>Demonstrates another scenario for using templates
* **[Azure Notification Hubs Overview][Templates]**<br/>Overview topic has more detailed information on templates.

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
