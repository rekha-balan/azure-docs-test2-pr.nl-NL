---
title: How to configure Google authentication for your App Services application
description: Learn how to configure Google authentication for your App Services application.
services: app-service
documentationcenter: ''
author: mattchenderson
manager: syntaxc4
editor: ''
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/19/2018
ms.author: mahender
ms.openlocfilehash: f89ff3a030f1da75bca538eefaf2496e9be8e97b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857728"
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="14d8c-103">How to configure your App Service application to use Google login</span><span class="sxs-lookup"><span data-stu-id="14d8c-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="14d8c-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span><span class="sxs-lookup"><span data-stu-id="14d8c-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="14d8c-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span><span class="sxs-lookup"><span data-stu-id="14d8c-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="14d8c-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="14d8c-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="14d8c-107"><a name="register"> </a>Register your application with Google</span><span class="sxs-lookup"><span data-stu-id="14d8c-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="14d8c-108">Log on to the [Azure portal], and navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="14d8c-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="14d8c-109">Copy your **URL**, which you use later to configure your Google app.</span><span class="sxs-lookup"><span data-stu-id="14d8c-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="14d8c-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="14d8c-111">Once the project is created, select it.</span><span class="sxs-lookup"><span data-stu-id="14d8c-111">Once the project is created, select it.</span></span> <span data-ttu-id="14d8c-112">From the project dashboard, click **Go to APIs overview**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-112">From the project dashboard, click **Go to APIs overview**.</span></span>
4. <span data-ttu-id="14d8c-113">Select **Enable APIs and services**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-113">Select **Enable APIs and services**.</span></span> <span data-ttu-id="14d8c-114">Search for **Google+ API**, and select it.</span><span class="sxs-lookup"><span data-stu-id="14d8c-114">Search for **Google+ API**, and select it.</span></span> <span data-ttu-id="14d8c-115">Then click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-115">Then click **Enable**.</span></span>
5. <span data-ttu-id="14d8c-116">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-116">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
6. <span data-ttu-id="14d8c-117">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-117">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**.</span></span>
7. <span data-ttu-id="14d8c-118">On the "Create client ID" screen, select **Web application**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-118">On the "Create client ID" screen, select **Web application**.</span></span>
8. <span data-ttu-id="14d8c-119">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-119">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="14d8c-120">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="14d8c-120">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="14d8c-121">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="14d8c-121">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="14d8c-122">Make sure that you are using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="14d8c-122">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="14d8c-123">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-123">Then click **Create**.</span></span>
9. <span data-ttu-id="14d8c-124">On the next screen, make a note of the values of the client ID and client secret.</span><span class="sxs-lookup"><span data-stu-id="14d8c-124">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="14d8c-125">The client secret is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="14d8c-125">The client secret is an important security credential.</span></span> <span data-ttu-id="14d8c-126">Do not share this secret with anyone or distribute it within a client application.</span><span class="sxs-lookup"><span data-stu-id="14d8c-126">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="14d8c-127"><a name="secrets"> </a>Add Google information to your application</span><span class="sxs-lookup"><span data-stu-id="14d8c-127"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="14d8c-128">Back in the [Azure portal], navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="14d8c-128">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="14d8c-129">Click **Settings**, and then **Authentication / Authorization**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-129">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="14d8c-130">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-130">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="14d8c-131">Click **Google**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-131">Click **Google**.</span></span> <span data-ttu-id="14d8c-132">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span><span class="sxs-lookup"><span data-stu-id="14d8c-132">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="14d8c-133">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-133">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="14d8c-134">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span><span class="sxs-lookup"><span data-stu-id="14d8c-134">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="14d8c-135">You must authorize users in your app code.</span><span class="sxs-lookup"><span data-stu-id="14d8c-135">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="14d8c-136">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-136">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="14d8c-137">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span><span class="sxs-lookup"><span data-stu-id="14d8c-137">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="14d8c-138">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14d8c-138">Click **Save**.</span></span>

<span data-ttu-id="14d8c-139">You are now ready to use Google for authentication in your app.</span><span class="sxs-lookup"><span data-stu-id="14d8c-139">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="14d8c-140"><a name="related-content"> </a>Related Content</span><span class="sxs-lookup"><span data-stu-id="14d8c-140"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure portal]: https://portal.azure.com/

