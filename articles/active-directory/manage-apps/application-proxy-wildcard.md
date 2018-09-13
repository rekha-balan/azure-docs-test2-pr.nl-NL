---
title: Wildcard applications in the Azure Active Directory application proxy | Microsoft Docs
description: Learn how to use Wildcard applications in the Azure Active Directory application proxy.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 638ae4c779af3bebb68622ccee6932618d42e4f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855781"
---
# <a name="wildcard-applications-in-the-azure-active-directory-application-proxy"></a><span data-ttu-id="2ccde-103">Wildcard applications in the Azure Active Directory application proxy</span><span class="sxs-lookup"><span data-stu-id="2ccde-103">Wildcard applications in the Azure Active Directory application proxy</span></span> 

<span data-ttu-id="2ccde-104">In Azure Active Directory (Azure AD), configuring a large number of on-premises applications can quickly become unmanageable and introduces unnecessary risks for configuration errors if many of them require the same settings.</span><span class="sxs-lookup"><span data-stu-id="2ccde-104">In Azure Active Directory (Azure AD), configuring a large number of on-premises applications can quickly become unmanageable and introduces unnecessary risks for configuration errors if many of them require the same settings.</span></span> <span data-ttu-id="2ccde-105">With [Azure AD Application Proxy](application-proxy.md), you can address this issue by using wildcard application publishing to publish and manage many applications at once.</span><span class="sxs-lookup"><span data-stu-id="2ccde-105">With [Azure AD Application Proxy](application-proxy.md), you can address this issue by using wildcard application publishing to publish and manage many applications at once.</span></span> <span data-ttu-id="2ccde-106">This is a solution that allows you to:</span><span class="sxs-lookup"><span data-stu-id="2ccde-106">This is a solution that allows you to:</span></span>

-   <span data-ttu-id="2ccde-107">Simplify your administrative overhead</span><span class="sxs-lookup"><span data-stu-id="2ccde-107">Simplify your administrative overhead</span></span>
-   <span data-ttu-id="2ccde-108">Reduce the number of potential configuration errors</span><span class="sxs-lookup"><span data-stu-id="2ccde-108">Reduce the number of potential configuration errors</span></span>
-   <span data-ttu-id="2ccde-109">Enable your users to securely access more resources</span><span class="sxs-lookup"><span data-stu-id="2ccde-109">Enable your users to securely access more resources</span></span>

<span data-ttu-id="2ccde-110">This article provides you with the information you need to configure wildcard application publishing in your environment.</span><span class="sxs-lookup"><span data-stu-id="2ccde-110">This article provides you with the information you need to configure wildcard application publishing in your environment.</span></span>


## <a name="create-a-wildcard-application"></a><span data-ttu-id="2ccde-111">Create a wildcard application</span><span class="sxs-lookup"><span data-stu-id="2ccde-111">Create a wildcard application</span></span> 

<span data-ttu-id="2ccde-112">You can create a wildcard (\*) application if you have a group of applications with the same configuration.</span><span class="sxs-lookup"><span data-stu-id="2ccde-112">You can create a wildcard (\*) application if you have a group of applications with the same configuration.</span></span> <span data-ttu-id="2ccde-113">Potential candidates for a wildcard application are applications sharing the following settings:</span><span class="sxs-lookup"><span data-stu-id="2ccde-113">Potential candidates for a wildcard application are applications sharing the following settings:</span></span>

- <span data-ttu-id="2ccde-114">The group of users having access to them</span><span class="sxs-lookup"><span data-stu-id="2ccde-114">The group of users having access to them</span></span>
- <span data-ttu-id="2ccde-115">The SSO method</span><span class="sxs-lookup"><span data-stu-id="2ccde-115">The SSO method</span></span>
- <span data-ttu-id="2ccde-116">The access protocol (http, https)</span><span class="sxs-lookup"><span data-stu-id="2ccde-116">The access protocol (http, https)</span></span>

<span data-ttu-id="2ccde-117">You can publish applications with wildcards if both, the internal and external URLs are in the following format:</span><span class="sxs-lookup"><span data-stu-id="2ccde-117">You can publish applications with wildcards if both, the internal and external URLs are in the following format:</span></span>

> <span data-ttu-id="2ccde-118">http(s)://\*.\<domain\></span><span class="sxs-lookup"><span data-stu-id="2ccde-118">http(s)://\*.\<domain\></span></span>

<span data-ttu-id="2ccde-119">For example: `http(s)://*.adventure-works.com`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-119">For example: `http(s)://*.adventure-works.com`.</span></span> <span data-ttu-id="2ccde-120">While the internal and external URLs can use different domains, as a best practice, they should be same.</span><span class="sxs-lookup"><span data-stu-id="2ccde-120">While the internal and external URLs can use different domains, as a best practice, they should be same.</span></span> <span data-ttu-id="2ccde-121">When publishing the application, you see an error if one of the URLs doesn't have a wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-121">When publishing the application, you see an error if one of the URLs doesn't have a wildcard.</span></span>

<span data-ttu-id="2ccde-122">If you have additional applications with different configuration settings, you must publish these exceptions as separate applications to overwrite the defaults set for the wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-122">If you have additional applications with different configuration settings, you must publish these exceptions as separate applications to overwrite the defaults set for the wildcard.</span></span> <span data-ttu-id="2ccde-123">Applications without a wildcard do always take precedence over wildcard applications.</span><span class="sxs-lookup"><span data-stu-id="2ccde-123">Applications without a wildcard do always take precedence over wildcard applications.</span></span> <span data-ttu-id="2ccde-124">From the configuration perspective, these are "just" regular applications.</span><span class="sxs-lookup"><span data-stu-id="2ccde-124">From the configuration perspective, these are "just" regular applications.</span></span>

<span data-ttu-id="2ccde-125">Creating a wildcard application is based on the same [application publishing flow](application-proxy-publish-azure-portal.md) that is available for all other applications.</span><span class="sxs-lookup"><span data-stu-id="2ccde-125">Creating a wildcard application is based on the same [application publishing flow](application-proxy-publish-azure-portal.md) that is available for all other applications.</span></span> <span data-ttu-id="2ccde-126">The only difference is that you include a wildcard in the URLs and potentially the SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="2ccde-126">The only difference is that you include a wildcard in the URLs and potentially the SSO configuration.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2ccde-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ccde-127">Prerequisites</span></span>

### <a name="custom-domains"></a><span data-ttu-id="2ccde-128">Custom domains</span><span class="sxs-lookup"><span data-stu-id="2ccde-128">Custom domains</span></span>

<span data-ttu-id="2ccde-129">While [custom domains](application-proxy-configure-custom-domain.md) are optional for all other applications, they are a prerequisite for wildcard applications.</span><span class="sxs-lookup"><span data-stu-id="2ccde-129">While [custom domains](application-proxy-configure-custom-domain.md) are optional for all other applications, they are a prerequisite for wildcard applications.</span></span> <span data-ttu-id="2ccde-130">Creating custom domains requires you to:</span><span class="sxs-lookup"><span data-stu-id="2ccde-130">Creating custom domains requires you to:</span></span>

1. <span data-ttu-id="2ccde-131">Create a verified domain within Azure</span><span class="sxs-lookup"><span data-stu-id="2ccde-131">Create a verified domain within Azure</span></span> 
2. <span data-ttu-id="2ccde-132">Upload an SSL certificate in the PFX format to your application proxy.</span><span class="sxs-lookup"><span data-stu-id="2ccde-132">Upload an SSL certificate in the PFX format to your application proxy.</span></span>

<span data-ttu-id="2ccde-133">You should consider using a wildcard certificate to match the application you plan to create.</span><span class="sxs-lookup"><span data-stu-id="2ccde-133">You should consider using a wildcard certificate to match the application you plan to create.</span></span> <span data-ttu-id="2ccde-134">Alternatively, you can also use a certificate that only lists specific applications.</span><span class="sxs-lookup"><span data-stu-id="2ccde-134">Alternatively, you can also use a certificate that only lists specific applications.</span></span> <span data-ttu-id="2ccde-135">In this case, only the applications listed in the certificate will be accessible through this wildcard application.</span><span class="sxs-lookup"><span data-stu-id="2ccde-135">In this case, only the applications listed in the certificate will be accessible through this wildcard application.</span></span>

<span data-ttu-id="2ccde-136">For security reasons, this is a hard requirement and we will not support wildcards for applications that cannot use a custom domain for the external URL.</span><span class="sxs-lookup"><span data-stu-id="2ccde-136">For security reasons, this is a hard requirement and we will not support wildcards for applications that cannot use a custom domain for the external URL.</span></span>

### <a name="dns-updates"></a><span data-ttu-id="2ccde-137">DNS updates</span><span class="sxs-lookup"><span data-stu-id="2ccde-137">DNS updates</span></span>

<span data-ttu-id="2ccde-138">When using custom domains, you need to create a DNS entry with a CNAME record for the external URL (for example,  `*.adventure-works.com`) pointing to the external URL of the application proxy endpoint.For wildcard applications, the CNAME record needs to point to the relevant external URLs:</span><span class="sxs-lookup"><span data-stu-id="2ccde-138">When using custom domains, you need to create a DNS entry with a CNAME record for the external URL (for example,  `*.adventure-works.com`) pointing to the external URL of the application proxy endpoint.For wildcard applications, the CNAME record needs to point to the relevant external URLs:</span></span>

> `<yourAADTenantId>.tenant.runtime.msappproxy.net`

<span data-ttu-id="2ccde-139">To confirm that you have configured your CNAME correctly, you can use [nslookup](https://docs.microsoft.com/windows-server/administration/windows-commands/nslookup) on one of the target endpoints, for example, `expenses.adventure-works.com`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-139">To confirm that you have configured your CNAME correctly, you can use [nslookup](https://docs.microsoft.com/windows-server/administration/windows-commands/nslookup) on one of the target endpoints, for example, `expenses.adventure-works.com`.</span></span>  <span data-ttu-id="2ccde-140">Your response should include the already mentioned alias (`<yourAADTenantId>.tenant.runtime.msappproxy.net`).</span><span class="sxs-lookup"><span data-stu-id="2ccde-140">Your response should include the already mentioned alias (`<yourAADTenantId>.tenant.runtime.msappproxy.net`).</span></span>


## <a name="considerations"></a><span data-ttu-id="2ccde-141">Considerations</span><span class="sxs-lookup"><span data-stu-id="2ccde-141">Considerations</span></span>


### <a name="accepted-formats"></a><span data-ttu-id="2ccde-142">Accepted formats</span><span class="sxs-lookup"><span data-stu-id="2ccde-142">Accepted formats</span></span>

<span data-ttu-id="2ccde-143">For wildcard applications, the **Internal URL** must be formatted as `http(s)://*.<domain>`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-143">For wildcard applications, the **Internal URL** must be formatted as `http(s)://*.<domain>`.</span></span> 

![AppId](./media/application-proxy-wildcard/22.png)


<span data-ttu-id="2ccde-145">When you configure an **External URL**, you must use the following format: `https://*.<custom domain>`</span><span class="sxs-lookup"><span data-stu-id="2ccde-145">When you configure an **External URL**, you must use the following format: `https://*.<custom domain>`</span></span> 

![AppId](./media/application-proxy-wildcard/21.png)

<span data-ttu-id="2ccde-147">Other positions of the wildcard, multiple wildcards, or other regex strings are not supported and are causing errors.</span><span class="sxs-lookup"><span data-stu-id="2ccde-147">Other positions of the wildcard, multiple wildcards, or other regex strings are not supported and are causing errors.</span></span>


### <a name="excluding-applications-from-the-wildcard"></a><span data-ttu-id="2ccde-148">Excluding applications from the wildcard</span><span class="sxs-lookup"><span data-stu-id="2ccde-148">Excluding applications from the wildcard</span></span>

<span data-ttu-id="2ccde-149">You can exclude an application from the wildcard application by</span><span class="sxs-lookup"><span data-stu-id="2ccde-149">You can exclude an application from the wildcard application by</span></span>

- <span data-ttu-id="2ccde-150">Publishing the exception application as regular application</span><span class="sxs-lookup"><span data-stu-id="2ccde-150">Publishing the exception application as regular application</span></span> 
- <span data-ttu-id="2ccde-151">Enabling the wildcard only for specific applications through your DNS settings</span><span class="sxs-lookup"><span data-stu-id="2ccde-151">Enabling the wildcard only for specific applications through your DNS settings</span></span>  


<span data-ttu-id="2ccde-152">Publishing an application as regular application is the preferred method to exclude an application from a wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-152">Publishing an application as regular application is the preferred method to exclude an application from a wildcard.</span></span> <span data-ttu-id="2ccde-153">You should publish the excluded applications before the wildcard applications to ensure that your exceptions are enforced from the beginning.</span><span class="sxs-lookup"><span data-stu-id="2ccde-153">You should publish the excluded applications before the wildcard applications to ensure that your exceptions are enforced from the beginning.</span></span> <span data-ttu-id="2ccde-154">The most specific application will always take precedence – an application published as `budgets.finance.adventure-works.com` takes precedence over the application `*.finance.adventure-works.com`, which in turn takes precedence over the application `*.adventure-works.com`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-154">The most specific application will always take precedence – an application published as `budgets.finance.adventure-works.com` takes precedence over the application `*.finance.adventure-works.com`, which in turn takes precedence over the application `*.adventure-works.com`.</span></span> 

<span data-ttu-id="2ccde-155">You can also limit the wildcard to only work for specific applications through your DNS management.</span><span class="sxs-lookup"><span data-stu-id="2ccde-155">You can also limit the wildcard to only work for specific applications through your DNS management.</span></span> <span data-ttu-id="2ccde-156">As a best practice, you should create a CNAME entry that includes a wildcard and matches the format of the external URL you have configured.</span><span class="sxs-lookup"><span data-stu-id="2ccde-156">As a best practice, you should create a CNAME entry that includes a wildcard and matches the format of the external URL you have configured.</span></span> <span data-ttu-id="2ccde-157">However, you can instead point specific application URLs to the wildcards.</span><span class="sxs-lookup"><span data-stu-id="2ccde-157">However, you can instead point specific application URLs to the wildcards.</span></span> <span data-ttu-id="2ccde-158">For example, instead of `*.adventure-works.com`, point `hr.adventure-works.com`, `expenses.adventure-works.com` and `travel.adventure-works.com individually` to `000aa000-11b1-2ccc-d333-4444eee4444e.tenant.runtime.msappproxy.net`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-158">For example, instead of `*.adventure-works.com`, point `hr.adventure-works.com`, `expenses.adventure-works.com` and `travel.adventure-works.com individually` to `000aa000-11b1-2ccc-d333-4444eee4444e.tenant.runtime.msappproxy.net`.</span></span> 

<span data-ttu-id="2ccde-159">If you use this option, you also need another CNAME entry for the value `AppId.domain`, for example, `00000000-1a11-22b2-c333-444d4d4dd444.adventure-works.com`, also pointing to the same location.</span><span class="sxs-lookup"><span data-stu-id="2ccde-159">If you use this option, you also need another CNAME entry for the value `AppId.domain`, for example, `00000000-1a11-22b2-c333-444d4d4dd444.adventure-works.com`, also pointing to the same location.</span></span> <span data-ttu-id="2ccde-160">You can find the **AppId** on the application properties page of the wildcard application:</span><span class="sxs-lookup"><span data-stu-id="2ccde-160">You can find the **AppId** on the application properties page of the wildcard application:</span></span>

![AppId](./media/application-proxy-wildcard/01.png)



### <a name="setting-the-homepage-url-for-the-myapps-panel"></a><span data-ttu-id="2ccde-162">Setting the homepage URL for the MyApps panel</span><span class="sxs-lookup"><span data-stu-id="2ccde-162">Setting the homepage URL for the MyApps panel</span></span>

<span data-ttu-id="2ccde-163">The wildcard application is represented with just one tile in the [MyApps panel](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2ccde-163">The wildcard application is represented with just one tile in the [MyApps panel](https://myapps.microsoft.com).</span></span> <span data-ttu-id="2ccde-164">By default this tile is hidden.</span><span class="sxs-lookup"><span data-stu-id="2ccde-164">By default this tile is hidden.</span></span> <span data-ttu-id="2ccde-165">To show the tile and have users land on a specific page:</span><span class="sxs-lookup"><span data-stu-id="2ccde-165">To show the tile and have users land on a specific page:</span></span>

1. <span data-ttu-id="2ccde-166">Follow the guidelines for [setting a homepage URL](application-proxy-configure-custom-home-page.md).</span><span class="sxs-lookup"><span data-stu-id="2ccde-166">Follow the guidelines for [setting a homepage URL](application-proxy-configure-custom-home-page.md).</span></span>
2. <span data-ttu-id="2ccde-167">Set **Show Application** to **true** on the application properties page.</span><span class="sxs-lookup"><span data-stu-id="2ccde-167">Set **Show Application** to **true** on the application properties page.</span></span>

### <a name="kerberos-constrained-delegation"></a><span data-ttu-id="2ccde-168">Kerberos constrained delegation</span><span class="sxs-lookup"><span data-stu-id="2ccde-168">Kerberos constrained delegation</span></span>

<span data-ttu-id="2ccde-169">For applications using [kerberos constrained delegation (KCD) as the SSO method](application-proxy-configure-single-sign-on-with-kcd.md), the SPN listed for the SSO method may also need a wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-169">For applications using [kerberos constrained delegation (KCD) as the SSO method](application-proxy-configure-single-sign-on-with-kcd.md), the SPN listed for the SSO method may also need a wildcard.</span></span> <span data-ttu-id="2ccde-170">For example, the SPN could be: `HTTP/*.adventure-works.com`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-170">For example, the SPN could be: `HTTP/*.adventure-works.com`.</span></span> <span data-ttu-id="2ccde-171">You still need to have the individual SPNs configured on your backend servers (for example, `http://expenses.adventure-works.com and HTTP/travel.adventure-works.com`).</span><span class="sxs-lookup"><span data-stu-id="2ccde-171">You still need to have the individual SPNs configured on your backend servers (for example, `http://expenses.adventure-works.com and HTTP/travel.adventure-works.com`).</span></span>



## <a name="scenario-1-general-wildcard-application"></a><span data-ttu-id="2ccde-172">Scenario 1: General wildcard application</span><span class="sxs-lookup"><span data-stu-id="2ccde-172">Scenario 1: General wildcard application</span></span>

<span data-ttu-id="2ccde-173">In this scenario, you have three different applications you want to publish:</span><span class="sxs-lookup"><span data-stu-id="2ccde-173">In this scenario, you have three different applications you want to publish:</span></span>

- `expenses.adventure-works.com`
- `hr.adventure-works.com`
- `travel.adventure-works.com`

<span data-ttu-id="2ccde-174">All three applications:</span><span class="sxs-lookup"><span data-stu-id="2ccde-174">All three applications:</span></span>

- <span data-ttu-id="2ccde-175">Are used by all your users</span><span class="sxs-lookup"><span data-stu-id="2ccde-175">Are used by all your users</span></span>
- <span data-ttu-id="2ccde-176">Use *Integrated Windows Authentication*</span><span class="sxs-lookup"><span data-stu-id="2ccde-176">Use *Integrated Windows Authentication*</span></span> 
- <span data-ttu-id="2ccde-177">Have the same properties</span><span class="sxs-lookup"><span data-stu-id="2ccde-177">Have the same properties</span></span>


<span data-ttu-id="2ccde-178">You can publish the wildcard application using the steps outlined in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2ccde-178">You can publish the wildcard application using the steps outlined in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span> <span data-ttu-id="2ccde-179">This scenario assumes:</span><span class="sxs-lookup"><span data-stu-id="2ccde-179">This scenario assumes:</span></span>

- <span data-ttu-id="2ccde-180">A tenant with the following ID: `000aa000-11b1-2ccc-d333-4444eee4444e`</span><span class="sxs-lookup"><span data-stu-id="2ccde-180">A tenant with the following ID: `000aa000-11b1-2ccc-d333-4444eee4444e`</span></span> 

- <span data-ttu-id="2ccde-181">A verified domain called `adventure-works.com` has been configured.</span><span class="sxs-lookup"><span data-stu-id="2ccde-181">A verified domain called `adventure-works.com` has been configured.</span></span>

- <span data-ttu-id="2ccde-182">A **CNAME** entry that points `*.adventure-works.com` to `000aa000-11b1-2ccc-d333-4444eee4444e.tenant.runtime.msappproxy.net` has been created.</span><span class="sxs-lookup"><span data-stu-id="2ccde-182">A **CNAME** entry that points `*.adventure-works.com` to `000aa000-11b1-2ccc-d333-4444eee4444e.tenant.runtime.msappproxy.net` has been created.</span></span>

<span data-ttu-id="2ccde-183">Following the [documented steps](application-proxy-publish-azure-portal.md), you create a new application proxy application in your tenant.</span><span class="sxs-lookup"><span data-stu-id="2ccde-183">Following the [documented steps](application-proxy-publish-azure-portal.md), you create a new application proxy application in your tenant.</span></span> <span data-ttu-id="2ccde-184">In this example, the wildcard is in the following fields:</span><span class="sxs-lookup"><span data-stu-id="2ccde-184">In this example, the wildcard is in the following fields:</span></span>

- <span data-ttu-id="2ccde-185">Internal URL:</span><span class="sxs-lookup"><span data-stu-id="2ccde-185">Internal URL:</span></span>

    ![Internal URL](./media/application-proxy-wildcard/42.png)


- <span data-ttu-id="2ccde-187">External URL:</span><span class="sxs-lookup"><span data-stu-id="2ccde-187">External URL:</span></span>

    ![External URL](./media/application-proxy-wildcard/43.png)

 
- <span data-ttu-id="2ccde-189">Internal Application SPN:</span><span class="sxs-lookup"><span data-stu-id="2ccde-189">Internal Application SPN:</span></span> 

    ![SPN configuration](./media/application-proxy-wildcard/44.png)


<span data-ttu-id="2ccde-191">By publishing the wildcard application, you can now access your three applications by navigating to the URLs you are used to (for example, `travel.adventure-works.com`).</span><span class="sxs-lookup"><span data-stu-id="2ccde-191">By publishing the wildcard application, you can now access your three applications by navigating to the URLs you are used to (for example, `travel.adventure-works.com`).</span></span>

<span data-ttu-id="2ccde-192">The configuration implements the following structure:</span><span class="sxs-lookup"><span data-stu-id="2ccde-192">The configuration implements the following structure:</span></span>

![AppId](./media/application-proxy-wildcard/05.png)

| <span data-ttu-id="2ccde-194">Color</span><span class="sxs-lookup"><span data-stu-id="2ccde-194">Color</span></span> | <span data-ttu-id="2ccde-195">Description</span><span class="sxs-lookup"><span data-stu-id="2ccde-195">Description</span></span> |
| ---   | ---         |
| <span data-ttu-id="2ccde-196">Blue</span><span class="sxs-lookup"><span data-stu-id="2ccde-196">Blue</span></span>  | <span data-ttu-id="2ccde-197">Applications explicitly published and visible in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2ccde-197">Applications explicitly published and visible in the Azure Portal.</span></span> |
| <span data-ttu-id="2ccde-198">Gray</span><span class="sxs-lookup"><span data-stu-id="2ccde-198">Gray</span></span>  | <span data-ttu-id="2ccde-199">Applications you can accessible through the parent application.</span><span class="sxs-lookup"><span data-stu-id="2ccde-199">Applications you can accessible through the parent application.</span></span> |




## <a name="scenario-2-general-wildcard-application-with-exception"></a><span data-ttu-id="2ccde-200">Scenario 2: General wildcard application with exception</span><span class="sxs-lookup"><span data-stu-id="2ccde-200">Scenario 2: General wildcard application with exception</span></span>

<span data-ttu-id="2ccde-201">In this scenario, you have in addition to the three general applications another application, `finance.adventure-works.com`, which should only be accessible by Finance division.</span><span class="sxs-lookup"><span data-stu-id="2ccde-201">In this scenario, you have in addition to the three general applications another application, `finance.adventure-works.com`, which should only be accessible by Finance division.</span></span> <span data-ttu-id="2ccde-202">With the current application structure, your finance application would be accessible through the wildcard application and by all employees.</span><span class="sxs-lookup"><span data-stu-id="2ccde-202">With the current application structure, your finance application would be accessible through the wildcard application and by all employees.</span></span> <span data-ttu-id="2ccde-203">To change this, you exclude your application from your wildcard by configuring Finance as a separate application with more restrictive permissions.</span><span class="sxs-lookup"><span data-stu-id="2ccde-203">To change this, you exclude your application from your wildcard by configuring Finance as a separate application with more restrictive permissions.</span></span>



<span data-ttu-id="2ccde-204">You need to make sure that a CNAME records exist that points `finance.adventure-works.com` to the application specific endpoint, specified on the Application Proxy page for the application.</span><span class="sxs-lookup"><span data-stu-id="2ccde-204">You need to make sure that a CNAME records exist that points `finance.adventure-works.com` to the application specific endpoint, specified on the Application Proxy page for the application.</span></span> <span data-ttu-id="2ccde-205">For this scenario, `finance.adventure-works.com` points to `https://finance-awcycles.msappproxy.net/`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-205">For this scenario, `finance.adventure-works.com` points to `https://finance-awcycles.msappproxy.net/`.</span></span> 

<span data-ttu-id="2ccde-206">Following the [documented steps](application-proxy-publish-azure-portal.md), this scenario requires the following settings:</span><span class="sxs-lookup"><span data-stu-id="2ccde-206">Following the [documented steps](application-proxy-publish-azure-portal.md), this scenario requires the following settings:</span></span>


- <span data-ttu-id="2ccde-207">In the **Internal URL**, you set **finance** instead of a wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-207">In the **Internal URL**, you set **finance** instead of a wildcard.</span></span> 

    ![Internal URL](./media/application-proxy-wildcard/52.png)

- <span data-ttu-id="2ccde-209">In the **External URL**, you set **finance** instead of a wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-209">In the **External URL**, you set **finance** instead of a wildcard.</span></span> 

    ![External URL](./media/application-proxy-wildcard/53.png)

- <span data-ttu-id="2ccde-211">Internal Application SPN you set **finance** instead of a wildcard.</span><span class="sxs-lookup"><span data-stu-id="2ccde-211">Internal Application SPN you set **finance** instead of a wildcard.</span></span>

    ![SPN configuration](./media/application-proxy-wildcard/54.png)


<span data-ttu-id="2ccde-213">This configuration implements the following scenario:</span><span class="sxs-lookup"><span data-stu-id="2ccde-213">This configuration implements the following scenario:</span></span>

![Scenario](./media/application-proxy-wildcard/09.png)

<span data-ttu-id="2ccde-215">Because `finance.adventure-works.com` is a more specific URL than `*.adventure-works.com`, it takes precedence.</span><span class="sxs-lookup"><span data-stu-id="2ccde-215">Because `finance.adventure-works.com` is a more specific URL than `*.adventure-works.com`, it takes precedence.</span></span> <span data-ttu-id="2ccde-216">Users navigating to `finance.adventure-works.com` have the experience specified in the Finance Resources application.</span><span class="sxs-lookup"><span data-stu-id="2ccde-216">Users navigating to `finance.adventure-works.com` have the experience specified in the Finance Resources application.</span></span> <span data-ttu-id="2ccde-217">In this case, only finance employees are able to access `finance.adventure-works.com`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-217">In this case, only finance employees are able to access `finance.adventure-works.com`.</span></span>

<span data-ttu-id="2ccde-218">If you have multiple applications published for finance and you have `finance.adventure-works.com` as a verified domain, you could publish another wildcard application `*.finance.adventure-works.com`.</span><span class="sxs-lookup"><span data-stu-id="2ccde-218">If you have multiple applications published for finance and you have `finance.adventure-works.com` as a verified domain, you could publish another wildcard application `*.finance.adventure-works.com`.</span></span> <span data-ttu-id="2ccde-219">Because this is more specific than the generic `*.adventure-works.com`, it takes precedence if a user accesses an application in the finance domain.</span><span class="sxs-lookup"><span data-stu-id="2ccde-219">Because this is more specific than the generic `*.adventure-works.com`, it takes precedence if a user accesses an application in the finance domain.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2ccde-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ccde-220">Next steps</span></span>

<span data-ttu-id="2ccde-221">For more information about:</span><span class="sxs-lookup"><span data-stu-id="2ccde-221">For more information about:</span></span>

- <span data-ttu-id="2ccde-222">**Custom domains**, see [Working with custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="2ccde-222">**Custom domains**, see [Working with custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span></span>

- <span data-ttu-id="2ccde-223">**Publishing applications**, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2ccde-223">**Publishing applications**, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md)</span></span>


