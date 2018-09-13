---
title: How to configure Google authentication for your App Services application
description: Learn how to configure Google authentication for your App Services application.
services: app-service
documentationcenter: ''
author: mattchenderson
manager: adrianha
editor: ''
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: fc668e53bb85285fceb872492a9334b82f6b9631
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563152"
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="d3fbc-103">How to configure your App Service application to use Google login</span><span class="sxs-lookup"><span data-stu-id="d3fbc-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="d3fbc-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="d3fbc-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="d3fbc-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="d3fbc-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="d3fbc-107"><a name="register"> </a>Register your application with Google</span><span class="sxs-lookup"><span data-stu-id="d3fbc-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="d3fbc-108">Log on to the [Azure portal], and navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="d3fbc-109">Copy your **URL**, which you use later to configure your Google app.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="d3fbc-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="d3fbc-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="d3fbc-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="d3fbc-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="d3fbc-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="d3fbc-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="d3fbc-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="d3fbc-117">Make sure that you are using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="d3fbc-118">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-118">Then click **Create**.</span></span>
7. <span data-ttu-id="d3fbc-119">On the next screen, make a note of the values of the client ID and client secret.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [AZURE.IMPORTANT]
    <span data-ttu-id="d3fbc-120">The client secret is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-120">The client secret is an important security credential.</span></span> <span data-ttu-id="d3fbc-121">Do not share this secret with anyone or distribute it within a client application.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="d3fbc-122"><a name="secrets"> </a>Add Google information to your application</span><span class="sxs-lookup"><span data-stu-id="d3fbc-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="d3fbc-123">Back in the [Azure portal], navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="d3fbc-124">Click **Settings**, and then **Authentication / Authorization**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="d3fbc-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="d3fbc-126">Click **Google**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-126">Click **Google**.</span></span> <span data-ttu-id="d3fbc-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="d3fbc-128">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="d3fbc-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="d3fbc-130">You must authorize users in your app code.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="d3fbc-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="d3fbc-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="d3fbc-133">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-133">Click **Save**.</span></span>

<span data-ttu-id="d3fbc-134">You are now ready to use Google for authentication in your app.</span><span class="sxs-lookup"><span data-stu-id="d3fbc-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="d3fbc-135"><a name="related-content"> </a>Related Content</span><span class="sxs-lookup"><span data-stu-id="d3fbc-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure portal]: https://portal.azure.com/


