---
title: Create Azure BizTalk Services in the Azure portal | Microsoft Docs
description: Learn how to provision or create Azure BizTalk Services in the Azure portal; MABS, WABS
services: biztalk-services
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 83857ba5a719ce8db7b40b03957c0fad22df65d5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551243"
---
# <a name="create-biztalk-services-using-the-azure-portal"></a><span data-ttu-id="cdf17-103">Create BizTalk Services using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cdf17-103">Create BizTalk Services using the Azure portal</span></span>

> [!TIP]
> <span data-ttu-id="cdf17-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cdf17-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="cdf17-105">If you don't have an account, you can create a free trial account within a few minutes.</span><span class="sxs-lookup"><span data-stu-id="cdf17-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="cdf17-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="cdf17-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>
> 
> 

## <a name="create-a-biztalk-service"></a><span data-ttu-id="cdf17-107">Create a BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="cdf17-107">Create a BizTalk Service</span></span>
<span data-ttu-id="cdf17-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span><span class="sxs-lookup"><span data-stu-id="cdf17-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="cdf17-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cdf17-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cdf17-110">In the bottom navigation pane, select **NEW**:</span><span class="sxs-lookup"><span data-stu-id="cdf17-110">In the bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="cdf17-111">![Select the New button][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="cdf17-111">![Select the New button][NEWButton]</span></span>
3. <span data-ttu-id="cdf17-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span><span class="sxs-lookup"><span data-stu-id="cdf17-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="cdf17-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="cdf17-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="cdf17-114">Enter the BizTalk Service settings:</span><span class="sxs-lookup"><span data-stu-id="cdf17-114">Enter the BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="cdf17-115"><strong>BizTalk service name</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="cdf17-116">You can enter any name but be specific.</span><span class="sxs-lookup"><span data-stu-id="cdf17-116">You can enter any name but be specific.</span></span> <span data-ttu-id="cdf17-117">Some examples include:</span><span class="sxs-lookup"><span data-stu-id="cdf17-117">Some examples include:</span></span><br/><br/><span data-ttu-id="cdf17-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="cdf17-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="cdf17-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="cdf17-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="cdf17-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="cdf17-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="cdf17-121">".biztalk.windows.net" is automatically added to the name you enter.</span><span class="sxs-lookup"><span data-stu-id="cdf17-121">".biztalk.windows.net" is automatically added to the name you enter.</span></span> <span data-ttu-id="cdf17-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="cdf17-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-123"><strong>Edition</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="cdf17-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="cdf17-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="cdf17-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span><span class="sxs-lookup"><span data-stu-id="cdf17-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-126"><strong>Region</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="cdf17-127">Select the geographic region to host your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-127">Select the geographic region to host your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-128"><strong>Domain URL</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="cdf17-129"><strong>Optional</strong>.</span><span class="sxs-lookup"><span data-stu-id="cdf17-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="cdf17-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="cdf17-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="cdf17-131">A custom domain can also be entered.</span><span class="sxs-lookup"><span data-stu-id="cdf17-131">A custom domain can also be entered.</span></span> <span data-ttu-id="cdf17-132">For example, if your domain is <em>contoso</em>, you can enter:</span><span class="sxs-lookup"><span data-stu-id="cdf17-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="cdf17-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cdf17-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="cdf17-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cdf17-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="cdf17-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cdf17-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="cdf17-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cdf17-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="cdf17-137">Select the NEXT arrow.</span><span class="sxs-lookup"><span data-stu-id="cdf17-137">Select the NEXT arrow.</span></span>
<span data-ttu-id="cdf17-138">5.</span><span class="sxs-lookup"><span data-stu-id="cdf17-138">5.</span></span> <span data-ttu-id="cdf17-139">Enter the Storage and Database Settings:</span><span class="sxs-lookup"><span data-stu-id="cdf17-139">Enter the Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="cdf17-140"><strong>Monitoring/Archiving storage account</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="cdf17-141">Select an existing storage account or create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="cdf17-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="cdf17-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span><span class="sxs-lookup"><span data-stu-id="cdf17-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-143"><strong>Tracking database</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="cdf17-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="cdf17-145">You need the login name and password entered when that Azure SQL Database Server was created.</span><span class="sxs-lookup"><span data-stu-id="cdf17-145">You need the login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="cdf17-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="cdf17-147">Select the NEXT arrow.</span><span class="sxs-lookup"><span data-stu-id="cdf17-147">Select the NEXT arrow.</span></span>
<span data-ttu-id="cdf17-148">6.</span><span class="sxs-lookup"><span data-stu-id="cdf17-148">6.</span></span> <span data-ttu-id="cdf17-149">Enter the Database settings:</span><span class="sxs-lookup"><span data-stu-id="cdf17-149">Enter the Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="cdf17-150"><strong>Name</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="cdf17-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span><span class="sxs-lookup"><span data-stu-id="cdf17-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="cdf17-152">Enter a SQL Database name to be used by your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-152">Enter a SQL Database name to be used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-153"><strong>Server</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="cdf17-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span><span class="sxs-lookup"><span data-stu-id="cdf17-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="cdf17-155">Select an existing SQL Database Server or create a new SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="cdf17-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-156"><strong>Server login name</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="cdf17-157">Enter the login user name.</span><span class="sxs-lookup"><span data-stu-id="cdf17-157">Enter the login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-158"><strong>Server login password</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="cdf17-159">Enter the login password.</span><span class="sxs-lookup"><span data-stu-id="cdf17-159">Enter the login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cdf17-160"><strong>Region</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="cdf17-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span><span class="sxs-lookup"><span data-stu-id="cdf17-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="cdf17-162">Select the geographic region to host your SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cdf17-162">Select the geographic region to host your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="cdf17-163">Select the check mark to complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="cdf17-163">Select the check mark to complete the wizard.</span></span> <span data-ttu-id="cdf17-164">The progress icon appears:</span><span class="sxs-lookup"><span data-stu-id="cdf17-164">The progress icon appears:</span></span>  
![Progress icon displays when complete][ProgressComplete]

<span data-ttu-id="cdf17-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span><span class="sxs-lookup"><span data-stu-id="cdf17-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="cdf17-167">The default settings are sufficient.</span><span class="sxs-lookup"><span data-stu-id="cdf17-167">The default settings are sufficient.</span></span> <span data-ttu-id="cdf17-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="cdf17-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span><span class="sxs-lookup"><span data-stu-id="cdf17-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span></span>

<span data-ttu-id="cdf17-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span><span class="sxs-lookup"><span data-stu-id="cdf17-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="cdf17-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="cdf17-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="cdf17-172">Post-provisioning steps</span><span class="sxs-lookup"><span data-stu-id="cdf17-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="cdf17-173">Install the certificate on a local computer</span><span class="sxs-lookup"><span data-stu-id="cdf17-173">Install the certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="cdf17-174">Add a production-ready certificate</span><span class="sxs-lookup"><span data-stu-id="cdf17-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="cdf17-175">Get the Access Control namespace</span><span class="sxs-lookup"><span data-stu-id="cdf17-175">Get the Access Control namespace</span></span>](#ACS)

#### <a name="InstallCert"></a><span data-ttu-id="cdf17-176">Install the certificate on a local computer</span><span class="sxs-lookup"><span data-stu-id="cdf17-176">Install the certificate on a local computer</span></span>
<span data-ttu-id="cdf17-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span><span class="sxs-lookup"><span data-stu-id="cdf17-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="cdf17-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span><span class="sxs-lookup"><span data-stu-id="cdf17-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="cdf17-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cdf17-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cdf17-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span><span class="sxs-lookup"><span data-stu-id="cdf17-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="cdf17-181">Select the **Dashboard** tab.</span><span class="sxs-lookup"><span data-stu-id="cdf17-181">Select the **Dashboard** tab.</span></span>
4. <span data-ttu-id="cdf17-182">Select **Download SSL Certificate**:</span><span class="sxs-lookup"><span data-stu-id="cdf17-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="cdf17-183">![Modify SSL Certificate][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="cdf17-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="cdf17-184">Double-click the certificate and run through the wizard to install the certificate.</span><span class="sxs-lookup"><span data-stu-id="cdf17-184">Double-click the certificate and run through the wizard to install the certificate.</span></span> <span data-ttu-id="cdf17-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span><span class="sxs-lookup"><span data-stu-id="cdf17-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span></span>

#### <a name="AddCert"></a><span data-ttu-id="cdf17-186">Add a production-ready certificate</span><span class="sxs-lookup"><span data-stu-id="cdf17-186">Add a production-ready certificate</span></span>
<span data-ttu-id="cdf17-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span><span class="sxs-lookup"><span data-stu-id="cdf17-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="cdf17-188">For production scenarios, replace it with a production-ready certificate.</span><span class="sxs-lookup"><span data-stu-id="cdf17-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="cdf17-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span><span class="sxs-lookup"><span data-stu-id="cdf17-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="cdf17-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span><span class="sxs-lookup"><span data-stu-id="cdf17-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span></span>

#### <a name="ACS"></a><span data-ttu-id="cdf17-191">Get the Access Control namespace</span><span class="sxs-lookup"><span data-stu-id="cdf17-191">Get the Access Control namespace</span></span>
1. <span data-ttu-id="cdf17-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cdf17-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cdf17-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="cdf17-194">In the task bar, select **Connection Information**:</span><span class="sxs-lookup"><span data-stu-id="cdf17-194">In the task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="cdf17-195">![Select Connection Information][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="cdf17-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="cdf17-196">Copy the Access Control values.</span><span class="sxs-lookup"><span data-stu-id="cdf17-196">Copy the Access Control values.</span></span>

<span data-ttu-id="cdf17-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span><span class="sxs-lookup"><span data-stu-id="cdf17-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="cdf17-198">The Access Control namespace is automatically created for your BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-198">The Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="cdf17-199">The Access Control values can be used with any application.</span><span class="sxs-lookup"><span data-stu-id="cdf17-199">The Access Control values can be used with any application.</span></span> <span data-ttu-id="cdf17-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span><span class="sxs-lookup"><span data-stu-id="cdf17-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="cdf17-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span><span class="sxs-lookup"><span data-stu-id="cdf17-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span></span> <span data-ttu-id="cdf17-202">The task bar lists your options.</span><span class="sxs-lookup"><span data-stu-id="cdf17-202">The task bar lists your options.</span></span>

<span data-ttu-id="cdf17-203">Clicking **Manage** opens the Access Control Management Portal.</span><span class="sxs-lookup"><span data-stu-id="cdf17-203">Clicking **Manage** opens the Access Control Management Portal.</span></span> <span data-ttu-id="cdf17-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span><span class="sxs-lookup"><span data-stu-id="cdf17-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="cdf17-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="cdf17-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="cdf17-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span><span class="sxs-lookup"><span data-stu-id="cdf17-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdf17-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span><span class="sxs-lookup"><span data-stu-id="cdf17-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span></span> <span data-ttu-id="cdf17-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span><span class="sxs-lookup"><span data-stu-id="cdf17-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span></span><br/><br/><span data-ttu-id="cdf17-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span><span class="sxs-lookup"><span data-stu-id="cdf17-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span></span>
> 
> 

<span data-ttu-id="cdf17-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span><span class="sxs-lookup"><span data-stu-id="cdf17-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="cdf17-211">Requirements explained</span><span class="sxs-lookup"><span data-stu-id="cdf17-211">Requirements explained</span></span>
<span data-ttu-id="cdf17-212">These requirements do not apply to the Free Edition.</span><span class="sxs-lookup"><span data-stu-id="cdf17-212">These requirements do not apply to the Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="cdf17-213"><strong>What you need</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="cdf17-214"><strong>Why you need it</strong></span><span class="sxs-lookup"><span data-stu-id="cdf17-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cdf17-215">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="cdf17-215">Azure subscription</span></span></td>
<td><span data-ttu-id="cdf17-216">The subscription determines who can sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cdf17-216">The subscription determines who can sign in to the Azure portal.</span></span> <span data-ttu-id="cdf17-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span><span class="sxs-lookup"><span data-stu-id="cdf17-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="cdf17-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span><span class="sxs-lookup"><span data-stu-id="cdf17-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="cdf17-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span><span class="sxs-lookup"><span data-stu-id="cdf17-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span></span> <span data-ttu-id="cdf17-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="cdf17-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="cdf17-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span><span class="sxs-lookup"><span data-stu-id="cdf17-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span></span>
<br/><br/><span data-ttu-id="cdf17-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span><span class="sxs-lookup"><span data-stu-id="cdf17-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="cdf17-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cdf17-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="cdf17-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span><span class="sxs-lookup"><span data-stu-id="cdf17-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="cdf17-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span><span class="sxs-lookup"><span data-stu-id="cdf17-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="cdf17-226">The SQL Database scale is automatically configured.</span><span class="sxs-lookup"><span data-stu-id="cdf17-226">The SQL Database scale is automatically configured.</span></span> <span data-ttu-id="cdf17-227">Typically, the default scale is sufficient for a BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-227">Typically, the default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="cdf17-228">Changing the scale impacts pricing.</span><span class="sxs-lookup"><span data-stu-id="cdf17-228">Changing the scale impacts pricing.</span></span> <span data-ttu-id="cdf17-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span><span class="sxs-lookup"><span data-stu-id="cdf17-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="cdf17-230">
<strong>Notes</strong>
</span><span class="sxs-lookup"><span data-stu-id="cdf17-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="cdf17-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="cdf17-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="cdf17-232">The BizTalk Service requires Azure Services be enabled.</span><span class="sxs-lookup"><span data-stu-id="cdf17-232">The BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="cdf17-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span><span class="sxs-lookup"><span data-stu-id="cdf17-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span></span> <span data-ttu-id="cdf17-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span><span class="sxs-lookup"><span data-stu-id="cdf17-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="cdf17-235">Azure Access Control namespace</span><span class="sxs-lookup"><span data-stu-id="cdf17-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="cdf17-236">Authenticates with Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="cdf17-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="cdf17-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span><span class="sxs-lookup"><span data-stu-id="cdf17-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="cdf17-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span><span class="sxs-lookup"><span data-stu-id="cdf17-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="cdf17-239">Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="cdf17-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="cdf17-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span><span class="sxs-lookup"><span data-stu-id="cdf17-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span></span>

<ul>
<li><span data-ttu-id="cdf17-241">Log files that monitor the BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-241">Log files that monitor the BizTalk Service.</span></span> <span data-ttu-id="cdf17-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cdf17-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span></span></li>
<li><span data-ttu-id="cdf17-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span><span class="sxs-lookup"><span data-stu-id="cdf17-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span></span> <span data-ttu-id="cdf17-244">This data is saved in the Storage account.</span><span class="sxs-lookup"><span data-stu-id="cdf17-244">This data is saved in the Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="cdf17-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span><span class="sxs-lookup"><span data-stu-id="cdf17-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="cdf17-246">The default Storage settings are sufficient for a BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="cdf17-246">The default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="cdf17-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span><span class="sxs-lookup"><span data-stu-id="cdf17-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="cdf17-248">These Keys control access to your Storage account.</span><span class="sxs-lookup"><span data-stu-id="cdf17-248">These Keys control access to your Storage account.</span></span> <span data-ttu-id="cdf17-249">The BizTalk Service automatically uses the Primary Key.</span><span class="sxs-lookup"><span data-stu-id="cdf17-249">The BizTalk Service automatically uses the Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="cdf17-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span><span class="sxs-lookup"><span data-stu-id="cdf17-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="cdf17-251">SSL private certificate</span><span class="sxs-lookup"><span data-stu-id="cdf17-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="cdf17-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span><span class="sxs-lookup"><span data-stu-id="cdf17-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="cdf17-253">This URL is automatically configured to use a self-signed development-only certificate.</span><span class="sxs-lookup"><span data-stu-id="cdf17-253">This URL is automatically configured to use a self-signed development-only certificate.</span></span> <span data-ttu-id="cdf17-254">For production, you need a private SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="cdf17-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="cdf17-255">
<strong>Important SSL Certificate Information</strong>

</span><span class="sxs-lookup"><span data-stu-id="cdf17-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="cdf17-256">The certificate expiration date must be less than 5 years.</span><span class="sxs-lookup"><span data-stu-id="cdf17-256">The certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="cdf17-257">All private certificates require a password.</span><span class="sxs-lookup"><span data-stu-id="cdf17-257">All private certificates require a password.</span></span> <span data-ttu-id="cdf17-258">Know this password and as a best practice, share this password with your administrators.</span><span class="sxs-lookup"><span data-stu-id="cdf17-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="cdf17-259">Self-signed certificates are used in a test/development environment.</span><span class="sxs-lookup"><span data-stu-id="cdf17-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="cdf17-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span><span class="sxs-lookup"><span data-stu-id="cdf17-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="cdf17-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span><span class="sxs-lookup"><span data-stu-id="cdf17-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="cdf17-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span><span class="sxs-lookup"><span data-stu-id="cdf17-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="cdf17-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span><span class="sxs-lookup"><span data-stu-id="cdf17-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="cdf17-264">See <a HREF="#BizTalk">Create a BizTalk Service</a> in this article.</span><span class="sxs-lookup"><span data-stu-id="cdf17-264">See <a HREF="#BizTalk">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="cdf17-265">A new or different certificate can be added after the BizTalk Service is created.</span><span class="sxs-lookup"><span data-stu-id="cdf17-265">A new or different certificate can be added after the BizTalk Service is created.</span></span>
</td>
</tr>
</table>



## <a name="hybrid-connections"></a><span data-ttu-id="cdf17-266">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="cdf17-266">Hybrid Connections</span></span>
<span data-ttu-id="cdf17-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span><span class="sxs-lookup"><span data-stu-id="cdf17-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span></span>

![Hybrid Connections Tab][HybridConnectionTab]

<span data-ttu-id="cdf17-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span><span class="sxs-lookup"><span data-stu-id="cdf17-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="cdf17-270">Hybrid Connections and the BizTalk Adapter Service are different.</span><span class="sxs-lookup"><span data-stu-id="cdf17-270">Hybrid Connections and the BizTalk Adapter Service are different.</span></span> <span data-ttu-id="cdf17-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span><span class="sxs-lookup"><span data-stu-id="cdf17-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="cdf17-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="cdf17-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdf17-273">Next steps</span><span class="sxs-lookup"><span data-stu-id="cdf17-273">Next steps</span></span>
<span data-ttu-id="cdf17-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="cdf17-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="cdf17-275">Your BizTalk Service is ready for your applications.</span><span class="sxs-lookup"><span data-stu-id="cdf17-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="cdf17-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="cdf17-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="cdf17-277">See also</span><span class="sxs-lookup"><span data-stu-id="cdf17-277">See also</span></span>
* [<span data-ttu-id="cdf17-278">BizTalk Services: Editions Chart</span><span class="sxs-lookup"><span data-stu-id="cdf17-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="cdf17-279">BizTalk Services: State Chart</span><span class="sxs-lookup"><span data-stu-id="cdf17-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="cdf17-280">BizTalk Services: Backup and Restore</span><span class="sxs-lookup"><span data-stu-id="cdf17-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="cdf17-281">BizTalk Services: Throttling</span><span class="sxs-lookup"><span data-stu-id="cdf17-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="cdf17-282">BizTalk Services: Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="cdf17-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="cdf17-283">How do I Start Using the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="cdf17-283">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="cdf17-284">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="cdf17-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-provision-services/WABS_HybridConnectionTab.png







