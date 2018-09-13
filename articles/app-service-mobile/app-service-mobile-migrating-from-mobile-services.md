---
title: Migrate from Mobile Services to an App Service Mobile App
description: Learn how to easily migrate your Mobile Services application to an App Service Mobile App
services: app-service\mobile
documentationcenter: ''
author: conceptdev
manager: crdun
editor: ''
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: crdun
ms.openlocfilehash: 5001704f47af0c7b07744f1dceb7aa58bdb6448c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808898"
---
# <a name="article-top"></a><span data-ttu-id="0c22e-103">Migrate your existing Azure Mobile Service to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0c22e-103">Migrate your existing Azure Mobile Service to Azure App Service</span></span>
<span data-ttu-id="0c22e-104">With the [general availability of Azure App Service], Azure Mobile Services sites can be easily migrated in-place to take advantage of all the features of the Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-104">With the [general availability of Azure App Service], Azure Mobile Services sites can be easily migrated in-place to take advantage of all the features of the Azure App Service.</span></span>  <span data-ttu-id="0c22e-105">This document explains what to expect when migrating your site from Azure Mobile Services to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-105">This document explains what to expect when migrating your site from Azure Mobile Services to Azure App Service.</span></span>

## <a name="what-does-migration-do"></a><span data-ttu-id="0c22e-106">What does migration do to your site</span><span class="sxs-lookup"><span data-stu-id="0c22e-106">What does migration do to your site</span></span>
<span data-ttu-id="0c22e-107">Migration of your Azure Mobile Service turns your Mobile Service into an [Azure App Service] app without affecting the code.</span><span class="sxs-lookup"><span data-stu-id="0c22e-107">Migration of your Azure Mobile Service turns your Mobile Service into an [Azure App Service] app without affecting the code.</span></span>  <span data-ttu-id="0c22e-108">Your Notification Hubs, SQL data connection, authentication settings, scheduled jobs, and domain name remain unchanged.</span><span class="sxs-lookup"><span data-stu-id="0c22e-108">Your Notification Hubs, SQL data connection, authentication settings, scheduled jobs, and domain name remain unchanged.</span></span>  <span data-ttu-id="0c22e-109">Mobile clients using your Azure Mobile Service continue to operate normally.</span><span class="sxs-lookup"><span data-stu-id="0c22e-109">Mobile clients using your Azure Mobile Service continue to operate normally.</span></span>  <span data-ttu-id="0c22e-110">Migration restarts your service once it is transferred to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-110">Migration restarts your service once it is transferred to Azure App Service.</span></span>

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a><span data-ttu-id="0c22e-111">Why you should migrate your site</span><span class="sxs-lookup"><span data-stu-id="0c22e-111">Why you should migrate your site</span></span>
<span data-ttu-id="0c22e-112">Microsoft is recommending that you migrate your Azure Mobile Service to take advantage of the features of Azure App Service, including:</span><span class="sxs-lookup"><span data-stu-id="0c22e-112">Microsoft is recommending that you migrate your Azure Mobile Service to take advantage of the features of Azure App Service, including:</span></span>

* <span data-ttu-id="0c22e-113">New host features, including [WebJobs] and [custom domain names].</span><span class="sxs-lookup"><span data-stu-id="0c22e-113">New host features, including [WebJobs] and [custom domain names].</span></span>
* <span data-ttu-id="0c22e-114">Monitoring and troubleshooting with [Application Insights].</span><span class="sxs-lookup"><span data-stu-id="0c22e-114">Monitoring and troubleshooting with [Application Insights].</span></span>
* <span data-ttu-id="0c22e-115">Built-in DevOps tooling, including [staging slots], roll-back, and in-production testing.</span><span class="sxs-lookup"><span data-stu-id="0c22e-115">Built-in DevOps tooling, including [staging slots], roll-back, and in-production testing.</span></span>
* <span data-ttu-id="0c22e-116">[Auto-scale], load balancing, and [performance monitoring].</span><span class="sxs-lookup"><span data-stu-id="0c22e-116">[Auto-scale], load balancing, and [performance monitoring].</span></span>

<span data-ttu-id="0c22e-117">For more information on the benefits of Azure App Service, see the [Mobile Services vs. App Service] topic.</span><span class="sxs-lookup"><span data-stu-id="0c22e-117">For more information on the benefits of Azure App Service, see the [Mobile Services vs. App Service] topic.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0c22e-118">Before you begin</span><span class="sxs-lookup"><span data-stu-id="0c22e-118">Before you begin</span></span>
<span data-ttu-id="0c22e-119">Before beginning any major work on your site, you should back up your Mobile Service scripts and SQL database.</span><span class="sxs-lookup"><span data-stu-id="0c22e-119">Before beginning any major work on your site, you should back up your Mobile Service scripts and SQL database.</span></span>

## <a name="migrating-site"></a><span data-ttu-id="0c22e-120">Migrating your sites</span><span class="sxs-lookup"><span data-stu-id="0c22e-120">Migrating your sites</span></span>
<span data-ttu-id="0c22e-121">The migration process migrates all sites within a single Azure Region.</span><span class="sxs-lookup"><span data-stu-id="0c22e-121">The migration process migrates all sites within a single Azure Region.</span></span>

<span data-ttu-id="0c22e-122">To migrate your site:</span><span class="sxs-lookup"><span data-stu-id="0c22e-122">To migrate your site:</span></span>

1. <span data-ttu-id="0c22e-123">Log in to the [Azure Classic Portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-123">Log in to the [Azure Classic Portal].</span></span>
2. <span data-ttu-id="0c22e-124">Select a Mobile Service in the region you wish to migrate.</span><span class="sxs-lookup"><span data-stu-id="0c22e-124">Select a Mobile Service in the region you wish to migrate.</span></span>
3. <span data-ttu-id="0c22e-125">Click the **Migrate to App Service** button.</span><span class="sxs-lookup"><span data-stu-id="0c22e-125">Click the **Migrate to App Service** button.</span></span>

   ![The Migrate Button][0]
4. <span data-ttu-id="0c22e-127">Read the Migrate to App Service dialog.</span><span class="sxs-lookup"><span data-stu-id="0c22e-127">Read the Migrate to App Service dialog.</span></span>
5. <span data-ttu-id="0c22e-128">Enter the name of your Mobile Service in the box provided.</span><span class="sxs-lookup"><span data-stu-id="0c22e-128">Enter the name of your Mobile Service in the box provided.</span></span>  <span data-ttu-id="0c22e-129">For example, if your domain name is contoso.azure-mobile.net, then enter *contoso* in the box provided.</span><span class="sxs-lookup"><span data-stu-id="0c22e-129">For example, if your domain name is contoso.azure-mobile.net, then enter *contoso* in the box provided.</span></span>
6. <span data-ttu-id="0c22e-130">Click the tick button.</span><span class="sxs-lookup"><span data-stu-id="0c22e-130">Click the tick button.</span></span>

<span data-ttu-id="0c22e-131">Monitor the status of the migration in the activity monitor.</span><span class="sxs-lookup"><span data-stu-id="0c22e-131">Monitor the status of the migration in the activity monitor.</span></span> <span data-ttu-id="0c22e-132">Your site is listed as *migrating* in the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="0c22e-132">Your site is listed as *migrating* in the Azure Classic Portal.</span></span>

  ![Migration Activity Monitor][1]

<span data-ttu-id="0c22e-134">Each migration can take anywhere from 3 to 15 minutes per mobile service being migrated.</span><span class="sxs-lookup"><span data-stu-id="0c22e-134">Each migration can take anywhere from 3 to 15 minutes per mobile service being migrated.</span></span>  <span data-ttu-id="0c22e-135">Your site remains available during the migration.</span><span class="sxs-lookup"><span data-stu-id="0c22e-135">Your site remains available during the migration.</span></span>
<span data-ttu-id="0c22e-136">Your site is restarted at the end of the migration process.</span><span class="sxs-lookup"><span data-stu-id="0c22e-136">Your site is restarted at the end of the migration process.</span></span>  <span data-ttu-id="0c22e-137">The site is unavailable during the restart process, which may last a couple of seconds.</span><span class="sxs-lookup"><span data-stu-id="0c22e-137">The site is unavailable during the restart process, which may last a couple of seconds.</span></span>

## <a name="finalizing-migration"></a><span data-ttu-id="0c22e-138">Finalizing the Migration</span><span class="sxs-lookup"><span data-stu-id="0c22e-138">Finalizing the Migration</span></span>
<span data-ttu-id="0c22e-139">Plan to test your site from a mobile client at the conclusion of the migration process.</span><span class="sxs-lookup"><span data-stu-id="0c22e-139">Plan to test your site from a mobile client at the conclusion of the migration process.</span></span>  <span data-ttu-id="0c22e-140">Ensure you can perform all common client actions without changes to the mobile client.</span><span class="sxs-lookup"><span data-stu-id="0c22e-140">Ensure you can perform all common client actions without changes to the mobile client.</span></span>  

### <a name="update-app-service-tier"></a><span data-ttu-id="0c22e-141">Select an appropriate App Service pricing tier</span><span class="sxs-lookup"><span data-stu-id="0c22e-141">Select an appropriate App Service pricing tier</span></span>
<span data-ttu-id="0c22e-142">You have more flexibility in pricing after you migrate to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-142">You have more flexibility in pricing after you migrate to Azure App Service.</span></span>

1. <span data-ttu-id="0c22e-143">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-143">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-144">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-144">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-145">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-145">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-146">Click **App Service Plan** in the Settings menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-146">Click **App Service Plan** in the Settings menu.</span></span>
5. <span data-ttu-id="0c22e-147">Click the **Pricing Tier** tile.</span><span class="sxs-lookup"><span data-stu-id="0c22e-147">Click the **Pricing Tier** tile.</span></span>
6. <span data-ttu-id="0c22e-148">Click the tile appropriate to your requirements, then Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="0c22e-148">Click the tile appropriate to your requirements, then Click **Select**.</span></span>  <span data-ttu-id="0c22e-149">You may need to Click **View all** to see the available pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="0c22e-149">You may need to Click **View all** to see the available pricing tiers.</span></span>

<span data-ttu-id="0c22e-150">As a starting point, we recommend the following tiers:</span><span class="sxs-lookup"><span data-stu-id="0c22e-150">As a starting point, we recommend the following tiers:</span></span>

| <span data-ttu-id="0c22e-151">Mobile Service Pricing Tier</span><span class="sxs-lookup"><span data-stu-id="0c22e-151">Mobile Service Pricing Tier</span></span> | <span data-ttu-id="0c22e-152">App Service Pricing Tier</span><span class="sxs-lookup"><span data-stu-id="0c22e-152">App Service Pricing Tier</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c22e-153">Free</span><span class="sxs-lookup"><span data-stu-id="0c22e-153">Free</span></span> |<span data-ttu-id="0c22e-154">F1 Free</span><span class="sxs-lookup"><span data-stu-id="0c22e-154">F1 Free</span></span> |
| <span data-ttu-id="0c22e-155">Basic</span><span class="sxs-lookup"><span data-stu-id="0c22e-155">Basic</span></span> |<span data-ttu-id="0c22e-156">B1 Basic</span><span class="sxs-lookup"><span data-stu-id="0c22e-156">B1 Basic</span></span> |
| <span data-ttu-id="0c22e-157">Standard</span><span class="sxs-lookup"><span data-stu-id="0c22e-157">Standard</span></span> |<span data-ttu-id="0c22e-158">S1 Standard</span><span class="sxs-lookup"><span data-stu-id="0c22e-158">S1 Standard</span></span> |

<span data-ttu-id="0c22e-159">There is considerable flexibility in choosing the right pricing tier for your application.</span><span class="sxs-lookup"><span data-stu-id="0c22e-159">There is considerable flexibility in choosing the right pricing tier for your application.</span></span>  <span data-ttu-id="0c22e-160">Refer to [App Service Pricing] for full details on the pricing of your new App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-160">Refer to [App Service Pricing] for full details on the pricing of your new App Service.</span></span>

> [!TIP]
> <span data-ttu-id="0c22e-161">The App Service Standard tier contains access to many features that you may want to use, including [staging slots], automatic backups, and auto-scaling.</span><span class="sxs-lookup"><span data-stu-id="0c22e-161">The App Service Standard tier contains access to many features that you may want to use, including [staging slots], automatic backups, and auto-scaling.</span></span>  <span data-ttu-id="0c22e-162">Check out the new capabilities while you are there!</span><span class="sxs-lookup"><span data-stu-id="0c22e-162">Check out the new capabilities while you are there!</span></span>
>
>

### <a name="review-migration-scheduler-jobs"></a><span data-ttu-id="0c22e-163">Review the Migrated Scheduler Jobs</span><span class="sxs-lookup"><span data-stu-id="0c22e-163">Review the Migrated Scheduler Jobs</span></span>
<span data-ttu-id="0c22e-164">Scheduler Jobs will not be visible until approximately 30 minutes after migration.</span><span class="sxs-lookup"><span data-stu-id="0c22e-164">Scheduler Jobs will not be visible until approximately 30 minutes after migration.</span></span>  <span data-ttu-id="0c22e-165">Scheduled jobs continue to run in the background.</span><span class="sxs-lookup"><span data-stu-id="0c22e-165">Scheduled jobs continue to run in the background.</span></span>
<span data-ttu-id="0c22e-166">To view your scheduled jobs after they are visible again:</span><span class="sxs-lookup"><span data-stu-id="0c22e-166">To view your scheduled jobs after they are visible again:</span></span>

1. <span data-ttu-id="0c22e-167">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-167">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-168">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span><span class="sxs-lookup"><span data-stu-id="0c22e-168">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span></span>

<span data-ttu-id="0c22e-169">There are a limited number of free scheduler jobs available post-migration.</span><span class="sxs-lookup"><span data-stu-id="0c22e-169">There are a limited number of free scheduler jobs available post-migration.</span></span>  <span data-ttu-id="0c22e-170">Review your usage and the [Azure Scheduler Plans].</span><span class="sxs-lookup"><span data-stu-id="0c22e-170">Review your usage and the [Azure Scheduler Plans].</span></span>

### <a name="configure-cors"></a><span data-ttu-id="0c22e-171">Configure CORS if needed</span><span class="sxs-lookup"><span data-stu-id="0c22e-171">Configure CORS if needed</span></span>
<span data-ttu-id="0c22e-172">Cross-origin resource sharing is a technique to allow a website to access a Web API on a different domain.</span><span class="sxs-lookup"><span data-stu-id="0c22e-172">Cross-origin resource sharing is a technique to allow a website to access a Web API on a different domain.</span></span>  <span data-ttu-id="0c22e-173">If you are using Azure Mobile Services with an associated website, then you need to configure CORS as part of the migration.</span><span class="sxs-lookup"><span data-stu-id="0c22e-173">If you are using Azure Mobile Services with an associated website, then you need to configure CORS as part of the migration.</span></span>  <span data-ttu-id="0c22e-174">If you are accessing Azure Mobile Services exclusively from mobile devices, then CORS does not need to be configured except in rare cases.</span><span class="sxs-lookup"><span data-stu-id="0c22e-174">If you are accessing Azure Mobile Services exclusively from mobile devices, then CORS does not need to be configured except in rare cases.</span></span>

<span data-ttu-id="0c22e-175">Your migrated CORS settings are available as the **MS_CrossDomainWhitelist** App Setting.</span><span class="sxs-lookup"><span data-stu-id="0c22e-175">Your migrated CORS settings are available as the **MS_CrossDomainWhitelist** App Setting.</span></span>  <span data-ttu-id="0c22e-176">To migrate your site to the App Service CORS facility:</span><span class="sxs-lookup"><span data-stu-id="0c22e-176">To migrate your site to the App Service CORS facility:</span></span>

1. <span data-ttu-id="0c22e-177">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-177">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-178">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-178">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-179">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-179">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-180">Click **CORS** in the API menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-180">Click **CORS** in the API menu.</span></span>
5. <span data-ttu-id="0c22e-181">Enter any Allowed Origins in the box provided, pressing Enter after each one.</span><span class="sxs-lookup"><span data-stu-id="0c22e-181">Enter any Allowed Origins in the box provided, pressing Enter after each one.</span></span>
6. <span data-ttu-id="0c22e-182">Once your list of Allowed Origins is correct, click the Save button.</span><span class="sxs-lookup"><span data-stu-id="0c22e-182">Once your list of Allowed Origins is correct, click the Save button.</span></span>

> [!TIP]
> <span data-ttu-id="0c22e-183">One of the advantages of using an Azure App Service is that you can run your web site and mobile service on the same site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-183">One of the advantages of using an Azure App Service is that you can run your web site and mobile service on the same site.</span></span>  <span data-ttu-id="0c22e-184">For more information, see the [next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="0c22e-184">For more information, see the [next steps](#next-steps) section.</span></span>
>
>

### <a name="download-publish-profile"></a><span data-ttu-id="0c22e-185">Download a new Publishing Profile</span><span class="sxs-lookup"><span data-stu-id="0c22e-185">Download a new Publishing Profile</span></span>
<span data-ttu-id="0c22e-186">The publishing profile of your site is changed when migrating to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-186">The publishing profile of your site is changed when migrating to Azure App Service.</span></span>  <span data-ttu-id="0c22e-187">If you intend to publish your site from within Visual Studio, you need a new publishing profile.</span><span class="sxs-lookup"><span data-stu-id="0c22e-187">If you intend to publish your site from within Visual Studio, you need a new publishing profile.</span></span>  <span data-ttu-id="0c22e-188">To download the new publishing profile:</span><span class="sxs-lookup"><span data-stu-id="0c22e-188">To download the new publishing profile:</span></span>

1. <span data-ttu-id="0c22e-189">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-189">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-190">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-190">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-191">Click **Get publish profile**.</span><span class="sxs-lookup"><span data-stu-id="0c22e-191">Click **Get publish profile**.</span></span>

<span data-ttu-id="0c22e-192">The PublishSettings file is downloaded to your computer.</span><span class="sxs-lookup"><span data-stu-id="0c22e-192">The PublishSettings file is downloaded to your computer.</span></span>  <span data-ttu-id="0c22e-193">It is normally called *sitename*.PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="0c22e-193">It is normally called *sitename*.PublishSettings.</span></span>  <span data-ttu-id="0c22e-194">Import the publish settings into your existing project:</span><span class="sxs-lookup"><span data-stu-id="0c22e-194">Import the publish settings into your existing project:</span></span>

1. <span data-ttu-id="0c22e-195">Open Visual Studio and your Azure Mobile Service project.</span><span class="sxs-lookup"><span data-stu-id="0c22e-195">Open Visual Studio and your Azure Mobile Service project.</span></span>
2. <span data-ttu-id="0c22e-196">Right-Click your project in the **Solution Explorer** and select **Publish...**</span><span class="sxs-lookup"><span data-stu-id="0c22e-196">Right-Click your project in the **Solution Explorer** and select **Publish...**</span></span>
3. <span data-ttu-id="0c22e-197">Click **Import**</span><span class="sxs-lookup"><span data-stu-id="0c22e-197">Click **Import**</span></span>
4. <span data-ttu-id="0c22e-198">Click **Browse** and select your downloaded publish settings file.</span><span class="sxs-lookup"><span data-stu-id="0c22e-198">Click **Browse** and select your downloaded publish settings file.</span></span>  <span data-ttu-id="0c22e-199">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="0c22e-199">Click **OK**</span></span>
5. <span data-ttu-id="0c22e-200">Click **Validate Connection** to ensure the publish settings work.</span><span class="sxs-lookup"><span data-stu-id="0c22e-200">Click **Validate Connection** to ensure the publish settings work.</span></span>
6. <span data-ttu-id="0c22e-201">Click **Publish** to publish your site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-201">Click **Publish** to publish your site.</span></span>

## <a name="working-with-your-site"></a><span data-ttu-id="0c22e-202">Working with your site post-migration</span><span class="sxs-lookup"><span data-stu-id="0c22e-202">Working with your site post-migration</span></span>
<span data-ttu-id="0c22e-203">Start working with your new App Service in the [Azure portal] post-migration.</span><span class="sxs-lookup"><span data-stu-id="0c22e-203">Start working with your new App Service in the [Azure portal] post-migration.</span></span>  <span data-ttu-id="0c22e-204">The following are some notes on specific operations that you used to perform in the [Azure Classic Portal], together with their App Service equivalent.</span><span class="sxs-lookup"><span data-stu-id="0c22e-204">The following are some notes on specific operations that you used to perform in the [Azure Classic Portal], together with their App Service equivalent.</span></span>

### <a name="publishing-your-site"></a><span data-ttu-id="0c22e-205">Downloading and Publishing your migrated site</span><span class="sxs-lookup"><span data-stu-id="0c22e-205">Downloading and Publishing your migrated site</span></span>
<span data-ttu-id="0c22e-206">Your site is available via git or ftp and can be republished with various different mechanisms, including WebDeploy, TFS, Mercurial, GitHub, and FTP.</span><span class="sxs-lookup"><span data-stu-id="0c22e-206">Your site is available via git or ftp and can be republished with various different mechanisms, including WebDeploy, TFS, Mercurial, GitHub, and FTP.</span></span>  <span data-ttu-id="0c22e-207">The deployment credentials are migrated with the rest of your site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-207">The deployment credentials are migrated with the rest of your site.</span></span>  <span data-ttu-id="0c22e-208">If you did not set your deployment credentials or you do not remember them, you can reset them:</span><span class="sxs-lookup"><span data-stu-id="0c22e-208">If you did not set your deployment credentials or you do not remember them, you can reset them:</span></span>

1. <span data-ttu-id="0c22e-209">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-209">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-210">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-210">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-211">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-211">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-212">Click **Deployment credentials** in the PUBLISHING menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-212">Click **Deployment credentials** in the PUBLISHING menu.</span></span>
5. <span data-ttu-id="0c22e-213">Enter the new deployment credentials in the boxes provided, then click the Save button.</span><span class="sxs-lookup"><span data-stu-id="0c22e-213">Enter the new deployment credentials in the boxes provided, then click the Save button.</span></span>

<span data-ttu-id="0c22e-214">You can use these credentials to clone the site with git or set up automated deployments from GitHub, TFS, or Mercurial.</span><span class="sxs-lookup"><span data-stu-id="0c22e-214">You can use these credentials to clone the site with git or set up automated deployments from GitHub, TFS, or Mercurial.</span></span>  <span data-ttu-id="0c22e-215">For more information, see the [Azure App Service deployment documentation].</span><span class="sxs-lookup"><span data-stu-id="0c22e-215">For more information, see the [Azure App Service deployment documentation].</span></span>

### <a name="appsettings"></a><span data-ttu-id="0c22e-216">Application Settings</span><span class="sxs-lookup"><span data-stu-id="0c22e-216">Application Settings</span></span>
<span data-ttu-id="0c22e-217">Most settings for a migrated mobile service are available via App Settings.</span><span class="sxs-lookup"><span data-stu-id="0c22e-217">Most settings for a migrated mobile service are available via App Settings.</span></span>  <span data-ttu-id="0c22e-218">You can get a list of the app settings from the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-218">You can get a list of the app settings from the [Azure portal].</span></span>
<span data-ttu-id="0c22e-219">To view or change your app settings:</span><span class="sxs-lookup"><span data-stu-id="0c22e-219">To view or change your app settings:</span></span>

1. <span data-ttu-id="0c22e-220">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-220">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-221">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-221">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-222">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-222">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-223">Click **Application settings** in the GENERAL menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-223">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="0c22e-224">Scroll to the App Settings section and find your app setting.</span><span class="sxs-lookup"><span data-stu-id="0c22e-224">Scroll to the App Settings section and find your app setting.</span></span>
6. <span data-ttu-id="0c22e-225">Click the value of the app setting to edit the value.</span><span class="sxs-lookup"><span data-stu-id="0c22e-225">Click the value of the app setting to edit the value.</span></span>  <span data-ttu-id="0c22e-226">Click **Save** to save the value.</span><span class="sxs-lookup"><span data-stu-id="0c22e-226">Click **Save** to save the value.</span></span>

<span data-ttu-id="0c22e-227">You can update multiple app settings at the same time.</span><span class="sxs-lookup"><span data-stu-id="0c22e-227">You can update multiple app settings at the same time.</span></span>

> [!TIP]
> <span data-ttu-id="0c22e-228">There are two Application Settings with the same value.</span><span class="sxs-lookup"><span data-stu-id="0c22e-228">There are two Application Settings with the same value.</span></span>  <span data-ttu-id="0c22e-229">For example, you may see *ApplicationKey* and *MS\_ApplicationKey*.</span><span class="sxs-lookup"><span data-stu-id="0c22e-229">For example, you may see *ApplicationKey* and *MS\_ApplicationKey*.</span></span>  <span data-ttu-id="0c22e-230">Update both application settings at the same time.</span><span class="sxs-lookup"><span data-stu-id="0c22e-230">Update both application settings at the same time.</span></span>
>
>

### <a name="authentication"></a><span data-ttu-id="0c22e-231">Authentication</span><span class="sxs-lookup"><span data-stu-id="0c22e-231">Authentication</span></span>
<span data-ttu-id="0c22e-232">All authentication settings are available as App Settings in your migrated site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-232">All authentication settings are available as App Settings in your migrated site.</span></span>  <span data-ttu-id="0c22e-233">To update your authentication settings, you must alter the appropriate app settings.</span><span class="sxs-lookup"><span data-stu-id="0c22e-233">To update your authentication settings, you must alter the appropriate app settings.</span></span>  <span data-ttu-id="0c22e-234">The following table shows the appropriate app settings for your authentication provider:</span><span class="sxs-lookup"><span data-stu-id="0c22e-234">The following table shows the appropriate app settings for your authentication provider:</span></span>

| <span data-ttu-id="0c22e-235">Provider</span><span class="sxs-lookup"><span data-stu-id="0c22e-235">Provider</span></span> | <span data-ttu-id="0c22e-236">Client ID</span><span class="sxs-lookup"><span data-stu-id="0c22e-236">Client ID</span></span> | <span data-ttu-id="0c22e-237">Client Secret</span><span class="sxs-lookup"><span data-stu-id="0c22e-237">Client Secret</span></span> | <span data-ttu-id="0c22e-238">Other Settings</span><span class="sxs-lookup"><span data-stu-id="0c22e-238">Other Settings</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0c22e-239">Microsoft Account</span><span class="sxs-lookup"><span data-stu-id="0c22e-239">Microsoft Account</span></span> |<span data-ttu-id="0c22e-240">**MS\_MicrosoftClientID**</span><span class="sxs-lookup"><span data-stu-id="0c22e-240">**MS\_MicrosoftClientID**</span></span> |<span data-ttu-id="0c22e-241">**MS\_MicrosoftClientSecret**</span><span class="sxs-lookup"><span data-stu-id="0c22e-241">**MS\_MicrosoftClientSecret**</span></span> |<span data-ttu-id="0c22e-242">**MS\_MicrosoftPackageSID**</span><span class="sxs-lookup"><span data-stu-id="0c22e-242">**MS\_MicrosoftPackageSID**</span></span> |
| <span data-ttu-id="0c22e-243">Facebook</span><span class="sxs-lookup"><span data-stu-id="0c22e-243">Facebook</span></span> |<span data-ttu-id="0c22e-244">**MS\_FacebookAppID**</span><span class="sxs-lookup"><span data-stu-id="0c22e-244">**MS\_FacebookAppID**</span></span> |<span data-ttu-id="0c22e-245">**MS\_FacebookAppSecret**</span><span class="sxs-lookup"><span data-stu-id="0c22e-245">**MS\_FacebookAppSecret**</span></span> | |
| <span data-ttu-id="0c22e-246">Twitter</span><span class="sxs-lookup"><span data-stu-id="0c22e-246">Twitter</span></span> |<span data-ttu-id="0c22e-247">**MS\_TwitterConsumerKey**</span><span class="sxs-lookup"><span data-stu-id="0c22e-247">**MS\_TwitterConsumerKey**</span></span> |<span data-ttu-id="0c22e-248">**MS\_TwitterConsumerSecret**</span><span class="sxs-lookup"><span data-stu-id="0c22e-248">**MS\_TwitterConsumerSecret**</span></span> | |
| <span data-ttu-id="0c22e-249">Google</span><span class="sxs-lookup"><span data-stu-id="0c22e-249">Google</span></span> |<span data-ttu-id="0c22e-250">**MS\_GoogleClientID**</span><span class="sxs-lookup"><span data-stu-id="0c22e-250">**MS\_GoogleClientID**</span></span> |<span data-ttu-id="0c22e-251">**MS\_GoogleClientSecret**</span><span class="sxs-lookup"><span data-stu-id="0c22e-251">**MS\_GoogleClientSecret**</span></span> | |
| <span data-ttu-id="0c22e-252">Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c22e-252">Azure AD</span></span> |<span data-ttu-id="0c22e-253">**MS\_AadClientID**</span><span class="sxs-lookup"><span data-stu-id="0c22e-253">**MS\_AadClientID**</span></span> | |<span data-ttu-id="0c22e-254">**MS\_AadTenants**</span><span class="sxs-lookup"><span data-stu-id="0c22e-254">**MS\_AadTenants**</span></span> |

<span data-ttu-id="0c22e-255">Note: **MS\_AadTenants** is stored as a comma-separated list of tenant domains (the "Allowed Tenants" fields in the Mobile Services portal).</span><span class="sxs-lookup"><span data-stu-id="0c22e-255">Note: **MS\_AadTenants** is stored as a comma-separated list of tenant domains (the "Allowed Tenants" fields in the Mobile Services portal).</span></span>

> [!WARNING]
> <span data-ttu-id="0c22e-256">**Do not use the authentication mechanisms in the Settings menu**</span><span class="sxs-lookup"><span data-stu-id="0c22e-256">**Do not use the authentication mechanisms in the Settings menu**</span></span>
>
> <span data-ttu-id="0c22e-257">Azure App Service provides a separate "no-code" Authentication and Authorization system under the *Authentication / Authorization* Settings menu and the (deprecated) *Mobile Authentication* option under the Settings menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-257">Azure App Service provides a separate "no-code" Authentication and Authorization system under the *Authentication / Authorization* Settings menu and the (deprecated) *Mobile Authentication* option under the Settings menu.</span></span>  <span data-ttu-id="0c22e-258">These options are incompatible with a migrated Azure Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-258">These options are incompatible with a migrated Azure Mobile Service.</span></span>  <span data-ttu-id="0c22e-259">You can [upgrade your site](app-service-mobile-net-upgrading-from-mobile-services.md) to take advantage of the Azure App Service authentication.</span><span class="sxs-lookup"><span data-stu-id="0c22e-259">You can [upgrade your site](app-service-mobile-net-upgrading-from-mobile-services.md) to take advantage of the Azure App Service authentication.</span></span>
>
>

### <a name="easytables"></a><span data-ttu-id="0c22e-260">Data</span><span class="sxs-lookup"><span data-stu-id="0c22e-260">Data</span></span>
<span data-ttu-id="0c22e-261">The *Data* tab in Mobile Services has been replaced by *Easy Tables* within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c22e-261">The *Data* tab in Mobile Services has been replaced by *Easy Tables* within the Azure portal.</span></span>  <span data-ttu-id="0c22e-262">To access Easy Tables:</span><span class="sxs-lookup"><span data-stu-id="0c22e-262">To access Easy Tables:</span></span>

1. <span data-ttu-id="0c22e-263">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-263">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-264">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-264">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-265">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-265">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-266">Click **Easy tables** in the MOBILE menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-266">Click **Easy tables** in the MOBILE menu.</span></span>

<span data-ttu-id="0c22e-267">You can add a table by clicking the **Add** button or access your existing tables by clicking a table name.</span><span class="sxs-lookup"><span data-stu-id="0c22e-267">You can add a table by clicking the **Add** button or access your existing tables by clicking a table name.</span></span>  <span data-ttu-id="0c22e-268">There are various operations you can do from this blade, including:</span><span class="sxs-lookup"><span data-stu-id="0c22e-268">There are various operations you can do from this blade, including:</span></span>

* <span data-ttu-id="0c22e-269">Changing table permissions</span><span class="sxs-lookup"><span data-stu-id="0c22e-269">Changing table permissions</span></span>
* <span data-ttu-id="0c22e-270">Editing the operational scripts</span><span class="sxs-lookup"><span data-stu-id="0c22e-270">Editing the operational scripts</span></span>
* <span data-ttu-id="0c22e-271">Managing the table schema</span><span class="sxs-lookup"><span data-stu-id="0c22e-271">Managing the table schema</span></span>
* <span data-ttu-id="0c22e-272">Deleting the table</span><span class="sxs-lookup"><span data-stu-id="0c22e-272">Deleting the table</span></span>
* <span data-ttu-id="0c22e-273">Clearing the table contents</span><span class="sxs-lookup"><span data-stu-id="0c22e-273">Clearing the table contents</span></span>
* <span data-ttu-id="0c22e-274">Deleting specific rows of the table</span><span class="sxs-lookup"><span data-stu-id="0c22e-274">Deleting specific rows of the table</span></span>

### <a name="easyapis"></a><span data-ttu-id="0c22e-275">API</span><span class="sxs-lookup"><span data-stu-id="0c22e-275">API</span></span>
<span data-ttu-id="0c22e-276">The *API* tab in Mobile Services has been replaced by *Easy APIs* within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0c22e-276">The *API* tab in Mobile Services has been replaced by *Easy APIs* within the Azure portal.</span></span>  <span data-ttu-id="0c22e-277">To access Easy APIs:</span><span class="sxs-lookup"><span data-stu-id="0c22e-277">To access Easy APIs:</span></span>

1. <span data-ttu-id="0c22e-278">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-278">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-279">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-279">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-280">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-280">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-281">Click **Easy APIs** in the MOBILE menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-281">Click **Easy APIs** in the MOBILE menu.</span></span>

<span data-ttu-id="0c22e-282">Your migrated APIs are already listed in the blade.</span><span class="sxs-lookup"><span data-stu-id="0c22e-282">Your migrated APIs are already listed in the blade.</span></span>  <span data-ttu-id="0c22e-283">You can also add an API from this blade.</span><span class="sxs-lookup"><span data-stu-id="0c22e-283">You can also add an API from this blade.</span></span>  <span data-ttu-id="0c22e-284">To manage a specific API, click the API.</span><span class="sxs-lookup"><span data-stu-id="0c22e-284">To manage a specific API, click the API.</span></span>
<span data-ttu-id="0c22e-285">From the new blade, you can adjust the permissions and edit the scripts for the API.</span><span class="sxs-lookup"><span data-stu-id="0c22e-285">From the new blade, you can adjust the permissions and edit the scripts for the API.</span></span>

### <a name="on-demand-jobs"></a><span data-ttu-id="0c22e-286">Scheduler Jobs</span><span class="sxs-lookup"><span data-stu-id="0c22e-286">Scheduler Jobs</span></span>
<span data-ttu-id="0c22e-287">All scheduler jobs are available through the Scheduler Job Collections section.</span><span class="sxs-lookup"><span data-stu-id="0c22e-287">All scheduler jobs are available through the Scheduler Job Collections section.</span></span>  <span data-ttu-id="0c22e-288">To access your scheduler jobs:</span><span class="sxs-lookup"><span data-stu-id="0c22e-288">To access your scheduler jobs:</span></span>

1. <span data-ttu-id="0c22e-289">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-289">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-290">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span><span class="sxs-lookup"><span data-stu-id="0c22e-290">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span></span>
3. <span data-ttu-id="0c22e-291">Select the Job Collection for your site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-291">Select the Job Collection for your site.</span></span>  <span data-ttu-id="0c22e-292">It is named *sitename*-Jobs.</span><span class="sxs-lookup"><span data-stu-id="0c22e-292">It is named *sitename*-Jobs.</span></span>
4. <span data-ttu-id="0c22e-293">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="0c22e-293">Click **Settings**.</span></span>
5. <span data-ttu-id="0c22e-294">Click **Scheduler Jobs** under MANAGE.</span><span class="sxs-lookup"><span data-stu-id="0c22e-294">Click **Scheduler Jobs** under MANAGE.</span></span>

<span data-ttu-id="0c22e-295">Scheduled jobs are listed with the frequency you specified before migration.</span><span class="sxs-lookup"><span data-stu-id="0c22e-295">Scheduled jobs are listed with the frequency you specified before migration.</span></span>  <span data-ttu-id="0c22e-296">On-demand jobs are disabled.</span><span class="sxs-lookup"><span data-stu-id="0c22e-296">On-demand jobs are disabled.</span></span>  <span data-ttu-id="0c22e-297">To run an on-demand job:</span><span class="sxs-lookup"><span data-stu-id="0c22e-297">To run an on-demand job:</span></span>

1. <span data-ttu-id="0c22e-298">Select the job you wish to run.</span><span class="sxs-lookup"><span data-stu-id="0c22e-298">Select the job you wish to run.</span></span>
2. <span data-ttu-id="0c22e-299">If necessary, click **Enable** to enable the job.</span><span class="sxs-lookup"><span data-stu-id="0c22e-299">If necessary, click **Enable** to enable the job.</span></span>
3. <span data-ttu-id="0c22e-300">Click **Settings**, then **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="0c22e-300">Click **Settings**, then **Schedule**.</span></span>
4. <span data-ttu-id="0c22e-301">Select a Recurrence of **Once**, then Click **Save**</span><span class="sxs-lookup"><span data-stu-id="0c22e-301">Select a Recurrence of **Once**, then Click **Save**</span></span>

<span data-ttu-id="0c22e-302">Your on-demand jobs are located in `App_Data/config/scripts/scheduler post-migration`.</span><span class="sxs-lookup"><span data-stu-id="0c22e-302">Your on-demand jobs are located in `App_Data/config/scripts/scheduler post-migration`.</span></span>  <span data-ttu-id="0c22e-303">We recommend that you convert all on-demand jobs to [WebJobs] or [Functions].</span><span class="sxs-lookup"><span data-stu-id="0c22e-303">We recommend that you convert all on-demand jobs to [WebJobs] or [Functions].</span></span>  <span data-ttu-id="0c22e-304">Write new scheduler jobs as [WebJobs] or [Functions].</span><span class="sxs-lookup"><span data-stu-id="0c22e-304">Write new scheduler jobs as [WebJobs] or [Functions].</span></span>

### <a name="notification-hubs"></a><span data-ttu-id="0c22e-305">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="0c22e-305">Notification Hubs</span></span>
<span data-ttu-id="0c22e-306">Mobile Services uses Notification Hubs for push notifications.</span><span class="sxs-lookup"><span data-stu-id="0c22e-306">Mobile Services uses Notification Hubs for push notifications.</span></span>  <span data-ttu-id="0c22e-307">The following App Settings are used to link the Notification Hub to your Mobile Service after migration:</span><span class="sxs-lookup"><span data-stu-id="0c22e-307">The following App Settings are used to link the Notification Hub to your Mobile Service after migration:</span></span>

| <span data-ttu-id="0c22e-308">Application Setting</span><span class="sxs-lookup"><span data-stu-id="0c22e-308">Application Setting</span></span> | <span data-ttu-id="0c22e-309">Description</span><span class="sxs-lookup"><span data-stu-id="0c22e-309">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c22e-310">**MS\_PushEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="0c22e-310">**MS\_PushEntityNamespace**</span></span> |<span data-ttu-id="0c22e-311">The Notification Hub Namespace</span><span class="sxs-lookup"><span data-stu-id="0c22e-311">The Notification Hub Namespace</span></span> |
| <span data-ttu-id="0c22e-312">**MS\_NotificationHubName**</span><span class="sxs-lookup"><span data-stu-id="0c22e-312">**MS\_NotificationHubName**</span></span> |<span data-ttu-id="0c22e-313">The Notification Hub Name</span><span class="sxs-lookup"><span data-stu-id="0c22e-313">The Notification Hub Name</span></span> |
| <span data-ttu-id="0c22e-314">**MS\_NotificationHubConnectionString**</span><span class="sxs-lookup"><span data-stu-id="0c22e-314">**MS\_NotificationHubConnectionString**</span></span> |<span data-ttu-id="0c22e-315">The Notification Hub Connection String</span><span class="sxs-lookup"><span data-stu-id="0c22e-315">The Notification Hub Connection String</span></span> |
| <span data-ttu-id="0c22e-316">**MS\_NamespaceName**</span><span class="sxs-lookup"><span data-stu-id="0c22e-316">**MS\_NamespaceName**</span></span> |<span data-ttu-id="0c22e-317">An alias for MS_PushEntityNamespace</span><span class="sxs-lookup"><span data-stu-id="0c22e-317">An alias for MS_PushEntityNamespace</span></span> |

<span data-ttu-id="0c22e-318">Your Notification Hub is managed through the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-318">Your Notification Hub is managed through the [Azure portal].</span></span>  <span data-ttu-id="0c22e-319">Note the Notification Hub name (you can find this using the App Settings):</span><span class="sxs-lookup"><span data-stu-id="0c22e-319">Note the Notification Hub name (you can find this using the App Settings):</span></span>

1. <span data-ttu-id="0c22e-320">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-320">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-321">Select **Browse**>, then select **Notification Hubs**</span><span class="sxs-lookup"><span data-stu-id="0c22e-321">Select **Browse**>, then select **Notification Hubs**</span></span>
3. <span data-ttu-id="0c22e-322">Click the Notification Hub name associated with the mobile service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-322">Click the Notification Hub name associated with the mobile service.</span></span>

> [!NOTE]
> <span data-ttu-id="0c22e-323">If your Notification HUb is a "Mixed" type, it is not visible.</span><span class="sxs-lookup"><span data-stu-id="0c22e-323">If your Notification HUb is a "Mixed" type, it is not visible.</span></span>  <span data-ttu-id="0c22e-324">"Mixed" type notification hubs utilize both Notification Hubs and legacy Service Bus features.</span><span class="sxs-lookup"><span data-stu-id="0c22e-324">"Mixed" type notification hubs utilize both Notification Hubs and legacy Service Bus features.</span></span>  <span data-ttu-id="0c22e-325">[Convert your Mixed namespaces] before continuing.</span><span class="sxs-lookup"><span data-stu-id="0c22e-325">[Convert your Mixed namespaces] before continuing.</span></span>  <span data-ttu-id="0c22e-326">Once the conversion is complete, your notification hub appears in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-326">Once the conversion is complete, your notification hub appears in the [Azure portal].</span></span>
>
>

<span data-ttu-id="0c22e-327">For more information, review the [Notification Hubs] documentation.</span><span class="sxs-lookup"><span data-stu-id="0c22e-327">For more information, review the [Notification Hubs] documentation.</span></span>

> [!TIP]
> <span data-ttu-id="0c22e-328">Notification Hubs management features in the [Azure portal] are still in preview.</span><span class="sxs-lookup"><span data-stu-id="0c22e-328">Notification Hubs management features in the [Azure portal] are still in preview.</span></span>  <span data-ttu-id="0c22e-329">The [Azure Classic Portal] remains available for managing all your Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="0c22e-329">The [Azure Classic Portal] remains available for managing all your Notification Hubs.</span></span>
>
>

### <a name="legacy-push"></a><span data-ttu-id="0c22e-330">Legacy Push Settings</span><span class="sxs-lookup"><span data-stu-id="0c22e-330">Legacy Push Settings</span></span>
<span data-ttu-id="0c22e-331">If you configured Push on your mobile service before the introduction on Notification Hubs, you are using *legacy push*.</span><span class="sxs-lookup"><span data-stu-id="0c22e-331">If you configured Push on your mobile service before the introduction on Notification Hubs, you are using *legacy push*.</span></span>  <span data-ttu-id="0c22e-332">If you are using Push and you do not see a Notification Hub listed in your configuration, then it is likely you are using *legacy push*.</span><span class="sxs-lookup"><span data-stu-id="0c22e-332">If you are using Push and you do not see a Notification Hub listed in your configuration, then it is likely you are using *legacy push*.</span></span>  <span data-ttu-id="0c22e-333">This feature is migrated with all the other features.</span><span class="sxs-lookup"><span data-stu-id="0c22e-333">This feature is migrated with all the other features.</span></span>  <span data-ttu-id="0c22e-334">However, we recommend that you upgrade to Notification Hubs soon after the migration is complete.</span><span class="sxs-lookup"><span data-stu-id="0c22e-334">However, we recommend that you upgrade to Notification Hubs soon after the migration is complete.</span></span>

<span data-ttu-id="0c22e-335">In the interim, all the legacy push settings (with the notable exception of the APNS certificate) are available in App Settings.</span><span class="sxs-lookup"><span data-stu-id="0c22e-335">In the interim, all the legacy push settings (with the notable exception of the APNS certificate) are available in App Settings.</span></span>  <span data-ttu-id="0c22e-336">Update the APNS certificate by replacing the appropriate file on the filesystem.</span><span class="sxs-lookup"><span data-stu-id="0c22e-336">Update the APNS certificate by replacing the appropriate file on the filesystem.</span></span>

### <a name="app-settings"></a><span data-ttu-id="0c22e-337">Other App Settings</span><span class="sxs-lookup"><span data-stu-id="0c22e-337">Other App Settings</span></span>
<span data-ttu-id="0c22e-338">The following additional app settings are migrated from your Mobile Service and available under *Settings* > *App Settings*:</span><span class="sxs-lookup"><span data-stu-id="0c22e-338">The following additional app settings are migrated from your Mobile Service and available under *Settings* > *App Settings*:</span></span>

| <span data-ttu-id="0c22e-339">Application Setting</span><span class="sxs-lookup"><span data-stu-id="0c22e-339">Application Setting</span></span> | <span data-ttu-id="0c22e-340">Description</span><span class="sxs-lookup"><span data-stu-id="0c22e-340">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c22e-341">**MS\_MobileServiceName**</span><span class="sxs-lookup"><span data-stu-id="0c22e-341">**MS\_MobileServiceName**</span></span> |<span data-ttu-id="0c22e-342">The name of your app</span><span class="sxs-lookup"><span data-stu-id="0c22e-342">The name of your app</span></span> |
| <span data-ttu-id="0c22e-343">**MS\_MobileServiceDomainSuffix**</span><span class="sxs-lookup"><span data-stu-id="0c22e-343">**MS\_MobileServiceDomainSuffix**</span></span> |<span data-ttu-id="0c22e-344">The domain prefix.</span><span class="sxs-lookup"><span data-stu-id="0c22e-344">The domain prefix.</span></span> <span data-ttu-id="0c22e-345">i.e</span><span class="sxs-lookup"><span data-stu-id="0c22e-345">i.e</span></span> <span data-ttu-id="0c22e-346">azure-mobile.net</span><span class="sxs-lookup"><span data-stu-id="0c22e-346">azure-mobile.net</span></span> |
| <span data-ttu-id="0c22e-347">**MS\_ApplicationKey**</span><span class="sxs-lookup"><span data-stu-id="0c22e-347">**MS\_ApplicationKey**</span></span> |<span data-ttu-id="0c22e-348">Your application key</span><span class="sxs-lookup"><span data-stu-id="0c22e-348">Your application key</span></span> |
| <span data-ttu-id="0c22e-349">**MS\_MasterKey**</span><span class="sxs-lookup"><span data-stu-id="0c22e-349">**MS\_MasterKey**</span></span> |<span data-ttu-id="0c22e-350">Your app master key</span><span class="sxs-lookup"><span data-stu-id="0c22e-350">Your app master key</span></span> |

<span data-ttu-id="0c22e-351">The application key and master key are identical to the Application Keys from your original Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-351">The application key and master key are identical to the Application Keys from your original Mobile Service.</span></span>  <span data-ttu-id="0c22e-352">In particular, the Application Key is sent by mobile clients to validate their use of the mobile API.</span><span class="sxs-lookup"><span data-stu-id="0c22e-352">In particular, the Application Key is sent by mobile clients to validate their use of the mobile API.</span></span>

### <a name="cliequivalents"></a><span data-ttu-id="0c22e-353">Command-Line Equivalents</span><span class="sxs-lookup"><span data-stu-id="0c22e-353">Command-Line Equivalents</span></span>
<span data-ttu-id="0c22e-354">You can longer use the *azure mobile* command to manage your Azure Mobile Services site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-354">You can longer use the *azure mobile* command to manage your Azure Mobile Services site.</span></span>  <span data-ttu-id="0c22e-355">Instead, many functions have been replaced with the *azure site* command.</span><span class="sxs-lookup"><span data-stu-id="0c22e-355">Instead, many functions have been replaced with the *azure site* command.</span></span>  <span data-ttu-id="0c22e-356">Use the following table to find equivalents for common commands:</span><span class="sxs-lookup"><span data-stu-id="0c22e-356">Use the following table to find equivalents for common commands:</span></span>

| <span data-ttu-id="0c22e-357">*Azure Mobile* Command</span><span class="sxs-lookup"><span data-stu-id="0c22e-357">*Azure Mobile* Command</span></span> | <span data-ttu-id="0c22e-358">Equivalent *Azure Site* command</span><span class="sxs-lookup"><span data-stu-id="0c22e-358">Equivalent *Azure Site* command</span></span> |
|:--- |:--- |
| <span data-ttu-id="0c22e-359">mobile locations</span><span class="sxs-lookup"><span data-stu-id="0c22e-359">mobile locations</span></span> |<span data-ttu-id="0c22e-360">site location list</span><span class="sxs-lookup"><span data-stu-id="0c22e-360">site location list</span></span> |
| <span data-ttu-id="0c22e-361">mobile list</span><span class="sxs-lookup"><span data-stu-id="0c22e-361">mobile list</span></span> |<span data-ttu-id="0c22e-362">site list</span><span class="sxs-lookup"><span data-stu-id="0c22e-362">site list</span></span> |
| <span data-ttu-id="0c22e-363">mobile show *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-363">mobile show *name*</span></span> |<span data-ttu-id="0c22e-364">site show *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-364">site show *name*</span></span> |
| <span data-ttu-id="0c22e-365">mobile restart *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-365">mobile restart *name*</span></span> |<span data-ttu-id="0c22e-366">site restart *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-366">site restart *name*</span></span> |
| <span data-ttu-id="0c22e-367">mobile redeploy *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-367">mobile redeploy *name*</span></span> |<span data-ttu-id="0c22e-368">site deployment redeploy *commitId* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-368">site deployment redeploy *commitId* *name*</span></span> |
| <span data-ttu-id="0c22e-369">mobile key set *name* *type* *value*</span><span class="sxs-lookup"><span data-stu-id="0c22e-369">mobile key set *name* *type* *value*</span></span> |<span data-ttu-id="0c22e-370">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-370">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="0c22e-371">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-371">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="0c22e-372">mobile config list *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-372">mobile config list *name*</span></span> |<span data-ttu-id="0c22e-373">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-373">site appsetting list *name*</span></span> |
| <span data-ttu-id="0c22e-374">mobile config get *name* *key*</span><span class="sxs-lookup"><span data-stu-id="0c22e-374">mobile config get *name* *key*</span></span> |<span data-ttu-id="0c22e-375">site appsetting show *key* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-375">site appsetting show *key* *name*</span></span> |
| <span data-ttu-id="0c22e-376">mobile config set *name* *key*</span><span class="sxs-lookup"><span data-stu-id="0c22e-376">mobile config set *name* *key*</span></span> |<span data-ttu-id="0c22e-377">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-377">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="0c22e-378">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-378">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="0c22e-379">mobile domain list *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-379">mobile domain list *name*</span></span> |<span data-ttu-id="0c22e-380">site domain list *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-380">site domain list *name*</span></span> |
| <span data-ttu-id="0c22e-381">mobile domain add *name* *domain*</span><span class="sxs-lookup"><span data-stu-id="0c22e-381">mobile domain add *name* *domain*</span></span> |<span data-ttu-id="0c22e-382">site domain add *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-382">site domain add *domain* *name*</span></span> |
| <span data-ttu-id="0c22e-383">mobile domain delete *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-383">mobile domain delete *name*</span></span> |<span data-ttu-id="0c22e-384">site domain delete *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-384">site domain delete *domain* *name*</span></span> |
| <span data-ttu-id="0c22e-385">mobile scale show *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-385">mobile scale show *name*</span></span> |<span data-ttu-id="0c22e-386">site show *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-386">site show *name*</span></span> |
| <span data-ttu-id="0c22e-387">mobile scale change *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-387">mobile scale change *name*</span></span> |<span data-ttu-id="0c22e-388">site scale mode *mode* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-388">site scale mode *mode* *name*</span></span> <br /> <span data-ttu-id="0c22e-389">site scale instances *instances* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-389">site scale instances *instances* *name*</span></span> |
| <span data-ttu-id="0c22e-390">mobile appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-390">mobile appsetting list *name*</span></span> |<span data-ttu-id="0c22e-391">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-391">site appsetting list *name*</span></span> |
| <span data-ttu-id="0c22e-392">mobile appsetting add *name* *key* *value*</span><span class="sxs-lookup"><span data-stu-id="0c22e-392">mobile appsetting add *name* *key* *value*</span></span> |<span data-ttu-id="0c22e-393">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-393">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="0c22e-394">mobile appsetting delete *name* *key*</span><span class="sxs-lookup"><span data-stu-id="0c22e-394">mobile appsetting delete *name* *key*</span></span> |<span data-ttu-id="0c22e-395">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-395">site appsetting delete *key* *name*</span></span> |
| <span data-ttu-id="0c22e-396">mobile appsetting show *name* *key*</span><span class="sxs-lookup"><span data-stu-id="0c22e-396">mobile appsetting show *name* *key*</span></span> |<span data-ttu-id="0c22e-397">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="0c22e-397">site appsetting delete *key* *name*</span></span> |

<span data-ttu-id="0c22e-398">Update authentication or push notification settings by updating the appropriate Application Setting.</span><span class="sxs-lookup"><span data-stu-id="0c22e-398">Update authentication or push notification settings by updating the appropriate Application Setting.</span></span>
<span data-ttu-id="0c22e-399">Edit files and publish your site via ftp or git.</span><span class="sxs-lookup"><span data-stu-id="0c22e-399">Edit files and publish your site via ftp or git.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="0c22e-400">Diagnostics and Logging</span><span class="sxs-lookup"><span data-stu-id="0c22e-400">Diagnostics and Logging</span></span>
<span data-ttu-id="0c22e-401">Diagnostic Logging is normally disabled in an Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-401">Diagnostic Logging is normally disabled in an Azure App Service.</span></span>  <span data-ttu-id="0c22e-402">To enable diagnostic logging:</span><span class="sxs-lookup"><span data-stu-id="0c22e-402">To enable diagnostic logging:</span></span>

1. <span data-ttu-id="0c22e-403">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-403">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-404">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-404">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-405">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="0c22e-405">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="0c22e-406">Select **Diagnostic Logs** under the FEATURES menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-406">Select **Diagnostic Logs** under the FEATURES menu.</span></span>
5. <span data-ttu-id="0c22e-407">Click **ON** for the following logs: **Application Logging (Filesystem)**, **Detailed error messages**, and **Failed request tracing**</span><span class="sxs-lookup"><span data-stu-id="0c22e-407">Click **ON** for the following logs: **Application Logging (Filesystem)**, **Detailed error messages**, and **Failed request tracing**</span></span>
6. <span data-ttu-id="0c22e-408">Click **File System** for Web server logging</span><span class="sxs-lookup"><span data-stu-id="0c22e-408">Click **File System** for Web server logging</span></span>
7. <span data-ttu-id="0c22e-409">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="0c22e-409">Click **Save**</span></span>

<span data-ttu-id="0c22e-410">To view the logs:</span><span class="sxs-lookup"><span data-stu-id="0c22e-410">To view the logs:</span></span>

1. <span data-ttu-id="0c22e-411">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0c22e-411">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="0c22e-412">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-412">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="0c22e-413">Click the **Tools** button</span><span class="sxs-lookup"><span data-stu-id="0c22e-413">Click the **Tools** button</span></span>
4. <span data-ttu-id="0c22e-414">Select **Log Stream** under the OBSERVE menu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-414">Select **Log Stream** under the OBSERVE menu.</span></span>

<span data-ttu-id="0c22e-415">Logs are displayed in the window as they are generated.</span><span class="sxs-lookup"><span data-stu-id="0c22e-415">Logs are displayed in the window as they are generated.</span></span>  <span data-ttu-id="0c22e-416">You can also download the logs for later analysis using your deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="0c22e-416">You can also download the logs for later analysis using your deployment credentials.</span></span> <span data-ttu-id="0c22e-417">For more information, see the [Logging] documentation.</span><span class="sxs-lookup"><span data-stu-id="0c22e-417">For more information, see the [Logging] documentation.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0c22e-418">Known Issues</span><span class="sxs-lookup"><span data-stu-id="0c22e-418">Known Issues</span></span>
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a><span data-ttu-id="0c22e-419">Deleting a Migrated Mobile App Clone causes a site outage</span><span class="sxs-lookup"><span data-stu-id="0c22e-419">Deleting a Migrated Mobile App Clone causes a site outage</span></span>
<span data-ttu-id="0c22e-420">If you clone your migrated mobile service using Azure PowerShell, then delete the clone, the DNS entry for your production service is removed.</span><span class="sxs-lookup"><span data-stu-id="0c22e-420">If you clone your migrated mobile service using Azure PowerShell, then delete the clone, the DNS entry for your production service is removed.</span></span>  <span data-ttu-id="0c22e-421">Your site is no longer be accessible from the Internet.</span><span class="sxs-lookup"><span data-stu-id="0c22e-421">Your site is no longer be accessible from the Internet.</span></span>  

<span data-ttu-id="0c22e-422">Resolution: If you wish to clone your site, do so through the portal.</span><span class="sxs-lookup"><span data-stu-id="0c22e-422">Resolution: If you wish to clone your site, do so through the portal.</span></span>

### <a name="changing-webconfig-does-not-work"></a><span data-ttu-id="0c22e-423">Changing Web.config does not work</span><span class="sxs-lookup"><span data-stu-id="0c22e-423">Changing Web.config does not work</span></span>
<span data-ttu-id="0c22e-424">If you have an ASP.NET site, changes to the `Web.config` file do not get applied.</span><span class="sxs-lookup"><span data-stu-id="0c22e-424">If you have an ASP.NET site, changes to the `Web.config` file do not get applied.</span></span>  <span data-ttu-id="0c22e-425">The Azure App Service builds a suitable `Web.config` file during startup to support the Mobile Services runtime.</span><span class="sxs-lookup"><span data-stu-id="0c22e-425">The Azure App Service builds a suitable `Web.config` file during startup to support the Mobile Services runtime.</span></span>  <span data-ttu-id="0c22e-426">You can override certain settings (such as custom headers) by using an XML transform file.</span><span class="sxs-lookup"><span data-stu-id="0c22e-426">You can override certain settings (such as custom headers) by using an XML transform file.</span></span>  <span data-ttu-id="0c22e-427">Create a file in called `applicationHost.xdt` - this file must end up in the `D:\home\site` directory on the Azure Service.</span><span class="sxs-lookup"><span data-stu-id="0c22e-427">Create a file in called `applicationHost.xdt` - this file must end up in the `D:\home\site` directory on the Azure Service.</span></span>  <span data-ttu-id="0c22e-428">Upload the `applicationHost.xdt` file via a custom deployment script or directly using Kudu.</span><span class="sxs-lookup"><span data-stu-id="0c22e-428">Upload the `applicationHost.xdt` file via a custom deployment script or directly using Kudu.</span></span>  <span data-ttu-id="0c22e-429">The following shows an example document:</span><span class="sxs-lookup"><span data-stu-id="0c22e-429">The following shows an example document:</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

<span data-ttu-id="0c22e-430">For more information, see the [XDT Transform Samples] documentation on GitHub.</span><span class="sxs-lookup"><span data-stu-id="0c22e-430">For more information, see the [XDT Transform Samples] documentation on GitHub.</span></span>

### <a name="migrated-mobile-services-cannot-be-added-to-traffic-manager"></a><span data-ttu-id="0c22e-431">Migrated Mobile Services cannot be added to Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0c22e-431">Migrated Mobile Services cannot be added to Traffic Manager</span></span>
<span data-ttu-id="0c22e-432">When you create a Traffic Manager profile, you cannot directly choose a migrated mobile service to the profile.</span><span class="sxs-lookup"><span data-stu-id="0c22e-432">When you create a Traffic Manager profile, you cannot directly choose a migrated mobile service to the profile.</span></span>  <span data-ttu-id="0c22e-433">Use an "external endpoint."</span><span class="sxs-lookup"><span data-stu-id="0c22e-433">Use an "external endpoint."</span></span>  <span data-ttu-id="0c22e-434">The external endpoint can only be added through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c22e-434">The external endpoint can only be added through PowerShell.</span></span>  <span data-ttu-id="0c22e-435">For more information, see the [Traffic Manager tutorial](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).</span><span class="sxs-lookup"><span data-stu-id="0c22e-435">For more information, see the [Traffic Manager tutorial](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c22e-436">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0c22e-436">Next Steps</span></span>
<span data-ttu-id="0c22e-437">Now that your application is migrated to App Service, there are even more features you can use:</span><span class="sxs-lookup"><span data-stu-id="0c22e-437">Now that your application is migrated to App Service, there are even more features you can use:</span></span>

* <span data-ttu-id="0c22e-438">Deployment [staging slots] allow you to stage changes to your site and perform A/B testing.</span><span class="sxs-lookup"><span data-stu-id="0c22e-438">Deployment [staging slots] allow you to stage changes to your site and perform A/B testing.</span></span>
* <span data-ttu-id="0c22e-439">[WebJobs] provide a replacement for On-demand scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="0c22e-439">[WebJobs] provide a replacement for On-demand scheduled jobs.</span></span>
* <span data-ttu-id="0c22e-440">You can [continuously deploy] your site by linking your site to GitHub, TFS, or Mercurial.</span><span class="sxs-lookup"><span data-stu-id="0c22e-440">You can [continuously deploy] your site by linking your site to GitHub, TFS, or Mercurial.</span></span>
* <span data-ttu-id="0c22e-441">You can use [Application Insights] to monitor your site.</span><span class="sxs-lookup"><span data-stu-id="0c22e-441">You can use [Application Insights] to monitor your site.</span></span>
* <span data-ttu-id="0c22e-442">Serve a website and a Mobile API from the same code.</span><span class="sxs-lookup"><span data-stu-id="0c22e-442">Serve a website and a Mobile API from the same code.</span></span>

### <a name="upgrading-your-site"></a><span data-ttu-id="0c22e-443">Upgrading your Mobile Services site to Azure Mobile Apps SDK</span><span class="sxs-lookup"><span data-stu-id="0c22e-443">Upgrading your Mobile Services site to Azure Mobile Apps SDK</span></span>
* <span data-ttu-id="0c22e-444">For Node.js-based server projects, the new [Mobile Apps Node.js SDK] provides several new features.</span><span class="sxs-lookup"><span data-stu-id="0c22e-444">For Node.js-based server projects, the new [Mobile Apps Node.js SDK] provides several new features.</span></span> <span data-ttu-id="0c22e-445">For instance, you can now do local development and debugging, use any Node.js version above 0.10, and customize with any Express.js middleware.</span><span class="sxs-lookup"><span data-stu-id="0c22e-445">For instance, you can now do local development and debugging, use any Node.js version above 0.10, and customize with any Express.js middleware.</span></span>
* <span data-ttu-id="0c22e-446">For .NET-based server projects, the new [Mobile Apps SDK NuGet packages](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) have more flexibility on NuGet dependencies.</span><span class="sxs-lookup"><span data-stu-id="0c22e-446">For .NET-based server projects, the new [Mobile Apps SDK NuGet packages](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) have more flexibility on NuGet dependencies.</span></span>  <span data-ttu-id="0c22e-447">These packages support the new App Service authentication, and compose with any ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="0c22e-447">These packages support the new App Service authentication, and compose with any ASP.NET project.</span></span> <span data-ttu-id="0c22e-448">To learn more about upgrading, see [Upgrade your existing .NET Mobile Service to App Service](app-service-mobile-net-upgrading-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="0c22e-448">To learn more about upgrading, see [Upgrade your existing .NET Mobile Service to App Service](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[App Service pricing]: https://azure.microsoft.com/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Auto-scale]: ../app-service/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-web-overview.md
[Azure Classic Portal]: https://manage.windowsazure.com
[Azure portal]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/regions/
[Azure Scheduler Plans]: ../scheduler/scheduler-plans-billing.md
[continuously deploy]: ../app-service/app-service-continuous-deployment.md
[Convert your Mixed namespaces]: https://azure.microsoft.com/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[custom domain names]: ../app-service/app-service-web-tutorial-custom-domain.md
[Fiddler]: http://www.telerik.com/fiddler
[general availability of Azure App Service]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[Hybrid Connections]: ../app-service/app-service-hybrid-connections.md
[Logging]: ../app-service/web-sites-enable-diagnostic-log.md
[Mobile Apps Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[Mobile Services vs. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[Notification Hubs]: ../notification-hubs/notification-hubs-push-notification-overview.md
[performance monitoring]: ../app-service/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[staging slots]: ../app-service/web-sites-staged-publishing.md
[VNet]: ../app-service/web-sites-integrate-with-vnet.md
[XDT Transform Samples]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[Functions]: ../azure-functions/functions-overview.md
