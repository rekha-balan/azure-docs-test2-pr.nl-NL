---
title: 'Azure Active Directory B2C: Acquiring a token using an Android application | Microsoft Docs'
description: This article will show you how to create an Android app that uses AppAuth with Azure Active Directory B2C to manage user identities and authenticate users.
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: ''
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: fdf9f494f30f11a00831b6c56a3d6ac40582c0ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662471"
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="7d01c-103">Azure AD B2C: Sign-in using an Android application</span><span class="sxs-lookup"><span data-stu-id="7d01c-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="7d01c-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="7d01c-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="7d01c-105">This allows developers to leverage any library they wish to integrate with our services.</span><span class="sxs-lookup"><span data-stu-id="7d01c-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="7d01c-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="7d01c-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="7d01c-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="7d01c-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="7d01c-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span><span class="sxs-lookup"><span data-stu-id="7d01c-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="7d01c-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7d01c-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="7d01c-110">Issues and feature requests should be directed to the library's open-source project.</span><span class="sxs-lookup"><span data-stu-id="7d01c-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="7d01c-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span><span class="sxs-lookup"><span data-stu-id="7d01c-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="7d01c-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span><span class="sxs-lookup"><span data-stu-id="7d01c-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="7d01c-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7d01c-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

<span data-ttu-id="7d01c-114">Not all Azure Active Directory scenarios & features are supported by the B2C platform.</span><span class="sxs-lookup"><span data-stu-id="7d01c-114">Not all Azure Active Directory scenarios & features are supported by the B2C platform.</span></span>  <span data-ttu-id="7d01c-115">To determine if you should use the B2C platform, read about [B2C limitations](active-directory-b2c-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7d01c-115">To determine if you should use the B2C platform, read about [B2C limitations](active-directory-b2c-limitations.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="7d01c-116">Get an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="7d01c-116">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="7d01c-117">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="7d01c-117">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="7d01c-118">A directory is a container for all of your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="7d01c-118">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="7d01c-119">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span><span class="sxs-lookup"><span data-stu-id="7d01c-119">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="7d01c-120">Create an application</span><span class="sxs-lookup"><span data-stu-id="7d01c-120">Create an application</span></span>

<span data-ttu-id="7d01c-121">Next, you need to create an app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="7d01c-121">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="7d01c-122">This gives Azure AD information that it needs to communicate securely with your app.</span><span class="sxs-lookup"><span data-stu-id="7d01c-122">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="7d01c-123">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7d01c-123">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="7d01c-124">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="7d01c-124">Be sure to:</span></span>

* <span data-ttu-id="7d01c-125">Include a **Native Client** in the application.</span><span class="sxs-lookup"><span data-stu-id="7d01c-125">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="7d01c-126">Copy the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="7d01c-126">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="7d01c-127">You will need this later.</span><span class="sxs-lookup"><span data-stu-id="7d01c-127">You will need this later.</span></span>
* <span data-ttu-id="7d01c-128">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="7d01c-128">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="7d01c-129">You will also need this later.</span><span class="sxs-lookup"><span data-stu-id="7d01c-129">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="7d01c-130">Create your policies</span><span class="sxs-lookup"><span data-stu-id="7d01c-130">Create your policies</span></span>

<span data-ttu-id="7d01c-131">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7d01c-131">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="7d01c-132">This app contains one identity experience: a combined sign-in and sign-up.</span><span class="sxs-lookup"><span data-stu-id="7d01c-132">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="7d01c-133">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="7d01c-133">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="7d01c-134">When you create the policy, be sure to:</span><span class="sxs-lookup"><span data-stu-id="7d01c-134">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="7d01c-135">Choose the **Display name** as a sign-up attribute in your policy.</span><span class="sxs-lookup"><span data-stu-id="7d01c-135">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="7d01c-136">Choose the **Display name** and **Object ID** application claims in every policy.</span><span class="sxs-lookup"><span data-stu-id="7d01c-136">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="7d01c-137">You can choose other claims as well.</span><span class="sxs-lookup"><span data-stu-id="7d01c-137">You can choose other claims as well.</span></span>
* <span data-ttu-id="7d01c-138">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="7d01c-138">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="7d01c-139">It should have the prefix `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="7d01c-139">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="7d01c-140">You'll need the policy name later.</span><span class="sxs-lookup"><span data-stu-id="7d01c-140">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="7d01c-141">After you have created your policies, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="7d01c-141">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="7d01c-142">Download the sample code</span><span class="sxs-lookup"><span data-stu-id="7d01c-142">Download the sample code</span></span>

<span data-ttu-id="7d01c-143">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="7d01c-143">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="7d01c-144">You can download the code and run it.</span><span class="sxs-lookup"><span data-stu-id="7d01c-144">You can download the code and run it.</span></span> <span data-ttu-id="7d01c-145">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="7d01c-145">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="7d01c-146">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="7d01c-146">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="7d01c-147">Please visit their page to learn more about AppAuth and its features.</span><span class="sxs-lookup"><span data-stu-id="7d01c-147">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="7d01c-148">Modifying your app to use Azure AD B2C with AppAuth</span><span class="sxs-lookup"><span data-stu-id="7d01c-148">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="7d01c-149">AppAuth supports Android API 16 (Jellybean) and above.</span><span class="sxs-lookup"><span data-stu-id="7d01c-149">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="7d01c-150">We recommend using API 23 and above.</span><span class="sxs-lookup"><span data-stu-id="7d01c-150">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="7d01c-151">Configuration</span><span class="sxs-lookup"><span data-stu-id="7d01c-151">Configuration</span></span>

<span data-ttu-id="7d01c-152">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span><span class="sxs-lookup"><span data-stu-id="7d01c-152">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="7d01c-153">In either case, you will need the following information:</span><span class="sxs-lookup"><span data-stu-id="7d01c-153">In either case, you will need the following information:</span></span>

* <span data-ttu-id="7d01c-154">Tenant ID (e.g. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="7d01c-154">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="7d01c-155">Policy name (e.g. B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="7d01c-155">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="7d01c-156">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span><span class="sxs-lookup"><span data-stu-id="7d01c-156">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="7d01c-157">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span><span class="sxs-lookup"><span data-stu-id="7d01c-157">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="7d01c-158">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span><span class="sxs-lookup"><span data-stu-id="7d01c-158">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="7d01c-159">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span><span class="sxs-lookup"><span data-stu-id="7d01c-159">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="7d01c-160">Run the following code to create your AuthorizationServiceConfiguration object:</span><span class="sxs-lookup"><span data-stu-id="7d01c-160">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="7d01c-161">Authorizing</span><span class="sxs-lookup"><span data-stu-id="7d01c-161">Authorizing</span></span>

<span data-ttu-id="7d01c-162">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span><span class="sxs-lookup"><span data-stu-id="7d01c-162">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="7d01c-163">To create the request, you will need the following information:</span><span class="sxs-lookup"><span data-stu-id="7d01c-163">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="7d01c-164">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="7d01c-164">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="7d01c-165">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="7d01c-165">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="7d01c-166">Both items should have been saved when you were [registering your app](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="7d01c-166">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="7d01c-167">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span><span class="sxs-lookup"><span data-stu-id="7d01c-167">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="7d01c-168">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="7d01c-168">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="7d01c-169">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span><span class="sxs-lookup"><span data-stu-id="7d01c-169">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="7d01c-170">We are always open to feedback and suggestions!</span><span class="sxs-lookup"><span data-stu-id="7d01c-170">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="7d01c-171">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7d01c-171">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="7d01c-172">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="7d01c-172">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

