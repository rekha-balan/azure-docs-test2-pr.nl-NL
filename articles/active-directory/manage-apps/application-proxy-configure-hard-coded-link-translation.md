---
title: Translate links and URLs Azure AD App Proxy | Microsoft Docs
description: Covers the basics about Azure AD Application Proxy connectors.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/04/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 618df9b4bcc4a1b6f44d9cabc29c797a2cabcc80
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857857"
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a><span data-ttu-id="59fa2-103">Redirect hardcoded links for apps published with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="59fa2-103">Redirect hardcoded links for apps published with Azure AD Application Proxy</span></span>

<span data-ttu-id="59fa2-104">Azure AD Application Proxy makes your on-premises apps available to users who are remote or on their own devices.</span><span class="sxs-lookup"><span data-stu-id="59fa2-104">Azure AD Application Proxy makes your on-premises apps available to users who are remote or on their own devices.</span></span> <span data-ttu-id="59fa2-105">Some apps, however, were developed with local links embedded in the HTML.</span><span class="sxs-lookup"><span data-stu-id="59fa2-105">Some apps, however, were developed with local links embedded in the HTML.</span></span> <span data-ttu-id="59fa2-106">These links don't work correctly when the app is used remotely.</span><span class="sxs-lookup"><span data-stu-id="59fa2-106">These links don't work correctly when the app is used remotely.</span></span> <span data-ttu-id="59fa2-107">When you have several on-premises applications point to each other, your users expect the links to keep working when they're not at the office.</span><span class="sxs-lookup"><span data-stu-id="59fa2-107">When you have several on-premises applications point to each other, your users expect the links to keep working when they're not at the office.</span></span> 

<span data-ttu-id="59fa2-108">The best way to make sure that links work the same both inside and outside of your corporate network is to configure the external URLs of your apps to be the same as their internal URLs.</span><span class="sxs-lookup"><span data-stu-id="59fa2-108">The best way to make sure that links work the same both inside and outside of your corporate network is to configure the external URLs of your apps to be the same as their internal URLs.</span></span> <span data-ttu-id="59fa2-109">Use [custom domains](application-proxy-configure-custom-domain.md) to configure your external URLs to have your corporate domain name instead of the default application proxy domain.</span><span class="sxs-lookup"><span data-stu-id="59fa2-109">Use [custom domains](application-proxy-configure-custom-domain.md) to configure your external URLs to have your corporate domain name instead of the default application proxy domain.</span></span>


<span data-ttu-id="59fa2-110">If you can't use custom domains in your tenant, there are several other options for providing this functionality.</span><span class="sxs-lookup"><span data-stu-id="59fa2-110">If you can't use custom domains in your tenant, there are several other options for providing this functionality.</span></span> <span data-ttu-id="59fa2-111">All of these are also compatible with custom domains and each other, so you can configure custom domains and other solutions if needed.</span><span class="sxs-lookup"><span data-stu-id="59fa2-111">All of these are also compatible with custom domains and each other, so you can configure custom domains and other solutions if needed.</span></span> 

<span data-ttu-id="59fa2-112">**Option 1: Use the Managed Browser** – This solution is only applicable if you plan to recommend or require that users access the application through the Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="59fa2-112">**Option 1: Use the Managed Browser** – This solution is only applicable if you plan to recommend or require that users access the application through the Intune Managed Browser.</span></span> <span data-ttu-id="59fa2-113">It will handle all published URLs.</span><span class="sxs-lookup"><span data-stu-id="59fa2-113">It will handle all published URLs.</span></span> 

<span data-ttu-id="59fa2-114">**Option 2: Use the MyApps Extension** – This solution requires users to install a client-side browser extension, but it will handle all published URLs and works with most popular browsers.</span><span class="sxs-lookup"><span data-stu-id="59fa2-114">**Option 2: Use the MyApps Extension** – This solution requires users to install a client-side browser extension, but it will handle all published URLs and works with most popular browsers.</span></span> 

<span data-ttu-id="59fa2-115">**Option 3: Use the link translation setting** – This is an admin side setting that is invisible to users.</span><span class="sxs-lookup"><span data-stu-id="59fa2-115">**Option 3: Use the link translation setting** – This is an admin side setting that is invisible to users.</span></span> <span data-ttu-id="59fa2-116">However, it will only handle URLs in HTML and CSS.</span><span class="sxs-lookup"><span data-stu-id="59fa2-116">However, it will only handle URLs in HTML and CSS.</span></span> <span data-ttu-id="59fa2-117">Hard-coded internal URLs generated through Javascript (for example) will not work.</span><span class="sxs-lookup"><span data-stu-id="59fa2-117">Hard-coded internal URLs generated through Javascript (for example) will not work.</span></span>  

<span data-ttu-id="59fa2-118">These three features keep your links working no matter where your users are.</span><span class="sxs-lookup"><span data-stu-id="59fa2-118">These three features keep your links working no matter where your users are.</span></span> <span data-ttu-id="59fa2-119">When you have apps that point directly to internal endpoints or ports, you can map these internal URLs to the published external Application Proxy URLs.</span><span class="sxs-lookup"><span data-stu-id="59fa2-119">When you have apps that point directly to internal endpoints or ports, you can map these internal URLs to the published external Application Proxy URLs.</span></span> 

 
> [!NOTE]
> <span data-ttu-id="59fa2-120">The last option is only for tenants that, for whatever reason, can't use custom domains to have the same  internal and external URLs for their apps.</span><span class="sxs-lookup"><span data-stu-id="59fa2-120">The last option is only for tenants that, for whatever reason, can't use custom domains to have the same  internal and external URLs for their apps.</span></span> <span data-ttu-id="59fa2-121">Before you enable this feature, see if [custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md) can work for you.</span><span class="sxs-lookup"><span data-stu-id="59fa2-121">Before you enable this feature, see if [custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md) can work for you.</span></span> 

><span data-ttu-id="59fa2-122">Or, if the application you need to configure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) for another approach to mapping links.</span><span class="sxs-lookup"><span data-stu-id="59fa2-122">Or, if the application you need to configure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) for another approach to mapping links.</span></span> 

 
### <a name="option-1-intune-managed-browser-integration"></a><span data-ttu-id="59fa2-123">Option 1: Intune Managed Browser Integration</span><span class="sxs-lookup"><span data-stu-id="59fa2-123">Option 1: Intune Managed Browser Integration</span></span> 

<span data-ttu-id="59fa2-124">You can use the Intune Managed Browser to further protect your application and content.</span><span class="sxs-lookup"><span data-stu-id="59fa2-124">You can use the Intune Managed Browser to further protect your application and content.</span></span> <span data-ttu-id="59fa2-125">To use this solution, you need to require/recommend users access the application through the Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="59fa2-125">To use this solution, you need to require/recommend users access the application through the Intune Managed Browser.</span></span> <span data-ttu-id="59fa2-126">All internal URLs published with Application Proxy will be recognized by the Managed Browser and redirected to the corresponding external URL.</span><span class="sxs-lookup"><span data-stu-id="59fa2-126">All internal URLs published with Application Proxy will be recognized by the Managed Browser and redirected to the corresponding external URL.</span></span> <span data-ttu-id="59fa2-127">This ensures that all the hard-coded internal URLs work, and if a user goes to the browser and directly types the internal URL, it works even if the user is remote.</span><span class="sxs-lookup"><span data-stu-id="59fa2-127">This ensures that all the hard-coded internal URLs work, and if a user goes to the browser and directly types the internal URL, it works even if the user is remote.</span></span>  

<span data-ttu-id="59fa2-128">To learn more, including how to configure this option, please see the [Managed Browser](https://docs.microsoft.com/intune/app-configuration-managed-browser) documentation.</span><span class="sxs-lookup"><span data-stu-id="59fa2-128">To learn more, including how to configure this option, please see the [Managed Browser](https://docs.microsoft.com/intune/app-configuration-managed-browser) documentation.</span></span>  

### <a name="option-2-myapps-browser-extension"></a><span data-ttu-id="59fa2-129">Option 2: MyApps Browser Extension</span><span class="sxs-lookup"><span data-stu-id="59fa2-129">Option 2: MyApps Browser Extension</span></span> 

<span data-ttu-id="59fa2-130">With the MyApps Browser Extension, all internal URLs published with Application Proxy are recognized by the extension and redirected to the corresponding external URL.</span><span class="sxs-lookup"><span data-stu-id="59fa2-130">With the MyApps Browser Extension, all internal URLs published with Application Proxy are recognized by the extension and redirected to the corresponding external URL.</span></span> <span data-ttu-id="59fa2-131">This ensures that all the hard-coded internal URLs work, and if a user goes to the browser's address bar and directly types the internal URL, it works even if the user is remote.</span><span class="sxs-lookup"><span data-stu-id="59fa2-131">This ensures that all the hard-coded internal URLs work, and if a user goes to the browser's address bar and directly types the internal URL, it works even if the user is remote.</span></span>  

<span data-ttu-id="59fa2-132">To use this feature, the user needs to download the extension and be logged in.</span><span class="sxs-lookup"><span data-stu-id="59fa2-132">To use this feature, the user needs to download the extension and be logged in.</span></span> <span data-ttu-id="59fa2-133">There is no other configuration needed for admins or the users.</span><span class="sxs-lookup"><span data-stu-id="59fa2-133">There is no other configuration needed for admins or the users.</span></span> 

 

### <a name="option-3-link-translation-setting"></a><span data-ttu-id="59fa2-134">Option 3: Link Translation Setting</span><span class="sxs-lookup"><span data-stu-id="59fa2-134">Option 3: Link Translation Setting</span></span> 

<span data-ttu-id="59fa2-135">When link translation is enabled, the Application Proxy service searches through HTML and CSS for published internal links and translates them so that your users get an uninterrupted experience.</span><span class="sxs-lookup"><span data-stu-id="59fa2-135">When link translation is enabled, the Application Proxy service searches through HTML and CSS for published internal links and translates them so that your users get an uninterrupted experience.</span></span> 



## <a name="how-link-translation-works"></a><span data-ttu-id="59fa2-136">How link translation works</span><span class="sxs-lookup"><span data-stu-id="59fa2-136">How link translation works</span></span>

<span data-ttu-id="59fa2-137">After authentication, when the proxy server passes the application data to the user, Application Proxy scans the application for hardcoded links and replaces them with their respective, published external URLs.</span><span class="sxs-lookup"><span data-stu-id="59fa2-137">After authentication, when the proxy server passes the application data to the user, Application Proxy scans the application for hardcoded links and replaces them with their respective, published external URLs.</span></span>

<span data-ttu-id="59fa2-138">Application Proxy assumes that applications are encoded in UTF-8.</span><span class="sxs-lookup"><span data-stu-id="59fa2-138">Application Proxy assumes that applications are encoded in UTF-8.</span></span> <span data-ttu-id="59fa2-139">If that's not the case, specify the encoding type in an http response header, like `Content-Type:text/html;charset=utf-8`.</span><span class="sxs-lookup"><span data-stu-id="59fa2-139">If that's not the case, specify the encoding type in an http response header, like `Content-Type:text/html;charset=utf-8`.</span></span>

### <a name="which-links-are-affected"></a><span data-ttu-id="59fa2-140">Which links are affected?</span><span class="sxs-lookup"><span data-stu-id="59fa2-140">Which links are affected?</span></span>

<span data-ttu-id="59fa2-141">The link translation feature only looks for links that are in code tags in the body of an app.</span><span class="sxs-lookup"><span data-stu-id="59fa2-141">The link translation feature only looks for links that are in code tags in the body of an app.</span></span> <span data-ttu-id="59fa2-142">Application Proxy has a separate feature for translating cookies or URLs in headers.</span><span class="sxs-lookup"><span data-stu-id="59fa2-142">Application Proxy has a separate feature for translating cookies or URLs in headers.</span></span> 

<span data-ttu-id="59fa2-143">There are two common types of internal links in on-premises applications:</span><span class="sxs-lookup"><span data-stu-id="59fa2-143">There are two common types of internal links in on-premises applications:</span></span>

- <span data-ttu-id="59fa2-144">**Relative internal links** that point to a shared resource in a local file structure like `/claims/claims.html`.</span><span class="sxs-lookup"><span data-stu-id="59fa2-144">**Relative internal links** that point to a shared resource in a local file structure like `/claims/claims.html`.</span></span> <span data-ttu-id="59fa2-145">These links automatically work in apps that are published through Application Proxy, and continue to work with or without link translation.</span><span class="sxs-lookup"><span data-stu-id="59fa2-145">These links automatically work in apps that are published through Application Proxy, and continue to work with or without link translation.</span></span> 
- <span data-ttu-id="59fa2-146">**Hardcoded internal links** to other on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`.</span><span class="sxs-lookup"><span data-stu-id="59fa2-146">**Hardcoded internal links** to other on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`.</span></span> <span data-ttu-id="59fa2-147">The link translation feature works on hardcoded internal links, and changes them to point to the external URLs that remote users need to go through.</span><span class="sxs-lookup"><span data-stu-id="59fa2-147">The link translation feature works on hardcoded internal links, and changes them to point to the external URLs that remote users need to go through.</span></span>

### <a name="how-do-apps-link-to-each-other"></a><span data-ttu-id="59fa2-148">How do apps link to each other?</span><span class="sxs-lookup"><span data-stu-id="59fa2-148">How do apps link to each other?</span></span>

<span data-ttu-id="59fa2-149">Link translation is enabled for each application, so that you have control over the user experience at the per-app level.</span><span class="sxs-lookup"><span data-stu-id="59fa2-149">Link translation is enabled for each application, so that you have control over the user experience at the per-app level.</span></span> <span data-ttu-id="59fa2-150">Turn on link translation for an app when you want the links *from* that app to be translated, not links *to* that app.</span><span class="sxs-lookup"><span data-stu-id="59fa2-150">Turn on link translation for an app when you want the links *from* that app to be translated, not links *to* that app.</span></span> 

<span data-ttu-id="59fa2-151">For example, suppose that you have three applications published through Application Proxy that all link to each other: Benefits, Expenses, and Travel.</span><span class="sxs-lookup"><span data-stu-id="59fa2-151">For example, suppose that you have three applications published through Application Proxy that all link to each other: Benefits, Expenses, and Travel.</span></span> <span data-ttu-id="59fa2-152">There's a fourth app, Feedback, that isn't published through Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="59fa2-152">There's a fourth app, Feedback, that isn't published through Application Proxy.</span></span>

<span data-ttu-id="59fa2-153">When you enable link translation for the Benefits app, the links to Expenses and Travel are redirected to the external URLs for those apps, but the link to Feedback is not redirected because there is no external URL.</span><span class="sxs-lookup"><span data-stu-id="59fa2-153">When you enable link translation for the Benefits app, the links to Expenses and Travel are redirected to the external URLs for those apps, but the link to Feedback is not redirected because there is no external URL.</span></span> <span data-ttu-id="59fa2-154">Links from Expenses and Travel back to Benefits don't work, because link translation has not been enabled for those two apps.</span><span class="sxs-lookup"><span data-stu-id="59fa2-154">Links from Expenses and Travel back to Benefits don't work, because link translation has not been enabled for those two apps.</span></span>

![Links from Benefits to other apps when link translation is enabled](./media/application-proxy-configure-hard-coded-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a><span data-ttu-id="59fa2-156">Which links aren't translated?</span><span class="sxs-lookup"><span data-stu-id="59fa2-156">Which links aren't translated?</span></span>

<span data-ttu-id="59fa2-157">To improve performance and security, some links aren't translated:</span><span class="sxs-lookup"><span data-stu-id="59fa2-157">To improve performance and security, some links aren't translated:</span></span>

- <span data-ttu-id="59fa2-158">Links not inside of code tags.</span><span class="sxs-lookup"><span data-stu-id="59fa2-158">Links not inside of code tags.</span></span> 
- <span data-ttu-id="59fa2-159">Links not in HTML or CSS.</span><span class="sxs-lookup"><span data-stu-id="59fa2-159">Links not in HTML or CSS.</span></span> 
- <span data-ttu-id="59fa2-160">Internal links opened from other programs.</span><span class="sxs-lookup"><span data-stu-id="59fa2-160">Internal links opened from other programs.</span></span> <span data-ttu-id="59fa2-161">Links sent through email or instant message, or included in other documents, won't be translated.</span><span class="sxs-lookup"><span data-stu-id="59fa2-161">Links sent through email or instant message, or included in other documents, won't be translated.</span></span> <span data-ttu-id="59fa2-162">The users need to know to go to the external URL.</span><span class="sxs-lookup"><span data-stu-id="59fa2-162">The users need to know to go to the external URL.</span></span>

<span data-ttu-id="59fa2-163">If you need to support one of these two scenarios, use the same internal and external URLs instead of link translation.</span><span class="sxs-lookup"><span data-stu-id="59fa2-163">If you need to support one of these two scenarios, use the same internal and external URLs instead of link translation.</span></span>  

## <a name="enable-link-translation"></a><span data-ttu-id="59fa2-164">Enable link translation</span><span class="sxs-lookup"><span data-stu-id="59fa2-164">Enable link translation</span></span>

<span data-ttu-id="59fa2-165">Getting started with link translation is as easy as clicking a button:</span><span class="sxs-lookup"><span data-stu-id="59fa2-165">Getting started with link translation is as easy as clicking a button:</span></span>

1. <span data-ttu-id="59fa2-166">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="59fa2-166">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="59fa2-167">Go to **Azure Active Directory** > **Enterprise applications** > **All applications** > select the app you want to manage > **Application proxy**.</span><span class="sxs-lookup"><span data-stu-id="59fa2-167">Go to **Azure Active Directory** > **Enterprise applications** > **All applications** > select the app you want to manage > **Application proxy**.</span></span>
3. <span data-ttu-id="59fa2-168">Turn **Translate URLs in application body** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="59fa2-168">Turn **Translate URLs in application body** to **Yes**.</span></span>

   ![Select Yes to translate URLs in application body](./media/application-proxy-configure-hard-coded-link-translation/select_yes.png)<span data-ttu-id="59fa2-170">.</span><span class="sxs-lookup"><span data-stu-id="59fa2-170">.</span></span>
4. <span data-ttu-id="59fa2-171">Select **Save** to apply your changes.</span><span class="sxs-lookup"><span data-stu-id="59fa2-171">Select **Save** to apply your changes.</span></span>

<span data-ttu-id="59fa2-172">Now, when your users access this application, the proxy will automatically scan for internal URLs that have been published through Application Proxy on your tenant.</span><span class="sxs-lookup"><span data-stu-id="59fa2-172">Now, when your users access this application, the proxy will automatically scan for internal URLs that have been published through Application Proxy on your tenant.</span></span>

## <a name="send-feedback"></a><span data-ttu-id="59fa2-173">Send feedback</span><span class="sxs-lookup"><span data-stu-id="59fa2-173">Send feedback</span></span>

<span data-ttu-id="59fa2-174">We want your help to make this feature work for all your apps.</span><span class="sxs-lookup"><span data-stu-id="59fa2-174">We want your help to make this feature work for all your apps.</span></span> <span data-ttu-id="59fa2-175">We search over 30 tags in HTML and CSS.</span><span class="sxs-lookup"><span data-stu-id="59fa2-175">We search over 30 tags in HTML and CSS.</span></span> <span data-ttu-id="59fa2-176">If you have an example of generated links that aren't being translated, send a code snippet to [Application Proxy Feedback](mailto:aadapfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="59fa2-176">If you have an example of generated links that aren't being translated, send a code snippet to [Application Proxy Feedback](mailto:aadapfeedback@microsoft.com).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="59fa2-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="59fa2-177">Next steps</span></span>
<span data-ttu-id="59fa2-178">[Use custom domains with Azure AD Application Proxy](application-proxy-configure-custom-domain.md) to have the same internal and external URL</span><span class="sxs-lookup"><span data-stu-id="59fa2-178">[Use custom domains with Azure AD Application Proxy](application-proxy-configure-custom-domain.md) to have the same internal and external URL</span></span>

[<span data-ttu-id="59fa2-179">Configure alternate access mappings for SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="59fa2-179">Configure alternate access mappings for SharePoint 2013</span></span>](https://technet.microsoft.com/library/cc263208.aspx)
