---
title: 'Azure Active Directory B2C: Acquiring a token using an iOS application | Microsoft Docs'
description: This article will show you how to create an iOS app that uses AppAuth with Azure Active Directory B2C to manage user identities and authenticate users.
services: active-directory-b2c
documentationcenter: ios
author: saeeda
manager: krassk
editor: ''
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeeda
ms.openlocfilehash: 992bbf513ac87b0d955f9dc4b27984ef03050b83
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540809"
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="5a98f-103">Azure AD B2C: Sign-in using an iOS application</span><span class="sxs-lookup"><span data-stu-id="5a98f-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="5a98f-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5a98f-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="5a98f-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span><span class="sxs-lookup"><span data-stu-id="5a98f-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="5a98f-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="5a98f-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="5a98f-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="5a98f-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="5a98f-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span><span class="sxs-lookup"><span data-stu-id="5a98f-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="5a98f-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5a98f-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="5a98f-110">Issues and feature requests should be directed to the library's open-source project.</span><span class="sxs-lookup"><span data-stu-id="5a98f-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="5a98f-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="5a98f-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="5a98f-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span><span class="sxs-lookup"><span data-stu-id="5a98f-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="5a98f-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="5a98f-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

<span data-ttu-id="5a98f-114">Not all Azure Active Directory scenarios & features are supported by the B2C platform.</span><span class="sxs-lookup"><span data-stu-id="5a98f-114">Not all Azure Active Directory scenarios & features are supported by the B2C platform.</span></span>  <span data-ttu-id="5a98f-115">To determine if you should use the B2C platform, read about [B2C limitations](active-directory-b2c-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="5a98f-115">To determine if you should use the B2C platform, read about [B2C limitations](active-directory-b2c-limitations.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="5a98f-116">Get an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="5a98f-116">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="5a98f-117">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="5a98f-117">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="5a98f-118">A directory is a container for all your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="5a98f-118">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="5a98f-119">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span><span class="sxs-lookup"><span data-stu-id="5a98f-119">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="5a98f-120">Create an application</span><span class="sxs-lookup"><span data-stu-id="5a98f-120">Create an application</span></span>
<span data-ttu-id="5a98f-121">Next, you need to create an app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="5a98f-121">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="5a98f-122">The app registration gives Azure AD information that it needs to communicate securely with your app.</span><span class="sxs-lookup"><span data-stu-id="5a98f-122">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="5a98f-123">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5a98f-123">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="5a98f-124">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="5a98f-124">Be sure to:</span></span>

* <span data-ttu-id="5a98f-125">Include a **Native client** in the application.</span><span class="sxs-lookup"><span data-stu-id="5a98f-125">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="5a98f-126">Copy the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="5a98f-126">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="5a98f-127">You need this GUID later.</span><span class="sxs-lookup"><span data-stu-id="5a98f-127">You need this GUID later.</span></span>
* <span data-ttu-id="5a98f-128">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="5a98f-128">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="5a98f-129">You need this URI later.</span><span class="sxs-lookup"><span data-stu-id="5a98f-129">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="5a98f-130">Create your policies</span><span class="sxs-lookup"><span data-stu-id="5a98f-130">Create your policies</span></span>
<span data-ttu-id="5a98f-131">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5a98f-131">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5a98f-132">This app contains one identity experience: a combined sign-in and sign-up.</span><span class="sxs-lookup"><span data-stu-id="5a98f-132">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="5a98f-133">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="5a98f-133">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="5a98f-134">When you create the policy, be sure to:</span><span class="sxs-lookup"><span data-stu-id="5a98f-134">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="5a98f-135">Under **Sign-up attributes**, select the attribute **Display name**.</span><span class="sxs-lookup"><span data-stu-id="5a98f-135">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="5a98f-136">You can select other attributes as well.</span><span class="sxs-lookup"><span data-stu-id="5a98f-136">You can select other attributes as well.</span></span>
* <span data-ttu-id="5a98f-137">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span><span class="sxs-lookup"><span data-stu-id="5a98f-137">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="5a98f-138">You can select other claims as well.</span><span class="sxs-lookup"><span data-stu-id="5a98f-138">You can select other claims as well.</span></span>
* <span data-ttu-id="5a98f-139">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="5a98f-139">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="5a98f-140">Your policy name is prefixed with `b2c_1_` when you save the policy.</span><span class="sxs-lookup"><span data-stu-id="5a98f-140">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="5a98f-141">You need the policy name later.</span><span class="sxs-lookup"><span data-stu-id="5a98f-141">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="5a98f-142">After you have created your policies, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="5a98f-142">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="5a98f-143">Download the sample code</span><span class="sxs-lookup"><span data-stu-id="5a98f-143">Download the sample code</span></span>
<span data-ttu-id="5a98f-144">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="5a98f-144">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="5a98f-145">You can download the code and run it.</span><span class="sxs-lookup"><span data-stu-id="5a98f-145">You can download the code and run it.</span></span> <span data-ttu-id="5a98f-146">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5a98f-146">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="5a98f-147">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="5a98f-147">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="5a98f-148">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a98f-148">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="5a98f-149">Modifying your app to use Azure AD B2C with AppAuth</span><span class="sxs-lookup"><span data-stu-id="5a98f-149">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="5a98f-150">AppAuth supports iOS 7 and above.</span><span class="sxs-lookup"><span data-stu-id="5a98f-150">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="5a98f-151">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span><span class="sxs-lookup"><span data-stu-id="5a98f-151">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="5a98f-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="5a98f-152">Configuration</span></span>

<span data-ttu-id="5a98f-153">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span><span class="sxs-lookup"><span data-stu-id="5a98f-153">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="5a98f-154">To generate these URIs, you need the following information:</span><span class="sxs-lookup"><span data-stu-id="5a98f-154">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="5a98f-155">Tenant ID (for example, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="5a98f-155">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="5a98f-156">Policy name (for example, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="5a98f-156">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="5a98f-157">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span><span class="sxs-lookup"><span data-stu-id="5a98f-157">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="5a98f-158">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span><span class="sxs-lookup"><span data-stu-id="5a98f-158">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="5a98f-159">Run the following code to create your AuthorizationServiceConfiguration object:</span><span class="sxs-lookup"><span data-stu-id="5a98f-159">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="5a98f-160">Authorizing</span><span class="sxs-lookup"><span data-stu-id="5a98f-160">Authorizing</span></span>

<span data-ttu-id="5a98f-161">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span><span class="sxs-lookup"><span data-stu-id="5a98f-161">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="5a98f-162">To create the request, you need the following information:</span><span class="sxs-lookup"><span data-stu-id="5a98f-162">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="5a98f-163">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="5a98f-163">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="5a98f-164">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="5a98f-164">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="5a98f-165">Both items should have been saved when you were [registering your app](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="5a98f-165">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="5a98f-166">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span><span class="sxs-lookup"><span data-stu-id="5a98f-166">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="5a98f-167">Open Info.pList.</span><span class="sxs-lookup"><span data-stu-id="5a98f-167">Open Info.pList.</span></span>
* <span data-ttu-id="5a98f-168">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span><span class="sxs-lookup"><span data-stu-id="5a98f-168">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="5a98f-169">Rename the new row 'URL types'.</span><span class="sxs-lookup"><span data-stu-id="5a98f-169">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="5a98f-170">Click the arrow to the left of 'URL types' to open the tree.</span><span class="sxs-lookup"><span data-stu-id="5a98f-170">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="5a98f-171">Click the arrow to the left of 'Item 0' to open the tree.</span><span class="sxs-lookup"><span data-stu-id="5a98f-171">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="5a98f-172">Rename first item underneath Item 0 to 'URL Schemes'.</span><span class="sxs-lookup"><span data-stu-id="5a98f-172">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="5a98f-173">Click the arrow to the left of 'URL Schemes' to open the tree.</span><span class="sxs-lookup"><span data-stu-id="5a98f-173">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="5a98f-174">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span><span class="sxs-lookup"><span data-stu-id="5a98f-174">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="5a98f-175">Set the value to your application's unique scheme.</span><span class="sxs-lookup"><span data-stu-id="5a98f-175">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="5a98f-176">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span><span class="sxs-lookup"><span data-stu-id="5a98f-176">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="5a98f-177">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="5a98f-177">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="5a98f-178">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span><span class="sxs-lookup"><span data-stu-id="5a98f-178">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="5a98f-179">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="5a98f-179">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="5a98f-180">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span><span class="sxs-lookup"><span data-stu-id="5a98f-180">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="5a98f-181">We are always open to feedback and suggestions!</span><span class="sxs-lookup"><span data-stu-id="5a98f-181">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="5a98f-182">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5a98f-182">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="5a98f-183">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="5a98f-183">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
