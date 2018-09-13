---
title: What is the location conditions in Azure Active Directory conditional access? | Microsoft Docs
description: Learn how to use the location condition to control access to your cloud apps based on a user's network location.
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
ms.openlocfilehash: eeb12500a5ddfb95317b3d20b41acf12e3978bad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866453"
---
# <a name="what-is-the-location-condition-in-azure-active-directory-conditional-access"></a><span data-ttu-id="7ede7-105">What is the location condition in Azure Active Directory conditional access?</span><span class="sxs-lookup"><span data-stu-id="7ede7-105">What is the location condition in Azure Active Directory conditional access?</span></span> 

<span data-ttu-id="7ede7-106">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users can access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="7ede7-106">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users can access your cloud apps.</span></span> <span data-ttu-id="7ede7-107">The location condition of a conditional access policy enables you to tie access controls settings to the network locations of your users.</span><span class="sxs-lookup"><span data-stu-id="7ede7-107">The location condition of a conditional access policy enables you to tie access controls settings to the network locations of your users.</span></span>

<span data-ttu-id="7ede7-108">This article provides you with the information you need to configure the location condition.</span><span class="sxs-lookup"><span data-stu-id="7ede7-108">This article provides you with the information you need to configure the location condition.</span></span> 

## <a name="locations"></a><span data-ttu-id="7ede7-109">Locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-109">Locations</span></span>

<span data-ttu-id="7ede7-110">Azure AD enables single sign on to devices, apps, and services from anywhere on the public internet.</span><span class="sxs-lookup"><span data-stu-id="7ede7-110">Azure AD enables single sign on to devices, apps, and services from anywhere on the public internet.</span></span> <span data-ttu-id="7ede7-111">With the location condition, you can control access to your cloud apps based on the network location of a user.</span><span class="sxs-lookup"><span data-stu-id="7ede7-111">With the location condition, you can control access to your cloud apps based on the network location of a user.</span></span> <span data-ttu-id="7ede7-112">Common use cases for the location condition are:</span><span class="sxs-lookup"><span data-stu-id="7ede7-112">Common use cases for the location condition are:</span></span>

- <span data-ttu-id="7ede7-113">Requiring multi-factor authentication for users accessing a service when they are off the corporate network</span><span class="sxs-lookup"><span data-stu-id="7ede7-113">Requiring multi-factor authentication for users accessing a service when they are off the corporate network</span></span>  

- <span data-ttu-id="7ede7-114">Blocking access for users accessing a service from specific countries or regions.</span><span class="sxs-lookup"><span data-stu-id="7ede7-114">Blocking access for users accessing a service from specific countries or regions.</span></span> 

<span data-ttu-id="7ede7-115">A location is a label for a network location that either represents a named location or multi-factor authentication trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="7ede7-115">A location is a label for a network location that either represents a named location or multi-factor authentication trusted IPs.</span></span>


## <a name="named-locations"></a><span data-ttu-id="7ede7-116">Named locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-116">Named locations</span></span> 

<span data-ttu-id="7ede7-117">With named locations, you can create logical groupings of IP address ranges, countries and regions.</span><span class="sxs-lookup"><span data-stu-id="7ede7-117">With named locations, you can create logical groupings of IP address ranges, countries and regions.</span></span> 

<span data-ttu-id="7ede7-118">You can access your named locations in the **Manage** section of the conditional access page.</span><span class="sxs-lookup"><span data-stu-id="7ede7-118">You can access your named locations in the **Manage** section of the conditional access page.</span></span>

![Locations](./media/location-condition/02.png)

 


<span data-ttu-id="7ede7-120">A named location has the following components:</span><span class="sxs-lookup"><span data-stu-id="7ede7-120">A named location has the following components:</span></span>

![Locations](./media/location-condition/42.png)

- <span data-ttu-id="7ede7-122">**Name** - The display name of a named location.</span><span class="sxs-lookup"><span data-stu-id="7ede7-122">**Name** - The display name of a named location.</span></span>

- <span data-ttu-id="7ede7-123">**IP ranges** - One or more IP address ranges in CIDR format.</span><span class="sxs-lookup"><span data-stu-id="7ede7-123">**IP ranges** - One or more IP address ranges in CIDR format.</span></span>

- <span data-ttu-id="7ede7-124">**Mark as trusted location** - A flag you can set for a named location to indicate a trusted location.</span><span class="sxs-lookup"><span data-stu-id="7ede7-124">**Mark as trusted location** - A flag you can set for a named location to indicate a trusted location.</span></span> <span data-ttu-id="7ede7-125">Typically, trusted locations are network areas that are controlled by your IT department.</span><span class="sxs-lookup"><span data-stu-id="7ede7-125">Typically, trusted locations are network areas that are controlled by your IT department.</span></span> <span data-ttu-id="7ede7-126">In addition to conditional access, trusted named locations are also used by Azure Identity Protection and Azure AD security reports to reduce [false positives](../reports-monitoring/concept-risk-events.md#impossible-travel-to-atypical-locations-1).</span><span class="sxs-lookup"><span data-stu-id="7ede7-126">In addition to conditional access, trusted named locations are also used by Azure Identity Protection and Azure AD security reports to reduce [false positives](../reports-monitoring/concept-risk-events.md#impossible-travel-to-atypical-locations-1).</span></span>

- <span data-ttu-id="7ede7-127">**Country / Regions** - This option enables you to select one or more country or region to define a named location.</span><span class="sxs-lookup"><span data-stu-id="7ede7-127">**Country / Regions** - This option enables you to select one or more country or region to define a named location.</span></span> 

- <span data-ttu-id="7ede7-128">**Include unknown areas** - Some IP addresses are not mapped to a specific country.</span><span class="sxs-lookup"><span data-stu-id="7ede7-128">**Include unknown areas** - Some IP addresses are not mapped to a specific country.</span></span> <span data-ttu-id="7ede7-129">This option allows you to choose if these IP addresses should be included in the named location.</span><span class="sxs-lookup"><span data-stu-id="7ede7-129">This option allows you to choose if these IP addresses should be included in the named location.</span></span> <span data-ttu-id="7ede7-130">They could be check when the policy using the named location should apply to unknown locations.</span><span class="sxs-lookup"><span data-stu-id="7ede7-130">They could be check when the policy using the named location should apply to unknown locations.</span></span>

<span data-ttu-id="7ede7-131">The number of named locations you can configure is constrained by the size of the related object in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ede7-131">The number of named locations you can configure is constrained by the size of the related object in Azure AD.</span></span> <span data-ttu-id="7ede7-132">You can configure:</span><span class="sxs-lookup"><span data-stu-id="7ede7-132">You can configure:</span></span>

- <span data-ttu-id="7ede7-133">One named location with up to 1200 IP ranges.</span><span class="sxs-lookup"><span data-stu-id="7ede7-133">One named location with up to 1200 IP ranges.</span></span>

- <span data-ttu-id="7ede7-134">A maximum of 90 named locations with one IP range assigned to each of them.</span><span class="sxs-lookup"><span data-stu-id="7ede7-134">A maximum of 90 named locations with one IP range assigned to each of them.</span></span>




## <a name="trusted-ips"></a><span data-ttu-id="7ede7-135">Trusted IPs</span><span class="sxs-lookup"><span data-stu-id="7ede7-135">Trusted IPs</span></span>

<span data-ttu-id="7ede7-136">You can also configure IP address ranges representing your organization's local intranet in the [multi-factor authentication service settings](https://account.activedirectory.windowsazure.com/usermanagement/mfasettings.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ede7-136">You can also configure IP address ranges representing your organization's local intranet in the [multi-factor authentication service settings](https://account.activedirectory.windowsazure.com/usermanagement/mfasettings.aspx).</span></span> <span data-ttu-id="7ede7-137">This feature enables you to configure up to 50 IP address ranges.</span><span class="sxs-lookup"><span data-stu-id="7ede7-137">This feature enables you to configure up to 50 IP address ranges.</span></span> <span data-ttu-id="7ede7-138">The IP address ranges are in CIDR format.</span><span class="sxs-lookup"><span data-stu-id="7ede7-138">The IP address ranges are in CIDR format.</span></span> <span data-ttu-id="7ede7-139">For more information, see [trusted IPs](../authentication/howto-mfa-mfasettings.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="7ede7-139">For more information, see [trusted IPs](../authentication/howto-mfa-mfasettings.md#trusted-ips).</span></span>  

<span data-ttu-id="7ede7-140">If you have trusted IPs configured, they show up as **MFA Trusted IPS** in the list of locations for the location condition.</span><span class="sxs-lookup"><span data-stu-id="7ede7-140">If you have trusted IPs configured, they show up as **MFA Trusted IPS** in the list of locations for the location condition.</span></span>   

### <a name="skipping-multi-factor-authentication"></a><span data-ttu-id="7ede7-141">Skipping multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="7ede7-141">Skipping multi-factor authentication</span></span>

<span data-ttu-id="7ede7-142">On the multi-factor authentication service settings page, you can identify corporate intranet users by selecting  **Skip multi-factor authentication for requests from federated users on my intranet**.</span><span class="sxs-lookup"><span data-stu-id="7ede7-142">On the multi-factor authentication service settings page, you can identify corporate intranet users by selecting  **Skip multi-factor authentication for requests from federated users on my intranet**.</span></span> <span data-ttu-id="7ede7-143">This setting indicates that the inside corporate network claim, which is issued by AD FS, should be trusted and used to identify the user as being on the corporate network.</span><span class="sxs-lookup"><span data-stu-id="7ede7-143">This setting indicates that the inside corporate network claim, which is issued by AD FS, should be trusted and used to identify the user as being on the corporate network.</span></span> <span data-ttu-id="7ede7-144">For more information, see [Enable the Trusted IPs feature by using conditional access](../authentication/howto-mfa-mfasettings.md#enable-the-trusted-ips-feature-by-using-conditional-access).</span><span class="sxs-lookup"><span data-stu-id="7ede7-144">For more information, see [Enable the Trusted IPs feature by using conditional access](../authentication/howto-mfa-mfasettings.md#enable-the-trusted-ips-feature-by-using-conditional-access).</span></span>

<span data-ttu-id="7ede7-145">After checking this option, including the named location **MFA Trusted IPS** will apply to any policies with this selected.</span><span class="sxs-lookup"><span data-stu-id="7ede7-145">After checking this option, including the named location **MFA Trusted IPS** will apply to any policies with this selected.</span></span>

<span data-ttu-id="7ede7-146">For mobile and desktop applications, which have long lived session lifetimes, conditional access is periodically re-evaluated.</span><span class="sxs-lookup"><span data-stu-id="7ede7-146">For mobile and desktop applications, which have long lived session lifetimes, conditional access is periodically re-evaluated.</span></span> <span data-ttu-id="7ede7-147">The default is once an hour.</span><span class="sxs-lookup"><span data-stu-id="7ede7-147">The default is once an hour.</span></span> <span data-ttu-id="7ede7-148">When the inside corporate network claim is and only issued at the time of the initial authentication, Azure AD may not have a list of trusted IP ranges.</span><span class="sxs-lookup"><span data-stu-id="7ede7-148">When the inside corporate network claim is and only issued at the time of the initial authentication, Azure AD may not have a list of trusted IP ranges.</span></span> <span data-ttu-id="7ede7-149">In this case, it is more difficult to determine if the user is still on the corporate network:</span><span class="sxs-lookup"><span data-stu-id="7ede7-149">In this case, it is more difficult to determine if the user is still on the corporate network:</span></span>

1. <span data-ttu-id="7ede7-150">Check if the user’s IP address is in one of the trusted IP ranges.</span><span class="sxs-lookup"><span data-stu-id="7ede7-150">Check if the user’s IP address is in one of the trusted IP ranges.</span></span>

2. <span data-ttu-id="7ede7-151">Check whether the first three octets of the user’s IP address match the first 3 octets of the IP address of the initial authentication.</span><span class="sxs-lookup"><span data-stu-id="7ede7-151">Check whether the first three octets of the user’s IP address match the first 3 octets of the IP address of the initial authentication.</span></span> <span data-ttu-id="7ede7-152">The IP address is compared with the initial authentication because this is when the inside corporate network claim was originally issued and the user location was validated.</span><span class="sxs-lookup"><span data-stu-id="7ede7-152">The IP address is compared with the initial authentication because this is when the inside corporate network claim was originally issued and the user location was validated.</span></span>

<span data-ttu-id="7ede7-153">If both steps fail, a user is considered to be no longer on a trusted IP.</span><span class="sxs-lookup"><span data-stu-id="7ede7-153">If both steps fail, a user is considered to be no longer on a trusted IP.</span></span>



## <a name="location-condition-configuration"></a><span data-ttu-id="7ede7-154">Location condition configuration</span><span class="sxs-lookup"><span data-stu-id="7ede7-154">Location condition configuration</span></span>

<span data-ttu-id="7ede7-155">When you configure the location condition, you have the option to distinguish between:</span><span class="sxs-lookup"><span data-stu-id="7ede7-155">When you configure the location condition, you have the option to distinguish between:</span></span>

- <span data-ttu-id="7ede7-156">Any location</span><span class="sxs-lookup"><span data-stu-id="7ede7-156">Any location</span></span> 
- <span data-ttu-id="7ede7-157">All trusted locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-157">All trusted locations</span></span>
- <span data-ttu-id="7ede7-158">Selected locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-158">Selected locations</span></span>

![Locations](./media/location-condition/01.png)

### <a name="any-location"></a><span data-ttu-id="7ede7-160">Any location</span><span class="sxs-lookup"><span data-stu-id="7ede7-160">Any location</span></span>

<span data-ttu-id="7ede7-161">By default, selecting **Any location** causes a policy to be applied to all IP addresses, which means any address on the Internet.</span><span class="sxs-lookup"><span data-stu-id="7ede7-161">By default, selecting **Any location** causes a policy to be applied to all IP addresses, which means any address on the Internet.</span></span> <span data-ttu-id="7ede7-162">This setting is not limited to IP addresses you have configured as named location.</span><span class="sxs-lookup"><span data-stu-id="7ede7-162">This setting is not limited to IP addresses you have configured as named location.</span></span> <span data-ttu-id="7ede7-163">When you select **Any location**, you can still exclude specific locations from a policy.</span><span class="sxs-lookup"><span data-stu-id="7ede7-163">When you select **Any location**, you can still exclude specific locations from a policy.</span></span> <span data-ttu-id="7ede7-164">For example, you can apply a policy to all locations except trusted locations to set the scope to all locations, except the corporate network.</span><span class="sxs-lookup"><span data-stu-id="7ede7-164">For example, you can apply a policy to all locations except trusted locations to set the scope to all locations, except the corporate network.</span></span>

### <a name="all-trusted-locations"></a><span data-ttu-id="7ede7-165">All trusted locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-165">All trusted locations</span></span>

<span data-ttu-id="7ede7-166">This option applies to:</span><span class="sxs-lookup"><span data-stu-id="7ede7-166">This option applies to:</span></span>

- <span data-ttu-id="7ede7-167">All locations that have been marked as trusted location</span><span class="sxs-lookup"><span data-stu-id="7ede7-167">All locations that have been marked as trusted location</span></span>
- <span data-ttu-id="7ede7-168">**MFA Trusted IPS** (if configured)</span><span class="sxs-lookup"><span data-stu-id="7ede7-168">**MFA Trusted IPS** (if configured)</span></span>


### <a name="selected-locations"></a><span data-ttu-id="7ede7-169">Selected locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-169">Selected locations</span></span>

<span data-ttu-id="7ede7-170">With this option, you can select one or more named locations.</span><span class="sxs-lookup"><span data-stu-id="7ede7-170">With this option, you can select one or more named locations.</span></span> <span data-ttu-id="7ede7-171">For a policy with this setting to apply, a user needs to connect from any of the selected locations.</span><span class="sxs-lookup"><span data-stu-id="7ede7-171">For a policy with this setting to apply, a user needs to connect from any of the selected locations.</span></span> <span data-ttu-id="7ede7-172">When you click **Select** the named network selection control that shows the list of named networks opens.</span><span class="sxs-lookup"><span data-stu-id="7ede7-172">When you click **Select** the named network selection control that shows the list of named networks opens.</span></span> <span data-ttu-id="7ede7-173">The list also shows if the network location has been marked as trusted.</span><span class="sxs-lookup"><span data-stu-id="7ede7-173">The list also shows if the network location has been marked as trusted.</span></span> <span data-ttu-id="7ede7-174">The named location called **MFA Trusted IPs** is used to include the IP settings that can be configured in the multi-factor authentication service setting page.</span><span class="sxs-lookup"><span data-stu-id="7ede7-174">The named location called **MFA Trusted IPs** is used to include the IP settings that can be configured in the multi-factor authentication service setting page.</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="7ede7-175">What you should know</span><span class="sxs-lookup"><span data-stu-id="7ede7-175">What you should know</span></span>

### <a name="when-is-a-location-evaluated"></a><span data-ttu-id="7ede7-176">When is a location evaluated?</span><span class="sxs-lookup"><span data-stu-id="7ede7-176">When is a location evaluated?</span></span>

<span data-ttu-id="7ede7-177">Conditional access policies are evaluated when:</span><span class="sxs-lookup"><span data-stu-id="7ede7-177">Conditional access policies are evaluated when:</span></span> 

- <span data-ttu-id="7ede7-178">A user initially signs in to a web app, mobile or desktop application.</span><span class="sxs-lookup"><span data-stu-id="7ede7-178">A user initially signs in to a web app, mobile or desktop application.</span></span> 

- <span data-ttu-id="7ede7-179">A mobile or desktop application that uses modern authentication, uses a refresh token to acquire a new access token.</span><span class="sxs-lookup"><span data-stu-id="7ede7-179">A mobile or desktop application that uses modern authentication, uses a refresh token to acquire a new access token.</span></span> <span data-ttu-id="7ede7-180">By default this is once an hour.</span><span class="sxs-lookup"><span data-stu-id="7ede7-180">By default this is once an hour.</span></span> 

<span data-ttu-id="7ede7-181">This means for mobile and desktop applications using modern authentication, a change in location would be detected within an hour of changing the network location.</span><span class="sxs-lookup"><span data-stu-id="7ede7-181">This means for mobile and desktop applications using modern authentication, a change in location would be detected within an hour of changing the network location.</span></span> <span data-ttu-id="7ede7-182">For mobile and desktop applications that don’t use modern authentication, the policy is applied on each token request.</span><span class="sxs-lookup"><span data-stu-id="7ede7-182">For mobile and desktop applications that don’t use modern authentication, the policy is applied on each token request.</span></span> <span data-ttu-id="7ede7-183">The frequency of the request can vary based on the application.</span><span class="sxs-lookup"><span data-stu-id="7ede7-183">The frequency of the request can vary based on the application.</span></span> <span data-ttu-id="7ede7-184">Similarly, for web applications, the policy is applied at initial sign-in and is good for the lifetime of the session at the web application.</span><span class="sxs-lookup"><span data-stu-id="7ede7-184">Similarly, for web applications, the policy is applied at initial sign-in and is good for the lifetime of the session at the web application.</span></span> <span data-ttu-id="7ede7-185">Due to differences in session lifetimes across applications, the time between policy evaluation will also vary.</span><span class="sxs-lookup"><span data-stu-id="7ede7-185">Due to differences in session lifetimes across applications, the time between policy evaluation will also vary.</span></span> <span data-ttu-id="7ede7-186">Each time the application requests a new sign-in token, the  policy is applied.</span><span class="sxs-lookup"><span data-stu-id="7ede7-186">Each time the application requests a new sign-in token, the  policy is applied.</span></span>


<span data-ttu-id="7ede7-187">By default, Azure AD issues a token on an hourly basis.</span><span class="sxs-lookup"><span data-stu-id="7ede7-187">By default, Azure AD issues a token on an hourly basis.</span></span> <span data-ttu-id="7ede7-188">After moving off the corporate network, within an hour the policy is enforced for applications using modern authentication.</span><span class="sxs-lookup"><span data-stu-id="7ede7-188">After moving off the corporate network, within an hour the policy is enforced for applications using modern authentication.</span></span>


### <a name="user-ip-address"></a><span data-ttu-id="7ede7-189">User IP address</span><span class="sxs-lookup"><span data-stu-id="7ede7-189">User IP address</span></span>

<span data-ttu-id="7ede7-190">The IP address that is used in policy evaluation is the public IP address of the user.</span><span class="sxs-lookup"><span data-stu-id="7ede7-190">The IP address that is used in policy evaluation is the public IP address of the user.</span></span> <span data-ttu-id="7ede7-191">For devices on a private network, this is not the client IP of the user’s device on the intranet, it is the address used by the network to connect to the public internet.</span><span class="sxs-lookup"><span data-stu-id="7ede7-191">For devices on a private network, this is not the client IP of the user’s device on the intranet, it is the address used by the network to connect to the public internet.</span></span> 

### <a name="bulk-uploading-and-downloading-of-named-locations"></a><span data-ttu-id="7ede7-192">Bulk uploading and downloading of named locations</span><span class="sxs-lookup"><span data-stu-id="7ede7-192">Bulk uploading and downloading of named locations</span></span>

<span data-ttu-id="7ede7-193">When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span><span class="sxs-lookup"><span data-stu-id="7ede7-193">When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="7ede7-194">An upload replaces the IP ranges in the list with those from the file.</span><span class="sxs-lookup"><span data-stu-id="7ede7-194">An upload replaces the IP ranges in the list with those from the file.</span></span> <span data-ttu-id="7ede7-195">Each row of the file contains one IP Address range in CIDR format.</span><span class="sxs-lookup"><span data-stu-id="7ede7-195">Each row of the file contains one IP Address range in CIDR format.</span></span> 


### <a name="cloud-proxies-and-vpns"></a><span data-ttu-id="7ede7-196">Cloud proxies and VPNs</span><span class="sxs-lookup"><span data-stu-id="7ede7-196">Cloud proxies and VPNs</span></span> 

<span data-ttu-id="7ede7-197">When you use a cloud hosted proxy or VPN solution, the IP address Azure AD uses while evaluating a policy is the IP address of the proxy.</span><span class="sxs-lookup"><span data-stu-id="7ede7-197">When you use a cloud hosted proxy or VPN solution, the IP address Azure AD uses while evaluating a policy is the IP address of the proxy.</span></span> <span data-ttu-id="7ede7-198">The X-Forwarded-For (XFF) header that contains the users public IP address is not used because there is no validation that it comes from a trusted source, so would present a method for faking an IP address.</span><span class="sxs-lookup"><span data-stu-id="7ede7-198">The X-Forwarded-For (XFF) header that contains the users public IP address is not used because there is no validation that it comes from a trusted source, so would present a method for faking an IP address.</span></span> 

<span data-ttu-id="7ede7-199">When a cloud proxy is in place, a policy that is used to require a domain joined device can be used, or the inside corpnet claim from AD FS.</span><span class="sxs-lookup"><span data-stu-id="7ede7-199">When a cloud proxy is in place, a policy that is used to require a domain joined device can be used, or the inside corpnet claim from AD FS.</span></span>



### <a name="api-support-and-powershell"></a><span data-ttu-id="7ede7-200">API support and PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ede7-200">API support and PowerShell</span></span> 

<span data-ttu-id="7ede7-201">API and PowerShell is not yet supported for named locations, or for conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="7ede7-201">API and PowerShell is not yet supported for named locations, or for conditional access policies.</span></span>





## <a name="next-steps"></a><span data-ttu-id="7ede7-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ede7-202">Next steps</span></span>

- <span data-ttu-id="7ede7-203">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="7ede7-203">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

- <span data-ttu-id="7ede7-204">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="7ede7-204">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 
