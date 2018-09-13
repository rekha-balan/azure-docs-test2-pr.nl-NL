---
title: Azure Active Directory Identity Protection playbook | Microsoft Docs
description: Learn how Azure AD Identity Protection enables you to limit the ability of an attacker to exploit a compromised identity or device and to secure an identity or a device that was previously suspected or known to be compromised.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: markvi
ms.openlocfilehash: 1056b14aa783fa052ba038560d14b8d6bc9819d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554781"
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="d0c58-104">Azure Active Directory Identity Protection playbook</span><span class="sxs-lookup"><span data-stu-id="d0c58-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="d0c58-105">This playbook helps you to:</span><span class="sxs-lookup"><span data-stu-id="d0c58-105">This playbook helps you to:</span></span>

* <span data-ttu-id="d0c58-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="d0c58-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="d0c58-107">Set up risk-based conditional access policies and test the impact of these policies</span><span class="sxs-lookup"><span data-stu-id="d0c58-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="d0c58-108">Simulating Risk Events</span><span class="sxs-lookup"><span data-stu-id="d0c58-108">Simulating Risk Events</span></span>
<span data-ttu-id="d0c58-109">This section provides you with steps for simulating the following risk event types:</span><span class="sxs-lookup"><span data-stu-id="d0c58-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="d0c58-110">Sign-ins from anonymous IP addresses (easy)</span><span class="sxs-lookup"><span data-stu-id="d0c58-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="d0c58-111">Sign-ins from unfamiliar locations (moderate)</span><span class="sxs-lookup"><span data-stu-id="d0c58-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="d0c58-112">Impossible travel to atypical locations (difficult)</span><span class="sxs-lookup"><span data-stu-id="d0c58-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="d0c58-113">Other risk events cannot be simulated in a secure manner.</span><span class="sxs-lookup"><span data-stu-id="d0c58-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="d0c58-114">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="d0c58-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="d0c58-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span><span class="sxs-lookup"><span data-stu-id="d0c58-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="d0c58-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span><span class="sxs-lookup"><span data-stu-id="d0c58-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="d0c58-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="d0c58-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="d0c58-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="d0c58-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="d0c58-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d0c58-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="d0c58-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span><span class="sxs-lookup"><span data-stu-id="d0c58-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="d0c58-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="d0c58-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="d0c58-122">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="d0c58-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="d0c58-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span><span class="sxs-lookup"><span data-stu-id="d0c58-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="d0c58-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span><span class="sxs-lookup"><span data-stu-id="d0c58-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="d0c58-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span><span class="sxs-lookup"><span data-stu-id="d0c58-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="d0c58-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="d0c58-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="d0c58-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span><span class="sxs-lookup"><span data-stu-id="d0c58-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="d0c58-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span><span class="sxs-lookup"><span data-stu-id="d0c58-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="d0c58-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span><span class="sxs-lookup"><span data-stu-id="d0c58-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="d0c58-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="d0c58-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="d0c58-131">Choose an account that has at least a 14-day sign-in history.</span><span class="sxs-lookup"><span data-stu-id="d0c58-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="d0c58-132">Do either:</span><span class="sxs-lookup"><span data-stu-id="d0c58-132">Do either:</span></span>
   
   <span data-ttu-id="d0c58-133">a.</span><span class="sxs-lookup"><span data-stu-id="d0c58-133">a.</span></span> <span data-ttu-id="d0c58-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span><span class="sxs-lookup"><span data-stu-id="d0c58-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="d0c58-135">b.</span><span class="sxs-lookup"><span data-stu-id="d0c58-135">b.</span></span> <span data-ttu-id="d0c58-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span><span class="sxs-lookup"><span data-stu-id="d0c58-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="d0c58-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="d0c58-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="d0c58-138">Impossible travel to atypical location</span><span class="sxs-lookup"><span data-stu-id="d0c58-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="d0c58-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span><span class="sxs-lookup"><span data-stu-id="d0c58-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="d0c58-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span><span class="sxs-lookup"><span data-stu-id="d0c58-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="d0c58-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="d0c58-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="d0c58-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d0c58-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="d0c58-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span><span class="sxs-lookup"><span data-stu-id="d0c58-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="d0c58-144">Change your user agent.</span><span class="sxs-lookup"><span data-stu-id="d0c58-144">Change your user agent.</span></span> <span data-ttu-id="d0c58-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span><span class="sxs-lookup"><span data-stu-id="d0c58-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="d0c58-146">Change your IP address.</span><span class="sxs-lookup"><span data-stu-id="d0c58-146">Change your IP address.</span></span> <span data-ttu-id="d0c58-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span><span class="sxs-lookup"><span data-stu-id="d0c58-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="d0c58-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span><span class="sxs-lookup"><span data-stu-id="d0c58-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="d0c58-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span><span class="sxs-lookup"><span data-stu-id="d0c58-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="d0c58-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span><span class="sxs-lookup"><span data-stu-id="d0c58-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="d0c58-151">You might want to replicate these steps for multiple Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d0c58-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="d0c58-152">Simulating vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="d0c58-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="d0c58-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span><span class="sxs-lookup"><span data-stu-id="d0c58-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="d0c58-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0c58-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="d0c58-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span><span class="sxs-lookup"><span data-stu-id="d0c58-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="d0c58-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d0c58-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="d0c58-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c58-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="d0c58-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d0c58-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="d0c58-159">User compromise risk</span><span class="sxs-lookup"><span data-stu-id="d0c58-159">User compromise risk</span></span>
<span data-ttu-id="d0c58-160">**To test User compromise risk, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="d0c58-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="d0c58-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="d0c58-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="d0c58-162">Navigate to **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="d0c58-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="d0c58-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="d0c58-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span><span class="sxs-lookup"><span data-stu-id="d0c58-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="d0c58-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span><span class="sxs-lookup"><span data-stu-id="d0c58-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="d0c58-167">This will elevate the user risk level for that user to **Medium**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="d0c58-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="d0c58-169">Go to the **Portal Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="d0c58-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="d0c58-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span><span class="sxs-lookup"><span data-stu-id="d0c58-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="d0c58-171">Select one of the following options:</span><span class="sxs-lookup"><span data-stu-id="d0c58-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="d0c58-172">a.</span><span class="sxs-lookup"><span data-stu-id="d0c58-172">a.</span></span> <span data-ttu-id="d0c58-173">To block, select **Medium** under **Block sign in**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="d0c58-174">b.</span><span class="sxs-lookup"><span data-stu-id="d0c58-174">b.</span></span> <span data-ttu-id="d0c58-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="d0c58-176">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-176">Click **Save**.</span></span>
12. <span data-ttu-id="d0c58-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span><span class="sxs-lookup"><span data-stu-id="d0c58-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="d0c58-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span><span class="sxs-lookup"><span data-stu-id="d0c58-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br>
    <span data-ttu-id="d0c58-179">![Playbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-playbook/201.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="d0c58-179">![Playbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-playbook/201.png "Playbook")</span></span>
    <br>

## <a name="sign-in-risk"></a><span data-ttu-id="d0c58-180">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="d0c58-180">Sign-in risk</span></span>
<span data-ttu-id="d0c58-181">**To test a sign in risk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0c58-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="d0c58-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="d0c58-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="d0c58-183">Navigate to **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="d0c58-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="d0c58-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="d0c58-186">On the \*\*Sign in Risk \*\*blade, select **On** under **Enable rule**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-186">On the \*\*Sign in Risk \*\*blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="d0c58-187">Select one of the following options:</span><span class="sxs-lookup"><span data-stu-id="d0c58-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="d0c58-188">a.</span><span class="sxs-lookup"><span data-stu-id="d0c58-188">a.</span></span> <span data-ttu-id="d0c58-189">To block, select **Medium** under **Block sign in**</span><span class="sxs-lookup"><span data-stu-id="d0c58-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="d0c58-190">b.</span><span class="sxs-lookup"><span data-stu-id="d0c58-190">b.</span></span> <span data-ttu-id="d0c58-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="d0c58-192">To block, select Medium under Block sign in.</span><span class="sxs-lookup"><span data-stu-id="d0c58-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="d0c58-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="d0c58-194">Click on **Save**.</span><span class="sxs-lookup"><span data-stu-id="d0c58-194">Click on **Save**.</span></span>
10. <span data-ttu-id="d0c58-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span><span class="sxs-lookup"><span data-stu-id="d0c58-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="d0c58-196">![Playbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="d0c58-196">![Playbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="d0c58-197">See also</span><span class="sxs-lookup"><span data-stu-id="d0c58-197">See also</span></span>
* [<span data-ttu-id="d0c58-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d0c58-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)



