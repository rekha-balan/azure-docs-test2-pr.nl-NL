---
title: Azure Active Directory Identity Protection playbook | Microsoft Docs
description: Learn how Azure AD Identity Protection enables you to limit the ability of an attacker to exploit a compromised identity or device and to secure an identity or a device that was previously suspected or known to be compromised.
services: active-directory
keywords: azure active directory identity protection, cloud discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 02d402b7de82631ce459c60cb42e5335c7e7cfe3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858031"
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="f791a-104">Azure Active Directory Identity Protection playbook</span><span class="sxs-lookup"><span data-stu-id="f791a-104">Azure Active Directory Identity Protection playbook</span></span>

<span data-ttu-id="f791a-105">This playbook helps you to:</span><span class="sxs-lookup"><span data-stu-id="f791a-105">This playbook helps you to:</span></span>

* <span data-ttu-id="f791a-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="f791a-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="f791a-107">Set up risk-based conditional access policies and test the impact of these policies</span><span class="sxs-lookup"><span data-stu-id="f791a-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>


## <a name="simulating-risk-events"></a><span data-ttu-id="f791a-108">Simulating Risk Events</span><span class="sxs-lookup"><span data-stu-id="f791a-108">Simulating Risk Events</span></span>

<span data-ttu-id="f791a-109">This section provides you with steps for simulating the following risk event types:</span><span class="sxs-lookup"><span data-stu-id="f791a-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="f791a-110">Sign-ins from anonymous IP addresses (easy)</span><span class="sxs-lookup"><span data-stu-id="f791a-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="f791a-111">Sign-ins from unfamiliar locations (moderate)</span><span class="sxs-lookup"><span data-stu-id="f791a-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="f791a-112">Impossible travel to atypical locations (difficult)</span><span class="sxs-lookup"><span data-stu-id="f791a-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="f791a-113">Other risk events cannot be simulated in a secure manner.</span><span class="sxs-lookup"><span data-stu-id="f791a-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="f791a-114">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="f791a-114">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="f791a-115">For more information about this risk event, see [Sign-ins from anonymous IP addresses](../reports-monitoring/concept-risk-events.md#sign-ins-from-anonymous-ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="f791a-115">For more information about this risk event, see [Sign-ins from anonymous IP addresses](../reports-monitoring/concept-risk-events.md#sign-ins-from-anonymous-ip-addresses).</span></span> 

<span data-ttu-id="f791a-116">Completing the following procedure requires you to use:</span><span class="sxs-lookup"><span data-stu-id="f791a-116">Completing the following procedure requires you to use:</span></span>

- <span data-ttu-id="f791a-117">The [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en) to simulate anonymous IP addresses.</span><span class="sxs-lookup"><span data-stu-id="f791a-117">The [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en) to simulate anonymous IP addresses.</span></span> <span data-ttu-id="f791a-118">You might need to use a virtual machine if your organization restricts using the Tor browser.</span><span class="sxs-lookup"><span data-stu-id="f791a-118">You might need to use a virtual machine if your organization restricts using the Tor browser.</span></span>
- <span data-ttu-id="f791a-119">A test account that is not yet registered for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="f791a-119">A test account that is not yet registered for multi-factor authentication.</span></span>

<span data-ttu-id="f791a-120">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="f791a-120">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="f791a-121">Using the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en), navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f791a-121">Using the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en), navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
2. <span data-ttu-id="f791a-122">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span><span class="sxs-lookup"><span data-stu-id="f791a-122">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="f791a-123">The sign-in shows up on the Identity Protection dashboard within 10 - 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f791a-123">The sign-in shows up on the Identity Protection dashboard within 10 - 15 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="f791a-124">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="f791a-124">Sign-ins from unfamiliar locations</span></span>

<span data-ttu-id="f791a-125">For more information about this risk event, see [Sign-ins from unfamiliar locations](../reports-monitoring/concept-risk-events.md#sign-in-from-unfamiliar-locations).</span><span class="sxs-lookup"><span data-stu-id="f791a-125">For more information about this risk event, see [Sign-ins from unfamiliar locations](../reports-monitoring/concept-risk-events.md#sign-in-from-unfamiliar-locations).</span></span> 

<span data-ttu-id="f791a-126">To simulate unfamiliar locations, you have to sign in from a location and device your test account has not signed in from before.</span><span class="sxs-lookup"><span data-stu-id="f791a-126">To simulate unfamiliar locations, you have to sign in from a location and device your test account has not signed in from before.</span></span>

<span data-ttu-id="f791a-127">The procedure below uses a newly created:</span><span class="sxs-lookup"><span data-stu-id="f791a-127">The procedure below uses a newly created:</span></span>

- <span data-ttu-id="f791a-128">VPN connection, to simulate new location.</span><span class="sxs-lookup"><span data-stu-id="f791a-128">VPN connection, to simulate new location.</span></span>

- <span data-ttu-id="f791a-129">Virtual machine, to simulate a new device.</span><span class="sxs-lookup"><span data-stu-id="f791a-129">Virtual machine, to simulate a new device.</span></span>

<span data-ttu-id="f791a-130">Completing the following procedure requires you to use a user account that has:</span><span class="sxs-lookup"><span data-stu-id="f791a-130">Completing the following procedure requires you to use a user account that has:</span></span>

- <span data-ttu-id="f791a-131">At least a 30-day sign-in history.</span><span class="sxs-lookup"><span data-stu-id="f791a-131">At least a 30-day sign-in history.</span></span>
- <span data-ttu-id="f791a-132">Multi-factor authentication enabled.</span><span class="sxs-lookup"><span data-stu-id="f791a-132">Multi-factor authentication enabled.</span></span>


<span data-ttu-id="f791a-133">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="f791a-133">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="f791a-134">When signing in with your test account, fail the MFA challenge by not passing the MFA challenge.</span><span class="sxs-lookup"><span data-stu-id="f791a-134">When signing in with your test account, fail the MFA challenge by not passing the MFA challenge.</span></span>
2. <span data-ttu-id="f791a-135">Using your new VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of your test account.</span><span class="sxs-lookup"><span data-stu-id="f791a-135">Using your new VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of your test account.</span></span>
   

<span data-ttu-id="f791a-136">The sign-in shows up on the Identity Protection dashboard within 10 - 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f791a-136">The sign-in shows up on the Identity Protection dashboard within 10 - 15 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="f791a-137">Impossible travel to atypical location</span><span class="sxs-lookup"><span data-stu-id="f791a-137">Impossible travel to atypical location</span></span>

<span data-ttu-id="f791a-138">For more information about this risk event, see [Impossible travel to atypical location](../reports-monitoring/concept-risk-events.md#impossible-travel-to-atypical-locations).</span><span class="sxs-lookup"><span data-stu-id="f791a-138">For more information about this risk event, see [Impossible travel to atypical location](../reports-monitoring/concept-risk-events.md#impossible-travel-to-atypical-locations).</span></span> 

<span data-ttu-id="f791a-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span><span class="sxs-lookup"><span data-stu-id="f791a-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="f791a-140">Additionally, the algorithm requires a sign-in history of 14 days and 10 logins of the user before it begins generating risk events.</span><span class="sxs-lookup"><span data-stu-id="f791a-140">Additionally, the algorithm requires a sign-in history of 14 days and 10 logins of the user before it begins generating risk events.</span></span> <span data-ttu-id="f791a-141">Because of the complex machine learning models and above rules, there is a chance that the following steps will not lead to a risk event.</span><span class="sxs-lookup"><span data-stu-id="f791a-141">Because of the complex machine learning models and above rules, there is a chance that the following steps will not lead to a risk event.</span></span> <span data-ttu-id="f791a-142">You might want to replicate these steps for multiple Azure AD accounts to publish this risk event.</span><span class="sxs-lookup"><span data-stu-id="f791a-142">You might want to replicate these steps for multiple Azure AD accounts to publish this risk event.</span></span>


<span data-ttu-id="f791a-143">**To simulate an impossible travel to atypical location, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="f791a-143">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="f791a-144">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f791a-144">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="f791a-145">Enter the credentials of the account you want to generate an impossible travel risk event for.</span><span class="sxs-lookup"><span data-stu-id="f791a-145">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="f791a-146">Change your user agent.</span><span class="sxs-lookup"><span data-stu-id="f791a-146">Change your user agent.</span></span> <span data-ttu-id="f791a-147">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span><span class="sxs-lookup"><span data-stu-id="f791a-147">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="f791a-148">Change your IP address.</span><span class="sxs-lookup"><span data-stu-id="f791a-148">Change your IP address.</span></span> <span data-ttu-id="f791a-149">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span><span class="sxs-lookup"><span data-stu-id="f791a-149">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="f791a-150">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span><span class="sxs-lookup"><span data-stu-id="f791a-150">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="f791a-151">The sign-in shows up in the Identity Protection dashboard within 2-4 hours.</span><span class="sxs-lookup"><span data-stu-id="f791a-151">The sign-in shows up in the Identity Protection dashboard within 2-4 hours.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="f791a-152">Simulating vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="f791a-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="f791a-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span><span class="sxs-lookup"><span data-stu-id="f791a-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="f791a-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f791a-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="f791a-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span><span class="sxs-lookup"><span data-stu-id="f791a-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="f791a-156">Azure AD [Multi-Factor Authentication](../authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f791a-156">Azure AD [Multi-Factor Authentication](../authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="f791a-157">Azure AD [Cloud Discovery](https://docs.microsoft.com/cloud-app-security/).</span><span class="sxs-lookup"><span data-stu-id="f791a-157">Azure AD [Cloud Discovery](https://docs.microsoft.com/cloud-app-security/).</span></span>
* <span data-ttu-id="f791a-158">Azure AD [Privileged Identity Management](../privileged-identity-management/pim-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f791a-158">Azure AD [Privileged Identity Management](../privileged-identity-management/pim-configure.md).</span></span> 


## <a name="testing-security-policies"></a><span data-ttu-id="f791a-159">Testing security policies</span><span class="sxs-lookup"><span data-stu-id="f791a-159">Testing security policies</span></span>

<span data-ttu-id="f791a-160">This section provides you with steps for testing the user risk and the sign-in risk security policy.</span><span class="sxs-lookup"><span data-stu-id="f791a-160">This section provides you with steps for testing the user risk and the sign-in risk security policy.</span></span>


### <a name="user-risk-security-policy"></a><span data-ttu-id="f791a-161">User risk security policy</span><span class="sxs-lookup"><span data-stu-id="f791a-161">User risk security policy</span></span>

<span data-ttu-id="f791a-162">For more information, see [User risk security policy](overview.md#user-risk-security-policy).</span><span class="sxs-lookup"><span data-stu-id="f791a-162">For more information, see [User risk security policy](overview.md#user-risk-security-policy).</span></span>

<span data-ttu-id="f791a-163">![User risk](./media/playbook/02.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="f791a-163">![User risk](./media/playbook/02.png "Playbook")</span></span>


<span data-ttu-id="f791a-164">**To test a user risk security policy, perform the following steps**:</span><span class="sxs-lookup"><span data-stu-id="f791a-164">**To test a user risk security policy, perform the following steps**:</span></span>

1. <span data-ttu-id="f791a-165">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="f791a-165">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="f791a-166">Navigate to **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="f791a-166">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="f791a-167">On the **Azure AD Identity Protection** page, click **User risk policy**.</span><span class="sxs-lookup"><span data-stu-id="f791a-167">On the **Azure AD Identity Protection** page, click **User risk policy**.</span></span>
4. <span data-ttu-id="f791a-168">In the **Assignments** section, select the desired users (and groups) and user risk level.</span><span class="sxs-lookup"><span data-stu-id="f791a-168">In the **Assignments** section, select the desired users (and groups) and user risk level.</span></span>

    <span data-ttu-id="f791a-169">![User risk](./media/playbook/03.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="f791a-169">![User risk](./media/playbook/03.png "Playbook")</span></span>

5. <span data-ttu-id="f791a-170">In the Controls section, select the desired Access control (e.g. Require password change).</span><span class="sxs-lookup"><span data-stu-id="f791a-170">In the Controls section, select the desired Access control (e.g. Require password change).</span></span>
5. <span data-ttu-id="f791a-171">As **Enforce Policy**, select **Off**.</span><span class="sxs-lookup"><span data-stu-id="f791a-171">As **Enforce Policy**, select **Off**.</span></span>
6. <span data-ttu-id="f791a-172">Elevate the user risk of a test account by, for example, simulating one of the risk events a few times.</span><span class="sxs-lookup"><span data-stu-id="f791a-172">Elevate the user risk of a test account by, for example, simulating one of the risk events a few times.</span></span>
7. <span data-ttu-id="f791a-173">Wait a few minutes, and then verify that user level for your user is Medium.</span><span class="sxs-lookup"><span data-stu-id="f791a-173">Wait a few minutes, and then verify that user level for your user is Medium.</span></span> <span data-ttu-id="f791a-174">If not, simulate more risk events for the user.</span><span class="sxs-lookup"><span data-stu-id="f791a-174">If not, simulate more risk events for the user.</span></span>
8. <span data-ttu-id="f791a-175">As **Enforce Policy**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="f791a-175">As **Enforce Policy**, select **On**.</span></span>
9. <span data-ttu-id="f791a-176">You can now test user risk-based conditional access by signing in using a user with an elevated risk level.</span><span class="sxs-lookup"><span data-stu-id="f791a-176">You can now test user risk-based conditional access by signing in using a user with an elevated risk level.</span></span>
    
    

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="f791a-177">Sign-in risk security policy</span><span class="sxs-lookup"><span data-stu-id="f791a-177">Sign-in risk security policy</span></span>

<span data-ttu-id="f791a-178">For more information, see [User risk security policy](overview.md#user-risk-security-policy).</span><span class="sxs-lookup"><span data-stu-id="f791a-178">For more information, see [User risk security policy](overview.md#user-risk-security-policy).</span></span>

<span data-ttu-id="f791a-179">![Sign-in risk](./media/playbook/01.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="f791a-179">![Sign-in risk](./media/playbook/01.png "Playbook")</span></span>


<span data-ttu-id="f791a-180">**To test a sign in risk policy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f791a-180">**To test a sign in risk policy, perform the following steps:**</span></span>

1. <span data-ttu-id="f791a-181">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="f791a-181">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>

2. <span data-ttu-id="f791a-182">Navigate to **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="f791a-182">Navigate to **Azure AD Identity Protection**.</span></span>

3. <span data-ttu-id="f791a-183">On the main **Azure AD Identity Protection** page, click **Sign-in risk policy**.</span><span class="sxs-lookup"><span data-stu-id="f791a-183">On the main **Azure AD Identity Protection** page, click **Sign-in risk policy**.</span></span> 

4. <span data-ttu-id="f791a-184">In the **Assignments** section, select the desired users (and groups) and sign-in risk level.</span><span class="sxs-lookup"><span data-stu-id="f791a-184">In the **Assignments** section, select the desired users (and groups) and sign-in risk level.</span></span>

    <span data-ttu-id="f791a-185">![Sign-in risk](./media/playbook/04.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="f791a-185">![Sign-in risk](./media/playbook/04.png "Playbook")</span></span>


5. <span data-ttu-id="f791a-186">In the **Controls** section, select the desired Access control (for example, **Require multi-factor authentication**).</span><span class="sxs-lookup"><span data-stu-id="f791a-186">In the **Controls** section, select the desired Access control (for example, **Require multi-factor authentication**).</span></span> 

6. <span data-ttu-id="f791a-187">As **Enforce Policy**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="f791a-187">As **Enforce Policy**, select **On**.</span></span>

7. <span data-ttu-id="f791a-188">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f791a-188">Click **Save**.</span></span>

8. <span data-ttu-id="f791a-189">You can now test Sign-in Risk-based conditional access by signing in using a risky session (for example, by using the Tor browser).</span><span class="sxs-lookup"><span data-stu-id="f791a-189">You can now test Sign-in Risk-based conditional access by signing in using a risky session (for example, by using the Tor browser).</span></span> 

 




## <a name="see-also"></a><span data-ttu-id="f791a-190">See also</span><span class="sxs-lookup"><span data-stu-id="f791a-190">See also</span></span>

- [<span data-ttu-id="f791a-191">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f791a-191">Azure Active Directory Identity Protection</span></span>](../active-directory-identityprotection.md)

