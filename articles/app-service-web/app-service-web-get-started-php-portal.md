---
title: Deploy a WordPress app in the Azure portal in five minutes | Microsoft Docs
description: Learn how easy it is to run web apps in App Service by deploying a WordPress app. See your results immediately.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 981dfcadb267df7a08432828b8aefd756cffd4ed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660731"
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="93d09-104">Deploy a WordPress app in the Azure portal in five minutes</span><span class="sxs-lookup"><span data-stu-id="93d09-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="93d09-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span><span class="sxs-lookup"><span data-stu-id="93d09-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="93d09-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="93d09-107">Prerequisites</span></span>
<span data-ttu-id="93d09-108">You need a Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="93d09-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="93d09-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="93d09-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="93d09-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span><span class="sxs-lookup"><span data-stu-id="93d09-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="93d09-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span><span class="sxs-lookup"><span data-stu-id="93d09-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="93d09-112">Deploy the WordPress app</span><span class="sxs-lookup"><span data-stu-id="93d09-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="93d09-113">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93d09-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="93d09-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="93d09-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="93d09-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="93d09-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="93d09-116">In **App name**, type a web app name.</span><span class="sxs-lookup"><span data-stu-id="93d09-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="93d09-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span><span class="sxs-lookup"><span data-stu-id="93d09-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="93d09-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span><span class="sxs-lookup"><span data-stu-id="93d09-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="93d09-119">In **Database Provider**, select **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="93d09-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="93d09-120">Click **App Service plan/Location** > **Create New**.</span><span class="sxs-lookup"><span data-stu-id="93d09-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="93d09-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span><span class="sxs-lookup"><span data-stu-id="93d09-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="93d09-122">In **App Service plan**, type the desired name.</span><span class="sxs-lookup"><span data-stu-id="93d09-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="93d09-123">In **Location**, choose a location to host your plan.</span><span class="sxs-lookup"><span data-stu-id="93d09-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="93d09-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="93d09-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="93d09-125">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="93d09-125">Click **OK**.</span></span>

8. <span data-ttu-id="93d09-126">Click **Database** > **Create New**.</span><span class="sxs-lookup"><span data-stu-id="93d09-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="93d09-127">Configure the SQL Database as shown:</span><span class="sxs-lookup"><span data-stu-id="93d09-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="93d09-128">In **Database Name**, type a database name.</span><span class="sxs-lookup"><span data-stu-id="93d09-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="93d09-129">In **Location**, choose the same location as the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="93d09-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="93d09-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="93d09-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="93d09-131">Click **Legal Terms** and click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="93d09-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="93d09-132">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="93d09-132">Click **OK**.</span></span>

9. <span data-ttu-id="93d09-133">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="93d09-133">Click **Create**.</span></span>

    <span data-ttu-id="93d09-134">Azure now creates your WordPress app based on your configuration.</span><span class="sxs-lookup"><span data-stu-id="93d09-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="93d09-135">You should see a **Deployment started...** notification.</span><span class="sxs-lookup"><span data-stu-id="93d09-135">You should see a **Deployment started...** notification.</span></span>

    ![Deployment started - first WordPress in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="93d09-137">Launch and manage your WordPress web app</span><span class="sxs-lookup"><span data-stu-id="93d09-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="93d09-138">When Azure completes app deployment you see another notification.</span><span class="sxs-lookup"><span data-stu-id="93d09-138">When Azure completes app deployment you see another notification.</span></span>

![Deployment succeeded - first WordPress in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="93d09-140">Click the notification.</span><span class="sxs-lookup"><span data-stu-id="93d09-140">Click the notification.</span></span> <span data-ttu-id="93d09-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="93d09-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="93d09-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="93d09-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="93d09-143">In the top of the Overview page, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="93d09-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Browse - first WordPress in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="93d09-145">Now you see the WordPress **Welcome** page.</span><span class="sxs-lookup"><span data-stu-id="93d09-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="93d09-146">Configure the WordPress installation and start playing with it!</span><span class="sxs-lookup"><span data-stu-id="93d09-146">Configure the WordPress installation and start playing with it!</span></span>

    ![WordPress configuration - first WordPress in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="93d09-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="93d09-148">Next steps</span></span>
* <span data-ttu-id="93d09-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span><span class="sxs-lookup"><span data-stu-id="93d09-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="93d09-150">Create and configure apps in Azure from PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="93d09-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="93d09-151">Set PHP version.</span><span class="sxs-lookup"><span data-stu-id="93d09-151">Set PHP version.</span></span>
    * <span data-ttu-id="93d09-152">Use a start file that is not in the root application directory.</span><span class="sxs-lookup"><span data-stu-id="93d09-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="93d09-153">Enable Composer automation.</span><span class="sxs-lookup"><span data-stu-id="93d09-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="93d09-154">Access environment-specific variables.</span><span class="sxs-lookup"><span data-stu-id="93d09-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="93d09-155">Troubleshoot common errors.</span><span class="sxs-lookup"><span data-stu-id="93d09-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="93d09-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span><span class="sxs-lookup"><span data-stu-id="93d09-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="93d09-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span><span class="sxs-lookup"><span data-stu-id="93d09-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="93d09-158">Authenticate your users.</span><span class="sxs-lookup"><span data-stu-id="93d09-158">Authenticate your users.</span></span> <span data-ttu-id="93d09-159">Scale it based on demand.</span><span class="sxs-lookup"><span data-stu-id="93d09-159">Scale it based on demand.</span></span> <span data-ttu-id="93d09-160">Set up some performance alerts.</span><span class="sxs-lookup"><span data-stu-id="93d09-160">Set up some performance alerts.</span></span> <span data-ttu-id="93d09-161">All with a few clicks.</span><span class="sxs-lookup"><span data-stu-id="93d09-161">All with a few clicks.</span></span>






