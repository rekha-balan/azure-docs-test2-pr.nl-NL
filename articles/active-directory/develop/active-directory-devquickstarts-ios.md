---
title: Azure AD iOS Getting Started | Microsoft Docs
description: How to build an iOS application that integrates with Azure AD for sign in and calls Azure AD protected APIs using OAuth.
services: active-directory
documentationcenter: ios
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: b91b59e1ffe9d8b92e25aa177aa229c2d38c0aaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549415"
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="6aa40-103">Integrate Azure AD into an iOS App</span><span class="sxs-lookup"><span data-stu-id="6aa40-103">Integrate Azure AD into an iOS App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="6aa40-104">Azure AD provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span><span class="sxs-lookup"><span data-stu-id="6aa40-104">Azure AD provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span>  <span data-ttu-id="6aa40-105">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="6aa40-105">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="6aa40-106">To demonstrate just how easy it is, here we’ll build a Objective C To-Do List application that:</span><span class="sxs-lookup"><span data-stu-id="6aa40-106">To demonstrate just how easy it is, here we’ll build a Objective C To-Do List application that:</span></span>

* <span data-ttu-id="6aa40-107">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="6aa40-107">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="6aa40-108">Searches a directory for users with a given alias.</span><span class="sxs-lookup"><span data-stu-id="6aa40-108">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="6aa40-109">To build the complete working application, you’ll need to:</span><span class="sxs-lookup"><span data-stu-id="6aa40-109">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="6aa40-110">Register your application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aa40-110">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="6aa40-111">Install & Configure ADAL.</span><span class="sxs-lookup"><span data-stu-id="6aa40-111">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="6aa40-112">Use ADAL to get tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aa40-112">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="6aa40-113">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6aa40-113">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  <span data-ttu-id="6aa40-114">You'll also need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="6aa40-114">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="6aa40-115">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6aa40-115">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

> [!TIP]
> <span data-ttu-id="6aa40-116">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that will help you get up and running with Azure Active Directory in just a few minutes!</span><span class="sxs-lookup"><span data-stu-id="6aa40-116">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that will help you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="6aa40-117">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span><span class="sxs-lookup"><span data-stu-id="6aa40-117">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="6aa40-118">When you’re finished, you will have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span><span class="sxs-lookup"><span data-stu-id="6aa40-118">When you’re finished, you will have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-will-be-for-ios"></a><span data-ttu-id="6aa40-119">1. Determine what your Redirect URI will be for iOS</span><span class="sxs-lookup"><span data-stu-id="6aa40-119">1. Determine what your Redirect URI will be for iOS</span></span>
<span data-ttu-id="6aa40-120">In order to securely launch your applications in certain SSO scenarios we require that you create a **Redirect URI** in a particular format.</span><span class="sxs-lookup"><span data-stu-id="6aa40-120">In order to securely launch your applications in certain SSO scenarios we require that you create a **Redirect URI** in a particular format.</span></span> <span data-ttu-id="6aa40-121">A Redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span><span class="sxs-lookup"><span data-stu-id="6aa40-121">A Redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>

<span data-ttu-id="6aa40-122">The iOS format for a Redirect URI is:</span><span class="sxs-lookup"><span data-stu-id="6aa40-122">The iOS format for a Redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="6aa40-123">**aap-scheme** - This is registered in your XCode project.</span><span class="sxs-lookup"><span data-stu-id="6aa40-123">**aap-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="6aa40-124">It is how other applications can call you.</span><span class="sxs-lookup"><span data-stu-id="6aa40-124">It is how other applications can call you.</span></span> <span data-ttu-id="6aa40-125">You can find this under Info.plist -> URL types -> URL Identifier.</span><span class="sxs-lookup"><span data-stu-id="6aa40-125">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="6aa40-126">You should create one if you don't already have one or more configured.</span><span class="sxs-lookup"><span data-stu-id="6aa40-126">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="6aa40-127">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span><span class="sxs-lookup"><span data-stu-id="6aa40-127">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="6aa40-128">An example for this QuickStart code would be: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="6aa40-128">An example for this QuickStart code would be: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="6aa40-129">2. Register the DirectorySearcher Application</span><span class="sxs-lookup"><span data-stu-id="6aa40-129">2. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="6aa40-130">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="6aa40-130">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="6aa40-131">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aa40-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aa40-132">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span><span class="sxs-lookup"><span data-stu-id="6aa40-132">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="6aa40-133">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6aa40-133">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6aa40-134">Click on **App registrations** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="6aa40-134">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="6aa40-135">Follow the prompts and create a new **Native Client Application**.</span><span class="sxs-lookup"><span data-stu-id="6aa40-135">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="6aa40-136">The **Name** of the application will describe your application to end-users</span><span class="sxs-lookup"><span data-stu-id="6aa40-136">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="6aa40-137">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span><span class="sxs-lookup"><span data-stu-id="6aa40-137">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="6aa40-138">Enter a value specific to your application based on the information above.</span><span class="sxs-lookup"><span data-stu-id="6aa40-138">Enter a value specific to your application based on the information above.</span></span>
6. <span data-ttu-id="6aa40-139">Once you've completed registration, AAD will assign your app a unique Application ID.</span><span class="sxs-lookup"><span data-stu-id="6aa40-139">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="6aa40-140">You'll need this value in the next sections, so copy it from the application tab.</span><span class="sxs-lookup"><span data-stu-id="6aa40-140">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="6aa40-141">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="6aa40-141">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="6aa40-142">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span><span class="sxs-lookup"><span data-stu-id="6aa40-142">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="6aa40-143">This will enable your application to query the Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="6aa40-143">This will enable your application to query the Graph API for users.</span></span>

## <a name="3-install--configure-adal"></a><span data-ttu-id="6aa40-144">3. Install & Configure ADAL</span><span class="sxs-lookup"><span data-stu-id="6aa40-144">3. Install & Configure ADAL</span></span>
<span data-ttu-id="6aa40-145">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="6aa40-145">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="6aa40-146">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span><span class="sxs-lookup"><span data-stu-id="6aa40-146">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="6aa40-147">Begin by adding ADAL to the DirectorySearcher project using Cocapods.</span><span class="sxs-lookup"><span data-stu-id="6aa40-147">Begin by adding ADAL to the DirectorySearcher project using Cocapods.</span></span>

```
$ vi Podfile
```
<span data-ttu-id="6aa40-148">Add the following to this podfile:</span><span class="sxs-lookup"><span data-stu-id="6aa40-148">Add the following to this podfile:</span></span>

```
source 'https://github.com/CocoaPods/Specs.git'
link_with ['QuickStart']
xcodeproj 'QuickStart'

pod 'ADALiOS'
```

<span data-ttu-id="6aa40-149">Now load the podfile using cocoapods.</span><span class="sxs-lookup"><span data-stu-id="6aa40-149">Now load the podfile using cocoapods.</span></span> <span data-ttu-id="6aa40-150">This will create a new XCode Workspace you will load.</span><span class="sxs-lookup"><span data-stu-id="6aa40-150">This will create a new XCode Workspace you will load.</span></span>

```
$ pod install
...
$ open QuickStart.xcworkspace
```

* <span data-ttu-id="6aa40-151">In the QuickStart project, open the plist file `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="6aa40-151">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="6aa40-152">Replace the values of the elements in the section to reflect the values you input into the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6aa40-152">Replace the values of the elements in the section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="6aa40-153">Your code will reference these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="6aa40-153">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="6aa40-154">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="6aa40-154">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="6aa40-155">The `clientId` is the clientId of your application you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="6aa40-155">The `clientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="6aa40-156">The `redirectUri` is the redirect url you registered in the portal.</span><span class="sxs-lookup"><span data-stu-id="6aa40-156">The `redirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="6aa40-157">4.    Use ADAL to Get Tokens from AAD</span><span class="sxs-lookup"><span data-stu-id="6aa40-157">4.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="6aa40-158">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span><span class="sxs-lookup"><span data-stu-id="6aa40-158">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

* <span data-ttu-id="6aa40-159">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span><span class="sxs-lookup"><span data-stu-id="6aa40-159">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="6aa40-160">This is where you pass ADAL the coordinates through a CompletionBlock to communicate with Azure AD and tell it how to cache tokens.</span><span class="sxs-lookup"><span data-stu-id="6aa40-160">This is where you pass ADAL the coordinates through a CompletionBlock to communicate with Azure AD and tell it how to cache tokens.</span></span>

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

* <span data-ttu-id="6aa40-161">Now we need to use this token to search for users in the graph.</span><span class="sxs-lookup"><span data-stu-id="6aa40-161">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="6aa40-162">Find the `// TODO: implement SearchUsersList` commentThis method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span><span class="sxs-lookup"><span data-stu-id="6aa40-162">Find the `// TODO: implement SearchUsersList` commentThis method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="6aa40-163">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span><span class="sxs-lookup"><span data-stu-id="6aa40-163">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

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
* <span data-ttu-id="6aa40-164">When your app requests a token by calling `getToken(...)`, ADAL will attempt to return a token without asking the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="6aa40-164">When your app requests a token by calling `getToken(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="6aa40-165">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span><span class="sxs-lookup"><span data-stu-id="6aa40-165">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="6aa40-166">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="6aa40-166">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="6aa40-167">Notice that the `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect information your app may need.</span><span class="sxs-lookup"><span data-stu-id="6aa40-167">Notice that the `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="6aa40-168">In the QuickStart, `tokenCacheStoreItem` is used to determine if authenitcation has already occurred.</span><span class="sxs-lookup"><span data-stu-id="6aa40-168">In the QuickStart, `tokenCacheStoreItem` is used to determine if authenitcation has already occurred.</span></span>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="6aa40-169">5: Build and Run the application</span><span class="sxs-lookup"><span data-stu-id="6aa40-169">5: Build and Run the application</span></span>
<span data-ttu-id="6aa40-170">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6aa40-170">Congratulations!</span></span> <span data-ttu-id="6aa40-171">You now have a working iOS application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="6aa40-171">You now have a working iOS application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="6aa40-172">If you haven't already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="6aa40-172">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="6aa40-173">Run your QuickStart app, and sign in with one of those users.</span><span class="sxs-lookup"><span data-stu-id="6aa40-173">Run your QuickStart app, and sign in with one of those users.</span></span>  <span data-ttu-id="6aa40-174">Search for other users based on their UPN.</span><span class="sxs-lookup"><span data-stu-id="6aa40-174">Search for other users based on their UPN.</span></span>  <span data-ttu-id="6aa40-175">Close the app, and re-run it.</span><span class="sxs-lookup"><span data-stu-id="6aa40-175">Close the app, and re-run it.</span></span>  <span data-ttu-id="6aa40-176">Notice how the user's session remains intact.</span><span class="sxs-lookup"><span data-stu-id="6aa40-176">Notice how the user's session remains intact.</span></span>

<span data-ttu-id="6aa40-177">ADAL makes it easy to incorporate all of these common identity features into your application.</span><span class="sxs-lookup"><span data-stu-id="6aa40-177">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="6aa40-178">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span><span class="sxs-lookup"><span data-stu-id="6aa40-178">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="6aa40-179">All you really need to know is a single API call, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="6aa40-179">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="6aa40-180">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6aa40-180">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="additional-scenarios"></a><span data-ttu-id="6aa40-181">Additional scenarios</span><span class="sxs-lookup"><span data-stu-id="6aa40-181">Additional scenarios</span></span>
<span data-ttu-id="6aa40-182">You can now move on to additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="6aa40-182">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="6aa40-183">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="6aa40-183">You may want to try:</span></span>

* [<span data-ttu-id="6aa40-184">Secure a Node.JS Web API with Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa40-184">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="6aa40-185">Learn [How to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="6aa40-185">Learn [How to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

