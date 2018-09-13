---
title: Create and Manage Hybrid Connections | Microsoft Docs
description: Learn how to create a hybrid connection, manage the connection, and install the Hybrid Connection Manager. MABS, WABS
services: biztalk-services
documentationcenter: ''
author: MandiOhlinger
manager: erikre
editor: ''
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 1751d33b5f6f6a506654daedd15bbd75ae271483
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825513"
---
# <a name="create-and-manage-hybrid-connections"></a><span data-ttu-id="e4c12-104">Create and Manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="e4c12-104">Create and Manage Hybrid Connections</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4c12-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="e4c12-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="e4c12-106">For more information, including how to manage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span><span class="sxs-lookup"><span data-stu-id="e4c12-106">For more information, including how to manage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>

>[!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

## <a name="overview-of-the-steps"></a><span data-ttu-id="e4c12-107">Overview of the Steps</span><span class="sxs-lookup"><span data-stu-id="e4c12-107">Overview of the Steps</span></span>
1. <span data-ttu-id="e4c12-108">Create a Hybrid Connection by entering the **host name** or **FQDN** of the on-premises resource in your private network.</span><span class="sxs-lookup"><span data-stu-id="e4c12-108">Create a Hybrid Connection by entering the **host name** or **FQDN** of the on-premises resource in your private network.</span></span>
2. <span data-ttu-id="e4c12-109">Link your Azure web apps or Azure mobile apps to the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="e4c12-109">Link your Azure web apps or Azure mobile apps to the Hybrid Connection.</span></span>
3. <span data-ttu-id="e4c12-110">Install the Hybrid Connection Manager on your on-premises resource and connect to the specific Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="e4c12-110">Install the Hybrid Connection Manager on your on-premises resource and connect to the specific Hybrid Connection.</span></span> <span data-ttu-id="e4c12-111">The Azure portal provides a single-click experience to install and connect.</span><span class="sxs-lookup"><span data-stu-id="e4c12-111">The Azure portal provides a single-click experience to install and connect.</span></span>
4. <span data-ttu-id="e4c12-112">Manage Hybrid Connections and their connection keys.</span><span class="sxs-lookup"><span data-stu-id="e4c12-112">Manage Hybrid Connections and their connection keys.</span></span>

<span data-ttu-id="e4c12-113">This topic lists these steps.</span><span class="sxs-lookup"><span data-stu-id="e4c12-113">This topic lists these steps.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e4c12-114">It is possible to set a Hybrid Connection endpoint to an IP address.</span><span class="sxs-lookup"><span data-stu-id="e4c12-114">It is possible to set a Hybrid Connection endpoint to an IP address.</span></span> <span data-ttu-id="e4c12-115">If you use an IP address, you may or may not reach the on-premises resource, depending on your client.</span><span class="sxs-lookup"><span data-stu-id="e4c12-115">If you use an IP address, you may or may not reach the on-premises resource, depending on your client.</span></span> <span data-ttu-id="e4c12-116">The Hybrid Connection depends on the client doing a DNS lookup.</span><span class="sxs-lookup"><span data-stu-id="e4c12-116">The Hybrid Connection depends on the client doing a DNS lookup.</span></span> <span data-ttu-id="e4c12-117">In most cases, the **client** is your application code.</span><span class="sxs-lookup"><span data-stu-id="e4c12-117">In most cases, the **client** is your application code.</span></span> <span data-ttu-id="e4c12-118">If the client does not perform a DNS lookup, (it does not try to resolve the IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="e4c12-118">If the client does not perform a DNS lookup, (it does not try to resolve the IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through the Hybrid Connection.</span></span>
> 
> <span data-ttu-id="e4c12-119">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span><span class="sxs-lookup"><span data-stu-id="e4c12-119">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span></span>
> 
> <span data-ttu-id="e4c12-120">**The following scenario works:**</span><span class="sxs-lookup"><span data-stu-id="e4c12-120">**The following scenario works:**</span></span>  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves to 127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> <span data-ttu-id="e4c12-121">**The following scenario doesn't work:**</span><span class="sxs-lookup"><span data-stu-id="e4c12-121">**The following scenario doesn't work:**</span></span>  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route to host`
> 
> 

## <a name="CreateHybridConnection"></a><span data-ttu-id="e4c12-122">Create a Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="e4c12-122">Create a Hybrid Connection</span></span>
<span data-ttu-id="e4c12-123">A Hybrid Connection can be created in [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) **or** using [BizTalk Services REST APIs](https://msdn.microsoft.com/library/azure/dn232347.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4c12-123">A Hybrid Connection can be created in [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) **or** using [BizTalk Services REST APIs](https://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span> 

<!-- **To create Hybrid Connections using Web Apps**, see [Connect Azure Web Apps to an On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md). You can also install the Hybrid Connection Manager (HCM) from your web app, which is the preferred method.  -->

#### <a name="additional"></a><span data-ttu-id="e4c12-124">Additional</span><span class="sxs-lookup"><span data-stu-id="e4c12-124">Additional</span></span>
* <span data-ttu-id="e4c12-125">Multiple Hybrid Connections can be created.</span><span class="sxs-lookup"><span data-stu-id="e4c12-125">Multiple Hybrid Connections can be created.</span></span> <span data-ttu-id="e4c12-126">See the [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for the number of connections allowed.</span><span class="sxs-lookup"><span data-stu-id="e4c12-126">See the [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for the number of connections allowed.</span></span> 
* <span data-ttu-id="e4c12-127">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span><span class="sxs-lookup"><span data-stu-id="e4c12-127">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span></span> <span data-ttu-id="e4c12-128">Each pair has a Primary and a Secondary key.</span><span class="sxs-lookup"><span data-stu-id="e4c12-128">Each pair has a Primary and a Secondary key.</span></span> 

## <a name="LinkWebSite"></a><span data-ttu-id="e4c12-129">Link your Azure App Service Web App or Mobile App</span><span class="sxs-lookup"><span data-stu-id="e4c12-129">Link your Azure App Service Web App or Mobile App</span></span>
<span data-ttu-id="e4c12-130">To link a Web App or Mobile App in Azure App Service to an existing Hybrid Connection, select **use an existing Hybrid Connection** in the Hybrid Connections blade.</span><span class="sxs-lookup"><span data-stu-id="e4c12-130">To link a Web App or Mobile App in Azure App Service to an existing Hybrid Connection, select **use an existing Hybrid Connection** in the Hybrid Connections blade.</span></span> 
<!-- See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md). -->

## <a name="InstallHCM"></a><span data-ttu-id="e4c12-131">Install the Hybrid Connection Manager on-premises</span><span class="sxs-lookup"><span data-stu-id="e4c12-131">Install the Hybrid Connection Manager on-premises</span></span>
<span data-ttu-id="e4c12-132">After a Hybrid Connection is created, install the Hybrid Connection Manager on the on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="e4c12-132">After a Hybrid Connection is created, install the Hybrid Connection Manager on the on-premises resource.</span></span> <span data-ttu-id="e4c12-133">It can be downloaded from your Azure web apps or from your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e4c12-133">It can be downloaded from your Azure web apps or from your BizTalk Service.</span></span> 

[!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]
 
<span data-ttu-id="e4c12-134">[Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) is also a good resource.</span><span class="sxs-lookup"><span data-stu-id="e4c12-134">[Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) is also a good resource.</span></span>

<!--
You can also download the Hybrid Connection Manager MSI file and copy the file to your on-premises resource. Specific steps:

1. Copy the on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for the specific steps.
2. Download the Hybrid Connection Manager MSI file. 
3. On the on-premises resource, install the Hybrid Connection Manager from the MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a><span data-ttu-id="e4c12-135">Additional</span><span class="sxs-lookup"><span data-stu-id="e4c12-135">Additional</span></span>
* <span data-ttu-id="e4c12-136">Hybrid Connection Manager can be installed on the following operating systems:</span><span class="sxs-lookup"><span data-stu-id="e4c12-136">Hybrid Connection Manager can be installed on the following operating systems:</span></span>
  
  * <span data-ttu-id="e4c12-137">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span><span class="sxs-lookup"><span data-stu-id="e4c12-137">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="e4c12-138">Windows Server 2012 (Windows Management Framework 4.0+ required)</span><span class="sxs-lookup"><span data-stu-id="e4c12-138">Windows Server 2012 (Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="e4c12-139">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e4c12-139">Windows Server 2012 R2</span></span>
* <span data-ttu-id="e4c12-140">After you install the Hybrid Connection Manager, the following occurs:</span><span class="sxs-lookup"><span data-stu-id="e4c12-140">After you install the Hybrid Connection Manager, the following occurs:</span></span> 
  
  * <span data-ttu-id="e4c12-141">The Hybrid Connection hosted on Azure is automatically configured to use the Primary Application Connection String.</span><span class="sxs-lookup"><span data-stu-id="e4c12-141">The Hybrid Connection hosted on Azure is automatically configured to use the Primary Application Connection String.</span></span> 
  * <span data-ttu-id="e4c12-142">The On-Premises resource is automatically configured to use the Primary On-Premises Connection String.</span><span class="sxs-lookup"><span data-stu-id="e4c12-142">The On-Premises resource is automatically configured to use the Primary On-Premises Connection String.</span></span>
* <span data-ttu-id="e4c12-143">The Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span><span class="sxs-lookup"><span data-stu-id="e4c12-143">The Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span></span> <span data-ttu-id="e4c12-144">The Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span><span class="sxs-lookup"><span data-stu-id="e4c12-144">The Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span></span>
* <span data-ttu-id="e4c12-145">You can scale Hybrid Connections by installing another instance of the Hybrid Connection Manager on another server.</span><span class="sxs-lookup"><span data-stu-id="e4c12-145">You can scale Hybrid Connections by installing another instance of the Hybrid Connection Manager on another server.</span></span> <span data-ttu-id="e4c12-146">Configure the on-premises listener to use the same address as the first on-premises listener.</span><span class="sxs-lookup"><span data-stu-id="e4c12-146">Configure the on-premises listener to use the same address as the first on-premises listener.</span></span> <span data-ttu-id="e4c12-147">In this situation, the traffic is randomly distributed (round robin) between the active on-premises listeners.</span><span class="sxs-lookup"><span data-stu-id="e4c12-147">In this situation, the traffic is randomly distributed (round robin) between the active on-premises listeners.</span></span> 

## <a name="ManageHybridConnection"></a><span data-ttu-id="e4c12-148">Manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="e4c12-148">Manage Hybrid Connections</span></span>

[!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)] 

<span data-ttu-id="e4c12-149">[Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) is also a good resource.</span><span class="sxs-lookup"><span data-stu-id="e4c12-149">[Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) is also a good resource.</span></span>

#### <a name="copyregenerate-the-hybrid-connection-strings"></a><span data-ttu-id="e4c12-150">Copy/regenerate the Hybrid Connection Strings</span><span class="sxs-lookup"><span data-stu-id="e4c12-150">Copy/regenerate the Hybrid Connection Strings</span></span>

[!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)] 

<span data-ttu-id="e4c12-151">[Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) is also a good resource.</span><span class="sxs-lookup"><span data-stu-id="e4c12-151">[Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md) is also a good resource.</span></span>

#### <a name="use-group-policy-to-control-the-on-premises-resources-used-by-a-hybrid-connection"></a><span data-ttu-id="e4c12-152">Use Group Policy to control the on-premises resources used by a Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="e4c12-152">Use Group Policy to control the on-premises resources used by a Hybrid Connection</span></span>
1. <span data-ttu-id="e4c12-153">Download the [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span><span class="sxs-lookup"><span data-stu-id="e4c12-153">Download the [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span></span>
2. <span data-ttu-id="e4c12-154">Extract the files.</span><span class="sxs-lookup"><span data-stu-id="e4c12-154">Extract the files.</span></span>
3. <span data-ttu-id="e4c12-155">On the computer that modifies group policy, do the following:</span><span class="sxs-lookup"><span data-stu-id="e4c12-155">On the computer that modifies group policy, do the following:</span></span>  
   
   * <span data-ttu-id="e4c12-156">Copy the .ADMX files to the *%WINROOT%\PolicyDefinitions* folder.</span><span class="sxs-lookup"><span data-stu-id="e4c12-156">Copy the .ADMX files to the *%WINROOT%\PolicyDefinitions* folder.</span></span>
   * <span data-ttu-id="e4c12-157">Copy the .ADML files to the *%WINROOT%\PolicyDefinitions\en-us* folder.</span><span class="sxs-lookup"><span data-stu-id="e4c12-157">Copy the .ADML files to the *%WINROOT%\PolicyDefinitions\en-us* folder.</span></span>

<span data-ttu-id="e4c12-158">Once copied, you can use Group Policy Editor to change the policy.</span><span class="sxs-lookup"><span data-stu-id="e4c12-158">Once copied, you can use Group Policy Editor to change the policy.</span></span>

## <a name="next"></a><span data-ttu-id="e4c12-159">Next</span><span class="sxs-lookup"><span data-stu-id="e4c12-159">Next</span></span>
[<span data-ttu-id="e4c12-160">Hybrid Connections Overview</span><span class="sxs-lookup"><span data-stu-id="e4c12-160">Hybrid Connections Overview</span></span>](integration-hybrid-connection-overview.md)

## <a name="see-also"></a><span data-ttu-id="e4c12-161">See Also</span><span class="sxs-lookup"><span data-stu-id="e4c12-161">See Also</span></span>
[<span data-ttu-id="e4c12-162">REST API for Managing BizTalk Services on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e4c12-162">REST API for Managing BizTalk Services on Microsoft Azure</span></span>](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[<span data-ttu-id="e4c12-163">BizTalk Services: Editions Chart</span><span class="sxs-lookup"><span data-stu-id="e4c12-163">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
[<span data-ttu-id="e4c12-164">Create a BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="e4c12-164">Create a BizTalk Service</span></span>](biztalk-provision-services.md)  
[<span data-ttu-id="e4c12-165">BizTalk Services: Dashboard, Monitor and Scale tabs</span><span class="sxs-lookup"><span data-stu-id="e4c12-165">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
