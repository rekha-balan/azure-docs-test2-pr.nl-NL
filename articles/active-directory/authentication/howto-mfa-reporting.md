---
title: Access and usage reports for Azure MFA | Microsoft Docs
description: This describes how to use the Azure Multi-Factor Authentication feature - reports.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/30/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: dc4cd28fe61c422f65f47c74c7cbc4686d73ab77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867972"
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="8862a-103">Reports in Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-103">Reports in Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="8862a-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization accessible through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8862a-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization accessible through the Azure portal.</span></span> <span data-ttu-id="8862a-105">The following table lists the available reports:</span><span class="sxs-lookup"><span data-stu-id="8862a-105">The following table lists the available reports:</span></span>

| <span data-ttu-id="8862a-106">Report</span><span class="sxs-lookup"><span data-stu-id="8862a-106">Report</span></span> | <span data-ttu-id="8862a-107">Location</span><span class="sxs-lookup"><span data-stu-id="8862a-107">Location</span></span> | <span data-ttu-id="8862a-108">Description</span><span class="sxs-lookup"><span data-stu-id="8862a-108">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8862a-109">Blocked User History</span><span class="sxs-lookup"><span data-stu-id="8862a-109">Blocked User History</span></span> | <span data-ttu-id="8862a-110">Azure AD > MFA Server > Block/unblock users</span><span class="sxs-lookup"><span data-stu-id="8862a-110">Azure AD > MFA Server > Block/unblock users</span></span> | <span data-ttu-id="8862a-111">Shows the history of requests to block or unblock users.</span><span class="sxs-lookup"><span data-stu-id="8862a-111">Shows the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="8862a-112">Usage and fraud alerts</span><span class="sxs-lookup"><span data-stu-id="8862a-112">Usage and fraud alerts</span></span> | <span data-ttu-id="8862a-113">Azure AD > Sign-ins</span><span class="sxs-lookup"><span data-stu-id="8862a-113">Azure AD > Sign-ins</span></span> | <span data-ttu-id="8862a-114">Provides information on overall usage, user summary, and user details; as well as a history of fraud alerts submitted during the date range specified.</span><span class="sxs-lookup"><span data-stu-id="8862a-114">Provides information on overall usage, user summary, and user details; as well as a history of fraud alerts submitted during the date range specified.</span></span> |
| <span data-ttu-id="8862a-115">Usage for on-premises components</span><span class="sxs-lookup"><span data-stu-id="8862a-115">Usage for on-premises components</span></span> | <span data-ttu-id="8862a-116">Azure AD > MFA Server > Activity Report</span><span class="sxs-lookup"><span data-stu-id="8862a-116">Azure AD > MFA Server > Activity Report</span></span> | <span data-ttu-id="8862a-117">Provides information on overall usage for MFA through the NPS extension, ADFS, and MFA server.</span><span class="sxs-lookup"><span data-stu-id="8862a-117">Provides information on overall usage for MFA through the NPS extension, ADFS, and MFA server.</span></span> |
| <span data-ttu-id="8862a-118">Bypassed User History</span><span class="sxs-lookup"><span data-stu-id="8862a-118">Bypassed User History</span></span> | <span data-ttu-id="8862a-119">Azure AD > MFA Server > One-time bypass</span><span class="sxs-lookup"><span data-stu-id="8862a-119">Azure AD > MFA Server > One-time bypass</span></span> | <span data-ttu-id="8862a-120">Provides a history of requests to bypass Multi-Factor Authentication for a user.</span><span class="sxs-lookup"><span data-stu-id="8862a-120">Provides a history of requests to bypass Multi-Factor Authentication for a user.</span></span> |
| <span data-ttu-id="8862a-121">Server status</span><span class="sxs-lookup"><span data-stu-id="8862a-121">Server status</span></span> | <span data-ttu-id="8862a-122">Azure AD > MFA Server > Server status</span><span class="sxs-lookup"><span data-stu-id="8862a-122">Azure AD > MFA Server > Server status</span></span> | <span data-ttu-id="8862a-123">Displays the status of Multi-Factor Authentication Servers associated with your account.</span><span class="sxs-lookup"><span data-stu-id="8862a-123">Displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |

## <a name="view-mfa-reports"></a><span data-ttu-id="8862a-124">View MFA reports</span><span class="sxs-lookup"><span data-stu-id="8862a-124">View MFA reports</span></span>

1. <span data-ttu-id="8862a-125">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8862a-125">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8862a-126">On the left, select **Azure Active Directory** > **MFA Server**.</span><span class="sxs-lookup"><span data-stu-id="8862a-126">On the left, select **Azure Active Directory** > **MFA Server**.</span></span>
3. <span data-ttu-id="8862a-127">Select the report that you wish to view.</span><span class="sxs-lookup"><span data-stu-id="8862a-127">Select the report that you wish to view.</span></span>

   <span data-ttu-id="8862a-128"><center>![Cloud](./media/howto-mfa-reporting/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="8862a-128"><center>![Cloud](./media/howto-mfa-reporting/report.png)</center></span></span>

## <a name="azure-ad-sign-ins-report"></a><span data-ttu-id="8862a-129">Azure AD sign-ins report</span><span class="sxs-lookup"><span data-stu-id="8862a-129">Azure AD sign-ins report</span></span>

<span data-ttu-id="8862a-130">With the **sign-ins activity report** in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="8862a-130">With the **sign-ins activity report** in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="8862a-131">The sign-ins report can provide you with information about the usage of managed applications and user sign-in activities, which includes information about multi-factor authentication (MFA) usage.</span><span class="sxs-lookup"><span data-stu-id="8862a-131">The sign-ins report can provide you with information about the usage of managed applications and user sign-in activities, which includes information about multi-factor authentication (MFA) usage.</span></span> <span data-ttu-id="8862a-132">The MFA data gives you insights into how MFA is working in your organization.</span><span class="sxs-lookup"><span data-stu-id="8862a-132">The MFA data gives you insights into how MFA is working in your organization.</span></span> <span data-ttu-id="8862a-133">It enables you to answer questions like:</span><span class="sxs-lookup"><span data-stu-id="8862a-133">It enables you to answer questions like:</span></span>

- <span data-ttu-id="8862a-134">Was the sign-in challenged with MFA?</span><span class="sxs-lookup"><span data-stu-id="8862a-134">Was the sign-in challenged with MFA?</span></span>
- <span data-ttu-id="8862a-135">How did the user complete MFA?</span><span class="sxs-lookup"><span data-stu-id="8862a-135">How did the user complete MFA?</span></span>
- <span data-ttu-id="8862a-136">Why was the user unable to complete MFA?</span><span class="sxs-lookup"><span data-stu-id="8862a-136">Why was the user unable to complete MFA?</span></span>
- <span data-ttu-id="8862a-137">How many users are challenged for MFA?</span><span class="sxs-lookup"><span data-stu-id="8862a-137">How many users are challenged for MFA?</span></span>
- <span data-ttu-id="8862a-138">How many users are unable to complete the MFA challenge?</span><span class="sxs-lookup"><span data-stu-id="8862a-138">How many users are unable to complete the MFA challenge?</span></span>
- <span data-ttu-id="8862a-139">What are the common MFA issues end users are running into?</span><span class="sxs-lookup"><span data-stu-id="8862a-139">What are the common MFA issues end users are running into?</span></span>

<span data-ttu-id="8862a-140">This data is available through the [Azure portal](https://portal.azure.com) and the [reporting API](../reports-monitoring/concept-reporting-api.md).</span><span class="sxs-lookup"><span data-stu-id="8862a-140">This data is available through the [Azure portal](https://portal.azure.com) and the [reporting API](../reports-monitoring/concept-reporting-api.md).</span></span>

![Cloud](./media/howto-mfa-reporting/sign-in-report.png)

### <a name="sign-ins-report-structure"></a><span data-ttu-id="8862a-142">Sign-ins report structure</span><span class="sxs-lookup"><span data-stu-id="8862a-142">Sign-ins report structure</span></span>

<span data-ttu-id="8862a-143">The sign-in activity reports for MFA give you access to the following information:</span><span class="sxs-lookup"><span data-stu-id="8862a-143">The sign-in activity reports for MFA give you access to the following information:</span></span>

<span data-ttu-id="8862a-144">**MFA required:** Whether MFA is required for the sign-in or not.</span><span class="sxs-lookup"><span data-stu-id="8862a-144">**MFA required:** Whether MFA is required for the sign-in or not.</span></span> <span data-ttu-id="8862a-145">MFA can be required due to per-user MFA, conditional access, or other reasons.</span><span class="sxs-lookup"><span data-stu-id="8862a-145">MFA can be required due to per-user MFA, conditional access, or other reasons.</span></span> <span data-ttu-id="8862a-146">Possible values are **Yes** or **No**.</span><span class="sxs-lookup"><span data-stu-id="8862a-146">Possible values are **Yes** or **No**.</span></span>

<span data-ttu-id="8862a-147">**MFA Result:** More information on whether MFA was satisfied or denied:</span><span class="sxs-lookup"><span data-stu-id="8862a-147">**MFA Result:** More information on whether MFA was satisfied or denied:</span></span>

- <span data-ttu-id="8862a-148">If MFA was satisfied, this column provides more information about how MFA was satisfied.</span><span class="sxs-lookup"><span data-stu-id="8862a-148">If MFA was satisfied, this column provides more information about how MFA was satisfied.</span></span>
   - <span data-ttu-id="8862a-149">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-149">Azure Multi-Factor Authentication</span></span>
      - <span data-ttu-id="8862a-150">completed in the cloud</span><span class="sxs-lookup"><span data-stu-id="8862a-150">completed in the cloud</span></span>
      - <span data-ttu-id="8862a-151">has expired due to the policies configured on tenant</span><span class="sxs-lookup"><span data-stu-id="8862a-151">has expired due to the policies configured on tenant</span></span>
      - <span data-ttu-id="8862a-152">registration prompted</span><span class="sxs-lookup"><span data-stu-id="8862a-152">registration prompted</span></span>
      - <span data-ttu-id="8862a-153">satisfied by claim in the token</span><span class="sxs-lookup"><span data-stu-id="8862a-153">satisfied by claim in the token</span></span>
      - <span data-ttu-id="8862a-154">satisfied by claim provided by external provider</span><span class="sxs-lookup"><span data-stu-id="8862a-154">satisfied by claim provided by external provider</span></span>
      - <span data-ttu-id="8862a-155">satisfied by strong authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-155">satisfied by strong authentication</span></span>
      - <span data-ttu-id="8862a-156">skipped as flow exercised was Windows broker logon flow</span><span class="sxs-lookup"><span data-stu-id="8862a-156">skipped as flow exercised was Windows broker logon flow</span></span>
      - <span data-ttu-id="8862a-157">skipped due to app password</span><span class="sxs-lookup"><span data-stu-id="8862a-157">skipped due to app password</span></span>
      - <span data-ttu-id="8862a-158">skipped due to location</span><span class="sxs-lookup"><span data-stu-id="8862a-158">skipped due to location</span></span>
      - <span data-ttu-id="8862a-159">skipped due to registered device</span><span class="sxs-lookup"><span data-stu-id="8862a-159">skipped due to registered device</span></span>
      - <span data-ttu-id="8862a-160">skipped due to remembered device</span><span class="sxs-lookup"><span data-stu-id="8862a-160">skipped due to remembered device</span></span>
      - <span data-ttu-id="8862a-161">successfully completed</span><span class="sxs-lookup"><span data-stu-id="8862a-161">successfully completed</span></span>
   - <span data-ttu-id="8862a-162">Redirected to external provider for multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-162">Redirected to external provider for multi-factor authentication</span></span>

- <span data-ttu-id="8862a-163">If MFA was denied, this column would provide the reason for denial.</span><span class="sxs-lookup"><span data-stu-id="8862a-163">If MFA was denied, this column would provide the reason for denial.</span></span>
   - <span data-ttu-id="8862a-164">Azure Multi-Factor Authentication denied;</span><span class="sxs-lookup"><span data-stu-id="8862a-164">Azure Multi-Factor Authentication denied;</span></span>
      - <span data-ttu-id="8862a-165">authentication in-progress</span><span class="sxs-lookup"><span data-stu-id="8862a-165">authentication in-progress</span></span>
      - <span data-ttu-id="8862a-166">duplicate authentication attempt</span><span class="sxs-lookup"><span data-stu-id="8862a-166">duplicate authentication attempt</span></span>
      - <span data-ttu-id="8862a-167">entered incorrect code too many times</span><span class="sxs-lookup"><span data-stu-id="8862a-167">entered incorrect code too many times</span></span>
      - <span data-ttu-id="8862a-168">invalid authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-168">invalid authentication</span></span>
      - <span data-ttu-id="8862a-169">invalid mobile app verification code</span><span class="sxs-lookup"><span data-stu-id="8862a-169">invalid mobile app verification code</span></span>
      - <span data-ttu-id="8862a-170">misconfiguration</span><span class="sxs-lookup"><span data-stu-id="8862a-170">misconfiguration</span></span>
      - <span data-ttu-id="8862a-171">phone call went to voicemail</span><span class="sxs-lookup"><span data-stu-id="8862a-171">phone call went to voicemail</span></span>
      - <span data-ttu-id="8862a-172">phone number has an invalid format</span><span class="sxs-lookup"><span data-stu-id="8862a-172">phone number has an invalid format</span></span>
      - <span data-ttu-id="8862a-173">service error</span><span class="sxs-lookup"><span data-stu-id="8862a-173">service error</span></span>
      - <span data-ttu-id="8862a-174">unable to reach the user’s phone</span><span class="sxs-lookup"><span data-stu-id="8862a-174">unable to reach the user’s phone</span></span>
      - <span data-ttu-id="8862a-175">unable to send the mobile app notification to the device</span><span class="sxs-lookup"><span data-stu-id="8862a-175">unable to send the mobile app notification to the device</span></span>
      - <span data-ttu-id="8862a-176">unable to send the mobile app notification</span><span class="sxs-lookup"><span data-stu-id="8862a-176">unable to send the mobile app notification</span></span>
      - <span data-ttu-id="8862a-177">user declined the authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-177">user declined the authentication</span></span>
      - <span data-ttu-id="8862a-178">user did not respond to mobile app notification</span><span class="sxs-lookup"><span data-stu-id="8862a-178">user did not respond to mobile app notification</span></span>
      - <span data-ttu-id="8862a-179">user does not have any verification methods registered</span><span class="sxs-lookup"><span data-stu-id="8862a-179">user does not have any verification methods registered</span></span>
      - <span data-ttu-id="8862a-180">user entered incorrect code</span><span class="sxs-lookup"><span data-stu-id="8862a-180">user entered incorrect code</span></span>
      - <span data-ttu-id="8862a-181">user entered incorrect PIN</span><span class="sxs-lookup"><span data-stu-id="8862a-181">user entered incorrect PIN</span></span>
      - <span data-ttu-id="8862a-182">user hung up the phone call without succeeding the authentication</span><span class="sxs-lookup"><span data-stu-id="8862a-182">user hung up the phone call without succeeding the authentication</span></span>
      - <span data-ttu-id="8862a-183">user is blocked</span><span class="sxs-lookup"><span data-stu-id="8862a-183">user is blocked</span></span>
      - <span data-ttu-id="8862a-184">user never entered the verification code</span><span class="sxs-lookup"><span data-stu-id="8862a-184">user never entered the verification code</span></span>
      - <span data-ttu-id="8862a-185">user not found</span><span class="sxs-lookup"><span data-stu-id="8862a-185">user not found</span></span>
      - <span data-ttu-id="8862a-186">verification code already used once</span><span class="sxs-lookup"><span data-stu-id="8862a-186">verification code already used once</span></span>

<span data-ttu-id="8862a-187">**MFA authentication method:** The authentication method the user used to complete MFA.</span><span class="sxs-lookup"><span data-stu-id="8862a-187">**MFA authentication method:** The authentication method the user used to complete MFA.</span></span> <span data-ttu-id="8862a-188">Possible values include:</span><span class="sxs-lookup"><span data-stu-id="8862a-188">Possible values include:</span></span>

- <span data-ttu-id="8862a-189">Text message</span><span class="sxs-lookup"><span data-stu-id="8862a-189">Text message</span></span>
- <span data-ttu-id="8862a-190">Mobile app notification</span><span class="sxs-lookup"><span data-stu-id="8862a-190">Mobile app notification</span></span>
- <span data-ttu-id="8862a-191">Phone call (Authentication phone)</span><span class="sxs-lookup"><span data-stu-id="8862a-191">Phone call (Authentication phone)</span></span>
- <span data-ttu-id="8862a-192">Mobile app verification code</span><span class="sxs-lookup"><span data-stu-id="8862a-192">Mobile app verification code</span></span>
- <span data-ttu-id="8862a-193">Phone call (Office phone)</span><span class="sxs-lookup"><span data-stu-id="8862a-193">Phone call (Office phone)</span></span>
- <span data-ttu-id="8862a-194">Phone call (Alternate authentication phone)</span><span class="sxs-lookup"><span data-stu-id="8862a-194">Phone call (Alternate authentication phone)</span></span>

<span data-ttu-id="8862a-195">**MFA authentication detail:** Scrubbed version of the phone number, for example: +X XXXXXXXX64.</span><span class="sxs-lookup"><span data-stu-id="8862a-195">**MFA authentication detail:** Scrubbed version of the phone number, for example: +X XXXXXXXX64.</span></span>

<span data-ttu-id="8862a-196">**Conditional Access** Find information about conditional access policies that affected the sign-in attempt including:</span><span class="sxs-lookup"><span data-stu-id="8862a-196">**Conditional Access** Find information about conditional access policies that affected the sign-in attempt including:</span></span>

- <span data-ttu-id="8862a-197">Policy name</span><span class="sxs-lookup"><span data-stu-id="8862a-197">Policy name</span></span>
- <span data-ttu-id="8862a-198">Grant controls</span><span class="sxs-lookup"><span data-stu-id="8862a-198">Grant controls</span></span>
- <span data-ttu-id="8862a-199">Session controls</span><span class="sxs-lookup"><span data-stu-id="8862a-199">Session controls</span></span>
- <span data-ttu-id="8862a-200">Result</span><span class="sxs-lookup"><span data-stu-id="8862a-200">Result</span></span>

## <a name="powershell-reporting"></a><span data-ttu-id="8862a-201">PowerShell reporting</span><span class="sxs-lookup"><span data-stu-id="8862a-201">PowerShell reporting</span></span>

<span data-ttu-id="8862a-202">Identify users who have registered for MFA using the PowerShell that follows.</span><span class="sxs-lookup"><span data-stu-id="8862a-202">Identify users who have registered for MFA using the PowerShell that follows.</span></span>

```Get-MsolUser -All | where {$_.StrongAuthenticationMethods -ne $null} | Select-Object -Property UserPrincipalName```

<span data-ttu-id="8862a-203">Identify users who have not registered for MFA using the PowerShell that follows.</span><span class="sxs-lookup"><span data-stu-id="8862a-203">Identify users who have not registered for MFA using the PowerShell that follows.</span></span>

```Get-MsolUser -All | where {$_.StrongAuthenticationMethods.Count -eq 0} | Select-Object -Property UserPrincipalName```

## <a name="next-steps"></a><span data-ttu-id="8862a-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="8862a-204">Next steps</span></span>

* [<span data-ttu-id="8862a-205">For Users</span><span class="sxs-lookup"><span data-stu-id="8862a-205">For Users</span></span>](../user-help/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="8862a-206">Where to deploy</span><span class="sxs-lookup"><span data-stu-id="8862a-206">Where to deploy</span></span>](concept-mfa-whichversion.md)
