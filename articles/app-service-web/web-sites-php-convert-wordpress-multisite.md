---
title: Convert WordPress to Multisite in Azure App Service
description: Learn how to take an existing WordPress web app created through the gallery in Azure and convert it to WordPress Multisite
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: dc884e9457968b3a7c2434bb626c677f746e7301
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661806"
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="ac485-103">Convert WordPress to Multisite in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ac485-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="ac485-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ac485-104">Overview</span></span>
<span data-ttu-id="ac485-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="ac485-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="ac485-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span><span class="sxs-lookup"><span data-stu-id="ac485-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="ac485-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span><span class="sxs-lookup"><span data-stu-id="ac485-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="ac485-108">It is assumed that you have an existing installation of WordPress.</span><span class="sxs-lookup"><span data-stu-id="ac485-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="ac485-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="ac485-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="ac485-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="ac485-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="ac485-111">Let's get started.</span><span class="sxs-lookup"><span data-stu-id="ac485-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="ac485-112">Allow Multisite</span><span class="sxs-lookup"><span data-stu-id="ac485-112">Allow Multisite</span></span>
<span data-ttu-id="ac485-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span><span class="sxs-lookup"><span data-stu-id="ac485-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="ac485-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span><span class="sxs-lookup"><span data-stu-id="ac485-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="ac485-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="ac485-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="ac485-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="ac485-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="ac485-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="ac485-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="ac485-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span><span class="sxs-lookup"><span data-stu-id="ac485-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="ac485-119">Be sure to save the file and upload it back to the server!</span><span class="sxs-lookup"><span data-stu-id="ac485-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="ac485-120">Network Setup</span><span class="sxs-lookup"><span data-stu-id="ac485-120">Network Setup</span></span>
<span data-ttu-id="ac485-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span><span class="sxs-lookup"><span data-stu-id="ac485-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="ac485-122">Click **Network Setup** and fill in the details of your network.</span><span class="sxs-lookup"><span data-stu-id="ac485-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Network Setup Screen][wordpress-network-setup]

<span data-ttu-id="ac485-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="ac485-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="ac485-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span><span class="sxs-lookup"><span data-stu-id="ac485-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="ac485-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span><span class="sxs-lookup"><span data-stu-id="ac485-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="ac485-127">Enable the Network</span><span class="sxs-lookup"><span data-stu-id="ac485-127">Enable the Network</span></span>
<span data-ttu-id="ac485-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span><span class="sxs-lookup"><span data-stu-id="ac485-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="ac485-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span><span class="sxs-lookup"><span data-stu-id="ac485-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="ac485-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span><span class="sxs-lookup"><span data-stu-id="ac485-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="ac485-131">However, you should always check the files to ensure the updates were successful.</span><span class="sxs-lookup"><span data-stu-id="ac485-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="ac485-132">If not, this screen will present you with the necessary updates.</span><span class="sxs-lookup"><span data-stu-id="ac485-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="ac485-133">Edit and save the files.</span><span class="sxs-lookup"><span data-stu-id="ac485-133">Edit and save the files.</span></span>

<span data-ttu-id="ac485-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span><span class="sxs-lookup"><span data-stu-id="ac485-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="ac485-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span><span class="sxs-lookup"><span data-stu-id="ac485-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="ac485-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span><span class="sxs-lookup"><span data-stu-id="ac485-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="ac485-137">Adding custom domains</span><span class="sxs-lookup"><span data-stu-id="ac485-137">Adding custom domains</span></span>
<span data-ttu-id="ac485-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span><span class="sxs-lookup"><span data-stu-id="ac485-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="ac485-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span><span class="sxs-lookup"><span data-stu-id="ac485-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="ac485-140">Enable domain mapping to the web app</span><span class="sxs-lookup"><span data-stu-id="ac485-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="ac485-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ac485-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="ac485-142">You will need to switch to **Shared** or **Standard** mode.</span><span class="sxs-lookup"><span data-stu-id="ac485-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="ac485-143">To do this:</span><span class="sxs-lookup"><span data-stu-id="ac485-143">To do this:</span></span>

* <span data-ttu-id="ac485-144">Log in to the Azure Portal and locate your web app.</span><span class="sxs-lookup"><span data-stu-id="ac485-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="ac485-145">Click on the **Scale up** tab in **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ac485-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="ac485-146">Under **General**, select either *SHARED* or *STANDARD*</span><span class="sxs-lookup"><span data-stu-id="ac485-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="ac485-147">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="ac485-147">Click **Save**</span></span>

<span data-ttu-id="ac485-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span><span class="sxs-lookup"><span data-stu-id="ac485-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="ac485-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span><span class="sxs-lookup"><span data-stu-id="ac485-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="ac485-150">Verify your domain</span><span class="sxs-lookup"><span data-stu-id="ac485-150">Verify your domain</span></span>
<span data-ttu-id="ac485-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span><span class="sxs-lookup"><span data-stu-id="ac485-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="ac485-152">To do so, you must add a new CNAME record to your DNS entry.</span><span class="sxs-lookup"><span data-stu-id="ac485-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="ac485-153">Log in to your domain's DNS manager</span><span class="sxs-lookup"><span data-stu-id="ac485-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="ac485-154">Create a new CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="ac485-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="ac485-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="ac485-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="ac485-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span><span class="sxs-lookup"><span data-stu-id="ac485-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="ac485-157">Add the domain to the web app</span><span class="sxs-lookup"><span data-stu-id="ac485-157">Add the domain to the web app</span></span>
<span data-ttu-id="ac485-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span><span class="sxs-lookup"><span data-stu-id="ac485-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="ac485-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span><span class="sxs-lookup"><span data-stu-id="ac485-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="ac485-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span><span class="sxs-lookup"><span data-stu-id="ac485-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Manage custom domains dialog][wordpress-manage-domains]

<span data-ttu-id="ac485-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span><span class="sxs-lookup"><span data-stu-id="ac485-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="ac485-163">If the DNS has not fully propagated, a red indicator will show.</span><span class="sxs-lookup"><span data-stu-id="ac485-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="ac485-164">If it was successful, you will see a green checkmark.</span><span class="sxs-lookup"><span data-stu-id="ac485-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="ac485-165">Take note of the IP Address listed at the bottom of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ac485-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="ac485-166">You will need this to setup the A record for your domain.</span><span class="sxs-lookup"><span data-stu-id="ac485-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="ac485-167">Setup the domain A record</span><span class="sxs-lookup"><span data-stu-id="ac485-167">Setup the domain A record</span></span>
<span data-ttu-id="ac485-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span><span class="sxs-lookup"><span data-stu-id="ac485-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="ac485-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span><span class="sxs-lookup"><span data-stu-id="ac485-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="ac485-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ac485-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="ac485-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span><span class="sxs-lookup"><span data-stu-id="ac485-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="ac485-172">Install and setup the plugin</span><span class="sxs-lookup"><span data-stu-id="ac485-172">Install and setup the plugin</span></span>
<span data-ttu-id="ac485-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span><span class="sxs-lookup"><span data-stu-id="ac485-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="ac485-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span><span class="sxs-lookup"><span data-stu-id="ac485-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="ac485-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span><span class="sxs-lookup"><span data-stu-id="ac485-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="ac485-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span><span class="sxs-lookup"><span data-stu-id="ac485-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="ac485-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span><span class="sxs-lookup"><span data-stu-id="ac485-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="ac485-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ac485-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="ac485-179">Map the domain</span><span class="sxs-lookup"><span data-stu-id="ac485-179">Map the domain</span></span>
<span data-ttu-id="ac485-180">Visit the **Dashboard** for the site you wish to map the domain to.</span><span class="sxs-lookup"><span data-stu-id="ac485-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="ac485-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ac485-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="ac485-182">By default, the new domain will be rewritten to the autogenerated site domain.</span><span class="sxs-lookup"><span data-stu-id="ac485-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="ac485-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span><span class="sxs-lookup"><span data-stu-id="ac485-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="ac485-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span><span class="sxs-lookup"><span data-stu-id="ac485-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="ac485-185">Do it again</span><span class="sxs-lookup"><span data-stu-id="ac485-185">Do it again</span></span>
<span data-ttu-id="ac485-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span><span class="sxs-lookup"><span data-stu-id="ac485-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="ac485-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span><span class="sxs-lookup"><span data-stu-id="ac485-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="ac485-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="ac485-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ac485-189">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="ac485-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="ac485-190">What's changed</span><span class="sxs-lookup"><span data-stu-id="ac485-190">What's changed</span></span>
* <span data-ttu-id="ac485-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ac485-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png




