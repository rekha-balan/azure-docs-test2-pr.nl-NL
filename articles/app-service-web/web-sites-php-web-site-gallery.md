---
title: Create a WordPress web app in Azure App Service | Microsoft Docs
description: Learn how to create a new Azure web app for a WordPress blog using the Azure Portal.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: hero-article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: b6db0bd4cf584f3c4cc6d6817eb77911dc01e32b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553001"
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="f700c-103">Create a WordPress web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f700c-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="f700c-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f700c-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="f700c-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f700c-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![WordPress site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="f700c-107">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="f700c-107">You'll learn:</span></span>

* <span data-ttu-id="f700c-108">How to find an application template in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f700c-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="f700c-109">How to create a web app in Azure App Service that is based on the template.</span><span class="sxs-lookup"><span data-stu-id="f700c-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="f700c-110">How to configure Azure App Service settings for the new web app and database.</span><span class="sxs-lookup"><span data-stu-id="f700c-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="f700c-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span><span class="sxs-lookup"><span data-stu-id="f700c-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="f700c-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span><span class="sxs-lookup"><span data-stu-id="f700c-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="f700c-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f700c-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="f700c-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span><span class="sxs-lookup"><span data-stu-id="f700c-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="f700c-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="f700c-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="f700c-116">**Project Nami** is also available through the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f700c-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="f700c-117">To complete this tutorial, you need a Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="f700c-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="f700c-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f700c-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="f700c-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f700c-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="f700c-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span><span class="sxs-lookup"><span data-stu-id="f700c-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="f700c-121">Select WordPress and configure for Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f700c-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="f700c-122">Log in to the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f700c-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f700c-123">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="f700c-123">Click **New**.</span></span>
   
    ![Create New][5]
3. <span data-ttu-id="f700c-125">Search for **WordPress**, and then click **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="f700c-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="f700c-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="f700c-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress from list][7]
4. <span data-ttu-id="f700c-128">After reading the description of the WordPress app, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f700c-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="f700c-130">Enter a name for the web app in the **Web app** box.</span><span class="sxs-lookup"><span data-stu-id="f700c-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="f700c-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="f700c-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="f700c-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span><span class="sxs-lookup"><span data-stu-id="f700c-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="f700c-133">If you have more than one subscription, choose the one you want to use.</span><span class="sxs-lookup"><span data-stu-id="f700c-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="f700c-134">Select a **Resource Group** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="f700c-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="f700c-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f700c-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="f700c-136">Select an **App Service plan/Location** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="f700c-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="f700c-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f700c-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="f700c-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span><span class="sxs-lookup"><span data-stu-id="f700c-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="f700c-139">a.</span><span class="sxs-lookup"><span data-stu-id="f700c-139">a.</span></span> <span data-ttu-id="f700c-140">Enter a new name or leave the default name.</span><span class="sxs-lookup"><span data-stu-id="f700c-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="f700c-141">b.</span><span class="sxs-lookup"><span data-stu-id="f700c-141">b.</span></span> <span data-ttu-id="f700c-142">Leave the **Database Type** set to **Shared**.</span><span class="sxs-lookup"><span data-stu-id="f700c-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="f700c-143">c.</span><span class="sxs-lookup"><span data-stu-id="f700c-143">c.</span></span> <span data-ttu-id="f700c-144">Choose the same location as the one you chose for the web app.</span><span class="sxs-lookup"><span data-stu-id="f700c-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="f700c-145">d.</span><span class="sxs-lookup"><span data-stu-id="f700c-145">d.</span></span> <span data-ttu-id="f700c-146">Choose a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="f700c-146">Choose a pricing tier.</span></span> <span data-ttu-id="f700c-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f700c-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="f700c-148">In the **New MySQL Database** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f700c-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="f700c-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f700c-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Configure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="f700c-151">Azure App Service creates the web app, typically in less than a minute.</span><span class="sxs-lookup"><span data-stu-id="f700c-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="f700c-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span><span class="sxs-lookup"><span data-stu-id="f700c-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Progress indicator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="f700c-154">Launch and manage your WordPress web app</span><span class="sxs-lookup"><span data-stu-id="f700c-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="f700c-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span><span class="sxs-lookup"><span data-stu-id="f700c-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="f700c-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span><span class="sxs-lookup"><span data-stu-id="f700c-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="f700c-157">In the **Resource group** blade, click the web app line.</span><span class="sxs-lookup"><span data-stu-id="f700c-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Configure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="f700c-159">In the Web app blade, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="f700c-159">In the Web app blade, click **Browse**.</span></span>
   
    ![site URL][browse]
4. <span data-ttu-id="f700c-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span><span class="sxs-lookup"><span data-stu-id="f700c-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configure WordPress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="f700c-163">Log in using the credentials you created on the **Welcome** page.</span><span class="sxs-lookup"><span data-stu-id="f700c-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="f700c-164">Your site Dashboard page opens.</span><span class="sxs-lookup"><span data-stu-id="f700c-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="f700c-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="f700c-166">Next steps</span></span>
<span data-ttu-id="f700c-167">You've seen how to create and deploy a PHP web app from the gallery.</span><span class="sxs-lookup"><span data-stu-id="f700c-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="f700c-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f700c-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="f700c-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span><span class="sxs-lookup"><span data-stu-id="f700c-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="f700c-170">What's changed</span><span class="sxs-lookup"><span data-stu-id="f700c-170">What's changed</span></span>
* <span data-ttu-id="f700c-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f700c-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-web-site-gallery/browse-web.png










