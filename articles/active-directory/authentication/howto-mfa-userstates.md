---
title: Microsoft Azure Multi-Factor Authentication User States
description: Learn about user states in Azure Multi-Factor Authentication.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: b9f0571c88b6ec4aa9e3851d5bf618e5104b0652
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968123"
---
# <a name="how-to-require-two-step-verification-for-a-user"></a><span data-ttu-id="1b6eb-103">How to require two-step verification for a user</span><span class="sxs-lookup"><span data-stu-id="1b6eb-103">How to require two-step verification for a user</span></span>

<span data-ttu-id="1b6eb-104">You can take one of two approaches for requiring two-step verification.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-104">You can take one of two approaches for requiring two-step verification.</span></span> <span data-ttu-id="1b6eb-105">The first option is to enable each user for Azure Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="1b6eb-105">The first option is to enable each user for Azure Multi-Factor Authentication (MFA).</span></span> <span data-ttu-id="1b6eb-106">When users are enabled individually, they perform two-step verification each time they sign in (with some exceptions, such as when they sign in from trusted IP addresses or when the _remembered devices_ feature is turned on).</span><span class="sxs-lookup"><span data-stu-id="1b6eb-106">When users are enabled individually, they perform two-step verification each time they sign in (with some exceptions, such as when they sign in from trusted IP addresses or when the _remembered devices_ feature is turned on).</span></span> <span data-ttu-id="1b6eb-107">The second option is to set up a conditional access policy that requires two-step verification under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-107">The second option is to set up a conditional access policy that requires two-step verification under certain conditions.</span></span>

> [!TIP]
> <span data-ttu-id="1b6eb-108">Choose one of these methods to require two-step verification, not both.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-108">Choose one of these methods to require two-step verification, not both.</span></span> <span data-ttu-id="1b6eb-109">Enabling a user for Azure Multi-Factor Authentication overrides any conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-109">Enabling a user for Azure Multi-Factor Authentication overrides any conditional access policies.</span></span>

## <a name="choose-how-to-enable"></a><span data-ttu-id="1b6eb-110">Choose how to enable</span><span class="sxs-lookup"><span data-stu-id="1b6eb-110">Choose how to enable</span></span>

<span data-ttu-id="1b6eb-111">**Enabled by changing user state** - This is the traditional method for requiring two-step verification and is discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-111">**Enabled by changing user state** - This is the traditional method for requiring two-step verification and is discussed in this article.</span></span> <span data-ttu-id="1b6eb-112">It works with both Azure MFA in the cloud and Azure MFA Server.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-112">It works with both Azure MFA in the cloud and Azure MFA Server.</span></span> <span data-ttu-id="1b6eb-113">Using this method requires users to perform two-step verification **every time** they sign in and overrides conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-113">Using this method requires users to perform two-step verification **every time** they sign in and overrides conditional access policies.</span></span>

<span data-ttu-id="1b6eb-114">Enabled by conditional access policy - This is the most flexible means to enable two-step verification for your users.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-114">Enabled by conditional access policy - This is the most flexible means to enable two-step verification for your users.</span></span> <span data-ttu-id="1b6eb-115">Enabling using conditional access policy only works for Azure MFA in the cloud and is a premium feature of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-115">Enabling using conditional access policy only works for Azure MFA in the cloud and is a premium feature of Azure AD.</span></span> <span data-ttu-id="1b6eb-116">More information on this method can be found in [Deploy cloud-based Azure Multi-Factor Authentication](howto-mfa-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="1b6eb-116">More information on this method can be found in [Deploy cloud-based Azure Multi-Factor Authentication](howto-mfa-getstarted.md).</span></span>

<span data-ttu-id="1b6eb-117">Enabled by Azure AD Identity Protection - This method uses the Azure AD Identity Protection risk policy to require two-step verification based only on sign-in risk for all cloud applications.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-117">Enabled by Azure AD Identity Protection - This method uses the Azure AD Identity Protection risk policy to require two-step verification based only on sign-in risk for all cloud applications.</span></span> <span data-ttu-id="1b6eb-118">This method requires Azure Active Directory P2 licensing.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-118">This method requires Azure Active Directory P2 licensing.</span></span> <span data-ttu-id="1b6eb-119">More information on this method can be found in [Azure Active Directory Identity Protection](../identity-protection/overview.md#risky-sign-ins)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-119">More information on this method can be found in [Azure Active Directory Identity Protection](../identity-protection/overview.md#risky-sign-ins)</span></span>

> [!Note]
> <span data-ttu-id="1b6eb-120">More information about licenses and pricing can be found on the [Azure AD](https://azure.microsoft.com/pricing/details/active-directory/
) and [Multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) pricing pages.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-120">More information about licenses and pricing can be found on the [Azure AD](https://azure.microsoft.com/pricing/details/active-directory/
) and [Multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) pricing pages.</span></span>

## <a name="enable-azure-mfa-by-changing-user-status"></a><span data-ttu-id="1b6eb-121">Enable Azure MFA by changing user status</span><span class="sxs-lookup"><span data-stu-id="1b6eb-121">Enable Azure MFA by changing user status</span></span>

<span data-ttu-id="1b6eb-122">User accounts in Azure Multi-Factor Authentication have the following three distinct states:</span><span class="sxs-lookup"><span data-stu-id="1b6eb-122">User accounts in Azure Multi-Factor Authentication have the following three distinct states:</span></span>

| <span data-ttu-id="1b6eb-123">Status</span><span class="sxs-lookup"><span data-stu-id="1b6eb-123">Status</span></span> | <span data-ttu-id="1b6eb-124">Description</span><span class="sxs-lookup"><span data-stu-id="1b6eb-124">Description</span></span> | <span data-ttu-id="1b6eb-125">Non-browser apps affected</span><span class="sxs-lookup"><span data-stu-id="1b6eb-125">Non-browser apps affected</span></span> | <span data-ttu-id="1b6eb-126">Browser apps affected</span><span class="sxs-lookup"><span data-stu-id="1b6eb-126">Browser apps affected</span></span> | <span data-ttu-id="1b6eb-127">Modern authentication affected</span><span class="sxs-lookup"><span data-stu-id="1b6eb-127">Modern authentication affected</span></span> |
|:---:|:---:|:---:|:--:|:--:|
| <span data-ttu-id="1b6eb-128">Disabled</span><span class="sxs-lookup"><span data-stu-id="1b6eb-128">Disabled</span></span> |<span data-ttu-id="1b6eb-129">The default state for a new user not enrolled in Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-129">The default state for a new user not enrolled in Azure MFA.</span></span> |<span data-ttu-id="1b6eb-130">No</span><span class="sxs-lookup"><span data-stu-id="1b6eb-130">No</span></span> |<span data-ttu-id="1b6eb-131">No</span><span class="sxs-lookup"><span data-stu-id="1b6eb-131">No</span></span> |<span data-ttu-id="1b6eb-132">No</span><span class="sxs-lookup"><span data-stu-id="1b6eb-132">No</span></span> |
| <span data-ttu-id="1b6eb-133">Enabled</span><span class="sxs-lookup"><span data-stu-id="1b6eb-133">Enabled</span></span> |<span data-ttu-id="1b6eb-134">The user has been enrolled in Azure MFA, but has not registered.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-134">The user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="1b6eb-135">They receive a prompt to register the next time they sign in.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-135">They receive a prompt to register the next time they sign in.</span></span> |<span data-ttu-id="1b6eb-136">No.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-136">No.</span></span>  <span data-ttu-id="1b6eb-137">They continue to work until the registration process is completed.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-137">They continue to work until the registration process is completed.</span></span> | <span data-ttu-id="1b6eb-138">Yes.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-138">Yes.</span></span> <span data-ttu-id="1b6eb-139">After the session expires, Azure MFA registration is required.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-139">After the session expires, Azure MFA registration is required.</span></span>| <span data-ttu-id="1b6eb-140">Yes.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-140">Yes.</span></span> <span data-ttu-id="1b6eb-141">After the access token expires, Azure MFA registration is required.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-141">After the access token expires, Azure MFA registration is required.</span></span> |
| <span data-ttu-id="1b6eb-142">Enforced</span><span class="sxs-lookup"><span data-stu-id="1b6eb-142">Enforced</span></span> |<span data-ttu-id="1b6eb-143">The user has been enrolled and has completed the registration process for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-143">The user has been enrolled and has completed the registration process for Azure MFA.</span></span> |<span data-ttu-id="1b6eb-144">Yes.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-144">Yes.</span></span> <span data-ttu-id="1b6eb-145">Apps require app passwords.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-145">Apps require app passwords.</span></span> |<span data-ttu-id="1b6eb-146">Yes.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-146">Yes.</span></span> <span data-ttu-id="1b6eb-147">Azure MFA is required at login.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-147">Azure MFA is required at login.</span></span> | <span data-ttu-id="1b6eb-148">Yes.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-148">Yes.</span></span> <span data-ttu-id="1b6eb-149">Azure MFA is required at login.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-149">Azure MFA is required at login.</span></span> |

<span data-ttu-id="1b6eb-150">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed the registration process.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-150">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed the registration process.</span></span>

<span data-ttu-id="1b6eb-151">All users start out *Disabled*.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-151">All users start out *Disabled*.</span></span> <span data-ttu-id="1b6eb-152">When you enroll users in Azure MFA, their state changes to *Enabled*.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-152">When you enroll users in Azure MFA, their state changes to *Enabled*.</span></span> <span data-ttu-id="1b6eb-153">When enabled users sign in and complete the registration process, their state changes to *Enforced*.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-153">When enabled users sign in and complete the registration process, their state changes to *Enforced*.</span></span>  

### <a name="view-the-status-for-a-user"></a><span data-ttu-id="1b6eb-154">View the status for a user</span><span class="sxs-lookup"><span data-stu-id="1b6eb-154">View the status for a user</span></span>

<span data-ttu-id="1b6eb-155">Use the following steps to access the page where you can view and manage user states:</span><span class="sxs-lookup"><span data-stu-id="1b6eb-155">Use the following steps to access the page where you can view and manage user states:</span></span>

1. <span data-ttu-id="1b6eb-156">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-156">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="1b6eb-157">Go to **Azure Active Directory** > **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-157">Go to **Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="1b6eb-158">Select **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-158">Select **Multi-Factor Authentication**.</span></span>
   <span data-ttu-id="1b6eb-159">![Select Multi-Factor Authentication](./media/howto-mfa-userstates/selectmfa.png)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-159">![Select Multi-Factor Authentication](./media/howto-mfa-userstates/selectmfa.png)</span></span>
4. <span data-ttu-id="1b6eb-160">A new page that displays the user states opens.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-160">A new page that displays the user states opens.</span></span>
   <span data-ttu-id="1b6eb-161">![multi-factor authentication user status - screenshot](./media/howto-mfa-userstates/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-161">![multi-factor authentication user status - screenshot](./media/howto-mfa-userstates/userstate1.png)</span></span>

### <a name="change-the-status-for-a-user"></a><span data-ttu-id="1b6eb-162">Change the status for a user</span><span class="sxs-lookup"><span data-stu-id="1b6eb-162">Change the status for a user</span></span>

1. <span data-ttu-id="1b6eb-163">Use the preceding steps to get to the Azure Multi-Factor Authentication **users** page.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-163">Use the preceding steps to get to the Azure Multi-Factor Authentication **users** page.</span></span>
2. <span data-ttu-id="1b6eb-164">Find the user you want to enable for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-164">Find the user you want to enable for Azure MFA.</span></span> <span data-ttu-id="1b6eb-165">You might need to change the view at the top.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-165">You might need to change the view at the top.</span></span>
   <span data-ttu-id="1b6eb-166">![Find user - screenshot](./media/howto-mfa-userstates/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-166">![Find user - screenshot](./media/howto-mfa-userstates/enable1.png)</span></span>
3. <span data-ttu-id="1b6eb-167">Check the box next to their name.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-167">Check the box next to their name.</span></span>
4. <span data-ttu-id="1b6eb-168">On the right, under **quick steps**, choose **Enable** or **Disable**.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-168">On the right, under **quick steps**, choose **Enable** or **Disable**.</span></span>
   <span data-ttu-id="1b6eb-169">![Enable selected user - screenshot](./media/howto-mfa-userstates/user1.png)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-169">![Enable selected user - screenshot](./media/howto-mfa-userstates/user1.png)</span></span>

   > [!TIP]
   > <span data-ttu-id="1b6eb-170">*Enabled* users are automatically switched to *Enforced* when they register for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-170">*Enabled* users are automatically switched to *Enforced* when they register for Azure MFA.</span></span> <span data-ttu-id="1b6eb-171">Do not manually change the user state to *Enforced*.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-171">Do not manually change the user state to *Enforced*.</span></span>

5. <span data-ttu-id="1b6eb-172">Confirm your selection in the pop-up window that opens.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-172">Confirm your selection in the pop-up window that opens.</span></span>

<span data-ttu-id="1b6eb-173">After you enable users, notify them via email.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-173">After you enable users, notify them via email.</span></span> <span data-ttu-id="1b6eb-174">Tell them that they'll be asked to register the next time they sign in.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-174">Tell them that they'll be asked to register the next time they sign in.</span></span> <span data-ttu-id="1b6eb-175">Also, if your organization uses non-browser apps that don't support modern authentication, they need to create app passwords.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-175">Also, if your organization uses non-browser apps that don't support modern authentication, they need to create app passwords.</span></span> <span data-ttu-id="1b6eb-176">You can also include a link to the [Azure MFA end-user guide](../user-help/multi-factor-authentication-end-user.md) to help them get started.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-176">You can also include a link to the [Azure MFA end-user guide](../user-help/multi-factor-authentication-end-user.md) to help them get started.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="1b6eb-177">Use PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b6eb-177">Use PowerShell</span></span>

<span data-ttu-id="1b6eb-178">To change the user state by using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-178">To change the user state by using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span></span> <span data-ttu-id="1b6eb-179">There are three possible states:</span><span class="sxs-lookup"><span data-stu-id="1b6eb-179">There are three possible states:</span></span>

* <span data-ttu-id="1b6eb-180">Enabled</span><span class="sxs-lookup"><span data-stu-id="1b6eb-180">Enabled</span></span>
* <span data-ttu-id="1b6eb-181">Enforced</span><span class="sxs-lookup"><span data-stu-id="1b6eb-181">Enforced</span></span>
* <span data-ttu-id="1b6eb-182">Disabled</span><span class="sxs-lookup"><span data-stu-id="1b6eb-182">Disabled</span></span>  

<span data-ttu-id="1b6eb-183">Don't move users directly to the *Enforced* state.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-183">Don't move users directly to the *Enforced* state.</span></span> <span data-ttu-id="1b6eb-184">If you do, non-browser-based apps stop working because the user has not gone through Azure MFA registration and obtained an [app password](howto-mfa-mfasettings.md#app-passwords).</span><span class="sxs-lookup"><span data-stu-id="1b6eb-184">If you do, non-browser-based apps stop working because the user has not gone through Azure MFA registration and obtained an [app password](howto-mfa-mfasettings.md#app-passwords).</span></span>

<span data-ttu-id="1b6eb-185">Using PowerShell is a good option when you need to bulk enabling users.</span><span class="sxs-lookup"><span data-stu-id="1b6eb-185">Using PowerShell is a good option when you need to bulk enabling users.</span></span> <span data-ttu-id="1b6eb-186">Create a PowerShell script that loops through a list of users and enables them:</span><span class="sxs-lookup"><span data-stu-id="1b6eb-186">Create a PowerShell script that loops through a list of users and enables them:</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="1b6eb-187">The following script is an example:</span><span class="sxs-lookup"><span data-stu-id="1b6eb-187">The following script is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="next-steps"></a><span data-ttu-id="1b6eb-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b6eb-188">Next steps</span></span>

<span data-ttu-id="1b6eb-189">To configure additional settings like trusted IPs, custom voice messages, and fraud alerts, see the article [Configure Azure Multi-Factor Authentication settings](howto-mfa-mfasettings.md)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-189">To configure additional settings like trusted IPs, custom voice messages, and fraud alerts, see the article [Configure Azure Multi-Factor Authentication settings](howto-mfa-mfasettings.md)</span></span>

<span data-ttu-id="1b6eb-190">Information about managing user settings for Azure Multi-Factor Authentication can be found in the article [Manage user settings with Azure Multi-Factor Authentication in the cloud](howto-mfa-userdevicesettings.md)</span><span class="sxs-lookup"><span data-stu-id="1b6eb-190">Information about managing user settings for Azure Multi-Factor Authentication can be found in the article [Manage user settings with Azure Multi-Factor Authentication in the cloud](howto-mfa-userdevicesettings.md)</span></span>
