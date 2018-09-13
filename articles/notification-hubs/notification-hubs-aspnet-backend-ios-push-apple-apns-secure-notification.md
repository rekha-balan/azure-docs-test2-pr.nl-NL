---
title: Azure Notification Hubs Secure Push
description: Learn how to send secure push notifications to an iOS app from Azure. Code samples written in Objective-C and C#.
documentationcenter: ios
author: ysxu
manager: erikre
editor: ''
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 79a1025be835003a4eff59f378b7a143c2e312a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540843"
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="fdbe9-104">Azure Notification Hubs Secure Push</span><span class="sxs-lookup"><span data-stu-id="fdbe9-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fdbe9-108">Overview</span><span class="sxs-lookup"><span data-stu-id="fdbe9-108">Overview</span></span>
<span data-ttu-id="fdbe9-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="fdbe9-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="fdbe9-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="fdbe9-112">At a high level, the flow is as follows:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="fdbe9-113">The app back-end:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-113">The app back-end:</span></span>
   * <span data-ttu-id="fdbe9-114">Stores secure payload in back-end database.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="fdbe9-115">Sends the ID of this notification to the device (no secure information is sent).</span><span class="sxs-lookup"><span data-stu-id="fdbe9-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="fdbe9-116">The app on the device, when receiving the notification:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="fdbe9-117">The device contacts the back-end requesting the secure payload.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="fdbe9-118">The app can show the payload as a notification on the device.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="fdbe9-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="fdbe9-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="fdbe9-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="fdbe9-122">The app then authenticates the user and shows the notification payload.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="fdbe9-123">This Secure Push tutorial shows how to send a push notification securely.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="fdbe9-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="fdbe9-126">Modify the iOS project</span><span class="sxs-lookup"><span data-stu-id="fdbe9-126">Modify the iOS project</span></span>
<span data-ttu-id="fdbe9-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="fdbe9-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="fdbe9-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="fdbe9-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="fdbe9-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="fdbe9-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="fdbe9-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="fdbe9-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="fdbe9-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="fdbe9-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="fdbe9-137">In **AppDelegate.m** add the following method to handle push notifications:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="fdbe9-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="fdbe9-139">The specific handling of these cases depend mostly on your target user experience.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="fdbe9-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="fdbe9-141">Run the Application</span><span class="sxs-lookup"><span data-stu-id="fdbe9-141">Run the Application</span></span>
<span data-ttu-id="fdbe9-142">To run the application, do the following:</span><span class="sxs-lookup"><span data-stu-id="fdbe9-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="fdbe9-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span><span class="sxs-lookup"><span data-stu-id="fdbe9-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="fdbe9-144">In the iOS app UI, enter a username and password.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="fdbe9-145">These can be any string, but they must be the same value.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="fdbe9-146">In the iOS app UI, click **Log in**.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="fdbe9-147">Then click **Send push**.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-147">Then click **Send push**.</span></span> <span data-ttu-id="fdbe9-148">You should see the secure notification being displayed in your notification center.</span><span class="sxs-lookup"><span data-stu-id="fdbe9-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png

