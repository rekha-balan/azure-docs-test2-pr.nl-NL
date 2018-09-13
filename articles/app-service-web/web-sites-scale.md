---
title: Scale up an app in Azure | Microsoft Docs
description: Learn how to scale up an app in Azure App Service to add capacity and features.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: bc81caa2784e6b0b27905a78717d268c100154ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553213"
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="70ce2-103">Scale up an app in Azure</span><span class="sxs-lookup"><span data-stu-id="70ce2-103">Scale up an app in Azure</span></span>
<span data-ttu-id="70ce2-104">This article shows you how to scale your app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="70ce2-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="70ce2-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span><span class="sxs-lookup"><span data-stu-id="70ce2-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="70ce2-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span><span class="sxs-lookup"><span data-stu-id="70ce2-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="70ce2-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span><span class="sxs-lookup"><span data-stu-id="70ce2-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="70ce2-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span><span class="sxs-lookup"><span data-stu-id="70ce2-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="70ce2-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span><span class="sxs-lookup"><span data-stu-id="70ce2-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="70ce2-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span><span class="sxs-lookup"><span data-stu-id="70ce2-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="70ce2-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="70ce2-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="70ce2-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span><span class="sxs-lookup"><span data-stu-id="70ce2-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="70ce2-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70ce2-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="70ce2-114">They do not require you to change your code or redeploy your application.</span><span class="sxs-lookup"><span data-stu-id="70ce2-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="70ce2-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="70ce2-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="70ce2-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="70ce2-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="70ce2-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="70ce2-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="70ce2-118">Scale up your pricing tier</span><span class="sxs-lookup"><span data-stu-id="70ce2-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="70ce2-119">In your browser, open the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="70ce2-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="70ce2-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span><span class="sxs-lookup"><span data-stu-id="70ce2-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navigate to scale up your Azure app.][ChooseWHP]
3. <span data-ttu-id="70ce2-122">Choose your tier, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="70ce2-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="70ce2-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="70ce2-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="70ce2-124">Scale related resources</span><span class="sxs-lookup"><span data-stu-id="70ce2-124">Scale related resources</span></span>
<span data-ttu-id="70ce2-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span><span class="sxs-lookup"><span data-stu-id="70ce2-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="70ce2-126">These resources are not scaled with the App Service plan and must be scaled separately.</span><span class="sxs-lookup"><span data-stu-id="70ce2-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="70ce2-127">In **Essentials**, click the **Resource group** link.</span><span class="sxs-lookup"><span data-stu-id="70ce2-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Scale up your Azure app's related resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="70ce2-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span><span class="sxs-lookup"><span data-stu-id="70ce2-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="70ce2-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span><span class="sxs-lookup"><span data-stu-id="70ce2-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navigate to resource group blade to scale up your Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="70ce2-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span><span class="sxs-lookup"><span data-stu-id="70ce2-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Scale up the SQL Database backend for your Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="70ce2-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="70ce2-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="70ce2-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span><span class="sxs-lookup"><span data-stu-id="70ce2-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Scale up the Azure Storage account used by your Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="70ce2-137">Learn about developer features</span><span class="sxs-lookup"><span data-stu-id="70ce2-137">Learn about developer features</span></span>
<span data-ttu-id="70ce2-138">Depending on the pricing tier, the following developer-oriented features are available:</span><span class="sxs-lookup"><span data-stu-id="70ce2-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="70ce2-139">Bitness</span><span class="sxs-lookup"><span data-stu-id="70ce2-139">Bitness</span></span>
* <span data-ttu-id="70ce2-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span><span class="sxs-lookup"><span data-stu-id="70ce2-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="70ce2-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span><span class="sxs-lookup"><span data-stu-id="70ce2-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="70ce2-142">Debugger support</span><span class="sxs-lookup"><span data-stu-id="70ce2-142">Debugger support</span></span>
* <span data-ttu-id="70ce2-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span><span class="sxs-lookup"><span data-stu-id="70ce2-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="70ce2-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span><span class="sxs-lookup"><span data-stu-id="70ce2-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="70ce2-145">Learn about other features</span><span class="sxs-lookup"><span data-stu-id="70ce2-145">Learn about other features</span></span>
* <span data-ttu-id="70ce2-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="70ce2-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="70ce2-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="70ce2-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="70ce2-148">No credit cards are required and there are no commitments.</span><span class="sxs-lookup"><span data-stu-id="70ce2-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="70ce2-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="70ce2-149">Next steps</span></span>
* <span data-ttu-id="70ce2-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70ce2-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="70ce2-151">For information about pricing, support, and SLA, visit the following links.</span><span class="sxs-lookup"><span data-stu-id="70ce2-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="70ce2-152">Data Transfers Pricing Details</span><span class="sxs-lookup"><span data-stu-id="70ce2-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="70ce2-153">Microsoft Azure Support Plans</span><span class="sxs-lookup"><span data-stu-id="70ce2-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="70ce2-154">Service Level Agreements</span><span class="sxs-lookup"><span data-stu-id="70ce2-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="70ce2-155">SQL Database Pricing Details</span><span class="sxs-lookup"><span data-stu-id="70ce2-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="70ce2-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="70ce2-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="70ce2-157">App Service Pricing Details</span><span class="sxs-lookup"><span data-stu-id="70ce2-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="70ce2-158">App Service Pricing Details - SSL Connections</span><span class="sxs-lookup"><span data-stu-id="70ce2-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="70ce2-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="70ce2-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="70ce2-160">For videos about scaling App Service apps, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="70ce2-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="70ce2-161">When to Scale Azure Websites - with Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="70ce2-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="70ce2-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="70ce2-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="70ce2-163">How Azure Websites Scale - with Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="70ce2-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/scale12SQLGeoReplication.png








