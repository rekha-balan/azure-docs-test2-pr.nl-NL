---
title: Sending push notifications to iOS with Azure Notification Hubs | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to send push notifications to an iOS application.
services: notification-hubs
documentationcenter: ios
keywords: push notification,push notifications,ios push notifications
author: ysxu
manager: erikre
editor: ''
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 649376272fff6593defc0da5fae16ff7d269020d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556527"
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="da853-104">Sending push notifications to iOS with Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="da853-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="da853-105">Overview</span><span class="sxs-lookup"><span data-stu-id="da853-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="da853-106">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="da853-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="da853-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="da853-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="da853-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="da853-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="da853-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span><span class="sxs-lookup"><span data-stu-id="da853-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="da853-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="da853-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="da853-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span><span class="sxs-lookup"><span data-stu-id="da853-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="da853-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="da853-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="da853-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="da853-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="da853-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="da853-114">Prerequisites</span></span>
<span data-ttu-id="da853-115">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="da853-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="da853-116">[Mobile Services iOS SDK version 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="da853-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="da853-117">Latest version of [Xcode]</span><span class="sxs-lookup"><span data-stu-id="da853-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="da853-118">An iOS 8 (or later version)-capable device</span><span class="sxs-lookup"><span data-stu-id="da853-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="da853-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span><span class="sxs-lookup"><span data-stu-id="da853-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="da853-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span><span class="sxs-lookup"><span data-stu-id="da853-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="da853-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span><span class="sxs-lookup"><span data-stu-id="da853-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="da853-122">Configure your Notification Hub for iOS push notifications</span><span class="sxs-lookup"><span data-stu-id="da853-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="da853-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span><span class="sxs-lookup"><span data-stu-id="da853-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="da853-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span><span class="sxs-lookup"><span data-stu-id="da853-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="da853-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="da853-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="da853-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span><span class="sxs-lookup"><span data-stu-id="da853-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="da853-127">Make sure you also specify the correct password.</span><span class="sxs-lookup"><span data-stu-id="da853-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="da853-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span><span class="sxs-lookup"><span data-stu-id="da853-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="da853-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span><span class="sxs-lookup"><span data-stu-id="da853-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="da853-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="da853-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configure APNS certification in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="da853-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span><span class="sxs-lookup"><span data-stu-id="da853-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="da853-133">Connect your iOS app to Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="da853-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="da853-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span><span class="sxs-lookup"><span data-stu-id="da853-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode - Single View Application][8]
    
2. <span data-ttu-id="da853-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="da853-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode - project options][11]
    
3. <span data-ttu-id="da853-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span><span class="sxs-lookup"><span data-stu-id="da853-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="da853-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span><span class="sxs-lookup"><span data-stu-id="da853-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="da853-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span><span class="sxs-lookup"><span data-stu-id="da853-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="da853-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span><span class="sxs-lookup"><span data-stu-id="da853-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode - provisioning profile][9]
4. <span data-ttu-id="da853-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span><span class="sxs-lookup"><span data-stu-id="da853-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="da853-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span><span class="sxs-lookup"><span data-stu-id="da853-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="da853-145">Select **Copy items if needed**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="da853-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da853-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="da853-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="da853-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span><span class="sxs-lookup"><span data-stu-id="da853-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Unzip Azure SDK][10]
5. <span data-ttu-id="da853-149">Add a new header file to your project named `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="da853-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="da853-150">This file will hold the constants for your notification hub.</span><span class="sxs-lookup"><span data-stu-id="da853-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="da853-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="da853-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="da853-152">Open your `AppDelegate.h` file add the following import directives:</span><span class="sxs-lookup"><span data-stu-id="da853-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="da853-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span><span class="sxs-lookup"><span data-stu-id="da853-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="da853-154">This code registers your device handle with APNs:</span><span class="sxs-lookup"><span data-stu-id="da853-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="da853-155">For iOS 8:</span><span class="sxs-lookup"><span data-stu-id="da853-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="da853-156">For iOS versions prior to 8:</span><span class="sxs-lookup"><span data-stu-id="da853-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="da853-157">In the same file, add the following methods.</span><span class="sxs-lookup"><span data-stu-id="da853-157">In the same file, add the following methods.</span></span> <span data-ttu-id="da853-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="da853-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="da853-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span><span class="sxs-lookup"><span data-stu-id="da853-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="da853-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span><span class="sxs-lookup"><span data-stu-id="da853-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="da853-161">Build and run the app on your device to verify that there are no failures.</span><span class="sxs-lookup"><span data-stu-id="da853-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="da853-162">Send test push notifications</span><span class="sxs-lookup"><span data-stu-id="da853-162">Send test push notifications</span></span>
<span data-ttu-id="da853-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span><span class="sxs-lookup"><span data-stu-id="da853-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Azure Portal - Test Send][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="da853-165">(Optional) Send push notifications from the app</span><span class="sxs-lookup"><span data-stu-id="da853-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="da853-166">This example of sending notifications from the client app is provided for learning purposes only.</span><span class="sxs-lookup"><span data-stu-id="da853-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="da853-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span><span class="sxs-lookup"><span data-stu-id="da853-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="da853-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span><span class="sxs-lookup"><span data-stu-id="da853-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="da853-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span><span class="sxs-lookup"><span data-stu-id="da853-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="da853-170">A label with no label text.</span><span class="sxs-lookup"><span data-stu-id="da853-170">A label with no label text.</span></span> <span data-ttu-id="da853-171">It will be used to report errors in sending notifications.</span><span class="sxs-lookup"><span data-stu-id="da853-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="da853-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span><span class="sxs-lookup"><span data-stu-id="da853-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="da853-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span><span class="sxs-lookup"><span data-stu-id="da853-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="da853-174">Constrain the field just below the label as shown below.</span><span class="sxs-lookup"><span data-stu-id="da853-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="da853-175">Set the View Controller as the outlet delegate.</span><span class="sxs-lookup"><span data-stu-id="da853-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="da853-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span><span class="sxs-lookup"><span data-stu-id="da853-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="da853-177">The view should look as follows:</span><span class="sxs-lookup"><span data-stu-id="da853-177">The view should look as follows:</span></span>
     
     ![Xcode designer][32]
2. <span data-ttu-id="da853-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="da853-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="da853-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span><span class="sxs-lookup"><span data-stu-id="da853-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="da853-181">Your ViewController.h file should look as follows:</span><span class="sxs-lookup"><span data-stu-id="da853-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="da853-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span><span class="sxs-lookup"><span data-stu-id="da853-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="da853-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span><span class="sxs-lookup"><span data-stu-id="da853-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="da853-184">Add the following `#import` statements to your `ViewController.h` file.</span><span class="sxs-lookup"><span data-stu-id="da853-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="da853-185">In `ViewController.m` add the following code to the interface implementation.</span><span class="sxs-lookup"><span data-stu-id="da853-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="da853-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span><span class="sxs-lookup"><span data-stu-id="da853-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="da853-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span><span class="sxs-lookup"><span data-stu-id="da853-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="da853-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span><span class="sxs-lookup"><span data-stu-id="da853-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="da853-189">Also add the utility methods, shown below, to the interface implementation.</span><span class="sxs-lookup"><span data-stu-id="da853-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="da853-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="da853-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="da853-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span><span class="sxs-lookup"><span data-stu-id="da853-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="da853-192">Update method with the following code to send the notification using the REST API.</span><span class="sxs-lookup"><span data-stu-id="da853-192">Update method with the following code to send the notification using the REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
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
3. <span data-ttu-id="da853-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span><span class="sxs-lookup"><span data-stu-id="da853-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="da853-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span><span class="sxs-lookup"><span data-stu-id="da853-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="da853-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="da853-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="da853-196">Build the project and verify that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="da853-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="da853-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span><span class="sxs-lookup"><span data-stu-id="da853-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="da853-198">The Notification Hubs SDK does not currently support bitcode.</span><span class="sxs-lookup"><span data-stu-id="da853-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="da853-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span><span class="sxs-lookup"><span data-stu-id="da853-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="da853-200">Checking if your app can receive push notifications</span><span class="sxs-lookup"><span data-stu-id="da853-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="da853-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span><span class="sxs-lookup"><span data-stu-id="da853-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="da853-202">You cannot send Apple push notifications by using the iOS Simulator.</span><span class="sxs-lookup"><span data-stu-id="da853-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="da853-203">Run the app and verify that registration succeeds, and then press **OK**.</span><span class="sxs-lookup"><span data-stu-id="da853-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![iOS App Push Notification Registration Test][33]
2. <span data-ttu-id="da853-205">You can send a test push notification from the [Azure Portal], as described above.</span><span class="sxs-lookup"><span data-stu-id="da853-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="da853-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span><span class="sxs-lookup"><span data-stu-id="da853-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="da853-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span><span class="sxs-lookup"><span data-stu-id="da853-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![iOS App Push Notification Send Test][34]
3. <span data-ttu-id="da853-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="da853-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![iOS App Push Notification Receive Test][35]

## <a name="next-steps"></a><span data-ttu-id="da853-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="da853-211">Next steps</span></span>
<span data-ttu-id="da853-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span><span class="sxs-lookup"><span data-stu-id="da853-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="da853-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span><span class="sxs-lookup"><span data-stu-id="da853-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="da853-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span><span class="sxs-lookup"><span data-stu-id="da853-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="da853-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span><span class="sxs-lookup"><span data-stu-id="da853-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com













