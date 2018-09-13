---
title: Register the current user for push notifications by using Web API | Microsoft Docs
description: Learn how to request push notification registration in an iOS app with Azure Notification Hubs when registeration is performed by ASP.NET Web API.
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: ''
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: de62f4b6b092c281f8110702874b79a300750d60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548975"
---
# <a name="register-the-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="c9600-103">Register the current user for push notifications by using ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c9600-103">Register the current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c9600-105">Overview</span><span class="sxs-lookup"><span data-stu-id="c9600-105">Overview</span></span>
<span data-ttu-id="c9600-106">This topic shows you how to request push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="c9600-106">This topic shows you how to request push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="c9600-107">This topic extends the tutorial [Notify users with Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="c9600-107">This topic extends the tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="c9600-108">You must have already completed the required steps in that tutorial to create the authenticated mobile service.</span><span class="sxs-lookup"><span data-stu-id="c9600-108">You must have already completed the required steps in that tutorial to create the authenticated mobile service.</span></span> <span data-ttu-id="c9600-109">For more information on the notify users scenario, see [Notify users with Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="c9600-109">For more information on the notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="c9600-110">Update your app</span><span class="sxs-lookup"><span data-stu-id="c9600-110">Update your app</span></span>
1. <span data-ttu-id="c9600-111">In your MainStoryboard_iPhone.storyboard, add the following components from the object library:</span><span class="sxs-lookup"><span data-stu-id="c9600-111">In your MainStoryboard_iPhone.storyboard, add the following components from the object library:</span></span>
   
   * <span data-ttu-id="c9600-112">**Label**: "Push to User with Notification Hubs"</span><span class="sxs-lookup"><span data-stu-id="c9600-112">**Label**: "Push to User with Notification Hubs"</span></span>
   * <span data-ttu-id="c9600-113">**Label**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="c9600-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="c9600-114">**Label**: "User"</span><span class="sxs-lookup"><span data-stu-id="c9600-114">**Label**: "User"</span></span>
   * <span data-ttu-id="c9600-115">**Text Field**: "User"</span><span class="sxs-lookup"><span data-stu-id="c9600-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="c9600-116">**Label**: "Password"</span><span class="sxs-lookup"><span data-stu-id="c9600-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="c9600-117">**Text Field**: "Password"</span><span class="sxs-lookup"><span data-stu-id="c9600-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="c9600-118">**Button**: "Login"</span><span class="sxs-lookup"><span data-stu-id="c9600-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="c9600-119">At this point, your storyboard looks like the following:</span><span class="sxs-lookup"><span data-stu-id="c9600-119">At this point, your storyboard looks like the following:</span></span>
     
      ![][0]
2. <span data-ttu-id="c9600-120">In the assistant editor, create outlets for all the switched controls and call them, connect the text fields with the View Controller (delegate), and create an **Action** for the **login** button.</span><span class="sxs-lookup"><span data-stu-id="c9600-120">In the assistant editor, create outlets for all the switched controls and call them, connect the text fields with the View Controller (delegate), and create an **Action** for the **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain the following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="c9600-121">Create a class named **DeviceInfo**, and copy the following code into the interface section of the file DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="c9600-121">Create a class named **DeviceInfo**, and copy the following code into the interface section of the file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="c9600-122">Copy the following code in the implementation section of the DeviceInfo.m file:</span><span class="sxs-lookup"><span data-stu-id="c9600-122">Copy the following code in the implementation section of the DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store the install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="c9600-123">In PushToUserAppDelegate.h, add the following property singleton:</span><span class="sxs-lookup"><span data-stu-id="c9600-123">In PushToUserAppDelegate.h, add the following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="c9600-124">In the **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add the following code:</span><span class="sxs-lookup"><span data-stu-id="c9600-124">In the **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add the following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="c9600-125">The first line initializes the **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="c9600-125">The first line initializes the **DeviceInfo** singleton.</span></span> <span data-ttu-id="c9600-126">The second line starts the registration for push notifications, which is already present is you have already completed the [Get Started with Notification Hubs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c9600-126">The second line starts the registration for push notifications, which is already present is you have already completed the [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="c9600-127">In PushToUserAppDelegate.m, implement the method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add the following code:</span><span class="sxs-lookup"><span data-stu-id="c9600-127">In PushToUserAppDelegate.m, implement the method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add the following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="c9600-128">This sets the device token for the request.</span><span class="sxs-lookup"><span data-stu-id="c9600-128">This sets the device token for the request.</span></span>
   
   > [!NOTE]
   > At this point, there should not be any other code in this method. If you already have a call to the **registerNativeWithDeviceToken** method that was added when you completed the [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.
   > 
   > 
8. <span data-ttu-id="c9600-131">In the PushToUserAppDelegate.m file, add the following handler method:</span><span class="sxs-lookup"><span data-stu-id="c9600-131">In the PushToUserAppDelegate.m file, add the following handler method:</span></span>
   
   * <span data-ttu-id="c9600-132">(void)application:(UIApplication \*)application didReceiveRemoteNotification:(NSDictionary \*)userInfo {   NSLog(@"%@", userInfo);   UIAlertView \*alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span><span class="sxs-lookup"><span data-stu-id="c9600-132">(void)application:(UIApplication \*)application didReceiveRemoteNotification:(NSDictionary \*)userInfo {   NSLog(@"%@", userInfo);   UIAlertView \*alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="c9600-133">This method displays an alert in the UI when your app receives notifications while it is running.</span><span class="sxs-lookup"><span data-stu-id="c9600-133">This method displays an alert in the UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="c9600-134">Open the PushToUserViewController.m file, and return the keyboard in the following implementation:</span><span class="sxs-lookup"><span data-stu-id="c9600-134">Open the PushToUserViewController.m file, and return the keyboard in the following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="c9600-135">In the **viewDidLoad** method in the PushToUserViewController.m file, initialize the installationId label as follows:</span><span class="sxs-lookup"><span data-stu-id="c9600-135">In the **viewDidLoad** method in the PushToUserViewController.m file, initialize the installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="c9600-136">Add the following properties in interface in PushToUserViewController.m:</span><span class="sxs-lookup"><span data-stu-id="c9600-136">Add the following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="c9600-137">Then, add the following implementation:</span><span class="sxs-lookup"><span data-stu-id="c9600-137">Then, add the following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="c9600-138">Copy the following code into the **login** handler method created by XCode:</span><span class="sxs-lookup"><span data-stu-id="c9600-138">Copy the following code into the **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="c9600-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="c9600-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="c9600-140">This Web API was defined in [Notify users with Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="c9600-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="c9600-141">Now that the client app has been updated, return to the [Notify users with Notification Hubs] and update the mobile service to send notifications by using Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="c9600-141">Now that the client app has been updated, return to the [Notify users with Notification Hubs] and update the mobile service to send notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet

[Get Started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios


