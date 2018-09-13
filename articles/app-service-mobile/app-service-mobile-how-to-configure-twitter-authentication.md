---
title: How to configure Twitter authentication for your App Services application
description: Learn how to configure Twitter authentication for your App Services application.
services: app-service
documentationcenter: ''
author: mattchenderson
manager: adrianha
editor: ''
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: a12b8390faa19e01ec7a55e29b5a84c7f3fd4383
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550628"
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="89171-103">How to configure your App Service application to use Twitter login</span><span class="sxs-lookup"><span data-stu-id="89171-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="89171-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span><span class="sxs-lookup"><span data-stu-id="89171-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="89171-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span><span class="sxs-lookup"><span data-stu-id="89171-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="89171-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="89171-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="89171-107"><a name="register"> </a>Register your application with Twitter</span><span class="sxs-lookup"><span data-stu-id="89171-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="89171-108">Log on to the [Azure portal], and navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="89171-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="89171-109">Copy your **URL**.</span><span class="sxs-lookup"><span data-stu-id="89171-109">Copy your **URL**.</span></span> <span data-ttu-id="89171-110">You will use this to configure your Twitter app.</span><span class="sxs-lookup"><span data-stu-id="89171-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="89171-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="89171-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="89171-112">Type in the **Name** and a **Description** for your new app.</span><span class="sxs-lookup"><span data-stu-id="89171-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="89171-113">Paste in your application's **URL** for the **Website** value.</span><span class="sxs-lookup"><span data-stu-id="89171-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="89171-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="89171-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="89171-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="89171-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="89171-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="89171-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="89171-117">Make sure that you are using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="89171-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="89171-118">At the bottom the page, read and accept the terms.</span><span class="sxs-lookup"><span data-stu-id="89171-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="89171-119">Then click **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="89171-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="89171-120">This registers the app displays the application details.</span><span class="sxs-lookup"><span data-stu-id="89171-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="89171-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span><span class="sxs-lookup"><span data-stu-id="89171-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="89171-122">Select the **Keys and Access Tokens** tab. Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span><span class="sxs-lookup"><span data-stu-id="89171-122">Select the **Keys and Access Tokens** tab. Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="89171-123">The consumer secret is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="89171-123">The consumer secret is an important security credential.</span></span> <span data-ttu-id="89171-124">Do not share this secret with anyone or distribute it with your app.</span><span class="sxs-lookup"><span data-stu-id="89171-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="89171-125"><a name="secrets"> </a>Add Twitter information to your application</span><span class="sxs-lookup"><span data-stu-id="89171-125"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="89171-126">Back in the [Azure portal], navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="89171-126">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="89171-127">Click **Settings**, and then **Authentication / Authorization**.</span><span class="sxs-lookup"><span data-stu-id="89171-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="89171-128">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span><span class="sxs-lookup"><span data-stu-id="89171-128">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="89171-129">Click **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="89171-129">Click **Twitter**.</span></span> <span data-ttu-id="89171-130">Paste in the App ID and App Secret values which you obtained previously.</span><span class="sxs-lookup"><span data-stu-id="89171-130">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="89171-131">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="89171-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="89171-132">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span><span class="sxs-lookup"><span data-stu-id="89171-132">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="89171-133">You must authorize users in your app code.</span><span class="sxs-lookup"><span data-stu-id="89171-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="89171-134">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="89171-134">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="89171-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span><span class="sxs-lookup"><span data-stu-id="89171-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="89171-136">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="89171-136">Click **Save**.</span></span>

<span data-ttu-id="89171-137">You are now ready to use Twitter for authentication in your app.</span><span class="sxs-lookup"><span data-stu-id="89171-137">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="89171-138"><a name="related-content"> </a>Related Content</span><span class="sxs-lookup"><span data-stu-id="89171-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure portal]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md

