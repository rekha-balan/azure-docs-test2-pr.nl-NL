---
title: Add sign-in to an iOS application using the Azure AD v2.0 endpoint | Microsoft Docs
description: How to build an iOS app that signs in users with both personal Microsoft account and work or school accounts by using third-party libraries.
services: active-directory
documentationcenter: ''
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 4d82b3085da8fb7ee4314756a46425dba39209c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554733"
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="ac17b-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="ac17b-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="ac17b-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ac17b-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="ac17b-105">Developers can use any library they want to integrate with our services.</span><span class="sxs-lookup"><span data-stu-id="ac17b-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="ac17b-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="ac17b-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="ac17b-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="ac17b-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="ac17b-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span><span class="sxs-lookup"><span data-stu-id="ac17b-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="ac17b-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span><span class="sxs-lookup"><span data-stu-id="ac17b-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="ac17b-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span><span class="sxs-lookup"><span data-stu-id="ac17b-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="ac17b-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span><span class="sxs-lookup"><span data-stu-id="ac17b-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="ac17b-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span><span class="sxs-lookup"><span data-stu-id="ac17b-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="ac17b-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ac17b-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="ac17b-114">Download code from GitHub</span><span class="sxs-lookup"><span data-stu-id="ac17b-114">Download code from GitHub</span></span>
<span data-ttu-id="ac17b-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="ac17b-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="ac17b-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="ac17b-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="ac17b-117">You can also just download the sample and get started right away:</span><span class="sxs-lookup"><span data-stu-id="ac17b-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="ac17b-118">Register an app</span><span class="sxs-lookup"><span data-stu-id="ac17b-118">Register an app</span></span>
<span data-ttu-id="ac17b-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ac17b-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="ac17b-120">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="ac17b-120">Make sure to:</span></span>

* <span data-ttu-id="ac17b-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span><span class="sxs-lookup"><span data-stu-id="ac17b-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="ac17b-122">Add the **Mobile** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="ac17b-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="ac17b-123">Copy the **Redirect URI** from the portal.</span><span class="sxs-lookup"><span data-stu-id="ac17b-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="ac17b-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="ac17b-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="ac17b-125">Download the third-party NXOAuth2 library and create a workspace</span><span class="sxs-lookup"><span data-stu-id="ac17b-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="ac17b-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="ac17b-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="ac17b-127">This library is based on draft 10 of the OAuth2 spec. It implements the native application profile and supports the authorization endpoint of the user.</span><span class="sxs-lookup"><span data-stu-id="ac17b-127">This library is based on draft 10 of the OAuth2 spec. It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="ac17b-128">These are all the things you'll need to integrate with the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="ac17b-128">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="ac17b-129">Add the library to your project by using CocoaPods</span><span class="sxs-lookup"><span data-stu-id="ac17b-129">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="ac17b-130">CocoaPods is a dependency manager for Xcode projects.</span><span class="sxs-lookup"><span data-stu-id="ac17b-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="ac17b-131">It manages the previous installation steps automatically.</span><span class="sxs-lookup"><span data-stu-id="ac17b-131">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="ac17b-132">Add the following to this podfile:</span><span class="sxs-lookup"><span data-stu-id="ac17b-132">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="ac17b-133">Load the podfile by using CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="ac17b-133">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="ac17b-134">This will create a new Xcode workspace that you will load.</span><span class="sxs-lookup"><span data-stu-id="ac17b-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="ac17b-135">Explore the structure of the project</span><span class="sxs-lookup"><span data-stu-id="ac17b-135">Explore the structure of the project</span></span>
<span data-ttu-id="ac17b-136">The following structure is set up for our project in the skeleton:</span><span class="sxs-lookup"><span data-stu-id="ac17b-136">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="ac17b-137">A Master View with a UPN Search</span><span class="sxs-lookup"><span data-stu-id="ac17b-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="ac17b-138">A Detail View for the data about the selected user</span><span class="sxs-lookup"><span data-stu-id="ac17b-138">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="ac17b-139">A Login View where a user can sign in to the app to query the graph</span><span class="sxs-lookup"><span data-stu-id="ac17b-139">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="ac17b-140">We will move to various files in the skeleton to add authentication.</span><span class="sxs-lookup"><span data-stu-id="ac17b-140">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="ac17b-141">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span><span class="sxs-lookup"><span data-stu-id="ac17b-141">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="ac17b-142">Set up the settings.plst file in the library</span><span class="sxs-lookup"><span data-stu-id="ac17b-142">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="ac17b-143">In the QuickStart project, open the `settings.plist` file.</span><span class="sxs-lookup"><span data-stu-id="ac17b-143">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="ac17b-144">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ac17b-144">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="ac17b-145">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="ac17b-145">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="ac17b-146">The `clientId` is the client ID of your application that you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="ac17b-146">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="ac17b-147">The `redirectUri` is the redirect URL that the portal provided.</span><span class="sxs-lookup"><span data-stu-id="ac17b-147">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="ac17b-148">Set up the NXOAuth2Client library in your LoginViewController</span><span class="sxs-lookup"><span data-stu-id="ac17b-148">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="ac17b-149">The NXOAuth2Client library requires some values to get set up.</span><span class="sxs-lookup"><span data-stu-id="ac17b-149">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="ac17b-150">After you complete that task, you can use the acquired token to call the Graph API.</span><span class="sxs-lookup"><span data-stu-id="ac17b-150">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="ac17b-151">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span><span class="sxs-lookup"><span data-stu-id="ac17b-151">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="ac17b-152">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span><span class="sxs-lookup"><span data-stu-id="ac17b-152">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="ac17b-153">Details about the values follow the code.</span><span class="sxs-lookup"><span data-stu-id="ac17b-153">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="ac17b-154">Let's look at details about the code.</span><span class="sxs-lookup"><span data-stu-id="ac17b-154">Let's look at details about the code.</span></span>

<span data-ttu-id="ac17b-155">The first string is for `scopes`.</span><span class="sxs-lookup"><span data-stu-id="ac17b-155">The first string is for `scopes`.</span></span>  <span data-ttu-id="ac17b-156">The `User.Read` value allows you to read the basic profile of the signed in user.</span><span class="sxs-lookup"><span data-stu-id="ac17b-156">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="ac17b-157">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="ac17b-157">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="ac17b-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span><span class="sxs-lookup"><span data-stu-id="ac17b-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="ac17b-159">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span><span class="sxs-lookup"><span data-stu-id="ac17b-159">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="ac17b-160">We've done the hard work of extracting these values for you.</span><span class="sxs-lookup"><span data-stu-id="ac17b-160">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="ac17b-161">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span><span class="sxs-lookup"><span data-stu-id="ac17b-161">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="ac17b-162">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span><span class="sxs-lookup"><span data-stu-id="ac17b-162">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="ac17b-163">This is explained in the Apple documentation.</span><span class="sxs-lookup"><span data-stu-id="ac17b-163">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="ac17b-164">The rest of these values are required to use the library and create places for you to carry values to the context.</span><span class="sxs-lookup"><span data-stu-id="ac17b-164">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="ac17b-165">Create a URL cache</span><span class="sxs-lookup"><span data-stu-id="ac17b-165">Create a URL cache</span></span>
<span data-ttu-id="ac17b-166">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span><span class="sxs-lookup"><span data-stu-id="ac17b-166">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="ac17b-167">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="ac17b-167">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="ac17b-168">Create a WebView for sign-in</span><span class="sxs-lookup"><span data-stu-id="ac17b-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="ac17b-169">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span><span class="sxs-lookup"><span data-stu-id="ac17b-169">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="ac17b-170">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span><span class="sxs-lookup"><span data-stu-id="ac17b-170">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="ac17b-171">Override the WebView methods to handle authentication</span><span class="sxs-lookup"><span data-stu-id="ac17b-171">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="ac17b-172">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span><span class="sxs-lookup"><span data-stu-id="ac17b-172">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="ac17b-173">Write code to handle the result of the OAuth2 request</span><span class="sxs-lookup"><span data-stu-id="ac17b-173">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="ac17b-174">The following code will handle the redirectURL that returns from the WebView.</span><span class="sxs-lookup"><span data-stu-id="ac17b-174">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="ac17b-175">If authentication wasn't successful, the code will try again.</span><span class="sxs-lookup"><span data-stu-id="ac17b-175">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="ac17b-176">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span><span class="sxs-lookup"><span data-stu-id="ac17b-176">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="ac17b-177">Set up the OAuth Context (called account store)</span><span class="sxs-lookup"><span data-stu-id="ac17b-177">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="ac17b-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span><span class="sxs-lookup"><span data-stu-id="ac17b-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="ac17b-179">The account type is a string that is used as an identifier for a certain service.</span><span class="sxs-lookup"><span data-stu-id="ac17b-179">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="ac17b-180">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="ac17b-180">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="ac17b-181">You then set up an observer that will tell you when anything changes with the token.</span><span class="sxs-lookup"><span data-stu-id="ac17b-181">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="ac17b-182">After you get the token, you return the user back to the `masterView`.</span><span class="sxs-lookup"><span data-stu-id="ac17b-182">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="ac17b-183">Set up the Master View to search and display the users from the Graph API</span><span class="sxs-lookup"><span data-stu-id="ac17b-183">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="ac17b-184">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span><span class="sxs-lookup"><span data-stu-id="ac17b-184">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="ac17b-185">All this code is in the skeleton file.</span><span class="sxs-lookup"><span data-stu-id="ac17b-185">All this code is in the skeleton file.</span></span> <span data-ttu-id="ac17b-186">However, you do need to deal with a few things in this MVC application:</span><span class="sxs-lookup"><span data-stu-id="ac17b-186">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="ac17b-187">Intercept when a user types something in the search field</span><span class="sxs-lookup"><span data-stu-id="ac17b-187">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="ac17b-188">Provide an object of data back to the MasterView so it can display the results in the grid</span><span class="sxs-lookup"><span data-stu-id="ac17b-188">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="ac17b-189">We'll do those below.</span><span class="sxs-lookup"><span data-stu-id="ac17b-189">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="ac17b-190">Add a check to see if you're logged in</span><span class="sxs-lookup"><span data-stu-id="ac17b-190">Add a check to see if you're logged in</span></span>
<span data-ttu-id="ac17b-191">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span><span class="sxs-lookup"><span data-stu-id="ac17b-191">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="ac17b-192">If not, you redirect to the LoginView for the user to sign in.</span><span class="sxs-lookup"><span data-stu-id="ac17b-192">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="ac17b-193">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span><span class="sxs-lookup"><span data-stu-id="ac17b-193">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="ac17b-194">Update the Table View when data is received</span><span class="sxs-lookup"><span data-stu-id="ac17b-194">Update the Table View when data is received</span></span>
<span data-ttu-id="ac17b-195">When the Graph API returns data, you need to display the data.</span><span class="sxs-lookup"><span data-stu-id="ac17b-195">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="ac17b-196">For simplicity, here is all the code to update the table.</span><span class="sxs-lookup"><span data-stu-id="ac17b-196">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="ac17b-197">You can just paste the right values in your MVC boilerplate code.</span><span class="sxs-lookup"><span data-stu-id="ac17b-197">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="ac17b-198">Provide a way to call the Graph API when someone types in the search field</span><span class="sxs-lookup"><span data-stu-id="ac17b-198">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="ac17b-199">When a user types a search in the box, you need to shove that over to the Graph API.</span><span class="sxs-lookup"><span data-stu-id="ac17b-199">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="ac17b-200">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span><span class="sxs-lookup"><span data-stu-id="ac17b-200">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="ac17b-201">For now, let's write the code that feeds any search characters to the Graph API.</span><span class="sxs-lookup"><span data-stu-id="ac17b-201">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="ac17b-202">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span><span class="sxs-lookup"><span data-stu-id="ac17b-202">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="ac17b-203">Write a Helper class to access the Graph API</span><span class="sxs-lookup"><span data-stu-id="ac17b-203">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="ac17b-204">This is the core of our application.</span><span class="sxs-lookup"><span data-stu-id="ac17b-204">This is the core of our application.</span></span> <span data-ttu-id="ac17b-205">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span><span class="sxs-lookup"><span data-stu-id="ac17b-205">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="ac17b-206">Here's the code, and a detailed explanation follows it.</span><span class="sxs-lookup"><span data-stu-id="ac17b-206">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="ac17b-207">Create a new Objective C header file</span><span class="sxs-lookup"><span data-stu-id="ac17b-207">Create a new Objective C header file</span></span>
<span data-ttu-id="ac17b-208">Name the file `GraphAPICaller.h`, and add the following code.</span><span class="sxs-lookup"><span data-stu-id="ac17b-208">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="ac17b-209">Here you see that a specified method takes a string and returns a completionBlock.</span><span class="sxs-lookup"><span data-stu-id="ac17b-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="ac17b-210">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span><span class="sxs-lookup"><span data-stu-id="ac17b-210">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="ac17b-211">Create a new Objective C file</span><span class="sxs-lookup"><span data-stu-id="ac17b-211">Create a new Objective C file</span></span>
<span data-ttu-id="ac17b-212">Name the file `GraphAPICaller.m`, and add the following method.</span><span class="sxs-lookup"><span data-stu-id="ac17b-212">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="ac17b-213">Let's go through this method in detail.</span><span class="sxs-lookup"><span data-stu-id="ac17b-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="ac17b-214">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span><span class="sxs-lookup"><span data-stu-id="ac17b-214">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="ac17b-215">The first step is to construct the right Graph API call.</span><span class="sxs-lookup"><span data-stu-id="ac17b-215">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="ac17b-216">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span><span class="sxs-lookup"><span data-stu-id="ac17b-216">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="ac17b-217">It makes sense to put these in an external settings file because these can change as the API evolves.</span><span class="sxs-lookup"><span data-stu-id="ac17b-217">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="ac17b-218">Next, you need to specify parameters that you will also provide to the Graph API call.</span><span class="sxs-lookup"><span data-stu-id="ac17b-218">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="ac17b-219">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span><span class="sxs-lookup"><span data-stu-id="ac17b-219">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="ac17b-220">All query code must be provided in the parameters.</span><span class="sxs-lookup"><span data-stu-id="ac17b-220">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="ac17b-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span><span class="sxs-lookup"><span data-stu-id="ac17b-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="ac17b-222">Let's do so now at the end of the file:</span><span class="sxs-lookup"><span data-stu-id="ac17b-222">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="ac17b-223">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span><span class="sxs-lookup"><span data-stu-id="ac17b-223">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="ac17b-224">Finally, let's look at how you return the data to the MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="ac17b-224">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="ac17b-225">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span><span class="sxs-lookup"><span data-stu-id="ac17b-225">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="ac17b-226">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span><span class="sxs-lookup"><span data-stu-id="ac17b-226">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="ac17b-227">You populate that User object with information from the graph.</span><span class="sxs-lookup"><span data-stu-id="ac17b-227">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="ac17b-228">Run the sample</span><span class="sxs-lookup"><span data-stu-id="ac17b-228">Run the sample</span></span>
<span data-ttu-id="ac17b-229">If you've used the skeleton or followed along with the walkthrough your application should now run.</span><span class="sxs-lookup"><span data-stu-id="ac17b-229">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="ac17b-230">Start the simulator and click **Sign in** to use the application.</span><span class="sxs-lookup"><span data-stu-id="ac17b-230">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="ac17b-231">Get security updates for our product</span><span class="sxs-lookup"><span data-stu-id="ac17b-231">Get security updates for our product</span></span>
<span data-ttu-id="ac17b-232">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="ac17b-232">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

