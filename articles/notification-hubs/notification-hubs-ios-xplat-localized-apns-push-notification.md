---
title: Push localized notifications to iOS devices using Azure Notification Hubs | Microsoft Docs
description: Learn how to use push localized notifications to iOS devices by using Azure Notification Hubs.
services: notification-hubs
documentationcenter: ios
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: d19fc4290f32359d3af66d96512f65abb17f5d34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812369"
---
# <a name="tutorial-push-localized-notifications-to-ios-devices-using-azure-notification-hubs"></a><span data-ttu-id="d1584-103">Tutorial: Push localized notifications to iOS devices using Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="d1584-103">Tutorial: Push localized notifications to iOS devices using Azure Notification Hubs</span></span> 

> [!div class="op_single_selector"]
> * [Windows Store C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)

<span data-ttu-id="d1584-106">This tutorial shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span><span class="sxs-lookup"><span data-stu-id="d1584-106">This tutorial shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="d1584-107">In this tutorial, you start with the iOS app created in [Use Notification Hubs to send breaking news].</span><span class="sxs-lookup"><span data-stu-id="d1584-107">In this tutorial, you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="d1584-108">When complete, you can register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span><span class="sxs-lookup"><span data-stu-id="d1584-108">When complete, you can register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="d1584-109">There are two parts to this scenario:</span><span class="sxs-lookup"><span data-stu-id="d1584-109">There are two parts to this scenario:</span></span>

* <span data-ttu-id="d1584-110">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span><span class="sxs-lookup"><span data-stu-id="d1584-110">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="d1584-111">The back-end broadcasts the notifications, using the **tag** and **template** features of Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="d1584-111">The back-end broadcasts the notifications, using the **tag** and **template** features of Azure Notification Hubs.</span></span>

<span data-ttu-id="d1584-112">In this tutorial, you take the following steps:</span><span class="sxs-lookup"><span data-stu-id="d1584-112">In this tutorial, you take the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d1584-113">Update the app user interface</span><span class="sxs-lookup"><span data-stu-id="d1584-113">Update the app user interface</span></span>
> * <span data-ttu-id="d1584-114">Build the iOS app</span><span class="sxs-lookup"><span data-stu-id="d1584-114">Build the iOS app</span></span>
> * <span data-ttu-id="d1584-115">Send localized template notifications from .NET console app</span><span class="sxs-lookup"><span data-stu-id="d1584-115">Send localized template notifications from .NET console app</span></span>
> * <span data-ttu-id="d1584-116">Send localized template notifications from the device</span><span class="sxs-lookup"><span data-stu-id="d1584-116">Send localized template notifications from the device</span></span>

## <a name="overview"></a><span data-ttu-id="d1584-117">Overview</span><span class="sxs-lookup"><span data-stu-id="d1584-117">Overview</span></span>

<span data-ttu-id="d1584-118">In [Use Notification Hubs to send breaking news], you built an app that used **tags** to subscribe to notifications for different news categories.</span><span class="sxs-lookup"><span data-stu-id="d1584-118">In [Use Notification Hubs to send breaking news], you built an app that used **tags** to subscribe to notifications for different news categories.</span></span> <span data-ttu-id="d1584-119">Many apps, however, target multiple markets and require localization.</span><span class="sxs-lookup"><span data-stu-id="d1584-119">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="d1584-120">It means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span><span class="sxs-lookup"><span data-stu-id="d1584-120">It means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span> <span data-ttu-id="d1584-121">This tutorial shows you how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span><span class="sxs-lookup"><span data-stu-id="d1584-121">This tutorial shows you how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

> [!NOTE]
> <span data-ttu-id="d1584-122">One way to send localized notifications is to create multiple versions of each tag.</span><span class="sxs-lookup"><span data-stu-id="d1584-122">One way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="d1584-123">For instance, to support English, French, and Mandarin, you would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span><span class="sxs-lookup"><span data-stu-id="d1584-123">For instance, to support English, French, and Mandarin, you would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="d1584-124">You would then have to send a localized version of the world news to each of these tags.</span><span class="sxs-lookup"><span data-stu-id="d1584-124">You would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="d1584-125">In this topic, you use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span><span class="sxs-lookup"><span data-stu-id="d1584-125">In this topic, you use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="d1584-126">At a high level, templates are a way to specify how a specific device should receive a notification.</span><span class="sxs-lookup"><span data-stu-id="d1584-126">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="d1584-127">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span><span class="sxs-lookup"><span data-stu-id="d1584-127">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="d1584-128">In your case, you send a locale-agnostic message containing all supported languages:</span><span class="sxs-lookup"><span data-stu-id="d1584-128">In your case, you send a locale-agnostic message containing all supported languages:</span></span>

```json
{
    "News_English": "...",
    "News_French": "...",
    "News_Mandarin": "..."
}
```

<span data-ttu-id="d1584-129">Then you ensure that devices register with a template that refers to the correct property.</span><span class="sxs-lookup"><span data-stu-id="d1584-129">Then you ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="d1584-130">For instance,  an iOS app that wants to register for French news registers using the following syntax:</span><span class="sxs-lookup"><span data-stu-id="d1584-130">For instance,  an iOS app that wants to register for French news registers using the following syntax:</span></span>

```json
{
    aps:{
        alert: "$(News_French)"
    }
}
```

<span data-ttu-id="d1584-131">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span><span class="sxs-lookup"><span data-stu-id="d1584-131">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1584-132">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1584-132">Prerequisites</span></span>

- <span data-ttu-id="d1584-133">Complete the [Push notifications to specific iOS devices](notification-hubs-ios-xplat-segmented-apns-push-notification.md) tutorial and have the code available, because this tutorial builds directly upon that code.</span><span class="sxs-lookup"><span data-stu-id="d1584-133">Complete the [Push notifications to specific iOS devices](notification-hubs-ios-xplat-segmented-apns-push-notification.md) tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>
- <span data-ttu-id="d1584-134">Visual Studio 2017 is optional.</span><span class="sxs-lookup"><span data-stu-id="d1584-134">Visual Studio 2017 is optional.</span></span>

## <a name="update-the-app-user-interface"></a><span data-ttu-id="d1584-135">Update the app user interface</span><span class="sxs-lookup"><span data-stu-id="d1584-135">Update the app user interface</span></span>

<span data-ttu-id="d1584-136">In this section, you modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span><span class="sxs-lookup"><span data-stu-id="d1584-136">In this section, you modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="d1584-137">In your **MainStoryboard_iPhone.storyboard**, add a Segmented Control with the three languages: English, French, and Mandarin.</span><span class="sxs-lookup"><span data-stu-id="d1584-137">In your **MainStoryboard_iPhone.storyboard**, add a Segmented Control with the three languages: English, French, and Mandarin.</span></span>

![Creating the iOS UI storyboard][13]

<span data-ttu-id="d1584-139">Then make sure to add an IBOutlet in your ViewController.h as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="d1584-139">Then make sure to add an IBOutlet in your ViewController.h as shown in the following image:</span></span>

![Create outlets for the switches][14]

## <a name="build-the-ios-app"></a><span data-ttu-id="d1584-141">Build the iOS app</span><span class="sxs-lookup"><span data-stu-id="d1584-141">Build the iOS app</span></span>

1. <span data-ttu-id="d1584-142">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="d1584-142">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown in the following code:</span></span>

    ```objc
    - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;

    - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;

    - (NSSet*) retrieveCategories;

    - (int) retrieveLocale;
    ```
    <span data-ttu-id="d1584-143">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span><span class="sxs-lookup"><span data-stu-id="d1584-143">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>

    ```objc
    - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
        NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
        [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
        [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
        [defaults synchronize];

        [self subscribeWithLocale: locale categories:categories completion:completion];
    }
    ````

    <span data-ttu-id="d1584-144">Then modify the *subscribe* method to include the locale:</span><span class="sxs-lookup"><span data-stu-id="d1584-144">Then modify the *subscribe* method to include the locale:</span></span>

    ```objc
    - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
        SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];

        NSString* localeString;
        switch (locale) {
            case 0:
                localeString = @"English";
                break;
            case 1:
                localeString = @"French";
                break;
            case 2:
                localeString = @"Mandarin";
                break;
        }

        NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];

        [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
    }
    ```

    <span data-ttu-id="d1584-145">You use the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="d1584-145">You use the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="d1584-146">When you register for a template, you have to provide the json template and also a name for the template (as the app might want to register different templates).</span><span class="sxs-lookup"><span data-stu-id="d1584-146">When you register for a template, you have to provide the json template and also a name for the template (as the app might want to register different templates).</span></span> <span data-ttu-id="d1584-147">Make sure to register your categories as tags, as you want to make sure to receive the notifciations for those news.</span><span class="sxs-lookup"><span data-stu-id="d1584-147">Make sure to register your categories as tags, as you want to make sure to receive the notifciations for those news.</span></span>

    <span data-ttu-id="d1584-148">Add a method to retrieve the locale from the user default settings:</span><span class="sxs-lookup"><span data-stu-id="d1584-148">Add a method to retrieve the locale from the user default settings:</span></span>

    ```objc
    - (int) retrieveLocale {
        NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

        int locale = [defaults integerForKey:@"BreakingNewsLocale"];

        return locale < 0?0:locale;
    }
    ```

2. <span data-ttu-id="d1584-149">Now that you modified the Notifications class, you have to make sure that the ViewController makes use of the new UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="d1584-149">Now that you modified the Notifications class, you have to make sure that the ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="d1584-150">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span><span class="sxs-lookup"><span data-stu-id="d1584-150">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>

    ```objc
    self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
    ```

    <span data-ttu-id="d1584-151">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following code:</span><span class="sxs-lookup"><span data-stu-id="d1584-151">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following code:</span></span>

    ```objc
    [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
        if (!error) {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                    @"Subscribed!" delegate:nil cancelButtonTitle:
                                    @"OK" otherButtonTitles:nil, nil];
            [alert show];
        } else {
            NSLog(@"Error subscribing: %@", error);
        }
    }];
    ```

3. <span data-ttu-id="d1584-152">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span><span class="sxs-lookup"><span data-stu-id="d1584-152">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="d1584-153">Change your call to the *subscribe* method of notifications with the following code:</span><span class="sxs-lookup"><span data-stu-id="d1584-153">Change your call to the *subscribe* method of notifications with the following code:</span></span>

    ```obj-c
    NSSet* categories = [self.notifications retrieveCategories];
    int locale = [self.notifications retrieveLocale];
    [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
        if (error != nil) {
            NSLog(@"Error registering for notifications: %@", error);
        }
    }];
    ```

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="d1584-154">(optional) Send localized template notifications from .NET console app</span><span class="sxs-lookup"><span data-stu-id="d1584-154">(optional) Send localized template notifications from .NET console app</span></span>

[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="d1584-155">(optional) Send localized template notifications from the device</span><span class="sxs-lookup"><span data-stu-id="d1584-155">(optional) Send localized template notifications from the device</span></span>

<span data-ttu-id="d1584-156">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span><span class="sxs-lookup"><span data-stu-id="d1584-156">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span> <span data-ttu-id="d1584-157">You can add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="d1584-157">You can add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

```objc
- (void)SendNotificationRESTAPI:(NSString*)categoryTag
{
    NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                defaultSessionConfiguration] delegate:nil delegateQueue:nil];

    NSString *json;

    // Construct the messages REST endpoint
    NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                        HUBNAME, API_VERSION]];

    // Generated the token to be used in the authorization header.
    NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

    //Create the request to add the template notification message to the hub
    NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
    [request setHTTPMethod:@"POST"];

    // Add the category as a tag
    [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

    // Template notification
    json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
            \"News_English\":\"Breaking %@ News in English : %@\","
            \"News_French\":\"Breaking %@ News in French : %@\","
            \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
            categoryTag, self.notificationMessage.text,
            categoryTag, self.notificationMessage.text,  // insert English localized news here
            categoryTag, self.notificationMessage.text,  // insert French localized news here
            categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

    // Signify template notification format
    [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

    // JSON Content-Type
    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

    //Authenticate the notification message POST request with the SaS token
    [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

    //Add the notification message body
    [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

    // Send the REST request
    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
        {
        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
            if (error || httpResponse.statusCode != 200)
            {
                NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
            }
            if (data != NULL)
            {
                //xmlParser = [[NSXMLParser alloc] initWithData:data];
                //[xmlParser setDelegate:self];
                //[xmlParser parse];
            }
        }];

    [dataTask resume];
}
```

## <a name="next-steps"></a><span data-ttu-id="d1584-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1584-158">Next steps</span></span>

<span data-ttu-id="d1584-159">In this tutorial, you sent localized notifications to iOS devices.</span><span class="sxs-lookup"><span data-stu-id="d1584-159">In this tutorial, you sent localized notifications to iOS devices.</span></span> <span data-ttu-id="d1584-160">To learn how to push notifications to specific users of iOS apps, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="d1584-160">To learn how to push notifications to specific users of iOS apps, advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="d1584-161">Push notifications to specific users</span><span class="sxs-lookup"><span data-stu-id="d1584-161">Push notifications to specific users</span></span>](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Notify users with Notification Hubs: Mobile Services]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
