---
title: How to configure Facebook authentication for your App Services application
description: Learn how to configure Facebook authentication for your App Services application.
services: app-service
documentationcenter: ''
author: mattchenderson
manager: syntaxc4
editor: ''
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/19/2018
ms.author: mahender
ms.openlocfilehash: 1d2b294fc0663770f9a699e300672695225dfdfd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856684"
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="d13ec-103">How to configure your App Service application to use Facebook login</span><span class="sxs-lookup"><span data-stu-id="d13ec-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="d13ec-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span><span class="sxs-lookup"><span data-stu-id="d13ec-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="d13ec-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span><span class="sxs-lookup"><span data-stu-id="d13ec-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="d13ec-106">To create a new Facebook account, go to [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="d13ec-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="d13ec-107"><a name="register"> </a>Register your application with Facebook</span><span class="sxs-lookup"><span data-stu-id="d13ec-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="d13ec-108">Log on to the [Azure portal], and navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="d13ec-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="d13ec-109">Copy your **URL**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-109">Copy your **URL**.</span></span> <span data-ttu-id="d13ec-110">You will use this to configure your Facebook app.</span><span class="sxs-lookup"><span data-stu-id="d13ec-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="d13ec-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span><span class="sxs-lookup"><span data-stu-id="d13ec-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="d13ec-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span><span class="sxs-lookup"><span data-stu-id="d13ec-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="d13ec-113">Click **My Apps** > **Add a New App**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-113">Click **My Apps** > **Add a New App**.</span></span>
5. <span data-ttu-id="d13ec-114">In **Display Name**, type a unique name for your app.</span><span class="sxs-lookup"><span data-stu-id="d13ec-114">In **Display Name**, type a unique name for your app.</span></span> <span data-ttu-id="d13ec-115">Also provide your **Contact Email**, and then click **Create App ID** and complete the security check.</span><span class="sxs-lookup"><span data-stu-id="d13ec-115">Also provide your **Contact Email**, and then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="d13ec-116">This takes you to the developer dashboard for your new Facebook app.</span><span class="sxs-lookup"><span data-stu-id="d13ec-116">This takes you to the developer dashboard for your new Facebook app.</span></span>
7. <span data-ttu-id="d13ec-117">Under **Facebook Login**, click **Set up**, and then choose **Settings** in the left-hand navigation under **Facebook Login**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-117">Under **Facebook Login**, click **Set up**, and then choose **Settings** in the left-hand navigation under **Facebook Login**.</span></span>
8. <span data-ttu-id="d13ec-118">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-118">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d13ec-119">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="d13ec-119">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="d13ec-120">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="d13ec-120">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="d13ec-121">Make sure that you are using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="d13ec-121">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="d13ec-122">In the left-hand navigation, click **Settings** > **Basic**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-122">In the left-hand navigation, click **Settings** > **Basic**.</span></span> <span data-ttu-id="d13ec-123">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-123">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="d13ec-124">You use these later to configure your application in Azure.</span><span class="sxs-lookup"><span data-stu-id="d13ec-124">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d13ec-125">The app secret is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="d13ec-125">The app secret is an important security credential.</span></span> <span data-ttu-id="d13ec-126">Do not share this secret with anyone or distribute it within a client application.</span><span class="sxs-lookup"><span data-stu-id="d13ec-126">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="d13ec-127">The Facebook account which was used to register the application is an administrator of the app.</span><span class="sxs-lookup"><span data-stu-id="d13ec-127">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="d13ec-128">At this point, only administrators can sign into this application.</span><span class="sxs-lookup"><span data-stu-id="d13ec-128">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="d13ec-129">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span><span class="sxs-lookup"><span data-stu-id="d13ec-129">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="d13ec-130"><a name="secrets"> </a>Add Facebook information to your application</span><span class="sxs-lookup"><span data-stu-id="d13ec-130"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="d13ec-131">Back in the [Azure portal], navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="d13ec-131">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="d13ec-132">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-132">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="d13ec-133">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-133">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="d13ec-134">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span><span class="sxs-lookup"><span data-stu-id="d13ec-134">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="d13ec-135">You must authorize users in your app code.</span><span class="sxs-lookup"><span data-stu-id="d13ec-135">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="d13ec-136">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-136">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="d13ec-137">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span><span class="sxs-lookup"><span data-stu-id="d13ec-137">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="d13ec-138">When done configuring authentication, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d13ec-138">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="d13ec-139">You are now ready to use Facebook for authentication in your app.</span><span class="sxs-lookup"><span data-stu-id="d13ec-139">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="d13ec-140"><a name="related-content"> </a>Related Content</span><span class="sxs-lookup"><span data-stu-id="d13ec-140"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure portal]: https://portal.azure.com/
