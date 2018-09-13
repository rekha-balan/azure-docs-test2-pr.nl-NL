---
title: Authentication and Authorization in Azure Mobile Apps | Microsoft Docs
description: Conceptual reference and overview of the Authentication / Authorization feature for Azure Mobile Apps
services: app-service\mobile
documentationcenter: ''
author: mattchenderson
manager: adrianha
editor: ''
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 94501117166e2a9614674ddb6b76b4265d63624c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556533"
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a><span data-ttu-id="2ec2c-103">Authentication and Authorization in Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="2ec2c-103">Authentication and Authorization in Azure Mobile Apps</span></span>
## <a name="what-is-app-service-authentication--authorization"></a><span data-ttu-id="2ec2c-104">What is App Service Authentication / Authorization?</span><span class="sxs-lookup"><span data-stu-id="2ec2c-104">What is App Service Authentication / Authorization?</span></span>
> [!NOTE]
> <span data-ttu-id="2ec2c-105">This topic will be migrated to a consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-105">This topic will be migrated to a consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="2ec2c-106">App Service Authentication / Authorization is a feature which allows your application to log in users with no code changes required on the app backend.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-106">App Service Authentication / Authorization is a feature which allows your application to log in users with no code changes required on the app backend.</span></span> <span data-ttu-id="2ec2c-107">It provides an easy way to protect your application and work with per-user data.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-107">It provides an easy way to protect your application and work with per-user data.</span></span>

<span data-ttu-id="2ec2c-108">App Service uses federated identity, in which a 3rd-party **identity provider** ("IDP") stores accounts and authenticates users, and the application uses this identity instead of its own.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-108">App Service uses federated identity, in which a 3rd-party **identity provider** ("IDP") stores accounts and authenticates users, and the application uses this identity instead of its own.</span></span> <span data-ttu-id="2ec2c-109">App Service supports five identity providers out of the box: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, and *Twitter*.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-109">App Service supports five identity providers out of the box: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, and *Twitter*.</span></span> <span data-ttu-id="2ec2c-110">You can also expand this support for your apps by integrating another identity provider or your own custom identity solution.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-110">You can also expand this support for your apps by integrating another identity provider or your own custom identity solution.</span></span>

<span data-ttu-id="2ec2c-111">Your app can leverage any number of these identity providers, so you can provide your end users with options for how they login.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-111">Your app can leverage any number of these identity providers, so you can provide your end users with options for how they login.</span></span>

<span data-ttu-id="2ec2c-112">If you wish to get started right away, please see one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="2ec2c-112">If you wish to get started right away, please see one of the following tutorials:</span></span>

* <span data-ttu-id="2ec2c-113">[Add authentication to your iOS app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-113">[Add authentication to your iOS app]</span></span>
* <span data-ttu-id="2ec2c-114">[Add authentication to your Xamarin.iOS app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-114">[Add authentication to your Xamarin.iOS app]</span></span>
* <span data-ttu-id="2ec2c-115">[Add authentication to your Xamarin.Android app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-115">[Add authentication to your Xamarin.Android app]</span></span>
* <span data-ttu-id="2ec2c-116">[Add Authentication to your Windows app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-116">[Add Authentication to your Windows app]</span></span>

## <a name="how-authentication-works"></a><span data-ttu-id="2ec2c-117">How authentication works</span><span class="sxs-lookup"><span data-stu-id="2ec2c-117">How authentication works</span></span>
<span data-ttu-id="2ec2c-118">In order to authenticate using one of the identity providers, you first need to configure the identity provider to know about your application.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-118">In order to authenticate using one of the identity providers, you first need to configure the identity provider to know about your application.</span></span> <span data-ttu-id="2ec2c-119">The identity provider will then provide you with IDs and secrets that you provide back to the application.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-119">The identity provider will then provide you with IDs and secrets that you provide back to the application.</span></span> <span data-ttu-id="2ec2c-120">This completes the trust relationship and allows App Service to validate identities provided to it.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-120">This completes the trust relationship and allows App Service to validate identities provided to it.</span></span>

<span data-ttu-id="2ec2c-121">These steps are detailed in the following topics:</span><span class="sxs-lookup"><span data-stu-id="2ec2c-121">These steps are detailed in the following topics:</span></span>

* <span data-ttu-id="2ec2c-122">[How to configure your app to use Azure Active Directory login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-122">[How to configure your app to use Azure Active Directory login]</span></span>
* <span data-ttu-id="2ec2c-123">[How to configure your app to use Facebook login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-123">[How to configure your app to use Facebook login]</span></span>
* <span data-ttu-id="2ec2c-124">[How to configure your app to use Google login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-124">[How to configure your app to use Google login]</span></span>
* <span data-ttu-id="2ec2c-125">[How to configure your app to use Microsoft Account login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-125">[How to configure your app to use Microsoft Account login]</span></span>
* <span data-ttu-id="2ec2c-126">[How to configure your app to use Twitter login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-126">[How to configure your app to use Twitter login]</span></span>

<span data-ttu-id="2ec2c-127">Once everything is configured on the backend, you can modify your client to log in.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-127">Once everything is configured on the backend, you can modify your client to log in.</span></span> <span data-ttu-id="2ec2c-128">There are two approaches here:</span><span class="sxs-lookup"><span data-stu-id="2ec2c-128">There are two approaches here:</span></span>

* <span data-ttu-id="2ec2c-129">Using a single line of code, let the Mobile Apps client SDK sign in users.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-129">Using a single line of code, let the Mobile Apps client SDK sign in users.</span></span>
* <span data-ttu-id="2ec2c-130">Leverage an SDK published by a given identity provider to establish identity and then gain access to App Service.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-130">Leverage an SDK published by a given identity provider to establish identity and then gain access to App Service.</span></span>

> [!TIP]
> <span data-ttu-id="2ec2c-131">Most applications should use a provider SDK to get a more native-feeling login experience and to leverage refresh support and other provider-specific benefits.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-131">Most applications should use a provider SDK to get a more native-feeling login experience and to leverage refresh support and other provider-specific benefits.</span></span>
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a><span data-ttu-id="2ec2c-132">How authentication without a provider SDK works</span><span class="sxs-lookup"><span data-stu-id="2ec2c-132">How authentication without a provider SDK works</span></span>
<span data-ttu-id="2ec2c-133">If you do not wish to set up a provider SDK, you can allow Mobile Apps to perform the login for you.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-133">If you do not wish to set up a provider SDK, you can allow Mobile Apps to perform the login for you.</span></span> <span data-ttu-id="2ec2c-134">The Mobile Apps client SDK will open a web view to the provider of your choosing and complete the sign in.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-134">The Mobile Apps client SDK will open a web view to the provider of your choosing and complete the sign in.</span></span> <span data-ttu-id="2ec2c-135">Occasionally on blogs and forums you will see this referred to as the "server flow" or "server-directed flow" since the server is managing the login, and the client SDK never receives the provider token.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-135">Occasionally on blogs and forums you will see this referred to as the "server flow" or "server-directed flow" since the server is managing the login, and the client SDK never receives the provider token.</span></span>

<span data-ttu-id="2ec2c-136">The code needed to start this flow is covered in the authentication tutorial for each platform.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-136">The code needed to start this flow is covered in the authentication tutorial for each platform.</span></span> <span data-ttu-id="2ec2c-137">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-137">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span></span>

### <a name="how-authentication-with-a-provider-sdk-works"></a><span data-ttu-id="2ec2c-138">How authentication with a provider SDK works</span><span class="sxs-lookup"><span data-stu-id="2ec2c-138">How authentication with a provider SDK works</span></span>
<span data-ttu-id="2ec2c-139">Working with a provider SDK allows the log-in experience to interact more tightly with the platform OS the app is running on.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-139">Working with a provider SDK allows the log-in experience to interact more tightly with the platform OS the app is running on.</span></span> <span data-ttu-id="2ec2c-140">This also gives you a provider token and some user information on the client, which makes it much easier to consume graph APIs and customize the user experience.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-140">This also gives you a provider token and some user information on the client, which makes it much easier to consume graph APIs and customize the user experience.</span></span> <span data-ttu-id="2ec2c-141">Occasionally on blogs and forums you will see this referred to as the "client flow" or "client-directed flow" since code on the client is handling the login, and the client code has access to a provider token.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-141">Occasionally on blogs and forums you will see this referred to as the "client flow" or "client-directed flow" since code on the client is handling the login, and the client code has access to a provider token.</span></span>

<span data-ttu-id="2ec2c-142">Once a provider token is obtained, it needs to be sent to App Service for validation.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-142">Once a provider token is obtained, it needs to be sent to App Service for validation.</span></span> <span data-ttu-id="2ec2c-143">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-143">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span></span> <span data-ttu-id="2ec2c-144">The developer can also keep a reference to the provider token if they so choose.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-144">The developer can also keep a reference to the provider token if they so choose.</span></span>

## <a name="how-authorization-works"></a><span data-ttu-id="2ec2c-145">How authorization works</span><span class="sxs-lookup"><span data-stu-id="2ec2c-145">How authorization works</span></span>
<span data-ttu-id="2ec2c-146">App Service Authentication / Authorization exposes several choices for **Action to take when request is not authenticated**.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-146">App Service Authentication / Authorization exposes several choices for **Action to take when request is not authenticated**.</span></span> <span data-ttu-id="2ec2c-147">Before your code receives a given request, you can have App Service check to see if the request is authenticated and if not, reject it and attempt to have the user log in before trying again.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-147">Before your code receives a given request, you can have App Service check to see if the request is authenticated and if not, reject it and attempt to have the user log in before trying again.</span></span>

<span data-ttu-id="2ec2c-148">One option is to have unauthenticated requests redirect to one of the identity providers.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-148">One option is to have unauthenticated requests redirect to one of the identity providers.</span></span> <span data-ttu-id="2ec2c-149">In a web browser, this would actually take the user to a new page.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-149">In a web browser, this would actually take the user to a new page.</span></span> <span data-ttu-id="2ec2c-150">However, your mobile client cannot be redirected in this way, and unauthenticated responses will receive an HTTP *401 Unauthorized* response.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-150">However, your mobile client cannot be redirected in this way, and unauthenticated responses will receive an HTTP *401 Unauthorized* response.</span></span> <span data-ttu-id="2ec2c-151">Given this, the first request your client makes should always be to the login endpoint, and then you can make calls to any other APIs.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-151">Given this, the first request your client makes should always be to the login endpoint, and then you can make calls to any other APIs.</span></span> <span data-ttu-id="2ec2c-152">If you attempt to call another API before logging in, your client will receive an error.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-152">If you attempt to call another API before logging in, your client will receive an error.</span></span>

<span data-ttu-id="2ec2c-153">If you wish to have more granular control over which endpoints require authentication, you can also pick "No action (allow request)" for unauthenticated requests.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-153">If you wish to have more granular control over which endpoints require authentication, you can also pick "No action (allow request)" for unauthenticated requests.</span></span> <span data-ttu-id="2ec2c-154">In this case, all authentication decisions are deferred to your application code.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-154">In this case, all authentication decisions are deferred to your application code.</span></span> <span data-ttu-id="2ec2c-155">This also allows you to allow access to specific users based on custom authorization rules.</span><span class="sxs-lookup"><span data-stu-id="2ec2c-155">This also allows you to allow access to specific users based on custom authorization rules.</span></span>

## <a name="documentation"></a><span data-ttu-id="2ec2c-156">Documentation</span><span class="sxs-lookup"><span data-stu-id="2ec2c-156">Documentation</span></span>
<span data-ttu-id="2ec2c-157">The following tutorials show how to add authentication to your mobile clients using App Service:</span><span class="sxs-lookup"><span data-stu-id="2ec2c-157">The following tutorials show how to add authentication to your mobile clients using App Service:</span></span>

* <span data-ttu-id="2ec2c-158">[Add authentication to your iOS app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-158">[Add authentication to your iOS app]</span></span>
* <span data-ttu-id="2ec2c-159">[Add authentication to your Xamarin.iOS app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-159">[Add authentication to your Xamarin.iOS app]</span></span>
* <span data-ttu-id="2ec2c-160">[Add authentication to your Xamarin.Android app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-160">[Add authentication to your Xamarin.Android app]</span></span>
* <span data-ttu-id="2ec2c-161">[Add Authentication to your Windows app]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-161">[Add Authentication to your Windows app]</span></span>

<span data-ttu-id="2ec2c-162">The following tutorials show how to configure App Service to leverage different authentication providers:</span><span class="sxs-lookup"><span data-stu-id="2ec2c-162">The following tutorials show how to configure App Service to leverage different authentication providers:</span></span>

* <span data-ttu-id="2ec2c-163">[How to configure your app to use Azure Active Directory login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-163">[How to configure your app to use Azure Active Directory login]</span></span>
* <span data-ttu-id="2ec2c-164">[How to configure your app to use Facebook login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-164">[How to configure your app to use Facebook login]</span></span>
* <span data-ttu-id="2ec2c-165">[How to configure your app to use Google login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-165">[How to configure your app to use Google login]</span></span>
* <span data-ttu-id="2ec2c-166">[How to configure your app to use Microsoft Account login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-166">[How to configure your app to use Microsoft Account login]</span></span>
* <span data-ttu-id="2ec2c-167">[How to configure your app to use Twitter login]</span><span class="sxs-lookup"><span data-stu-id="2ec2c-167">[How to configure your app to use Twitter login]</span></span>

<span data-ttu-id="2ec2c-168">If you wish to use an identity system other than the ones provided here, you can also leverage the [preview custom authentication support in the .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).</span><span class="sxs-lookup"><span data-stu-id="2ec2c-168">If you wish to use an identity system other than the ones provided here, you can also leverage the [preview custom authentication support in the .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).</span></span>

[Add authentication to your iOS app]: app-service-mobile-ios-get-started-users.md
[Add authentication to your Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started-users.md
[Add authentication to your Xamarin.Android app]: app-service-mobile-xamarin-android-get-started-users.md
[Add Authentication to your Windows app]: app-service-mobile-windows-store-dotnet-get-started-users.md

[How to configure your app to use Azure Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md
[How to configure your app to use Facebook login]: app-service-mobile-how-to-configure-facebook-authentication.md
[How to configure your app to use Google login]: app-service-mobile-how-to-configure-google-authentication.md
[How to configure your app to use Microsoft Account login]: app-service-mobile-how-to-configure-microsoft-authentication.md
[How to configure your app to use Twitter login]: app-service-mobile-how-to-configure-twitter-authentication.md
