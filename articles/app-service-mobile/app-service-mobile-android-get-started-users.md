---
title: Add authentication on Android with Mobile Apps | Microsoft Docs
description: Learn how to use the Mobile Apps feature of Azure App Service to authenticate users of your Android app through a variety of identity providers, including Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: android
author: ysxu
manager: ''
editor: ''
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fcaab18c2c22bcbdbb42708da9840fb6e5c25b2e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553548"
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="b10e1-103">Add authentication to your Android app</span><span class="sxs-lookup"><span data-stu-id="b10e1-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="b10e1-104">Summary</span><span class="sxs-lookup"><span data-stu-id="b10e1-104">Summary</span></span>
<span data-ttu-id="b10e1-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span><span class="sxs-lookup"><span data-stu-id="b10e1-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="b10e1-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span><span class="sxs-lookup"><span data-stu-id="b10e1-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <a name="register"></a><span data-ttu-id="b10e1-107">Register your app for authentication and configure Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b10e1-107">Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a><span data-ttu-id="b10e1-108">Add your app to the Allowed External Redirect URLs</span><span class="sxs-lookup"><span data-stu-id="b10e1-108">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="b10e1-109">Secure authentication requires that you define a new URL scheme for your app.</span><span class="sxs-lookup"><span data-stu-id="b10e1-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="b10e1-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span><span class="sxs-lookup"><span data-stu-id="b10e1-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="b10e1-111">In this tutorial, we use the URL scheme _appname_ throughout.</span><span class="sxs-lookup"><span data-stu-id="b10e1-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="b10e1-112">However, you can use any URL scheme you choose.</span><span class="sxs-lookup"><span data-stu-id="b10e1-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="b10e1-113">It should be unique to your mobile application.</span><span class="sxs-lookup"><span data-stu-id="b10e1-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="b10e1-114">To enable the redirection on the server side:</span><span class="sxs-lookup"><span data-stu-id="b10e1-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="b10e1-115">In the [Azure portal], select your App Service.</span><span class="sxs-lookup"><span data-stu-id="b10e1-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="b10e1-116">Click the **Authentication / Authorization** menu option.</span><span class="sxs-lookup"><span data-stu-id="b10e1-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="b10e1-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="b10e1-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="b10e1-118">The _appname_ in this string is the URL Scheme for your mobile application.</span><span class="sxs-lookup"><span data-stu-id="b10e1-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="b10e1-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span><span class="sxs-lookup"><span data-stu-id="b10e1-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="b10e1-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span><span class="sxs-lookup"><span data-stu-id="b10e1-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="b10e1-121">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b10e1-121">Click **OK**.</span></span>

5. <span data-ttu-id="b10e1-122">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b10e1-122">Click **Save**.</span></span>

## <a name="permissions"></a><span data-ttu-id="b10e1-123">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="b10e1-123">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="b10e1-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b10e1-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="b10e1-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="b10e1-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="b10e1-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="b10e1-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="b10e1-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span><span class="sxs-lookup"><span data-stu-id="b10e1-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="b10e1-128">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="b10e1-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a><span data-ttu-id="b10e1-129">Cache authentication tokens on the client</span><span class="sxs-lookup"><span data-stu-id="b10e1-129">Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="b10e1-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="b10e1-130">Next steps</span></span>
<span data-ttu-id="b10e1-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="b10e1-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="b10e1-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="b10e1-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="b10e1-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="b10e1-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="b10e1-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="b10e1-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="b10e1-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span><span class="sxs-lookup"><span data-stu-id="b10e1-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="b10e1-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="b10e1-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Get started with Mobile Apps]: app-service-mobile-android-get-started.md
