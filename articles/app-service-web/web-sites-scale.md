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
# <a name="scale-up-an-app-in-azure"></a>Scale up an app in Azure
This article shows you how to scale your app in Azure App Service. There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.

* [Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more. You scale up by changing the pricing tier of the App Service plan that your app belongs to.
* [Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.
  You can scale out to as many as 20 instances, depending on your pricing tier. [App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances. For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md). There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.

The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
They do not require you to change your code or redeploy your application.

For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription. To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Scale up your pricing tier
1. In your browser, open the [Azure portal][portal].
2. In your app's blade, click **All settings**, and then click **Scale Up**.
   
    ![Navigate to scale up your Azure app.][ChooseWHP]
3. Choose your tier, and then click **Select**.
   
    The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Scale related resources
If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs. These resources are not scaled with the App Service plan and must be scaled separately.

1. In **Essentials**, click the **Resource group** link.
   
    ![Scale up your Azure app's related resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/RGEssentialsLink.png)
2. In the **Summary** part of the **Resource group** blade, click a resource that you want to scale. The following screenshot shows a SQL Database resource and an Azure Storage resource.
   
    ![Navigate to resource group blade to scale up your Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/ResourceGroup.png)
3. For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.
   
    ![Scale up the SQL Database backend for your Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/ScaleDatabase.png)
   
    You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.
   
    For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.
   
    ![Scale up the Azure Storage account used by your Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Learn about developer features
Depending on the pricing tier, the following developer-oriented features are available:

### <a name="bitness"></a>Bitness
* The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.
* The **Free** and **Shared** plan tiers support 32-bit applications only.

### <a name="debugger-support"></a>Debugger support
* Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.
* Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Learn about other features
* For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service. No credit cards are required and there are no commitments.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Next steps
* To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).
* For information about pricing, support, and SLA, visit the following links.
  
    [Data Transfers Pricing Details](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Microsoft Azure Support Plans](https://azure.microsoft.com/support/plans/)
  
    [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/)
  
    [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]
  
    [App Service Pricing Details](https://azure.microsoft.com/pricing/details/app-service/)
  
    [App Service Pricing Details - SSL Connections](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* For videos about scaling App Service apps, see the following resources:
  
  * [When to Scale Azure Websites - with Stefan Schackow](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [How Azure Websites Scale - with Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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








