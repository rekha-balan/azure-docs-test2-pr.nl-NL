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
ms.openlocfilehash: 79450cdd0928304c3b98cf13f8aaca7a1bf11d33
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858046"
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="ac852-103">Scale up an app in Azure</span><span class="sxs-lookup"><span data-stu-id="ac852-103">Scale up an app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="ac852-104">The new **PremiumV2** tier gives you faster CPUs, SSD storage, and doubles the memory-to-core ratio of the existing pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="ac852-104">The new **PremiumV2** tier gives you faster CPUs, SSD storage, and doubles the memory-to-core ratio of the existing pricing tiers.</span></span> <span data-ttu-id="ac852-105">With the performance advantage, you could save money by running your apps on fewer instances.</span><span class="sxs-lookup"><span data-stu-id="ac852-105">With the performance advantage, you could save money by running your apps on fewer instances.</span></span> <span data-ttu-id="ac852-106">To scale up to **PremiumV2** tier, see [Configure PremiumV2 tier for App Service](app-service-configure-premium-tier.md).</span><span class="sxs-lookup"><span data-stu-id="ac852-106">To scale up to **PremiumV2** tier, see [Configure PremiumV2 tier for App Service](app-service-configure-premium-tier.md).</span></span>
>

<span data-ttu-id="ac852-107">This article shows you how to scale your app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ac852-107">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="ac852-108">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span><span class="sxs-lookup"><span data-stu-id="ac852-108">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="ac852-109">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span><span class="sxs-lookup"><span data-stu-id="ac852-109">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="ac852-110">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span><span class="sxs-lookup"><span data-stu-id="ac852-110">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="ac852-111">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span><span class="sxs-lookup"><span data-stu-id="ac852-111">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="ac852-112">You can scale out to as many as 20 instances, depending on your pricing tier.</span><span class="sxs-lookup"><span data-stu-id="ac852-112">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="ac852-113">[App Service Environments](environment/intro.md) in **Isolated** tier further increases your scale-out count to 100 instances.</span><span class="sxs-lookup"><span data-stu-id="ac852-113">[App Service Environments](environment/intro.md) in **Isolated** tier further increases your scale-out count to 100 instances.</span></span> <span data-ttu-id="ac852-114">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ac852-114">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="ac852-115">There, you find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span><span class="sxs-lookup"><span data-stu-id="ac852-115">There, you find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="ac852-116">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac852-116">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="ac852-117">They don't require you to change your code or redeploy your application.</span><span class="sxs-lookup"><span data-stu-id="ac852-117">They don't require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="ac852-118">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="ac852-118">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="ac852-119">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ac852-119">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="ac852-120">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="ac852-120">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="ac852-121">Scale up your pricing tier</span><span class="sxs-lookup"><span data-stu-id="ac852-121">Scale up your pricing tier</span></span>
1. <span data-ttu-id="ac852-122">In your browser, open the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="ac852-122">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="ac852-123">In your App Service app page, click **All settings**, and then click **Scale Up**.</span><span class="sxs-lookup"><span data-stu-id="ac852-123">In your App Service app page, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navigate to scale up your Azure app.][ChooseWHP]
3. <span data-ttu-id="ac852-125">Choose your tier, and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ac852-125">Choose your tier, and then click **Apply**.</span></span>
   
    <span data-ttu-id="ac852-126">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="ac852-126">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="ac852-127">Scale related resources</span><span class="sxs-lookup"><span data-stu-id="ac852-127">Scale related resources</span></span>
<span data-ttu-id="ac852-128">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can scale up these resources separately.</span><span class="sxs-lookup"><span data-stu-id="ac852-128">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can scale up these resources separately.</span></span> <span data-ttu-id="ac852-129">These resources aren't managed by the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="ac852-129">These resources aren't managed by the App Service plan.</span></span>

1. <span data-ttu-id="ac852-130">In **Essentials**, click the **Resource group** link.</span><span class="sxs-lookup"><span data-stu-id="ac852-130">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Scale up your Azure app's related resources](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="ac852-132">In the **Summary** part of the **Resource group** page, click a resource that you want to scale.</span><span class="sxs-lookup"><span data-stu-id="ac852-132">In the **Summary** part of the **Resource group** page, click a resource that you want to scale.</span></span> <span data-ttu-id="ac852-133">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span><span class="sxs-lookup"><span data-stu-id="ac852-133">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navigate to resource group page to scale up your Azure app](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="ac852-135">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span><span class="sxs-lookup"><span data-stu-id="ac852-135">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Scale up the SQL Database backend for your Azure app](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="ac852-137">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="ac852-137">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="ac852-138">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span><span class="sxs-lookup"><span data-stu-id="ac852-138">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Scale up the Azure Storage account used by your Azure app](./media/web-sites-scale/ScaleStorage.png)

<a name="OtherFeatures"></a>
<a name="devfeatures"></a>

## <a name="compare-pricing-tiers"></a><span data-ttu-id="ac852-140">Compare pricing tiers</span><span class="sxs-lookup"><span data-stu-id="ac852-140">Compare pricing tiers</span></span>
<span data-ttu-id="ac852-141">For detailed information, such as VM sizes for each pricing tier, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="ac852-141">For detailed information, such as VM sizes for each pricing tier, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>
<span data-ttu-id="ac852-142">For a table of service limits, quotas, and constraints, and supported features in each tier, see [App Service limits](../azure-subscription-service-limits.md#app-service-limits).</span><span class="sxs-lookup"><span data-stu-id="ac852-142">For a table of service limits, quotas, and constraints, and supported features in each tier, see [App Service limits](../azure-subscription-service-limits.md#app-service-limits).</span></span>

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="ac852-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac852-143">Next steps</span></span>
* <span data-ttu-id="ac852-144">For information about pricing, support, and SLA, visit the following links:</span><span class="sxs-lookup"><span data-stu-id="ac852-144">For information about pricing, support, and SLA, visit the following links:</span></span>
  
    [<span data-ttu-id="ac852-145">Data Transfers Pricing Details</span><span class="sxs-lookup"><span data-stu-id="ac852-145">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="ac852-146">Microsoft Azure Support Plans</span><span class="sxs-lookup"><span data-stu-id="ac852-146">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="ac852-147">Service Level Agreements</span><span class="sxs-lookup"><span data-stu-id="ac852-147">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="ac852-148">SQL Database Pricing Details</span><span class="sxs-lookup"><span data-stu-id="ac852-148">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="ac852-149">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="ac852-149">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
* <span data-ttu-id="ac852-150">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](https://azure.microsoft.com/blog/best-practices-windows-azure-websites-waws/).</span><span class="sxs-lookup"><span data-stu-id="ac852-150">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](https://azure.microsoft.com/blog/best-practices-windows-azure-websites-waws/).</span></span>
* <span data-ttu-id="ac852-151">For videos about scaling App Service apps, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="ac852-151">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="ac852-152">When to Scale Azure Websites - with Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="ac852-152">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="ac852-153">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="ac852-153">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="ac852-154">How Azure Websites Scale - with Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="ac852-154">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:https://azure.microsoft.com/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:https://account.windowsazure.com/subscriptions
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
