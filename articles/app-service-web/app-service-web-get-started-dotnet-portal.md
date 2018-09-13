---
title: Deploy an Umbraco web app in the Azure portal in five minutes | Microsoft Docs
description: Learn how easy it is to run web apps in App Service by deploying a sample ASP.NET app. See your results immediately.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 4e94653a0603437ef37e8a1f2c76926cd509115c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555025"
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="5a99d-104">Deploy an Umbraco web app in the Azure portal in five minutes</span><span class="sxs-lookup"><span data-stu-id="5a99d-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="5a99d-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span><span class="sxs-lookup"><span data-stu-id="5a99d-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="5a99d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5a99d-107">Prerequisites</span></span>
<span data-ttu-id="5a99d-108">You need a Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="5a99d-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="5a99d-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="5a99d-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="5a99d-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span><span class="sxs-lookup"><span data-stu-id="5a99d-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="5a99d-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span><span class="sxs-lookup"><span data-stu-id="5a99d-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="5a99d-112">Deploy the ASP.NET app</span><span class="sxs-lookup"><span data-stu-id="5a99d-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="5a99d-113">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a99d-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5a99d-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="5a99d-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="5a99d-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5a99d-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="5a99d-116">In **App name**, type a web app name.</span><span class="sxs-lookup"><span data-stu-id="5a99d-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="5a99d-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span><span class="sxs-lookup"><span data-stu-id="5a99d-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="5a99d-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span><span class="sxs-lookup"><span data-stu-id="5a99d-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="5a99d-119">Click **App Service plan/Location** > **Create New**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="5a99d-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span><span class="sxs-lookup"><span data-stu-id="5a99d-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="5a99d-121">In **App Service plan**, type the desired name.</span><span class="sxs-lookup"><span data-stu-id="5a99d-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="5a99d-122">In **Location**, choose a location to host your plan.</span><span class="sxs-lookup"><span data-stu-id="5a99d-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="5a99d-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="5a99d-124">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-124">Click **OK**.</span></span>

    <span data-ttu-id="5a99d-125">Your Umbraco CMS configuration should now look like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="5a99d-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuration in progress - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="5a99d-127">Click **SQL Database** > **Create a new database**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="5a99d-128">Configure the SQL Database as shown:</span><span class="sxs-lookup"><span data-stu-id="5a99d-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="5a99d-129">In **Name**, type a name, such as **myDB**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="5a99d-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="5a99d-131">Click **Target server** > **Create a new server**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="5a99d-132">Configure the database server as shown:</span><span class="sxs-lookup"><span data-stu-id="5a99d-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="5a99d-133">In **Server name**, type a server name.</span><span class="sxs-lookup"><span data-stu-id="5a99d-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="5a99d-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span><span class="sxs-lookup"><span data-stu-id="5a99d-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="5a99d-135">In **Server admin login**, type the desired admininistrator username.</span><span class="sxs-lookup"><span data-stu-id="5a99d-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="5a99d-136">In **Password** and **Confirm password**, type the desired password.</span><span class="sxs-lookup"><span data-stu-id="5a99d-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="5a99d-137">In Location, select the same location you use for the web app.</span><span class="sxs-lookup"><span data-stu-id="5a99d-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="5a99d-138">Make sure **Allow azure services to access server** is selected.</span><span class="sxs-lookup"><span data-stu-id="5a99d-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="5a99d-139">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="5a99d-140">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-140">Click **Select**.</span></span>

13. <span data-ttu-id="5a99d-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="5a99d-142">Your Umbraco CMS configuration should now look like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="5a99d-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuration complete - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="5a99d-144">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-144">Click **Create**.</span></span>
    
    <span data-ttu-id="5a99d-145">Azure now creates your Umbraco app based on your configuration.</span><span class="sxs-lookup"><span data-stu-id="5a99d-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="5a99d-146">You should see a **Deployment started...** notification.</span><span class="sxs-lookup"><span data-stu-id="5a99d-146">You should see a **Deployment started...** notification.</span></span>

    ![Deployment succeeded - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="5a99d-148">Launch and manage your Umrbaco web app</span><span class="sxs-lookup"><span data-stu-id="5a99d-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="5a99d-149">When Azure completes app deployment you see another notification.</span><span class="sxs-lookup"><span data-stu-id="5a99d-149">When Azure completes app deployment you see another notification.</span></span>

![Deployment succeeded - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="5a99d-151">Click the notification.</span><span class="sxs-lookup"><span data-stu-id="5a99d-151">Click the notification.</span></span> <span data-ttu-id="5a99d-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="5a99d-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="5a99d-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="5a99d-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="5a99d-154">In the top of the Overview page, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="5a99d-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Browse - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="5a99d-156">Now you see the Umbraco **Welcome** page.</span><span class="sxs-lookup"><span data-stu-id="5a99d-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="5a99d-157">Configure the Umbraco installation and start playing with it!</span><span class="sxs-lookup"><span data-stu-id="5a99d-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Umbraco configuration - first Umbraco in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="5a99d-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a99d-159">Next steps</span></span>
* <span data-ttu-id="5a99d-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span><span class="sxs-lookup"><span data-stu-id="5a99d-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="5a99d-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span><span class="sxs-lookup"><span data-stu-id="5a99d-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="5a99d-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span><span class="sxs-lookup"><span data-stu-id="5a99d-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="5a99d-163">Authenticate your users.</span><span class="sxs-lookup"><span data-stu-id="5a99d-163">Authenticate your users.</span></span> <span data-ttu-id="5a99d-164">Scale it based on demand.</span><span class="sxs-lookup"><span data-stu-id="5a99d-164">Scale it based on demand.</span></span> <span data-ttu-id="5a99d-165">Set up some performance alerts.</span><span class="sxs-lookup"><span data-stu-id="5a99d-165">Set up some performance alerts.</span></span> <span data-ttu-id="5a99d-166">All with a few clicks.</span><span class="sxs-lookup"><span data-stu-id="5a99d-166">All with a few clicks.</span></span>








