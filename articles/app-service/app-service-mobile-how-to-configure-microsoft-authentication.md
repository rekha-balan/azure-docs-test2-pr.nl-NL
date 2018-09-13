---
title: How to configure Microsoft Account authentication for your App Services application
description: Learn how to configure Microsoft Account authentication for your App Services application.
author: mattchenderson
services: app-service
documentationcenter: ''
manager: syntaxc4
editor: ''
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/19/2018
ms.author: mahender
ms.openlocfilehash: 4fb5bdf30502dbca3eba961165a1ab643427abd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866022"
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="2dcda-103">How to configure your App Service application to use Microsoft Account login</span><span class="sxs-lookup"><span data-stu-id="2dcda-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="2dcda-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span><span class="sxs-lookup"><span data-stu-id="2dcda-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="2dcda-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span><span class="sxs-lookup"><span data-stu-id="2dcda-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="2dcda-106">Log on to the [Azure portal], and navigate to your application.</span><span class="sxs-lookup"><span data-stu-id="2dcda-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="2dcda-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span><span class="sxs-lookup"><span data-stu-id="2dcda-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="2dcda-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span><span class="sxs-lookup"><span data-stu-id="2dcda-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="2dcda-109">Click **Add an app**, then type an application name, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-109">Click **Add an app**, then type an application name, and click **Create**.</span></span>
4. <span data-ttu-id="2dcda-110">Make a note of the **Application ID**, as you will need it later.</span><span class="sxs-lookup"><span data-stu-id="2dcda-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="2dcda-111">Under "Platforms," click **Add Platform** and select "Web".</span><span class="sxs-lookup"><span data-stu-id="2dcda-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="2dcda-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2dcda-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="2dcda-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="2dcda-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="2dcda-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="2dcda-115">Make sure that you are using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="2dcda-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="2dcda-116">Under "Application Secrets," click **Generate New Password**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="2dcda-117">Make note of the value that appears.</span><span class="sxs-lookup"><span data-stu-id="2dcda-117">Make note of the value that appears.</span></span> <span data-ttu-id="2dcda-118">Once you leave the page, it will not be displayed again.</span><span class="sxs-lookup"><span data-stu-id="2dcda-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2dcda-119">The password is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="2dcda-119">The password is an important security credential.</span></span> <span data-ttu-id="2dcda-120">Do not share the password with anyone or distribute it within a client application.</span><span class="sxs-lookup"><span data-stu-id="2dcda-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="2dcda-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span><span class="sxs-lookup"><span data-stu-id="2dcda-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="2dcda-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="2dcda-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="2dcda-124">Click **Microsoft Account**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="2dcda-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span><span class="sxs-lookup"><span data-stu-id="2dcda-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="2dcda-126">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="2dcda-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span><span class="sxs-lookup"><span data-stu-id="2dcda-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="2dcda-128">You must authorize users in your app code.</span><span class="sxs-lookup"><span data-stu-id="2dcda-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="2dcda-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="2dcda-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span><span class="sxs-lookup"><span data-stu-id="2dcda-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="2dcda-131">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2dcda-131">Click **Save**.</span></span>

<span data-ttu-id="2dcda-132">You are now ready to use Microsoft Account for authentication in your app.</span><span class="sxs-lookup"><span data-stu-id="2dcda-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="2dcda-133"><a name="related-content"> </a>Related content</span><span class="sxs-lookup"><span data-stu-id="2dcda-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure portal]: https://portal.azure.com/
