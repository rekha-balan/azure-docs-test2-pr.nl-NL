---
title: What are conditions in Azure Active Directory conditional access? | Microsoft Docs
description: Learn how conditions are used in Azure Active Directory conditional access to trigger a policy.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/13/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9feb6ef5b708813c2f73a70a930cabfd69dff114
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871295"
---
# <a name="what-are-conditions-in-azure-active-directory-conditional-access"></a><span data-ttu-id="0ef1e-105">What are conditions in Azure Active Directory conditional access?</span><span class="sxs-lookup"><span data-stu-id="0ef1e-105">What are conditions in Azure Active Directory conditional access?</span></span> 

<span data-ttu-id="0ef1e-106">You can control how authorized users access your cloud apps by using [Azure Active Directory (Azure AD) conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-106">You can control how authorized users access your cloud apps by using [Azure Active Directory (Azure AD) conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).</span></span> <span data-ttu-id="0ef1e-107">In a conditional access policy, you define the response ("Then do this") to the reason for triggering your policy ("When this happens").</span><span class="sxs-lookup"><span data-stu-id="0ef1e-107">In a conditional access policy, you define the response ("Then do this") to the reason for triggering your policy ("When this happens").</span></span> 

![Reason and response](./media/conditions/10.png)


<span data-ttu-id="0ef1e-109">In the context of conditional access, **When this happens** is called a **condition**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-109">In the context of conditional access, **When this happens** is called a **condition**.</span></span> <span data-ttu-id="0ef1e-110">**Then do this** is called an **access control**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-110">**Then do this** is called an **access control**.</span></span> <span data-ttu-id="0ef1e-111">The combination of your conditions and your access controls represents a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-111">The combination of your conditions and your access controls represents a conditional access policy.</span></span>

![Conditional access policy](./media/conditions/61.png)


<span data-ttu-id="0ef1e-113">Conditions you haven't configured in a conditional access policy aren't applied.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-113">Conditions you haven't configured in a conditional access policy aren't applied.</span></span> <span data-ttu-id="0ef1e-114">Some conditions are [mandatory](best-practices.md) to apply a conditional access policy to an environment.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-114">Some conditions are [mandatory](best-practices.md) to apply a conditional access policy to an environment.</span></span> 

<span data-ttu-id="0ef1e-115">This article is an overview of the conditions and how they're used in a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-115">This article is an overview of the conditions and how they're used in a conditional access policy.</span></span> 

## <a name="users-and-groups"></a><span data-ttu-id="0ef1e-116">Users and groups</span><span class="sxs-lookup"><span data-stu-id="0ef1e-116">Users and groups</span></span>

<span data-ttu-id="0ef1e-117">The users and groups condition is mandatory in a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-117">The users and groups condition is mandatory in a conditional access policy.</span></span> <span data-ttu-id="0ef1e-118">In your policy, you can either select **All users** or select specific users and groups.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-118">In your policy, you can either select **All users** or select specific users and groups.</span></span>

![Users and groups](./media/conditions/111.png)

<span data-ttu-id="0ef1e-120">When you select **All users**, your policy is applied to all users in the directory, including guest users.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-120">When you select **All users**, your policy is applied to all users in the directory, including guest users.</span></span>

<span data-ttu-id="0ef1e-121">When you **Select users and groups**, you can set the following options:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-121">When you **Select users and groups**, you can set the following options:</span></span>

* <span data-ttu-id="0ef1e-122">**All guest users** targets a policy to B2B guest users.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-122">**All guest users** targets a policy to B2B guest users.</span></span> <span data-ttu-id="0ef1e-123">This condition matches any user account that has the **userType** attribute set to **guest**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-123">This condition matches any user account that has the **userType** attribute set to **guest**.</span></span> <span data-ttu-id="0ef1e-124">You can use this setting when a policy needs to be applied as soon as the account is created in an invite flow in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-124">You can use this setting when a policy needs to be applied as soon as the account is created in an invite flow in Azure AD.</span></span>

* <span data-ttu-id="0ef1e-125">**Directory roles** targets a policy based on a user’s role assignment.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-125">**Directory roles** targets a policy based on a user’s role assignment.</span></span> <span data-ttu-id="0ef1e-126">This condition supports directory roles like **Global administrator** or **Password administrator**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-126">This condition supports directory roles like **Global administrator** or **Password administrator**.</span></span>

* <span data-ttu-id="0ef1e-127">**Users and groups** targets specific sets of users.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-127">**Users and groups** targets specific sets of users.</span></span> <span data-ttu-id="0ef1e-128">For example, you can select a group that contains all members of the HR department when an HR app is selected as the cloud app.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-128">For example, you can select a group that contains all members of the HR department when an HR app is selected as the cloud app.</span></span> <span data-ttu-id="0ef1e-129">A group can be any type of group in Azure AD, including dynamic or assigned security and distribution groups.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-129">A group can be any type of group in Azure AD, including dynamic or assigned security and distribution groups.</span></span>

<span data-ttu-id="0ef1e-130">You can also exclude specific users or groups from a policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-130">You can also exclude specific users or groups from a policy.</span></span> <span data-ttu-id="0ef1e-131">One common use case is service accounts if your policy enforces multifactor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-131">One common use case is service accounts if your policy enforces multifactor authentication (MFA).</span></span> 

<span data-ttu-id="0ef1e-132">Targeting specific sets of users is useful for the deployment of a new policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-132">Targeting specific sets of users is useful for the deployment of a new policy.</span></span> <span data-ttu-id="0ef1e-133">In a new policy, you should target only an initial set of users to validate the policy behavior.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-133">In a new policy, you should target only an initial set of users to validate the policy behavior.</span></span> 



## <a name="cloud-apps"></a><span data-ttu-id="0ef1e-134">Cloud apps</span><span class="sxs-lookup"><span data-stu-id="0ef1e-134">Cloud apps</span></span> 

<span data-ttu-id="0ef1e-135">A cloud app is a website or service.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-135">A cloud app is a website or service.</span></span> <span data-ttu-id="0ef1e-136">Websites protected by the Azure AD Application Proxy are also cloud apps.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-136">Websites protected by the Azure AD Application Proxy are also cloud apps.</span></span> <span data-ttu-id="0ef1e-137">For a detailed description of supported cloud apps, see [cloud apps assignments](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#cloud-apps-assignments).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-137">For a detailed description of supported cloud apps, see [cloud apps assignments](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#cloud-apps-assignments).</span></span> 

<span data-ttu-id="0ef1e-138">The **cloud apps** condition is mandatory in a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-138">The **cloud apps** condition is mandatory in a conditional access policy.</span></span> <span data-ttu-id="0ef1e-139">In your policy, you can either select **All cloud apps** or select specific apps.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-139">In your policy, you can either select **All cloud apps** or select specific apps.</span></span>

![Include cloud apps](./media/conditions/03.png)

<span data-ttu-id="0ef1e-141">Select:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-141">Select:</span></span>

- <span data-ttu-id="0ef1e-142">**All cloud apps** to baseline policies to apply to the entire organization.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-142">**All cloud apps** to baseline policies to apply to the entire organization.</span></span> <span data-ttu-id="0ef1e-143">Use this selection for policies that require multifactor authentication when sign-in risk is detected for any cloud app.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-143">Use this selection for policies that require multifactor authentication when sign-in risk is detected for any cloud app.</span></span> <span data-ttu-id="0ef1e-144">A policy applied to **All cloud apps** applies to access to all websites and services.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-144">A policy applied to **All cloud apps** applies to access to all websites and services.</span></span> <span data-ttu-id="0ef1e-145">This setting isn't limited to the cloud apps that appear on the **Select apps** list.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-145">This setting isn't limited to the cloud apps that appear on the **Select apps** list.</span></span> 

- <span data-ttu-id="0ef1e-146">Individual cloud apps to target specific services by policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-146">Individual cloud apps to target specific services by policy.</span></span> <span data-ttu-id="0ef1e-147">For example, you can require users to have a [compliant device](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online) to access SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-147">For example, you can require users to have a [compliant device](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online) to access SharePoint Online.</span></span> <span data-ttu-id="0ef1e-148">This policy is also applied to other services when they access SharePoint content.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-148">This policy is also applied to other services when they access SharePoint content.</span></span> <span data-ttu-id="0ef1e-149">An example is Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-149">An example is Microsoft Teams.</span></span> 

<span data-ttu-id="0ef1e-150">You can exclude specific apps from a policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-150">You can exclude specific apps from a policy.</span></span> <span data-ttu-id="0ef1e-151">However, these apps are still subject to the policies applied to the services they access.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-151">However, these apps are still subject to the policies applied to the services they access.</span></span> 



## <a name="sign-in-risk"></a><span data-ttu-id="0ef1e-152">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="0ef1e-152">Sign-in risk</span></span>

<span data-ttu-id="0ef1e-153">A sign-in risk is an indicator of the likelihood (high, medium, or low) that a sign-in attempt wasn't made by the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-153">A sign-in risk is an indicator of the likelihood (high, medium, or low) that a sign-in attempt wasn't made by the legitimate owner of a user account.</span></span> <span data-ttu-id="0ef1e-154">Azure AD calculates the sign-in risk level during a user's sign-in.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-154">Azure AD calculates the sign-in risk level during a user's sign-in.</span></span> <span data-ttu-id="0ef1e-155">You can use the calculated sign-in risk level as condition in a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-155">You can use the calculated sign-in risk level as condition in a conditional access policy.</span></span>

![Sign-in risk levels](./media/conditions/22.png)

<span data-ttu-id="0ef1e-157">To use this condition, you need to have [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable) enabled.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-157">To use this condition, you need to have [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable) enabled.</span></span>
 
<span data-ttu-id="0ef1e-158">Common use cases for this condition are policies that have the following protections:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-158">Common use cases for this condition are policies that have the following protections:</span></span> 

- <span data-ttu-id="0ef1e-159">Block users with a high sign-in risk.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-159">Block users with a high sign-in risk.</span></span> <span data-ttu-id="0ef1e-160">This protection prevents potentially non-legitimate users from accessing your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-160">This protection prevents potentially non-legitimate users from accessing your cloud apps.</span></span> 
- <span data-ttu-id="0ef1e-161">Require multifactor authentication for users with a medium sign-in risk.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-161">Require multifactor authentication for users with a medium sign-in risk.</span></span> <span data-ttu-id="0ef1e-162">By enforcing multifactor authentication, you can provide additional confidence that the sign-in is done by the legitimate owner of an account.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-162">By enforcing multifactor authentication, you can provide additional confidence that the sign-in is done by the legitimate owner of an account.</span></span>

<span data-ttu-id="0ef1e-163">For more information, see [Risky sign-ins](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-163">For more information, see [Risky sign-ins](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).</span></span>  

## <a name="device-platforms"></a><span data-ttu-id="0ef1e-164">Device platforms</span><span class="sxs-lookup"><span data-stu-id="0ef1e-164">Device platforms</span></span>

<span data-ttu-id="0ef1e-165">The device platform is characterized by the operating system that runs on your device.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-165">The device platform is characterized by the operating system that runs on your device.</span></span> <span data-ttu-id="0ef1e-166">Azure AD identifies the platform by using information provided by the device, such as user agent.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-166">Azure AD identifies the platform by using information provided by the device, such as user agent.</span></span> <span data-ttu-id="0ef1e-167">This information is unverified.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-167">This information is unverified.</span></span> <span data-ttu-id="0ef1e-168">We recommend that all platforms have a policy applied to them.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-168">We recommend that all platforms have a policy applied to them.</span></span> <span data-ttu-id="0ef1e-169">The policy should either block access, require compliance with Microsoft Intune policies, or require the device be domain joined.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-169">The policy should either block access, require compliance with Microsoft Intune policies, or require the device be domain joined.</span></span> <span data-ttu-id="0ef1e-170">The default is to apply a policy to all device platforms.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-170">The default is to apply a policy to all device platforms.</span></span> 


![Configure device platforms](./media/conditions/24.png)

<span data-ttu-id="0ef1e-172">For a list of the supported device platforms, see [device platform condition](technical-reference.md#device-platform-condition).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-172">For a list of the supported device platforms, see [device platform condition](technical-reference.md#device-platform-condition).</span></span>


<span data-ttu-id="0ef1e-173">A common use case for this condition is a policy that restricts access to your cloud apps to [managed devices](require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-173">A common use case for this condition is a policy that restricts access to your cloud apps to [managed devices](require-managed-devices.md).</span></span> <span data-ttu-id="0ef1e-174">For more scenarios including the device platform condition, see [Azure Active Directory app-based conditional access](app-based-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-174">For more scenarios including the device platform condition, see [Azure Active Directory app-based conditional access](app-based-conditional-access.md).</span></span>



## <a name="device-state"></a><span data-ttu-id="0ef1e-175">Device state</span><span class="sxs-lookup"><span data-stu-id="0ef1e-175">Device state</span></span>

<span data-ttu-id="0ef1e-176">The device state condition excludes hybrid Azure AD joined devices and devices marked as compliant from a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-176">The device state condition excludes hybrid Azure AD joined devices and devices marked as compliant from a conditional access policy.</span></span> <span data-ttu-id="0ef1e-177">This condition is useful when a policy should apply only to an unmanaged device to provide additional session security.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-177">This condition is useful when a policy should apply only to an unmanaged device to provide additional session security.</span></span> <span data-ttu-id="0ef1e-178">For example, only enforce the Microsoft Cloud App Security session control when a device is unmanaged.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-178">For example, only enforce the Microsoft Cloud App Security session control when a device is unmanaged.</span></span> 


![Configure device state](./media/conditions/112.png)

<span data-ttu-id="0ef1e-180">If you want to block access for unmanaged devices, implement [device-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-180">If you want to block access for unmanaged devices, implement [device-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online).</span></span>


## <a name="locations"></a><span data-ttu-id="0ef1e-181">Locations</span><span class="sxs-lookup"><span data-stu-id="0ef1e-181">Locations</span></span>

<span data-ttu-id="0ef1e-182">By using locations, you can define conditions based on where a connection was attempted.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-182">By using locations, you can define conditions based on where a connection was attempted.</span></span> 

![Configure locations](./media/conditions/25.png)

<span data-ttu-id="0ef1e-184">Common use cases for this condition are policies with the following protections:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-184">Common use cases for this condition are policies with the following protections:</span></span>

- <span data-ttu-id="0ef1e-185">Require multifactor authentication for users accessing a service when they're off the corporate network.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-185">Require multifactor authentication for users accessing a service when they're off the corporate network.</span></span>  

- <span data-ttu-id="0ef1e-186">Block access for users accessing a service from specific countries or regions.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-186">Block access for users accessing a service from specific countries or regions.</span></span> 

<span data-ttu-id="0ef1e-187">For more information, see [What is the location condition in Azure Active Directory conditional access?](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-locations).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-187">For more information, see [What is the location condition in Azure Active Directory conditional access?](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-locations).</span></span>


## <a name="client-apps"></a><span data-ttu-id="0ef1e-188">Client apps</span><span class="sxs-lookup"><span data-stu-id="0ef1e-188">Client apps</span></span>

<span data-ttu-id="0ef1e-189">By using the client apps condition, you can apply a policy to different types of applications.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-189">By using the client apps condition, you can apply a policy to different types of applications.</span></span> <span data-ttu-id="0ef1e-190">Examples are websites,services, mobile apps, and desktop applications.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-190">Examples are websites,services, mobile apps, and desktop applications.</span></span> 



<span data-ttu-id="0ef1e-191">An application is classified as follows:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-191">An application is classified as follows:</span></span>

- <span data-ttu-id="0ef1e-192">A website or service if it uses web SSO protocols, SAML, WS-Fed, or OpenID Connect for a confidential client.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-192">A website or service if it uses web SSO protocols, SAML, WS-Fed, or OpenID Connect for a confidential client.</span></span>

- <span data-ttu-id="0ef1e-193">A mobile app or desktop application if it uses the mobile app OpenID Connect for a native client.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-193">A mobile app or desktop application if it uses the mobile app OpenID Connect for a native client.</span></span>

<span data-ttu-id="0ef1e-194">For a list of the client apps you can use in your conditional access policy, see [Client apps condition](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#client-apps-condition) in the Azure Active Directory Conditional Access technical reference.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-194">For a list of the client apps you can use in your conditional access policy, see [Client apps condition](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference#client-apps-condition) in the Azure Active Directory Conditional Access technical reference.</span></span>

<span data-ttu-id="0ef1e-195">Common use cases for this condition are policies with the following protections:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-195">Common use cases for this condition are policies with the following protections:</span></span> 

- <span data-ttu-id="0ef1e-196">Require a [compliant device](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online) for mobile and desktop applications that download large amounts of data to the device.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-196">Require a [compliant device](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online) for mobile and desktop applications that download large amounts of data to the device.</span></span> <span data-ttu-id="0ef1e-197">At the same time, allow browser access from any device.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-197">At the same time, allow browser access from any device.</span></span>

- <span data-ttu-id="0ef1e-198">Block access from web applications but allow access from mobile and desktop applications.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-198">Block access from web applications but allow access from mobile and desktop applications.</span></span>

<span data-ttu-id="0ef1e-199">You can apply this condition to web SSO and modern authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-199">You can apply this condition to web SSO and modern authentication protocols.</span></span> <span data-ttu-id="0ef1e-200">You can also apply it to mail applications that use Microsoft Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-200">You can also apply it to mail applications that use Microsoft Exchange ActiveSync.</span></span> <span data-ttu-id="0ef1e-201">Examples are the native mail apps on most smartphones.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-201">Examples are the native mail apps on most smartphones.</span></span> 

<span data-ttu-id="0ef1e-202">You can only select the client apps condition if Microsoft Office 365 Exchange Online is the only cloud app you've selected.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-202">You can only select the client apps condition if Microsoft Office 365 Exchange Online is the only cloud app you've selected.</span></span>

![Cloud apps](./media/conditions/32.png)

<span data-ttu-id="0ef1e-204">Selecting **Exchange ActiveSync** as a client apps condition is supported only if you don't have other conditions  configured in a policy.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-204">Selecting **Exchange ActiveSync** as a client apps condition is supported only if you don't have other conditions  configured in a policy.</span></span> <span data-ttu-id="0ef1e-205">However, you can narrow down the scope of this condition to apply only to supported platforms.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-205">However, you can narrow down the scope of this condition to apply only to supported platforms.</span></span>

 
![Apply policy only to supported platforms](./media/conditions/33.png)

<span data-ttu-id="0ef1e-207">Applying this condition only to supported platforms is equal to all device platforms in a [device platform condition](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-207">Applying this condition only to supported platforms is equal to all device platforms in a [device platform condition](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online).</span></span>

![Configure device platforms](./media/conditions/34.png)


 <span data-ttu-id="0ef1e-209">For more information, see these articles:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-209">For more information, see these articles:</span></span>

- <span data-ttu-id="0ef1e-210">[Set up SharePoint Online and Exchange Online for Azure Active Directory conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-no-modern-authentication).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-210">[Set up SharePoint Online and Exchange Online for Azure Active Directory conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-no-modern-authentication).</span></span>
 
- <span data-ttu-id="0ef1e-211">[Azure Active Directory app-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-211">[Azure Active Directory app-based conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).</span></span> 


### <a name="legacy-authentication"></a><span data-ttu-id="0ef1e-212">Legacy authentication</span><span class="sxs-lookup"><span data-stu-id="0ef1e-212">Legacy authentication</span></span>  

<span data-ttu-id="0ef1e-213">Conditional access now applies to older Microsoft Office clients that don't support modern authentication.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-213">Conditional access now applies to older Microsoft Office clients that don't support modern authentication.</span></span> <span data-ttu-id="0ef1e-214">It also applies to clients that use mail protocols like POP, IMAP, and SMTP.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-214">It also applies to clients that use mail protocols like POP, IMAP, and SMTP.</span></span> <span data-ttu-id="0ef1e-215">By using legacy authentication, you can configure policies like **block access from other clients**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-215">By using legacy authentication, you can configure policies like **block access from other clients**.</span></span>


![Configure client apps](./media/conditions/160.png)  


#### <a name="known-issues"></a><span data-ttu-id="0ef1e-217">Known issues</span><span class="sxs-lookup"><span data-stu-id="0ef1e-217">Known issues</span></span>

- <span data-ttu-id="0ef1e-218">Configuring a policy for **Other clients** blocks the entire organization from certain clients like SPConnect.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-218">Configuring a policy for **Other clients** blocks the entire organization from certain clients like SPConnect.</span></span> <span data-ttu-id="0ef1e-219">This block happens because older clients authenticate in unexpected ways.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-219">This block happens because older clients authenticate in unexpected ways.</span></span> <span data-ttu-id="0ef1e-220">The issue doesn't apply to major Office applications like the older Office clients.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-220">The issue doesn't apply to major Office applications like the older Office clients.</span></span> 

- <span data-ttu-id="0ef1e-221">It can take up to 24 hours for the policy to go into effect.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-221">It can take up to 24 hours for the policy to go into effect.</span></span> 


#### <a name="frequently-asked-questions"></a><span data-ttu-id="0ef1e-222">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="0ef1e-222">Frequently asked questions</span></span>

<span data-ttu-id="0ef1e-223">**Q:** Will this authentication block Microsoft Exchange Web Services?</span><span class="sxs-lookup"><span data-stu-id="0ef1e-223">**Q:** Will this authentication block Microsoft Exchange Web Services?</span></span>

<span data-ttu-id="0ef1e-224">It depends on the authentication protocol that Exchange Web Services uses.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-224">It depends on the authentication protocol that Exchange Web Services uses.</span></span> <span data-ttu-id="0ef1e-225">If the Exchange Web Services application uses modern authentication, it's covered by the **Mobile apps and desktop clients** client app.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-225">If the Exchange Web Services application uses modern authentication, it's covered by the **Mobile apps and desktop clients** client app.</span></span> <span data-ttu-id="0ef1e-226">Basic authentication is covered by the **Other clients** client app.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-226">Basic authentication is covered by the **Other clients** client app.</span></span>


<span data-ttu-id="0ef1e-227">**Q:** What controls can I use for **Other clients**?</span><span class="sxs-lookup"><span data-stu-id="0ef1e-227">**Q:** What controls can I use for **Other clients**?</span></span>

<span data-ttu-id="0ef1e-228">Any control can be configured for **Other clients**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-228">Any control can be configured for **Other clients**.</span></span> <span data-ttu-id="0ef1e-229">However, the end-user experience will be blocked access for all cases.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-229">However, the end-user experience will be blocked access for all cases.</span></span> <span data-ttu-id="0ef1e-230">**Other clients** don't support controls like MFA, compliant device, and domain join.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-230">**Other clients** don't support controls like MFA, compliant device, and domain join.</span></span> 
 
<span data-ttu-id="0ef1e-231">**Q:** What conditions can I use for **Other clients**?</span><span class="sxs-lookup"><span data-stu-id="0ef1e-231">**Q:** What conditions can I use for **Other clients**?</span></span>

<span data-ttu-id="0ef1e-232">Any condition can be configured for **Other clients**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-232">Any condition can be configured for **Other clients**.</span></span>

<span data-ttu-id="0ef1e-233">**Q:** Does Exchange ActiveSync support all conditions and controls?</span><span class="sxs-lookup"><span data-stu-id="0ef1e-233">**Q:** Does Exchange ActiveSync support all conditions and controls?</span></span>

<span data-ttu-id="0ef1e-234">No.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-234">No.</span></span> <span data-ttu-id="0ef1e-235">The following list summarizes Exchange ActiveSync support:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-235">The following list summarizes Exchange ActiveSync support:</span></span> 

- <span data-ttu-id="0ef1e-236">Exchange ActiveSync supports only user and group targeting.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-236">Exchange ActiveSync supports only user and group targeting.</span></span> <span data-ttu-id="0ef1e-237">It doesn’t support guests or roles.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-237">It doesn’t support guests or roles.</span></span> <span data-ttu-id="0ef1e-238">If a guest or role condition is configured, all users are blocked.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-238">If a guest or role condition is configured, all users are blocked.</span></span> <span data-ttu-id="0ef1e-239">Exchange ActiveSync blocks all users because it can't determine if the policy should apply to the user or not.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-239">Exchange ActiveSync blocks all users because it can't determine if the policy should apply to the user or not.</span></span>

- <span data-ttu-id="0ef1e-240">Exchange ActiveSync works only with Microsoft Exchange Online as the cloud app.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-240">Exchange ActiveSync works only with Microsoft Exchange Online as the cloud app.</span></span> 

- <span data-ttu-id="0ef1e-241">Exchange ActiveSync doesn't support any condition except the client app itself.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-241">Exchange ActiveSync doesn't support any condition except the client app itself.</span></span> 

- <span data-ttu-id="0ef1e-242">Exchange ActiveSync can be configured with any control.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-242">Exchange ActiveSync can be configured with any control.</span></span> <span data-ttu-id="0ef1e-243">All controls except device compliance lead to a block.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-243">All controls except device compliance lead to a block.</span></span>

<span data-ttu-id="0ef1e-244">**Q:** Do the policies apply to all client apps by default going forward?</span><span class="sxs-lookup"><span data-stu-id="0ef1e-244">**Q:** Do the policies apply to all client apps by default going forward?</span></span>

<span data-ttu-id="0ef1e-245">No.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-245">No.</span></span> <span data-ttu-id="0ef1e-246">There's no change in the default policy behavior.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-246">There's no change in the default policy behavior.</span></span> <span data-ttu-id="0ef1e-247">The policies continue to apply to browser and mobile applications and desktop clients by default.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-247">The policies continue to apply to browser and mobile applications and desktop clients by default.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0ef1e-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ef1e-248">Next steps</span></span>

- <span data-ttu-id="0ef1e-249">To find out how to configure a conditional access policy, see [Quickstart: Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-249">To find out how to configure a conditional access policy, see [Quickstart: Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

- <span data-ttu-id="0ef1e-250">To configure conditional access policies for your environment, see the [Best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-250">To configure conditional access policies for your environment, see the [Best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 

