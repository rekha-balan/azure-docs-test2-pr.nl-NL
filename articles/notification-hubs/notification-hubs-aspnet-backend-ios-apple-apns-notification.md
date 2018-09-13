---
title: Push notifications to specific users using Azure Notification Hubs | Microsoft Docs
description: Learn how to send push notifications to specific users by using Azure Notification Hubs.
documentationcenter: ios
author: dimazaid
manager: kpiteira
editor: spelluru
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/13/2018
ms.author: dimazaid
ms.openlocfilehash: 270311af94d0c0551626fc2906cade84e0c60664
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805797"
---
# <a name="tutorial-push-notifications-to-specific-users-using-azure-notification-hubs"></a><span data-ttu-id="7c1d2-103">Tutorial: Push notifications to specific users using Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="7c1d2-103">Tutorial: Push notifications to specific users using Azure Notification Hubs</span></span>

[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

<span data-ttu-id="7c1d2-104">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-104">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="7c1d2-105">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="7c1d2-105">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

<span data-ttu-id="7c1d2-106">In this tutorial, you take the following steps:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-106">In this tutorial, you take the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c1d2-107">Create the WebAPI project</span><span class="sxs-lookup"><span data-stu-id="7c1d2-107">Create the WebAPI project</span></span>
> * <span data-ttu-id="7c1d2-108">Authenticate clients to the WebAPI backend</span><span class="sxs-lookup"><span data-stu-id="7c1d2-108">Authenticate clients to the WebAPI backend</span></span>
> * <span data-ttu-id="7c1d2-109">Register for notifications by using the WebAPI backend</span><span class="sxs-lookup"><span data-stu-id="7c1d2-109">Register for notifications by using the WebAPI backend</span></span>
> * <span data-ttu-id="7c1d2-110">Send notifications from the WebAPI backend</span><span class="sxs-lookup"><span data-stu-id="7c1d2-110">Send notifications from the WebAPI backend</span></span>
> * <span data-ttu-id="7c1d2-111">Publish the new WebAPI backend</span><span class="sxs-lookup"><span data-stu-id="7c1d2-111">Publish the new WebAPI backend</span></span>
> * <span data-ttu-id="7c1d2-112">Modify your iOS app</span><span class="sxs-lookup"><span data-stu-id="7c1d2-112">Modify your iOS app</span></span>
> * <span data-ttu-id="7c1d2-113">Test the application</span><span class="sxs-lookup"><span data-stu-id="7c1d2-113">Test the application</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c1d2-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c1d2-114">Prerequisites</span></span>

<span data-ttu-id="7c1d2-115">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d2-115">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="7c1d2-116">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-116">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
<span data-ttu-id="7c1d2-117">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d2-117">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="7c1d2-118">Modify your iOS app</span><span class="sxs-lookup"><span data-stu-id="7c1d2-118">Modify your iOS app</span></span>

1. <span data-ttu-id="7c1d2-119">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-119">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7c1d2-120">This section assumes that your project is configured with an empty organization name.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-120">This section assumes that your project is configured with an empty organization name.</span></span> <span data-ttu-id="7c1d2-121">If not, you need to prepend your organization name to all class names.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-121">If not, you need to prepend your organization name to all class names.</span></span>

2. <span data-ttu-id="7c1d2-122">In the **Main.storyboard**, add the components shown in the screenshot from the object library.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-122">In the **Main.storyboard**, add the components shown in the screenshot from the object library.</span></span>

    ![Edit storybard in Xcode interface builder][1]

   * <span data-ttu-id="7c1d2-124">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-124">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="7c1d2-125">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-125">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="7c1d2-126">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-126">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="7c1d2-127">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span><span class="sxs-lookup"><span data-stu-id="7c1d2-127">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="7c1d2-128">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been set up on the hub.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-128">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been set up on the hub.</span></span> <span data-ttu-id="7c1d2-129">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-129">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="7c1d2-130">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been set up on the hub.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-130">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been set up on the hub.</span></span> <span data-ttu-id="7c1d2-131">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-131">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="7c1d2-132">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-132">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="7c1d2-133">**Recipient Username:A** UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-133">**Recipient Username:A** UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="7c1d2-134">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-134">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

3. <span data-ttu-id="7c1d2-135">**Ctrl** drag from the components in the view to **ViewController.h** and add these new outlets.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-135">**Ctrl** drag from the components in the view to **ViewController.h** and add these new outlets.</span></span>

    ```objc
    @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
    @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
    @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
    @property (weak, nonatomic) IBOutlet UITextField *NotificationField;

    // Used to enable the buttons on the UI
    @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
    @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;

    // Used to enabled sending notifications across platforms
    @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
    @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
    @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;

    - (IBAction)LogInAction:(id)sender;
    ```

4. <span data-ttu-id="7c1d2-136">In **ViewController.h**, add the following `#define` after your import statements.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-136">In **ViewController.h**, add the following `#define` after your import statements.</span></span> <span data-ttu-id="7c1d2-137">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-137">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="7c1d2-138">For example, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-138">For example, *http://you_backend.azurewebsites.net*.</span></span>

    ```objc
    #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
    ```

5. <span data-ttu-id="7c1d2-139">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-139">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="7c1d2-140">Create the class inheriting from `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-140">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="7c1d2-141">Then add the following code in the RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-141">Then add the following code in the RegisterClient.h.</span></span>

    ```objc
    @interface RegisterClient : NSObject

    @property (strong, nonatomic) NSString* authenticationHeader;

    -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
        andCompletion:(void(^)(NSError*))completion;

    -(instancetype) initWithEndpoint:(NSString*)Endpoint;

    @end
    ```

6. <span data-ttu-id="7c1d2-142">In the `RegisterClient.m`, update the `@interface` section:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-142">In the `RegisterClient.m`, update the `@interface` section:</span></span>

    ```objc
    @interface RegisterClient ()

    @property (strong, nonatomic) NSURLSession* session;
    @property (strong, nonatomic) NSURLSession* endpoint;

    -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                andCompletion:(void(^)(NSError*))completion;
    -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                completion:(void(^)(NSString*, NSError*))completion;
    -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;

    @end
    ```

7. <span data-ttu-id="7c1d2-143">Replace the `@implementation` section in the RegisterClient.m with the following code:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-143">Replace the `@implementation` section in the RegisterClient.m with the following code:</span></span>

    ```objc
    @implementation RegisterClient

    // Globals used by RegisterClient
    NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

    -(instancetype) initWithEndpoint:(NSString*)Endpoint
    {
        self = [super init];
        if (self) {
            NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
            _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
            _endpoint = Endpoint;
        }
        return self;
    }

    -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                andCompletion:(void(^)(NSError*))completion
    {
        [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
    }

    -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                andCompletion:(void(^)(NSError*))completion
    {
        NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

        NSString *deviceTokenString = [[token description]
            stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
        deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                uppercaseString];

        [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
            completion:^(NSString* registrationId, NSError *error) {
            NSLog(@"regId: %@", registrationId);
            if (error) {
                completion(error);
                return;
            }

            [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                if (error) {
                    completion(error);
                    return;
                }

                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                if (httpResponse.statusCode == 200) {
                    completion(nil);
                } else if (httpResponse.statusCode == 410 && retry) {
                    [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                } else {
                    NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                    completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                userInfo:nil]);
                }

            }];
        }];
    }

    -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
    {
        NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                @"Tags": [tags allObjects]};
        NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                            options:NSJSONWritingPrettyPrinted error:nil];

        NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                            encoding:NSUTF8StringEncoding]);

        NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                registrationId];
        NSURL* requestURL = [NSURL URLWithString:endpoint];
        NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
        [request setHTTPMethod:@"PUT"];
        [request setHTTPBody:jsonData];
        NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                self.authenticationHeader];
        [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
        [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

        NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
            completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
        {
            if (!error)
            {
                completion(response, error);
            }
            else
            {
                NSLog(@"Error request: %@", error);
                completion(nil, error);
            }
        }];
        [dataTask resume];
    }

    -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                completion:(void(^)(NSString*, NSError*))completion
    {
        NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                    objectForKey:RegistrationIdLocalStorageKey];

        if (registrationId)
        {
            completion(registrationId, nil);
            return;
        }

        // request new one & save
        NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                _endpoint, token]];
        NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
        [request setHTTPMethod:@"POST"];
        NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                self.authenticationHeader];
        [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

        NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
            completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
        {
            NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
            if (!error && httpResponse.statusCode == 200)
            {
                NSString* registrationId = [[NSString alloc] initWithData:data
                    encoding:NSUTF8StringEncoding];

                // remove quotes
                registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                    [registrationId length]-2)];

                [[NSUserDefaults standardUserDefaults] setObject:registrationId
                    forKey:RegistrationIdLocalStorageKey];
                [[NSUserDefaults standardUserDefaults] synchronize];

                completion(registrationId, nil);
            }
            else
            {
                NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                if (error)
                    completion(nil, error);
                else {
                    completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                userInfo:nil]);
                }
            }
        }];
        [dataTask resume];
    }

    @end
    ```

    <span data-ttu-id="7c1d2-144">This code implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-144">This code implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="7c1d2-145">This class requires its property **authorizationHeader** to be set in order to work properly.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-145">This class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="7c1d2-146">This property is set by the **ViewController** class after the login.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-146">This property is set by the **ViewController** class after the login.</span></span>

8. <span data-ttu-id="7c1d2-147">In ViewController.h, add a `#import` statement for RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-147">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="7c1d2-148">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-148">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>

    ```objc
    #import "RegisterClient.h"

    @property (strong, nonatomic) NSData* deviceToken;
    @property (strong, nonatomic) RegisterClient* registerClient;
    ```

9. <span data-ttu-id="7c1d2-149">In ViewController.m, add a private method declaration in the `@interface` section:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-149">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>

    ```objc
    @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>

    // create the Authorization header to perform Basic authentication with your app back-end
    -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                    AndPassword:(NSString*)password;

    @end
    ```

    > [!NOTE]
    > <span data-ttu-id="7c1d2-150">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-150">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>

10. <span data-ttu-id="7c1d2-151">Then in the `@implementation` section of `ViewController.m`, add the following code, which adds the implementation for setting the device token and authentication header.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-151">Then in the `@implementation` section of `ViewController.m`, add the following code, which adds the implementation for setting the device token and authentication header.</span></span>

    ```objc
    -(void) setDeviceToken: (NSData*) deviceToken
    {
        _deviceToken = deviceToken;
        self.LogInButton.enabled = YES;
    }

    -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                    AndPassword:(NSString*)password;
    {
        NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];

        NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];

        self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                    encoding:NSUTF8StringEncoding];
    }

    -(BOOL)textFieldShouldReturn:(UITextField *)textField
    {
        [textField resignFirstResponder];
        return YES;
    }
    ```

    <span data-ttu-id="7c1d2-152">Notice how setting the device token enables the log in button.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-152">Notice how setting the device token enables the log in button.</span></span> <span data-ttu-id="7c1d2-153">It's because as a part of the login action, the view controller registers for push notifications with the app backend.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-153">It's because as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="7c1d2-154">Hence, do not want Log In action to be accessible until the device token has been properly set up.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-154">Hence, do not want Log In action to be accessible until the device token has been properly set up.</span></span> <span data-ttu-id="7c1d2-155">You can decouple the login from the push registration as long as the former happens before the latter.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-155">You can decouple the login from the push registration as long as the former happens before the latter.</span></span>

11. <span data-ttu-id="7c1d2-156">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-156">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>

    ```objc
    - (IBAction)LogInAction:(id)sender {
        // create authentication header and set it in register client
        NSString* username = self.UsernameField.text;
        NSString* password = self.PasswordField.text;

        [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];

        __weak ViewController* selfie = self;
        [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil
            andCompletion:^(NSError* error) {
            if (!error) {
                dispatch_async(dispatch_get_main_queue(),
                ^{
                    selfie.SendNotificationButton.enabled = YES;
                    [self MessageBox:@"Success" message:@"Registered successfully!"];
                });
            }
        }];
    }

    - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag
                Message:(NSString*)message
    {
        NSURLSession* session = [NSURLSession
            sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil
            delegateQueue:nil];

        // Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend
        NSURL* requestURL = [NSURL URLWithString:[NSString
            stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,
            usernameTag]];

        NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
        [request setHTTPMethod:@"POST"];

        // Get the mock authenticationheader from the register client
        NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
            self.registerClient.authenticationHeader];
        [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

        //Add the notification message body
        [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
        [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];

        // Execute the send notification REST API on the ASP.NET Backend
        NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
            completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
        {
            NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
            if (error || httpResponse.statusCode != 200)
            {
                NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",
                                    pns, httpResponse.statusCode, error];
                dispatch_async(dispatch_get_main_queue(),
                ^{
                    // Append text because all 3 PNS calls may also have information to view
                    [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];
                });
                NSLog(status);
            }

            if (data != NULL)
            {
                xmlParser = [[NSXMLParser alloc] initWithData:data];
                [xmlParser setDelegate:self];
                [xmlParser parse];
            }
        }];
        [dataTask resume];
    }
    ```

12. <span data-ttu-id="7c1d2-157">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-157">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

    ```objc
    - (IBAction)SendNotificationMessage:(id)sender
    {
        //[self SendNotificationRESTAPI];
        [self SendToEnabledPlatforms];
    }

    -(void)SendToEnabledPlatforms
    {
        NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

        [self.sendResults setText:@""];

        if ([self.WNSSwitch isOn])
            [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

        if ([self.GCMSwitch isOn])
            [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

        if ([self.APNSSwitch isOn])
            [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
    }
    ```

13. <span data-ttu-id="7c1d2-158">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-158">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>

    ```objc
    self.UsernameField.delegate = self;
    self.PasswordField.delegate = self;
    self.RecipientField.delegate = self;
    self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
    ```

14. <span data-ttu-id="7c1d2-159">Now in **AppDelegate.m**, remove all the content of the method `application:didRegisterForPushNotificationWithDeviceToken:` and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-159">Now in **AppDelegate.m**, remove all the content of the method `application:didRegisterForPushNotificationWithDeviceToken:` and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>

    ```objc
    // Add import to the top of the file
    #import "ViewController.h"

    - (void)application:(UIApplication *)application
                didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
    {
        ViewController* rvc = (ViewController*) self.window.rootViewController;
        rvc.deviceToken = deviceToken;
    }
    ```

15. <span data-ttu-id="7c1d2-160">Finally in **AppDelegate.m**, make sure you have the following method:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-160">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>

    ```objc
    - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
        NSLog(@"%@", userInfo);
        [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
    }
    ```

## <a name="test-the-application"></a><span data-ttu-id="7c1d2-161">Test the application</span><span class="sxs-lookup"><span data-stu-id="7c1d2-161">Test the application</span></span>

1. <span data-ttu-id="7c1d2-162">In XCode, run the app on a physical iOS device (push notifications do not work in the simulator).</span><span class="sxs-lookup"><span data-stu-id="7c1d2-162">In XCode, run the app on a physical iOS device (push notifications do not work in the simulator).</span></span>
2. <span data-ttu-id="7c1d2-163">In the iOS app UI, enter same value for both username and password.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-163">In the iOS app UI, enter same value for both username and password.</span></span> <span data-ttu-id="7c1d2-164">Then click **Log In**.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-164">Then click **Log In**.</span></span>

    ![iOS test application][2]

3. <span data-ttu-id="7c1d2-166">You should see a pop-up informing you of registration success.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-166">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="7c1d2-167">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-167">Click **OK**.</span></span>

    ![iOS test notification displayed][3]

4. <span data-ttu-id="7c1d2-169">In the \**Recipient username tag* text field, enter the user name tag used with the registration from another device.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-169">In the \**Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="7c1d2-170">Enter a notification message and click **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-170">Enter a notification message and click **Send Notification**.</span></span> <span data-ttu-id="7c1d2-171">Only the devices that have a registration with the recipient user name tag receive the notification message.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-171">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span> <span data-ttu-id="7c1d2-172">It is only sent to those users.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-172">It is only sent to those users.</span></span>

    ![iOS test tagged notification][4]

## <a name="next-steps"></a><span data-ttu-id="7c1d2-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c1d2-174">Next steps</span></span>

<span data-ttu-id="7c1d2-175">In this tutorial, you learned how to push notifications to specific users that have tags associated with their registrations.</span><span class="sxs-lookup"><span data-stu-id="7c1d2-175">In this tutorial, you learned how to push notifications to specific users that have tags associated with their registrations.</span></span> <span data-ttu-id="7c1d2-176">To learn how to push location-based notifications, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="7c1d2-176">To learn how to push location-based notifications, advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="7c1d2-177">Push location-based notifications</span><span class="sxs-lookup"><span data-stu-id="7c1d2-177">Push location-based notifications</span></span>](notification-hubs-push-bing-spartial-data-geofencing-notification.md)


[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
