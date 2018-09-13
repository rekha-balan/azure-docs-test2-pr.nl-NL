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
ms.openlocfilehash: 5b299d762f3144bca59c7b874cb2c435278674fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554755"
---
# <a name="create-and-manage-hybrid-connections"></a><span data-ttu-id="d4370-104">Create and Manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="d4370-104">Create and Manage Hybrid Connections</span></span>
## <a name="overview-of-the-steps"></a><span data-ttu-id="d4370-105">Overview of the Steps</span><span class="sxs-lookup"><span data-stu-id="d4370-105">Overview of the Steps</span></span>
1. <span data-ttu-id="d4370-106">Create a Hybrid Connection by entering the **host name** or **FQDN** of the on-premises resource in your private network.</span><span class="sxs-lookup"><span data-stu-id="d4370-106">Create a Hybrid Connection by entering the **host name** or **FQDN** of the on-premises resource in your private network.</span></span>
2. <span data-ttu-id="d4370-107">Link your Azure web apps or Azure mobile apps to the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="d4370-107">Link your Azure web apps or Azure mobile apps to the Hybrid Connection.</span></span>
3. <span data-ttu-id="d4370-108">Install the Hybrid Connection Manager on your on-premises resource and connect to the specific Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="d4370-108">Install the Hybrid Connection Manager on your on-premises resource and connect to the specific Hybrid Connection.</span></span> <span data-ttu-id="d4370-109">The Azure portal provides a single-click experience to install and connect.</span><span class="sxs-lookup"><span data-stu-id="d4370-109">The Azure portal provides a single-click experience to install and connect.</span></span>
4. <span data-ttu-id="d4370-110">Manage Hybrid Connections and their connection keys.</span><span class="sxs-lookup"><span data-stu-id="d4370-110">Manage Hybrid Connections and their connection keys.</span></span>

<span data-ttu-id="d4370-111">This topic lists these steps.</span><span class="sxs-lookup"><span data-stu-id="d4370-111">This topic lists these steps.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4370-112">It is possible to set a Hybrid Connection endpoint to an IP address.</span><span class="sxs-lookup"><span data-stu-id="d4370-112">It is possible to set a Hybrid Connection endpoint to an IP address.</span></span> <span data-ttu-id="d4370-113">If you use an IP address, you may or may not reach the on-premises resource, depending on your client.</span><span class="sxs-lookup"><span data-stu-id="d4370-113">If you use an IP address, you may or may not reach the on-premises resource, depending on your client.</span></span> <span data-ttu-id="d4370-114">The Hybrid Connection depends on the client doing a DNS lookup.</span><span class="sxs-lookup"><span data-stu-id="d4370-114">The Hybrid Connection depends on the client doing a DNS lookup.</span></span> <span data-ttu-id="d4370-115">In most cases, the **client** is your application code.</span><span class="sxs-lookup"><span data-stu-id="d4370-115">In most cases, the **client** is your application code.</span></span> <span data-ttu-id="d4370-116">If the client does not perform a DNS lookup, (it does not try to resolve the IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="d4370-116">If the client does not perform a DNS lookup, (it does not try to resolve the IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through the Hybrid Connection.</span></span>
> 
> <span data-ttu-id="d4370-117">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span><span class="sxs-lookup"><span data-stu-id="d4370-117">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span></span>
> 
> <span data-ttu-id="d4370-118">**The following scenario works:**</span><span class="sxs-lookup"><span data-stu-id="d4370-118">**The following scenario works:**</span></span>  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves to 127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> <span data-ttu-id="d4370-119">**The following scenario doesn't work:**</span><span class="sxs-lookup"><span data-stu-id="d4370-119">**The following scenario doesn't work:**</span></span>  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route to host`
> 
> 

## <a name="CreateHybridConnection"></a><span data-ttu-id="d4370-120">Create a Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="d4370-120">Create a Hybrid Connection</span></span>
<span data-ttu-id="d4370-121">A Hybrid Connection can be created in the Azure portal using Web Apps **or** using BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="d4370-121">A Hybrid Connection can be created in the Azure portal using Web Apps **or** using BizTalk Services.</span></span> 

<span data-ttu-id="d4370-122">**To create Hybrid Connections using Web Apps**, see [Connect Azure Web Apps to an On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4370-122">**To create Hybrid Connections using Web Apps**, see [Connect Azure Web Apps to an On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span> <span data-ttu-id="d4370-123">You can also install the Hybrid Connection Manager (HCM) from your web app, which is the preferred method.</span><span class="sxs-lookup"><span data-stu-id="d4370-123">You can also install the Hybrid Connection Manager (HCM) from your web app, which is the preferred method.</span></span> 

<span data-ttu-id="d4370-124">**To create Hybrid Connections in BizTalk Services**:</span><span class="sxs-lookup"><span data-stu-id="d4370-124">**To create Hybrid Connections in BizTalk Services**:</span></span>

1. <span data-ttu-id="d4370-125">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d4370-125">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d4370-126">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="d4370-126">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
   
    <span data-ttu-id="d4370-127">If you don't have an existing BizTalk Service, you can [Create a BizTalk Service](biztalk-provision-services.md).</span><span class="sxs-lookup"><span data-stu-id="d4370-127">If you don't have an existing BizTalk Service, you can [Create a BizTalk Service](biztalk-provision-services.md).</span></span>
3. <span data-ttu-id="d4370-128">Select the **Hybrid Connections** tab:</span><span class="sxs-lookup"><span data-stu-id="d4370-128">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="d4370-129">![Hybrid Connections Tab][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="d4370-129">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="d4370-130">Select **Create a Hybrid Connection** or select the **ADD** button in the task bar.</span><span class="sxs-lookup"><span data-stu-id="d4370-130">Select **Create a Hybrid Connection** or select the **ADD** button in the task bar.</span></span> <span data-ttu-id="d4370-131">Enter the following:</span><span class="sxs-lookup"><span data-stu-id="d4370-131">Enter the following:</span></span>
   
   | <span data-ttu-id="d4370-132">Property</span><span class="sxs-lookup"><span data-stu-id="d4370-132">Property</span></span> | <span data-ttu-id="d4370-133">Description</span><span class="sxs-lookup"><span data-stu-id="d4370-133">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d4370-134">Name</span><span class="sxs-lookup"><span data-stu-id="d4370-134">Name</span></span> |<span data-ttu-id="d4370-135">The Hybrid Connection name must be unique and cannot be the same name as the BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="d4370-135">The Hybrid Connection name must be unique and cannot be the same name as the BizTalk Service.</span></span> <span data-ttu-id="d4370-136">You can enter any name but be specific with its purpose.</span><span class="sxs-lookup"><span data-stu-id="d4370-136">You can enter any name but be specific with its purpose.</span></span> <span data-ttu-id="d4370-137">Examples include:</span><span class="sxs-lookup"><span data-stu-id="d4370-137">Examples include:</span></span><br/><br/><span data-ttu-id="d4370-138">Payroll*SQLServer*</span><span class="sxs-lookup"><span data-stu-id="d4370-138">Payroll*SQLServer*</span></span><br/><span data-ttu-id="d4370-139">SupplyList*SharepointServer*</span><span class="sxs-lookup"><span data-stu-id="d4370-139">SupplyList*SharepointServer*</span></span><br/><span data-ttu-id="d4370-140">Customers*OracleServer*</span><span class="sxs-lookup"><span data-stu-id="d4370-140">Customers*OracleServer*</span></span> |
   | <span data-ttu-id="d4370-141">Host Name</span><span class="sxs-lookup"><span data-stu-id="d4370-141">Host Name</span></span> |<span data-ttu-id="d4370-142">Enter the fully qualified host name, only the host name, or the IPv4 address of the on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="d4370-142">Enter the fully qualified host name, only the host name, or the IPv4 address of the on-premises resource.</span></span> <span data-ttu-id="d4370-143">Examples include:</span><span class="sxs-lookup"><span data-stu-id="d4370-143">Examples include:</span></span><br/><br/><span data-ttu-id="d4370-144">mySQLServer</span><span class="sxs-lookup"><span data-stu-id="d4370-144">mySQLServer</span></span><br/><span data-ttu-id="d4370-145">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="d4370-145">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span></span><br/><span data-ttu-id="d4370-146">*myHTTPSharePointServer*</span><span class="sxs-lookup"><span data-stu-id="d4370-146">*myHTTPSharePointServer*</span></span><br/><span data-ttu-id="d4370-147">*myHTTPSharePointServer*.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="d4370-147">*myHTTPSharePointServer*.*yourCompany*.com</span></span><br/><span data-ttu-id="d4370-148">10.100.10.10</span><span class="sxs-lookup"><span data-stu-id="d4370-148">10.100.10.10</span></span><br/><br/><span data-ttu-id="d4370-149">If you use the IPv4 address, note that your client or application code may not resolve the IP address.</span><span class="sxs-lookup"><span data-stu-id="d4370-149">If you use the IPv4 address, note that your client or application code may not resolve the IP address.</span></span> <span data-ttu-id="d4370-150">See the Important note at the top of this topic.</span><span class="sxs-lookup"><span data-stu-id="d4370-150">See the Important note at the top of this topic.</span></span> |
   | <span data-ttu-id="d4370-151">Port</span><span class="sxs-lookup"><span data-stu-id="d4370-151">Port</span></span> |<span data-ttu-id="d4370-152">Enter the port number of the on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="d4370-152">Enter the port number of the on-premises resource.</span></span> <span data-ttu-id="d4370-153">For example, if you're using Web Apps, enter port 80 or port 443.</span><span class="sxs-lookup"><span data-stu-id="d4370-153">For example, if you're using Web Apps, enter port 80 or port 443.</span></span> <span data-ttu-id="d4370-154">If you're using SQL Server, enter port 1433.</span><span class="sxs-lookup"><span data-stu-id="d4370-154">If you're using SQL Server, enter port 1433.</span></span> |
5. <span data-ttu-id="d4370-155">Select the check mark to complete the setup.</span><span class="sxs-lookup"><span data-stu-id="d4370-155">Select the check mark to complete the setup.</span></span> 

#### <a name="additional"></a><span data-ttu-id="d4370-156">Additional</span><span class="sxs-lookup"><span data-stu-id="d4370-156">Additional</span></span>
* <span data-ttu-id="d4370-157">Multiple Hybrid Connections can be created.</span><span class="sxs-lookup"><span data-stu-id="d4370-157">Multiple Hybrid Connections can be created.</span></span> <span data-ttu-id="d4370-158">See the [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for the number of connections allowed.</span><span class="sxs-lookup"><span data-stu-id="d4370-158">See the [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for the number of connections allowed.</span></span> 
* <span data-ttu-id="d4370-159">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span><span class="sxs-lookup"><span data-stu-id="d4370-159">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span></span> <span data-ttu-id="d4370-160">Each pair has a Primary and a Secondary key.</span><span class="sxs-lookup"><span data-stu-id="d4370-160">Each pair has a Primary and a Secondary key.</span></span> 

## <a name="LinkWebSite"></a><span data-ttu-id="d4370-161">Link your Azure App Service Web App or Mobile App</span><span class="sxs-lookup"><span data-stu-id="d4370-161">Link your Azure App Service Web App or Mobile App</span></span>
<span data-ttu-id="d4370-162">To link a Web App or Mobile App in Azure App Service to an existing Hybrid Connection, select **use an existing Hybrid Connection** in the Hybrid Connections blade.</span><span class="sxs-lookup"><span data-stu-id="d4370-162">To link a Web App or Mobile App in Azure App Service to an existing Hybrid Connection, select **use an existing Hybrid Connection** in the Hybrid Connections blade.</span></span> <span data-ttu-id="d4370-163">See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4370-163">See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="InstallHCM"></a><span data-ttu-id="d4370-164">Install the Hybrid Connection Manager on-premises</span><span class="sxs-lookup"><span data-stu-id="d4370-164">Install the Hybrid Connection Manager on-premises</span></span>
<span data-ttu-id="d4370-165">After a Hybrid Connection is created, install the Hybrid Connection Manager on the on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="d4370-165">After a Hybrid Connection is created, install the Hybrid Connection Manager on the on-premises resource.</span></span> <span data-ttu-id="d4370-166">It can be downloaded from your Azure web apps or from your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="d4370-166">It can be downloaded from your Azure web apps or from your BizTalk Service.</span></span> <span data-ttu-id="d4370-167">BizTalk Services steps:</span><span class="sxs-lookup"><span data-stu-id="d4370-167">BizTalk Services steps:</span></span> 

1. <span data-ttu-id="d4370-168">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d4370-168">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d4370-169">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="d4370-169">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="d4370-170">Select the **Hybrid Connections** tab:</span><span class="sxs-lookup"><span data-stu-id="d4370-170">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="d4370-171">![Hybrid Connections Tab][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="d4370-171">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="d4370-172">In the task bar, select **On-Premises Setup**:</span><span class="sxs-lookup"><span data-stu-id="d4370-172">In the task bar, select **On-Premises Setup**:</span></span>  
   <span data-ttu-id="d4370-173">![On-Premises Setup][HCOnPremSetup]</span><span class="sxs-lookup"><span data-stu-id="d4370-173">![On-Premises Setup][HCOnPremSetup]</span></span>
5. <span data-ttu-id="d4370-174">Select **Install and Configure** to run or download the Hybrid Connection Manager on the on-premises system.</span><span class="sxs-lookup"><span data-stu-id="d4370-174">Select **Install and Configure** to run or download the Hybrid Connection Manager on the on-premises system.</span></span> 
6. <span data-ttu-id="d4370-175">Select the check mark to start the installation.</span><span class="sxs-lookup"><span data-stu-id="d4370-175">Select the check mark to start the installation.</span></span> 

<!--
You can also download the Hybrid Connection Manager MSI file and copy the file to your on-premises resource. Specific steps:

1. Copy the on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for the specific steps.
2. Download the Hybrid Connection Manager MSI file. 
3. On the on-premises resource, install the Hybrid Connection Manager from the MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a><span data-ttu-id="d4370-176">Additional</span><span class="sxs-lookup"><span data-stu-id="d4370-176">Additional</span></span>
* <span data-ttu-id="d4370-177">Hybrid Connection Manager can be installed on the following operating systems:</span><span class="sxs-lookup"><span data-stu-id="d4370-177">Hybrid Connection Manager can be installed on the following operating systems:</span></span>
  
  * <span data-ttu-id="d4370-178">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span><span class="sxs-lookup"><span data-stu-id="d4370-178">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="d4370-179">Windows Server 2012 (Windows Management Framework 4.0+ required)</span><span class="sxs-lookup"><span data-stu-id="d4370-179">Windows Server 2012 (Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="d4370-180">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d4370-180">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d4370-181">After you install the Hybrid Connection Manager, the following occurs:</span><span class="sxs-lookup"><span data-stu-id="d4370-181">After you install the Hybrid Connection Manager, the following occurs:</span></span> 
  
  * <span data-ttu-id="d4370-182">The Hybrid Connection hosted on Azure is automatically configured to use the Primary Application Connection String.</span><span class="sxs-lookup"><span data-stu-id="d4370-182">The Hybrid Connection hosted on Azure is automatically configured to use the Primary Application Connection String.</span></span> 
  * <span data-ttu-id="d4370-183">The On-Premises resource is automatically configured to use the Primary On-Premises Connection String.</span><span class="sxs-lookup"><span data-stu-id="d4370-183">The On-Premises resource is automatically configured to use the Primary On-Premises Connection String.</span></span>
* <span data-ttu-id="d4370-184">The Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span><span class="sxs-lookup"><span data-stu-id="d4370-184">The Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span></span> <span data-ttu-id="d4370-185">The Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span><span class="sxs-lookup"><span data-stu-id="d4370-185">The Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span></span>
* <span data-ttu-id="d4370-186">You can scale Hybrid Connections by installing another instance of the Hybrid Connection Manager on another server.</span><span class="sxs-lookup"><span data-stu-id="d4370-186">You can scale Hybrid Connections by installing another instance of the Hybrid Connection Manager on another server.</span></span> <span data-ttu-id="d4370-187">Configure the on-premises listener to use the same address as the first on-premises listener.</span><span class="sxs-lookup"><span data-stu-id="d4370-187">Configure the on-premises listener to use the same address as the first on-premises listener.</span></span> <span data-ttu-id="d4370-188">In this situation, the traffic is randomly distributed (round robin) between the active on-premises listeners.</span><span class="sxs-lookup"><span data-stu-id="d4370-188">In this situation, the traffic is randomly distributed (round robin) between the active on-premises listeners.</span></span> 

## <a name="ManageHybridConnection"></a><span data-ttu-id="d4370-189">Manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="d4370-189">Manage Hybrid Connections</span></span>
<span data-ttu-id="d4370-190">To manage your Hybrid Connections, you can:</span><span class="sxs-lookup"><span data-stu-id="d4370-190">To manage your Hybrid Connections, you can:</span></span>

* <span data-ttu-id="d4370-191">Use the Azure portal and go to your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="d4370-191">Use the Azure portal and go to your BizTalk Service.</span></span> 
* <span data-ttu-id="d4370-192">Use [REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4370-192">Use [REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

#### <a name="copyregenerate-the-hybrid-connection-strings"></a><span data-ttu-id="d4370-193">Copy/regenerate the Hybrid Connection Strings</span><span class="sxs-lookup"><span data-stu-id="d4370-193">Copy/regenerate the Hybrid Connection Strings</span></span>
1. <span data-ttu-id="d4370-194">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d4370-194">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d4370-195">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="d4370-195">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="d4370-196">Select the **Hybrid Connections** tab:</span><span class="sxs-lookup"><span data-stu-id="d4370-196">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="d4370-197">![Hybrid Connections Tab][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="d4370-197">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="d4370-198">Select the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="d4370-198">Select the Hybrid Connection.</span></span> <span data-ttu-id="d4370-199">In the task bar, select **Manage Connection**:</span><span class="sxs-lookup"><span data-stu-id="d4370-199">In the task bar, select **Manage Connection**:</span></span>  
   <span data-ttu-id="d4370-200">![Manage Options][HCManageConnection]</span><span class="sxs-lookup"><span data-stu-id="d4370-200">![Manage Options][HCManageConnection]</span></span>
   
    <span data-ttu-id="d4370-201">**Manage Connection** lists the Application and On-Premises connection strings.</span><span class="sxs-lookup"><span data-stu-id="d4370-201">**Manage Connection** lists the Application and On-Premises connection strings.</span></span> <span data-ttu-id="d4370-202">You can copy the Connection Strings or regenerate the Access Key used in the connection string.</span><span class="sxs-lookup"><span data-stu-id="d4370-202">You can copy the Connection Strings or regenerate the Access Key used in the connection string.</span></span> 
   
    <span data-ttu-id="d4370-203">**If you select Regenerate**, the Shared Access Key used within the Connection String is changed.</span><span class="sxs-lookup"><span data-stu-id="d4370-203">**If you select Regenerate**, the Shared Access Key used within the Connection String is changed.</span></span> <span data-ttu-id="d4370-204">Do the following:</span><span class="sxs-lookup"><span data-stu-id="d4370-204">Do the following:</span></span>
   
   * <span data-ttu-id="d4370-205">In the Azure classic portal, select **Sync Keys** in the Azure application.</span><span class="sxs-lookup"><span data-stu-id="d4370-205">In the Azure classic portal, select **Sync Keys** in the Azure application.</span></span>
   * <span data-ttu-id="d4370-206">Re-run the **On-Premises Setup**.</span><span class="sxs-lookup"><span data-stu-id="d4370-206">Re-run the **On-Premises Setup**.</span></span> <span data-ttu-id="d4370-207">When you re-run the On-Premises Setup, the on-premises resource is automatically configured to use the updated Primary connection string.</span><span class="sxs-lookup"><span data-stu-id="d4370-207">When you re-run the On-Premises Setup, the on-premises resource is automatically configured to use the updated Primary connection string.</span></span>

#### <a name="use-group-policy-to-control-the-on-premises-resources-used-by-a-hybrid-connection"></a><span data-ttu-id="d4370-208">Use Group Policy to control the on-premises resources used by a Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="d4370-208">Use Group Policy to control the on-premises resources used by a Hybrid Connection</span></span>
1. <span data-ttu-id="d4370-209">Download the [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span><span class="sxs-lookup"><span data-stu-id="d4370-209">Download the [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span></span>
2. <span data-ttu-id="d4370-210">Extract the files.</span><span class="sxs-lookup"><span data-stu-id="d4370-210">Extract the files.</span></span>
3. <span data-ttu-id="d4370-211">On the computer that modifies group policy, do the following:</span><span class="sxs-lookup"><span data-stu-id="d4370-211">On the computer that modifies group policy, do the following:</span></span>  
   
   * <span data-ttu-id="d4370-212">Copy the .ADMX files to the *%WINROOT%\PolicyDefinitions* folder.</span><span class="sxs-lookup"><span data-stu-id="d4370-212">Copy the .ADMX files to the *%WINROOT%\PolicyDefinitions* folder.</span></span>
   * <span data-ttu-id="d4370-213">Copy the .ADML files to the *%WINROOT%\PolicyDefinitions\en-us* folder.</span><span class="sxs-lookup"><span data-stu-id="d4370-213">Copy the .ADML files to the *%WINROOT%\PolicyDefinitions\en-us* folder.</span></span>

<span data-ttu-id="d4370-214">Once copied, you can use Group Policy Editor to change the policy.</span><span class="sxs-lookup"><span data-stu-id="d4370-214">Once copied, you can use Group Policy Editor to change the policy.</span></span>

## <a name="next"></a><span data-ttu-id="d4370-215">Next</span><span class="sxs-lookup"><span data-stu-id="d4370-215">Next</span></span>
[<span data-ttu-id="d4370-216">Connect Azure Web Apps to an On-Premises Resource</span><span class="sxs-lookup"><span data-stu-id="d4370-216">Connect Azure Web Apps to an On-Premises Resource</span></span>](../app-service-web/web-sites-hybrid-connection-get-started.md)  
<span data-ttu-id="d4370-217">[Connect to on-premises SQL Server from Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="d4370-217">[Connect to on-premises SQL Server from Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span></span>  
[<span data-ttu-id="d4370-218">Hybrid Connections Overview</span><span class="sxs-lookup"><span data-stu-id="d4370-218">Hybrid Connections Overview</span></span>](integration-hybrid-connection-overview.md)

## <a name="see-also"></a><span data-ttu-id="d4370-219">See Also</span><span class="sxs-lookup"><span data-stu-id="d4370-219">See Also</span></span>
[<span data-ttu-id="d4370-220">REST API for Managing BizTalk Services on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d4370-220">REST API for Managing BizTalk Services on Microsoft Azure</span></span>](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[<span data-ttu-id="d4370-221">BizTalk Services: Editions Chart</span><span class="sxs-lookup"><span data-stu-id="d4370-221">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
[<span data-ttu-id="d4370-222">Create a BizTalk Service using Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d4370-222">Create a BizTalk Service using Azure classic portal</span></span>](biztalk-provision-services.md)  
[<span data-ttu-id="d4370-223">BizTalk Services: Dashboard, Monitor and Scale tabs</span><span class="sxs-lookup"><span data-stu-id="d4370-223">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 



