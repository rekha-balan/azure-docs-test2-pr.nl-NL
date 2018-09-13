---
title: What's new? Release notes for Azure AD | Microsoft Docs
description: Learn what is new with Azure Active Directory (Azure AD), such as the latest release notes, known issues, bug fixes, deprecated functionality, and upcoming changes.
services: active-directory
author: eross-msft
manager: mtillman
featureFlags:
- clicktale
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.component: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: lizross
ms.reviewer: dhanyahk
ms.openlocfilehash: 0fa220822c65065538db70df8a74de2fcca51938
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856967"
---
# <a name="whats-new-in-azure-active-directory"></a><span data-ttu-id="f8612-104">What's new in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8612-104">What's new in Azure Active Directory?</span></span>

><span data-ttu-id="f8612-105">Get notified about when to revisit this page for updates by adding this [URL](https://docs.microsoft.com/api/search/rss?search=%22whats%20new%20in%20azure%20active%20directory%22&locale=en-us) to your ![RSS icon](./media/whats-new/feed-icon-16x16.png) feed reader.</span><span class="sxs-lookup"><span data-stu-id="f8612-105">Get notified about when to revisit this page for updates by adding this [URL](https://docs.microsoft.com/api/search/rss?search=%22whats%20new%20in%20azure%20active%20directory%22&locale=en-us) to your ![RSS icon](./media/whats-new/feed-icon-16x16.png) feed reader.</span></span>

<span data-ttu-id="f8612-106">Azure AD receives improvements on an ongoing basis.</span><span class="sxs-lookup"><span data-stu-id="f8612-106">Azure AD receives improvements on an ongoing basis.</span></span> <span data-ttu-id="f8612-107">To stay up-to-date with the most recent developments, this article provides you with information about:</span><span class="sxs-lookup"><span data-stu-id="f8612-107">To stay up-to-date with the most recent developments, this article provides you with information about:</span></span>

- <span data-ttu-id="f8612-108">The latest releases</span><span class="sxs-lookup"><span data-stu-id="f8612-108">The latest releases</span></span>
- <span data-ttu-id="f8612-109">Known issues</span><span class="sxs-lookup"><span data-stu-id="f8612-109">Known issues</span></span>
- <span data-ttu-id="f8612-110">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="f8612-110">Bug fixes</span></span>
- <span data-ttu-id="f8612-111">Deprecated functionality</span><span class="sxs-lookup"><span data-stu-id="f8612-111">Deprecated functionality</span></span>
- <span data-ttu-id="f8612-112">Plans for changes</span><span class="sxs-lookup"><span data-stu-id="f8612-112">Plans for changes</span></span>

<span data-ttu-id="f8612-113">This page is updated monthly, so revisit it regularly.</span><span class="sxs-lookup"><span data-stu-id="f8612-113">This page is updated monthly, so revisit it regularly.</span></span>

---
## <a name="august-2018"></a><span data-ttu-id="f8612-114">August 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-114">August 2018</span></span>

### <a name="changes-to-azure-active-directory-ip-address-ranges"></a><span data-ttu-id="f8612-115">Changes to Azure Active Directory IP address ranges</span><span class="sxs-lookup"><span data-stu-id="f8612-115">Changes to Azure Active Directory IP address ranges</span></span>

<span data-ttu-id="f8612-116">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-116">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-117">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-117">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-118">**Product capability:** Platform</span><span class="sxs-lookup"><span data-stu-id="f8612-118">**Product capability:** Platform</span></span>

<span data-ttu-id="f8612-119">We're introducing larger IP ranges to Azure AD, which means if you've configured Azure AD IP address ranges for your firewalls, routers, or Network Security Groups, you'll need to update them.</span><span class="sxs-lookup"><span data-stu-id="f8612-119">We're introducing larger IP ranges to Azure AD, which means if you've configured Azure AD IP address ranges for your firewalls, routers, or Network Security Groups, you'll need to update them.</span></span> <span data-ttu-id="f8612-120">We're making this update so you won't have to change your firewall, router, or Network Security Groups IP range configurations again when Azure AD adds new endpoints.</span><span class="sxs-lookup"><span data-stu-id="f8612-120">We're making this update so you won't have to change your firewall, router, or Network Security Groups IP range configurations again when Azure AD adds new endpoints.</span></span> 

<span data-ttu-id="f8612-121">Network traffic is moving to these new ranges over the next two months.</span><span class="sxs-lookup"><span data-stu-id="f8612-121">Network traffic is moving to these new ranges over the next two months.</span></span> <span data-ttu-id="f8612-122">To continue with uninterrupted service, you must add these updated values to your IP Addresses before September 10, 2018:</span><span class="sxs-lookup"><span data-stu-id="f8612-122">To continue with uninterrupted service, you must add these updated values to your IP Addresses before September 10, 2018:</span></span>

- <span data-ttu-id="f8612-123">20.190.128.0/18</span><span class="sxs-lookup"><span data-stu-id="f8612-123">20.190.128.0/18</span></span> 

- <span data-ttu-id="f8612-124">40.126.0.0/18</span><span class="sxs-lookup"><span data-stu-id="f8612-124">40.126.0.0/18</span></span> 

<span data-ttu-id="f8612-125">We strongly recommend not removing the old IP Address ranges until all of your network traffic has moved to the new ranges.</span><span class="sxs-lookup"><span data-stu-id="f8612-125">We strongly recommend not removing the old IP Address ranges until all of your network traffic has moved to the new ranges.</span></span> <span data-ttu-id="f8612-126">For updates about the move and to learn when you can remove the old ranges, see [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span><span class="sxs-lookup"><span data-stu-id="f8612-126">For updates about the move and to learn when you can remove the old ranges, see [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span></span>

---

### <a name="change-notice-authorization-codes-will-no-longer-be-available-for-reuse"></a><span data-ttu-id="f8612-127">Change notice: Authorization codes will no longer be available for reuse</span><span class="sxs-lookup"><span data-stu-id="f8612-127">Change notice: Authorization codes will no longer be available for reuse</span></span> 

<span data-ttu-id="f8612-128">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-128">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-129">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-129">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-130">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-130">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-131">Starting on October 10, 2018, Azure AD will stop accepting previously-used authentication codes for new apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-131">Starting on October 10, 2018, Azure AD will stop accepting previously-used authentication codes for new apps.</span></span> <span data-ttu-id="f8612-132">Any app created before October 10, 2018 will still be able to reuse authentication codes.</span><span class="sxs-lookup"><span data-stu-id="f8612-132">Any app created before October 10, 2018 will still be able to reuse authentication codes.</span></span> <span data-ttu-id="f8612-133">This security change helps to bring Azure AD in line with the OAuth specification and will be enforced on both the v1 and v2 endpoints.</span><span class="sxs-lookup"><span data-stu-id="f8612-133">This security change helps to bring Azure AD in line with the OAuth specification and will be enforced on both the v1 and v2 endpoints.</span></span>

<span data-ttu-id="f8612-134">If your app reuses authorization codes to get tokens for multiple resources, we recommend that you use the code to get a refresh token, and then use that refresh token to acquire additional tokens for other resources.</span><span class="sxs-lookup"><span data-stu-id="f8612-134">If your app reuses authorization codes to get tokens for multiple resources, we recommend that you use the code to get a refresh token, and then use that refresh token to acquire additional tokens for other resources.</span></span> <span data-ttu-id="f8612-135">Authorization codes can only be used once, but refresh tokens can be used multiple times across multiple resources.</span><span class="sxs-lookup"><span data-stu-id="f8612-135">Authorization codes can only be used once, but refresh tokens can be used multiple times across multiple resources.</span></span> <span data-ttu-id="f8612-136">Any new app that attempts to reuse an authentication code during the OAuth code flow will get an invalid_grant error, revoking the previous refresh token that was acquired using that duplicate code.</span><span class="sxs-lookup"><span data-stu-id="f8612-136">Any new app that attempts to reuse an authentication code during the OAuth code flow will get an invalid_grant error, revoking the previous refresh token that was acquired using that duplicate code.</span></span>

<span data-ttu-id="f8612-137">For more information about refresh tokens, see [Refreshing the access tokens](https://docs.microsoft.com/azure/active-directory/develop/v1-protocols-oauth-code#refreshing-the-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="f8612-137">For more information about refresh tokens, see [Refreshing the access tokens](https://docs.microsoft.com/azure/active-directory/develop/v1-protocols-oauth-code#refreshing-the-access-tokens).</span></span>
 
---

### <a name="converged-security-info-management-for-self-service-password-sspr-and-multi-factor-authentication-mfa"></a><span data-ttu-id="f8612-138">Converged security info management for self-service password (SSPR) and Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="f8612-138">Converged security info management for self-service password (SSPR) and Multi-Factor Authentication (MFA)</span></span>

<span data-ttu-id="f8612-139">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-139">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-140">**Service category:** SSPR</span><span class="sxs-lookup"><span data-stu-id="f8612-140">**Service category:** SSPR</span></span>  
<span data-ttu-id="f8612-141">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-141">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-142">This new feature helps people manage their security info (such as, phone number, mobile app, and so on) for SSPR and MFA in a single location and experience; as compared to previously, where it was done in two different locations.</span><span class="sxs-lookup"><span data-stu-id="f8612-142">This new feature helps people manage their security info (such as, phone number, mobile app, and so on) for SSPR and MFA in a single location and experience; as compared to previously, where it was done in two different locations.</span></span>

<span data-ttu-id="f8612-143">This converged experience also works for people using either SSPR or MFA.</span><span class="sxs-lookup"><span data-stu-id="f8612-143">This converged experience also works for people using either SSPR or MFA.</span></span> <span data-ttu-id="f8612-144">Additionally, if your organization doesn't enforce MFA or SSPR registration, people can still register any MFA or SSPR security info methods allowed by your organization from the My Apps portal.</span><span class="sxs-lookup"><span data-stu-id="f8612-144">Additionally, if your organization doesn't enforce MFA or SSPR registration, people can still register any MFA or SSPR security info methods allowed by your organization from the My Apps portal.</span></span>

<span data-ttu-id="f8612-145">This is an opt-in public preview.</span><span class="sxs-lookup"><span data-stu-id="f8612-145">This is an opt-in public preview.</span></span> <span data-ttu-id="f8612-146">Administrators can turn on the new experience (if desired) for a selected group or for all users in a tenant.</span><span class="sxs-lookup"><span data-stu-id="f8612-146">Administrators can turn on the new experience (if desired) for a selected group or for all users in a tenant.</span></span> <span data-ttu-id="f8612-147">For more information about the converged experience, see the [Converged experience blog](https://cloudblogs.microsoft.com/enterprisemobility/2018/08/06/mfa-and-sspr-updates-now-in-public-preview/)</span><span class="sxs-lookup"><span data-stu-id="f8612-147">For more information about the converged experience, see the [Converged experience blog](https://cloudblogs.microsoft.com/enterprisemobility/2018/08/06/mfa-and-sspr-updates-now-in-public-preview/)</span></span>

---

### <a name="new-http-only-cookies-setting-in-azure-ad-application-proxy-apps"></a><span data-ttu-id="f8612-148">New HTTP-Only cookies setting in Azure AD Application proxy apps</span><span class="sxs-lookup"><span data-stu-id="f8612-148">New HTTP-Only cookies setting in Azure AD Application proxy apps</span></span>

<span data-ttu-id="f8612-149">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-149">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-150">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-150">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-151">**Product capability:** Access Control</span><span class="sxs-lookup"><span data-stu-id="f8612-151">**Product capability:** Access Control</span></span>

<span data-ttu-id="f8612-152">There's a new setting called, **HTTP-Only Cookies** in your Application Proxy apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-152">There's a new setting called, **HTTP-Only Cookies** in your Application Proxy apps.</span></span> <span data-ttu-id="f8612-153">This setting helps provide extra security by including the HTTPOnly flag in the HTTP response header for both Application Proxy access and session cookies, stopping access to the cookie from a client-side script and further preventing actions like copying or modifying the cookie.</span><span class="sxs-lookup"><span data-stu-id="f8612-153">This setting helps provide extra security by including the HTTPOnly flag in the HTTP response header for both Application Proxy access and session cookies, stopping access to the cookie from a client-side script and further preventing actions like copying or modifying the cookie.</span></span> <span data-ttu-id="f8612-154">Although this flag hasn't been used previously, your cookies have always been encrypted and transmitted using a SSL connection to help protect against improper modifications.</span><span class="sxs-lookup"><span data-stu-id="f8612-154">Although this flag hasn't been used previously, your cookies have always been encrypted and transmitted using a SSL connection to help protect against improper modifications.</span></span>

<span data-ttu-id="f8612-155">This setting isn't compatible with apps using ActiveX controls, such as Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="f8612-155">This setting isn't compatible with apps using ActiveX controls, such as Remote Desktop.</span></span> <span data-ttu-id="f8612-156">If you're in this situation, we recommend that you turn this setting off.</span><span class="sxs-lookup"><span data-stu-id="f8612-156">If you're in this situation, we recommend that you turn this setting off.</span></span>

<span data-ttu-id="f8612-157">For more information about the HTTP-Only Cookies setting, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f8612-157">For more information about the HTTP-Only Cookies setting, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-publish-azure-portal).</span></span>

---

### <a name="privileged-identity-management-pim-for-azure-resources-supports-management-group-resource-types"></a><span data-ttu-id="f8612-158">Privileged Identity Management (PIM) for Azure resources supports Management Group resource types</span><span class="sxs-lookup"><span data-stu-id="f8612-158">Privileged Identity Management (PIM) for Azure resources supports Management Group resource types</span></span>

<span data-ttu-id="f8612-159">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-159">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-160">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-160">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-161">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-161">**Product capability:** Privileged Identity Management</span></span>
 
<span data-ttu-id="f8612-162">Just-In-Time activation and assignment settings can now be applied to Management Group resource types, just like you already do for Subscriptions, Resource Groups, and Resources (such as VMs, App Services, and more).</span><span class="sxs-lookup"><span data-stu-id="f8612-162">Just-In-Time activation and assignment settings can now be applied to Management Group resource types, just like you already do for Subscriptions, Resource Groups, and Resources (such as VMs, App Services, and more).</span></span> <span data-ttu-id="f8612-163">In addition, anyone with a role that provides administrator access for a Management Group can discover and manage that resource in PIM.</span><span class="sxs-lookup"><span data-stu-id="f8612-163">In addition, anyone with a role that provides administrator access for a Management Group can discover and manage that resource in PIM.</span></span>

<span data-ttu-id="f8612-164">For more information about PIM and Azure resources, see [Discover and manage Azure resources by using Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-discover-resources)</span><span class="sxs-lookup"><span data-stu-id="f8612-164">For more information about PIM and Azure resources, see [Discover and manage Azure resources by using Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-discover-resources)</span></span>
 
---

### <a name="application-access-preview-provides-faster-access-to-the-azure-ad-portal"></a><span data-ttu-id="f8612-165">Application access (preview) provides faster access to the Azure AD portal</span><span class="sxs-lookup"><span data-stu-id="f8612-165">Application access (preview) provides faster access to the Azure AD portal</span></span>

<span data-ttu-id="f8612-166">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-166">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-167">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-167">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-168">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-168">**Product capability:** Privileged Identity Management</span></span>
 
<span data-ttu-id="f8612-169">Today, when activating a role using PIM, it can take over 10 minutes for the permissions to take effect.</span><span class="sxs-lookup"><span data-stu-id="f8612-169">Today, when activating a role using PIM, it can take over 10 minutes for the permissions to take effect.</span></span> <span data-ttu-id="f8612-170">If you choose to use Application access, which is currently in public preview, administrators can access the Azure AD portal as soon as the activation request completes.</span><span class="sxs-lookup"><span data-stu-id="f8612-170">If you choose to use Application access, which is currently in public preview, administrators can access the Azure AD portal as soon as the activation request completes.</span></span>

<span data-ttu-id="f8612-171">Currently, Application access only supports the Azure AD portal experience and Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f8612-171">Currently, Application access only supports the Azure AD portal experience and Azure resources.</span></span> <span data-ttu-id="f8612-172">For more information about PIM and Application access, see [What is Azure AD Privileged Identity Management?](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure)</span><span class="sxs-lookup"><span data-stu-id="f8612-172">For more information about PIM and Application access, see [What is Azure AD Privileged Identity Management?](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure)</span></span>
 
---

### <a name="new-federated-apps-available-in-azure-ad-app-gallery---august-2018"></a><span data-ttu-id="f8612-173">New Federated Apps available in Azure AD app gallery - August 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-173">New Federated Apps available in Azure AD app gallery - August 2018</span></span>

<span data-ttu-id="f8612-174">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-174">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-175">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-175">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-176">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-176">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-177">In August 2018, we've added these 16 new apps with Federation support to the app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-177">In August 2018, we've added these 16 new apps with Federation support to the app gallery:</span></span>

<span data-ttu-id="f8612-178">[Hornbill](https://docs.microsoft.com/azure/active-directory/saas-apps/hornbill-tutorial), [Bridgeline Unbound](https://docs.microsoft.com/azure/active-directory/saas-apps/bridgelineunbound-tutorial), [Sauce Labs - Mobile and Web Testing](https://docs.microsoft.com/azure/active-directory/saas-apps/saucelabs-mobileandwebtesting-tutorial), [Meta Networks Connector](https://docs.microsoft.com/azure/active-directory/saas-apps/metanetworksconnector-tutorial), [Way We Do](https://docs.microsoft.com/azure/active-directory/saas-apps/waywedo-tutorial), [Spotinst](https://docs.microsoft.com/azure/active-directory/saas-apps/spotinst-tutorial), [ProMaster (by Inlogik)](https://docs.microsoft.com/azure/active-directory/saas-apps/promaster-tutorial), SchoolBooking, [4me](https://docs.microsoft.com/azure/active-directory/saas-apps/4me-tutorial), [Dossier](https://docs.microsoft.com/azure/active-directory/saas-apps/DOSSIER-tutorial), [N2F - Expense reports](https://docs.microsoft.com/azure/active-directory/saas-apps/n2f-expensereports-tutorial), [Comm100 Live Chat](https://docs.microsoft.com/azure/active-directory/saas-apps/comm100livechat-tutorial), [SafeConnect](https://docs.microsoft.com/azure/active-directory/saas-apps/safeconnect-tutorial), [ZenQMS](https://docs.microsoft.com/azure/active-directory/saas-apps/zenqms-tutorial), [eLuminate](https://docs.microsoft.com/azure/active-directory/saas-apps/eluminate-tutorial), [Dovetale](https://docs.microsoft.com/azure/active-directory/saas-apps/dovetale-tutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-178">[Hornbill](https://docs.microsoft.com/azure/active-directory/saas-apps/hornbill-tutorial), [Bridgeline Unbound](https://docs.microsoft.com/azure/active-directory/saas-apps/bridgelineunbound-tutorial), [Sauce Labs - Mobile and Web Testing](https://docs.microsoft.com/azure/active-directory/saas-apps/saucelabs-mobileandwebtesting-tutorial), [Meta Networks Connector](https://docs.microsoft.com/azure/active-directory/saas-apps/metanetworksconnector-tutorial), [Way We Do](https://docs.microsoft.com/azure/active-directory/saas-apps/waywedo-tutorial), [Spotinst](https://docs.microsoft.com/azure/active-directory/saas-apps/spotinst-tutorial), [ProMaster (by Inlogik)](https://docs.microsoft.com/azure/active-directory/saas-apps/promaster-tutorial), SchoolBooking, [4me](https://docs.microsoft.com/azure/active-directory/saas-apps/4me-tutorial), [Dossier](https://docs.microsoft.com/azure/active-directory/saas-apps/DOSSIER-tutorial), [N2F - Expense reports](https://docs.microsoft.com/azure/active-directory/saas-apps/n2f-expensereports-tutorial), [Comm100 Live Chat](https://docs.microsoft.com/azure/active-directory/saas-apps/comm100livechat-tutorial), [SafeConnect](https://docs.microsoft.com/azure/active-directory/saas-apps/safeconnect-tutorial), [ZenQMS](https://docs.microsoft.com/azure/active-directory/saas-apps/zenqms-tutorial), [eLuminate](https://docs.microsoft.com/azure/active-directory/saas-apps/eluminate-tutorial), [Dovetale](https://docs.microsoft.com/azure/active-directory/saas-apps/dovetale-tutorial).</span></span>

<span data-ttu-id="f8612-179">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-179">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span> <span data-ttu-id="f8612-180">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://aka.ms/azureadapprequest).</span><span class="sxs-lookup"><span data-stu-id="f8612-180">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://aka.ms/azureadapprequest).</span></span>

---

### <a name="native-tableau-support-is-now-available-in-azure-ad-application-proxy"></a><span data-ttu-id="f8612-181">Native Tableau support is now available in Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-181">Native Tableau support is now available in Azure AD Application Proxy</span></span>

<span data-ttu-id="f8612-182">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-182">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-183">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-183">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-184">**Product capability:** Access Control</span><span class="sxs-lookup"><span data-stu-id="f8612-184">**Product capability:** Access Control</span></span>

<span data-ttu-id="f8612-185">With our update from the OpenID Connect to the OAuth 2.0 Code Grant protocol for our pre-authentication protocol, you no longer have to do any additional configuration to use Tableau with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="f8612-185">With our update from the OpenID Connect to the OAuth 2.0 Code Grant protocol for our pre-authentication protocol, you no longer have to do any additional configuration to use Tableau with Application Proxy.</span></span> <span data-ttu-id="f8612-186">This protocol change also helps Application Proxy better support more modern apps by using only HTTP redirects, which are commonly supported in JavaScript and HTML tags.</span><span class="sxs-lookup"><span data-stu-id="f8612-186">This protocol change also helps Application Proxy better support more modern apps by using only HTTP redirects, which are commonly supported in JavaScript and HTML tags.</span></span>

<span data-ttu-id="f8612-187">For more information about our native support for Tableau, see [Azure AD Application Proxy now with native Tableau support](https://blogs.technet.microsoft.com/applicationproxyblog/2018/08/14/azure-ad-application-proxy-now-with-native-tableau-support).</span><span class="sxs-lookup"><span data-stu-id="f8612-187">For more information about our native support for Tableau, see [Azure AD Application Proxy now with native Tableau support](https://blogs.technet.microsoft.com/applicationproxyblog/2018/08/14/azure-ad-application-proxy-now-with-native-tableau-support).</span></span>

---

### <a name="new-support-to-add-google-as-an-identity-provider-for-b2b-guest-users-in-azure-active-directory-preview"></a><span data-ttu-id="f8612-188">New support to add Google as an identity provider for B2B guest users in Azure Active Directory (preview)</span><span class="sxs-lookup"><span data-stu-id="f8612-188">New support to add Google as an identity provider for B2B guest users in Azure Active Directory (preview)</span></span>

<span data-ttu-id="f8612-189">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-189">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-190">**Service category:** B2B</span><span class="sxs-lookup"><span data-stu-id="f8612-190">**Service category:** B2B</span></span>  
<span data-ttu-id="f8612-191">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-191">**Product capability:** B2B/B2C</span></span>

<span data-ttu-id="f8612-192">By setting up federation with Google in your organization, you can let invited Gmail users sign-in to your shared apps and resources using their existing Google account, without having to create a personal Microsoft Account (MSAs) or an Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="f8612-192">By setting up federation with Google in your organization, you can let invited Gmail users sign-in to your shared apps and resources using their existing Google account, without having to create a personal Microsoft Account (MSAs) or an Azure AD account.</span></span>

<span data-ttu-id="f8612-193">This is an opt-in public preview.</span><span class="sxs-lookup"><span data-stu-id="f8612-193">This is an opt-in public preview.</span></span> <span data-ttu-id="f8612-194">For more information about Google federation, see [Add Google as an identity provider for B2B guest users](https://docs.microsoft.com/azure/active-directory/b2b/google-federation).</span><span class="sxs-lookup"><span data-stu-id="f8612-194">For more information about Google federation, see [Add Google as an identity provider for B2B guest users](https://docs.microsoft.com/azure/active-directory/b2b/google-federation).</span></span>

---

## <a name="july-2018"></a><span data-ttu-id="f8612-195">July 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-195">July 2018</span></span>

### <a name="improvements-to-azure-active-directory-email-notifications"></a><span data-ttu-id="f8612-196">Improvements to Azure Active Directory email notifications</span><span class="sxs-lookup"><span data-stu-id="f8612-196">Improvements to Azure Active Directory email notifications</span></span>

<span data-ttu-id="f8612-197">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-197">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-198">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-198">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-199">**Product capability:** Identity lifecycle management</span><span class="sxs-lookup"><span data-stu-id="f8612-199">**Product capability:** Identity lifecycle management</span></span>
 
<span data-ttu-id="f8612-200">Azure Active Directory (Azure AD) emails now feature an updated design, as well as changes to the sender email address and sender display name, when sent from the following services:</span><span class="sxs-lookup"><span data-stu-id="f8612-200">Azure Active Directory (Azure AD) emails now feature an updated design, as well as changes to the sender email address and sender display name, when sent from the following services:</span></span>
 
- <span data-ttu-id="f8612-201">Azure AD Access Reviews</span><span class="sxs-lookup"><span data-stu-id="f8612-201">Azure AD Access Reviews</span></span>
- <span data-ttu-id="f8612-202">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="f8612-202">Azure AD Connect Health</span></span> 
- <span data-ttu-id="f8612-203">Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-203">Azure AD Identity Protection</span></span> 
- <span data-ttu-id="f8612-204">Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-204">Azure AD Privileged Identity Management</span></span>
- <span data-ttu-id="f8612-205">Enterprise App Expiring Certificate Notifications</span><span class="sxs-lookup"><span data-stu-id="f8612-205">Enterprise App Expiring Certificate Notifications</span></span>
- <span data-ttu-id="f8612-206">Enterprise App Provisioning Service Notifications</span><span class="sxs-lookup"><span data-stu-id="f8612-206">Enterprise App Provisioning Service Notifications</span></span>
 
<span data-ttu-id="f8612-207">The email notifications will be sent from the following email address and display name:</span><span class="sxs-lookup"><span data-stu-id="f8612-207">The email notifications will be sent from the following email address and display name:</span></span>

- <span data-ttu-id="f8612-208">Email address: azure-noreply@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f8612-208">Email address: azure-noreply@microsoft.com</span></span>
- <span data-ttu-id="f8612-209">Display name: Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f8612-209">Display name: Microsoft Azure</span></span>
 
<span data-ttu-id="f8612-210">For an example of some of the new e-mail designs and more information, see [Email notifications in Azure AD PIM](https://go.microsoft.com/fwlink/?linkid=2005832).</span><span class="sxs-lookup"><span data-stu-id="f8612-210">For an example of some of the new e-mail designs and more information, see [Email notifications in Azure AD PIM](https://go.microsoft.com/fwlink/?linkid=2005832).</span></span>

---

### <a name="azure-ad-activity-logs-are-now-available-through-azure-monitor"></a><span data-ttu-id="f8612-211">Azure AD Activity Logs are now available through Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f8612-211">Azure AD Activity Logs are now available through Azure Monitor</span></span>

<span data-ttu-id="f8612-212">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-212">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-213">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-213">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-214">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-214">**Product capability:** Monitoring & Reporting</span></span>

<span data-ttu-id="f8612-215">The Azure AD Activity Logs are now available in public preview for the Azure Monitor (Azure's platform-wide monitoring service).</span><span class="sxs-lookup"><span data-stu-id="f8612-215">The Azure AD Activity Logs are now available in public preview for the Azure Monitor (Azure's platform-wide monitoring service).</span></span> <span data-ttu-id="f8612-216">Azure Monitor offers you long-term retention and seamless integration, in addition to these improvements:</span><span class="sxs-lookup"><span data-stu-id="f8612-216">Azure Monitor offers you long-term retention and seamless integration, in addition to these improvements:</span></span>

- <span data-ttu-id="f8612-217">Long-term retention by routing your log files to your own Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="f8612-217">Long-term retention by routing your log files to your own Azure storage account.</span></span>

- <span data-ttu-id="f8612-218">Seamless SIEM integration, without requiring you to write or maintain custom scripts.</span><span class="sxs-lookup"><span data-stu-id="f8612-218">Seamless SIEM integration, without requiring you to write or maintain custom scripts.</span></span>

- <span data-ttu-id="f8612-219">Seamless integration with your own custom solutions, analytics tools, or incident management solutions.</span><span class="sxs-lookup"><span data-stu-id="f8612-219">Seamless integration with your own custom solutions, analytics tools, or incident management solutions.</span></span>

<span data-ttu-id="f8612-220">For more information about these new capabilities, see our blog [Azure AD activity logs in Azure Monitor diagnostics is now in public preview](https://cloudblogs.microsoft.com/enterprisemobility/2018/07/26/azure-ad-activity-logs-in-azure-monitor-diagnostics-now-in-public-preview/) and our documentation, [Azure Active Directory activity logs in Azure Monitor (preview)](https://docs.microsoft.com/azure/active-directory/reporting-azure-monitor-diagnostics-overview).</span><span class="sxs-lookup"><span data-stu-id="f8612-220">For more information about these new capabilities, see our blog [Azure AD activity logs in Azure Monitor diagnostics is now in public preview](https://cloudblogs.microsoft.com/enterprisemobility/2018/07/26/azure-ad-activity-logs-in-azure-monitor-diagnostics-now-in-public-preview/) and our documentation, [Azure Active Directory activity logs in Azure Monitor (preview)](https://docs.microsoft.com/azure/active-directory/reporting-azure-monitor-diagnostics-overview).</span></span>

---

### <a name="conditional-access-information-added-to-the-azure-ad-sign-ins-report"></a><span data-ttu-id="f8612-221">Conditional access information added to the Azure AD sign-ins report</span><span class="sxs-lookup"><span data-stu-id="f8612-221">Conditional access information added to the Azure AD sign-ins report</span></span>

<span data-ttu-id="f8612-222">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-222">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-223">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-223">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-224">**Product capability:** Identity Security & Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-224">**Product capability:** Identity Security & Protection</span></span>
 
<span data-ttu-id="f8612-225">This update lets you see which policies are evaluated when a user signs in along with the policy outcome.</span><span class="sxs-lookup"><span data-stu-id="f8612-225">This update lets you see which policies are evaluated when a user signs in along with the policy outcome.</span></span> <span data-ttu-id="f8612-226">In addition, the report now includes the type of client app used by the user, so you can identify legacy protocol traffic.</span><span class="sxs-lookup"><span data-stu-id="f8612-226">In addition, the report now includes the type of client app used by the user, so you can identify legacy protocol traffic.</span></span> <span data-ttu-id="f8612-227">Report entries can also now be searched for a correlation ID, which can be found in the user-facing error message and can be used to identify and troubleshoot the matching sign-in request.</span><span class="sxs-lookup"><span data-stu-id="f8612-227">Report entries can also now be searched for a correlation ID, which can be found in the user-facing error message and can be used to identify and troubleshoot the matching sign-in request.</span></span>

---

### <a name="view-legacy-authentications-through-sign-ins-activity-logs"></a><span data-ttu-id="f8612-228">View legacy authentications through Sign-ins activity logs</span><span class="sxs-lookup"><span data-stu-id="f8612-228">View legacy authentications through Sign-ins activity logs</span></span>

<span data-ttu-id="f8612-229">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-229">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-230">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-230">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-231">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-231">**Product capability:** Monitoring & Reporting</span></span>
 
<span data-ttu-id="f8612-232">With the introduction of the **Client App** field in the Sign-in activity logs, customers can now see users that are using legacy authentications.</span><span class="sxs-lookup"><span data-stu-id="f8612-232">With the introduction of the **Client App** field in the Sign-in activity logs, customers can now see users that are using legacy authentications.</span></span> <span data-ttu-id="f8612-233">Customers will be able to access this information using the Sign-ins MS Graph API or through the Sign-in activity logs in Azure AD portal where you can use the **Client App** control to filter on legacy authentications.</span><span class="sxs-lookup"><span data-stu-id="f8612-233">Customers will be able to access this information using the Sign-ins MS Graph API or through the Sign-in activity logs in Azure AD portal where you can use the **Client App** control to filter on legacy authentications.</span></span> <span data-ttu-id="f8612-234">Check out the documentation for more details.</span><span class="sxs-lookup"><span data-stu-id="f8612-234">Check out the documentation for more details.</span></span>

---

### <a name="new-federated-apps-available-in-azure-ad-app-gallery---july-2018"></a><span data-ttu-id="f8612-235">New Federated Apps available in Azure AD app gallery - July 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-235">New Federated Apps available in Azure AD app gallery - July 2018</span></span>

<span data-ttu-id="f8612-236">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-236">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-237">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-237">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-238">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-238">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-239">In July 2018, we've added these 16 new apps with Federation support to the app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-239">In July 2018, we've added these 16 new apps with Federation support to the app gallery:</span></span>

<span data-ttu-id="f8612-240">[Innovation Hub](https://docs.microsoft.com/azure/active-directory/saas-apps/innovationhub-tutorial), [Leapsome](https://docs.microsoft.com/azure/active-directory/saas-apps/leapsome-tutorial), [Certain Admin SSO](https://docs.microsoft.com/azure/active-directory/saas-apps/certainadminsso-tutorial), PSUC Staging, [iPass SmartConnect](https://docs.microsoft.com/azure/active-directory/saas-apps/ipasssmartconnect-tutorial), [Screencast-O-Matic](https://docs.microsoft.com/azure/active-directory/saas-apps/screencast-tutorial), PowerSchool Unified Classroom, [Eli Onboarding](https://docs.microsoft.com/azure/active-directory/saas-apps/elionboarding-tutorial), [Bomgar Remote Support](https://docs.microsoft.com/azure/active-directory/saas-apps/bomgarremotesupport-tutorial), [Nimblex](https://docs.microsoft.com/azure/active-directory/saas-apps/nimblex-tutorial), [Imagineer WebVision](https://docs.microsoft.com/azure/active-directory/saas-apps/imagineerwebvision-tutorial), [Insight4GRC](https://docs.microsoft.com/azure/active-directory/saas-apps/insight4grc-tutorial), [SecureW2 JoinNow Connector](https://docs.microsoft.com/azure/active-directory/saas-apps/securejoinnow-tutorial), [Kanbanize](https://review.docs.microsoft.com/azure/active-directory/saas-apps/kanbanize-tutorial), [SmartLPA](https://review.docs.microsoft.com/azure/active-directory/saas-apps/smartlpa-tutorial), [Skills Base](https://docs.microsoft.com/azure/active-directory/saas-apps/skillsbase-tutorial)</span><span class="sxs-lookup"><span data-stu-id="f8612-240">[Innovation Hub](https://docs.microsoft.com/azure/active-directory/saas-apps/innovationhub-tutorial), [Leapsome](https://docs.microsoft.com/azure/active-directory/saas-apps/leapsome-tutorial), [Certain Admin SSO](https://docs.microsoft.com/azure/active-directory/saas-apps/certainadminsso-tutorial), PSUC Staging, [iPass SmartConnect](https://docs.microsoft.com/azure/active-directory/saas-apps/ipasssmartconnect-tutorial), [Screencast-O-Matic](https://docs.microsoft.com/azure/active-directory/saas-apps/screencast-tutorial), PowerSchool Unified Classroom, [Eli Onboarding](https://docs.microsoft.com/azure/active-directory/saas-apps/elionboarding-tutorial), [Bomgar Remote Support](https://docs.microsoft.com/azure/active-directory/saas-apps/bomgarremotesupport-tutorial), [Nimblex](https://docs.microsoft.com/azure/active-directory/saas-apps/nimblex-tutorial), [Imagineer WebVision](https://docs.microsoft.com/azure/active-directory/saas-apps/imagineerwebvision-tutorial), [Insight4GRC](https://docs.microsoft.com/azure/active-directory/saas-apps/insight4grc-tutorial), [SecureW2 JoinNow Connector](https://docs.microsoft.com/azure/active-directory/saas-apps/securejoinnow-tutorial), [Kanbanize](https://review.docs.microsoft.com/azure/active-directory/saas-apps/kanbanize-tutorial), [SmartLPA](https://review.docs.microsoft.com/azure/active-directory/saas-apps/smartlpa-tutorial), [Skills Base](https://docs.microsoft.com/azure/active-directory/saas-apps/skillsbase-tutorial)</span></span>

<span data-ttu-id="f8612-241">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-241">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span> <span data-ttu-id="f8612-242">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://aka.ms/azureadapprequest).</span><span class="sxs-lookup"><span data-stu-id="f8612-242">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://aka.ms/azureadapprequest).</span></span>

---
 
### <a name="new-user-provisioning-saas-app-integrations---july-2018"></a><span data-ttu-id="f8612-243">New user provisioning SaaS app integrations - July 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-243">New user provisioning SaaS app integrations - July 2018</span></span>

<span data-ttu-id="f8612-244">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-244">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-245">**Service category:** App Provisioning</span><span class="sxs-lookup"><span data-stu-id="f8612-245">**Service category:** App Provisioning</span></span>  
<span data-ttu-id="f8612-246">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-246">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-247">Azure AD allows you to automate the creation, maintenance, and removal of user identities in SaaS applications such as Dropbox, Salesforce, ServiceNow, and more.</span><span class="sxs-lookup"><span data-stu-id="f8612-247">Azure AD allows you to automate the creation, maintenance, and removal of user identities in SaaS applications such as Dropbox, Salesforce, ServiceNow, and more.</span></span> <span data-ttu-id="f8612-248">For July 2018, we have added user provisioning support for the following applications in the Azure AD app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-248">For July 2018, we have added user provisioning support for the following applications in the Azure AD app gallery:</span></span>

- [<span data-ttu-id="f8612-249">Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="f8612-249">Cisco Spark</span></span>](https://docs.microsoft.com/azure/active-directory/saas-apps/cisco-spark-provisioning-tutorial)

- [<span data-ttu-id="f8612-250">Cisco WebEx</span><span class="sxs-lookup"><span data-stu-id="f8612-250">Cisco WebEx</span></span>](https://docs.microsoft.com/azure/active-directory/saas-apps/cisco-webex-provisioning-tutorial)

- [<span data-ttu-id="f8612-251">Bonusly</span><span class="sxs-lookup"><span data-stu-id="f8612-251">Bonusly</span></span>](https://docs.microsoft.com/azure/active-directory/saas-apps/bonusly-provisioning-tutorial)

<span data-ttu-id="f8612-252">For a list of all applications that support user provisioning in the Azure AD gallery, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-252">For a list of all applications that support user provisioning in the Azure AD gallery, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span>

---

### <a name="connect-health-for-sync---an-easier-way-to-fix-orphaned-and-duplicate-attribute-sync-errors"></a><span data-ttu-id="f8612-253">Connect Health for Sync - An easier way to fix orphaned and duplicate attribute sync errors</span><span class="sxs-lookup"><span data-stu-id="f8612-253">Connect Health for Sync - An easier way to fix orphaned and duplicate attribute sync errors</span></span>

<span data-ttu-id="f8612-254">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-254">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-255">**Service category:** AD Connect</span><span class="sxs-lookup"><span data-stu-id="f8612-255">**Service category:** AD Connect</span></span>  
<span data-ttu-id="f8612-256">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-256">**Product capability:** Monitoring & Reporting</span></span>
 
<span data-ttu-id="f8612-257">Azure AD Connect Health introduces self-service remediation to help you highlight and fix sync errors.</span><span class="sxs-lookup"><span data-stu-id="f8612-257">Azure AD Connect Health introduces self-service remediation to help you highlight and fix sync errors.</span></span> <span data-ttu-id="f8612-258">This feature troubleshoots duplicated attribute sync errors and fixes objects that are orphaned from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-258">This feature troubleshoots duplicated attribute sync errors and fixes objects that are orphaned from Azure AD.</span></span> <span data-ttu-id="f8612-259">This diagnosis has the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f8612-259">This diagnosis has the following benefits:</span></span>

- <span data-ttu-id="f8612-260">Narrows down duplicated attribute sync errors, providing specific fixes</span><span class="sxs-lookup"><span data-stu-id="f8612-260">Narrows down duplicated attribute sync errors, providing specific fixes</span></span>

- <span data-ttu-id="f8612-261">Applies a fix for dedicated Azure AD scenarios, resolving errors in a single step</span><span class="sxs-lookup"><span data-stu-id="f8612-261">Applies a fix for dedicated Azure AD scenarios, resolving errors in a single step</span></span>

- <span data-ttu-id="f8612-262">No upgrade or configuration is required to turn on and use this feature</span><span class="sxs-lookup"><span data-stu-id="f8612-262">No upgrade or configuration is required to turn on and use this feature</span></span>

<span data-ttu-id="f8612-263">For more information, see [Diagnose and remediate duplicated attribute sync errors](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-diagnose-sync-errors)</span><span class="sxs-lookup"><span data-stu-id="f8612-263">For more information, see [Diagnose and remediate duplicated attribute sync errors](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-diagnose-sync-errors)</span></span>

---

### <a name="visual-updates-to-the-azure-ad-and-msa-sign-in-experiences"></a><span data-ttu-id="f8612-264">Visual updates to the Azure AD and MSA sign-in experiences</span><span class="sxs-lookup"><span data-stu-id="f8612-264">Visual updates to the Azure AD and MSA sign-in experiences</span></span>

<span data-ttu-id="f8612-265">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-265">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-266">**Service category:** Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-266">**Service category:** Azure AD</span></span>  
<span data-ttu-id="f8612-267">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-267">**Product capability:** User Authentication</span></span>

<span data-ttu-id="f8612-268">We've updated the UI for Microsoft's online services sign-in experience, such as for Office 365 and Azure.</span><span class="sxs-lookup"><span data-stu-id="f8612-268">We've updated the UI for Microsoft's online services sign-in experience, such as for Office 365 and Azure.</span></span> <span data-ttu-id="f8612-269">This change makes the screens less cluttered and more straightforward.</span><span class="sxs-lookup"><span data-stu-id="f8612-269">This change makes the screens less cluttered and more straightforward.</span></span> <span data-ttu-id="f8612-270">For more information about this change, see the [Upcoming improvements to the Azure AD sign-in experience](https://cloudblogs.microsoft.com/enterprisemobility/2018/04/04/upcoming-improvements-to-the-azure-ad-sign-in-experience/) blog.</span><span class="sxs-lookup"><span data-stu-id="f8612-270">For more information about this change, see the [Upcoming improvements to the Azure AD sign-in experience](https://cloudblogs.microsoft.com/enterprisemobility/2018/04/04/upcoming-improvements-to-the-azure-ad-sign-in-experience/) blog.</span></span>

---

### <a name="new-release-of-azure-ad-connect---july-2018"></a><span data-ttu-id="f8612-271">New release of Azure AD Connect - July 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-271">New release of Azure AD Connect - July 2018</span></span>

<span data-ttu-id="f8612-272">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-272">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-273">**Service category:** App Provisioning</span><span class="sxs-lookup"><span data-stu-id="f8612-273">**Service category:** App Provisioning</span></span>  
<span data-ttu-id="f8612-274">**Product capability:** Identity Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="f8612-274">**Product capability:** Identity Lifecycle Management</span></span>

<span data-ttu-id="f8612-275">The latest release of Azure AD Connect includes:</span><span class="sxs-lookup"><span data-stu-id="f8612-275">The latest release of Azure AD Connect includes:</span></span> 

- <span data-ttu-id="f8612-276">Bug fixes and supportability updates</span><span class="sxs-lookup"><span data-stu-id="f8612-276">Bug fixes and supportability updates</span></span> 

- <span data-ttu-id="f8612-277">General Availability of the Ping Federate integration</span><span class="sxs-lookup"><span data-stu-id="f8612-277">General Availability of the Ping Federate integration</span></span>

- <span data-ttu-id="f8612-278">Updates to the latest SQL 2012 client</span><span class="sxs-lookup"><span data-stu-id="f8612-278">Updates to the latest SQL 2012 client</span></span> 

<span data-ttu-id="f8612-279">For more information about this update, see [Azure AD Connect: Version release history](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-version-history)</span><span class="sxs-lookup"><span data-stu-id="f8612-279">For more information about this update, see [Azure AD Connect: Version release history](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-version-history)</span></span>

---

### <a name="updates-to-the-terms-of-use-tou-end-user-ui"></a><span data-ttu-id="f8612-280">Updates to the Terms of Use (ToU) end-user UI</span><span class="sxs-lookup"><span data-stu-id="f8612-280">Updates to the Terms of Use (ToU) end-user UI</span></span>

<span data-ttu-id="f8612-281">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-281">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-282">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-282">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-283">**Product capability:** Governance</span><span class="sxs-lookup"><span data-stu-id="f8612-283">**Product capability:** Governance</span></span>

<span data-ttu-id="f8612-284">We're updating the acceptance string in the TOU end-user UI.</span><span class="sxs-lookup"><span data-stu-id="f8612-284">We're updating the acceptance string in the TOU end-user UI.</span></span>

<span data-ttu-id="f8612-285">**Current text.**</span><span class="sxs-lookup"><span data-stu-id="f8612-285">**Current text.**</span></span> <span data-ttu-id="f8612-286">In order to access [tenantName] resources, you must accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="f8612-286">In order to access [tenantName] resources, you must accept the terms of use.</span></span><br><span data-ttu-id="f8612-287">**New text.**</span><span class="sxs-lookup"><span data-stu-id="f8612-287">**New text.**</span></span> <span data-ttu-id="f8612-288">In order to access [tenantName] resource, you must read the terms of use.</span><span class="sxs-lookup"><span data-stu-id="f8612-288">In order to access [tenantName] resource, you must read the terms of use.</span></span>

<span data-ttu-id="f8612-289">**Current text:** Choosing to accept means that you agree to all of the above terms of use.</span><span class="sxs-lookup"><span data-stu-id="f8612-289">**Current text:** Choosing to accept means that you agree to all of the above terms of use.</span></span><br><span data-ttu-id="f8612-290">**New text:** Please click Accept to confirm that you have read and understood the terms of use.</span><span class="sxs-lookup"><span data-stu-id="f8612-290">**New text:** Please click Accept to confirm that you have read and understood the terms of use.</span></span>

---
 
### <a name="pass-through-authentication-supports-legacy-protocols-and-applications"></a><span data-ttu-id="f8612-291">Pass-through Authentication supports legacy protocols and applications</span><span class="sxs-lookup"><span data-stu-id="f8612-291">Pass-through Authentication supports legacy protocols and applications</span></span>

<span data-ttu-id="f8612-292">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-292">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-293">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-293">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-294">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-294">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-295">Pass-through Authentication now supports legacy protocols and apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-295">Pass-through Authentication now supports legacy protocols and apps.</span></span> <span data-ttu-id="f8612-296">The following limitations are now fully supported:</span><span class="sxs-lookup"><span data-stu-id="f8612-296">The following limitations are now fully supported:</span></span>

- <span data-ttu-id="f8612-297">User sign-ins to legacy Office client applications, Office 2010 and Office 2013, without requiring modern authentication.</span><span class="sxs-lookup"><span data-stu-id="f8612-297">User sign-ins to legacy Office client applications, Office 2010 and Office 2013, without requiring modern authentication.</span></span>

- <span data-ttu-id="f8612-298">Access to calendar sharing and free/busy information in Exchange hybrid environments on Office 2010 only.</span><span class="sxs-lookup"><span data-stu-id="f8612-298">Access to calendar sharing and free/busy information in Exchange hybrid environments on Office 2010 only.</span></span>

- <span data-ttu-id="f8612-299">User sign-ins to Skype for Business client applications without requiring modern authentication.</span><span class="sxs-lookup"><span data-stu-id="f8612-299">User sign-ins to Skype for Business client applications without requiring modern authentication.</span></span>

- <span data-ttu-id="f8612-300">User sign-ins to PowerShell version 1.0.</span><span class="sxs-lookup"><span data-stu-id="f8612-300">User sign-ins to PowerShell version 1.0.</span></span>

- <span data-ttu-id="f8612-301">The Apple Device Enrollment Program (Apple DEP), using the iOS Setup Assistant.</span><span class="sxs-lookup"><span data-stu-id="f8612-301">The Apple Device Enrollment Program (Apple DEP), using the iOS Setup Assistant.</span></span> 

---
 
### <a name="converged-security-info-management-for-self-service-password-reset-and-multi-factor-authentication"></a><span data-ttu-id="f8612-302">Converged security info management for self-service password reset and Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-302">Converged security info management for self-service password reset and Multi-Factor Authentication</span></span>

<span data-ttu-id="f8612-303">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-303">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-304">**Service category:** SSPR</span><span class="sxs-lookup"><span data-stu-id="f8612-304">**Service category:** SSPR</span></span>  
<span data-ttu-id="f8612-305">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-305">**Product capability:** User Authentication</span></span>

<span data-ttu-id="f8612-306">This new feature lets users manage their security info (for example, phone number, email address, mobile app, and so on) for self-service password reset (SSPR) and Multi-Factor Authentication (MFA) in a single experience.</span><span class="sxs-lookup"><span data-stu-id="f8612-306">This new feature lets users manage their security info (for example, phone number, email address, mobile app, and so on) for self-service password reset (SSPR) and Multi-Factor Authentication (MFA) in a single experience.</span></span> <span data-ttu-id="f8612-307">Users will no longer have to register the same security info for SSPR and MFA in two different experiences.</span><span class="sxs-lookup"><span data-stu-id="f8612-307">Users will no longer have to register the same security info for SSPR and MFA in two different experiences.</span></span> <span data-ttu-id="f8612-308">This new experience also applies to users who have either SSPR or MFA.</span><span class="sxs-lookup"><span data-stu-id="f8612-308">This new experience also applies to users who have either SSPR or MFA.</span></span>

<span data-ttu-id="f8612-309">If an organization isn't enforcing MFA or SSPR registration, users can register their security info through the **My Apps** portal.</span><span class="sxs-lookup"><span data-stu-id="f8612-309">If an organization isn't enforcing MFA or SSPR registration, users can register their security info through the **My Apps** portal.</span></span> <span data-ttu-id="f8612-310">From there, users can register any methods enabled for MFA or SSPR.</span><span class="sxs-lookup"><span data-stu-id="f8612-310">From there, users can register any methods enabled for MFA or SSPR.</span></span> 

<span data-ttu-id="f8612-311">This is an opt-in public preview.</span><span class="sxs-lookup"><span data-stu-id="f8612-311">This is an opt-in public preview.</span></span> <span data-ttu-id="f8612-312">Admins can turn on the new experience (if desired) for a selected group of users or all users in a tenant.</span><span class="sxs-lookup"><span data-stu-id="f8612-312">Admins can turn on the new experience (if desired) for a selected group of users or all users in a tenant.</span></span>

---
 
### <a name="use-the-microsoft-authenticator-app-to-verify-your-identity-when-you-reset-your-password"></a><span data-ttu-id="f8612-313">Use the Microsoft Authenticator app to verify your identity when you reset your password</span><span class="sxs-lookup"><span data-stu-id="f8612-313">Use the Microsoft Authenticator app to verify your identity when you reset your password</span></span>

<span data-ttu-id="f8612-314">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-314">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-315">**Service category:** SSPR</span><span class="sxs-lookup"><span data-stu-id="f8612-315">**Service category:** SSPR</span></span>  
<span data-ttu-id="f8612-316">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-316">**Product capability:** User Authentication</span></span>

<span data-ttu-id="f8612-317">This feature lets non-admins verify their identity while resetting a password using a notification or code from Microsoft Authenticator (or any other authenticator app).</span><span class="sxs-lookup"><span data-stu-id="f8612-317">This feature lets non-admins verify their identity while resetting a password using a notification or code from Microsoft Authenticator (or any other authenticator app).</span></span> <span data-ttu-id="f8612-318">After admins turn this self-service password reset method on, users who have registered a mobile app through aka.ms/mfasetup or aka.ms/setupsecurityinfo can use their mobile app as a verification method while resetting their password.</span><span class="sxs-lookup"><span data-stu-id="f8612-318">After admins turn this self-service password reset method on, users who have registered a mobile app through aka.ms/mfasetup or aka.ms/setupsecurityinfo can use their mobile app as a verification method while resetting their password.</span></span>

<span data-ttu-id="f8612-319">Mobile app notification can only be turned on as part of a policy that requires two methods to reset your password.</span><span class="sxs-lookup"><span data-stu-id="f8612-319">Mobile app notification can only be turned on as part of a policy that requires two methods to reset your password.</span></span>

---

## <a name="june-2018"></a><span data-ttu-id="f8612-320">June 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-320">June 2018</span></span>

### <a name="change-notice-security-fix-to-the-delegated-authorization-flow-for-apps-using-azure-ad-activity-logs-api"></a><span data-ttu-id="f8612-321">Change notice: Security fix to the delegated authorization flow for apps using Azure AD Activity Logs API</span><span class="sxs-lookup"><span data-stu-id="f8612-321">Change notice: Security fix to the delegated authorization flow for apps using Azure AD Activity Logs API</span></span>

<span data-ttu-id="f8612-322">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-322">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-323">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-323">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-324">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-324">**Product capability:** Monitoring & Reporting</span></span>

<span data-ttu-id="f8612-325">Due to our stronger security enforcement, we’ve had to make a change to the permissions for apps that use a delegated authorization flow to access [Azure AD Activity Logs APIs](https://aka.ms/aadreportsapi).</span><span class="sxs-lookup"><span data-stu-id="f8612-325">Due to our stronger security enforcement, we’ve had to make a change to the permissions for apps that use a delegated authorization flow to access [Azure AD Activity Logs APIs](https://aka.ms/aadreportsapi).</span></span> <span data-ttu-id="f8612-326">This change will occur by **June 26, 2018**.</span><span class="sxs-lookup"><span data-stu-id="f8612-326">This change will occur by **June 26, 2018**.</span></span>

<span data-ttu-id="f8612-327">If any of your apps use Azure AD Activity Log APIs, follow these steps to ensure the app doesn’t break after the change happens.</span><span class="sxs-lookup"><span data-stu-id="f8612-327">If any of your apps use Azure AD Activity Log APIs, follow these steps to ensure the app doesn’t break after the change happens.</span></span>

<span data-ttu-id="f8612-328">**To update your app permissions**</span><span class="sxs-lookup"><span data-stu-id="f8612-328">**To update your app permissions**</span></span>

1. <span data-ttu-id="f8612-329">Sign in to the Azure portal, select **Azure Active Directory**, and then select **App Registrations**.</span><span class="sxs-lookup"><span data-stu-id="f8612-329">Sign in to the Azure portal, select **Azure Active Directory**, and then select **App Registrations**.</span></span>
2. <span data-ttu-id="f8612-330">Select your app that uses the Azure AD Activity Logs API, select **Settings**, select **Required permissions**, and then select the **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="f8612-330">Select your app that uses the Azure AD Activity Logs API, select **Settings**, select **Required permissions**, and then select the **Windows Azure Active Directory** API.</span></span>
3. <span data-ttu-id="f8612-331">In the **Delegated permissions** area of the **Enable access** blade, select the box next to **Read directory** data, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f8612-331">In the **Delegated permissions** area of the **Enable access** blade, select the box next to **Read directory** data, and then select **Save**.</span></span>
4. <span data-ttu-id="f8612-332">Select **Grant permissions**, and then select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f8612-332">Select **Grant permissions**, and then select **Yes**.</span></span>
    
    >[!Note]
    ><span data-ttu-id="f8612-333">You must be a Global administrator to grant permissions to the app.</span><span class="sxs-lookup"><span data-stu-id="f8612-333">You must be a Global administrator to grant permissions to the app.</span></span>

<span data-ttu-id="f8612-334">For more information, see the [Grant permissions](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-prerequisites-azure-portal#grant-permissions) area of the Prerequisites to access the Azure AD reporting API article.</span><span class="sxs-lookup"><span data-stu-id="f8612-334">For more information, see the [Grant permissions](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-prerequisites-azure-portal#grant-permissions) area of the Prerequisites to access the Azure AD reporting API article.</span></span>

---

### <a name="configure-tls-settings-to-connect-to-azure-ad-services-for-pci-dss-compliance"></a><span data-ttu-id="f8612-335">Configure TLS settings to connect to Azure AD services for PCI DSS compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-335">Configure TLS settings to connect to Azure AD services for PCI DSS compliance</span></span>

<span data-ttu-id="f8612-336">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-336">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-337">**Service category:** N/A</span><span class="sxs-lookup"><span data-stu-id="f8612-337">**Service category:** N/A</span></span>  
<span data-ttu-id="f8612-338">**Product capability:** Platform</span><span class="sxs-lookup"><span data-stu-id="f8612-338">**Product capability:** Platform</span></span>

<span data-ttu-id="f8612-339">Transport Layer Security (TLS) is a protocol that provides privacy and data integrity between two communicating applications and is the most widely deployed security protocol used today.</span><span class="sxs-lookup"><span data-stu-id="f8612-339">Transport Layer Security (TLS) is a protocol that provides privacy and data integrity between two communicating applications and is the most widely deployed security protocol used today.</span></span>

<span data-ttu-id="f8612-340">The [PCI Security Standards Council](https://www.pcisecuritystandards.org/) has determined that early versions of TLS and Secure Sockets Layer (SSL) must be disabled in favor of enabling new and more secure app protocols, with compliance starting on **June 30, 2018**.</span><span class="sxs-lookup"><span data-stu-id="f8612-340">The [PCI Security Standards Council](https://www.pcisecuritystandards.org/) has determined that early versions of TLS and Secure Sockets Layer (SSL) must be disabled in favor of enabling new and more secure app protocols, with compliance starting on **June 30, 2018**.</span></span> <span data-ttu-id="f8612-341">This change means that if you connect to Azure AD services and require PCI DSS-compliance, you must disable TLS 1.0.</span><span class="sxs-lookup"><span data-stu-id="f8612-341">This change means that if you connect to Azure AD services and require PCI DSS-compliance, you must disable TLS 1.0.</span></span> <span data-ttu-id="f8612-342">Multiple versions of TLS are available, but TLS 1.2 is the latest version available for Azure Active Directory Services.</span><span class="sxs-lookup"><span data-stu-id="f8612-342">Multiple versions of TLS are available, but TLS 1.2 is the latest version available for Azure Active Directory Services.</span></span> <span data-ttu-id="f8612-343">We highly recommend moving directly to TLS 1.2 for both client/server and browser/server combinations.</span><span class="sxs-lookup"><span data-stu-id="f8612-343">We highly recommend moving directly to TLS 1.2 for both client/server and browser/server combinations.</span></span>

<span data-ttu-id="f8612-344">Out-of-date browsers might not support newer TLS versions, such as TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="f8612-344">Out-of-date browsers might not support newer TLS versions, such as TLS 1.2.</span></span> <span data-ttu-id="f8612-345">To see which versions of TLS are supported by your browser, go to the [Qualys SSL Labs](https://www.ssllabs.com/) site and click **Test your browser**.</span><span class="sxs-lookup"><span data-stu-id="f8612-345">To see which versions of TLS are supported by your browser, go to the [Qualys SSL Labs](https://www.ssllabs.com/) site and click **Test your browser**.</span></span> <span data-ttu-id="f8612-346">We recommend you upgrade to the latest version of your web browser and preferably enable only TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="f8612-346">We recommend you upgrade to the latest version of your web browser and preferably enable only TLS 1.2.</span></span>

<span data-ttu-id="f8612-347">**To enable TLS 1.2, by browser**</span><span class="sxs-lookup"><span data-stu-id="f8612-347">**To enable TLS 1.2, by browser**</span></span>

- <span data-ttu-id="f8612-348">**Microsoft Edge and Internet Explorer (both are set using Internet Explorer)**</span><span class="sxs-lookup"><span data-stu-id="f8612-348">**Microsoft Edge and Internet Explorer (both are set using Internet Explorer)**</span></span>

    1. <span data-ttu-id="f8612-349">Open Internet Explorer, select **Tools** > **Internet Options** > **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="f8612-349">Open Internet Explorer, select **Tools** > **Internet Options** > **Advanced**.</span></span>
    2. <span data-ttu-id="f8612-350">In the **Security** area, select **use TLS 1.2**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8612-350">In the **Security** area, select **use TLS 1.2**, and then select **OK**.</span></span>
    3. <span data-ttu-id="f8612-351">Close all browser windows and restart Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f8612-351">Close all browser windows and restart Internet Explorer.</span></span> 

- <span data-ttu-id="f8612-352">**Google Chrome**</span><span class="sxs-lookup"><span data-stu-id="f8612-352">**Google Chrome**</span></span>

    1. <span data-ttu-id="f8612-353">Open Google Chrome, type *chrome://settings/* into the address bar, and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f8612-353">Open Google Chrome, type *chrome://settings/* into the address bar, and press **Enter**.</span></span>
    2. <span data-ttu-id="f8612-354">Expand the **Advanced** options, go to the **System** area, and select **Open proxy settings**.</span><span class="sxs-lookup"><span data-stu-id="f8612-354">Expand the **Advanced** options, go to the **System** area, and select **Open proxy settings**.</span></span>
    3. <span data-ttu-id="f8612-355">In the **Internet Properties** box, select the **Advanced** tab, go to the **Security** area, select **use TLS 1.2**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8612-355">In the **Internet Properties** box, select the **Advanced** tab, go to the **Security** area, select **use TLS 1.2**, and then select **OK**.</span></span>
    4. <span data-ttu-id="f8612-356">Close all browser windows and restart Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="f8612-356">Close all browser windows and restart Google Chrome.</span></span>

- <span data-ttu-id="f8612-357">**Mozilla Firefox**</span><span class="sxs-lookup"><span data-stu-id="f8612-357">**Mozilla Firefox**</span></span>

    1. <span data-ttu-id="f8612-358">Open Firefox, type *about:config* into the address bar, and then press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f8612-358">Open Firefox, type *about:config* into the address bar, and then press **Enter**.</span></span>
    2. <span data-ttu-id="f8612-359">Search for the term, *TLS*, and then select the **security.tls.version.max** entry.</span><span class="sxs-lookup"><span data-stu-id="f8612-359">Search for the term, *TLS*, and then select the **security.tls.version.max** entry.</span></span>
    3. <span data-ttu-id="f8612-360">Set the value to **3** to force the browser to use up to version TLS 1.2, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8612-360">Set the value to **3** to force the browser to use up to version TLS 1.2, and then select **OK**.</span></span>

        >[!NOTE]
        ><span data-ttu-id="f8612-361">Firefox version 60.0 supports TLS 1.3, so you can also set the security.tls.version.max value to **4**.</span><span class="sxs-lookup"><span data-stu-id="f8612-361">Firefox version 60.0 supports TLS 1.3, so you can also set the security.tls.version.max value to **4**.</span></span>

    4. <span data-ttu-id="f8612-362">Close all browser windows and restart Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="f8612-362">Close all browser windows and restart Mozilla Firefox.</span></span>

---

### <a name="new-federated-apps-available-in-azure-ad-app-gallery---june-2018"></a><span data-ttu-id="f8612-363">New Federated Apps available in Azure AD app gallery - June 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-363">New Federated Apps available in Azure AD app gallery - June 2018</span></span>

<span data-ttu-id="f8612-364">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-364">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-365">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-365">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-366">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-366">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-367">In June 2018, we've added these 15 new apps with Federation support to the app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-367">In June 2018, we've added these 15 new apps with Federation support to the app gallery:</span></span>

<span data-ttu-id="f8612-368">[Skytap](https://docs.microsoft.com/azure/active-directory/active-directory-saas-skytap-tutorial), [Settling music](https://docs.microsoft.com/azure/active-directory/active-directory-saas-settlingmusic-tutorial), [SAML 1.1 Token enabled LOB App](https://docs.microsoft.com/azure/active-directory/active-directory-saas-saml-tutorial), [Supermood](https://docs.microsoft.com/azure/active-directory/active-directory-saas-supermood-tutorial), [Autotask](https://docs.microsoft.com/azure/active-directory/active-directory-saas-autotaskendpointbackup-tutorial), [Endpoint Backup](https://docs.microsoft.com/azure/active-directory/active-directory-saas-autotaskendpointbackup-tutorial), [Skyhigh Networks](https://docs.microsoft.com/azure/active-directory/active-directory-saas-skyhighnetworks-tutorial), Smartway2, [TonicDM](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tonicdm-tutorial), [Moconavi](https://docs.microsoft.com/azure/active-directory/active-directory-saas-moconavi-tutorial), [Zoho One](https://docs.microsoft.com/azure/active-directory/active-directory-saas-zohoone-tutorial), [SharePoint on-premises](https://docs.microsoft.com/azure/active-directory/active-directory-saas-sharepoint-on-premises-tutorial), [ForeSee CX Suite](https://docs.microsoft.com/azure/active-directory/active-directory-saas-foreseecxsuite-tutorial), [Vidyard](https://docs.microsoft.com/azure/active-directory/active-directory-saas-vidyard-tutorial), [ChronicX](https://docs.microsoft.com/azure/active-directory/active-directory-saas-chronicx-tutorial)</span><span class="sxs-lookup"><span data-stu-id="f8612-368">[Skytap](https://docs.microsoft.com/azure/active-directory/active-directory-saas-skytap-tutorial), [Settling music](https://docs.microsoft.com/azure/active-directory/active-directory-saas-settlingmusic-tutorial), [SAML 1.1 Token enabled LOB App](https://docs.microsoft.com/azure/active-directory/active-directory-saas-saml-tutorial), [Supermood](https://docs.microsoft.com/azure/active-directory/active-directory-saas-supermood-tutorial), [Autotask](https://docs.microsoft.com/azure/active-directory/active-directory-saas-autotaskendpointbackup-tutorial), [Endpoint Backup](https://docs.microsoft.com/azure/active-directory/active-directory-saas-autotaskendpointbackup-tutorial), [Skyhigh Networks](https://docs.microsoft.com/azure/active-directory/active-directory-saas-skyhighnetworks-tutorial), Smartway2, [TonicDM](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tonicdm-tutorial), [Moconavi](https://docs.microsoft.com/azure/active-directory/active-directory-saas-moconavi-tutorial), [Zoho One](https://docs.microsoft.com/azure/active-directory/active-directory-saas-zohoone-tutorial), [SharePoint on-premises](https://docs.microsoft.com/azure/active-directory/active-directory-saas-sharepoint-on-premises-tutorial), [ForeSee CX Suite](https://docs.microsoft.com/azure/active-directory/active-directory-saas-foreseecxsuite-tutorial), [Vidyard](https://docs.microsoft.com/azure/active-directory/active-directory-saas-vidyard-tutorial), [ChronicX](https://docs.microsoft.com/azure/active-directory/active-directory-saas-chronicx-tutorial)</span></span>

<span data-ttu-id="f8612-369">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-369">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span> <span data-ttu-id="f8612-370">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span><span class="sxs-lookup"><span data-stu-id="f8612-370">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span></span> 

---

### <a name="azure-ad-password-protection-is-available-in-public-preview"></a><span data-ttu-id="f8612-371">Azure AD Password Protection is available in public preview</span><span class="sxs-lookup"><span data-stu-id="f8612-371">Azure AD Password Protection is available in public preview</span></span>

<span data-ttu-id="f8612-372">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-372">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-373">**Service category:** Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-373">**Service category:** Identity Protection</span></span>  
<span data-ttu-id="f8612-374">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-374">**Product capability:** User Authentication</span></span>

<span data-ttu-id="f8612-375">Use Azure AD Password Protection to help eliminate easily guessed passwords from your environment.</span><span class="sxs-lookup"><span data-stu-id="f8612-375">Use Azure AD Password Protection to help eliminate easily guessed passwords from your environment.</span></span> <span data-ttu-id="f8612-376">Eliminating these passwords helps to lower the risk of compromise from a password spray type of attack.</span><span class="sxs-lookup"><span data-stu-id="f8612-376">Eliminating these passwords helps to lower the risk of compromise from a password spray type of attack.</span></span>

<span data-ttu-id="f8612-377">Specifically, Azure AD Password Protection helps you:</span><span class="sxs-lookup"><span data-stu-id="f8612-377">Specifically, Azure AD Password Protection helps you:</span></span>

- <span data-ttu-id="f8612-378">Protect your organization's accounts in both Azure AD and Windows Server Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="f8612-378">Protect your organization's accounts in both Azure AD and Windows Server Active Directory (AD).</span></span> 
- <span data-ttu-id="f8612-379">Stops your users from using passwords on a list of more than 500 of the most commonly used passwords, and over 1 million character substitution variations of those passwords.</span><span class="sxs-lookup"><span data-stu-id="f8612-379">Stops your users from using passwords on a list of more than 500 of the most commonly used passwords, and over 1 million character substitution variations of those passwords.</span></span>
- <span data-ttu-id="f8612-380">Administer Azure AD Password Protection from a single location in the Azure AD portal, for both Azure AD and on-premises Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-380">Administer Azure AD Password Protection from a single location in the Azure AD portal, for both Azure AD and on-premises Windows Server AD.</span></span>

<span data-ttu-id="f8612-381">For more information about Azure AD Password Protection, see [Eliminate bad passwords in your organization](https://aka.ms/aadpasswordprotectiondocs).</span><span class="sxs-lookup"><span data-stu-id="f8612-381">For more information about Azure AD Password Protection, see [Eliminate bad passwords in your organization](https://aka.ms/aadpasswordprotectiondocs).</span></span>

---

### <a name="new-all-guests-conditional-access-policy-template-created-during-terms-of-use-tou-creation"></a><span data-ttu-id="f8612-382">New "all guests" conditional access policy template created during Terms of Use (ToU) creation</span><span class="sxs-lookup"><span data-stu-id="f8612-382">New "all guests" conditional access policy template created during Terms of Use (ToU) creation</span></span>

<span data-ttu-id="f8612-383">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-383">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-384">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-384">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-385">**Product capability:** Governance</span><span class="sxs-lookup"><span data-stu-id="f8612-385">**Product capability:** Governance</span></span>

<span data-ttu-id="f8612-386">During the creation of your Terms of Use (ToU), a new conditional access policy template is also created for "all guests" and "all apps".</span><span class="sxs-lookup"><span data-stu-id="f8612-386">During the creation of your Terms of Use (ToU), a new conditional access policy template is also created for "all guests" and "all apps".</span></span> <span data-ttu-id="f8612-387">This new policy template applies the newly created ToU, streamlining the creation and enforcement process for guests.</span><span class="sxs-lookup"><span data-stu-id="f8612-387">This new policy template applies the newly created ToU, streamlining the creation and enforcement process for guests.</span></span>

<span data-ttu-id="f8612-388">For more information, see [Azure Active Directory Terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-388">For more information, see [Azure Active Directory Terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>

---

### <a name="new-custom-conditional-access-policy-template-created-during-terms-of-use-tou-creation"></a><span data-ttu-id="f8612-389">New "custom" conditional access policy template created during Terms of Use (ToU) creation</span><span class="sxs-lookup"><span data-stu-id="f8612-389">New "custom" conditional access policy template created during Terms of Use (ToU) creation</span></span>

<span data-ttu-id="f8612-390">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-390">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-391">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-391">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-392">**Product capability:** Governance</span><span class="sxs-lookup"><span data-stu-id="f8612-392">**Product capability:** Governance</span></span>

<span data-ttu-id="f8612-393">During the creation of your Terms of Use (ToU), a new “custom” conditional access policy template is also created.</span><span class="sxs-lookup"><span data-stu-id="f8612-393">During the creation of your Terms of Use (ToU), a new “custom” conditional access policy template is also created.</span></span> <span data-ttu-id="f8612-394">This new policy template lets you create the ToU and then immediately go to the conditional access policy creation blade, without needing to manually navigate through the portal.</span><span class="sxs-lookup"><span data-stu-id="f8612-394">This new policy template lets you create the ToU and then immediately go to the conditional access policy creation blade, without needing to manually navigate through the portal.</span></span>

<span data-ttu-id="f8612-395">For more information, see [Azure Active Directory Terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-395">For more information, see [Azure Active Directory Terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>

---

### <a name="new-and-comprehensive-guidance-about-deploying-azure-multi-factor-authentication"></a><span data-ttu-id="f8612-396">New and comprehensive guidance about deploying Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-396">New and comprehensive guidance about deploying Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="f8612-397">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-397">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-398">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-398">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-399">**Product capability:** Identity Security & Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-399">**Product capability:** Identity Security & Protection</span></span>
 
<span data-ttu-id="f8612-400">We've released new step-by-step guidance about how to deploy Azure Multi-Factor Authentication (MFA) in your organization.</span><span class="sxs-lookup"><span data-stu-id="f8612-400">We've released new step-by-step guidance about how to deploy Azure Multi-Factor Authentication (MFA) in your organization.</span></span>

<span data-ttu-id="f8612-401">To view the MFA deployment guide, go to the [Identity Deployment Guides](https://aka.ms/DeploymentPlans) repo on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8612-401">To view the MFA deployment guide, go to the [Identity Deployment Guides](https://aka.ms/DeploymentPlans) repo on GitHub.</span></span> <span data-ttu-id="f8612-402">To provide feedback about the deployment guides, use the [Deployment Plan Feedback form](https://aka.ms/deploymentplanfeedback).</span><span class="sxs-lookup"><span data-stu-id="f8612-402">To provide feedback about the deployment guides, use the [Deployment Plan Feedback form](https://aka.ms/deploymentplanfeedback).</span></span> <span data-ttu-id="f8612-403">If you have any questions about the deployment guides, contact us at [IDGitDeploy](mailto:idgitdeploy@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f8612-403">If you have any questions about the deployment guides, contact us at [IDGitDeploy](mailto:idgitdeploy@microsoft.com).</span></span>

---

### <a name="azure-ad-delegated-app-management-roles-are-in-public-preview"></a><span data-ttu-id="f8612-404">Azure AD delegated app management roles are in public preview</span><span class="sxs-lookup"><span data-stu-id="f8612-404">Azure AD delegated app management roles are in public preview</span></span>

<span data-ttu-id="f8612-405">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-405">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-406">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-406">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-407">**Product capability:** Access Control</span><span class="sxs-lookup"><span data-stu-id="f8612-407">**Product capability:** Access Control</span></span>

<span data-ttu-id="f8612-408">Admins can now delegate app management tasks without assigning the Global Administrator role.</span><span class="sxs-lookup"><span data-stu-id="f8612-408">Admins can now delegate app management tasks without assigning the Global Administrator role.</span></span> <span data-ttu-id="f8612-409">The new roles and capabilities are:</span><span class="sxs-lookup"><span data-stu-id="f8612-409">The new roles and capabilities are:</span></span>

- <span data-ttu-id="f8612-410">**New standard Azure AD admin roles:**</span><span class="sxs-lookup"><span data-stu-id="f8612-410">**New standard Azure AD admin roles:**</span></span>

    - <span data-ttu-id="f8612-411">**Application Administrator.**</span><span class="sxs-lookup"><span data-stu-id="f8612-411">**Application Administrator.**</span></span> <span data-ttu-id="f8612-412">Grants the ability to manage all aspects of all apps, including registration, SSO settings, app assignments and licensing, App proxy settings, and consent (except to Azure AD resources).</span><span class="sxs-lookup"><span data-stu-id="f8612-412">Grants the ability to manage all aspects of all apps, including registration, SSO settings, app assignments and licensing, App proxy settings, and consent (except to Azure AD resources).</span></span>

    - <span data-ttu-id="f8612-413">**Cloud Application Administrator.**</span><span class="sxs-lookup"><span data-stu-id="f8612-413">**Cloud Application Administrator.**</span></span> <span data-ttu-id="f8612-414">Grants all of the Application Administrator abilities, except for App proxy because it doesn't provide on-premises access.</span><span class="sxs-lookup"><span data-stu-id="f8612-414">Grants all of the Application Administrator abilities, except for App proxy because it doesn't provide on-premises access.</span></span>

    - <span data-ttu-id="f8612-415">**Application Developer.**</span><span class="sxs-lookup"><span data-stu-id="f8612-415">**Application Developer.**</span></span> <span data-ttu-id="f8612-416">Grants the ability to create app registrations, even if the **allow users to register apps** option is turned off.</span><span class="sxs-lookup"><span data-stu-id="f8612-416">Grants the ability to create app registrations, even if the **allow users to register apps** option is turned off.</span></span>

- <span data-ttu-id="f8612-417">**Ownership (set up per-app registration and per-enterprise app, similar to the group ownership process:**</span><span class="sxs-lookup"><span data-stu-id="f8612-417">**Ownership (set up per-app registration and per-enterprise app, similar to the group ownership process:**</span></span>
 
    - <span data-ttu-id="f8612-418">**App Registration Owner.**</span><span class="sxs-lookup"><span data-stu-id="f8612-418">**App Registration Owner.**</span></span> <span data-ttu-id="f8612-419">Grants the ability to manage all aspects of owned app registration, including the app manifest and adding additional owners.</span><span class="sxs-lookup"><span data-stu-id="f8612-419">Grants the ability to manage all aspects of owned app registration, including the app manifest and adding additional owners.</span></span>

    - <span data-ttu-id="f8612-420">**Enterprise App Owner.**</span><span class="sxs-lookup"><span data-stu-id="f8612-420">**Enterprise App Owner.**</span></span> <span data-ttu-id="f8612-421">Grants the ability to manage many aspects of owned enterprise apps, including SSO settings, app assignments, and consent (except to Azure AD resources).</span><span class="sxs-lookup"><span data-stu-id="f8612-421">Grants the ability to manage many aspects of owned enterprise apps, including SSO settings, app assignments, and consent (except to Azure AD resources).</span></span>

<span data-ttu-id="f8612-422">For more information about public preview, see the [Azure AD delegated application management roles are in public preview!](https://cloudblogs.microsoft.com/enterprisemobility/2018/06/13/hallelujah-azure-ad-delegated-application-management-roles-are-in-public-preview/)</span><span class="sxs-lookup"><span data-stu-id="f8612-422">For more information about public preview, see the [Azure AD delegated application management roles are in public preview!](https://cloudblogs.microsoft.com/enterprisemobility/2018/06/13/hallelujah-azure-ad-delegated-application-management-roles-are-in-public-preview/)</span></span> <span data-ttu-id="f8612-423">blog.</span><span class="sxs-lookup"><span data-stu-id="f8612-423">blog.</span></span> <span data-ttu-id="f8612-424">For more information about roles and permissions, see [Assigning administrator roles in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f8612-424">For more information about roles and permissions, see [Assigning administrator roles in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal).</span></span>

---

## <a name="may-2018"></a><span data-ttu-id="f8612-425">May 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-425">May 2018</span></span>

### <a name="expressroute-support-changes"></a><span data-ttu-id="f8612-426">ExpressRoute support changes</span><span class="sxs-lookup"><span data-stu-id="f8612-426">ExpressRoute support changes</span></span>

<span data-ttu-id="f8612-427">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-427">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-428">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-428">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-429">**Product capability:** Platform</span><span class="sxs-lookup"><span data-stu-id="f8612-429">**Product capability:** Platform</span></span>  

<span data-ttu-id="f8612-430">Software as a Service offering, like Azure Active Directory (Azure AD) are designed to work best by going directly through the Internet, without requiring ExpressRoute or any other private VPN tunnels.</span><span class="sxs-lookup"><span data-stu-id="f8612-430">Software as a Service offering, like Azure Active Directory (Azure AD) are designed to work best by going directly through the Internet, without requiring ExpressRoute or any other private VPN tunnels.</span></span> <span data-ttu-id="f8612-431">Because of this, on **August 1, 2018**, we will stop supporting ExpressRoute for Azure AD services using Azure public peering and Azure communities in Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="f8612-431">Because of this, on **August 1, 2018**, we will stop supporting ExpressRoute for Azure AD services using Azure public peering and Azure communities in Microsoft peering.</span></span> <span data-ttu-id="f8612-432">Any services impacted by this change might notice Azure AD traffic gradually shifting from ExpressRoute to the Internet.</span><span class="sxs-lookup"><span data-stu-id="f8612-432">Any services impacted by this change might notice Azure AD traffic gradually shifting from ExpressRoute to the Internet.</span></span>

<span data-ttu-id="f8612-433">While we're changing our support, we also know there are still situations where you might need to use a dedicated set of circuits for your authentication traffic.</span><span class="sxs-lookup"><span data-stu-id="f8612-433">While we're changing our support, we also know there are still situations where you might need to use a dedicated set of circuits for your authentication traffic.</span></span> <span data-ttu-id="f8612-434">Because of this, Azure AD will continue to support per-tenant IP range restrictions using ExpressRoute and services already on Microsoft peering with the "Other Office 365 Online services" community.</span><span class="sxs-lookup"><span data-stu-id="f8612-434">Because of this, Azure AD will continue to support per-tenant IP range restrictions using ExpressRoute and services already on Microsoft peering with the "Other Office 365 Online services" community.</span></span> <span data-ttu-id="f8612-435">If your services are impacted, but you require ExpressRoute, you must do the following:</span><span class="sxs-lookup"><span data-stu-id="f8612-435">If your services are impacted, but you require ExpressRoute, you must do the following:</span></span>

- <span data-ttu-id="f8612-436">**If you're on Azure public peering.**</span><span class="sxs-lookup"><span data-stu-id="f8612-436">**If you're on Azure public peering.**</span></span> <span data-ttu-id="f8612-437">Move to Microsoft peering and sign up for the **Other Office 365 Online services (12076:5100)** community.</span><span class="sxs-lookup"><span data-stu-id="f8612-437">Move to Microsoft peering and sign up for the **Other Office 365 Online services (12076:5100)** community.</span></span> <span data-ttu-id="f8612-438">For more info about how to move from Azure public peering to Microsoft peering, see the [Move a public peering to Microsoft peering](https://docs.microsoft.com/azure/expressroute/how-to-move-peering) article.</span><span class="sxs-lookup"><span data-stu-id="f8612-438">For more info about how to move from Azure public peering to Microsoft peering, see the [Move a public peering to Microsoft peering](https://docs.microsoft.com/azure/expressroute/how-to-move-peering) article.</span></span>

- <span data-ttu-id="f8612-439">**If you're on Microsoft peering.**</span><span class="sxs-lookup"><span data-stu-id="f8612-439">**If you're on Microsoft peering.**</span></span> <span data-ttu-id="f8612-440">Sign up for the **Other Office 365 Online service (12076:5100)** community.</span><span class="sxs-lookup"><span data-stu-id="f8612-440">Sign up for the **Other Office 365 Online service (12076:5100)** community.</span></span> <span data-ttu-id="f8612-441">For more info about routing requirements, see the [Support for BGP communities section](https://docs.microsoft.com/azure/expressroute/expressroute-routing#bgp) of the ExpressRoute routing requirements article.</span><span class="sxs-lookup"><span data-stu-id="f8612-441">For more info about routing requirements, see the [Support for BGP communities section](https://docs.microsoft.com/azure/expressroute/expressroute-routing#bgp) of the ExpressRoute routing requirements article.</span></span>

<span data-ttu-id="f8612-442">If you must continue to use dedicated circuits, you'll need to talk to your Microsoft Account team about how to get authorization to use the **Other Office 365 Online service (12076:5100)** community.</span><span class="sxs-lookup"><span data-stu-id="f8612-442">If you must continue to use dedicated circuits, you'll need to talk to your Microsoft Account team about how to get authorization to use the **Other Office 365 Online service (12076:5100)** community.</span></span> <span data-ttu-id="f8612-443">The MS Office-managed review board will verify whether you need those circuits and make sure you understand the technical implications of keeping them.</span><span class="sxs-lookup"><span data-stu-id="f8612-443">The MS Office-managed review board will verify whether you need those circuits and make sure you understand the technical implications of keeping them.</span></span> <span data-ttu-id="f8612-444">Unauthorized subscriptions trying to create route filters for Office 365 will receive an error message.</span><span class="sxs-lookup"><span data-stu-id="f8612-444">Unauthorized subscriptions trying to create route filters for Office 365 will receive an error message.</span></span> 
 
---

### <a name="microsoft-graph-apis-for-administrative-scenarios-for-tou"></a><span data-ttu-id="f8612-445">Microsoft Graph APIs for administrative scenarios for TOU</span><span class="sxs-lookup"><span data-stu-id="f8612-445">Microsoft Graph APIs for administrative scenarios for TOU</span></span>

<span data-ttu-id="f8612-446">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-446">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-447">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-447">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-448">**Product capability:** Developer Experience</span><span class="sxs-lookup"><span data-stu-id="f8612-448">**Product capability:** Developer Experience</span></span>
 
<span data-ttu-id="f8612-449">We've added Microsoft Graph APIs for administration operation of Azure AD Terms of Use.</span><span class="sxs-lookup"><span data-stu-id="f8612-449">We've added Microsoft Graph APIs for administration operation of Azure AD Terms of Use.</span></span> <span data-ttu-id="f8612-450">You are able to create, update, delete the Terms of Use object.</span><span class="sxs-lookup"><span data-stu-id="f8612-450">You are able to create, update, delete the Terms of Use object.</span></span>

---

### <a name="add-azure-ad-multi-tenant-endpoint-as-an-identity-provider-in-azure-ad-b2c"></a><span data-ttu-id="f8612-451">Add Azure AD multi-tenant endpoint as an identity provider in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-451">Add Azure AD multi-tenant endpoint as an identity provider in Azure AD B2C</span></span>

<span data-ttu-id="f8612-452">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-452">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-453">**Service category:** B2C - Consumer Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-453">**Service category:** B2C - Consumer Identity Management</span></span>  
<span data-ttu-id="f8612-454">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-454">**Product capability:** B2B/B2C</span></span>
 
<span data-ttu-id="f8612-455">Using custom policies, you can now add the Azure AD common endpoint as an identity provider in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f8612-455">Using custom policies, you can now add the Azure AD common endpoint as an identity provider in Azure AD B2C.</span></span> <span data-ttu-id="f8612-456">This allows you to have a single point of entry for all Azure AD users that are signing into your applications.</span><span class="sxs-lookup"><span data-stu-id="f8612-456">This allows you to have a single point of entry for all Azure AD users that are signing into your applications.</span></span> <span data-ttu-id="f8612-457">For more information, see [Azure Active Directory B2C: Allow users to sign in to a multi-tenant Azure AD identity provider using custom policies](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-commonaad-custom).</span><span class="sxs-lookup"><span data-stu-id="f8612-457">For more information, see [Azure Active Directory B2C: Allow users to sign in to a multi-tenant Azure AD identity provider using custom policies](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-commonaad-custom).</span></span>

---

### <a name="use-internal-urls-to-access-apps-from-anywhere-with-our-my-apps-sign-in-extension-and-the-azure-ad-application-proxy"></a><span data-ttu-id="f8612-458">Use Internal URLs to access apps from anywhere with our My Apps Sign-in Extension and the Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-458">Use Internal URLs to access apps from anywhere with our My Apps Sign-in Extension and the Azure AD Application Proxy</span></span>

<span data-ttu-id="f8612-459">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-459">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-460">**Service category:** My Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-460">**Service category:** My Apps</span></span>  
<span data-ttu-id="f8612-461">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-461">**Product capability:** SSO</span></span>
 
<span data-ttu-id="f8612-462">Users can now access applications through internal URLs even when outside your corporate network by using the My Apps Secure Sign-in Extension for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-462">Users can now access applications through internal URLs even when outside your corporate network by using the My Apps Secure Sign-in Extension for Azure AD.</span></span> <span data-ttu-id="f8612-463">This will work with any application that you have published using Azure AD Application Proxy, on any browser that also has the Access Panel browser extension installed.</span><span class="sxs-lookup"><span data-stu-id="f8612-463">This will work with any application that you have published using Azure AD Application Proxy, on any browser that also has the Access Panel browser extension installed.</span></span> <span data-ttu-id="f8612-464">The URL redirection functionality is automatically enabled once a user logs into the extension.</span><span class="sxs-lookup"><span data-stu-id="f8612-464">The URL redirection functionality is automatically enabled once a user logs into the extension.</span></span> <span data-ttu-id="f8612-465">The extension is available for download on [Edge](https://go.microsoft.com/fwlink/?linkid=845176), [Chrome](https://go.microsoft.com/fwlink/?linkid=866367), and [Firefox](https://go.microsoft.com/fwlink/?linkid=866366).</span><span class="sxs-lookup"><span data-stu-id="f8612-465">The extension is available for download on [Edge](https://go.microsoft.com/fwlink/?linkid=845176), [Chrome](https://go.microsoft.com/fwlink/?linkid=866367), and [Firefox](https://go.microsoft.com/fwlink/?linkid=866366).</span></span>

---
 
### <a name="azure-active-directory---data-in-europe-for-europe-customers"></a><span data-ttu-id="f8612-466">Azure Active Directory - Data in Europe for Europe customers</span><span class="sxs-lookup"><span data-stu-id="f8612-466">Azure Active Directory - Data in Europe for Europe customers</span></span>

<span data-ttu-id="f8612-467">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-467">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-468">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-468">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-469">**Product capability:** GoLocal</span><span class="sxs-lookup"><span data-stu-id="f8612-469">**Product capability:** GoLocal</span></span>

<span data-ttu-id="f8612-470">Customers in Europe require their data to stay in Europe and not replicated outside of European datacenters for meeting privacy and European laws.</span><span class="sxs-lookup"><span data-stu-id="f8612-470">Customers in Europe require their data to stay in Europe and not replicated outside of European datacenters for meeting privacy and European laws.</span></span> <span data-ttu-id="f8612-471">This [article](https://go.microsoft.com/fwlink/?linkid=872328) provides the specific details on what identity information will be stored within Europe and also provide details on information that will be stored outside European datacenters.</span><span class="sxs-lookup"><span data-stu-id="f8612-471">This [article](https://go.microsoft.com/fwlink/?linkid=872328) provides the specific details on what identity information will be stored within Europe and also provide details on information that will be stored outside European datacenters.</span></span> 

---
 
### <a name="new-user-provisioning-saas-app-integrations---may-2018"></a><span data-ttu-id="f8612-472">New user provisioning SaaS app integrations - May 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-472">New user provisioning SaaS app integrations - May 2018</span></span>

<span data-ttu-id="f8612-473">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-473">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-474">**Service category:** App Provisioning</span><span class="sxs-lookup"><span data-stu-id="f8612-474">**Service category:** App Provisioning</span></span>  
<span data-ttu-id="f8612-475">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-475">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-476">Azure AD allows you to automate the creation, maintenance, and removal of user identities in SaaS applications such as Dropbox, Salesforce, ServiceNow, and more.</span><span class="sxs-lookup"><span data-stu-id="f8612-476">Azure AD allows you to automate the creation, maintenance, and removal of user identities in SaaS applications such as Dropbox, Salesforce, ServiceNow, and more.</span></span> <span data-ttu-id="f8612-477">For May 2018, we have added user provisioning support for the following applications in the Azure AD app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-477">For May 2018, we have added user provisioning support for the following applications in the Azure AD app gallery:</span></span>

- [<span data-ttu-id="f8612-478">BlueJeans</span><span class="sxs-lookup"><span data-stu-id="f8612-478">BlueJeans</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-bluejeans-provisioning-tutorial)

- [<span data-ttu-id="f8612-479">Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="f8612-479">Cornerstone OnDemand</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-cornerstone-ondemand-provisioning-tutorial)

- [<span data-ttu-id="f8612-480">Zendesk</span><span class="sxs-lookup"><span data-stu-id="f8612-480">Zendesk</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-zendesk-provisioning-tutorial)

<span data-ttu-id="f8612-481">For a list of all applications that support user provisioning in the Azure AD gallery, see [https://aka.ms/appstutorial](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-481">For a list of all applications that support user provisioning in the Azure AD gallery, see [https://aka.ms/appstutorial](https://aka.ms/appstutorial).</span></span>

---
 
### <a name="azure-ad-access-reviews-of-groups-and-app-access-now-provides-recurring-reviews"></a><span data-ttu-id="f8612-482">Azure AD access reviews of groups and app access now provides recurring reviews</span><span class="sxs-lookup"><span data-stu-id="f8612-482">Azure AD access reviews of groups and app access now provides recurring reviews</span></span>

<span data-ttu-id="f8612-483">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-483">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-484">**Service category:** Access Reviews</span><span class="sxs-lookup"><span data-stu-id="f8612-484">**Service category:** Access Reviews</span></span>  
<span data-ttu-id="f8612-485">**Product capability:** Governance</span><span class="sxs-lookup"><span data-stu-id="f8612-485">**Product capability:** Governance</span></span>
 
<span data-ttu-id="f8612-486">Access review of groups and apps is now generally available as part of Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="f8612-486">Access review of groups and apps is now generally available as part of Azure AD Premium P2.</span></span>  <span data-ttu-id="f8612-487">Administrators will be able to configure access reviews of group memberships and application assignments to automatically recur at regular intervals, such as monthly or quarterly.</span><span class="sxs-lookup"><span data-stu-id="f8612-487">Administrators will be able to configure access reviews of group memberships and application assignments to automatically recur at regular intervals, such as monthly or quarterly.</span></span>

---

### <a name="azure-ad-activity-logs-sign-ins-and-audit-are-now-available-through-ms-graph"></a><span data-ttu-id="f8612-488">Azure AD Activity logs (sign-ins and audit) are now available through MS Graph</span><span class="sxs-lookup"><span data-stu-id="f8612-488">Azure AD Activity logs (sign-ins and audit) are now available through MS Graph</span></span>

<span data-ttu-id="f8612-489">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-489">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-490">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-490">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-491">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-491">**Product capability:** Monitoring & Reporting</span></span>
 
<span data-ttu-id="f8612-492">Azure AD Activity logs, which, includes Sign-ins and Audit logs, are now available through MS Graph.</span><span class="sxs-lookup"><span data-stu-id="f8612-492">Azure AD Activity logs, which, includes Sign-ins and Audit logs, are now available through MS Graph.</span></span> <span data-ttu-id="f8612-493">We have exposed two end points through MS Graph to access these logs.</span><span class="sxs-lookup"><span data-stu-id="f8612-493">We have exposed two end points through MS Graph to access these logs.</span></span> <span data-ttu-id="f8612-494">Check out our [documents](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal) for programmatic access to Azure AD Reporting APIs to get started.</span><span class="sxs-lookup"><span data-stu-id="f8612-494">Check out our [documents](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal) for programmatic access to Azure AD Reporting APIs to get started.</span></span> 

---
 
### <a name="improvements-to-the-b2b-redemption-experience-and-leave-an-org"></a><span data-ttu-id="f8612-495">Improvements to the B2B redemption experience and leave an org</span><span class="sxs-lookup"><span data-stu-id="f8612-495">Improvements to the B2B redemption experience and leave an org</span></span>

<span data-ttu-id="f8612-496">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-496">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-497">**Service category:** B2B</span><span class="sxs-lookup"><span data-stu-id="f8612-497">**Service category:** B2B</span></span>  
<span data-ttu-id="f8612-498">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-498">**Product capability:** B2B/B2C</span></span>

<span data-ttu-id="f8612-499">**Just in time redemption:** Once you share a resource with a guest user using B2B API – you don’t need to send out a special invitation email.</span><span class="sxs-lookup"><span data-stu-id="f8612-499">**Just in time redemption:** Once you share a resource with a guest user using B2B API – you don’t need to send out a special invitation email.</span></span> <span data-ttu-id="f8612-500">In most      cases, the guest user can access the resource and will be taken through the redemption experience just in time.</span><span class="sxs-lookup"><span data-stu-id="f8612-500">In most      cases, the guest user can access the resource and will be taken through the redemption experience just in time.</span></span> <span data-ttu-id="f8612-501">No more impact due to missed emails.</span><span class="sxs-lookup"><span data-stu-id="f8612-501">No more impact due to missed emails.</span></span> <span data-ttu-id="f8612-502">No more asking your guest users “Did you click on that redemption link the system sent you?”.</span><span class="sxs-lookup"><span data-stu-id="f8612-502">No more asking your guest users “Did you click on that redemption link the system sent you?”.</span></span> <span data-ttu-id="f8612-503">This means once SPO uses the invitation manager – cloudy attachments can have the same canonical URL for all users – internal and external – in any state of redemption.</span><span class="sxs-lookup"><span data-stu-id="f8612-503">This means once SPO uses the invitation manager – cloudy attachments can have the same canonical URL for all users – internal and external – in any state of redemption.</span></span>

<span data-ttu-id="f8612-504">**Modern redemption experience:** No more split screen redemption landing page.</span><span class="sxs-lookup"><span data-stu-id="f8612-504">**Modern redemption experience:** No more split screen redemption landing page.</span></span> <span data-ttu-id="f8612-505">Users will see a modern consent experience with the inviting organization's privacy statement, just like they do for third-party apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-505">Users will see a modern consent experience with the inviting organization's privacy statement, just like they do for third-party apps.</span></span>

<span data-ttu-id="f8612-506">**Guest users can leave the org:** Once a user’s relationship with an org is over, they can self-serve leaving the organization.</span><span class="sxs-lookup"><span data-stu-id="f8612-506">**Guest users can leave the org:** Once a user’s relationship with an org is over, they can self-serve leaving the organization.</span></span> <span data-ttu-id="f8612-507">No more calling the inviting org’s admin to “be removed”, no more raising support tickets.</span><span class="sxs-lookup"><span data-stu-id="f8612-507">No more calling the inviting org’s admin to “be removed”, no more raising support tickets.</span></span>

---

### <a name="new-federated-apps-available-in-azure-ad-app-gallery---may-2018"></a><span data-ttu-id="f8612-508">New Federated Apps available in Azure AD app gallery - May 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-508">New Federated Apps available in Azure AD app gallery - May 2018</span></span>

<span data-ttu-id="f8612-509">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-509">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-510">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-510">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-511">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-511">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-512">In May 2018, we've added these 18 new apps with Federation support to our app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-512">In May 2018, we've added these 18 new apps with Federation support to our app gallery:</span></span>

<span data-ttu-id="f8612-513">[AwardSpring](https://docs.microsoft.com/azure/active-directory/active-directory-saas-awardspring-tutorial), Infogix Data3Sixty Govern, [Yodeck](https://docs.microsoft.com/azure/active-directory/active-directory-saas-infogix-tutorial), [Jamf Pro](https://docs.microsoft.com/azure/active-directory/active-directory-saas-jamfprosamlconnector-tutorial), [KnowledgeOwl](https://docs.microsoft.com/azure/active-directory/active-directory-saas-knowledgeowl-tutorial), [Envi MMIS](https://docs.microsoft.com/azure/active-directory/active-directory-saas-envimmis-tutorial), [LaunchDarkly](https://docs.microsoft.com/azure/active-directory/active-directory-saas-launchdarkly-tutorial), [Adobe Captivate Prime](https://docs.microsoft.com/azure/active-directory/active-directory-saas-adobecaptivateprime-tutorial), [Montage Online](https://docs.microsoft.com/azure/active-directory/active-directory-saas-montageonline-tutorial), [まなびポケット](https://docs.microsoft.com/azure/active-directory/active-directory-saas-manabipocket-tutorial), OpenReel, [Arc Publishing - SSO](https://docs.microsoft.com/azure/active-directory/active-directory-saas-arc-tutorial), [PlanGrid](https://docs.microsoft.com/azure/active-directory/active-directory-saas-plangrid-tutorial), [iWellnessNow](https://docs.microsoft.com/azure/active-directory/active-directory-saas-iwellnessnow-tutorial), [Proxyclick](https://docs.microsoft.com/azure/active-directory/active-directory-saas-proxyclick-tutorial), [Riskware](https://docs.microsoft.com/azure/active-directory/active-directory-saas-riskware-tutorial), [Flock](https://docs.microsoft.com/azure/active-directory/active-directory-saas-flock-tutorial), [Reviewsnap](https://docs.microsoft.com/azure/active-directory/active-directory-saas-reviewsnap-tutorial)</span><span class="sxs-lookup"><span data-stu-id="f8612-513">[AwardSpring](https://docs.microsoft.com/azure/active-directory/active-directory-saas-awardspring-tutorial), Infogix Data3Sixty Govern, [Yodeck](https://docs.microsoft.com/azure/active-directory/active-directory-saas-infogix-tutorial), [Jamf Pro](https://docs.microsoft.com/azure/active-directory/active-directory-saas-jamfprosamlconnector-tutorial), [KnowledgeOwl](https://docs.microsoft.com/azure/active-directory/active-directory-saas-knowledgeowl-tutorial), [Envi MMIS](https://docs.microsoft.com/azure/active-directory/active-directory-saas-envimmis-tutorial), [LaunchDarkly](https://docs.microsoft.com/azure/active-directory/active-directory-saas-launchdarkly-tutorial), [Adobe Captivate Prime](https://docs.microsoft.com/azure/active-directory/active-directory-saas-adobecaptivateprime-tutorial), [Montage Online](https://docs.microsoft.com/azure/active-directory/active-directory-saas-montageonline-tutorial), [まなびポケット](https://docs.microsoft.com/azure/active-directory/active-directory-saas-manabipocket-tutorial), OpenReel, [Arc Publishing - SSO](https://docs.microsoft.com/azure/active-directory/active-directory-saas-arc-tutorial), [PlanGrid](https://docs.microsoft.com/azure/active-directory/active-directory-saas-plangrid-tutorial), [iWellnessNow](https://docs.microsoft.com/azure/active-directory/active-directory-saas-iwellnessnow-tutorial), [Proxyclick](https://docs.microsoft.com/azure/active-directory/active-directory-saas-proxyclick-tutorial), [Riskware](https://docs.microsoft.com/azure/active-directory/active-directory-saas-riskware-tutorial), [Flock](https://docs.microsoft.com/azure/active-directory/active-directory-saas-flock-tutorial), [Reviewsnap](https://docs.microsoft.com/azure/active-directory/active-directory-saas-reviewsnap-tutorial)</span></span>

<span data-ttu-id="f8612-514">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-514">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span>

<span data-ttu-id="f8612-515">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span><span class="sxs-lookup"><span data-stu-id="f8612-515">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span></span>

---
 
### <a name="new-step-by-step-deployment-guides-for-azure-active-directory"></a><span data-ttu-id="f8612-516">New step-by-step deployment guides for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-516">New step-by-step deployment guides for Azure Active Directory</span></span>

<span data-ttu-id="f8612-517">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-517">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-518">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-518">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-519">**Product capability:** Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-519">**Product capability:** Directory</span></span>
 
<span data-ttu-id="f8612-520">New, step-by-step guidance about how to deploy Azure Active Directory (Azure AD), including self-service password reset (SSPR), single sign-on (SSO), conditional access (CA), App proxy, User provisioning, Active Directory Federation Services (ADFS) to Pass-through Authentication (PTA), and ADFS to Password hash sync (PHS).</span><span class="sxs-lookup"><span data-stu-id="f8612-520">New, step-by-step guidance about how to deploy Azure Active Directory (Azure AD), including self-service password reset (SSPR), single sign-on (SSO), conditional access (CA), App proxy, User provisioning, Active Directory Federation Services (ADFS) to Pass-through Authentication (PTA), and ADFS to Password hash sync (PHS).</span></span>

<span data-ttu-id="f8612-521">To view the deployment guides, go to the [Identity Deployment Guides](https://aka.ms/DeploymentPlans) repo on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8612-521">To view the deployment guides, go to the [Identity Deployment Guides](https://aka.ms/DeploymentPlans) repo on GitHub.</span></span> <span data-ttu-id="f8612-522">To provide feedback about the deployment guides, use the [Deployment Plan Feedback form](https://aka.ms/deploymentplanfeedback).</span><span class="sxs-lookup"><span data-stu-id="f8612-522">To provide feedback about the deployment guides, use the [Deployment Plan Feedback form](https://aka.ms/deploymentplanfeedback).</span></span> <span data-ttu-id="f8612-523">If you have any questions about the deployment guides, contact us at [IDGitDeploy](mailto:idgitdeploy@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f8612-523">If you have any questions about the deployment guides, contact us at [IDGitDeploy](mailto:idgitdeploy@microsoft.com).</span></span>

---

### <a name="enterprise-applications-search---load-more-apps"></a><span data-ttu-id="f8612-524">Enterprise Applications Search - Load More Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-524">Enterprise Applications Search - Load More Apps</span></span>

<span data-ttu-id="f8612-525">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-525">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-526">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-526">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-527">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-527">**Product capability:** SSO</span></span>
 
<span data-ttu-id="f8612-528">Having trouble finding your applications / service principals?</span><span class="sxs-lookup"><span data-stu-id="f8612-528">Having trouble finding your applications / service principals?</span></span> <span data-ttu-id="f8612-529">We've added the ability to load more applications in your enterprise applications all applications list.</span><span class="sxs-lookup"><span data-stu-id="f8612-529">We've added the ability to load more applications in your enterprise applications all applications list.</span></span> <span data-ttu-id="f8612-530">By default, we show 20 applications.</span><span class="sxs-lookup"><span data-stu-id="f8612-530">By default, we show 20 applications.</span></span> <span data-ttu-id="f8612-531">You can now click, **Load more** to view additional applications.</span><span class="sxs-lookup"><span data-stu-id="f8612-531">You can now click, **Load more** to view additional applications.</span></span> 

---
 
### <a name="the-may-release-of-aadconnect-contains-a-public-preview-of-the-integration-with-pingfederate-important-security-updates-many-bug-fixes-and-new-great-new-troubleshooting-tools"></a><span data-ttu-id="f8612-532">The May release of AADConnect contains a public preview of the integration with PingFederate, important security updates, many bug fixes, and new great new troubleshooting tools.</span><span class="sxs-lookup"><span data-stu-id="f8612-532">The May release of AADConnect contains a public preview of the integration with PingFederate, important security updates, many bug fixes, and new great new troubleshooting tools.</span></span> 

<span data-ttu-id="f8612-533">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-533">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-534">**Service category:** AD Connect</span><span class="sxs-lookup"><span data-stu-id="f8612-534">**Service category:** AD Connect</span></span>  
<span data-ttu-id="f8612-535">**Product capability:** Identity Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="f8612-535">**Product capability:** Identity Lifecycle Management</span></span>
 
<span data-ttu-id="f8612-536">The May release of AADConnect contains a public preview of the integration with PingFederate, important security updates, many bug fixes, and new great new troubleshooting tools.</span><span class="sxs-lookup"><span data-stu-id="f8612-536">The May release of AADConnect contains a public preview of the integration with PingFederate, important security updates, many bug fixes, and new great new troubleshooting tools.</span></span> <span data-ttu-id="f8612-537">You can find the release notes [here](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-version-history#118190).</span><span class="sxs-lookup"><span data-stu-id="f8612-537">You can find the release notes [here](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-version-history#118190).</span></span>

---

### <a name="azure-ad-access-reviews-auto-apply"></a><span data-ttu-id="f8612-538">Azure AD access reviews: auto-apply</span><span class="sxs-lookup"><span data-stu-id="f8612-538">Azure AD access reviews: auto-apply</span></span>

<span data-ttu-id="f8612-539">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-539">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-540">**Service category:** Access Reviews</span><span class="sxs-lookup"><span data-stu-id="f8612-540">**Service category:** Access Reviews</span></span>  
<span data-ttu-id="f8612-541">**Product capability:** Governance</span><span class="sxs-lookup"><span data-stu-id="f8612-541">**Product capability:** Governance</span></span>

<span data-ttu-id="f8612-542">Access reviews of groups and apps are now generally available as part of Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="f8612-542">Access reviews of groups and apps are now generally available as part of Azure AD Premium P2.</span></span> <span data-ttu-id="f8612-543">An administrator can configure to automatically apply the reviewer's changes to that group or app as the access review completes.</span><span class="sxs-lookup"><span data-stu-id="f8612-543">An administrator can configure to automatically apply the reviewer's changes to that group or app as the access review completes.</span></span> <span data-ttu-id="f8612-544">The administrator can also specify what happens to the user's continued access if reviewers didn't respond, remove access, keep access, or take system recommendations.</span><span class="sxs-lookup"><span data-stu-id="f8612-544">The administrator can also specify what happens to the user's continued access if reviewers didn't respond, remove access, keep access, or take system recommendations.</span></span> 

---

### <a name="id-tokens-can-no-longer-be-returned-using-the-query-responsemode-for-new-apps"></a><span data-ttu-id="f8612-545">ID tokens can no longer be returned using the query response_mode for new apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-545">ID tokens can no longer be returned using the query response_mode for new apps.</span></span> 

<span data-ttu-id="f8612-546">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-546">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-547">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-547">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-548">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-548">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-549">Apps created on or after April 25, 2018 will no longer be able to request an **id_token** using the **query** response_mode.</span><span class="sxs-lookup"><span data-stu-id="f8612-549">Apps created on or after April 25, 2018 will no longer be able to request an **id_token** using the **query** response_mode.</span></span>  <span data-ttu-id="f8612-550">This brings Azure AD inline with the OIDC specifications and helps reduce your apps attack surface.</span><span class="sxs-lookup"><span data-stu-id="f8612-550">This brings Azure AD inline with the OIDC specifications and helps reduce your apps attack surface.</span></span>  <span data-ttu-id="f8612-551">Apps created before April 25, 2018 are not blocked from using the **query** response_mode with a response_type of **id_token**.</span><span class="sxs-lookup"><span data-stu-id="f8612-551">Apps created before April 25, 2018 are not blocked from using the **query** response_mode with a response_type of **id_token**.</span></span>  <span data-ttu-id="f8612-552">The error returned, when requesting an id_token from AAD, is **AADSTS70007: ‘query’ is not a supported value of ‘response_mode’ when requesting a token**.</span><span class="sxs-lookup"><span data-stu-id="f8612-552">The error returned, when requesting an id_token from AAD, is **AADSTS70007: ‘query’ is not a supported value of ‘response_mode’ when requesting a token**.</span></span>

<span data-ttu-id="f8612-553">The **fragment** and **form_post** response_modes continue to work - when creating new application objects (for example, for App Proxy usage), ensure use of one of these response_modes before they create a new application.</span><span class="sxs-lookup"><span data-stu-id="f8612-553">The **fragment** and **form_post** response_modes continue to work - when creating new application objects (for example, for App Proxy usage), ensure use of one of these response_modes before they create a new application.</span></span>  
 
---
 
## <a name="april-2018"></a><span data-ttu-id="f8612-554">April 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-554">April 2018</span></span> 

### <a name="azure-ad-b2c-access-token-are-ga"></a><span data-ttu-id="f8612-555">Azure AD B2C Access Token are GA</span><span class="sxs-lookup"><span data-stu-id="f8612-555">Azure AD B2C Access Token are GA</span></span>

<span data-ttu-id="f8612-556">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-556">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-557">**Service category:** B2C - Consumer Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-557">**Service category:** B2C - Consumer Identity Management</span></span>  
<span data-ttu-id="f8612-558">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-558">**Product capability:** B2B/B2C</span></span> 

<span data-ttu-id="f8612-559">You can now access Web APIs secured by Azure AD B2C using access tokens.</span><span class="sxs-lookup"><span data-stu-id="f8612-559">You can now access Web APIs secured by Azure AD B2C using access tokens.</span></span> <span data-ttu-id="f8612-560">The feature is moving from public preview to GA.</span><span class="sxs-lookup"><span data-stu-id="f8612-560">The feature is moving from public preview to GA.</span></span> <span data-ttu-id="f8612-561">The UI experience to configure Azure AD B2C applications and web APIs has been improved, and other minor improvements were made.</span><span class="sxs-lookup"><span data-stu-id="f8612-561">The UI experience to configure Azure AD B2C applications and web APIs has been improved, and other minor improvements were made.</span></span>
 
<span data-ttu-id="f8612-562">For more information, see [Azure AD B2C: Requesting access tokens](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="f8612-562">For more information, see [Azure AD B2C: Requesting access tokens](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-access-tokens).</span></span>

---

### <a name="test-single-sign-on-configuration-for-saml-based-applications"></a><span data-ttu-id="f8612-563">Test single sign-on configuration for SAML-based applications</span><span class="sxs-lookup"><span data-stu-id="f8612-563">Test single sign-on configuration for SAML-based applications</span></span>

<span data-ttu-id="f8612-564">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-564">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-565">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-565">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-566">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-566">**Product capability:** SSO</span></span>

<span data-ttu-id="f8612-567">When configuring SAML-based SSO applications, you're able to test the integration on the configuration page.</span><span class="sxs-lookup"><span data-stu-id="f8612-567">When configuring SAML-based SSO applications, you're able to test the integration on the configuration page.</span></span> <span data-ttu-id="f8612-568">If you encounter an error during sign in, you can provide the error in the testing experience and Azure AD provides you with resolution steps to solve the specific issue.</span><span class="sxs-lookup"><span data-stu-id="f8612-568">If you encounter an error during sign in, you can provide the error in the testing experience and Azure AD provides you with resolution steps to solve the specific issue.</span></span>

<span data-ttu-id="f8612-569">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-569">For more information, see:</span></span>

- [<span data-ttu-id="f8612-570">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="f8612-570">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)
- [<span data-ttu-id="f8612-571">How to debug SAML-based single sign-on to applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-571">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)

---
 
### <a name="azure-ad-terms-of-use-now-has-per-user-reporting"></a><span data-ttu-id="f8612-572">Azure AD Terms of Use now has per user reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-572">Azure AD Terms of Use now has per user reporting</span></span>

<span data-ttu-id="f8612-573">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-573">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-574">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-574">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-575">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-575">**Product capability:** Compliance</span></span>
 
<span data-ttu-id="f8612-576">Administrators can now select a given ToU and see all the users that have consented to that ToU and what date/time it took place.</span><span class="sxs-lookup"><span data-stu-id="f8612-576">Administrators can now select a given ToU and see all the users that have consented to that ToU and what date/time it took place.</span></span>

<span data-ttu-id="f8612-577">For more information, see the [Azure AD terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-577">For more information, see the [Azure AD terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>

---
 
### <a name="azure-ad-connect-health-risky-ip-for-ad-fs-extranet-lockout-protection"></a><span data-ttu-id="f8612-578">Azure AD Connect Health: Risky IP for AD FS extranet lockout protection</span><span class="sxs-lookup"><span data-stu-id="f8612-578">Azure AD Connect Health: Risky IP for AD FS extranet lockout protection</span></span> 

<span data-ttu-id="f8612-579">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-579">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-580">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-580">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-581">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-581">**Product capability:** Monitoring & Reporting</span></span>

<span data-ttu-id="f8612-582">Connect Health now supports the ability to detect IP addresses that exceed a threshold of failed U/P logins on an hourly or daily basis.</span><span class="sxs-lookup"><span data-stu-id="f8612-582">Connect Health now supports the ability to detect IP addresses that exceed a threshold of failed U/P logins on an hourly or daily basis.</span></span> <span data-ttu-id="f8612-583">The capabilities provided by this feature are:</span><span class="sxs-lookup"><span data-stu-id="f8612-583">The capabilities provided by this feature are:</span></span>

- <span data-ttu-id="f8612-584">Comprehensive report showing IP address and the number of failed logins generated on an hourly/daily basis with customizable threshold.</span><span class="sxs-lookup"><span data-stu-id="f8612-584">Comprehensive report showing IP address and the number of failed logins generated on an hourly/daily basis with customizable threshold.</span></span>
- <span data-ttu-id="f8612-585">Email-based alerts showing when a specific IP address has exceeded the threshold of failed U/P logins on an hourly/daily basis.</span><span class="sxs-lookup"><span data-stu-id="f8612-585">Email-based alerts showing when a specific IP address has exceeded the threshold of failed U/P logins on an hourly/daily basis.</span></span>
- <span data-ttu-id="f8612-586">A download option to do a detailed analysis of the data</span><span class="sxs-lookup"><span data-stu-id="f8612-586">A download option to do a detailed analysis of the data</span></span>

<span data-ttu-id="f8612-587">For more information, see [Risky IP Report](https://aka.ms/aadchriskyip).</span><span class="sxs-lookup"><span data-stu-id="f8612-587">For more information, see [Risky IP Report](https://aka.ms/aadchriskyip).</span></span>

---
 
### <a name="easy-app-config-with-metadata-file-or-url"></a><span data-ttu-id="f8612-588">Easy app config with metadata file or URL</span><span class="sxs-lookup"><span data-stu-id="f8612-588">Easy app config with metadata file or URL</span></span>

<span data-ttu-id="f8612-589">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-589">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-590">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-590">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-591">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-591">**Product capability:** SSO</span></span>

<span data-ttu-id="f8612-592">On the Enterprise applications page, administrators can upload a SAML metadata file to configure SAML based sign-on for AAD Gallery and Non-Gallery application.</span><span class="sxs-lookup"><span data-stu-id="f8612-592">On the Enterprise applications page, administrators can upload a SAML metadata file to configure SAML based sign-on for AAD Gallery and Non-Gallery application.</span></span>

<span data-ttu-id="f8612-593">Additionally, you can use Azure AD application federation metadata URL to configure SSO with the targeted application.</span><span class="sxs-lookup"><span data-stu-id="f8612-593">Additionally, you can use Azure AD application federation metadata URL to configure SSO with the targeted application.</span></span>

<span data-ttu-id="f8612-594">For more information, see [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps).</span><span class="sxs-lookup"><span data-stu-id="f8612-594">For more information, see [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps).</span></span>

---

### <a name="azure-ad-terms-of-use-now-generally-available"></a><span data-ttu-id="f8612-595">Azure AD Terms of use now generally available</span><span class="sxs-lookup"><span data-stu-id="f8612-595">Azure AD Terms of use now generally available</span></span>

<span data-ttu-id="f8612-596">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-596">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-597">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-597">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-598">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-598">**Product capability:** Compliance</span></span>
 

<span data-ttu-id="f8612-599">Azure AD Terms of Use have moved from public preview to generally available.</span><span class="sxs-lookup"><span data-stu-id="f8612-599">Azure AD Terms of Use have moved from public preview to generally available.</span></span>

<span data-ttu-id="f8612-600">For more information, see the [Azure AD terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-600">For more information, see the [Azure AD terms of use feature](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>

---

### <a name="allow-or-block-invitations-to-b2b-users-from-specific-organizations"></a><span data-ttu-id="f8612-601">Allow or block invitations to B2B users from specific organizations</span><span class="sxs-lookup"><span data-stu-id="f8612-601">Allow or block invitations to B2B users from specific organizations</span></span>

<span data-ttu-id="f8612-602">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-602">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-603">**Service category:** B2B</span><span class="sxs-lookup"><span data-stu-id="f8612-603">**Service category:** B2B</span></span>  
<span data-ttu-id="f8612-604">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-604">**Product capability:** B2B/B2C</span></span>
 

<span data-ttu-id="f8612-605">You can now specify which partner organizations you want to share and collaborate with in Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="f8612-605">You can now specify which partner organizations you want to share and collaborate with in Azure AD B2B Collaboration.</span></span> <span data-ttu-id="f8612-606">To do this, you can choose to create list of specific allow or deny domains.</span><span class="sxs-lookup"><span data-stu-id="f8612-606">To do this, you can choose to create list of specific allow or deny domains.</span></span> <span data-ttu-id="f8612-607">When a domain is blocked using these capabilities, employees can no longer send invitations to people in that domain.</span><span class="sxs-lookup"><span data-stu-id="f8612-607">When a domain is blocked using these capabilities, employees can no longer send invitations to people in that domain.</span></span>

<span data-ttu-id="f8612-608">This helps you to control access to your resources, while enabling a smooth experience for approved users.</span><span class="sxs-lookup"><span data-stu-id="f8612-608">This helps you to control access to your resources, while enabling a smooth experience for approved users.</span></span>

<span data-ttu-id="f8612-609">This B2B Collaboration feature is available for all Azure Active Directory customers and can be used in conjunction with Azure AD Premium features like conditional access and identity protection for more granular control of when and how external business users sign in and gain access.</span><span class="sxs-lookup"><span data-stu-id="f8612-609">This B2B Collaboration feature is available for all Azure Active Directory customers and can be used in conjunction with Azure AD Premium features like conditional access and identity protection for more granular control of when and how external business users sign in and gain access.</span></span>

<span data-ttu-id="f8612-610">For more information, see [Allow or block invitations to B2B users from specific organizations](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-allow-deny-list).</span><span class="sxs-lookup"><span data-stu-id="f8612-610">For more information, see [Allow or block invitations to B2B users from specific organizations](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-allow-deny-list).</span></span>

---
 
### <a name="new-federated-apps-available-in-azure-ad-app-gallery"></a><span data-ttu-id="f8612-611">New federated apps available in Azure AD app gallery</span><span class="sxs-lookup"><span data-stu-id="f8612-611">New federated apps available in Azure AD app gallery</span></span>

<span data-ttu-id="f8612-612">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-612">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-613">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-613">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-614">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-614">**Product capability:** 3rd Party Integration</span></span>

<span data-ttu-id="f8612-615">In April 2018, we've added these 13 new apps with Federation support to our app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-615">In April 2018, we've added these 13 new apps with Federation support to our app gallery:</span></span>

<span data-ttu-id="f8612-616">Criterion HCM, [FiscalNote](https://docs.microsoft.com/azure/active-directory/active-directory-saas-fiscalnote-tutorial), [Secret Server (On-Premises)](https://docs.microsoft.com/azure/active-directory/active-directory-saas-secretserver-on-premises-tutorial), [Dynamic Signal](https://docs.microsoft.com/azure/active-directory/active-directory-saas-dynamicsignal-tutorial), [mindWireless](https://docs.microsoft.com/azure/active-directory/active-directory-saas-mindwireless-tutorial), [OrgChart Now](https://docs.microsoft.com/azure/active-directory/active-directory-saas-orgchartnow-tutorial), [Ziflow](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ziflow-tutorial), [AppNeta Performance Monitor](https://docs.microsoft.com/azure/active-directory/active-directory-saas-appneta-tutorial), [Elium](https://docs.microsoft.com/azure/active-directory/active-directory-saas-elium-tutorial) , [Fluxx Labs](https://docs.microsoft.com/azure/active-directory/active-directory-saas-fluxxlabs-tutorial), [Cisco Cloud](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ciscocloud-tutorial), Shelf, [SafetyNet](https://docs.microsoft.com/azure/active-directory/active-directory-saas-safetynet-tutorial)</span><span class="sxs-lookup"><span data-stu-id="f8612-616">Criterion HCM, [FiscalNote](https://docs.microsoft.com/azure/active-directory/active-directory-saas-fiscalnote-tutorial), [Secret Server (On-Premises)](https://docs.microsoft.com/azure/active-directory/active-directory-saas-secretserver-on-premises-tutorial), [Dynamic Signal](https://docs.microsoft.com/azure/active-directory/active-directory-saas-dynamicsignal-tutorial), [mindWireless](https://docs.microsoft.com/azure/active-directory/active-directory-saas-mindwireless-tutorial), [OrgChart Now](https://docs.microsoft.com/azure/active-directory/active-directory-saas-orgchartnow-tutorial), [Ziflow](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ziflow-tutorial), [AppNeta Performance Monitor](https://docs.microsoft.com/azure/active-directory/active-directory-saas-appneta-tutorial), [Elium](https://docs.microsoft.com/azure/active-directory/active-directory-saas-elium-tutorial) , [Fluxx Labs](https://docs.microsoft.com/azure/active-directory/active-directory-saas-fluxxlabs-tutorial), [Cisco Cloud](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ciscocloud-tutorial), Shelf, [SafetyNet](https://docs.microsoft.com/azure/active-directory/active-directory-saas-safetynet-tutorial)</span></span>

<span data-ttu-id="f8612-617">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-617">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span>

<span data-ttu-id="f8612-618">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span><span class="sxs-lookup"><span data-stu-id="f8612-618">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span></span>

---
 
### <a name="grant-b2b-users-in-azure-ad-access-to-your-on-premises-applications-public-preview"></a><span data-ttu-id="f8612-619">Grant B2B users in Azure AD access to your on-premises applications (public preview)</span><span class="sxs-lookup"><span data-stu-id="f8612-619">Grant B2B users in Azure AD access to your on-premises applications (public preview)</span></span>

<span data-ttu-id="f8612-620">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-620">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-621">**Service category:** B2B</span><span class="sxs-lookup"><span data-stu-id="f8612-621">**Service category:** B2B</span></span>  
<span data-ttu-id="f8612-622">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-622">**Product capability:** B2B/B2C</span></span>

<span data-ttu-id="f8612-623">As an organization that uses Azure Active Directory (Azure AD) B2B collaboration capabilities to invite guest users from partner organizations to your Azure AD, you can now provide these B2B users access to on-premises apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-623">As an organization that uses Azure Active Directory (Azure AD) B2B collaboration capabilities to invite guest users from partner organizations to your Azure AD, you can now provide these B2B users access to on-premises apps.</span></span> <span data-ttu-id="f8612-624">These on-premises apps can use SAML-based authentication or Integrated Windows Authentication (IWA) with Kerberos constrained delegation (KCD).</span><span class="sxs-lookup"><span data-stu-id="f8612-624">These on-premises apps can use SAML-based authentication or Integrated Windows Authentication (IWA) with Kerberos constrained delegation (KCD).</span></span>

<span data-ttu-id="f8612-625">For more information, see [Grant B2B users in Azure AD access to your on-premises applications](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-hybrid-cloud-to-on-premises).</span><span class="sxs-lookup"><span data-stu-id="f8612-625">For more information, see [Grant B2B users in Azure AD access to your on-premises applications](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-hybrid-cloud-to-on-premises).</span></span>

---
 
### <a name="get-sso-integration-tutorials-from-the-azure-marketplace"></a><span data-ttu-id="f8612-626">Get SSO integration tutorials from the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f8612-626">Get SSO integration tutorials from the Azure Marketplace</span></span>

<span data-ttu-id="f8612-627">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-627">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-628">**Service category:** Other</span><span class="sxs-lookup"><span data-stu-id="f8612-628">**Service category:** Other</span></span>  
<span data-ttu-id="f8612-629">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-629">**Product capability:** 3rd Party Integration</span></span>

<span data-ttu-id="f8612-630">If an application that is listed in the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1) supports SAML based single sign-on, clicking **Get it now** provides you with the integration tutorial associated with that application.</span><span class="sxs-lookup"><span data-stu-id="f8612-630">If an application that is listed in the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1) supports SAML based single sign-on, clicking **Get it now** provides you with the integration tutorial associated with that application.</span></span> 

---

### <a name="faster-performance-of-azure-ad-automatic-user-provisioning-to-saas-applications"></a><span data-ttu-id="f8612-631">Faster performance of Azure AD automatic user provisioning to SaaS applications</span><span class="sxs-lookup"><span data-stu-id="f8612-631">Faster performance of Azure AD automatic user provisioning to SaaS applications</span></span>

<span data-ttu-id="f8612-632">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-632">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-633">**Service category:** App Provisioning</span><span class="sxs-lookup"><span data-stu-id="f8612-633">**Service category:** App Provisioning</span></span>  
<span data-ttu-id="f8612-634">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-634">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-635">Previously, customers using the Azure Active Directory user provisioning connectors for SaaS applications (for example Salesforce, ServiceNow, and Box) could experience slow performance if their Azure AD tenants contained over 100,000 combined users and groups, and they were using user and group assignments to determine which users should be provisioned.</span><span class="sxs-lookup"><span data-stu-id="f8612-635">Previously, customers using the Azure Active Directory user provisioning connectors for SaaS applications (for example Salesforce, ServiceNow, and Box) could experience slow performance if their Azure AD tenants contained over 100,000 combined users and groups, and they were using user and group assignments to determine which users should be provisioned.</span></span>

<span data-ttu-id="f8612-636">On April 2, 2018, significant performance enhancements were deployed to the Azure AD provisioning service that greatly reduce the amount of time needed to perform initial synchronizations between Azure Active Directory and target SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="f8612-636">On April 2, 2018, significant performance enhancements were deployed to the Azure AD provisioning service that greatly reduce the amount of time needed to perform initial synchronizations between Azure Active Directory and target SaaS applications.</span></span>

<span data-ttu-id="f8612-637">As a result, many customers that had initial synchronizations to apps that took many days or never completed, are now completing within a matter of minutes or hours.</span><span class="sxs-lookup"><span data-stu-id="f8612-637">As a result, many customers that had initial synchronizations to apps that took many days or never completed, are now completing within a matter of minutes or hours.</span></span>

<span data-ttu-id="f8612-638">For more information, see [What happens during provisioning?](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning#what-happens-during-provisioning)</span><span class="sxs-lookup"><span data-stu-id="f8612-638">For more information, see [What happens during provisioning?](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning#what-happens-during-provisioning)</span></span>

---

### <a name="self-service-password-reset-from-windows-10-lock-screen-for-hybrid-azure-ad-joined-machines"></a><span data-ttu-id="f8612-639">Self-service password reset from Windows 10 lock screen for hybrid Azure AD joined machines</span><span class="sxs-lookup"><span data-stu-id="f8612-639">Self-service password reset from Windows 10 lock screen for hybrid Azure AD joined machines</span></span>

<span data-ttu-id="f8612-640">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-640">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-641">**Service category:** Self Service Password Reset</span><span class="sxs-lookup"><span data-stu-id="f8612-641">**Service category:** Self Service Password Reset</span></span>  
<span data-ttu-id="f8612-642">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-642">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-643">We have updated the Windows 10 SSPR feature to include support for machines that are hybrid Azure AD joined.</span><span class="sxs-lookup"><span data-stu-id="f8612-643">We have updated the Windows 10 SSPR feature to include support for machines that are hybrid Azure AD joined.</span></span> <span data-ttu-id="f8612-644">This feature is available in Windows 10 RS4 allows users to reset their password from the lock screen of a Windows 10 machine.</span><span class="sxs-lookup"><span data-stu-id="f8612-644">This feature is available in Windows 10 RS4 allows users to reset their password from the lock screen of a Windows 10 machine.</span></span> <span data-ttu-id="f8612-645">Users who are enabled and registered for self-service password reset can utilize this feature.</span><span class="sxs-lookup"><span data-stu-id="f8612-645">Users who are enabled and registered for self-service password reset can utilize this feature.</span></span>

<span data-ttu-id="f8612-646">For more information, see [Azure AD password reset from the login screen](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-sspr-windows).</span><span class="sxs-lookup"><span data-stu-id="f8612-646">For more information, see [Azure AD password reset from the login screen](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-sspr-windows).</span></span>
 
---

## <a name="march-2018"></a><span data-ttu-id="f8612-647">March 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-647">March 2018</span></span>
 
### <a name="certificate-expire-notification"></a><span data-ttu-id="f8612-648">Certificate expire notification</span><span class="sxs-lookup"><span data-stu-id="f8612-648">Certificate expire notification</span></span>

<span data-ttu-id="f8612-649">**Type:** Fixed</span><span class="sxs-lookup"><span data-stu-id="f8612-649">**Type:** Fixed</span></span>  
<span data-ttu-id="f8612-650">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-650">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-651">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-651">**Product capability:** SSO</span></span>
 
<span data-ttu-id="f8612-652">Azure AD sends a notification when a certificate for a gallery or non-gallery application is about to expire.</span><span class="sxs-lookup"><span data-stu-id="f8612-652">Azure AD sends a notification when a certificate for a gallery or non-gallery application is about to expire.</span></span> 

<span data-ttu-id="f8612-653">Some users did not receive notifications for enterprise applications configured for SAML-based single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8612-653">Some users did not receive notifications for enterprise applications configured for SAML-based single sign-on.</span></span> <span data-ttu-id="f8612-654">This issue was resolved.</span><span class="sxs-lookup"><span data-stu-id="f8612-654">This issue was resolved.</span></span> <span data-ttu-id="f8612-655">Azure AD sends notification for certificates expiring in 7, 30 and 60 days.</span><span class="sxs-lookup"><span data-stu-id="f8612-655">Azure AD sends notification for certificates expiring in 7, 30 and 60 days.</span></span> <span data-ttu-id="f8612-656">You are able to see this event in the audit logs.</span><span class="sxs-lookup"><span data-stu-id="f8612-656">You are able to see this event in the audit logs.</span></span> 

<span data-ttu-id="f8612-657">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-657">For more information, see:</span></span>

- [<span data-ttu-id="f8612-658">Manage Certificates for federated single sign-on in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-658">Manage Certificates for federated single sign-on in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-sso-certs)
- [<span data-ttu-id="f8612-659">Audit activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="f8612-659">Audit activity reports in the Azure Active Directory portal</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)
 
---
 
### <a name="twitter-and-github-identity-providers-in-azure-ad-b2c"></a><span data-ttu-id="f8612-660">Twitter and GitHub identity providers in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-660">Twitter and GitHub identity providers in Azure AD B2C</span></span>

<span data-ttu-id="f8612-661">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-661">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-662">**Service category:** B2C - Consumer Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-662">**Service category:** B2C - Consumer Identity Management</span></span>  
<span data-ttu-id="f8612-663">**Product capability:** B2B/B2C</span><span class="sxs-lookup"><span data-stu-id="f8612-663">**Product capability:** B2B/B2C</span></span>
 
<span data-ttu-id="f8612-664">You can now add Twitter or GitHub as an identity provider in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f8612-664">You can now add Twitter or GitHub as an identity provider in Azure AD B2C.</span></span> <span data-ttu-id="f8612-665">Twitter is moving from public preview to GA.</span><span class="sxs-lookup"><span data-stu-id="f8612-665">Twitter is moving from public preview to GA.</span></span> <span data-ttu-id="f8612-666">GitHub is being released in public preview.</span><span class="sxs-lookup"><span data-stu-id="f8612-666">GitHub is being released in public preview.</span></span>

<span data-ttu-id="f8612-667">For more information, see [What is Azure AD B2B collaboration?](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).</span><span class="sxs-lookup"><span data-stu-id="f8612-667">For more information, see [What is Azure AD B2B collaboration?](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).</span></span>
 
---

### <a name="restrict-browser-access-using-intune-managed-browser-with-azure-ad-application-based-conditional-access-for-ios-and-android"></a><span data-ttu-id="f8612-668">Restrict browser access using Intune Managed Browser with Azure AD application-based conditional access for iOS and Android</span><span class="sxs-lookup"><span data-stu-id="f8612-668">Restrict browser access using Intune Managed Browser with Azure AD application-based conditional access for iOS and Android</span></span>

<span data-ttu-id="f8612-669">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-669">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-670">**Service category:** Conditional Access</span><span class="sxs-lookup"><span data-stu-id="f8612-670">**Service category:** Conditional Access</span></span>  
<span data-ttu-id="f8612-671">**Product capability:** Identity Security & Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-671">**Product capability:** Identity Security & Protection</span></span>
 
<span data-ttu-id="f8612-672">**Now in public preview!**</span><span class="sxs-lookup"><span data-stu-id="f8612-672">**Now in public preview!**</span></span>

<span data-ttu-id="f8612-673">**Intune Managed Browser SSO:** Your employees can use single sign-on across native clients (like Microsoft Outlook) and the Intune Managed Browser for all Azure AD-connected apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-673">**Intune Managed Browser SSO:** Your employees can use single sign-on across native clients (like Microsoft Outlook) and the Intune Managed Browser for all Azure AD-connected apps.</span></span>

<span data-ttu-id="f8612-674">**Intune Managed Browser Conditional Access Support:** You can now require employees to use the Intune Managed browser using application-based conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="f8612-674">**Intune Managed Browser Conditional Access Support:** You can now require employees to use the Intune Managed browser using application-based conditional access policies.</span></span>

<span data-ttu-id="f8612-675">Read more about this in our [blog post](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/15/the-intune-managed-browser-now-supports-azure-ad-sso-and-conditional-access/).</span><span class="sxs-lookup"><span data-stu-id="f8612-675">Read more about this in our [blog post](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/15/the-intune-managed-browser-now-supports-azure-ad-sso-and-conditional-access/).</span></span>

<span data-ttu-id="f8612-676">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-676">For more information, see:</span></span>

- [<span data-ttu-id="f8612-677">Setup application-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-677">Setup application-based conditional access</span></span>](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access)

- [<span data-ttu-id="f8612-678">Configure managed browser policies</span><span class="sxs-lookup"><span data-stu-id="f8612-678">Configure managed browser policies</span></span>](https://aka.ms/managedbrowser)  

---
 
### <a name="app-proxy-cmdlets-in-powershell-ga-module"></a><span data-ttu-id="f8612-679">App Proxy Cmdlets in Powershell GA Module</span><span class="sxs-lookup"><span data-stu-id="f8612-679">App Proxy Cmdlets in Powershell GA Module</span></span>

<span data-ttu-id="f8612-680">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-680">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-681">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-681">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-682">**Product capability:** Access Control</span><span class="sxs-lookup"><span data-stu-id="f8612-682">**Product capability:** Access Control</span></span>
 
<span data-ttu-id="f8612-683">Support for Application Proxy cmdlets is now in the Powershell GA Module!</span><span class="sxs-lookup"><span data-stu-id="f8612-683">Support for Application Proxy cmdlets is now in the Powershell GA Module!</span></span> <span data-ttu-id="f8612-684">This does require you to stay updated on Powershell modules - if you become more than a year behind, some cmdlets may stop working.</span><span class="sxs-lookup"><span data-stu-id="f8612-684">This does require you to stay updated on Powershell modules - if you become more than a year behind, some cmdlets may stop working.</span></span> 

<span data-ttu-id="f8612-685">For more information, see [AzureAD](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="f8612-685">For more information, see [AzureAD](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0).</span></span>
 
---
 
### <a name="office-365-native-clients-are-supported-by-seamless-sso-using-a-non-interactive-protocol"></a><span data-ttu-id="f8612-686">Office 365 native clients are supported by Seamless SSO using a non-interactive protocol</span><span class="sxs-lookup"><span data-stu-id="f8612-686">Office 365 native clients are supported by Seamless SSO using a non-interactive protocol</span></span>

<span data-ttu-id="f8612-687">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-687">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-688">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-688">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-689">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-689">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-690">User using Office 365 native clients (version 16.0.8730.xxxx and above) get a silent sign-on experience using Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="f8612-690">User using Office 365 native clients (version 16.0.8730.xxxx and above) get a silent sign-on experience using Seamless SSO.</span></span> <span data-ttu-id="f8612-691">This support is provided by the addition a non-interactive protocol (WS-Trust) to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-691">This support is provided by the addition a non-interactive protocol (WS-Trust) to Azure AD.</span></span>

<span data-ttu-id="f8612-692">For more information, see [How does sign-in on a native client with Seamless SSO work?](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso-how-it-works#how-does-sign-in-on-a-native-client-with-seamless-sso-work)</span><span class="sxs-lookup"><span data-stu-id="f8612-692">For more information, see [How does sign-in on a native client with Seamless SSO work?](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso-how-it-works#how-does-sign-in-on-a-native-client-with-seamless-sso-work)</span></span>
 
---

### <a name="users-get-a-silent-sign-on-experience-with-seamless-sso-if-an-application-sends-sign-in-requests-to-azure-ads-tenant-endpoints"></a><span data-ttu-id="f8612-693">Users get a silent sign-on experience, with Seamless SSO, if an application sends sign-in requests to Azure AD's tenant endpoints</span><span class="sxs-lookup"><span data-stu-id="f8612-693">Users get a silent sign-on experience, with Seamless SSO, if an application sends sign-in requests to Azure AD's tenant endpoints</span></span>

<span data-ttu-id="f8612-694">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-694">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-695">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-695">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-696">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-696">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-697">Users get a silent sign-on experience, with Seamless SSO, if an application (for example, `https://contoso.sharepoint.com`) sends sign-in requests to Azure AD's tenant endpoints - that is, `https://login.microsoftonline.com/contoso.com/<..>` or `https://login.microsoftonline.com/<tenant_ID>/<..>` - instead of Azure AD's common endpoint (`https://login.microsoftonline.com/common/<...>`).</span><span class="sxs-lookup"><span data-stu-id="f8612-697">Users get a silent sign-on experience, with Seamless SSO, if an application (for example, `https://contoso.sharepoint.com`) sends sign-in requests to Azure AD's tenant endpoints - that is, `https://login.microsoftonline.com/contoso.com/<..>` or `https://login.microsoftonline.com/<tenant_ID>/<..>` - instead of Azure AD's common endpoint (`https://login.microsoftonline.com/common/<...>`).</span></span>

<span data-ttu-id="f8612-698">For more information, see [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso).</span><span class="sxs-lookup"><span data-stu-id="f8612-698">For more information, see [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso).</span></span> 

---
 
### <a name="need-to-add-only-one-azure-ad-url-instead-of-two-urls-previously-to-users-intranet-zone-settings-to-roll-out-seamless-sso"></a><span data-ttu-id="f8612-699">Need to add only one Azure AD URL, instead of two URLs previously, to users' Intranet zone settings to roll out Seamless SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-699">Need to add only one Azure AD URL, instead of two URLs previously, to users' Intranet zone settings to roll out Seamless SSO</span></span>

<span data-ttu-id="f8612-700">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-700">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-701">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-701">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-702">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-702">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-703">To roll out Seamless SSO to your users, you need to add only one Azure AD URL to the users' Intranet zone settings by using group policy in Active Directory: `https://autologon.microsoftazuread-sso.com`.</span><span class="sxs-lookup"><span data-stu-id="f8612-703">To roll out Seamless SSO to your users, you need to add only one Azure AD URL to the users' Intranet zone settings by using group policy in Active Directory: `https://autologon.microsoftazuread-sso.com`.</span></span> <span data-ttu-id="f8612-704">Previously, customers were required to add two URLs.</span><span class="sxs-lookup"><span data-stu-id="f8612-704">Previously, customers were required to add two URLs.</span></span>

<span data-ttu-id="f8612-705">For more information, see [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso).</span><span class="sxs-lookup"><span data-stu-id="f8612-705">For more information, see [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso).</span></span> 
 
---
 
### <a name="new-federated-apps-available-in-azure-ad-app-gallery"></a><span data-ttu-id="f8612-706">New Federated Apps available in Azure AD app gallery</span><span class="sxs-lookup"><span data-stu-id="f8612-706">New Federated Apps available in Azure AD app gallery</span></span>

<span data-ttu-id="f8612-707">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-707">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-708">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-708">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-709">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-709">**Product capability:** 3rd Party Integration</span></span>

<span data-ttu-id="f8612-710">In March 2018, we've added these 15 new apps with Federation support to our app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-710">In March 2018, we've added these 15 new apps with Federation support to our app gallery:</span></span>

<span data-ttu-id="f8612-711">[Boxcryptor](https://docs.microsoft.com/azure/active-directory/active-directory-saas-boxcryptor-tutorial), [CylancePROTECT](https://docs.microsoft.com/azure/active-directory/active-directory-saas-cylanceprotect-tutorial), Wrike, [SignalFx](https://docs.microsoft.com/azure/active-directory/active-directory-saas-signalfx-tutorial), Assistant by FirstAgenda, [YardiOne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-yardione-tutorial), Vtiger CRM, inwink, [Amplitude](https://docs.microsoft.com/azure/active-directory/active-directory-saas-amplitude-tutorial), [Spacio](https://docs.microsoft.com/azure/active-directory/active-directory-saas-spacio-tutorial), [ContractWorks](https://docs.microsoft.com/azure/active-directory/active-directory-saas-contractworks-tutorial), [Bersin](https://docs.microsoft.com/azure/active-directory/active-directory-saas-bersin-tutorial), [Mercell](https://docs.microsoft.com/azure/active-directory/active-directory-saas-mercell-tutorial), [Trisotech Digital Enterprise Server](https://docs.microsoft.com/azure/active-directory/active-directory-saas-trisotechdigitalenterpriseserver-tutorial), [Qumu Cloud](https://docs.microsoft.com/azure/active-directory/active-directory-saas-qumucloud-tutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-711">[Boxcryptor](https://docs.microsoft.com/azure/active-directory/active-directory-saas-boxcryptor-tutorial), [CylancePROTECT](https://docs.microsoft.com/azure/active-directory/active-directory-saas-cylanceprotect-tutorial), Wrike, [SignalFx](https://docs.microsoft.com/azure/active-directory/active-directory-saas-signalfx-tutorial), Assistant by FirstAgenda, [YardiOne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-yardione-tutorial), Vtiger CRM, inwink, [Amplitude](https://docs.microsoft.com/azure/active-directory/active-directory-saas-amplitude-tutorial), [Spacio](https://docs.microsoft.com/azure/active-directory/active-directory-saas-spacio-tutorial), [ContractWorks](https://docs.microsoft.com/azure/active-directory/active-directory-saas-contractworks-tutorial), [Bersin](https://docs.microsoft.com/azure/active-directory/active-directory-saas-bersin-tutorial), [Mercell](https://docs.microsoft.com/azure/active-directory/active-directory-saas-mercell-tutorial), [Trisotech Digital Enterprise Server](https://docs.microsoft.com/azure/active-directory/active-directory-saas-trisotechdigitalenterpriseserver-tutorial), [Qumu Cloud](https://docs.microsoft.com/azure/active-directory/active-directory-saas-qumucloud-tutorial).</span></span>
 
<span data-ttu-id="f8612-712">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-712">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span>

<span data-ttu-id="f8612-713">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span><span class="sxs-lookup"><span data-stu-id="f8612-713">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span></span> 

---
 
### <a name="pim-for-azure-resources-is-generally-available"></a><span data-ttu-id="f8612-714">PIM for Azure Resources is generally available</span><span class="sxs-lookup"><span data-stu-id="f8612-714">PIM for Azure Resources is generally available</span></span>

<span data-ttu-id="f8612-715">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-715">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-716">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-716">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-717">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-717">**Product capability:** Privileged Identity Management</span></span>
 
<span data-ttu-id="f8612-718">If you are using Azure AD Privileged Identity Management for directory roles, you can now use PIM's time-bound access and assignment capabilities for Azure Resource roles such as Subscriptions, Resource Groups, Virtual Machines, and any other resource supported by Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f8612-718">If you are using Azure AD Privileged Identity Management for directory roles, you can now use PIM's time-bound access and assignment capabilities for Azure Resource roles such as Subscriptions, Resource Groups, Virtual Machines, and any other resource supported by Azure Resource Manager.</span></span> <span data-ttu-id="f8612-719">Enforce Multi-Factor Authentication when activating roles Just-In-Time, and schedule activations in coordination with approved change windows.</span><span class="sxs-lookup"><span data-stu-id="f8612-719">Enforce Multi-Factor Authentication when activating roles Just-In-Time, and schedule activations in coordination with approved change windows.</span></span> <span data-ttu-id="f8612-720">In addition, this release adds enhancements not available during public preview including an updated UI, approval workflows, and the ability to extend roles expiring soon and renew expired roles.</span><span class="sxs-lookup"><span data-stu-id="f8612-720">In addition, this release adds enhancements not available during public preview including an updated UI, approval workflows, and the ability to extend roles expiring soon and renew expired roles.</span></span>

<span data-ttu-id="f8612-721">For more information, see [PIM for Azure resources (Preview)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac)</span><span class="sxs-lookup"><span data-stu-id="f8612-721">For more information, see [PIM for Azure resources (Preview)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac)</span></span>
 
---
 
### <a name="adding-optional-claims-to-your-apps-tokens-public-preview"></a><span data-ttu-id="f8612-722">Adding Optional Claims to your apps tokens (public preview)</span><span class="sxs-lookup"><span data-stu-id="f8612-722">Adding Optional Claims to your apps tokens (public preview)</span></span>

<span data-ttu-id="f8612-723">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-723">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-724">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-724">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-725">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-725">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-726">Your Azure AD app can now request custom or optional claims in JWTs or SAML tokens.</span><span class="sxs-lookup"><span data-stu-id="f8612-726">Your Azure AD app can now request custom or optional claims in JWTs or SAML tokens.</span></span>  <span data-ttu-id="f8612-727">These are claims about the user or tenant that are not included by default in the token, due to size or applicability constraints.</span><span class="sxs-lookup"><span data-stu-id="f8612-727">These are claims about the user or tenant that are not included by default in the token, due to size or applicability constraints.</span></span>  <span data-ttu-id="f8612-728">This is currently in public preview for Azure AD apps on the v1.0 and v2.0 endpoints.</span><span class="sxs-lookup"><span data-stu-id="f8612-728">This is currently in public preview for Azure AD apps on the v1.0 and v2.0 endpoints.</span></span>  <span data-ttu-id="f8612-729">See the documentation for information on what claims can be added and how to edit your application manifest to request them.</span><span class="sxs-lookup"><span data-stu-id="f8612-729">See the documentation for information on what claims can be added and how to edit your application manifest to request them.</span></span>  

<span data-ttu-id="f8612-730">For more information, see [Optional claims in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims).</span><span class="sxs-lookup"><span data-stu-id="f8612-730">For more information, see [Optional claims in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims).</span></span>
 
---
 
### <a name="azure-ad-supports-pkce-for-more-secure-oauth-flows"></a><span data-ttu-id="f8612-731">Azure AD supports PKCE for more secure OAuth flows</span><span class="sxs-lookup"><span data-stu-id="f8612-731">Azure AD supports PKCE for more secure OAuth flows</span></span>

<span data-ttu-id="f8612-732">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-732">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-733">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-733">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-734">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-734">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-735">Azure AD docs have been updated to note support for PKCE, which allows for more secure communication during the OAuth 2.0 Authorization Code grant flow.</span><span class="sxs-lookup"><span data-stu-id="f8612-735">Azure AD docs have been updated to note support for PKCE, which allows for more secure communication during the OAuth 2.0 Authorization Code grant flow.</span></span>  <span data-ttu-id="f8612-736">Both S256 and plaintext code_challenges are supported on the v1.0 and v2.0 endpoints.</span><span class="sxs-lookup"><span data-stu-id="f8612-736">Both S256 and plaintext code_challenges are supported on the v1.0 and v2.0 endpoints.</span></span> 

<span data-ttu-id="f8612-737">For more information, see [Request an authorization code](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-protocols-oauth-code#request-an-authorization-code).</span><span class="sxs-lookup"><span data-stu-id="f8612-737">For more information, see [Request an authorization code](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-protocols-oauth-code#request-an-authorization-code).</span></span> 
 
---
 
### <a name="support-for-provisioning-all-user-attribute-values-available-in-the-workday-getworkers-api"></a><span data-ttu-id="f8612-738">Support for provisioning all user attribute values available in the Workday Get_Workers API</span><span class="sxs-lookup"><span data-stu-id="f8612-738">Support for provisioning all user attribute values available in the Workday Get_Workers API</span></span>

<span data-ttu-id="f8612-739">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-739">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-740">**Service category:** App Provisioning</span><span class="sxs-lookup"><span data-stu-id="f8612-740">**Service category:** App Provisioning</span></span>  
<span data-ttu-id="f8612-741">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-741">**Product capability:** 3rd Party Integration</span></span>
 
<span data-ttu-id="f8612-742">The public preview of inbound provisioning from Workday to Active Directory and Azure AD now supports the ability to extract and provisioning all attribute values available in the Workday Get_Workers API.</span><span class="sxs-lookup"><span data-stu-id="f8612-742">The public preview of inbound provisioning from Workday to Active Directory and Azure AD now supports the ability to extract and provisioning all attribute values available in the Workday Get_Workers API.</span></span> <span data-ttu-id="f8612-743">This adds supports for hundreds of additional standard and custom attributes beyond the ones shipped with the initial version of the Workday inbound provisioning connector.</span><span class="sxs-lookup"><span data-stu-id="f8612-743">This adds supports for hundreds of additional standard and custom attributes beyond the ones shipped with the initial version of the Workday inbound provisioning connector.</span></span>

<span data-ttu-id="f8612-744">For more information, see: [Customizing the list of Workday user attributes](https://docs.microsoft.com/azure/active-directory/active-directory-saas-workday-inbound-tutorial#customizing-the-list-of-workday-user-attributes)</span><span class="sxs-lookup"><span data-stu-id="f8612-744">For more information, see: [Customizing the list of Workday user attributes](https://docs.microsoft.com/azure/active-directory/active-directory-saas-workday-inbound-tutorial#customizing-the-list-of-workday-user-attributes)</span></span>

---

### <a name="changing-group-membership-from-dynamic-to-static-and-vice-versa"></a><span data-ttu-id="f8612-745">Changing group membership from dynamic to static, and vice versa</span><span class="sxs-lookup"><span data-stu-id="f8612-745">Changing group membership from dynamic to static, and vice versa</span></span>

<span data-ttu-id="f8612-746">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-746">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-747">**Service category:** Group Management</span><span class="sxs-lookup"><span data-stu-id="f8612-747">**Service category:** Group Management</span></span>  
<span data-ttu-id="f8612-748">**Product capability:** Collaboration</span><span class="sxs-lookup"><span data-stu-id="f8612-748">**Product capability:** Collaboration</span></span>
 
<span data-ttu-id="f8612-749">It is possible to change how membership is managed in a group.</span><span class="sxs-lookup"><span data-stu-id="f8612-749">It is possible to change how membership is managed in a group.</span></span> <span data-ttu-id="f8612-750">This is useful when you want to keep the same group name and ID in the system, so any existing references to the group are still valid; creating a new group would require updating those references.</span><span class="sxs-lookup"><span data-stu-id="f8612-750">This is useful when you want to keep the same group name and ID in the system, so any existing references to the group are still valid; creating a new group would require updating those references.</span></span>
<span data-ttu-id="f8612-751">We've updated the Azure AD Admin center to support this functionality.</span><span class="sxs-lookup"><span data-stu-id="f8612-751">We've updated the Azure AD Admin center to support this functionality.</span></span> <span data-ttu-id="f8612-752">Now, customers can convert existing groups from dynamic membership to assigned membership and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="f8612-752">Now, customers can convert existing groups from dynamic membership to assigned membership and vice-versa.</span></span> <span data-ttu-id="f8612-753">The existing PowerShell cmdlets are also still available.</span><span class="sxs-lookup"><span data-stu-id="f8612-753">The existing PowerShell cmdlets are also still available.</span></span>

<span data-ttu-id="f8612-754">For more information, see [Changing dynamic membership to static and vice-versa](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#changing-dynamic-membership-to-static-and-vice-versa)</span><span class="sxs-lookup"><span data-stu-id="f8612-754">For more information, see [Changing dynamic membership to static and vice-versa](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#changing-dynamic-membership-to-static-and-vice-versa)</span></span>

---

### <a name="improved-sign-out-behavior-with-seamless-sso"></a><span data-ttu-id="f8612-755">Improved sign-out behavior with Seamless SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-755">Improved sign-out behavior with Seamless SSO</span></span>

<span data-ttu-id="f8612-756">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-756">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-757">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-757">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-758">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-758">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-759">Previously, even if users explicitly signed out of an application secured by Azure AD, they would be automatically signed back in using Seamless SSO if they were trying to access an Azure AD application again within their corpnet from their domain joined devices.</span><span class="sxs-lookup"><span data-stu-id="f8612-759">Previously, even if users explicitly signed out of an application secured by Azure AD, they would be automatically signed back in using Seamless SSO if they were trying to access an Azure AD application again within their corpnet from their domain joined devices.</span></span> <span data-ttu-id="f8612-760">With this change, sign out is supported.</span><span class="sxs-lookup"><span data-stu-id="f8612-760">With this change, sign out is supported.</span></span>  <span data-ttu-id="f8612-761">This allows users to choose the same or different Azure AD account to sign back in with, instead of being automatically signed in using Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="f8612-761">This allows users to choose the same or different Azure AD account to sign back in with, instead of being automatically signed in using Seamless SSO.</span></span>

<span data-ttu-id="f8612-762">For more information, see [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso)</span><span class="sxs-lookup"><span data-stu-id="f8612-762">For more information, see [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso)</span></span>
 
---
 
### <a name="application-proxy-connector-version-154020-released"></a><span data-ttu-id="f8612-763">Application Proxy Connector Version 1.5.402.0 Released</span><span class="sxs-lookup"><span data-stu-id="f8612-763">Application Proxy Connector Version 1.5.402.0 Released</span></span>

<span data-ttu-id="f8612-764">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-764">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-765">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-765">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-766">**Product capability:** Identity Security & Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-766">**Product capability:** Identity Security & Protection</span></span>
 
<span data-ttu-id="f8612-767">This connector version is gradually being rolled out through November.</span><span class="sxs-lookup"><span data-stu-id="f8612-767">This connector version is gradually being rolled out through November.</span></span> <span data-ttu-id="f8612-768">This new connector version includes the following changes:</span><span class="sxs-lookup"><span data-stu-id="f8612-768">This new connector version includes the following changes:</span></span>

- <span data-ttu-id="f8612-769">The connector now sets domain level cookies instead subdomain level.</span><span class="sxs-lookup"><span data-stu-id="f8612-769">The connector now sets domain level cookies instead subdomain level.</span></span> <span data-ttu-id="f8612-770">This ensures a smoother SSO experience and avoids redundant authentication prompts.</span><span class="sxs-lookup"><span data-stu-id="f8612-770">This ensures a smoother SSO experience and avoids redundant authentication prompts.</span></span>
- <span data-ttu-id="f8612-771">Support for chunked encoding requests</span><span class="sxs-lookup"><span data-stu-id="f8612-771">Support for chunked encoding requests</span></span>
- <span data-ttu-id="f8612-772">Improved connector health monitoring</span><span class="sxs-lookup"><span data-stu-id="f8612-772">Improved connector health monitoring</span></span> 
- <span data-ttu-id="f8612-773">Several bug fixes and stability improvements</span><span class="sxs-lookup"><span data-stu-id="f8612-773">Several bug fixes and stability improvements</span></span>

<span data-ttu-id="f8612-774">For more information, see [Understand Azure AD Application Proxy connectors](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="f8612-774">For more information, see [Understand Azure AD Application Proxy connectors](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>
 
---

## <a name="february-2018"></a><span data-ttu-id="f8612-775">February 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-775">February 2018</span></span>
 
### <a name="improved-navigation-for-managing-users-and-groups"></a><span data-ttu-id="f8612-776">Improved navigation for managing users and groups</span><span class="sxs-lookup"><span data-stu-id="f8612-776">Improved navigation for managing users and groups</span></span>

<span data-ttu-id="f8612-777">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-777">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-778">**Service category:** Directory Management</span><span class="sxs-lookup"><span data-stu-id="f8612-778">**Service category:** Directory Management</span></span>  
<span data-ttu-id="f8612-779">**Product capability:** Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-779">**Product capability:** Directory</span></span>

<span data-ttu-id="f8612-780">The navigation experience for managing users and groups has been streamlined.</span><span class="sxs-lookup"><span data-stu-id="f8612-780">The navigation experience for managing users and groups has been streamlined.</span></span> <span data-ttu-id="f8612-781">You can now navigate from the directory overview directly to the list of all users, with easier access to the list of deleted users.</span><span class="sxs-lookup"><span data-stu-id="f8612-781">You can now navigate from the directory overview directly to the list of all users, with easier access to the list of deleted users.</span></span> <span data-ttu-id="f8612-782">You can also navigate from the directory overview directly to the list of all groups, with easier access to group management settings.</span><span class="sxs-lookup"><span data-stu-id="f8612-782">You can also navigate from the directory overview directly to the list of all groups, with easier access to group management settings.</span></span> <span data-ttu-id="f8612-783">And also from the directory overview page, you can search for a user, group, enterprise application, or app registration.</span><span class="sxs-lookup"><span data-stu-id="f8612-783">And also from the directory overview page, you can search for a user, group, enterprise application, or app registration.</span></span> 

---

### <a name="availability-of-sign-ins-and-audit-reports-in-microsoft-azure-operated-by-21vianet-azure-china-21vianet"></a><span data-ttu-id="f8612-784">Availability of sign-ins and audit reports in Microsoft Azure operated by 21Vianet (Azure China 21Vianet)</span><span class="sxs-lookup"><span data-stu-id="f8612-784">Availability of sign-ins and audit reports in Microsoft Azure operated by 21Vianet (Azure China 21Vianet)</span></span>

<span data-ttu-id="f8612-785">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-785">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-786">**Service category:** Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f8612-786">**Service category:** Azure Stack</span></span>  
<span data-ttu-id="f8612-787">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-787">**Product capability:** Monitoring & Reporting</span></span>

<span data-ttu-id="f8612-788">Azure AD Activity log reports are now available in Microsoft Azure operated by 21Vianet (Azure China 21Vianet) instances.</span><span class="sxs-lookup"><span data-stu-id="f8612-788">Azure AD Activity log reports are now available in Microsoft Azure operated by 21Vianet (Azure China 21Vianet) instances.</span></span> <span data-ttu-id="f8612-789">The following logs are included:</span><span class="sxs-lookup"><span data-stu-id="f8612-789">The following logs are included:</span></span>

- <span data-ttu-id="f8612-790">**Sign-ins activity logs**  - Includes all the sign-ins logs associated with your tenant.</span><span class="sxs-lookup"><span data-stu-id="f8612-790">**Sign-ins activity logs**  - Includes all the sign-ins logs associated with your tenant.</span></span>

- <span data-ttu-id="f8612-791">**Self service Password Audit Logs** - Includes all the SSPR audit logs.</span><span class="sxs-lookup"><span data-stu-id="f8612-791">**Self service Password Audit Logs** - Includes all the SSPR audit logs.</span></span>

- <span data-ttu-id="f8612-792">**Directory Management Audit logs** - Includes all the directory management-related audit logs like User management, App Management, and others.</span><span class="sxs-lookup"><span data-stu-id="f8612-792">**Directory Management Audit logs** - Includes all the directory management-related audit logs like User management, App Management, and others.</span></span>

<span data-ttu-id="f8612-793">With these logs, you can gain insights into how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="f8612-793">With these logs, you can gain insights into how your environment is doing.</span></span> <span data-ttu-id="f8612-794">The provided data enables you to:</span><span class="sxs-lookup"><span data-stu-id="f8612-794">The provided data enables you to:</span></span>

- <span data-ttu-id="f8612-795">Determine how your apps and services are utilized by your users.</span><span class="sxs-lookup"><span data-stu-id="f8612-795">Determine how your apps and services are utilized by your users.</span></span>

- <span data-ttu-id="f8612-796">Troubleshoot issues preventing your users from getting their work done.</span><span class="sxs-lookup"><span data-stu-id="f8612-796">Troubleshoot issues preventing your users from getting their work done.</span></span>

<span data-ttu-id="f8612-797">For more information about how to use these reports, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f8612-797">For more information about how to use these reports, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal).</span></span>

---

### <a name="use-report-reader-role-non-admin-role-to-view-azure-ad-activity-reports"></a><span data-ttu-id="f8612-798">Use "Report Reader" role (non-admin role) to view Azure AD Activity Reports</span><span class="sxs-lookup"><span data-stu-id="f8612-798">Use "Report Reader" role (non-admin role) to view Azure AD Activity Reports</span></span>

<span data-ttu-id="f8612-799">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-799">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-800">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-800">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-801">**Product capability:** Monitoring & Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-801">**Product capability:** Monitoring & Reporting</span></span>

<span data-ttu-id="f8612-802">As part of customers feedback to enable non-admin roles to have access to Azure AD activity logs, we have enabled the ability for users who are in the "Report Reader" role to access Sign-ins and Audit activity within the Azure portal as well as using our Graph APIs.</span><span class="sxs-lookup"><span data-stu-id="f8612-802">As part of customers feedback to enable non-admin roles to have access to Azure AD activity logs, we have enabled the ability for users who are in the "Report Reader" role to access Sign-ins and Audit activity within the Azure portal as well as using our Graph APIs.</span></span> 

<span data-ttu-id="f8612-803">For more information, how to use these reports, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f8612-803">For more information, how to use these reports, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal).</span></span> 

---

### <a name="employeeid-claim-available-as-user-attribute-and-user-identifier"></a><span data-ttu-id="f8612-804">EmployeeID claim available as user attribute and user identifier</span><span class="sxs-lookup"><span data-stu-id="f8612-804">EmployeeID claim available as user attribute and user identifier</span></span>

<span data-ttu-id="f8612-805">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-805">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-806">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-806">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-807">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-807">**Product capability:** SSO</span></span>
 
<span data-ttu-id="f8612-808">You can configure **EmployeeID** as the User identifier and User attribute for member users and B2B guests in SAML-based sign-on applications from the Enterprise application UI.</span><span class="sxs-lookup"><span data-stu-id="f8612-808">You can configure **EmployeeID** as the User identifier and User attribute for member users and B2B guests in SAML-based sign-on applications from the Enterprise application UI.</span></span>

<span data-ttu-id="f8612-809">For more information, see [Customizing claims issued in the SAML token for enterprise applications in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization).</span><span class="sxs-lookup"><span data-stu-id="f8612-809">For more information, see [Customizing claims issued in the SAML token for enterprise applications in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization).</span></span>

---

### <a name="simplified-application-management-using-wildcards-in-azure-ad-application-proxy"></a><span data-ttu-id="f8612-810">Simplified Application Management using Wildcards in Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-810">Simplified Application Management using Wildcards in Azure AD Application Proxy</span></span>

<span data-ttu-id="f8612-811">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-811">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-812">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-812">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-813">**Product capability:** User Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-813">**Product capability:** User Authentication</span></span>
 
<span data-ttu-id="f8612-814">To make application deployment easier and reduce your administrative overhead, we now support the ability to publish applications using wildcards.</span><span class="sxs-lookup"><span data-stu-id="f8612-814">To make application deployment easier and reduce your administrative overhead, we now support the ability to publish applications using wildcards.</span></span> <span data-ttu-id="f8612-815">To publish a wildcard application, you can follow the standard application publishing flow, but use a wildcard in the internal and external URLs.</span><span class="sxs-lookup"><span data-stu-id="f8612-815">To publish a wildcard application, you can follow the standard application publishing flow, but use a wildcard in the internal and external URLs.</span></span>

<span data-ttu-id="f8612-816">For more information, see [Wildcard applications in the Azure Active Directory application proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-wildcard)</span><span class="sxs-lookup"><span data-stu-id="f8612-816">For more information, see [Wildcard applications in the Azure Active Directory application proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-wildcard)</span></span>

---

### <a name="new-cmdlets-to-support-configuration-of-application-proxy"></a><span data-ttu-id="f8612-817">New cmdlets to support configuration of Application Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-817">New cmdlets to support configuration of Application Proxy</span></span>

<span data-ttu-id="f8612-818">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-818">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-819">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-819">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-820">**Product capability:** Platform</span><span class="sxs-lookup"><span data-stu-id="f8612-820">**Product capability:** Platform</span></span>

<span data-ttu-id="f8612-821">The latest release of the AzureAD PowerShell Preview module contains new cmdlets that allow customers to configure Application Proxy Applications using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8612-821">The latest release of the AzureAD PowerShell Preview module contains new cmdlets that allow customers to configure Application Proxy Applications using PowerShell.</span></span>

<span data-ttu-id="f8612-822">The new cmdlets are:</span><span class="sxs-lookup"><span data-stu-id="f8612-822">The new cmdlets are:</span></span> 

- <span data-ttu-id="f8612-823">Get-AzureADApplicationProxyApplication</span><span class="sxs-lookup"><span data-stu-id="f8612-823">Get-AzureADApplicationProxyApplication</span></span>
- <span data-ttu-id="f8612-824">Get-AzureADApplicationProxyApplicationConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-824">Get-AzureADApplicationProxyApplicationConnectorGroup</span></span>
- <span data-ttu-id="f8612-825">Get-AzureADApplicationProxyConnector</span><span class="sxs-lookup"><span data-stu-id="f8612-825">Get-AzureADApplicationProxyConnector</span></span>
- <span data-ttu-id="f8612-826">Get-AzureADApplicationProxyConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-826">Get-AzureADApplicationProxyConnectorGroup</span></span>
- <span data-ttu-id="f8612-827">Get-AzureADApplicationProxyConnectorGroupMembers</span><span class="sxs-lookup"><span data-stu-id="f8612-827">Get-AzureADApplicationProxyConnectorGroupMembers</span></span>
- <span data-ttu-id="f8612-828">Get-AzureADApplicationProxyConnectorMemberOf</span><span class="sxs-lookup"><span data-stu-id="f8612-828">Get-AzureADApplicationProxyConnectorMemberOf</span></span>
- <span data-ttu-id="f8612-829">New-AzureADApplicationProxyApplication</span><span class="sxs-lookup"><span data-stu-id="f8612-829">New-AzureADApplicationProxyApplication</span></span>
- <span data-ttu-id="f8612-830">New-AzureADApplicationProxyConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-830">New-AzureADApplicationProxyConnectorGroup</span></span>
- <span data-ttu-id="f8612-831">Remove-AzureADApplicationProxyApplication</span><span class="sxs-lookup"><span data-stu-id="f8612-831">Remove-AzureADApplicationProxyApplication</span></span>
- <span data-ttu-id="f8612-832">Remove-AzureADApplicationProxyApplicationConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-832">Remove-AzureADApplicationProxyApplicationConnectorGroup</span></span>
- <span data-ttu-id="f8612-833">Remove-AzureADApplicationProxyConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-833">Remove-AzureADApplicationProxyConnectorGroup</span></span>
- <span data-ttu-id="f8612-834">Set-AzureADApplicationProxyApplication</span><span class="sxs-lookup"><span data-stu-id="f8612-834">Set-AzureADApplicationProxyApplication</span></span>
- <span data-ttu-id="f8612-835">Set-AzureADApplicationProxyApplicationConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-835">Set-AzureADApplicationProxyApplicationConnectorGroup</span></span>
- <span data-ttu-id="f8612-836">Set-AzureADApplicationProxyApplicationCustomDomainCertificate</span><span class="sxs-lookup"><span data-stu-id="f8612-836">Set-AzureADApplicationProxyApplicationCustomDomainCertificate</span></span>
- <span data-ttu-id="f8612-837">Set-AzureADApplicationProxyApplicationSingleSignOn</span><span class="sxs-lookup"><span data-stu-id="f8612-837">Set-AzureADApplicationProxyApplicationSingleSignOn</span></span>
- <span data-ttu-id="f8612-838">Set-AzureADApplicationProxyConnector</span><span class="sxs-lookup"><span data-stu-id="f8612-838">Set-AzureADApplicationProxyConnector</span></span>
- <span data-ttu-id="f8612-839">Set-AzureADApplicationProxyConnectorGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-839">Set-AzureADApplicationProxyConnectorGroup</span></span>

---
 
### <a name="new-cmdlets-to-support-configuration-of-groups"></a><span data-ttu-id="f8612-840">New cmdlets to support configuration of groups</span><span class="sxs-lookup"><span data-stu-id="f8612-840">New cmdlets to support configuration of groups</span></span>

<span data-ttu-id="f8612-841">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-841">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-842">**Service category:** App Proxy</span><span class="sxs-lookup"><span data-stu-id="f8612-842">**Service category:** App Proxy</span></span>  
<span data-ttu-id="f8612-843">**Product capability:** Platform</span><span class="sxs-lookup"><span data-stu-id="f8612-843">**Product capability:** Platform</span></span>

<span data-ttu-id="f8612-844">The latest release of the AzureAD PowerShell module contains cmdlets to manage groups in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-844">The latest release of the AzureAD PowerShell module contains cmdlets to manage groups in Azure AD.</span></span> <span data-ttu-id="f8612-845">These cmdlets were previously available in the AzureADPreview module and are now added to the AzureAD module</span><span class="sxs-lookup"><span data-stu-id="f8612-845">These cmdlets were previously available in the AzureADPreview module and are now added to the AzureAD module</span></span>

<span data-ttu-id="f8612-846">The Group cmdlets that are now release for General Availability are:</span><span class="sxs-lookup"><span data-stu-id="f8612-846">The Group cmdlets that are now release for General Availability are:</span></span> 

- <span data-ttu-id="f8612-847">Get-AzureADMSGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-847">Get-AzureADMSGroup</span></span>
- <span data-ttu-id="f8612-848">New-AzureADMSGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-848">New-AzureADMSGroup</span></span>
- <span data-ttu-id="f8612-849">Remove-AzureADMSGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-849">Remove-AzureADMSGroup</span></span>
- <span data-ttu-id="f8612-850">Set-AzureADMSGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-850">Set-AzureADMSGroup</span></span>
- <span data-ttu-id="f8612-851">Get-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="f8612-851">Get-AzureADMSGroupLifecyclePolicy</span></span>
- <span data-ttu-id="f8612-852">New-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="f8612-852">New-AzureADMSGroupLifecyclePolicy</span></span>
- <span data-ttu-id="f8612-853">Remove-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="f8612-853">Remove-AzureADMSGroupLifecyclePolicy</span></span>
- <span data-ttu-id="f8612-854">Add-AzureADMSLifecyclePolicyGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-854">Add-AzureADMSLifecyclePolicyGroup</span></span>
- <span data-ttu-id="f8612-855">Remove-AzureADMSLifecyclePolicyGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-855">Remove-AzureADMSLifecyclePolicyGroup</span></span>
- <span data-ttu-id="f8612-856">Reset-AzureADMSLifeCycleGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-856">Reset-AzureADMSLifeCycleGroup</span></span>   
- <span data-ttu-id="f8612-857">Get-AzureADMSLifecyclePolicyGroup</span><span class="sxs-lookup"><span data-stu-id="f8612-857">Get-AzureADMSLifecyclePolicyGroup</span></span>

---
 
### <a name="a-new-release-of-azure-ad-connect-is-available"></a><span data-ttu-id="f8612-858">A new release of Azure AD Connect is available</span><span class="sxs-lookup"><span data-stu-id="f8612-858">A new release of Azure AD Connect is available</span></span>

<span data-ttu-id="f8612-859">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-859">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-860">**Service category:** AD Sync</span><span class="sxs-lookup"><span data-stu-id="f8612-860">**Service category:** AD Sync</span></span>  
<span data-ttu-id="f8612-861">**Product capability:** Platform</span><span class="sxs-lookup"><span data-stu-id="f8612-861">**Product capability:** Platform</span></span>
 
<span data-ttu-id="f8612-862">Azure AD Connect is the preferred tool to synchronize data between Azure AD and on premises data sources, including Windows Server Active Directory and LDAP.</span><span class="sxs-lookup"><span data-stu-id="f8612-862">Azure AD Connect is the preferred tool to synchronize data between Azure AD and on premises data sources, including Windows Server Active Directory and LDAP.</span></span>

>[!Important]
><span data-ttu-id="f8612-863">This build introduces schema and sync rule changes.</span><span class="sxs-lookup"><span data-stu-id="f8612-863">This build introduces schema and sync rule changes.</span></span> <span data-ttu-id="f8612-864">The Azure AD Connect Synchronization Service triggers a Full Import and Full Synchronization steps after an upgrade.</span><span class="sxs-lookup"><span data-stu-id="f8612-864">The Azure AD Connect Synchronization Service triggers a Full Import and Full Synchronization steps after an upgrade.</span></span> <span data-ttu-id="f8612-865">For information on how to change this behavior, see [How to defer full synchronization after upgrade](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#how-to-defer-full-synchronization-after-upgrade).</span><span class="sxs-lookup"><span data-stu-id="f8612-865">For information on how to change this behavior, see [How to defer full synchronization after upgrade](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#how-to-defer-full-synchronization-after-upgrade).</span></span>

<span data-ttu-id="f8612-866">This release has the following updates and changes:</span><span class="sxs-lookup"><span data-stu-id="f8612-866">This release has the following updates and changes:</span></span>

<span data-ttu-id="f8612-867">**Fixed issues**</span><span class="sxs-lookup"><span data-stu-id="f8612-867">**Fixed issues**</span></span>

- <span data-ttu-id="f8612-868">Fix timing window on background tasks for Partition Filtering page when switching to next page.</span><span class="sxs-lookup"><span data-stu-id="f8612-868">Fix timing window on background tasks for Partition Filtering page when switching to next page.</span></span>

- <span data-ttu-id="f8612-869">Fixed a bug that caused Access violation during the ConfigDB custom action.</span><span class="sxs-lookup"><span data-stu-id="f8612-869">Fixed a bug that caused Access violation during the ConfigDB custom action.</span></span>

- <span data-ttu-id="f8612-870">Fixed a bug to recover from sql connection timeout.</span><span class="sxs-lookup"><span data-stu-id="f8612-870">Fixed a bug to recover from sql connection timeout.</span></span>

- <span data-ttu-id="f8612-871">Fixed a bug where certificates with SAN wildcards fail pre-req check.</span><span class="sxs-lookup"><span data-stu-id="f8612-871">Fixed a bug where certificates with SAN wildcards fail pre-req check.</span></span>

- <span data-ttu-id="f8612-872">Fixed a bug that causes miiserver.exe crash during AAD connector export.</span><span class="sxs-lookup"><span data-stu-id="f8612-872">Fixed a bug that causes miiserver.exe crash during AAD connector export.</span></span>

- <span data-ttu-id="f8612-873">Fixed a bug where a bad password attempt logged on DC when running caused the AAD connect wizard to change configuration</span><span class="sxs-lookup"><span data-stu-id="f8612-873">Fixed a bug where a bad password attempt logged on DC when running caused the AAD connect wizard to change configuration</span></span>

<span data-ttu-id="f8612-874">**New features and improvements**</span><span class="sxs-lookup"><span data-stu-id="f8612-874">**New features and improvements**</span></span>
 
- <span data-ttu-id="f8612-875">Application telemetry - Administrators can switch this class of data on/off.</span><span class="sxs-lookup"><span data-stu-id="f8612-875">Application telemetry - Administrators can switch this class of data on/off.</span></span>

- <span data-ttu-id="f8612-876">Azure AD Health data - Administrators must visit the health portal to control their health settings.</span><span class="sxs-lookup"><span data-stu-id="f8612-876">Azure AD Health data - Administrators must visit the health portal to control their health settings.</span></span> <span data-ttu-id="f8612-877">Once the service policy has been changed, the agents will read and enforce it.</span><span class="sxs-lookup"><span data-stu-id="f8612-877">Once the service policy has been changed, the agents will read and enforce it.</span></span>

- <span data-ttu-id="f8612-878">Added device writeback configuration actions and a progress bar for page initialization.</span><span class="sxs-lookup"><span data-stu-id="f8612-878">Added device writeback configuration actions and a progress bar for page initialization.</span></span>

- <span data-ttu-id="f8612-879">Improved general diagnostics with HTML report and full data collection in a ZIP-Text / HTML Report.</span><span class="sxs-lookup"><span data-stu-id="f8612-879">Improved general diagnostics with HTML report and full data collection in a ZIP-Text / HTML Report.</span></span>

- <span data-ttu-id="f8612-880">Improved reliability of auto upgrade and added additional telemetry to ensure the health of the server can be determined.</span><span class="sxs-lookup"><span data-stu-id="f8612-880">Improved reliability of auto upgrade and added additional telemetry to ensure the health of the server can be determined.</span></span>

- <span data-ttu-id="f8612-881">Restrict permissions available to privileged accounts on AD Connector account.</span><span class="sxs-lookup"><span data-stu-id="f8612-881">Restrict permissions available to privileged accounts on AD Connector account.</span></span> <span data-ttu-id="f8612-882">For new installations, the wizard restricts the permissions that privileged accounts have on the MSOL account after creating the MSOL account.</span><span class="sxs-lookup"><span data-stu-id="f8612-882">For new installations, the wizard restricts the permissions that privileged accounts have on the MSOL account after creating the MSOL account.</span></span> <span data-ttu-id="f8612-883">The changes affect express installations and custom installations with Auto-Create account.</span><span class="sxs-lookup"><span data-stu-id="f8612-883">The changes affect express installations and custom installations with Auto-Create account.</span></span>

- <span data-ttu-id="f8612-884">Changed the installer to not require SA privilege on clean install of AADConnect.</span><span class="sxs-lookup"><span data-stu-id="f8612-884">Changed the installer to not require SA privilege on clean install of AADConnect.</span></span>

- <span data-ttu-id="f8612-885">New utility to troubleshoot synchronization issues for a specific object.</span><span class="sxs-lookup"><span data-stu-id="f8612-885">New utility to troubleshoot synchronization issues for a specific object.</span></span> <span data-ttu-id="f8612-886">Currently, the utility checks for the following things:</span><span class="sxs-lookup"><span data-stu-id="f8612-886">Currently, the utility checks for the following things:</span></span>

    - <span data-ttu-id="f8612-887">UserPrincipalName mismatch between synchronized user object and the user account in Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="f8612-887">UserPrincipalName mismatch between synchronized user object and the user account in Azure AD Tenant.</span></span>
  
    - <span data-ttu-id="f8612-888">If the object is filtered from synchronization due to domain filtering</span><span class="sxs-lookup"><span data-stu-id="f8612-888">If the object is filtered from synchronization due to domain filtering</span></span>
  
    - <span data-ttu-id="f8612-889">If the object is filtered from synchronization due to organizational unit (OU) filtering</span><span class="sxs-lookup"><span data-stu-id="f8612-889">If the object is filtered from synchronization due to organizational unit (OU) filtering</span></span>

- <span data-ttu-id="f8612-890">New utility to synchronize the current password hash stored in the on-premises Active Directory for a specific user account.</span><span class="sxs-lookup"><span data-stu-id="f8612-890">New utility to synchronize the current password hash stored in the on-premises Active Directory for a specific user account.</span></span> <span data-ttu-id="f8612-891">The utility does not require a password change.</span><span class="sxs-lookup"><span data-stu-id="f8612-891">The utility does not require a password change.</span></span> 

---
 
### <a name="applications-supporting-intune-app-protection-policies-added-for-use-with-azure-ad-application-based-conditional-access"></a><span data-ttu-id="f8612-892">Applications supporting Intune App Protection policies added for use with Azure AD application-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-892">Applications supporting Intune App Protection policies added for use with Azure AD application-based conditional access</span></span>

<span data-ttu-id="f8612-893">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-893">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-894">**Service category:** Conditional Access</span><span class="sxs-lookup"><span data-stu-id="f8612-894">**Service category:** Conditional Access</span></span>  
<span data-ttu-id="f8612-895">**Product capability:** Identity Security & Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-895">**Product capability:** Identity Security & Protection</span></span>

<span data-ttu-id="f8612-896">We have added more applications that support application-based conditional access.</span><span class="sxs-lookup"><span data-stu-id="f8612-896">We have added more applications that support application-based conditional access.</span></span> <span data-ttu-id="f8612-897">Now, you can get access to Office 365 and other Azure AD-connected cloud apps using these approved client apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-897">Now, you can get access to Office 365 and other Azure AD-connected cloud apps using these approved client apps.</span></span>

<span data-ttu-id="f8612-898">The following applications will be added by the end of February:</span><span class="sxs-lookup"><span data-stu-id="f8612-898">The following applications will be added by the end of February:</span></span>

- <span data-ttu-id="f8612-899">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="f8612-899">Microsoft Power BI</span></span>

- <span data-ttu-id="f8612-900">Microsoft Launcher</span><span class="sxs-lookup"><span data-stu-id="f8612-900">Microsoft Launcher</span></span>

- <span data-ttu-id="f8612-901">Microsoft Invoicing</span><span class="sxs-lookup"><span data-stu-id="f8612-901">Microsoft Invoicing</span></span>

<span data-ttu-id="f8612-902">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-902">For more information, see:</span></span>

- [<span data-ttu-id="f8612-903">Approved client app requirement</span><span class="sxs-lookup"><span data-stu-id="f8612-903">Approved client app requirement</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement)
- [<span data-ttu-id="f8612-904">Azure AD app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-904">Azure AD app-based conditional access</span></span>](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access)

---

### <a name="terms-of-use-update-to-mobile-experience"></a><span data-ttu-id="f8612-905">Terms of Use update to mobile experience</span><span class="sxs-lookup"><span data-stu-id="f8612-905">Terms of Use update to mobile experience</span></span> 

<span data-ttu-id="f8612-906">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-906">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-907">**Service category:** Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f8612-907">**Service category:** Terms of Use</span></span>  
<span data-ttu-id="f8612-908">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-908">**Product capability:** Compliance</span></span>

<span data-ttu-id="f8612-909">When the terms of use are displayed, you can now click **Having trouble viewing? Click here**.</span><span class="sxs-lookup"><span data-stu-id="f8612-909">When the terms of use are displayed, you can now click **Having trouble viewing? Click here**.</span></span> <span data-ttu-id="f8612-910">Clicking this link opens the terms of use natively on your device.</span><span class="sxs-lookup"><span data-stu-id="f8612-910">Clicking this link opens the terms of use natively on your device.</span></span> <span data-ttu-id="f8612-911">Regardless of the font size in the document or the screen size of device, you can zoom and read the document as needed.</span><span class="sxs-lookup"><span data-stu-id="f8612-911">Regardless of the font size in the document or the screen size of device, you can zoom and read the document as needed.</span></span> 

---
 
## <a name="january-2018"></a><span data-ttu-id="f8612-912">January 2018</span><span class="sxs-lookup"><span data-stu-id="f8612-912">January 2018</span></span>
 
### <a name="new-federated-apps-available-in-azure-ad-app-gallery"></a><span data-ttu-id="f8612-913">New Federated Apps available in Azure AD app gallery</span><span class="sxs-lookup"><span data-stu-id="f8612-913">New Federated Apps available in Azure AD app gallery</span></span> 

<span data-ttu-id="f8612-914">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-914">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-915">**Service category:** Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-915">**Service category:** Enterprise Apps</span></span>  
<span data-ttu-id="f8612-916">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-916">**Product capability:** 3rd Party Integration</span></span>

<span data-ttu-id="f8612-917">In January 2018, the following new apps with federation support were added in the app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-917">In January 2018, the following new apps with federation support were added in the app gallery:</span></span>

<span data-ttu-id="f8612-918">[IBM OpenPages](https://go.microsoft.com/fwlink/?linkid=864698), [OneTrust Privacy Management Software](https://go.microsoft.com/fwlink/?linkid=861660), [Dealpath](https://go.microsoft.com/fwlink/?linkid=863526), [IriusRisk Federated Directory, and [Fidelity NetBenefits](https://go.microsoft.com/fwlink/?linkid=864701).</span><span class="sxs-lookup"><span data-stu-id="f8612-918">[IBM OpenPages](https://go.microsoft.com/fwlink/?linkid=864698), [OneTrust Privacy Management Software](https://go.microsoft.com/fwlink/?linkid=861660), [Dealpath](https://go.microsoft.com/fwlink/?linkid=863526), [IriusRisk Federated Directory, and [Fidelity NetBenefits](https://go.microsoft.com/fwlink/?linkid=864701).</span></span>

<span data-ttu-id="f8612-919">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-919">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span>

<span data-ttu-id="f8612-920">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span><span class="sxs-lookup"><span data-stu-id="f8612-920">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span></span> 

---
 
### <a name="sign-in-with-additional-risk-detected"></a><span data-ttu-id="f8612-921">Sign in with additional risk detected</span><span class="sxs-lookup"><span data-stu-id="f8612-921">Sign in with additional risk detected</span></span>

<span data-ttu-id="f8612-922">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-922">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-923">**Service category:** Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-923">**Service category:** Identity Protection</span></span>  
<span data-ttu-id="f8612-924">**Product capability:** Identity Security & Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-924">**Product capability:** Identity Security & Protection</span></span>

<span data-ttu-id="f8612-925">The insight you get for a detected risk event is tied to your Azure AD subscription.</span><span class="sxs-lookup"><span data-stu-id="f8612-925">The insight you get for a detected risk event is tied to your Azure AD subscription.</span></span> <span data-ttu-id="f8612-926">With the Azure AD Premium P2 edition, you get the most detailed information about all underlying detections.</span><span class="sxs-lookup"><span data-stu-id="f8612-926">With the Azure AD Premium P2 edition, you get the most detailed information about all underlying detections.</span></span>

<span data-ttu-id="f8612-927">With the Azure AD Premium P1 edition, detections that are not covered by your license appear as the risk event Sign-in with additional risk detected.</span><span class="sxs-lookup"><span data-stu-id="f8612-927">With the Azure AD Premium P1 edition, detections that are not covered by your license appear as the risk event Sign-in with additional risk detected.</span></span>

<span data-ttu-id="f8612-928">For more information, see [Azure Active Directory risk events](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events).</span><span class="sxs-lookup"><span data-stu-id="f8612-928">For more information, see [Azure Active Directory risk events](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events).</span></span>
 
---

### <a name="hide-office-365-applications-from-end-users-access-panels"></a><span data-ttu-id="f8612-929">Hide Office 365 applications from end user's access panels</span><span class="sxs-lookup"><span data-stu-id="f8612-929">Hide Office 365 applications from end user's access panels</span></span>

<span data-ttu-id="f8612-930">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-930">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-931">**Service category:** My Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-931">**Service category:** My Apps</span></span>  
<span data-ttu-id="f8612-932">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-932">**Product capability:** SSO</span></span>

<span data-ttu-id="f8612-933">You can now better manage how Office 365 applications show up on your user's access panels through a new user setting.</span><span class="sxs-lookup"><span data-stu-id="f8612-933">You can now better manage how Office 365 applications show up on your user's access panels through a new user setting.</span></span> <span data-ttu-id="f8612-934">This option is helpful for reducing the number of apps in a user's access panels if you prefer to only show Office apps in the Office portal.</span><span class="sxs-lookup"><span data-stu-id="f8612-934">This option is helpful for reducing the number of apps in a user's access panels if you prefer to only show Office apps in the Office portal.</span></span> <span data-ttu-id="f8612-935">The setting is located in the **User Settings** and is labeled, **Users can only see Office 365 apps in the Office 365 portal**.</span><span class="sxs-lookup"><span data-stu-id="f8612-935">The setting is located in the **User Settings** and is labeled, **Users can only see Office 365 apps in the Office 365 portal**.</span></span>

<span data-ttu-id="f8612-936">For more information, see [Hide an application from user's experience in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-hide-third-party-app).</span><span class="sxs-lookup"><span data-stu-id="f8612-936">For more information, see [Hide an application from user's experience in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-hide-third-party-app).</span></span>

---
 
### <a name="seamless-sign-into-apps-enabled-for-password-sso-directly-from-apps-url"></a><span data-ttu-id="f8612-937">Seamless sign into apps enabled for Password SSO directly from app's URL</span><span class="sxs-lookup"><span data-stu-id="f8612-937">Seamless sign into apps enabled for Password SSO directly from app's URL</span></span> 

<span data-ttu-id="f8612-938">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-938">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-939">**Service category:** My Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-939">**Service category:** My Apps</span></span>  
<span data-ttu-id="f8612-940">**Product capability:** SSO</span><span class="sxs-lookup"><span data-stu-id="f8612-940">**Product capability:** SSO</span></span>

<span data-ttu-id="f8612-941">The My Apps browser extension is now available via a convenient tool that gives you the My Apps single-sign on capability as a shortcut in your browser.</span><span class="sxs-lookup"><span data-stu-id="f8612-941">The My Apps browser extension is now available via a convenient tool that gives you the My Apps single-sign on capability as a shortcut in your browser.</span></span> <span data-ttu-id="f8612-942">After installing, user's will see a waffle icon in their browser that provides them quick access to apps.</span><span class="sxs-lookup"><span data-stu-id="f8612-942">After installing, user's will see a waffle icon in their browser that provides them quick access to apps.</span></span> <span data-ttu-id="f8612-943">Users can now take advantage of:</span><span class="sxs-lookup"><span data-stu-id="f8612-943">Users can now take advantage of:</span></span>

- <span data-ttu-id="f8612-944">The ability to directly sign in to password-SSO based apps from the app’s sign-in page</span><span class="sxs-lookup"><span data-stu-id="f8612-944">The ability to directly sign in to password-SSO based apps from the app’s sign-in page</span></span>
- <span data-ttu-id="f8612-945">Launch any app using the quick search feature</span><span class="sxs-lookup"><span data-stu-id="f8612-945">Launch any app using the quick search feature</span></span>
- <span data-ttu-id="f8612-946">Shortcuts to recently used apps from the extension</span><span class="sxs-lookup"><span data-stu-id="f8612-946">Shortcuts to recently used apps from the extension</span></span>
- <span data-ttu-id="f8612-947">The extension is available for Edge, Chrome, and Firefox.</span><span class="sxs-lookup"><span data-stu-id="f8612-947">The extension is available for Edge, Chrome, and Firefox.</span></span>
 
<span data-ttu-id="f8612-948">For more information, see [My Apps Secure Sign-in Extension](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction#my-apps-secure-sign-in-extension).</span><span class="sxs-lookup"><span data-stu-id="f8612-948">For more information, see [My Apps Secure Sign-in Extension](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction#my-apps-secure-sign-in-extension).</span></span>

---

### <a name="azure-ad-administration-experience-in-azure-classic-portal-has-been-retired"></a><span data-ttu-id="f8612-949">Azure AD administration experience in Azure Classic Portal has been retired</span><span class="sxs-lookup"><span data-stu-id="f8612-949">Azure AD administration experience in Azure Classic Portal has been retired</span></span>

<span data-ttu-id="f8612-950">**Type:** Deprecated</span><span class="sxs-lookup"><span data-stu-id="f8612-950">**Type:** Deprecated</span></span>   
<span data-ttu-id="f8612-951">**Service category:** Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-951">**Service category:** Azure AD</span></span>  
<span data-ttu-id="f8612-952">**Product capability:** Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-952">**Product capability:** Directory</span></span>

<span data-ttu-id="f8612-953">As of January 8, 2018, the Azure AD administration experience in the Azure classic portal has been retired.</span><span class="sxs-lookup"><span data-stu-id="f8612-953">As of January 8, 2018, the Azure AD administration experience in the Azure classic portal has been retired.</span></span> <span data-ttu-id="f8612-954">This took place in conjunction with the retirement of the Azure classic portal itself.</span><span class="sxs-lookup"><span data-stu-id="f8612-954">This took place in conjunction with the retirement of the Azure classic portal itself.</span></span> <span data-ttu-id="f8612-955">In the future, you should use the [Azure AD admin center](https://aad.portal.azure.com) for all your portal-based administration of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-955">In the future, you should use the [Azure AD admin center](https://aad.portal.azure.com) for all your portal-based administration of Azure AD.</span></span>
 
---

### <a name="the-phonefactor-web-portal-has-been-retired"></a><span data-ttu-id="f8612-956">The PhoneFactor web portal has been retired</span><span class="sxs-lookup"><span data-stu-id="f8612-956">The PhoneFactor web portal has been retired</span></span>

<span data-ttu-id="f8612-957">**Type:** Deprecated</span><span class="sxs-lookup"><span data-stu-id="f8612-957">**Type:** Deprecated</span></span>  
<span data-ttu-id="f8612-958">**Service category:** Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-958">**Service category:** Azure AD</span></span>  
<span data-ttu-id="f8612-959">**Product capability:** Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-959">**Product capability:** Directory</span></span>
 
<span data-ttu-id="f8612-960">As of January 8, 2018, the PhoneFactor web portal has been retired.</span><span class="sxs-lookup"><span data-stu-id="f8612-960">As of January 8, 2018, the PhoneFactor web portal has been retired.</span></span> <span data-ttu-id="f8612-961">This portal was used for the administration of MFA server, but those functions have been moved into the Azure portal at portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="f8612-961">This portal was used for the administration of MFA server, but those functions have been moved into the Azure portal at portal.azure.com.</span></span> 

<span data-ttu-id="f8612-962">The MFA configuration is located at: **Azure Active Directory \> MFA Server**</span><span class="sxs-lookup"><span data-stu-id="f8612-962">The MFA configuration is located at: **Azure Active Directory \> MFA Server**</span></span>
 
---
 
### <a name="deprecate-azure-ad-reports"></a><span data-ttu-id="f8612-963">Deprecate Azure AD reports</span><span class="sxs-lookup"><span data-stu-id="f8612-963">Deprecate Azure AD reports</span></span>

<span data-ttu-id="f8612-964">**Type:** Deprecated</span><span class="sxs-lookup"><span data-stu-id="f8612-964">**Type:** Deprecated</span></span>  
<span data-ttu-id="f8612-965">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-965">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-966">**Product capability:** Identity Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="f8612-966">**Product capability:** Identity Lifecycle Management</span></span>  


<span data-ttu-id="f8612-967">With the general availability of the new Azure Active Directory Administration console and new APIs now available for both activity and security reports, the report APIs under "/reports" endpoint have been retired as of end of December 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="f8612-967">With the general availability of the new Azure Active Directory Administration console and new APIs now available for both activity and security reports, the report APIs under "/reports" endpoint have been retired as of end of December 31, 2017.</span></span>

<span data-ttu-id="f8612-968">**What's available?**</span><span class="sxs-lookup"><span data-stu-id="f8612-968">**What's available?**</span></span>

<span data-ttu-id="f8612-969">As part of the transition to the new admin console, we have made 2 new APIs available for retrieving Azure AD Activity Logs.</span><span class="sxs-lookup"><span data-stu-id="f8612-969">As part of the transition to the new admin console, we have made 2 new APIs available for retrieving Azure AD Activity Logs.</span></span> <span data-ttu-id="f8612-970">The new set of APIs provides richer filtering and sorting functionality in addition to providing richer audit and sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="f8612-970">The new set of APIs provides richer filtering and sorting functionality in addition to providing richer audit and sign-in activities.</span></span> <span data-ttu-id="f8612-971">The data previously available through the security reports can now be accessed through the Identity Protection risk events API in Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f8612-971">The data previously available through the security reports can now be accessed through the Identity Protection risk events API in Microsoft Graph.</span></span>

<span data-ttu-id="f8612-972">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-972">For more information, see:</span></span>

- [<span data-ttu-id="f8612-973">Get started with the Azure Active Directory reporting API</span><span class="sxs-lookup"><span data-stu-id="f8612-973">Get started with the Azure Active Directory reporting API</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

- [<span data-ttu-id="f8612-974">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f8612-974">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-graph-getting-started)

---

## <a name="december-2017"></a><span data-ttu-id="f8612-975">December 2017</span><span class="sxs-lookup"><span data-stu-id="f8612-975">December 2017</span></span>

### <a name="terms-of-use-in-the-access-panel"></a><span data-ttu-id="f8612-976">Terms of use in the Access Panel</span><span class="sxs-lookup"><span data-stu-id="f8612-976">Terms of use in the Access Panel</span></span>

<span data-ttu-id="f8612-977">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-977">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-978">**Service category:** Terms of use</span><span class="sxs-lookup"><span data-stu-id="f8612-978">**Service category:** Terms of use</span></span>  
<span data-ttu-id="f8612-979">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-979">**Product capability:** Compliance</span></span>
 
<span data-ttu-id="f8612-980">You now can go to the Access Panel and view the terms of use that you previously accepted.</span><span class="sxs-lookup"><span data-stu-id="f8612-980">You now can go to the Access Panel and view the terms of use that you previously accepted.</span></span>

<span data-ttu-id="f8612-981">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f8612-981">Follow these steps:</span></span>

1. <span data-ttu-id="f8612-982">Go to the [MyApps portal](https://myapps.microsoft.com), and sign in.</span><span class="sxs-lookup"><span data-stu-id="f8612-982">Go to the [MyApps portal](https://myapps.microsoft.com), and sign in.</span></span>

2. <span data-ttu-id="f8612-983">In the upper-right corner, select your name, and then select **Profile** from the list.</span><span class="sxs-lookup"><span data-stu-id="f8612-983">In the upper-right corner, select your name, and then select **Profile** from the list.</span></span> 

3. <span data-ttu-id="f8612-984">On your **Profile**, select **Review terms of use**.</span><span class="sxs-lookup"><span data-stu-id="f8612-984">On your **Profile**, select **Review terms of use**.</span></span> 

4. <span data-ttu-id="f8612-985">Now you can review the terms of use you accepted.</span><span class="sxs-lookup"><span data-stu-id="f8612-985">Now you can review the terms of use you accepted.</span></span> 

<span data-ttu-id="f8612-986">For more information, see the [Azure AD terms of use feature (preview)](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-986">For more information, see the [Azure AD terms of use feature (preview)](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>
 
---
 
### <a name="new-azure-ad-sign-in-experience"></a><span data-ttu-id="f8612-987">New Azure AD sign-in experience</span><span class="sxs-lookup"><span data-stu-id="f8612-987">New Azure AD sign-in experience</span></span>

<span data-ttu-id="f8612-988">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-988">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-989">**Service category:** Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-989">**Service category:** Azure AD</span></span>  
<span data-ttu-id="f8612-990">**Product capability:** User authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-990">**Product capability:** User authentication</span></span>
 
<span data-ttu-id="f8612-991">The Azure AD and Microsoft account identity system UIs were redesigned so that they have a consistent look and feel.</span><span class="sxs-lookup"><span data-stu-id="f8612-991">The Azure AD and Microsoft account identity system UIs were redesigned so that they have a consistent look and feel.</span></span> <span data-ttu-id="f8612-992">In addition, the Azure AD sign-in page collects the user name first, followed by the credential on a second screen.</span><span class="sxs-lookup"><span data-stu-id="f8612-992">In addition, the Azure AD sign-in page collects the user name first, followed by the credential on a second screen.</span></span>

<span data-ttu-id="f8612-993">For more information, see [The new Azure AD sign-in experience is now in public preview](https://cloudblogs.microsoft.com/enterprisemobility/2017/08/02/the-new-azure-ad-signin-experience-is-now-in-public-preview/).</span><span class="sxs-lookup"><span data-stu-id="f8612-993">For more information, see [The new Azure AD sign-in experience is now in public preview](https://cloudblogs.microsoft.com/enterprisemobility/2017/08/02/the-new-azure-ad-signin-experience-is-now-in-public-preview/).</span></span>
 
---
 
### <a name="fewer-sign-in-prompts-a-new-keep-me-signed-in-experience-for-azure-ad-sign-in"></a><span data-ttu-id="f8612-994">Fewer sign-in prompts: A new "keep me signed in" experience for Azure AD sign-in</span><span class="sxs-lookup"><span data-stu-id="f8612-994">Fewer sign-in prompts: A new "keep me signed in" experience for Azure AD sign-in</span></span>

<span data-ttu-id="f8612-995">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-995">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-996">**Service category:** Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-996">**Service category:** Azure AD</span></span>  
<span data-ttu-id="f8612-997">**Product capability:** User authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-997">**Product capability:** User authentication</span></span>
 
<span data-ttu-id="f8612-998">The **Keep me signed in** check box on the Azure AD sign-in page was replaced with a new prompt that shows up after you successfully authenticate.</span><span class="sxs-lookup"><span data-stu-id="f8612-998">The **Keep me signed in** check box on the Azure AD sign-in page was replaced with a new prompt that shows up after you successfully authenticate.</span></span> 

<span data-ttu-id="f8612-999">If you respond **Yes** to this prompt, the service gives you a persistent refresh token.</span><span class="sxs-lookup"><span data-stu-id="f8612-999">If you respond **Yes** to this prompt, the service gives you a persistent refresh token.</span></span> <span data-ttu-id="f8612-1000">This behavior is the same as when you selected the **Keep me signed in** check box in the old experience.</span><span class="sxs-lookup"><span data-stu-id="f8612-1000">This behavior is the same as when you selected the **Keep me signed in** check box in the old experience.</span></span> <span data-ttu-id="f8612-1001">For federated tenants, this prompt shows after you successfully authenticate with the federated service.</span><span class="sxs-lookup"><span data-stu-id="f8612-1001">For federated tenants, this prompt shows after you successfully authenticate with the federated service.</span></span>

<span data-ttu-id="f8612-1002">For more information, see [Fewer sign-in prompts: The new "keep me signed in" experience for Azure AD is in preview](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/19/fewer-login-prompts-the-new-keep-me-signed-in-experience-for-azure-ad-is-in-preview/).</span><span class="sxs-lookup"><span data-stu-id="f8612-1002">For more information, see [Fewer sign-in prompts: The new "keep me signed in" experience for Azure AD is in preview](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/19/fewer-login-prompts-the-new-keep-me-signed-in-experience-for-azure-ad-is-in-preview/).</span></span> 

---

### <a name="add-configuration-to-require-the-terms-of-use-to-be-expanded-prior-to-accepting"></a><span data-ttu-id="f8612-1003">Add configuration to require the terms of use to be expanded prior to accepting</span><span class="sxs-lookup"><span data-stu-id="f8612-1003">Add configuration to require the terms of use to be expanded prior to accepting</span></span>

<span data-ttu-id="f8612-1004">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1004">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1005">**Service category:** Terms of use</span><span class="sxs-lookup"><span data-stu-id="f8612-1005">**Service category:** Terms of use</span></span>  
<span data-ttu-id="f8612-1006">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-1006">**Product capability:** Compliance</span></span>
 
<span data-ttu-id="f8612-1007">An option for administrators requires their users to expand the terms of use prior to accepting the terms.</span><span class="sxs-lookup"><span data-stu-id="f8612-1007">An option for administrators requires their users to expand the terms of use prior to accepting the terms.</span></span>

<span data-ttu-id="f8612-1008">Select either **On** or **Off** to require users to expand the terms of use.</span><span class="sxs-lookup"><span data-stu-id="f8612-1008">Select either **On** or **Off** to require users to expand the terms of use.</span></span> <span data-ttu-id="f8612-1009">The **On** setting requires users to view the terms of use prior to accepting them.</span><span class="sxs-lookup"><span data-stu-id="f8612-1009">The **On** setting requires users to view the terms of use prior to accepting them.</span></span>

<span data-ttu-id="f8612-1010">For more information, see the [Azure AD terms of use feature (preview)](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-1010">For more information, see the [Azure AD terms of use feature (preview)](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>
 
---

### <a name="scoped-activation-for-eligible-role-assignments"></a><span data-ttu-id="f8612-1011">Scoped activation for eligible role assignments</span><span class="sxs-lookup"><span data-stu-id="f8612-1011">Scoped activation for eligible role assignments</span></span>

<span data-ttu-id="f8612-1012">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1012">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1013">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1013">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-1014">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1014">**Product capability:** Privileged Identity Management</span></span>
 
<span data-ttu-id="f8612-1015">You can use scoped activation to activate eligible Azure resource role assignments with less autonomy than the original assignment defaults.</span><span class="sxs-lookup"><span data-stu-id="f8612-1015">You can use scoped activation to activate eligible Azure resource role assignments with less autonomy than the original assignment defaults.</span></span> <span data-ttu-id="f8612-1016">An example is if you're assigned as the owner of a subscription in your tenant.</span><span class="sxs-lookup"><span data-stu-id="f8612-1016">An example is if you're assigned as the owner of a subscription in your tenant.</span></span> <span data-ttu-id="f8612-1017">With scoped activation, you can activate the owner role for up to five resources contained within the subscription (such as resource groups and virtual machines).</span><span class="sxs-lookup"><span data-stu-id="f8612-1017">With scoped activation, you can activate the owner role for up to five resources contained within the subscription (such as resource groups and virtual machines).</span></span> <span data-ttu-id="f8612-1018">Scoping your activation might reduce the possibility of executing unwanted changes to critical Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f8612-1018">Scoping your activation might reduce the possibility of executing unwanted changes to critical Azure resources.</span></span>

<span data-ttu-id="f8612-1019">For more information, see [What is Azure AD Privileged Identity Management?](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure).</span><span class="sxs-lookup"><span data-stu-id="f8612-1019">For more information, see [What is Azure AD Privileged Identity Management?](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure).</span></span>
 
---
 
### <a name="new-federated-apps-in-the-azure-ad-app-gallery"></a><span data-ttu-id="f8612-1020">New federated apps in the Azure AD app gallery</span><span class="sxs-lookup"><span data-stu-id="f8612-1020">New federated apps in the Azure AD app gallery</span></span>

<span data-ttu-id="f8612-1021">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1021">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1022">**Service category:** Enterprise apps</span><span class="sxs-lookup"><span data-stu-id="f8612-1022">**Service category:** Enterprise apps</span></span>  
<span data-ttu-id="f8612-1023">**Product capability:** 3rd Party Integration</span><span class="sxs-lookup"><span data-stu-id="f8612-1023">**Product capability:** 3rd Party Integration</span></span>

<span data-ttu-id="f8612-1024">In December 2017, we've added these new apps with Federation support to our app gallery:</span><span class="sxs-lookup"><span data-stu-id="f8612-1024">In December 2017, we've added these new apps with Federation support to our app gallery:</span></span>

<span data-ttu-id="f8612-1025">[Accredible](https://go.microsoft.com/fwlink/?linkid=863523), Adobe Experience Manager, [EFI Digital StoreFront](https://go.microsoft.com/fwlink/?linkid=861685), [Communifire](https://go.microsoft.com/fwlink/?linkid=861676) CybSafe, [FactSet](https://go.microsoft.com/fwlink/?linkid=863525), [IMAGE WORKS](https://go.microsoft.com/fwlink/?linkid=863517), [MOBI](https://go.microsoft.com/fwlink/?linkid=863521), [MobileIron Azure AD integration](https://go.microsoft.com/fwlink/?linkid=858027), [Reflektive](https://go.microsoft.com/fwlink/?linkid=863518), [SAML SSO for Bamboo by resolution GmbH](https://go.microsoft.com/fwlink/?linkid=863520), [SAML SSO for Bitbucket by resolution GmbH](https://go.microsoft.com/fwlink/?linkid=863519), [Vodeclic](https://go.microsoft.com/fwlink/?linkid=863522), WebHR, Zenegy Azure AD Integration.</span><span class="sxs-lookup"><span data-stu-id="f8612-1025">[Accredible](https://go.microsoft.com/fwlink/?linkid=863523), Adobe Experience Manager, [EFI Digital StoreFront](https://go.microsoft.com/fwlink/?linkid=861685), [Communifire](https://go.microsoft.com/fwlink/?linkid=861676) CybSafe, [FactSet](https://go.microsoft.com/fwlink/?linkid=863525), [IMAGE WORKS](https://go.microsoft.com/fwlink/?linkid=863517), [MOBI](https://go.microsoft.com/fwlink/?linkid=863521), [MobileIron Azure AD integration](https://go.microsoft.com/fwlink/?linkid=858027), [Reflektive](https://go.microsoft.com/fwlink/?linkid=863518), [SAML SSO for Bamboo by resolution GmbH](https://go.microsoft.com/fwlink/?linkid=863520), [SAML SSO for Bitbucket by resolution GmbH](https://go.microsoft.com/fwlink/?linkid=863519), [Vodeclic](https://go.microsoft.com/fwlink/?linkid=863522), WebHR, Zenegy Azure AD Integration.</span></span>

<span data-ttu-id="f8612-1026">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span><span class="sxs-lookup"><span data-stu-id="f8612-1026">For more information about the apps, see [SaaS application integration with Azure Active Directory](https://aka.ms/appstutorial).</span></span>

<span data-ttu-id="f8612-1027">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span><span class="sxs-lookup"><span data-stu-id="f8612-1027">For more information about listing your application in the Azure AD app gallery, see [List your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing).</span></span> 
 
---

### <a name="approval-workflows-for-azure-ad-directory-roles"></a><span data-ttu-id="f8612-1028">Approval workflows for Azure AD directory roles</span><span class="sxs-lookup"><span data-stu-id="f8612-1028">Approval workflows for Azure AD directory roles</span></span>

<span data-ttu-id="f8612-1029">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1029">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-1030">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1030">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-1031">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1031">**Product capability:** Privileged Identity Management</span></span>
 
<span data-ttu-id="f8612-1032">Approval workflow for Azure AD directory roles is generally available.</span><span class="sxs-lookup"><span data-stu-id="f8612-1032">Approval workflow for Azure AD directory roles is generally available.</span></span>

<span data-ttu-id="f8612-1033">With approval workflow, privileged-role administrators can require eligible-role members to request role activation before they can use the privileged role.</span><span class="sxs-lookup"><span data-stu-id="f8612-1033">With approval workflow, privileged-role administrators can require eligible-role members to request role activation before they can use the privileged role.</span></span> <span data-ttu-id="f8612-1034">Multiple users and groups can be delegated approval responsibilities.</span><span class="sxs-lookup"><span data-stu-id="f8612-1034">Multiple users and groups can be delegated approval responsibilities.</span></span> <span data-ttu-id="f8612-1035">Eligible role members receive notifications when approval is finished and their role is active.</span><span class="sxs-lookup"><span data-stu-id="f8612-1035">Eligible role members receive notifications when approval is finished and their role is active.</span></span>

---
 
### <a name="pass-through-authentication-skype-for-business-support"></a><span data-ttu-id="f8612-1036">Pass-through authentication: Skype for Business support</span><span class="sxs-lookup"><span data-stu-id="f8612-1036">Pass-through authentication: Skype for Business support</span></span>

<span data-ttu-id="f8612-1037">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1037">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-1038">**Service category:** Authentications (Logins)</span><span class="sxs-lookup"><span data-stu-id="f8612-1038">**Service category:** Authentications (Logins)</span></span>  
<span data-ttu-id="f8612-1039">**Product capability:** User authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-1039">**Product capability:** User authentication</span></span>

<span data-ttu-id="f8612-1040">Pass-through authentication now supports user sign-ins to Skype for Business client applications that support modern authentication, which includes online and hybrid topologies.</span><span class="sxs-lookup"><span data-stu-id="f8612-1040">Pass-through authentication now supports user sign-ins to Skype for Business client applications that support modern authentication, which includes online and hybrid topologies.</span></span> 

<span data-ttu-id="f8612-1041">For more information, see [Skype for Business topologies supported with modern authentication](https://technet.microsoft.com/library/mt803262.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8612-1041">For more information, see [Skype for Business topologies supported with modern authentication](https://technet.microsoft.com/library/mt803262.aspx).</span></span>
 
---

### <a name="updates-to-azure-ad-privileged-identity-management-for-azure-rbac-preview"></a><span data-ttu-id="f8612-1042">Updates to Azure AD Privileged Identity Management for Azure RBAC (preview)</span><span class="sxs-lookup"><span data-stu-id="f8612-1042">Updates to Azure AD Privileged Identity Management for Azure RBAC (preview)</span></span>

<span data-ttu-id="f8612-1043">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1043">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-1044">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1044">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-1045">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1045">**Product capability:** Privileged Identity Management</span></span>
 
<span data-ttu-id="f8612-1046">With the public preview refresh of Azure AD Privileged Identity Management (PIM) for Azure Role-Based Access Control (RBAC), you can now:</span><span class="sxs-lookup"><span data-stu-id="f8612-1046">With the public preview refresh of Azure AD Privileged Identity Management (PIM) for Azure Role-Based Access Control (RBAC), you can now:</span></span>

* <span data-ttu-id="f8612-1047">Use Just Enough Administration.</span><span class="sxs-lookup"><span data-stu-id="f8612-1047">Use Just Enough Administration.</span></span>
* <span data-ttu-id="f8612-1048">Require approval to activate resource roles.</span><span class="sxs-lookup"><span data-stu-id="f8612-1048">Require approval to activate resource roles.</span></span>
* <span data-ttu-id="f8612-1049">Schedule a future activation of a role that requires approval for both Azure AD and Azure RBAC roles.</span><span class="sxs-lookup"><span data-stu-id="f8612-1049">Schedule a future activation of a role that requires approval for both Azure AD and Azure RBAC roles.</span></span>
 
<span data-ttu-id="f8612-1050">For more information, see [Privileged Identity Management for Azure resources (preview)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac).</span><span class="sxs-lookup"><span data-stu-id="f8612-1050">For more information, see [Privileged Identity Management for Azure resources (preview)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac).</span></span>

---
 
## <a name="november-2017"></a><span data-ttu-id="f8612-1051">November 2017</span><span class="sxs-lookup"><span data-stu-id="f8612-1051">November 2017</span></span>
 
### <a name="access-control-service-retirement"></a><span data-ttu-id="f8612-1052">Access Control service retirement</span><span class="sxs-lookup"><span data-stu-id="f8612-1052">Access Control service retirement</span></span>

<span data-ttu-id="f8612-1053">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-1053">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-1054">**Service category:** Access Control service</span><span class="sxs-lookup"><span data-stu-id="f8612-1054">**Service category:** Access Control service</span></span>  
<span data-ttu-id="f8612-1055">**Product capability:** Access Control service</span><span class="sxs-lookup"><span data-stu-id="f8612-1055">**Product capability:** Access Control service</span></span> 

<span data-ttu-id="f8612-1056">Azure Active Directory Access Control (also known as the Access Control service) will be retired in late 2018.</span><span class="sxs-lookup"><span data-stu-id="f8612-1056">Azure Active Directory Access Control (also known as the Access Control service) will be retired in late 2018.</span></span> <span data-ttu-id="f8612-1057">More information that includes a detailed schedule and high-level migration guidance will be provided in the next few weeks.</span><span class="sxs-lookup"><span data-stu-id="f8612-1057">More information that includes a detailed schedule and high-level migration guidance will be provided in the next few weeks.</span></span> <span data-ttu-id="f8612-1058">You can leave comments on this page with any questions about the Access Control service, and a team member will answer them.</span><span class="sxs-lookup"><span data-stu-id="f8612-1058">You can leave comments on this page with any questions about the Access Control service, and a team member will answer them.</span></span>

---

### <a name="restrict-browser-access-to-the-intune-managed-browser"></a><span data-ttu-id="f8612-1059">Restrict browser access to the Intune Managed Browser</span><span class="sxs-lookup"><span data-stu-id="f8612-1059">Restrict browser access to the Intune Managed Browser</span></span> 

<span data-ttu-id="f8612-1060">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-1060">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-1061">**Service category:** Conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1061">**Service category:** Conditional access</span></span>  
<span data-ttu-id="f8612-1062">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1062">**Product capability:** Identity security and protection</span></span>

<span data-ttu-id="f8612-1063">You can restrict browser access to Office 365 and other Azure AD-connected cloud apps by using the Intune Managed Browser as an approved app.</span><span class="sxs-lookup"><span data-stu-id="f8612-1063">You can restrict browser access to Office 365 and other Azure AD-connected cloud apps by using the Intune Managed Browser as an approved app.</span></span> 

<span data-ttu-id="f8612-1064">You now can configure the following condition for application-based conditional access:</span><span class="sxs-lookup"><span data-stu-id="f8612-1064">You now can configure the following condition for application-based conditional access:</span></span>

<span data-ttu-id="f8612-1065">**Client apps:** Browser</span><span class="sxs-lookup"><span data-stu-id="f8612-1065">**Client apps:** Browser</span></span>

<span data-ttu-id="f8612-1066">**What is the effect of the change?**</span><span class="sxs-lookup"><span data-stu-id="f8612-1066">**What is the effect of the change?**</span></span>

<span data-ttu-id="f8612-1067">Today, access is blocked when you use this condition.</span><span class="sxs-lookup"><span data-stu-id="f8612-1067">Today, access is blocked when you use this condition.</span></span> <span data-ttu-id="f8612-1068">When the preview is available, all access will require the use of the managed browser application.</span><span class="sxs-lookup"><span data-stu-id="f8612-1068">When the preview is available, all access will require the use of the managed browser application.</span></span> 

<span data-ttu-id="f8612-1069">Look for this capability and more information in upcoming blogs and release notes.</span><span class="sxs-lookup"><span data-stu-id="f8612-1069">Look for this capability and more information in upcoming blogs and release notes.</span></span> 

<span data-ttu-id="f8612-1070">For more information, see [Conditional access in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f8612-1070">For more information, see [Conditional access in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).</span></span>
 
---

### <a name="new-approved-client-apps-for-azure-ad-app-based-conditional-access"></a><span data-ttu-id="f8612-1071">New approved client apps for Azure AD app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1071">New approved client apps for Azure AD app-based conditional access</span></span>

<span data-ttu-id="f8612-1072">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-1072">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-1073">**Service category:** Conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1073">**Service category:** Conditional access</span></span>  
<span data-ttu-id="f8612-1074">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1074">**Product capability:** Identity security and protection</span></span>

<span data-ttu-id="f8612-1075">The following apps are on the list of [approved client apps](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement):</span><span class="sxs-lookup"><span data-stu-id="f8612-1075">The following apps are on the list of [approved client apps](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement):</span></span>

- [<span data-ttu-id="f8612-1076">Microsoft Kaizala</span><span class="sxs-lookup"><span data-stu-id="f8612-1076">Microsoft Kaizala</span></span>](https://www.microsoft.com/garage/profiles/kaizala/)
- [<span data-ttu-id="f8612-1077">Microsoft StaffHub</span><span class="sxs-lookup"><span data-stu-id="f8612-1077">Microsoft StaffHub</span></span>](https://staffhub.office.com/what-it-is)

<span data-ttu-id="f8612-1078">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-1078">For more information, see:</span></span>

- [<span data-ttu-id="f8612-1079">Approved client app requirement</span><span class="sxs-lookup"><span data-stu-id="f8612-1079">Approved client app requirement</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement)
- [<span data-ttu-id="f8612-1080">Azure AD app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1080">Azure AD app-based conditional access</span></span>](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access)

---

### <a name="terms-of-use-support-for-multiple-languages"></a><span data-ttu-id="f8612-1081">Terms-of-use support for multiple languages</span><span class="sxs-lookup"><span data-stu-id="f8612-1081">Terms-of-use support for multiple languages</span></span>

<span data-ttu-id="f8612-1082">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1082">**Type:** New feature</span></span>    
<span data-ttu-id="f8612-1083">**Service category:** Terms of use</span><span class="sxs-lookup"><span data-stu-id="f8612-1083">**Service category:** Terms of use</span></span>  
<span data-ttu-id="f8612-1084">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-1084">**Product capability:** Compliance</span></span>

<span data-ttu-id="f8612-1085">Administrators now can create new terms of use that contain multiple PDF documents.</span><span class="sxs-lookup"><span data-stu-id="f8612-1085">Administrators now can create new terms of use that contain multiple PDF documents.</span></span> <span data-ttu-id="f8612-1086">You can tag these PDF documents with a corresponding language.</span><span class="sxs-lookup"><span data-stu-id="f8612-1086">You can tag these PDF documents with a corresponding language.</span></span> <span data-ttu-id="f8612-1087">Users are shown the PDF with the matching language based on their preferences.</span><span class="sxs-lookup"><span data-stu-id="f8612-1087">Users are shown the PDF with the matching language based on their preferences.</span></span> <span data-ttu-id="f8612-1088">If there is no match, the default language is shown.</span><span class="sxs-lookup"><span data-stu-id="f8612-1088">If there is no match, the default language is shown.</span></span>

---
 

### <a name="real-time-password-writeback-client-status"></a><span data-ttu-id="f8612-1089">Real-time password writeback client status</span><span class="sxs-lookup"><span data-stu-id="f8612-1089">Real-time password writeback client status</span></span>

<span data-ttu-id="f8612-1090">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1090">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1091">**Service category:** Self-service password reset</span><span class="sxs-lookup"><span data-stu-id="f8612-1091">**Service category:** Self-service password reset</span></span>  
<span data-ttu-id="f8612-1092">**Product capability:** User authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-1092">**Product capability:** User authentication</span></span>

<span data-ttu-id="f8612-1093">You now can review the status of your on-premises password writeback client.</span><span class="sxs-lookup"><span data-stu-id="f8612-1093">You now can review the status of your on-premises password writeback client.</span></span> <span data-ttu-id="f8612-1094">This option is available in the **On-premises integration** section of the [Password reset](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) page.</span><span class="sxs-lookup"><span data-stu-id="f8612-1094">This option is available in the **On-premises integration** section of the [Password reset](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) page.</span></span> 

<span data-ttu-id="f8612-1095">If there are issues with your connection to your on-premises writeback client, you see an error message that provides you with:</span><span class="sxs-lookup"><span data-stu-id="f8612-1095">If there are issues with your connection to your on-premises writeback client, you see an error message that provides you with:</span></span>

- <span data-ttu-id="f8612-1096">Information on why you can't connect to your on-premises writeback client.</span><span class="sxs-lookup"><span data-stu-id="f8612-1096">Information on why you can't connect to your on-premises writeback client.</span></span>
- <span data-ttu-id="f8612-1097">A link to documentation that assists you in resolving the issue.</span><span class="sxs-lookup"><span data-stu-id="f8612-1097">A link to documentation that assists you in resolving the issue.</span></span> 

<span data-ttu-id="f8612-1098">For more information, see [on-premises integration](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-how-it-works#on-premises-integration).</span><span class="sxs-lookup"><span data-stu-id="f8612-1098">For more information, see [on-premises integration](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-how-it-works#on-premises-integration).</span></span>

---

### <a name="azure-ad-app-based-conditional-access"></a><span data-ttu-id="f8612-1099">Azure AD app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1099">Azure AD app-based conditional access</span></span> 
 
<span data-ttu-id="f8612-1100">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1100">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1101">**Service category:** Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-1101">**Service category:** Azure AD</span></span>  
<span data-ttu-id="f8612-1102">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1102">**Product capability:** Identity security and protection</span></span>

<span data-ttu-id="f8612-1103">You now can restrict access to Office 365 and other Azure AD-connected cloud apps to [approved client apps](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement) that support Intune app protection policies by using [Azure AD app-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).</span><span class="sxs-lookup"><span data-stu-id="f8612-1103">You now can restrict access to Office 365 and other Azure AD-connected cloud apps to [approved client apps](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement) that support Intune app protection policies by using [Azure AD app-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).</span></span> <span data-ttu-id="f8612-1104">Intune app protection policies are used to configure and protect company data on these client applications.</span><span class="sxs-lookup"><span data-stu-id="f8612-1104">Intune app protection policies are used to configure and protect company data on these client applications.</span></span>

<span data-ttu-id="f8612-1105">By combining [app-based](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access) with [device-based](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-policy-connected-applications) conditional access policies, you have the flexibility to protect data for personal and company devices.</span><span class="sxs-lookup"><span data-stu-id="f8612-1105">By combining [app-based](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access) with [device-based](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-policy-connected-applications) conditional access policies, you have the flexibility to protect data for personal and company devices.</span></span>

<span data-ttu-id="f8612-1106">The following conditions and controls are now available for use with app-based conditional access:</span><span class="sxs-lookup"><span data-stu-id="f8612-1106">The following conditions and controls are now available for use with app-based conditional access:</span></span>

<span data-ttu-id="f8612-1107">**Supported platform condition**</span><span class="sxs-lookup"><span data-stu-id="f8612-1107">**Supported platform condition**</span></span>

- <span data-ttu-id="f8612-1108">iOS</span><span class="sxs-lookup"><span data-stu-id="f8612-1108">iOS</span></span>
- <span data-ttu-id="f8612-1109">Android</span><span class="sxs-lookup"><span data-stu-id="f8612-1109">Android</span></span>

<span data-ttu-id="f8612-1110">**Client apps condition**</span><span class="sxs-lookup"><span data-stu-id="f8612-1110">**Client apps condition**</span></span>

- <span data-ttu-id="f8612-1111">Mobile apps and desktop clients</span><span class="sxs-lookup"><span data-stu-id="f8612-1111">Mobile apps and desktop clients</span></span>

<span data-ttu-id="f8612-1112">**Access control**</span><span class="sxs-lookup"><span data-stu-id="f8612-1112">**Access control**</span></span>

- <span data-ttu-id="f8612-1113">Require approved client app</span><span class="sxs-lookup"><span data-stu-id="f8612-1113">Require approved client app</span></span>

<span data-ttu-id="f8612-1114">For more information, see [Azure AD app-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).</span><span class="sxs-lookup"><span data-stu-id="f8612-1114">For more information, see [Azure AD app-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).</span></span>
 
---

### <a name="manage-azure-ad-devices-in-the-azure-portal"></a><span data-ttu-id="f8612-1115">Manage Azure AD devices in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f8612-1115">Manage Azure AD devices in the Azure Portal</span></span>

<span data-ttu-id="f8612-1116">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1116">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1117">**Service category:** Device registration and management</span><span class="sxs-lookup"><span data-stu-id="f8612-1117">**Service category:** Device registration and management</span></span>  
<span data-ttu-id="f8612-1118">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1118">**Product capability:** Identity security and protection</span></span>

<span data-ttu-id="f8612-1119">You now can find all your devices connected to Azure AD and the device-related activities in one place.</span><span class="sxs-lookup"><span data-stu-id="f8612-1119">You now can find all your devices connected to Azure AD and the device-related activities in one place.</span></span> <span data-ttu-id="f8612-1120">There is a new administration experience to manage all your device identities and settings in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f8612-1120">There is a new administration experience to manage all your device identities and settings in the Azure portal.</span></span> <span data-ttu-id="f8612-1121">In this release, you can:</span><span class="sxs-lookup"><span data-stu-id="f8612-1121">In this release, you can:</span></span>

- <span data-ttu-id="f8612-1122">View all your devices that are available for conditional access in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-1122">View all your devices that are available for conditional access in Azure AD.</span></span>
- <span data-ttu-id="f8612-1123">View properties, which include your hybrid Azure AD-joined devices.</span><span class="sxs-lookup"><span data-stu-id="f8612-1123">View properties, which include your hybrid Azure AD-joined devices.</span></span>
- <span data-ttu-id="f8612-1124">Find BitLocker keys for your Azure AD-joined devices, manage your device with Intune, and more.</span><span class="sxs-lookup"><span data-stu-id="f8612-1124">Find BitLocker keys for your Azure AD-joined devices, manage your device with Intune, and more.</span></span>
- <span data-ttu-id="f8612-1125">Manage Azure AD device-related settings.</span><span class="sxs-lookup"><span data-stu-id="f8612-1125">Manage Azure AD device-related settings.</span></span>

<span data-ttu-id="f8612-1126">For more information, see [Manage devices by using the Azure portal](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f8612-1126">For more information, see [Manage devices by using the Azure portal](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal).</span></span>

---

### <a name="support-for-macos-as-a-device-platform-for-azure-ad-conditional-access"></a><span data-ttu-id="f8612-1127">Support for macOS as a device platform for Azure AD conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1127">Support for macOS as a device platform for Azure AD conditional access</span></span> 

<span data-ttu-id="f8612-1128">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1128">**Type:** New feature</span></span>    
<span data-ttu-id="f8612-1129">**Service category:** Conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1129">**Service category:** Conditional access</span></span>  
<span data-ttu-id="f8612-1130">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1130">**Product capability:** Identity security and protection</span></span> 

<span data-ttu-id="f8612-1131">You now can include (or exclude) macOS as a device platform condition in your Azure AD conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="f8612-1131">You now can include (or exclude) macOS as a device platform condition in your Azure AD conditional access policy.</span></span> <span data-ttu-id="f8612-1132">With the addition of macOS to the supported device platforms, you can:</span><span class="sxs-lookup"><span data-stu-id="f8612-1132">With the addition of macOS to the supported device platforms, you can:</span></span>

- <span data-ttu-id="f8612-1133">**Enroll and manage macOS devices by using Intune.**</span><span class="sxs-lookup"><span data-stu-id="f8612-1133">**Enroll and manage macOS devices by using Intune.**</span></span> <span data-ttu-id="f8612-1134">Similar to other platforms like iOS and Android, a company portal application is available for macOS to do unified enrollments.</span><span class="sxs-lookup"><span data-stu-id="f8612-1134">Similar to other platforms like iOS and Android, a company portal application is available for macOS to do unified enrollments.</span></span> <span data-ttu-id="f8612-1135">You can use the new company portal app for macOS to enroll a device with Intune and register it with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8612-1135">You can use the new company portal app for macOS to enroll a device with Intune and register it with Azure AD.</span></span>
- <span data-ttu-id="f8612-1136">**Ensure macOS devices adhere to your organization's compliance policies defined in Intune.**</span><span class="sxs-lookup"><span data-stu-id="f8612-1136">**Ensure macOS devices adhere to your organization's compliance policies defined in Intune.**</span></span> <span data-ttu-id="f8612-1137">In Intune on the Azure portal, you now can set up compliance policies for macOS devices.</span><span class="sxs-lookup"><span data-stu-id="f8612-1137">In Intune on the Azure portal, you now can set up compliance policies for macOS devices.</span></span> 
- <span data-ttu-id="f8612-1138">**Restrict access to applications in Azure AD to only compliant macOS devices.**</span><span class="sxs-lookup"><span data-stu-id="f8612-1138">**Restrict access to applications in Azure AD to only compliant macOS devices.**</span></span> <span data-ttu-id="f8612-1139">Conditional access policy authoring has macOS as a separate device platform option.</span><span class="sxs-lookup"><span data-stu-id="f8612-1139">Conditional access policy authoring has macOS as a separate device platform option.</span></span> <span data-ttu-id="f8612-1140">Now you can author macOS-specific conditional access policies for the targeted application set in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8612-1140">Now you can author macOS-specific conditional access policies for the targeted application set in Azure.</span></span>

<span data-ttu-id="f8612-1141">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-1141">For more information, see:</span></span>

- [<span data-ttu-id="f8612-1142">Create a device compliance policy for macOS devices with Intune</span><span class="sxs-lookup"><span data-stu-id="f8612-1142">Create a device compliance policy for macOS devices with Intune</span></span>](https://aka.ms/macoscompliancepolicy)
- [<span data-ttu-id="f8612-1143">Conditional access in Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8612-1143">Conditional access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
 
---

### <a name="network-policy-server-extension-for-azure-multi-factor-authentication"></a><span data-ttu-id="f8612-1144">Network Policy Server extension for Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-1144">Network Policy Server extension for Azure Multi-Factor Authentication</span></span> 

<span data-ttu-id="f8612-1145">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1145">**Type:** New feature</span></span>    
<span data-ttu-id="f8612-1146">**Service category:**  Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-1146">**Service category:**  Multi-factor authentication</span></span>  
<span data-ttu-id="f8612-1147">**Product capability:** User authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-1147">**Product capability:** User authentication</span></span>

<span data-ttu-id="f8612-1148">The Network Policy Server extension for Azure Multi-Factor Authentication adds cloud-based Multi-Factor Authentication capabilities to your authentication infrastructure by using your existing servers.</span><span class="sxs-lookup"><span data-stu-id="f8612-1148">The Network Policy Server extension for Azure Multi-Factor Authentication adds cloud-based Multi-Factor Authentication capabilities to your authentication infrastructure by using your existing servers.</span></span> <span data-ttu-id="f8612-1149">With the Network Policy Server extension, you can add phone call, text message, or phone app verification to your existing authentication flow.</span><span class="sxs-lookup"><span data-stu-id="f8612-1149">With the Network Policy Server extension, you can add phone call, text message, or phone app verification to your existing authentication flow.</span></span> <span data-ttu-id="f8612-1150">You don't have to install, configure, and maintain new servers.</span><span class="sxs-lookup"><span data-stu-id="f8612-1150">You don't have to install, configure, and maintain new servers.</span></span> 

<span data-ttu-id="f8612-1151">This extension was created for organizations that want to protect virtual private network connections without deploying the Azure Multi-Factor Authentication Server.</span><span class="sxs-lookup"><span data-stu-id="f8612-1151">This extension was created for organizations that want to protect virtual private network connections without deploying the Azure Multi-Factor Authentication Server.</span></span> <span data-ttu-id="f8612-1152">The Network Policy Server extension acts as an adapter between RADIUS and cloud-based Azure Multi-Factor Authentication to provide a second factor of authentication for federated or synced users.</span><span class="sxs-lookup"><span data-stu-id="f8612-1152">The Network Policy Server extension acts as an adapter between RADIUS and cloud-based Azure Multi-Factor Authentication to provide a second factor of authentication for federated or synced users.</span></span>


<span data-ttu-id="f8612-1153">For more information, see [Integrate your existing Network Policy Server infrastructure with Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-nps-extension).</span><span class="sxs-lookup"><span data-stu-id="f8612-1153">For more information, see [Integrate your existing Network Policy Server infrastructure with Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-nps-extension).</span></span>

 
---

### <a name="restore-or-permanently-remove-deleted-users"></a><span data-ttu-id="f8612-1154">Restore or permanently remove deleted users</span><span class="sxs-lookup"><span data-stu-id="f8612-1154">Restore or permanently remove deleted users</span></span>

<span data-ttu-id="f8612-1155">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1155">**Type:** New feature</span></span>    
<span data-ttu-id="f8612-1156">**Service category:** User management</span><span class="sxs-lookup"><span data-stu-id="f8612-1156">**Service category:** User management</span></span>  
<span data-ttu-id="f8612-1157">**Product capability:** Directory</span><span class="sxs-lookup"><span data-stu-id="f8612-1157">**Product capability:** Directory</span></span> 


<span data-ttu-id="f8612-1158">In the Azure AD admin center, you can now:</span><span class="sxs-lookup"><span data-stu-id="f8612-1158">In the Azure AD admin center, you can now:</span></span>

- <span data-ttu-id="f8612-1159">Restore a deleted user.</span><span class="sxs-lookup"><span data-stu-id="f8612-1159">Restore a deleted user.</span></span> 
- <span data-ttu-id="f8612-1160">Permanently delete a user.</span><span class="sxs-lookup"><span data-stu-id="f8612-1160">Permanently delete a user.</span></span>


<span data-ttu-id="f8612-1161">**To try it out:**</span><span class="sxs-lookup"><span data-stu-id="f8612-1161">**To try it out:**</span></span>

1. <span data-ttu-id="f8612-1162">In the Azure AD admin center, select [All users](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All) in the **Manage** section.</span><span class="sxs-lookup"><span data-stu-id="f8612-1162">In the Azure AD admin center, select [All users](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All) in the **Manage** section.</span></span> 

2. <span data-ttu-id="f8612-1163">From the **Show** list, select **Recently deleted users**.</span><span class="sxs-lookup"><span data-stu-id="f8612-1163">From the **Show** list, select **Recently deleted users**.</span></span> 

3. <span data-ttu-id="f8612-1164">Select one or more recently deleted users, and then either restore them or permanently delete them.</span><span class="sxs-lookup"><span data-stu-id="f8612-1164">Select one or more recently deleted users, and then either restore them or permanently delete them.</span></span>

 
---

### <a name="new-approved-client-apps-for-azure-ad-app-based-conditional-access"></a><span data-ttu-id="f8612-1165">New approved client apps for Azure AD app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1165">New approved client apps for Azure AD app-based conditional access</span></span>

 
<span data-ttu-id="f8612-1166">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1166">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-1167">**Service category:** Conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1167">**Service category:** Conditional access</span></span>  
<span data-ttu-id="f8612-1168">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1168">**Product capability:** Identity security and protection</span></span>


<span data-ttu-id="f8612-1169">The following apps were added to the list of [approved client apps](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement):</span><span class="sxs-lookup"><span data-stu-id="f8612-1169">The following apps were added to the list of [approved client apps](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement):</span></span>

- <span data-ttu-id="f8612-1170">Microsoft Planner</span><span class="sxs-lookup"><span data-stu-id="f8612-1170">Microsoft Planner</span></span>
- <span data-ttu-id="f8612-1171">Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1171">Azure Information Protection</span></span> 


<span data-ttu-id="f8612-1172">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="f8612-1172">For more information, see:</span></span>

- [<span data-ttu-id="f8612-1173">Approved client app requirement</span><span class="sxs-lookup"><span data-stu-id="f8612-1173">Approved client app requirement</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#approved-client-app-requirement)
- [<span data-ttu-id="f8612-1174">Azure AD app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1174">Azure AD app-based conditional access</span></span>](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access)


---

### <a name="use-or-between-controls-in-a-conditional-access-policy"></a><span data-ttu-id="f8612-1175">Use "OR" between controls in a conditional access policy</span><span class="sxs-lookup"><span data-stu-id="f8612-1175">Use "OR" between controls in a conditional access policy</span></span> 


<span data-ttu-id="f8612-1176">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1176">**Type:** Changed feature</span></span>    
<span data-ttu-id="f8612-1177">**Service category:** Conditional access</span><span class="sxs-lookup"><span data-stu-id="f8612-1177">**Service category:** Conditional access</span></span>  
<span data-ttu-id="f8612-1178">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1178">**Product capability:** Identity security and protection</span></span>

 
<span data-ttu-id="f8612-1179">You now can use "OR" (require one of the selected controls) for conditional access controls.</span><span class="sxs-lookup"><span data-stu-id="f8612-1179">You now can use "OR" (require one of the selected controls) for conditional access controls.</span></span> <span data-ttu-id="f8612-1180">You can use this feature to create policies with "OR" between access controls.</span><span class="sxs-lookup"><span data-stu-id="f8612-1180">You can use this feature to create policies with "OR" between access controls.</span></span> <span data-ttu-id="f8612-1181">For example, you can use this feature to create a policy that requires a user to sign in by using Multi-Factor Authentication "OR" to be on a compliant device.</span><span class="sxs-lookup"><span data-stu-id="f8612-1181">For example, you can use this feature to create a policy that requires a user to sign in by using Multi-Factor Authentication "OR" to be on a compliant device.</span></span>

<span data-ttu-id="f8612-1182">For more information, see [Controls in Azure AD conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls).</span><span class="sxs-lookup"><span data-stu-id="f8612-1182">For more information, see [Controls in Azure AD conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls).</span></span>

 
---

### <a name="aggregation-of-real-time-risk-events"></a><span data-ttu-id="f8612-1183">Aggregation of real-time risk events</span><span class="sxs-lookup"><span data-stu-id="f8612-1183">Aggregation of real-time risk events</span></span>


<span data-ttu-id="f8612-1184">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1184">**Type:** Changed feature</span></span>    
<span data-ttu-id="f8612-1185">**Service category:** Identity protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1185">**Service category:** Identity protection</span></span>  
<span data-ttu-id="f8612-1186">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1186">**Product capability:** Identity security and protection</span></span>


<span data-ttu-id="f8612-1187">In Azure AD Identity Protection, all real-time risk events that originated from the same IP address on a given day are now aggregated for each risk event type.</span><span class="sxs-lookup"><span data-stu-id="f8612-1187">In Azure AD Identity Protection, all real-time risk events that originated from the same IP address on a given day are now aggregated for each risk event type.</span></span> <span data-ttu-id="f8612-1188">This change limits the volume of risk events shown without any change in user security.</span><span class="sxs-lookup"><span data-stu-id="f8612-1188">This change limits the volume of risk events shown without any change in user security.</span></span>

<span data-ttu-id="f8612-1189">The underlying real-time detection works each time the user signs in.</span><span class="sxs-lookup"><span data-stu-id="f8612-1189">The underlying real-time detection works each time the user signs in.</span></span> <span data-ttu-id="f8612-1190">If you have a sign-in risk security policy set up to Multi-Factor Authentication or block access, it is still triggered during each risky sign-in.</span><span class="sxs-lookup"><span data-stu-id="f8612-1190">If you have a sign-in risk security policy set up to Multi-Factor Authentication or block access, it is still triggered during each risky sign-in.</span></span>

 
---
 




## <a name="october-2017"></a><span data-ttu-id="f8612-1191">October 2017</span><span class="sxs-lookup"><span data-stu-id="f8612-1191">October 2017</span></span>


### <a name="deprecate-azure-ad-reports"></a><span data-ttu-id="f8612-1192">Deprecate Azure AD reports</span><span class="sxs-lookup"><span data-stu-id="f8612-1192">Deprecate Azure AD reports</span></span>


<span data-ttu-id="f8612-1193">**Type:** Plan for change</span><span class="sxs-lookup"><span data-stu-id="f8612-1193">**Type:** Plan for change</span></span>  
<span data-ttu-id="f8612-1194">**Service category:** Reporting</span><span class="sxs-lookup"><span data-stu-id="f8612-1194">**Service category:** Reporting</span></span>  
<span data-ttu-id="f8612-1195">**Product capability:** Identity Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1195">**Product capability:** Identity Lifecycle Management</span></span>  



<span data-ttu-id="f8612-1196">The Azure portal provides you with:</span><span class="sxs-lookup"><span data-stu-id="f8612-1196">The Azure portal provides you with:</span></span>

- <span data-ttu-id="f8612-1197">A new Azure AD administration console.</span><span class="sxs-lookup"><span data-stu-id="f8612-1197">A new Azure AD administration console.</span></span>
- <span data-ttu-id="f8612-1198">New APIs for activity and security reports.</span><span class="sxs-lookup"><span data-stu-id="f8612-1198">New APIs for activity and security reports.</span></span>
 
<span data-ttu-id="f8612-1199">Due to these new capabilities, the report APIs under the /reports endpoint were retired on December 10, 2017.</span><span class="sxs-lookup"><span data-stu-id="f8612-1199">Due to these new capabilities, the report APIs under the /reports endpoint were retired on December 10, 2017.</span></span> 

---

### <a name="automatic-sign-in-field-detection"></a><span data-ttu-id="f8612-1200">Automatic sign-in field detection</span><span class="sxs-lookup"><span data-stu-id="f8612-1200">Automatic sign-in field detection</span></span>


<span data-ttu-id="f8612-1201">**Type:** Fixed</span><span class="sxs-lookup"><span data-stu-id="f8612-1201">**Type:** Fixed</span></span>   
<span data-ttu-id="f8612-1202">**Service category:** My Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-1202">**Service category:** My Apps</span></span>  
<span data-ttu-id="f8612-1203">**Product capability:** Single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8612-1203">**Product capability:** Single sign-on</span></span>  



<span data-ttu-id="f8612-1204">Azure AD supports automatic sign-in field detection for applications that render an HTML user name and password field.</span><span class="sxs-lookup"><span data-stu-id="f8612-1204">Azure AD supports automatic sign-in field detection for applications that render an HTML user name and password field.</span></span> <span data-ttu-id="f8612-1205">These steps are documented in [How to automatically capture sign-in fields for an application](https://docs.microsoft.com/azure/active-directory/application-config-sso-problem-configure-password-sso-non-gallery#how-to-manually-capture-sign-in-fields-for-an-application).</span><span class="sxs-lookup"><span data-stu-id="f8612-1205">These steps are documented in [How to automatically capture sign-in fields for an application](https://docs.microsoft.com/azure/active-directory/application-config-sso-problem-configure-password-sso-non-gallery#how-to-manually-capture-sign-in-fields-for-an-application).</span></span> <span data-ttu-id="f8612-1206">You can find this capability by adding a *Non-Gallery* application on the **Enterprise Applications** page in the [Azure portal](http://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8612-1206">You can find this capability by adding a *Non-Gallery* application on the **Enterprise Applications** page in the [Azure portal](http://aad.portal.azure.com).</span></span> <span data-ttu-id="f8612-1207">Additionally, you can configure the **Single Sign-on** mode on this new application to **Password-based Single Sign-on**, enter a web URL, and then save the page.</span><span class="sxs-lookup"><span data-stu-id="f8612-1207">Additionally, you can configure the **Single Sign-on** mode on this new application to **Password-based Single Sign-on**, enter a web URL, and then save the page.</span></span>
 
<span data-ttu-id="f8612-1208">Due to a service issue, this functionality was temporarily disabled.</span><span class="sxs-lookup"><span data-stu-id="f8612-1208">Due to a service issue, this functionality was temporarily disabled.</span></span> <span data-ttu-id="f8612-1209">The issue was resolved, and the automatic sign-in field detection is available again.</span><span class="sxs-lookup"><span data-stu-id="f8612-1209">The issue was resolved, and the automatic sign-in field detection is available again.</span></span>

---

### <a name="new-multi-factor-authentication-features"></a><span data-ttu-id="f8612-1210">New Multi-Factor Authentication features</span><span class="sxs-lookup"><span data-stu-id="f8612-1210">New Multi-Factor Authentication features</span></span>


<span data-ttu-id="f8612-1211">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1211">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1212">**Service category:** Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="f8612-1212">**Service category:** Multi-factor authentication</span></span>  
<span data-ttu-id="f8612-1213">**Product capability:** Identity security and protection</span><span class="sxs-lookup"><span data-stu-id="f8612-1213">**Product capability:** Identity security and protection</span></span>  



<span data-ttu-id="f8612-1214">Multi-factor authentication (MFA) is an essential part of protecting your organization.</span><span class="sxs-lookup"><span data-stu-id="f8612-1214">Multi-factor authentication (MFA) is an essential part of protecting your organization.</span></span> <span data-ttu-id="f8612-1215">To make credentials more adaptive and the experience more seamless, the following features were added:</span><span class="sxs-lookup"><span data-stu-id="f8612-1215">To make credentials more adaptive and the experience more seamless, the following features were added:</span></span> 

- <span data-ttu-id="f8612-1216">Multi-factor challenge results are directly integrated into the Azure AD sign-in report, which includes programmatic access to MFA results.</span><span class="sxs-lookup"><span data-stu-id="f8612-1216">Multi-factor challenge results are directly integrated into the Azure AD sign-in report, which includes programmatic access to MFA results.</span></span>
- <span data-ttu-id="f8612-1217">The MFA configuration is more deeply integrated into the Azure AD configuration experience in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f8612-1217">The MFA configuration is more deeply integrated into the Azure AD configuration experience in the Azure portal.</span></span>

<span data-ttu-id="f8612-1218">With this public preview, MFA management and reporting are an integrated part of the core Azure AD configuration experience.</span><span class="sxs-lookup"><span data-stu-id="f8612-1218">With this public preview, MFA management and reporting are an integrated part of the core Azure AD configuration experience.</span></span> <span data-ttu-id="f8612-1219">Now you can manage the MFA management portal functionality within the Azure AD experience.</span><span class="sxs-lookup"><span data-stu-id="f8612-1219">Now you can manage the MFA management portal functionality within the Azure AD experience.</span></span>

<span data-ttu-id="f8612-1220">For more information, see [Reference for MFA reporting in the Azure portal](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins-mfa).</span><span class="sxs-lookup"><span data-stu-id="f8612-1220">For more information, see [Reference for MFA reporting in the Azure portal](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins-mfa).</span></span> 


---

### <a name="terms-of-use"></a><span data-ttu-id="f8612-1221">Terms of use</span><span class="sxs-lookup"><span data-stu-id="f8612-1221">Terms of use</span></span>



<span data-ttu-id="f8612-1222">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1222">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1223">**Service category:** Terms of use</span><span class="sxs-lookup"><span data-stu-id="f8612-1223">**Service category:** Terms of use</span></span>  
<span data-ttu-id="f8612-1224">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-1224">**Product capability:** Compliance</span></span>  



<span data-ttu-id="f8612-1225">You can use Azure AD terms of use to present information such as relevant disclaimers for legal or compliance requirements to users.</span><span class="sxs-lookup"><span data-stu-id="f8612-1225">You can use Azure AD terms of use to present information such as relevant disclaimers for legal or compliance requirements to users.</span></span>

<span data-ttu-id="f8612-1226">You can use Azure AD terms of use in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="f8612-1226">You can use Azure AD terms of use in the following scenarios:</span></span>

- <span data-ttu-id="f8612-1227">General terms of use for all users in your organization</span><span class="sxs-lookup"><span data-stu-id="f8612-1227">General terms of use for all users in your organization</span></span>
- <span data-ttu-id="f8612-1228">Specific terms of use based on a user's attributes (for example, doctors vs. nurses or domestic vs. international employees, done by dynamic groups)</span><span class="sxs-lookup"><span data-stu-id="f8612-1228">Specific terms of use based on a user's attributes (for example, doctors vs. nurses or domestic vs. international employees, done by dynamic groups)</span></span>
- <span data-ttu-id="f8612-1229">Specific terms of use for accessing high-impact business apps, like Salesforce</span><span class="sxs-lookup"><span data-stu-id="f8612-1229">Specific terms of use for accessing high-impact business apps, like Salesforce</span></span>

<span data-ttu-id="f8612-1230">For more information, see [Azure AD terms of use](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span><span class="sxs-lookup"><span data-stu-id="f8612-1230">For more information, see [Azure AD terms of use](https://docs.microsoft.com/azure/active-directory/active-directory-tou).</span></span>


---

### <a name="enhancements-to-privileged-identity-management"></a><span data-ttu-id="f8612-1231">Enhancements to Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1231">Enhancements to Privileged Identity Management</span></span>


<span data-ttu-id="f8612-1232">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1232">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1233">**Service category:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1233">**Service category:** Privileged Identity Management</span></span>  
<span data-ttu-id="f8612-1234">**Product capability:** Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="f8612-1234">**Product capability:** Privileged Identity Management</span></span>  


<span data-ttu-id="f8612-1235">With Azure AD Privileged Identity Management, you can manage, control, and monitor access to Azure resources (preview) within your organization to:</span><span class="sxs-lookup"><span data-stu-id="f8612-1235">With Azure AD Privileged Identity Management, you can manage, control, and monitor access to Azure resources (preview) within your organization to:</span></span>

- <span data-ttu-id="f8612-1236">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="f8612-1236">Subscriptions</span></span>
- <span data-ttu-id="f8612-1237">Resource groups</span><span class="sxs-lookup"><span data-stu-id="f8612-1237">Resource groups</span></span>
- <span data-ttu-id="f8612-1238">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="f8612-1238">Virtual machines</span></span> 

<span data-ttu-id="f8612-1239">All resources within the Azure portal that use the Azure RBAC functionality can take advantage of all the security and lifecycle management capabilities that Azure AD Privileged Identity Management has to offer.</span><span class="sxs-lookup"><span data-stu-id="f8612-1239">All resources within the Azure portal that use the Azure RBAC functionality can take advantage of all the security and lifecycle management capabilities that Azure AD Privileged Identity Management has to offer.</span></span>

<span data-ttu-id="f8612-1240">For more information, see [Privileged Identity Management for Azure resources](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac).</span><span class="sxs-lookup"><span data-stu-id="f8612-1240">For more information, see [Privileged Identity Management for Azure resources](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac).</span></span>


---

### <a name="access-reviews"></a><span data-ttu-id="f8612-1241">Access reviews</span><span class="sxs-lookup"><span data-stu-id="f8612-1241">Access reviews</span></span>


<span data-ttu-id="f8612-1242">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1242">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1243">**Service category:** Access reviews</span><span class="sxs-lookup"><span data-stu-id="f8612-1243">**Service category:** Access reviews</span></span>  
<span data-ttu-id="f8612-1244">**Product capability:** Compliance</span><span class="sxs-lookup"><span data-stu-id="f8612-1244">**Product capability:** Compliance</span></span>  



<span data-ttu-id="f8612-1245">Organizations can use access reviews (preview) to efficiently manage group memberships and access to enterprise applications:</span><span class="sxs-lookup"><span data-stu-id="f8612-1245">Organizations can use access reviews (preview) to efficiently manage group memberships and access to enterprise applications:</span></span> 

- <span data-ttu-id="f8612-1246">You can recertify guest user access by using access reviews of their access to applications and memberships of groups.</span><span class="sxs-lookup"><span data-stu-id="f8612-1246">You can recertify guest user access by using access reviews of their access to applications and memberships of groups.</span></span> <span data-ttu-id="f8612-1247">Reviewers can efficiently decide whether to allow guests continued access based on the insights provided by the access reviews.</span><span class="sxs-lookup"><span data-stu-id="f8612-1247">Reviewers can efficiently decide whether to allow guests continued access based on the insights provided by the access reviews.</span></span>
- <span data-ttu-id="f8612-1248">You can recertify employee access to applications and group memberships with access reviews.</span><span class="sxs-lookup"><span data-stu-id="f8612-1248">You can recertify employee access to applications and group memberships with access reviews.</span></span>

<span data-ttu-id="f8612-1249">You can collect the access review controls into programs relevant for your organization to track reviews for compliance or risk-sensitive applications.</span><span class="sxs-lookup"><span data-stu-id="f8612-1249">You can collect the access review controls into programs relevant for your organization to track reviews for compliance or risk-sensitive applications.</span></span>

<span data-ttu-id="f8612-1250">For more information, see [Azure AD access reviews](https://docs.microsoft.com/azure/active-directory/active-directory-azure-ad-controls-access-reviews-overview).</span><span class="sxs-lookup"><span data-stu-id="f8612-1250">For more information, see [Azure AD access reviews](https://docs.microsoft.com/azure/active-directory/active-directory-azure-ad-controls-access-reviews-overview).</span></span>


---

### <a name="hide-third-party-applications-from-my-apps-and-the-office-365-app-launcher"></a><span data-ttu-id="f8612-1251">Hide third-party applications from My Apps and the Office 365 app launcher</span><span class="sxs-lookup"><span data-stu-id="f8612-1251">Hide third-party applications from My Apps and the Office 365 app launcher</span></span>



<span data-ttu-id="f8612-1252">**Type:** New feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1252">**Type:** New feature</span></span>  
<span data-ttu-id="f8612-1253">**Service category:** My Apps</span><span class="sxs-lookup"><span data-stu-id="f8612-1253">**Service category:** My Apps</span></span>  
<span data-ttu-id="f8612-1254">**Product capability:** Single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8612-1254">**Product capability:** Single sign-on</span></span>  



<span data-ttu-id="f8612-1255">You now can better manage apps that show up on your users' portals through a new **hide app** property.</span><span class="sxs-lookup"><span data-stu-id="f8612-1255">You now can better manage apps that show up on your users' portals through a new **hide app** property.</span></span> <span data-ttu-id="f8612-1256">You can hide apps to help in cases where app tiles show up for back-end services or duplicate tiles and clutter users' app launchers.</span><span class="sxs-lookup"><span data-stu-id="f8612-1256">You can hide apps to help in cases where app tiles show up for back-end services or duplicate tiles and clutter users' app launchers.</span></span> <span data-ttu-id="f8612-1257">The toggle is in the **Properties** section of the third-party app and is labeled **Visible to user?**</span><span class="sxs-lookup"><span data-stu-id="f8612-1257">The toggle is in the **Properties** section of the third-party app and is labeled **Visible to user?**</span></span> <span data-ttu-id="f8612-1258">You also can hide an app programmatically through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8612-1258">You also can hide an app programmatically through PowerShell.</span></span> 

<span data-ttu-id="f8612-1259">For more information, see [Hide a third-party application from a user's experience in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-hide-third-party-app).</span><span class="sxs-lookup"><span data-stu-id="f8612-1259">For more information, see [Hide a third-party application from a user's experience in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-hide-third-party-app).</span></span> 


<span data-ttu-id="f8612-1260">**What's available?**</span><span class="sxs-lookup"><span data-stu-id="f8612-1260">**What's available?**</span></span>

 <span data-ttu-id="f8612-1261">As part of the transition to the new admin console, two new APIs for retrieving Azure AD activity logs are available.</span><span class="sxs-lookup"><span data-stu-id="f8612-1261">As part of the transition to the new admin console, two new APIs for retrieving Azure AD activity logs are available.</span></span> <span data-ttu-id="f8612-1262">The new set of APIs provides richer filtering and sorting functionality in addition to providing richer audit and sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="f8612-1262">The new set of APIs provides richer filtering and sorting functionality in addition to providing richer audit and sign-in activities.</span></span> <span data-ttu-id="f8612-1263">The data previously available through the security reports now can be accessed through the Identity Protection Risk Events API in Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f8612-1263">The data previously available through the security reports now can be accessed through the Identity Protection Risk Events API in Microsoft Graph.</span></span>


## <a name="september-2017"></a><span data-ttu-id="f8612-1264">September 2017</span><span class="sxs-lookup"><span data-stu-id="f8612-1264">September 2017</span></span>

### <a name="hotfix-for-identity-manager"></a><span data-ttu-id="f8612-1265">Hotfix for Identity Manager</span><span class="sxs-lookup"><span data-stu-id="f8612-1265">Hotfix for Identity Manager</span></span>


<span data-ttu-id="f8612-1266">**Type:** Changed feature</span><span class="sxs-lookup"><span data-stu-id="f8612-1266">**Type:** Changed feature</span></span>  
<span data-ttu-id="f8612-1267">**Service category:** Identity Manager</span><span class="sxs-lookup"><span data-stu-id="f8612-1267">**Service category:** Identity Manager</span></span>  
<span data-ttu-id="f8612-1268">**Product capability:** Identity lifecycle management</span><span class="sxs-lookup"><span data-stu-id="f8612-1268">**Product capability:** Identity lifecycle management</span></span>  



<span data-ttu-id="f8612-1269">A hotfix roll-up package (build 4.4.1642.0) is available as of September 25, 2017, for Identity Manager 2016 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="f8612-1269">A hotfix roll-up package (build 4.4.1642.0) is available as of September 25, 2017, for Identity Manager 2016 Service Pack 1.</span></span> <span data-ttu-id="f8612-1270">This roll-up package:</span><span class="sxs-lookup"><span data-stu-id="f8612-1270">This roll-up package:</span></span>

- <span data-ttu-id="f8612-1271">Resolves issues and adds improvements.</span><span class="sxs-lookup"><span data-stu-id="f8612-1271">Resolves issues and adds improvements.</span></span>
- <span data-ttu-id="f8612-1272">Is a cumulative update that replaces all Identity Manager 2016 Service Pack 1 updates up to build 4.4.1459.0 for Identity Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="f8612-1272">Is a cumulative update that replaces all Identity Manager 2016 Service Pack 1 updates up to build 4.4.1459.0 for Identity Manager 2016.</span></span> 
- <span data-ttu-id="f8612-1273">Requires you to have Identity Manager 2016 build 4.4.1302.0.</span><span class="sxs-lookup"><span data-stu-id="f8612-1273">Requires you to have Identity Manager 2016 build 4.4.1302.0.</span></span> 

<span data-ttu-id="f8612-1274">For more information, see [Hotfix rollup package (build 4.4.1642.0) is available for Identity Manager 2016 Service Pack 1](https://support.microsoft.com/help/4021562).</span><span class="sxs-lookup"><span data-stu-id="f8612-1274">For more information, see [Hotfix rollup package (build 4.4.1642.0) is available for Identity Manager 2016 Service Pack 1](https://support.microsoft.com/help/4021562).</span></span> 

---
