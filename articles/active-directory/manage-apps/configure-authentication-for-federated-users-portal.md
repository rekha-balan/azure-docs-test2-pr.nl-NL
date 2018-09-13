---
title: Configure sign-in auto-acceleration for an application using a Home Realm Discovery policy | Microsoft Docs
description: Explains what an Azure AD tenant is, and how to manage Azure through Azure Active Directory.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/08/2018
ms.author: barbkess
ms.openlocfilehash: f24be44b00f9c4e789e8d4797f6a0516dcfe940f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967027"
---
# <a name="configure-azure-active-directory-sign-in-behavior-for-an-application-by-using-a-home-realm-discovery-policy"></a><span data-ttu-id="570a8-103">Configure Azure Active Directory sign in behavior for an application by using a Home Realm Discovery policy</span><span class="sxs-lookup"><span data-stu-id="570a8-103">Configure Azure Active Directory sign in behavior for an application by using a Home Realm Discovery policy</span></span>

<span data-ttu-id="570a8-104">The following document provides an introduction to configuring Azure Active Directory authentication behavior for federated users.</span><span class="sxs-lookup"><span data-stu-id="570a8-104">The following document provides an introduction to configuring Azure Active Directory authentication behavior for federated users.</span></span>   <span data-ttu-id="570a8-105">It covers configuration of auto-acceleration and authentication restrictions for users in federated domains.</span><span class="sxs-lookup"><span data-stu-id="570a8-105">It covers configuration of auto-acceleration and authentication restrictions for users in federated domains.</span></span>

## <a name="home-realm-discovery"></a><span data-ttu-id="570a8-106">Home Realm Discovery</span><span class="sxs-lookup"><span data-stu-id="570a8-106">Home Realm Discovery</span></span>
<span data-ttu-id="570a8-107">Home Realm Discovery (HRD) is the process that allows Azure Active Directory (Azure AD) to determine where a user needs to authenticate at sign-in time.</span><span class="sxs-lookup"><span data-stu-id="570a8-107">Home Realm Discovery (HRD) is the process that allows Azure Active Directory (Azure AD) to determine where a user needs to authenticate at sign-in time.</span></span>  <span data-ttu-id="570a8-108">When a user signs in to an Azure AD tenant to access a resource, or to the Azure AD common sign-in page, they type a user name (UPN).</span><span class="sxs-lookup"><span data-stu-id="570a8-108">When a user signs in to an Azure AD tenant to access a resource, or to the Azure AD common sign-in page, they type a user name (UPN).</span></span> <span data-ttu-id="570a8-109">Azure AD uses that to discover where the user needs to sign in.</span><span class="sxs-lookup"><span data-stu-id="570a8-109">Azure AD uses that to discover where the user needs to sign in.</span></span> 

<span data-ttu-id="570a8-110">The user might need to be taken to one of the following locations to be authenticated:</span><span class="sxs-lookup"><span data-stu-id="570a8-110">The user might need to be taken to one of the following locations to be authenticated:</span></span>

- <span data-ttu-id="570a8-111">The home tenant of the user (might be the same tenant as the resource that the user is attempting to access).</span><span class="sxs-lookup"><span data-stu-id="570a8-111">The home tenant of the user (might be the same tenant as the resource that the user is attempting to access).</span></span> 

- <span data-ttu-id="570a8-112">Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="570a8-112">Microsoft account.</span></span>  <span data-ttu-id="570a8-113">The user is a guest in the resource tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-113">The user is a guest in the resource tenant.</span></span>

-  <span data-ttu-id="570a8-114">An on-premises identity provider such as Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="570a8-114">An on-premises identity provider such as Active Directory Federation Services (AD FS).</span></span>

- <span data-ttu-id="570a8-115">Another identity provider that's federated with the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-115">Another identity provider that's federated with the Azure AD tenant.</span></span>

## <a name="auto-acceleration"></a><span data-ttu-id="570a8-116">Auto-acceleration</span><span class="sxs-lookup"><span data-stu-id="570a8-116">Auto-acceleration</span></span> 
<span data-ttu-id="570a8-117">Some organizations configure domains in their Azure Active Directory tenant to federate with another IdP, such as AD FS for user authentication.</span><span class="sxs-lookup"><span data-stu-id="570a8-117">Some organizations configure domains in their Azure Active Directory tenant to federate with another IdP, such as AD FS for user authentication.</span></span>  

<span data-ttu-id="570a8-118">When a user signs into an application, they are first presented with an Azure AD sign-in page.</span><span class="sxs-lookup"><span data-stu-id="570a8-118">When a user signs into an application, they are first presented with an Azure AD sign-in page.</span></span> <span data-ttu-id="570a8-119">After they have typed their UPN, if they are in a federated domain they are then taken to the sign-in page of the IdP serving that domain.</span><span class="sxs-lookup"><span data-stu-id="570a8-119">After they have typed their UPN, if they are in a federated domain they are then taken to the sign-in page of the IdP serving that domain.</span></span> <span data-ttu-id="570a8-120">Under certain circumstances, administrators might want to direct users to the sign-in page when they're signing in to specific applications.</span><span class="sxs-lookup"><span data-stu-id="570a8-120">Under certain circumstances, administrators might want to direct users to the sign-in page when they're signing in to specific applications.</span></span> 

<span data-ttu-id="570a8-121">As a result users can skip the initial Azure Active Directory page.</span><span class="sxs-lookup"><span data-stu-id="570a8-121">As a result users can skip the initial Azure Active Directory page.</span></span> <span data-ttu-id="570a8-122">This process is referred to as “sign-in auto-acceleration.”</span><span class="sxs-lookup"><span data-stu-id="570a8-122">This process is referred to as “sign-in auto-acceleration.”</span></span>

<span data-ttu-id="570a8-123">In cases where the tenant is federated to another IdP for sign-in, auto-acceleration makes user sign-in more streamlined.</span><span class="sxs-lookup"><span data-stu-id="570a8-123">In cases where the tenant is federated to another IdP for sign-in, auto-acceleration makes user sign-in more streamlined.</span></span>  <span data-ttu-id="570a8-124">You can configure auto-acceleration for individual applications.</span><span class="sxs-lookup"><span data-stu-id="570a8-124">You can configure auto-acceleration for individual applications.</span></span>

>[!NOTE]
><span data-ttu-id="570a8-125">If you configure an application for auto-acceleration, guest users cannot sign in.</span><span class="sxs-lookup"><span data-stu-id="570a8-125">If you configure an application for auto-acceleration, guest users cannot sign in.</span></span> <span data-ttu-id="570a8-126">If you take a user straight to a federated IdP for authentication, there is no way to for them to get back to the Azure Active Directory sign-in page.</span><span class="sxs-lookup"><span data-stu-id="570a8-126">If you take a user straight to a federated IdP for authentication, there is no way to for them to get back to the Azure Active Directory sign-in page.</span></span> <span data-ttu-id="570a8-127">Guest users, who might need to be directed to other tenants or an external IdP such as a Microsoft account, can't sign in to that application because they're skipping the Home Realm Discovery step.</span><span class="sxs-lookup"><span data-stu-id="570a8-127">Guest users, who might need to be directed to other tenants or an external IdP such as a Microsoft account, can't sign in to that application because they're skipping the Home Realm Discovery step.</span></span>  

<span data-ttu-id="570a8-128">There are two ways to control auto-acceleration to a federated IdP:</span><span class="sxs-lookup"><span data-stu-id="570a8-128">There are two ways to control auto-acceleration to a federated IdP:</span></span>   

- <span data-ttu-id="570a8-129">Use a domain hint on authentication requests for an application.</span><span class="sxs-lookup"><span data-stu-id="570a8-129">Use a domain hint on authentication requests for an application.</span></span> 
- <span data-ttu-id="570a8-130">Configure a Home Realm Discovery policy to enable auto-acceleration.</span><span class="sxs-lookup"><span data-stu-id="570a8-130">Configure a Home Realm Discovery policy to enable auto-acceleration.</span></span>

### <a name="domain-hints"></a><span data-ttu-id="570a8-131">Domain hints</span><span class="sxs-lookup"><span data-stu-id="570a8-131">Domain hints</span></span>    
<span data-ttu-id="570a8-132">Domain hints are directives that are included in the authentication request from an application.</span><span class="sxs-lookup"><span data-stu-id="570a8-132">Domain hints are directives that are included in the authentication request from an application.</span></span> <span data-ttu-id="570a8-133">They can be used to accelerate the user to their federated IdP sign-in page.</span><span class="sxs-lookup"><span data-stu-id="570a8-133">They can be used to accelerate the user to their federated IdP sign-in page.</span></span> <span data-ttu-id="570a8-134">Or they can be used by a multi-tenant application to accelerate the user straight to the branded Azure AD sign-in page for their tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-134">Or they can be used by a multi-tenant application to accelerate the user straight to the branded Azure AD sign-in page for their tenant.</span></span>  

<span data-ttu-id="570a8-135">For example, the application "largeapp.com" might enable their customers to access the application at a custom URL "contoso.largeapp.com."</span><span class="sxs-lookup"><span data-stu-id="570a8-135">For example, the application "largeapp.com" might enable their customers to access the application at a custom URL "contoso.largeapp.com."</span></span> <span data-ttu-id="570a8-136">The app might also include a domain hint to contoso.com in the authentication request.</span><span class="sxs-lookup"><span data-stu-id="570a8-136">The app might also include a domain hint to contoso.com in the authentication request.</span></span> 

<span data-ttu-id="570a8-137">Domain hint syntax varies depending on the protocol that's used, and it's typically configured in the application.</span><span class="sxs-lookup"><span data-stu-id="570a8-137">Domain hint syntax varies depending on the protocol that's used, and it's typically configured in the application.</span></span>

<span data-ttu-id="570a8-138">**WS-Federation**:  whr=contoso.com in the query string.</span><span class="sxs-lookup"><span data-stu-id="570a8-138">**WS-Federation**:  whr=contoso.com in the query string.</span></span>

<span data-ttu-id="570a8-139">**SAML**:  Either a SAML authentication request that contains a domain hint or a query string whr=contoso.com.</span><span class="sxs-lookup"><span data-stu-id="570a8-139">**SAML**:  Either a SAML authentication request that contains a domain hint or a query string whr=contoso.com.</span></span>

<span data-ttu-id="570a8-140">**Open ID Connect**: A query string domain_hint=contoso.com.</span><span class="sxs-lookup"><span data-stu-id="570a8-140">**Open ID Connect**: A query string domain_hint=contoso.com.</span></span> 

<span data-ttu-id="570a8-141">If a domain hint is included in the authentication request from the application, and the tenant is federated with that domain, Azure AD attempts to redirect sign-in to the IdP that's configured for that domain.</span><span class="sxs-lookup"><span data-stu-id="570a8-141">If a domain hint is included in the authentication request from the application, and the tenant is federated with that domain, Azure AD attempts to redirect sign-in to the IdP that's configured for that domain.</span></span> 

<span data-ttu-id="570a8-142">If the domain hint doesn’t refer to a verified federated domain, it is ignored and normal Home Realm Discovery is invoked.</span><span class="sxs-lookup"><span data-stu-id="570a8-142">If the domain hint doesn’t refer to a verified federated domain, it is ignored and normal Home Realm Discovery is invoked.</span></span>

<span data-ttu-id="570a8-143">For more information about auto-acceleration using the domain hints that are supported by Azure Active Directory, see the [Enterprise Mobility + Security blog](https://cloudblogs.microsoft.com/enterprisemobility/2015/02/11/using-azure-ad-to-land-users-on-their-custom-login-page-from-within-your-app/).</span><span class="sxs-lookup"><span data-stu-id="570a8-143">For more information about auto-acceleration using the domain hints that are supported by Azure Active Directory, see the [Enterprise Mobility + Security blog](https://cloudblogs.microsoft.com/enterprisemobility/2015/02/11/using-azure-ad-to-land-users-on-their-custom-login-page-from-within-your-app/).</span></span>

>[!NOTE]
><span data-ttu-id="570a8-144">If a domain hint is included in an authentication request, its presence overrides auto-acceleration that is set for the application in HRD policy.</span><span class="sxs-lookup"><span data-stu-id="570a8-144">If a domain hint is included in an authentication request, its presence overrides auto-acceleration that is set for the application in HRD policy.</span></span>

### <a name="home-realm-discovery-policy-for-auto-acceleration"></a><span data-ttu-id="570a8-145">Home Realm Discovery policy for auto-acceleration</span><span class="sxs-lookup"><span data-stu-id="570a8-145">Home Realm Discovery policy for auto-acceleration</span></span>
<span data-ttu-id="570a8-146">Some applications do not provide a way to configure the authentication request they emit.</span><span class="sxs-lookup"><span data-stu-id="570a8-146">Some applications do not provide a way to configure the authentication request they emit.</span></span> <span data-ttu-id="570a8-147">In these cases, it’s not possible to use domain hints to control auto-acceleration.</span><span class="sxs-lookup"><span data-stu-id="570a8-147">In these cases, it’s not possible to use domain hints to control auto-acceleration.</span></span> <span data-ttu-id="570a8-148">Auto-acceleration can be configured via policy to achieve the same behavior.</span><span class="sxs-lookup"><span data-stu-id="570a8-148">Auto-acceleration can be configured via policy to achieve the same behavior.</span></span>  

## <a name="enable-direct-authentication-for-legacy-applications"></a><span data-ttu-id="570a8-149">Enable direct authentication for legacy applications</span><span class="sxs-lookup"><span data-stu-id="570a8-149">Enable direct authentication for legacy applications</span></span>
<span data-ttu-id="570a8-150">Best practice is for applications to use AAD libraries and interactive sign-in to authenticate users.</span><span class="sxs-lookup"><span data-stu-id="570a8-150">Best practice is for applications to use AAD libraries and interactive sign-in to authenticate users.</span></span> <span data-ttu-id="570a8-151">The libraries take care of the federated user flows.</span><span class="sxs-lookup"><span data-stu-id="570a8-151">The libraries take care of the federated user flows.</span></span>  <span data-ttu-id="570a8-152">Sometimes legacy applications aren't written to understand federation.</span><span class="sxs-lookup"><span data-stu-id="570a8-152">Sometimes legacy applications aren't written to understand federation.</span></span> <span data-ttu-id="570a8-153">They don't perform home realm discovery and do not interact with the correct federated endpoint to authenticate a user.</span><span class="sxs-lookup"><span data-stu-id="570a8-153">They don't perform home realm discovery and do not interact with the correct federated endpoint to authenticate a user.</span></span> <span data-ttu-id="570a8-154">If you choose to, you can use HRD Policy to enable specific legacy applications that submit username/password credentials to authenticate directly with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="570a8-154">If you choose to, you can use HRD Policy to enable specific legacy applications that submit username/password credentials to authenticate directly with Azure Active Directory.</span></span> <span data-ttu-id="570a8-155">Password Hash Sync must be enabled.</span><span class="sxs-lookup"><span data-stu-id="570a8-155">Password Hash Sync must be enabled.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="570a8-156">Only enable direct authentication if you have Password Hash Sync turned on and you know it's okay to authenticate this application without any policies implemented by your on-premises IdP.</span><span class="sxs-lookup"><span data-stu-id="570a8-156">Only enable direct authentication if you have Password Hash Sync turned on and you know it's okay to authenticate this application without any policies implemented by your on-premises IdP.</span></span> <span data-ttu-id="570a8-157">If you turn off Password Hash Sync, or turn off Directory Synchronization with AD Connect for any reason, you should remove this policy to prevent the possibility of direct authentication using a stale password hash.</span><span class="sxs-lookup"><span data-stu-id="570a8-157">If you turn off Password Hash Sync, or turn off Directory Synchronization with AD Connect for any reason, you should remove this policy to prevent the possibility of direct authentication using a stale password hash.</span></span>

## <a name="set-hrd-policy"></a><span data-ttu-id="570a8-158">Set HRD policy</span><span class="sxs-lookup"><span data-stu-id="570a8-158">Set HRD policy</span></span>
<span data-ttu-id="570a8-159">There are three steps to setting HRD policy on an application for federated sign-in auto-acceleration or direct cloud-based applications:</span><span class="sxs-lookup"><span data-stu-id="570a8-159">There are three steps to setting HRD policy on an application for federated sign-in auto-acceleration or direct cloud-based applications:</span></span>

1. <span data-ttu-id="570a8-160">Create an HRD policy.</span><span class="sxs-lookup"><span data-stu-id="570a8-160">Create an HRD policy.</span></span>

2. <span data-ttu-id="570a8-161">Locate the service principal to which to attach the policy.</span><span class="sxs-lookup"><span data-stu-id="570a8-161">Locate the service principal to which to attach the policy.</span></span>

3. <span data-ttu-id="570a8-162">Attach the policy to the service principal.</span><span class="sxs-lookup"><span data-stu-id="570a8-162">Attach the policy to the service principal.</span></span> 

<span data-ttu-id="570a8-163">Policies only take effect for a specific application when they are attached to a service principal.</span><span class="sxs-lookup"><span data-stu-id="570a8-163">Policies only take effect for a specific application when they are attached to a service principal.</span></span> 

<span data-ttu-id="570a8-164">Only one HRD policy can be active on a service principal at any one time.</span><span class="sxs-lookup"><span data-stu-id="570a8-164">Only one HRD policy can be active on a service principal at any one time.</span></span>  

<span data-ttu-id="570a8-165">You can use either the Microsoft Azure Active Directory Graph API directly, or the Azure Active Directory PowerShell cmdlets to create and manage HRD policy.</span><span class="sxs-lookup"><span data-stu-id="570a8-165">You can use either the Microsoft Azure Active Directory Graph API directly, or the Azure Active Directory PowerShell cmdlets to create and manage HRD policy.</span></span>

<span data-ttu-id="570a8-166">The Graph API that manipulates policy is described in the [Operations on policy](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) article on MSDN.</span><span class="sxs-lookup"><span data-stu-id="570a8-166">The Graph API that manipulates policy is described in the [Operations on policy](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) article on MSDN.</span></span>

<span data-ttu-id="570a8-167">Following is an example HRD policy definition:</span><span class="sxs-lookup"><span data-stu-id="570a8-167">Following is an example HRD policy definition:</span></span>
    
 ```
   {  
    "HomeRealmDiscoveryPolicy":
    {  
    "AccelerateToFederatedDomain":true,
    "PreferredDomain":"federated.example.edu",
    "AllowCloudPasswordValidation":true
    }
   }
```

<span data-ttu-id="570a8-168">The policy type is "HomeRealmDiscoveryPolicy."</span><span class="sxs-lookup"><span data-stu-id="570a8-168">The policy type is "HomeRealmDiscoveryPolicy."</span></span>

<span data-ttu-id="570a8-169">**AccelerateToFederatedDomain** is optional.</span><span class="sxs-lookup"><span data-stu-id="570a8-169">**AccelerateToFederatedDomain** is optional.</span></span> <span data-ttu-id="570a8-170">If **AccelerateToFederatedDomain** is false, the policy has no effect on auto-acceleration.</span><span class="sxs-lookup"><span data-stu-id="570a8-170">If **AccelerateToFederatedDomain** is false, the policy has no effect on auto-acceleration.</span></span> <span data-ttu-id="570a8-171">If **AccelerateToFederatedDomain** is true and there is only one verified and federated domain in the tenant, then users will be taken straight to the federated IdP for sign in.</span><span class="sxs-lookup"><span data-stu-id="570a8-171">If **AccelerateToFederatedDomain** is true and there is only one verified and federated domain in the tenant, then users will be taken straight to the federated IdP for sign in.</span></span> <span data-ttu-id="570a8-172">If it is true and there is more than one verified domain in the tenant, **PreferredDomain** must be specified.</span><span class="sxs-lookup"><span data-stu-id="570a8-172">If it is true and there is more than one verified domain in the tenant, **PreferredDomain** must be specified.</span></span>

<span data-ttu-id="570a8-173">**PreferredDomain** is optional.</span><span class="sxs-lookup"><span data-stu-id="570a8-173">**PreferredDomain** is optional.</span></span> <span data-ttu-id="570a8-174">**PreferredDomain** should indicate a domain to which to accelerate.</span><span class="sxs-lookup"><span data-stu-id="570a8-174">**PreferredDomain** should indicate a domain to which to accelerate.</span></span> <span data-ttu-id="570a8-175">It can be omitted if the tenant has only one federated domain.</span><span class="sxs-lookup"><span data-stu-id="570a8-175">It can be omitted if the tenant has only one federated domain.</span></span>  <span data-ttu-id="570a8-176">If it is omitted, and there is more than one verified federated domain, the policy has no effect.</span><span class="sxs-lookup"><span data-stu-id="570a8-176">If it is omitted, and there is more than one verified federated domain, the policy has no effect.</span></span>

 <span data-ttu-id="570a8-177">If **PreferredDomain** is specified, it must match a verified, federated domain for the tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-177">If **PreferredDomain** is specified, it must match a verified, federated domain for the tenant.</span></span> <span data-ttu-id="570a8-178">All users of the application must be able to sign in to that domain.</span><span class="sxs-lookup"><span data-stu-id="570a8-178">All users of the application must be able to sign in to that domain.</span></span>

<span data-ttu-id="570a8-179">**AllowCloudPasswordValidation** is optional.</span><span class="sxs-lookup"><span data-stu-id="570a8-179">**AllowCloudPasswordValidation** is optional.</span></span> <span data-ttu-id="570a8-180">If **AllowCloudPasswordValidation** is true then the application is allowed to authenticate a federated user by presenting username/password credentials directly to the Azure Active Directory token endpoint.</span><span class="sxs-lookup"><span data-stu-id="570a8-180">If **AllowCloudPasswordValidation** is true then the application is allowed to authenticate a federated user by presenting username/password credentials directly to the Azure Active Directory token endpoint.</span></span> <span data-ttu-id="570a8-181">This only works if Password Hash Sync is enabled.</span><span class="sxs-lookup"><span data-stu-id="570a8-181">This only works if Password Hash Sync is enabled.</span></span>

### <a name="priority-and-evaluation-of-hrd-policies"></a><span data-ttu-id="570a8-182">Priority and evaluation of HRD policies</span><span class="sxs-lookup"><span data-stu-id="570a8-182">Priority and evaluation of HRD policies</span></span>
<span data-ttu-id="570a8-183">HRD policies can be created and then assigned to specific organizations and service principals.</span><span class="sxs-lookup"><span data-stu-id="570a8-183">HRD policies can be created and then assigned to specific organizations and service principals.</span></span> <span data-ttu-id="570a8-184">This means that it is possible for multiple policies to apply to a specific application.</span><span class="sxs-lookup"><span data-stu-id="570a8-184">This means that it is possible for multiple policies to apply to a specific application.</span></span> <span data-ttu-id="570a8-185">The HRD policy that takes effect follows these rules:</span><span class="sxs-lookup"><span data-stu-id="570a8-185">The HRD policy that takes effect follows these rules:</span></span>


- <span data-ttu-id="570a8-186">If a domain hint is present in the authentication request, then any HRD policy is ignored for auto-acceleration.</span><span class="sxs-lookup"><span data-stu-id="570a8-186">If a domain hint is present in the authentication request, then any HRD policy is ignored for auto-acceleration.</span></span> <span data-ttu-id="570a8-187">The behavior that's specified by the domain hint is used.</span><span class="sxs-lookup"><span data-stu-id="570a8-187">The behavior that's specified by the domain hint is used.</span></span>

- <span data-ttu-id="570a8-188">Otherwise, if a policy is explicitly assigned to the service principal, it is enforced.</span><span class="sxs-lookup"><span data-stu-id="570a8-188">Otherwise, if a policy is explicitly assigned to the service principal, it is enforced.</span></span> 

- <span data-ttu-id="570a8-189">If there is no domain hint, and no policy is explicitly assigned to the service principal, a policy that's explicitly assigned to the parent organization of the service principal is enforced.</span><span class="sxs-lookup"><span data-stu-id="570a8-189">If there is no domain hint, and no policy is explicitly assigned to the service principal, a policy that's explicitly assigned to the parent organization of the service principal is enforced.</span></span> 

- <span data-ttu-id="570a8-190">If there is no domain hint, and no policy has been assigned to the service principal or the organization, the default HRD behavior is used.</span><span class="sxs-lookup"><span data-stu-id="570a8-190">If there is no domain hint, and no policy has been assigned to the service principal or the organization, the default HRD behavior is used.</span></span>

## <a name="tutorial-for-setting-hrd-policy-on-an-application"></a><span data-ttu-id="570a8-191">Tutorial for setting HRD policy on an application</span><span class="sxs-lookup"><span data-stu-id="570a8-191">Tutorial for setting HRD policy on an application</span></span> 
<span data-ttu-id="570a8-192">We'll use Azure AD PowerShell cmdlets to walk through a few scenarios, including:</span><span class="sxs-lookup"><span data-stu-id="570a8-192">We'll use Azure AD PowerShell cmdlets to walk through a few scenarios, including:</span></span>


- <span data-ttu-id="570a8-193">Setting up HRD policy to do auto-acceleration for an application in a tenant with a single federated domain.</span><span class="sxs-lookup"><span data-stu-id="570a8-193">Setting up HRD policy to do auto-acceleration for an application in a tenant with a single federated domain.</span></span>

- <span data-ttu-id="570a8-194">Setting up HRD policy to do auto-acceleration  for an application to one of several domains that are verified for your tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-194">Setting up HRD policy to do auto-acceleration  for an application to one of several domains that are verified for your tenant.</span></span>

- <span data-ttu-id="570a8-195">Setting up HRD policy to enable a legacy application to do direct username/password authentication to Azure Active Directory for a federated user.</span><span class="sxs-lookup"><span data-stu-id="570a8-195">Setting up HRD policy to enable a legacy application to do direct username/password authentication to Azure Active Directory for a federated user.</span></span>

- <span data-ttu-id="570a8-196">Listing the applications for which a policy is configured.</span><span class="sxs-lookup"><span data-stu-id="570a8-196">Listing the applications for which a policy is configured.</span></span>


### <a name="prerequisites"></a><span data-ttu-id="570a8-197">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="570a8-197">Prerequisites</span></span>
<span data-ttu-id="570a8-198">In the following examples, you create, update, link, and delete policies on application service principals in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="570a8-198">In the following examples, you create, update, link, and delete policies on application service principals in Azure AD.</span></span>

1.  <span data-ttu-id="570a8-199">To begin, download the latest Azure AD PowerShell cmdlet preview.</span><span class="sxs-lookup"><span data-stu-id="570a8-199">To begin, download the latest Azure AD PowerShell cmdlet preview.</span></span> 

2.  <span data-ttu-id="570a8-200">After you have downloaded the Azure AD PowerShell cmdlets, run the Connect command to sign in to Azure AD with your admin account:</span><span class="sxs-lookup"><span data-stu-id="570a8-200">After you have downloaded the Azure AD PowerShell cmdlets, run the Connect command to sign in to Azure AD with your admin account:</span></span>

    ``` powershell
    Connect-AzureAD -Confirm
    ```
3.  <span data-ttu-id="570a8-201">Run the following command to see all the policies in your organization:</span><span class="sxs-lookup"><span data-stu-id="570a8-201">Run the following command to see all the policies in your organization:</span></span>

    ``` powershell
    Get-AzureADPolicy
    ```

<span data-ttu-id="570a8-202">If nothing is returned, it means you have no policies created in your tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-202">If nothing is returned, it means you have no policies created in your tenant.</span></span>

### <a name="example-set-hrd-policy-for-an-application"></a><span data-ttu-id="570a8-203">Example: Set HRD policy for an application</span><span class="sxs-lookup"><span data-stu-id="570a8-203">Example: Set HRD policy for an application</span></span> 

<span data-ttu-id="570a8-204">In this example, you create a policy that when it is assigned to an application either:</span><span class="sxs-lookup"><span data-stu-id="570a8-204">In this example, you create a policy that when it is assigned to an application either:</span></span> 
- <span data-ttu-id="570a8-205">Auto-accelerates users to an AD FS sign-in screen when they are signing in to an application when there is a single domain in your tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-205">Auto-accelerates users to an AD FS sign-in screen when they are signing in to an application when there is a single domain in your tenant.</span></span> 
- <span data-ttu-id="570a8-206">Auto-accelerates users to an AD FS sign-in screen there is more than one federated domain in your tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-206">Auto-accelerates users to an AD FS sign-in screen there is more than one federated domain in your tenant.</span></span>
- <span data-ttu-id="570a8-207">Enables non-interactive username/password sign in directly to Azure Active Directory for federated users for the applications the policy is assigned to.</span><span class="sxs-lookup"><span data-stu-id="570a8-207">Enables non-interactive username/password sign in directly to Azure Active Directory for federated users for the applications the policy is assigned to.</span></span>

#### <a name="step-1-create-an-hrd-policy"></a><span data-ttu-id="570a8-208">Step 1: Create an HRD policy</span><span class="sxs-lookup"><span data-stu-id="570a8-208">Step 1: Create an HRD policy</span></span>

<span data-ttu-id="570a8-209">The following policy auto-accelerates users to an AD FS sign-in screen when they are signing in to an application when there is a single domain in your tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-209">The following policy auto-accelerates users to an AD FS sign-in screen when they are signing in to an application when there is a single domain in your tenant.</span></span>

``` powershell
New-AzureADPolicy -Definition @("{`"HomeRealmDiscoveryPolicy`":{`"AccelerateToFederatedDomain`":true}}") -DisplayName BasicAutoAccelerationPolicy -Type HomeRealmDiscoveryPolicy
```
<span data-ttu-id="570a8-210">The following policy auto-accelerates users to an AD FS sign-in screen there is more than one federated domain in your tenant.</span><span class="sxs-lookup"><span data-stu-id="570a8-210">The following policy auto-accelerates users to an AD FS sign-in screen there is more than one federated domain in your tenant.</span></span> <span data-ttu-id="570a8-211">If you have more than one federated domain that authenticates users for applications, you need specify the domain to auto-accelerate.</span><span class="sxs-lookup"><span data-stu-id="570a8-211">If you have more than one federated domain that authenticates users for applications, you need specify the domain to auto-accelerate.</span></span>

``` powershell
New-AzureADPolicy -Definition @("{`"HomeRealmDiscoveryPolicy`":{`"AccelerateToFederatedDomain`":true, `"PreferredDomain`":`"federated.example.edu`"}}") -DisplayName MultiDomainAutoAccelerationPolicy -Type HomeRealmDiscoveryPolicy
```

<span data-ttu-id="570a8-212">To create a policy to enable username/password authentication for federated users directly with Azure Active Directory for specific applications, run the following command:</span><span class="sxs-lookup"><span data-stu-id="570a8-212">To create a policy to enable username/password authentication for federated users directly with Azure Active Directory for specific applications, run the following command:</span></span>

``` powershell
New-AzureADPolicy -Definition @("{`"HomeRealmDiscoveryPolicy`":{`"AllowCloudPasswordValidation`":true}}") -DisplayName EnableDirectAuthPolicy -Type HomeRealmDiscoveryPolicy
```


<span data-ttu-id="570a8-213">To see your new policy and get its **ObjectID**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="570a8-213">To see your new policy and get its **ObjectID**, run the following command:</span></span>

``` powershell
Get-AzureADPolicy
```


<span data-ttu-id="570a8-214">To apply the HRD policy after you have created it, you can assign it to multiple application service principals.</span><span class="sxs-lookup"><span data-stu-id="570a8-214">To apply the HRD policy after you have created it, you can assign it to multiple application service principals.</span></span>

#### <a name="step-2-locate-the-service-principal-to-which-to-assign-the-policy"></a><span data-ttu-id="570a8-215">Step 2: Locate the service principal to which to assign the policy</span><span class="sxs-lookup"><span data-stu-id="570a8-215">Step 2: Locate the service principal to which to assign the policy</span></span>  
<span data-ttu-id="570a8-216">You need the **ObjectID** of the service principals to which you want to assign the policy.</span><span class="sxs-lookup"><span data-stu-id="570a8-216">You need the **ObjectID** of the service principals to which you want to assign the policy.</span></span> <span data-ttu-id="570a8-217">There are several ways to find the **ObjectID** of service principals.</span><span class="sxs-lookup"><span data-stu-id="570a8-217">There are several ways to find the **ObjectID** of service principals.</span></span>    

<span data-ttu-id="570a8-218">You can use the portal, or you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span><span class="sxs-lookup"><span data-stu-id="570a8-218">You can use the portal, or you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="570a8-219">You can also go to the [Graph Explorer Tool](https://developer.microsoft.com/graph/graph-explorer) and sign in to your Azure AD account to see all your organization's service principals.</span><span class="sxs-lookup"><span data-stu-id="570a8-219">You can also go to the [Graph Explorer Tool](https://developer.microsoft.com/graph/graph-explorer) and sign in to your Azure AD account to see all your organization's service principals.</span></span> <span data-ttu-id="570a8-220">Because you are using PowerShell, you can use the get-AzureADServicePrincipal cmdlet to list the service principals and their IDs.</span><span class="sxs-lookup"><span data-stu-id="570a8-220">Because you are using PowerShell, you can use the get-AzureADServicePrincipal cmdlet to list the service principals and their IDs.</span></span>

#### <a name="step-3-assign-the-policy-to-your-service-principal"></a><span data-ttu-id="570a8-221">Step 3: Assign the policy to your service principal</span><span class="sxs-lookup"><span data-stu-id="570a8-221">Step 3: Assign the policy to your service principal</span></span>  
<span data-ttu-id="570a8-222">After you have the **ObjectID** of the service principal of the application for which you want to configure auto-acceleration, run the following command.</span><span class="sxs-lookup"><span data-stu-id="570a8-222">After you have the **ObjectID** of the service principal of the application for which you want to configure auto-acceleration, run the following command.</span></span> <span data-ttu-id="570a8-223">This command associates the HRD policy that you created in step 1 with the service principal that you located in step 2.</span><span class="sxs-lookup"><span data-stu-id="570a8-223">This command associates the HRD policy that you created in step 1 with the service principal that you located in step 2.</span></span>

``` powershell
Add-AzureADServicePrincipalPolicy -Id <ObjectID of the Service Principal> -RefObjectId <ObjectId of the Policy>
```

<span data-ttu-id="570a8-224">You can repeat this command for each service principal to which you want to add the policy.</span><span class="sxs-lookup"><span data-stu-id="570a8-224">You can repeat this command for each service principal to which you want to add the policy.</span></span>

<span data-ttu-id="570a8-225">In the case where an application already has a HomeRealmDiscovery policy assigned, you won’t be able to add a second one.</span><span class="sxs-lookup"><span data-stu-id="570a8-225">In the case where an application already has a HomeRealmDiscovery policy assigned, you won’t be able to add a second one.</span></span>  <span data-ttu-id="570a8-226">In that case, change the definition of the Home Realm Discovery policy that is assigned to the application to add additional parameters.</span><span class="sxs-lookup"><span data-stu-id="570a8-226">In that case, change the definition of the Home Realm Discovery policy that is assigned to the application to add additional parameters.</span></span>

#### <a name="step-4-check-which-application-service-principals-your-hrd-policy-is-assigned-to"></a><span data-ttu-id="570a8-227">Step 4: Check which application service principals your HRD policy is assigned to</span><span class="sxs-lookup"><span data-stu-id="570a8-227">Step 4: Check which application service principals your HRD policy is assigned to</span></span>
<span data-ttu-id="570a8-228">To check which applications have HRD policy configured, use the **Get-AzureADPolicyAppliedObject** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="570a8-228">To check which applications have HRD policy configured, use the **Get-AzureADPolicyAppliedObject** cmdlet.</span></span> <span data-ttu-id="570a8-229">Pass it the **ObjectID** of the policy that you want to check on.</span><span class="sxs-lookup"><span data-stu-id="570a8-229">Pass it the **ObjectID** of the policy that you want to check on.</span></span>

``` powershell
Get-AzureADPolicyAppliedObject -ObjectId <ObjectId of the Policy>
```
#### <a name="step-5-youre-done"></a><span data-ttu-id="570a8-230">Step 5: You're done!</span><span class="sxs-lookup"><span data-stu-id="570a8-230">Step 5: You're done!</span></span>
<span data-ttu-id="570a8-231">Try the application to check that the new policy is working.</span><span class="sxs-lookup"><span data-stu-id="570a8-231">Try the application to check that the new policy is working.</span></span>

### <a name="example-list-the-applications-for-which-hrd-policy-is-configured"></a><span data-ttu-id="570a8-232">Example: List the applications for which HRD policy is configured</span><span class="sxs-lookup"><span data-stu-id="570a8-232">Example: List the applications for which HRD policy is configured</span></span>

#### <a name="step-1-list-all-policies-that-were-created-in-your-organization"></a><span data-ttu-id="570a8-233">Step 1: List all policies that were created in your organization</span><span class="sxs-lookup"><span data-stu-id="570a8-233">Step 1: List all policies that were created in your organization</span></span> 

``` powershell
Get-AzureADPolicy
```

<span data-ttu-id="570a8-234">Note the **ObjectID** of the policy that you want to list assignments for.</span><span class="sxs-lookup"><span data-stu-id="570a8-234">Note the **ObjectID** of the policy that you want to list assignments for.</span></span>

#### <a name="step-2-list-the-service-principals-to-which-the-policy-is-assigned"></a><span data-ttu-id="570a8-235">Step 2: List the service principals to which the policy is assigned</span><span class="sxs-lookup"><span data-stu-id="570a8-235">Step 2: List the service principals to which the policy is assigned</span></span>  

``` powershell
Get-AzureADPolicyAppliedObject -ObjectId <ObjectId of the Policy>
```

### <a name="example-remove-an-hrd-policy-for-an-application"></a><span data-ttu-id="570a8-236">Example: Remove an HRD policy for an application</span><span class="sxs-lookup"><span data-stu-id="570a8-236">Example: Remove an HRD policy for an application</span></span>
#### <a name="step-1-get-the-objectid"></a><span data-ttu-id="570a8-237">Step 1: Get the ObjectID</span><span class="sxs-lookup"><span data-stu-id="570a8-237">Step 1: Get the ObjectID</span></span>
<span data-ttu-id="570a8-238">Use the previous example to get the **ObjectID** of the policy, and that of the application service principal from which you want to remove it.</span><span class="sxs-lookup"><span data-stu-id="570a8-238">Use the previous example to get the **ObjectID** of the policy, and that of the application service principal from which you want to remove it.</span></span> 

#### <a name="step-2-remove-the-policy-assignment-from-the-application-service-principal"></a><span data-ttu-id="570a8-239">Step 2: Remove the policy assignment from the application service principal</span><span class="sxs-lookup"><span data-stu-id="570a8-239">Step 2: Remove the policy assignment from the application service principal</span></span>  

``` powershell
Remove-AzureADApplicationPolicy -ObjectId <ObjectId of the Service Principal>  -PolicyId <ObjectId of the policy>
```

#### <a name="step-3-check-removal-by-listing-the-service-principals-to-which-the-policy-is-assigned"></a><span data-ttu-id="570a8-240">Step 3: Check removal by listing the service principals to which the policy is assigned</span><span class="sxs-lookup"><span data-stu-id="570a8-240">Step 3: Check removal by listing the service principals to which the policy is assigned</span></span> 

``` powershell
Get-AzureADPolicyAppliedObject -ObjectId <ObjectId of the Policy>
```
## <a name="next-steps"></a><span data-ttu-id="570a8-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="570a8-241">Next steps</span></span>
- <span data-ttu-id="570a8-242">For more information about how authentication works in Azure AD, see [Authentication scenarios for Azure AD](../develop/authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="570a8-242">For more information about how authentication works in Azure AD, see [Authentication scenarios for Azure AD](../develop/authentication-scenarios.md).</span></span>
- <span data-ttu-id="570a8-243">For more information about user single sign-on, see [Application access and single sign-on with Azure Active Directory](configure-single-sign-on-portal.md).</span><span class="sxs-lookup"><span data-stu-id="570a8-243">For more information about user single sign-on, see [Application access and single sign-on with Azure Active Directory](configure-single-sign-on-portal.md).</span></span>
- <span data-ttu-id="570a8-244">Visit the [Active Directory developer's guide](../develop/azure-ad-developers-guide.md) for an overview of all developer-related content.</span><span class="sxs-lookup"><span data-stu-id="570a8-244">Visit the [Active Directory developer's guide](../develop/azure-ad-developers-guide.md) for an overview of all developer-related content.</span></span>
