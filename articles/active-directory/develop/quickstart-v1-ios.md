---
title: Azure AD iOS getting started | Microsoft Docs
description: How to build an iOS application that integrates with Azure AD for sign-in and calls Azure AD protected APIs by using OAuth.
services: active-directory
documentationcenter: ios
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/30/2018
ms.author: celested
ms.custom: aaddev
ms.reviewer: jmprieur
ms.openlocfilehash: c370a90cf050a88e66ea0417f018429f7815b7c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864437"
---
# <a name="azure-ad-ios-getting-started"></a><span data-ttu-id="716ae-103">Azure AD iOS getting started</span><span class="sxs-lookup"><span data-stu-id="716ae-103">Azure AD iOS getting started</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

<span data-ttu-id="716ae-104">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span><span class="sxs-lookup"><span data-stu-id="716ae-104">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="716ae-105">ADAL simplifies the process that your app uses to obtain access tokens.</span><span class="sxs-lookup"><span data-stu-id="716ae-105">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="716ae-106">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span><span class="sxs-lookup"><span data-stu-id="716ae-106">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="716ae-107">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="716ae-107">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="716ae-108">Searches a directory for users with a given alias.</span><span class="sxs-lookup"><span data-stu-id="716ae-108">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="716ae-109">To build the complete working application, you need to:</span><span class="sxs-lookup"><span data-stu-id="716ae-109">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="716ae-110">Register your application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="716ae-110">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="716ae-111">Install and configure ADAL.</span><span class="sxs-lookup"><span data-stu-id="716ae-111">Install and configure ADAL.</span></span>
3. <span data-ttu-id="716ae-112">Use ADAL to get tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="716ae-112">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="716ae-113">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="716ae-113">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="716ae-114">You also need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="716ae-114">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="716ae-115">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="716ae-115">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="716ae-116">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="716ae-116">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="716ae-117">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span><span class="sxs-lookup"><span data-stu-id="716ae-117">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="716ae-118">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span><span class="sxs-lookup"><span data-stu-id="716ae-118">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="716ae-119">1. Determine what your redirect URI is for iOS</span><span class="sxs-lookup"><span data-stu-id="716ae-119">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="716ae-120">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span><span class="sxs-lookup"><span data-stu-id="716ae-120">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="716ae-121">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span><span class="sxs-lookup"><span data-stu-id="716ae-121">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="716ae-122">The iOS format for a redirect URI is:</span><span class="sxs-lookup"><span data-stu-id="716ae-122">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="716ae-123">**app-scheme** - This is registered in your XCode project.</span><span class="sxs-lookup"><span data-stu-id="716ae-123">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="716ae-124">It is how other applications can call you.</span><span class="sxs-lookup"><span data-stu-id="716ae-124">It is how other applications can call you.</span></span> <span data-ttu-id="716ae-125">You can find this under Info.plist -> URL types -> URL Identifier.</span><span class="sxs-lookup"><span data-stu-id="716ae-125">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="716ae-126">You should create one if you don't already have one or more configured.</span><span class="sxs-lookup"><span data-stu-id="716ae-126">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="716ae-127">**bundle-id** - This is the Bundle Identifier found under "identity" in your XCode project settings.</span><span class="sxs-lookup"><span data-stu-id="716ae-127">**bundle-id** - This is the Bundle Identifier found under "identity" in your XCode project settings.</span></span>

<span data-ttu-id="716ae-128">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="716ae-128">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="716ae-129">2. Register the DirectorySearcher application</span><span class="sxs-lookup"><span data-stu-id="716ae-129">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="716ae-130">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="716ae-130">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="716ae-131">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="716ae-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="716ae-132">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="716ae-132">On the top bar, click your account.</span></span> <span data-ttu-id="716ae-133">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="716ae-133">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="716ae-134">Click **All services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="716ae-134">Click **All services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="716ae-135">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="716ae-135">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="716ae-136">Follow the prompts to create a new **Native Client Application**.</span><span class="sxs-lookup"><span data-stu-id="716ae-136">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="716ae-137">The **Name** of the application describes your application to end users.</span><span class="sxs-lookup"><span data-stu-id="716ae-137">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="716ae-138">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span><span class="sxs-lookup"><span data-stu-id="716ae-138">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="716ae-139">Enter a value that is specific to your application and is based on the previous redirect URI information.</span><span class="sxs-lookup"><span data-stu-id="716ae-139">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="716ae-140">After you've completed the registration, Azure AD assigns your app a unique application ID.</span><span class="sxs-lookup"><span data-stu-id="716ae-140">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="716ae-141">You'll need this value in the next sections, so copy it from the application tab.</span><span class="sxs-lookup"><span data-stu-id="716ae-141">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="716ae-142">From the **Settings** page, select **Required Permissions** and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="716ae-142">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="716ae-143">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span><span class="sxs-lookup"><span data-stu-id="716ae-143">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span> <span data-ttu-id="716ae-144">This sets up your application to query the Azure AD Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="716ae-144">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="716ae-145">3. Install and configure ADAL</span><span class="sxs-lookup"><span data-stu-id="716ae-145">3. Install and configure ADAL</span></span>
<span data-ttu-id="716ae-146">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="716ae-146">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="716ae-147">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span><span class="sxs-lookup"><span data-stu-id="716ae-147">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="716ae-148">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="716ae-148">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="716ae-149">Add the following to this podfile:</span><span class="sxs-lookup"><span data-stu-id="716ae-149">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="716ae-150">Now load the podfile by using CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="716ae-150">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="716ae-151">This step creates a new XCode workspace that you load.</span><span class="sxs-lookup"><span data-stu-id="716ae-151">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="716ae-152">In the QuickStart project, open the plist file `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="716ae-152">In the QuickStart project, open the plist file `settings.plist`.</span></span> <span data-ttu-id="716ae-153">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="716ae-153">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="716ae-154">Your code references these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="716ae-154">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="716ae-155">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="716ae-155">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="716ae-156">The `clientId` is the client ID of your application that you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="716ae-156">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="716ae-157">The `redirectUri` is the redirect URL that you registered in the portal.</span><span class="sxs-lookup"><span data-stu-id="716ae-157">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="716ae-158">4. Use ADAL to get tokens from Azure AD</span><span class="sxs-lookup"><span data-stu-id="716ae-158">4. Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="716ae-159">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span><span class="sxs-lookup"><span data-stu-id="716ae-159">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span> 

1. <span data-ttu-id="716ae-160">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span><span class="sxs-lookup"><span data-stu-id="716ae-160">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span> <span data-ttu-id="716ae-161">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span><span class="sxs-lookup"><span data-stu-id="716ae-161">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="716ae-162">Now we need to use this token to search for users in the graph.</span><span class="sxs-lookup"><span data-stu-id="716ae-162">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="716ae-163">Find the `// TODO: implement SearchUsersList` comment.</span><span class="sxs-lookup"><span data-stu-id="716ae-163">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="716ae-164">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span><span class="sxs-lookup"><span data-stu-id="716ae-164">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="716ae-165">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span><span class="sxs-lookup"><span data-stu-id="716ae-165">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="716ae-166">This is where ADAL comes in.</span><span class="sxs-lookup"><span data-stu-id="716ae-166">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. <span data-ttu-id="716ae-167">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="716ae-167">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="716ae-168">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="716ae-168">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span> <span data-ttu-id="716ae-169">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="716ae-169">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="716ae-170">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span><span class="sxs-lookup"><span data-stu-id="716ae-170">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="716ae-171">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span><span class="sxs-lookup"><span data-stu-id="716ae-171">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="716ae-172">5. Build and run the application</span><span class="sxs-lookup"><span data-stu-id="716ae-172">5. Build and run the application</span></span>
<span data-ttu-id="716ae-173">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="716ae-173">Congratulations!</span></span> <span data-ttu-id="716ae-174">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="716ae-174">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="716ae-175">If you haven't already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="716ae-175">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="716ae-176">Start your QuickStart app, and then sign in with one of those users.</span><span class="sxs-lookup"><span data-stu-id="716ae-176">Start your QuickStart app, and then sign in with one of those users.</span></span> <span data-ttu-id="716ae-177">Search for other users based on their UPN.</span><span class="sxs-lookup"><span data-stu-id="716ae-177">Search for other users based on their UPN.</span></span> <span data-ttu-id="716ae-178">Close the app, and then start it again.</span><span class="sxs-lookup"><span data-stu-id="716ae-178">Close the app, and then start it again.</span></span> <span data-ttu-id="716ae-179">Notice that the user's session remains intact.</span><span class="sxs-lookup"><span data-stu-id="716ae-179">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="716ae-180">ADAL makes it easy to incorporate all of these common identity features into your application.</span><span class="sxs-lookup"><span data-stu-id="716ae-180">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span> <span data-ttu-id="716ae-181">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span><span class="sxs-lookup"><span data-stu-id="716ae-181">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span> <span data-ttu-id="716ae-182">All you really need to know is a single API call, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="716ae-182">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="716ae-183">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="716ae-183">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="716ae-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="716ae-184">Next steps</span></span>
<span data-ttu-id="716ae-185">You can now move on to additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="716ae-185">You can now move on to additional scenarios.</span></span> <span data-ttu-id="716ae-186">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="716ae-186">You may want to try:</span></span>

* [<span data-ttu-id="716ae-187">Secure a Node.JS Web API with Azure AD</span><span class="sxs-lookup"><span data-stu-id="716ae-187">Secure a Node.JS Web API with Azure AD</span></span>](quickstart-v1-nodejs-webapi.md)
* <span data-ttu-id="716ae-188">Learn [how to enable cross-app SSO on iOS using ADAL](howto-v1-enable-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="716ae-188">Learn [how to enable cross-app SSO on iOS using ADAL](howto-v1-enable-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

