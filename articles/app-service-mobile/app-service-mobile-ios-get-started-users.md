---
title: Add Authentication on iOS with Azure Mobile Apps
description: Learn how to use Azure Mobile Apps to authenticate users of your iOS app through a variety of identity providers, including AAD, Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: ios
author: conceptdev
manager: crdun
editor: ''
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: crdun
ms.openlocfilehash: e0eeee05ebad2e8148752f988bbbc2f6a0d7c296
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789131"
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="4a85e-103">Add authentication to your iOS app</span><span class="sxs-lookup"><span data-stu-id="4a85e-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="4a85e-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span><span class="sxs-lookup"><span data-stu-id="4a85e-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="4a85e-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span><span class="sxs-lookup"><span data-stu-id="4a85e-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <a name="register"></a><span data-ttu-id="4a85e-106">Register your app for authentication and configure the App Service</span><span class="sxs-lookup"><span data-stu-id="4a85e-106">Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a><span data-ttu-id="4a85e-107">Add your app to the Allowed External Redirect URLs</span><span class="sxs-lookup"><span data-stu-id="4a85e-107">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="4a85e-108">Secure authentication requires that you define a new URL scheme for your app.</span><span class="sxs-lookup"><span data-stu-id="4a85e-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="4a85e-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span><span class="sxs-lookup"><span data-stu-id="4a85e-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="4a85e-110">In this tutorial, we use the URL scheme _appname_ throughout.</span><span class="sxs-lookup"><span data-stu-id="4a85e-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="4a85e-111">However, you can use any URL scheme you choose.</span><span class="sxs-lookup"><span data-stu-id="4a85e-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="4a85e-112">It should be unique to your mobile application.</span><span class="sxs-lookup"><span data-stu-id="4a85e-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="4a85e-113">To enable the redirection on th server side:</span><span class="sxs-lookup"><span data-stu-id="4a85e-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="4a85e-114">In the [Azure portal], select your App Service.</span><span class="sxs-lookup"><span data-stu-id="4a85e-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="4a85e-115">Click the **Authentication / Authorization** menu option.</span><span class="sxs-lookup"><span data-stu-id="4a85e-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="4a85e-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span><span class="sxs-lookup"><span data-stu-id="4a85e-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="4a85e-117">Set the **Management mode** to **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="4a85e-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="4a85e-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="4a85e-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="4a85e-119">The _appname_ in this string is the URL Scheme for your mobile application.</span><span class="sxs-lookup"><span data-stu-id="4a85e-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="4a85e-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span><span class="sxs-lookup"><span data-stu-id="4a85e-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="4a85e-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span><span class="sxs-lookup"><span data-stu-id="4a85e-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="4a85e-122">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a85e-122">Click **OK**.</span></span>

7. <span data-ttu-id="4a85e-123">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4a85e-123">Click **Save**.</span></span>

## <a name="permissions"></a><span data-ttu-id="4a85e-124">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="4a85e-124">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="4a85e-125">In Xcode, press **Run** to start the app.</span><span class="sxs-lookup"><span data-stu-id="4a85e-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="4a85e-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="4a85e-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <a name="add-authentication"></a><span data-ttu-id="4a85e-127">Add authentication to app</span><span class="sxs-lookup"><span data-stu-id="4a85e-127">Add authentication to app</span></span>
<span data-ttu-id="4a85e-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4a85e-128">**Objective-C**:</span></span>

1. <span data-ttu-id="4a85e-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span><span class="sxs-lookup"><span data-stu-id="4a85e-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="4a85e-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span><span class="sxs-lookup"><span data-stu-id="4a85e-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="4a85e-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span><span class="sxs-lookup"><span data-stu-id="4a85e-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="4a85e-132">Replace the **urlScheme** with a unique name for your application.</span><span class="sxs-lookup"><span data-stu-id="4a85e-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="4a85e-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4a85e-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="4a85e-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span><span class="sxs-lookup"><span data-stu-id="4a85e-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="4a85e-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span><span class="sxs-lookup"><span data-stu-id="4a85e-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="4a85e-136">Open the `QSAppDelegate.h` file and add the following code:</span><span class="sxs-lookup"><span data-stu-id="4a85e-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="4a85e-137">Open the `QSAppDelegate.m` file and add the following code:</span><span class="sxs-lookup"><span data-stu-id="4a85e-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="4a85e-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="4a85e-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="4a85e-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span><span class="sxs-lookup"><span data-stu-id="4a85e-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="4a85e-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span><span class="sxs-lookup"><span data-stu-id="4a85e-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="4a85e-141">This code should be placed inside the `<dict>` element.</span><span class="sxs-lookup"><span data-stu-id="4a85e-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="4a85e-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span><span class="sxs-lookup"><span data-stu-id="4a85e-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="4a85e-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span><span class="sxs-lookup"><span data-stu-id="4a85e-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="4a85e-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span><span class="sxs-lookup"><span data-stu-id="4a85e-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="4a85e-145">Press *Run* to start the app, and then log in.</span><span class="sxs-lookup"><span data-stu-id="4a85e-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="4a85e-146">When you are logged in, you should be able to view the Todo list and make updates.</span><span class="sxs-lookup"><span data-stu-id="4a85e-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="4a85e-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="4a85e-147">**Swift**:</span></span>

1. <span data-ttu-id="4a85e-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span><span class="sxs-lookup"><span data-stu-id="4a85e-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="4a85e-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span><span class="sxs-lookup"><span data-stu-id="4a85e-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="4a85e-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span><span class="sxs-lookup"><span data-stu-id="4a85e-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="4a85e-151">Replace the **urlScheme** with a unique name for your application.</span><span class="sxs-lookup"><span data-stu-id="4a85e-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="4a85e-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4a85e-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="4a85e-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span><span class="sxs-lookup"><span data-stu-id="4a85e-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="4a85e-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="4a85e-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="4a85e-155">Add a call to `loginAndGetData()` in their place:</span><span class="sxs-lookup"><span data-stu-id="4a85e-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="4a85e-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span><span class="sxs-lookup"><span data-stu-id="4a85e-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="4a85e-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span><span class="sxs-lookup"><span data-stu-id="4a85e-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="4a85e-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span><span class="sxs-lookup"><span data-stu-id="4a85e-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="4a85e-159">This code should be placed inside the `<dict>` element.</span><span class="sxs-lookup"><span data-stu-id="4a85e-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="4a85e-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span><span class="sxs-lookup"><span data-stu-id="4a85e-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="4a85e-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span><span class="sxs-lookup"><span data-stu-id="4a85e-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="4a85e-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span><span class="sxs-lookup"><span data-stu-id="4a85e-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="4a85e-163">Press *Run* to start the app, and then log in.</span><span class="sxs-lookup"><span data-stu-id="4a85e-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="4a85e-164">When you are logged in, you should be able to view the Todo list and make updates.</span><span class="sxs-lookup"><span data-stu-id="4a85e-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="4a85e-165">App Service Authentication uses Apples Inter-App Communication.</span><span class="sxs-lookup"><span data-stu-id="4a85e-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="4a85e-166">For more details on this subject, refer to the [Apple Documentation][2]
<!-- URLs. --></span><span class="sxs-lookup"><span data-stu-id="4a85e-166">For more details on this subject, refer to the [Apple Documentation][2]
<!-- URLs. --></span></span>

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure portal]: https://portal.azure.com

[iOS quick start]: app-service-mobile-ios-get-started.md

