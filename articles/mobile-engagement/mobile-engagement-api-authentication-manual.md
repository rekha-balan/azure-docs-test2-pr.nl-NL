---
title: Authenticate with Mobile Engagement REST APIs - manual setup
description: Describes how to manually setup authentication for Mobile Engagement REST APIs
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d1b929193c1820f48d61c2f04e626fc5f5c0679d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552517"
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="9fefe-103">Authenticate with Mobile Engagement REST APIs - manual setup</span><span class="sxs-lookup"><span data-stu-id="9fefe-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="9fefe-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9fefe-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="9fefe-105">Make sure you read it first to get the context.</span><span class="sxs-lookup"><span data-stu-id="9fefe-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="9fefe-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9fefe-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="9fefe-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span><span class="sxs-lookup"><span data-stu-id="9fefe-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="9fefe-108">So refer to it if you want to understand the steps below in detail.</span><span class="sxs-lookup"><span data-stu-id="9fefe-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="9fefe-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="9fefe-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="9fefe-110">Select **Active Directory** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="9fefe-110">Select **Active Directory** from the left pane.</span></span>
   
     ![select Active Directory][1]
3. <span data-ttu-id="9fefe-112">Choose the **Default Active Directory** in your Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9fefe-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![choose directory][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="9fefe-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span><span class="sxs-lookup"><span data-stu-id="9fefe-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="9fefe-115">To view the applications in your directory, click on **Applications**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![view applications][3]
5. <span data-ttu-id="9fefe-117">Click on **ADD**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-117">Click on **ADD**.</span></span> 
   
     ![add application][4]
6. <span data-ttu-id="9fefe-119">Click on **Add an application my organization is developing**</span><span class="sxs-lookup"><span data-stu-id="9fefe-119">Click on **Add an application my organization is developing**</span></span>
   
     ![new application][5]
7. <span data-ttu-id="9fefe-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span><span class="sxs-lookup"><span data-stu-id="9fefe-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![name application][6]
8. <span data-ttu-id="9fefe-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="9fefe-124">They are not used for our scenario and the URLs themselves are not validated.</span><span class="sxs-lookup"><span data-stu-id="9fefe-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![application properties][7]
9. <span data-ttu-id="9fefe-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span><span class="sxs-lookup"><span data-stu-id="9fefe-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="9fefe-127">This is your **AD\_APP\_NAME** and make a note of it.</span><span class="sxs-lookup"><span data-stu-id="9fefe-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![app name][8]
10. <span data-ttu-id="9fefe-129">Click on the app name and click on **Configure**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-129">Click on the app name and click on **Configure**.</span></span>
    
      ![configure app][9]
11. <span data-ttu-id="9fefe-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span><span class="sxs-lookup"><span data-stu-id="9fefe-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configure app][10]
12. <span data-ttu-id="9fefe-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configure app][11]
13. <span data-ttu-id="9fefe-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span><span class="sxs-lookup"><span data-stu-id="9fefe-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="9fefe-136">If you lose it then you will have to generate a new key.</span><span class="sxs-lookup"><span data-stu-id="9fefe-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="9fefe-137">This will be the **CLIENT_SECRET** for your API calls.</span><span class="sxs-lookup"><span data-stu-id="9fefe-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configure app][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="9fefe-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span><span class="sxs-lookup"><span data-stu-id="9fefe-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="9fefe-140">You can also delete and recreate this key if you think that it has been compromised.</span><span class="sxs-lookup"><span data-stu-id="9fefe-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="9fefe-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9fefe-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="9fefe-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="9fefe-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span><span class="sxs-lookup"><span data-stu-id="9fefe-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="9fefe-144">Now we will proceed to configure the permissions on this app.</span><span class="sxs-lookup"><span data-stu-id="9fefe-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="9fefe-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9fefe-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="9fefe-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span><span class="sxs-lookup"><span data-stu-id="9fefe-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="9fefe-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span><span class="sxs-lookup"><span data-stu-id="9fefe-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="9fefe-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span><span class="sxs-lookup"><span data-stu-id="9fefe-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="9fefe-149">Click on **Select a role**</span><span class="sxs-lookup"><span data-stu-id="9fefe-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="9fefe-150">Click on **Owner**</span><span class="sxs-lookup"><span data-stu-id="9fefe-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="9fefe-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span><span class="sxs-lookup"><span data-stu-id="9fefe-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="9fefe-152">You will not see this by default here.</span><span class="sxs-lookup"><span data-stu-id="9fefe-152">You will not see this by default here.</span></span> <span data-ttu-id="9fefe-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="9fefe-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="9fefe-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span><span class="sxs-lookup"><span data-stu-id="9fefe-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="9fefe-155">Click **OK** on this blade to confirm the change.</span><span class="sxs-lookup"><span data-stu-id="9fefe-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="9fefe-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span><span class="sxs-lookup"><span data-stu-id="9fefe-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/client-id.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/keys.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/add-users.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/add-role.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/select-role.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication-manual/add-access-final.png
























