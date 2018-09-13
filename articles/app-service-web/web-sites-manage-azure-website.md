---
title: Manage a web app in Azure App Service
description: Links to resources for managing a web app in Azure App Service.
services: app-service\web
documentationcenter: ''
author: erikre
manager: erikre
editor: ''
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: b5d00cf094a813c7a14a3fd5b4a5d73b5e2de49e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563690"
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="c906b-103">Manage a web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c906b-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="c906b-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c906b-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c906b-105">Management includes all of the tasks that keep your web app running smoothly.</span><span class="sxs-lookup"><span data-stu-id="c906b-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="c906b-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span><span class="sxs-lookup"><span data-stu-id="c906b-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="c906b-107">Many web app management tasks can be performed in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c906b-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="c906b-108">Before you deploy your web app to production</span><span class="sxs-lookup"><span data-stu-id="c906b-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="c906b-109">Choose a tier</span><span class="sxs-lookup"><span data-stu-id="c906b-109">Choose a tier</span></span>
<span data-ttu-id="c906b-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span><span class="sxs-lookup"><span data-stu-id="c906b-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="c906b-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="c906b-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="c906b-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span><span class="sxs-lookup"><span data-stu-id="c906b-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="c906b-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span><span class="sxs-lookup"><span data-stu-id="c906b-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="c906b-114">Configuration</span><span class="sxs-lookup"><span data-stu-id="c906b-114">Configuration</span></span>
<span data-ttu-id="c906b-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span><span class="sxs-lookup"><span data-stu-id="c906b-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="c906b-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="c906b-117">Here is a quick checklist:</span><span class="sxs-lookup"><span data-stu-id="c906b-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="c906b-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span><span class="sxs-lookup"><span data-stu-id="c906b-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="c906b-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span><span class="sxs-lookup"><span data-stu-id="c906b-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="c906b-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="c906b-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="c906b-121">Are you running continuous web jobs?</span><span class="sxs-lookup"><span data-stu-id="c906b-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="c906b-122">If so, enable **Always On**.</span><span class="sxs-lookup"><span data-stu-id="c906b-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="c906b-123">Set the **default document**, such as index.html.</span><span class="sxs-lookup"><span data-stu-id="c906b-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="c906b-124">In addition to these basic configuration settings, you may want to configure the following:</span><span class="sxs-lookup"><span data-stu-id="c906b-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="c906b-125">**Secure Socket Layer (SSL)** encryption.</span><span class="sxs-lookup"><span data-stu-id="c906b-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="c906b-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span><span class="sxs-lookup"><span data-stu-id="c906b-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="c906b-127">See [Enable HTTPS for a web app in Azure App Service](web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-127">See [Enable HTTPS for a web app in Azure App Service](web-sites-configure-ssl-certificate.md).</span></span>
* <span data-ttu-id="c906b-128">**Custom domain name.**</span><span class="sxs-lookup"><span data-stu-id="c906b-128">**Custom domain name.**</span></span> <span data-ttu-id="c906b-129">Your web app automatically has a subdomain under azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c906b-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="c906b-130">You can associate a custom domain name, such as contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c906b-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="c906b-131">See [Configure a custom domain name in Azure App Service](web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-131">See [Configure a custom domain name in Azure App Service](web-sites-custom-domain-name.md).</span></span>

<span data-ttu-id="c906b-132">Language-specific configuration:</span><span class="sxs-lookup"><span data-stu-id="c906b-132">Language-specific configuration:</span></span>

* <span data-ttu-id="c906b-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="c906b-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="c906b-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="c906b-135">While your web app is running</span><span class="sxs-lookup"><span data-stu-id="c906b-135">While your web app is running</span></span>
<span data-ttu-id="c906b-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span><span class="sxs-lookup"><span data-stu-id="c906b-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="c906b-137">You may also need to troubleshoot errors.</span><span class="sxs-lookup"><span data-stu-id="c906b-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="c906b-138">Monitoring</span><span class="sxs-lookup"><span data-stu-id="c906b-138">Monitoring</span></span>
* <span data-ttu-id="c906b-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span><span class="sxs-lookup"><span data-stu-id="c906b-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="c906b-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span><span class="sxs-lookup"><span data-stu-id="c906b-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="c906b-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span><span class="sxs-lookup"><span data-stu-id="c906b-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="c906b-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span><span class="sxs-lookup"><span data-stu-id="c906b-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="c906b-143">Backups</span><span class="sxs-lookup"><span data-stu-id="c906b-143">Backups</span></span>
* <span data-ttu-id="c906b-144">Set [automatic backups](web-sites-backup.md) of your web app.</span><span class="sxs-lookup"><span data-stu-id="c906b-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="c906b-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="c906b-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="c906b-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c906b-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="c906b-147">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c906b-147">Troubleshooting</span></span>
* <span data-ttu-id="c906b-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c906b-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="c906b-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="c906b-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="c906b-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="c906b-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="c906b-152">Restoring Data</span><span class="sxs-lookup"><span data-stu-id="c906b-152">Restoring Data</span></span>
* <span data-ttu-id="c906b-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span><span class="sxs-lookup"><span data-stu-id="c906b-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="c906b-154">When you update your web app</span><span class="sxs-lookup"><span data-stu-id="c906b-154">When you update your web app</span></span>
<span data-ttu-id="c906b-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="c906b-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c906b-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="c906b-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span><span class="sxs-lookup"><span data-stu-id="c906b-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 

<span data-ttu-id="c906b-158">If you use Visual Studio Team Services, you can set up continuous deployment from source control:</span><span class="sxs-lookup"><span data-stu-id="c906b-158">If you use Visual Studio Team Services, you can set up continuous deployment from source control:</span></span>

* [<span data-ttu-id="c906b-159">Using Team Foundation Version Control (TFVC)</span><span class="sxs-lookup"><span data-stu-id="c906b-159">Using Team Foundation Version Control (TFVC)</span></span>](../cloud-services/cloud-services-continuous-delivery-use-vso.md) 
* [<span data-ttu-id="c906b-160">Using Git</span><span class="sxs-lookup"><span data-stu-id="c906b-160">Using Git</span></span>](../cloud-services/cloud-services-continuous-delivery-use-vso-git.md)

<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


