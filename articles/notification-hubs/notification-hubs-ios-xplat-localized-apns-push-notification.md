---
title: Notification Hubs Localized Breaking News Tutorial for iOS
description: Learn how to use Azure Service Bus Notification Hubs to send localized breaking news notifications (iOS).
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: ''
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 6077caf2ceabff38b37836c8f0cd10087515e59b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555897"
---
# <a name="use-notification-hubs-to-send-localized-breaking-news-to-ios-devices"></a><span data-ttu-id="050b3-103">Use Notification Hubs to send localized breaking news to iOS devices</span><span class="sxs-lookup"><span data-stu-id="050b3-103">Use Notification Hubs to send localized breaking news to iOS devices</span></span>
> [!div class="op_single_selector"]
> * [Windows Store C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="050b3-106">Overview</span><span class="sxs-lookup"><span data-stu-id="050b3-106">Overview</span></span>
<span data-ttu-id="050b3-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span><span class="sxs-lookup"><span data-stu-id="050b3-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="050b3-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span><span class="sxs-lookup"><span data-stu-id="050b3-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="050b3-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span><span class="sxs-lookup"><span data-stu-id="050b3-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="050b3-110">There are two parts to this scenario:</span><span class="sxs-lookup"><span data-stu-id="050b3-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="050b3-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span><span class="sxs-lookup"><span data-stu-id="050b3-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="050b3-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="050b3-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="050b3-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="050b3-113">Prerequisites</span></span>
<span data-ttu-id="050b3-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span><span class="sxs-lookup"><span data-stu-id="050b3-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="050b3-115">Visual Studio 2012 or later is optional.</span><span class="sxs-lookup"><span data-stu-id="050b3-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="050b3-116">Template concepts</span><span class="sxs-lookup"><span data-stu-id="050b3-116">Template concepts</span></span>
<span data-ttu-id="050b3-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span><span class="sxs-lookup"><span data-stu-id="050b3-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="050b3-118">Many apps, however, target multiple markets and require localization.</span><span class="sxs-lookup"><span data-stu-id="050b3-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="050b3-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span><span class="sxs-lookup"><span data-stu-id="050b3-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="050b3-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span><span class="sxs-lookup"><span data-stu-id="050b3-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="050b3-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span><span class="sxs-lookup"><span data-stu-id="050b3-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="050b3-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span><span class="sxs-lookup"><span data-stu-id="050b3-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="050b3-123">We would then have to send a localized version of the world news to each of these tags.</span><span class="sxs-lookup"><span data-stu-id="050b3-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="050b3-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span><span class="sxs-lookup"><span data-stu-id="050b3-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="050b3-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span><span class="sxs-lookup"><span data-stu-id="050b3-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="050b3-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span><span class="sxs-lookup"><span data-stu-id="050b3-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="050b3-127">In our case, we will send a locale-agnostic message containing all supported languages:</span><span class="sxs-lookup"><span data-stu-id="050b3-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="050b3-128">Then we will ensure that devices register with a template that refers to the correct property.</span><span class="sxs-lookup"><span data-stu-id="050b3-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="050b3-129">For instance,  an iOS app that wants to register for French news will register the following:</span><span class="sxs-lookup"><span data-stu-id="050b3-129">For instance,  an iOS app that wants to register for French news will register the following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="050b3-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span><span class="sxs-lookup"><span data-stu-id="050b3-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="the-app-user-interface"></a><span data-ttu-id="050b3-131">The app user interface</span><span class="sxs-lookup"><span data-stu-id="050b3-131">The app user interface</span></span>
<span data-ttu-id="050b3-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span><span class="sxs-lookup"><span data-stu-id="050b3-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="050b3-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span><span class="sxs-lookup"><span data-stu-id="050b3-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="050b3-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span><span class="sxs-lookup"><span data-stu-id="050b3-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-the-ios-app"></a><span data-ttu-id="050b3-135">Building the iOS app</span><span class="sxs-lookup"><span data-stu-id="050b3-135">Building the iOS app</span></span>
1. <span data-ttu-id="050b3-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span><span class="sxs-lookup"><span data-stu-id="050b3-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="050b3-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span><span class="sxs-lookup"><span data-stu-id="050b3-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="050b3-138">Then modify the *subscribe* method to include the locale:</span><span class="sxs-lookup"><span data-stu-id="050b3-138">Then modify the *subscribe* method to include the locale:</span></span>
   
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
   
    <span data-ttu-id="050b3-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="050b3-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="050b3-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span><span class="sxs-lookup"><span data-stu-id="050b3-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span></span> <span data-ttu-id="050b3-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span><span class="sxs-lookup"><span data-stu-id="050b3-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span></span>
   
    <span data-ttu-id="050b3-142">Add a method to retrieve the locale from the user default settings:</span><span class="sxs-lookup"><span data-stu-id="050b3-142">Add a method to retrieve the locale from the user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="050b3-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="050b3-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="050b3-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span><span class="sxs-lookup"><span data-stu-id="050b3-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="050b3-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span><span class="sxs-lookup"><span data-stu-id="050b3-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span></span>
   
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
3. <span data-ttu-id="050b3-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span><span class="sxs-lookup"><span data-stu-id="050b3-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="050b3-147">Change your call to the *subscribe* method of notifications with the following:</span><span class="sxs-lookup"><span data-stu-id="050b3-147">Change your call to the *subscribe* method of notifications with the following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="050b3-148">(optional) Send localized template notifications from .NET console app.</span><span class="sxs-lookup"><span data-stu-id="050b3-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="050b3-149">(optional) Send localized template notifications from the device</span><span class="sxs-lookup"><span data-stu-id="050b3-149">(optional) Send localized template notifications from the device</span></span>
<span data-ttu-id="050b3-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span><span class="sxs-lookup"><span data-stu-id="050b3-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span>  <span data-ttu-id="050b3-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="050b3-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="050b3-152">Next Steps</span><span class="sxs-lookup"><span data-stu-id="050b3-152">Next Steps</span></span>
<span data-ttu-id="050b3-153">For more information on using templates, see:</span><span class="sxs-lookup"><span data-stu-id="050b3-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="050b3-154">[Notify users with Notification Hubs: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="050b3-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="050b3-155">[Notify users with Notification Hubs: Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="050b3-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
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


