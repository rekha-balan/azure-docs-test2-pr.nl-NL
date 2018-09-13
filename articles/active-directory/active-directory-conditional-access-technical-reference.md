---
title: Azure Active Directory Conditional Access technical reference | Microsoft Docs
description: With Conditional access control, Azure Active Directory checks the specific conditions you pick when authenticating the user and before allowing access to the application. Once those conditions are met, the user is authenticated and allowed access to the application.
services: active-directory.
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/28/2017
ms.author: markvi
ms.openlocfilehash: 734491c1cd929de27dc166692f6893b2c2f2fdfe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551209"
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="1c401-104">Azure Active Directory Conditional Access technical reference</span><span class="sxs-lookup"><span data-stu-id="1c401-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="1c401-105">Services enabled with conditional access</span><span class="sxs-lookup"><span data-stu-id="1c401-105">Services enabled with conditional access</span></span>

<span data-ttu-id="1c401-106">Conditional Access rules are supported across various Azure AD application types.</span><span class="sxs-lookup"><span data-stu-id="1c401-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="1c401-107">This list includes:</span><span class="sxs-lookup"><span data-stu-id="1c401-107">This list includes:</span></span>


* <span data-ttu-id="1c401-108">Applications registered with the Azure Application Proxy</span><span class="sxs-lookup"><span data-stu-id="1c401-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="1c401-109">Azure Remote App</span><span class="sxs-lookup"><span data-stu-id="1c401-109">Azure Remote App</span></span>
* <span data-ttu-id="1c401-110">Developed line of business and multi-tenant applications registered with Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c401-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="1c401-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="1c401-111">Dynamics CRM</span></span>
* <span data-ttu-id="1c401-112">Federated applications from the Azure AD application gallery</span><span class="sxs-lookup"><span data-stu-id="1c401-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="1c401-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="1c401-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="1c401-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="1c401-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="1c401-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span><span class="sxs-lookup"><span data-stu-id="1c401-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="1c401-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="1c401-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="1c401-117">Password SSO applications from the Azure AD application gallery</span><span class="sxs-lookup"><span data-stu-id="1c401-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="1c401-118">Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="1c401-118">Visual Studio Online</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="1c401-119">Enable access rules</span><span class="sxs-lookup"><span data-stu-id="1c401-119">Enable access rules</span></span>
<span data-ttu-id="1c401-120">Each rule can be enabled or disabled on a per application bases.</span><span class="sxs-lookup"><span data-stu-id="1c401-120">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="1c401-121">When rules are **ON** they will be enabled and enforced for users accessing the application.</span><span class="sxs-lookup"><span data-stu-id="1c401-121">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="1c401-122">When they are **OFF** they will not be used and will not impact the users sign in experience.</span><span class="sxs-lookup"><span data-stu-id="1c401-122">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="1c401-123">Applying rules to specific users</span><span class="sxs-lookup"><span data-stu-id="1c401-123">Applying rules to specific users</span></span>
<span data-ttu-id="1c401-124">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span><span class="sxs-lookup"><span data-stu-id="1c401-124">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="1c401-125">**Apply To** can be set to **All Users** or **Groups**.</span><span class="sxs-lookup"><span data-stu-id="1c401-125">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="1c401-126">When set to **All Users** the rules will apply to any user with access to the application.</span><span class="sxs-lookup"><span data-stu-id="1c401-126">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="1c401-127">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span><span class="sxs-lookup"><span data-stu-id="1c401-127">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="1c401-128">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span><span class="sxs-lookup"><span data-stu-id="1c401-128">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="1c401-129">Once complete the rule can be applied to **All Users**.</span><span class="sxs-lookup"><span data-stu-id="1c401-129">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="1c401-130">This will cause the rule to be enforced for all users in the organization.</span><span class="sxs-lookup"><span data-stu-id="1c401-130">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="1c401-131">Select groups may also be exempted from policy using the **Except** option.</span><span class="sxs-lookup"><span data-stu-id="1c401-131">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="1c401-132">Any members of these groups will be exempted even if they appear in an included group.</span><span class="sxs-lookup"><span data-stu-id="1c401-132">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="1c401-133">“At work” networks</span><span class="sxs-lookup"><span data-stu-id="1c401-133">“At work” networks</span></span>
<span data-ttu-id="1c401-134">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span><span class="sxs-lookup"><span data-stu-id="1c401-134">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="1c401-135">These rules include:</span><span class="sxs-lookup"><span data-stu-id="1c401-135">These rules include:</span></span>

* <span data-ttu-id="1c401-136">Require multi-factor authentication when not at work</span><span class="sxs-lookup"><span data-stu-id="1c401-136">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="1c401-137">Block access when not at work</span><span class="sxs-lookup"><span data-stu-id="1c401-137">Block access when not at work</span></span>

<span data-ttu-id="1c401-138">Options for specifiying “at work” networks</span><span class="sxs-lookup"><span data-stu-id="1c401-138">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="1c401-139">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="1c401-139">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="1c401-140">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span><span class="sxs-lookup"><span data-stu-id="1c401-140">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="1c401-141">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span><span class="sxs-lookup"><span data-stu-id="1c401-141">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="1c401-142">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="1c401-142">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="1c401-143">Rules based on application sensitivity</span><span class="sxs-lookup"><span data-stu-id="1c401-143">Rules based on application sensitivity</span></span>
<span data-ttu-id="1c401-144">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span><span class="sxs-lookup"><span data-stu-id="1c401-144">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="1c401-145">Conditional access rules can be configured on the  **Configure** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="1c401-145">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="1c401-146">Rules currently offered:</span><span class="sxs-lookup"><span data-stu-id="1c401-146">Rules currently offered:</span></span>

* <span data-ttu-id="1c401-147">**Require multi-factor authentication**</span><span class="sxs-lookup"><span data-stu-id="1c401-147">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="1c401-148">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span><span class="sxs-lookup"><span data-stu-id="1c401-148">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="1c401-149">**Require multi-factor authentication when not at work**</span><span class="sxs-lookup"><span data-stu-id="1c401-149">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="1c401-150">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span><span class="sxs-lookup"><span data-stu-id="1c401-150">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="1c401-151">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span><span class="sxs-lookup"><span data-stu-id="1c401-151">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="1c401-152">**Block access when not at work**</span><span class="sxs-lookup"><span data-stu-id="1c401-152">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="1c401-153">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span><span class="sxs-lookup"><span data-stu-id="1c401-153">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="1c401-154">They will be re-allowed access when at a work location.</span><span class="sxs-lookup"><span data-stu-id="1c401-154">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="1c401-155">Related topics</span><span class="sxs-lookup"><span data-stu-id="1c401-155">Related topics</span></span>
* [<span data-ttu-id="1c401-156">Securing access to Office 365 and other apps connected to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c401-156">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="1c401-157">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c401-157">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

