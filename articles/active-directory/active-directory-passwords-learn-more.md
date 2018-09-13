---
title: 'Learn more: Azure Active Directory password management | Microsoft Docs'
description: Advanced topics on Azure AD password management, including how password writeback works, password writeback security, how the password reset portal works, and what data is used by password reset.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
editor: curtand
ms.assetid: d3be2912-76c8-40a0-9507-b7b1a7ce2f8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: joflore
ms.openlocfilehash: 0ba4b345f66dfcb70358a2c8345347f3908ebb63
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549474"
---
# <a name="learn-more-about-password-management"></a><span data-ttu-id="5b952-103">Learn more about password management</span><span class="sxs-lookup"><span data-stu-id="5b952-103">Learn more about password management</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5b952-104">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="5b952-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="5b952-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="5b952-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
>
>

<span data-ttu-id="5b952-106">If you have already deployed password management, or are just looking to learn more about the technical nitty gritty of how it works before deploying, this section will give you a good overview of the technical concepts behind the service.</span><span class="sxs-lookup"><span data-stu-id="5b952-106">If you have already deployed password management, or are just looking to learn more about the technical nitty gritty of how it works before deploying, this section will give you a good overview of the technical concepts behind the service.</span></span> <span data-ttu-id="5b952-107">We'll cover the following:</span><span class="sxs-lookup"><span data-stu-id="5b952-107">We'll cover the following:</span></span>

* [<span data-ttu-id="5b952-108">**How does the password reset portal work?**</span><span class="sxs-lookup"><span data-stu-id="5b952-108">**How does the password reset portal work?**</span></span>](#how-does-the-password-reset-portal-work)
* [<span data-ttu-id="5b952-109">**Password writeback overview**</span><span class="sxs-lookup"><span data-stu-id="5b952-109">**Password writeback overview**</span></span>](#password-writeback-overview)
 * [<span data-ttu-id="5b952-110">How pasword writeback works</span><span class="sxs-lookup"><span data-stu-id="5b952-110">How pasword writeback works</span></span>](#how-password-writeback-works)
* [<span data-ttu-id="5b952-111">**Scenarios supported for password writeback**</span><span class="sxs-lookup"><span data-stu-id="5b952-111">**Scenarios supported for password writeback**</span></span>](#scenarios-supported-for-password-writeback)
 * [<span data-ttu-id="5b952-112">Supported Azure AD Connect, Azure AD Sync, and DirSync client</span><span class="sxs-lookup"><span data-stu-id="5b952-112">Supported Azure AD Connect, Azure AD Sync, and DirSync client</span></span>](#supported-clients)
 * [<span data-ttu-id="5b952-113">Licenses required for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-113">Licenses required for password writeback</span></span>](#licenses-required-for-password-writeback)
 * [<span data-ttu-id="5b952-114">On-premises authentication modes supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-114">On-premises authentication modes supported for password writeback</span></span>](#on-premises-authentication-modes-supported-for-password-writeback)
 * [<span data-ttu-id="5b952-115">User and Admin operations supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-115">User and Admin operations supported for password writeback</span></span>](#user-and-admin-operations-supported-for-password-writeback)
 * [<span data-ttu-id="5b952-116">User and Admin operations not supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-116">User and Admin operations not supported for password writeback</span></span>](#user-and-admin-operations-not-supported-for-password-writeback)
* [<span data-ttu-id="5b952-117">**Password writeback security model**</span><span class="sxs-lookup"><span data-stu-id="5b952-117">**Password writeback security model**</span></span>](#password-writeback-security-model)
 * [<span data-ttu-id="5b952-118">Password writeback encryption details</span><span class="sxs-lookup"><span data-stu-id="5b952-118">Password writeback encryption details</span></span>](#password-writeback-encryption-details)
 * [<span data-ttu-id="5b952-119">Password writeback bandwidth usage</span><span class="sxs-lookup"><span data-stu-id="5b952-119">Password writeback bandwidth usage</span></span>](#password-writeback-bandwidth-usage)
* [<span data-ttu-id="5b952-120">**Deploying, managing, and accessing password reset data for your users**</span><span class="sxs-lookup"><span data-stu-id="5b952-120">**Deploying, managing, and accessing password reset data for your users**</span></span>](#deploying-managing-and-accessing-password-reset-data-for-your-users)
 * [<span data-ttu-id="5b952-121">What data is used by password reset?</span><span class="sxs-lookup"><span data-stu-id="5b952-121">What data is used by password reset?</span></span>](#what-data-is-used-by-password-reset)
 * [<span data-ttu-id="5b952-122">Deploying password reset without requiring end user registration</span><span class="sxs-lookup"><span data-stu-id="5b952-122">Deploying password reset without requiring end user registration</span></span>](#deploying-password-reset-without-requiring-end-user-registration)
 * [<span data-ttu-id="5b952-123">What happens when a user registers for password reset?</span><span class="sxs-lookup"><span data-stu-id="5b952-123">What happens when a user registers for password reset?</span></span>](#what-happens-when-a-user-registers)
 * [<span data-ttu-id="5b952-124">How to access password reset data for your users</span><span class="sxs-lookup"><span data-stu-id="5b952-124">How to access password reset data for your users</span></span>](#how-to-access-password-reset-data-for-your-users)
 * [<span data-ttu-id="5b952-125">Setting password reset data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-125">Setting password reset data with PowerShell</span></span>](#setting-password-reset-data-with-powershell)
 * [<span data-ttu-id="5b952-126">Reading password reset data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-126">Reading password reset data with PowerShell</span></span>](#reading-password-reset-data-with-powershell)
* [<span data-ttu-id="5b952-127">**How does Password Reset work for B2B users?**</span><span class="sxs-lookup"><span data-stu-id="5b952-127">**How does Password Reset work for B2B users?**</span></span>](#how-does-password-reset-work-for-b2b-users)

## <a name="how-does-the-password-reset-portal-work"></a><span data-ttu-id="5b952-128">How does the password reset portal work?</span><span class="sxs-lookup"><span data-stu-id="5b952-128">How does the password reset portal work?</span></span>
<span data-ttu-id="5b952-129">When a user navigates to the password reset portal, a workflow is kicked off to determine if that user account is valid, what organization that users belongs to, where that user’s password is managed, and whether or not the user is licensed to use the feature.</span><span class="sxs-lookup"><span data-stu-id="5b952-129">When a user navigates to the password reset portal, a workflow is kicked off to determine if that user account is valid, what organization that users belongs to, where that user’s password is managed, and whether or not the user is licensed to use the feature.</span></span>  <span data-ttu-id="5b952-130">Read through the steps below to learn about the logic behind the password reset page.</span><span class="sxs-lookup"><span data-stu-id="5b952-130">Read through the steps below to learn about the logic behind the password reset page.</span></span>

1. <span data-ttu-id="5b952-131">User clicks on the Can’t access your account link or goes directly to [https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).</span><span class="sxs-lookup"><span data-stu-id="5b952-131">User clicks on the Can’t access your account link or goes directly to [https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).</span></span>
2. <span data-ttu-id="5b952-132">User enters a user id and passes a captcha.</span><span class="sxs-lookup"><span data-stu-id="5b952-132">User enters a user id and passes a captcha.</span></span>
3. <span data-ttu-id="5b952-133">Azure AD verifies if the user is able to use this feature by doing the following:</span><span class="sxs-lookup"><span data-stu-id="5b952-133">Azure AD verifies if the user is able to use this feature by doing the following:</span></span>
   * <span data-ttu-id="5b952-134">Checks that the user has this feature enabled and an Azure AD license assigned.</span><span class="sxs-lookup"><span data-stu-id="5b952-134">Checks that the user has this feature enabled and an Azure AD license assigned.</span></span>
     * <span data-ttu-id="5b952-135">If the user does not have this feature enabled or a license assigned, the user is asked to contact his or her administrator to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="5b952-135">If the user does not have this feature enabled or a license assigned, the user is asked to contact his or her administrator to reset his or her password.</span></span>
   * <span data-ttu-id="5b952-136">Checks that the user has the right challenge data defined on his or her account in accordance with administrator policy.</span><span class="sxs-lookup"><span data-stu-id="5b952-136">Checks that the user has the right challenge data defined on his or her account in accordance with administrator policy.</span></span>
     * <span data-ttu-id="5b952-137">If policy requires only one challenge, then it is ensured that the user has the appropriate data defined for at least one of the challenges enabled by the administrator policy.</span><span class="sxs-lookup"><span data-stu-id="5b952-137">If policy requires only one challenge, then it is ensured that the user has the appropriate data defined for at least one of the challenges enabled by the administrator policy.</span></span>
       * <span data-ttu-id="5b952-138">If the user is not configured, then the user is advised to contact his or her administrator to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="5b952-138">If the user is not configured, then the user is advised to contact his or her administrator to reset his or her password.</span></span>
     * <span data-ttu-id="5b952-139">If the policy requires two challenges, then it is ensured that the user has the appropriate data defined for at least two of the challenges enabled by the administrator policy.</span><span class="sxs-lookup"><span data-stu-id="5b952-139">If the policy requires two challenges, then it is ensured that the user has the appropriate data defined for at least two of the challenges enabled by the administrator policy.</span></span>
       * <span data-ttu-id="5b952-140">If the user is not configured, then we the user is advised to contact his or her administrator to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="5b952-140">If the user is not configured, then we the user is advised to contact his or her administrator to reset his or her password.</span></span>
   * <span data-ttu-id="5b952-141">Checks whether or not the user’s password is managed on premises (federated or password hash sync’d).</span><span class="sxs-lookup"><span data-stu-id="5b952-141">Checks whether or not the user’s password is managed on premises (federated or password hash sync’d).</span></span>
     * <span data-ttu-id="5b952-142">If writeback is deployed and the user’s password is managed on premises, then the user is allowed to proceed to authenticate and reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="5b952-142">If writeback is deployed and the user’s password is managed on premises, then the user is allowed to proceed to authenticate and reset his or her password.</span></span>
     * <span data-ttu-id="5b952-143">If writeback is not deployed and the user’s password is managed on premises, then the user is asked to contact his or her administrator to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="5b952-143">If writeback is not deployed and the user’s password is managed on premises, then the user is asked to contact his or her administrator to reset his or her password.</span></span>
4. <span data-ttu-id="5b952-144">If it is determined that the user is able to successfully reset his or her password, then the user is guided through the reset process.</span><span class="sxs-lookup"><span data-stu-id="5b952-144">If it is determined that the user is able to successfully reset his or her password, then the user is guided through the reset process.</span></span>

<span data-ttu-id="5b952-145">Learn more about how to deploy password writeback at [Getting Started: Azure AD password management](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5b952-145">Learn more about how to deploy password writeback at [Getting Started: Azure AD password management](active-directory-passwords-getting-started.md).</span></span>

## <a name="password-writeback-overview"></a><span data-ttu-id="5b952-146">Password writeback overview</span><span class="sxs-lookup"><span data-stu-id="5b952-146">Password writeback overview</span></span>
<span data-ttu-id="5b952-147">Password writeback is an [Azure Active Directory Connect](connect/active-directory-aadconnect.md) component that can be enabled and used by the current subscribers of Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="5b952-147">Password writeback is an [Azure Active Directory Connect](connect/active-directory-aadconnect.md) component that can be enabled and used by the current subscribers of Azure Active Directory Premium.</span></span> <span data-ttu-id="5b952-148">For more information, see [Azure Active Directory Editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="5b952-148">For more information, see [Azure Active Directory Editions](active-directory-editions.md).</span></span>

<span data-ttu-id="5b952-149">Password writeback allows you to configure your cloud tenant to write passwords back to you on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b952-149">Password writeback allows you to configure your cloud tenant to write passwords back to you on-premises Active Directory.</span></span>  <span data-ttu-id="5b952-150">It obviates you from having to set up and manage a complicated on-premises self-service password reset solution, and it provides a convenient cloud-based way for your users to reset their on-premises passwords wherever they are.</span><span class="sxs-lookup"><span data-stu-id="5b952-150">It obviates you from having to set up and manage a complicated on-premises self-service password reset solution, and it provides a convenient cloud-based way for your users to reset their on-premises passwords wherever they are.</span></span>  <span data-ttu-id="5b952-151">Read on for some of the key features of password writeback:</span><span class="sxs-lookup"><span data-stu-id="5b952-151">Read on for some of the key features of password writeback:</span></span>

* <span data-ttu-id="5b952-152">**Zero delay feedback.**</span><span class="sxs-lookup"><span data-stu-id="5b952-152">**Zero delay feedback.**</span></span>  <span data-ttu-id="5b952-153">Password writeback is a synchronous operation.</span><span class="sxs-lookup"><span data-stu-id="5b952-153">Password writeback is a synchronous operation.</span></span>  <span data-ttu-id="5b952-154">Your users will be notified immediately if their password did not meet policy or was not able to be reset or changed for any reason.</span><span class="sxs-lookup"><span data-stu-id="5b952-154">Your users will be notified immediately if their password did not meet policy or was not able to be reset or changed for any reason.</span></span>
* <span data-ttu-id="5b952-155">**Supports resetting passwords for users using AD FS or other federation technologies.**</span><span class="sxs-lookup"><span data-stu-id="5b952-155">**Supports resetting passwords for users using AD FS or other federation technologies.**</span></span>  <span data-ttu-id="5b952-156">With password writeback, as long as the federated user accounts are synchronized into your Azure AD tenant, they will be able to manage their on-premises AD passwords from the cloud.</span><span class="sxs-lookup"><span data-stu-id="5b952-156">With password writeback, as long as the federated user accounts are synchronized into your Azure AD tenant, they will be able to manage their on-premises AD passwords from the cloud.</span></span>
* <span data-ttu-id="5b952-157">**Supports resetting passwords for users using password hash sync.** When the password reset service detects that a synchronized user account is enabled for password hash sync, we reset both this account’s on-premises and cloud password simultaneously.</span><span class="sxs-lookup"><span data-stu-id="5b952-157">**Supports resetting passwords for users using password hash sync.** When the password reset service detects that a synchronized user account is enabled for password hash sync, we reset both this account’s on-premises and cloud password simultaneously.</span></span>
* <span data-ttu-id="5b952-158">**Supports changing passwords from the access panel and Office 365.**</span><span class="sxs-lookup"><span data-stu-id="5b952-158">**Supports changing passwords from the access panel and Office 365.**</span></span>  <span data-ttu-id="5b952-159">When federated or password sync’d users come to change their expired or non-expired passwords, we’ll write those passwords back to your local AD environment.</span><span class="sxs-lookup"><span data-stu-id="5b952-159">When federated or password sync’d users come to change their expired or non-expired passwords, we’ll write those passwords back to your local AD environment.</span></span>
* <span data-ttu-id="5b952-160">**Supports writing back passwords when an admin reset them from the** [**Azure Management Portal**](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5b952-160">**Supports writing back passwords when an admin reset them from the** [**Azure Management Portal**](https://manage.windowsazure.com).</span></span>  <span data-ttu-id="5b952-161">Whenever an admin resets a user’s password in the [Azure Management Portal](https://manage.windowsazure.com), if that user is federated or password sync’d, we’ll set the password the admin selects on your local AD, as well.</span><span class="sxs-lookup"><span data-stu-id="5b952-161">Whenever an admin resets a user’s password in the [Azure Management Portal](https://manage.windowsazure.com), if that user is federated or password sync’d, we’ll set the password the admin selects on your local AD, as well.</span></span>  <span data-ttu-id="5b952-162">This is currently not supported in the Office Admin Portal.</span><span class="sxs-lookup"><span data-stu-id="5b952-162">This is currently not supported in the Office Admin Portal.</span></span>
* <span data-ttu-id="5b952-163">**Enforces your on-premises AD password policies.**</span><span class="sxs-lookup"><span data-stu-id="5b952-163">**Enforces your on-premises AD password policies.**</span></span>  <span data-ttu-id="5b952-164">When a user resets his/her password, we make sure that it meets your on-premises AD policy before committing it to that directory.</span><span class="sxs-lookup"><span data-stu-id="5b952-164">When a user resets his/her password, we make sure that it meets your on-premises AD policy before committing it to that directory.</span></span>  <span data-ttu-id="5b952-165">This includes history, complexity, age, password filters, and any other password restrictions you have defined in your local AD.</span><span class="sxs-lookup"><span data-stu-id="5b952-165">This includes history, complexity, age, password filters, and any other password restrictions you have defined in your local AD.</span></span>
* <span data-ttu-id="5b952-166">**Doesn’t require any inbound firewall rules.**</span><span class="sxs-lookup"><span data-stu-id="5b952-166">**Doesn’t require any inbound firewall rules.**</span></span>  <span data-ttu-id="5b952-167">Password writeback uses an Azure Service Bus relay as an underlying communication channel, meaning that you do not have to open any inbound ports on your firewall for this feature to work.</span><span class="sxs-lookup"><span data-stu-id="5b952-167">Password writeback uses an Azure Service Bus relay as an underlying communication channel, meaning that you do not have to open any inbound ports on your firewall for this feature to work.</span></span>
* <span data-ttu-id="5b952-168">**Is not supported for user accounts that exist within protected groups in your on-premises Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="5b952-168">**Is not supported for user accounts that exist within protected groups in your on-premises Active Directory.**</span></span> <span data-ttu-id="5b952-169">For more information about protected groups, see [Protected Accounts and Groups in Active Directory](https://technet.microsoft.com/library/dn535499.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b952-169">For more information about protected groups, see [Protected Accounts and Groups in Active Directory](https://technet.microsoft.com/library/dn535499.aspx).</span></span>

### <a name="how-password-writeback-works"></a><span data-ttu-id="5b952-170">How password writeback works</span><span class="sxs-lookup"><span data-stu-id="5b952-170">How password writeback works</span></span>
<span data-ttu-id="5b952-171">Password writeback has three main components:</span><span class="sxs-lookup"><span data-stu-id="5b952-171">Password writeback has three main components:</span></span>

* <span data-ttu-id="5b952-172">Password Reset cloud service (this is also integrated into Azure AD’s password change pages)</span><span class="sxs-lookup"><span data-stu-id="5b952-172">Password Reset cloud service (this is also integrated into Azure AD’s password change pages)</span></span>
* <span data-ttu-id="5b952-173">Tenant-specific Azure Service Bus relay</span><span class="sxs-lookup"><span data-stu-id="5b952-173">Tenant-specific Azure Service Bus relay</span></span>
* <span data-ttu-id="5b952-174">On-prem password reset endpoint</span><span class="sxs-lookup"><span data-stu-id="5b952-174">On-prem password reset endpoint</span></span>

<span data-ttu-id="5b952-175">They fit together as described in the below diagram:</span><span class="sxs-lookup"><span data-stu-id="5b952-175">They fit together as described in the below diagram:</span></span>

  ![][001]

<span data-ttu-id="5b952-176">When a federated or password hash sync’d user comes to reset or change his or her password in the cloud, the following occurs:</span><span class="sxs-lookup"><span data-stu-id="5b952-176">When a federated or password hash sync’d user comes to reset or change his or her password in the cloud, the following occurs:</span></span>

1. <span data-ttu-id="5b952-177">We check to see what type of password the user has.</span><span class="sxs-lookup"><span data-stu-id="5b952-177">We check to see what type of password the user has.</span></span>  <span data-ttu-id="5b952-178">If we see the password is managed on premises, then we ensure the writeback service is up and running.</span><span class="sxs-lookup"><span data-stu-id="5b952-178">If we see the password is managed on premises, then we ensure the writeback service is up and running.</span></span>  <span data-ttu-id="5b952-179">If it is, we let the user proceed, if it is not, we tell the user that their password cannot be reset here.</span><span class="sxs-lookup"><span data-stu-id="5b952-179">If it is, we let the user proceed, if it is not, we tell the user that their password cannot be reset here.</span></span>
2. <span data-ttu-id="5b952-180">Next, the user passes the appropriate authentication gates and reaches the reset password screen.</span><span class="sxs-lookup"><span data-stu-id="5b952-180">Next, the user passes the appropriate authentication gates and reaches the reset password screen.</span></span>
3. <span data-ttu-id="5b952-181">The user selects a new password and confirms it.</span><span class="sxs-lookup"><span data-stu-id="5b952-181">The user selects a new password and confirms it.</span></span>
4. <span data-ttu-id="5b952-182">Upon clicking submit, we encrypt the plaintext password with a symmetric key that was created during the writeback setup process.</span><span class="sxs-lookup"><span data-stu-id="5b952-182">Upon clicking submit, we encrypt the plaintext password with a symmetric key that was created during the writeback setup process.</span></span>
5. <span data-ttu-id="5b952-183">After encrypting the password, we include it in a payload that gets sent over an HTTPS channel to your tenant specific service bus relay (that we also set up for you during the writeback setup process).</span><span class="sxs-lookup"><span data-stu-id="5b952-183">After encrypting the password, we include it in a payload that gets sent over an HTTPS channel to your tenant specific service bus relay (that we also set up for you during the writeback setup process).</span></span>  <span data-ttu-id="5b952-184">This relay is protected by a randomly generated password that only your on-premises installation knows.</span><span class="sxs-lookup"><span data-stu-id="5b952-184">This relay is protected by a randomly generated password that only your on-premises installation knows.</span></span>
6. <span data-ttu-id="5b952-185">Once the message reaches service bus, the password reset endpoint automatically wakes up and sees that it has a reset request pending.</span><span class="sxs-lookup"><span data-stu-id="5b952-185">Once the message reaches service bus, the password reset endpoint automatically wakes up and sees that it has a reset request pending.</span></span>
7. <span data-ttu-id="5b952-186">The service then looks for the user in question by using the cloud anchor attribute.</span><span class="sxs-lookup"><span data-stu-id="5b952-186">The service then looks for the user in question by using the cloud anchor attribute.</span></span>  <span data-ttu-id="5b952-187">For this lookup to succeed, the user object must exist in the AD connector space, it must be linked to the corresponding MV object, and it must be linked to the corresponding AAD connector object.</span><span class="sxs-lookup"><span data-stu-id="5b952-187">For this lookup to succeed, the user object must exist in the AD connector space, it must be linked to the corresponding MV object, and it must be linked to the corresponding AAD connector object.</span></span> <span data-ttu-id="5b952-188">Finally, in order for sync to find this user account, the link from AD connector object to MV must have the sync rule `Microsoft.InfromADUserAccountEnabled.xxx` on the link.</span><span class="sxs-lookup"><span data-stu-id="5b952-188">Finally, in order for sync to find this user account, the link from AD connector object to MV must have the sync rule `Microsoft.InfromADUserAccountEnabled.xxx` on the link.</span></span>  <span data-ttu-id="5b952-189">This is needed because when the call comes in from the cloud, the sync engine uses the cloudAnchor attribute to look up the AAD connector space object, then follows the link back to the MV object, and then follows the link back to the AD object.</span><span class="sxs-lookup"><span data-stu-id="5b952-189">This is needed because when the call comes in from the cloud, the sync engine uses the cloudAnchor attribute to look up the AAD connector space object, then follows the link back to the MV object, and then follows the link back to the AD object.</span></span> <span data-ttu-id="5b952-190">Because there could be multiple AD objects (multi-forest) for the same user, the sync engine relies on the `Microsoft.InfromADUserAccountEnabled.xxx` link to pick the correct one.</span><span class="sxs-lookup"><span data-stu-id="5b952-190">Because there could be multiple AD objects (multi-forest) for the same user, the sync engine relies on the `Microsoft.InfromADUserAccountEnabled.xxx` link to pick the correct one.</span></span> <span data-ttu-id="5b952-191">Note that as a result of this logic, you must connect Azure AD Connect to the Primary Domain Controller for password writeback to work.</span><span class="sxs-lookup"><span data-stu-id="5b952-191">Note that as a result of this logic, you must connect Azure AD Connect to the Primary Domain Controller for password writeback to work.</span></span>  <span data-ttu-id="5b952-192">If you need to do this, you can configure Azure AD Connect to use a Primary Domain Controller Emulator by right clicking on the **properties** of the Active Directory synchronization connector, then selecting **configure directory partitions**.</span><span class="sxs-lookup"><span data-stu-id="5b952-192">If you need to do this, you can configure Azure AD Connect to use a Primary Domain Controller Emulator by right clicking on the **properties** of the Active Directory synchronization connector, then selecting **configure directory partitions**.</span></span> <span data-ttu-id="5b952-193">From there, look for the **domain controller connection settings** section and check the box titled **only use preferred domain controllers**.</span><span class="sxs-lookup"><span data-stu-id="5b952-193">From there, look for the **domain controller connection settings** section and check the box titled **only use preferred domain controllers**.</span></span> <span data-ttu-id="5b952-194">Note: if the preferred DC is not a PDC emulator, Azure AD Connect will still reach out to the PDC for password writeback.</span><span class="sxs-lookup"><span data-stu-id="5b952-194">Note: if the preferred DC is not a PDC emulator, Azure AD Connect will still reach out to the PDC for password writeback.</span></span>
8. <span data-ttu-id="5b952-195">Once the user account is found, we attempt to reset the password directly in the appropriate AD forest.</span><span class="sxs-lookup"><span data-stu-id="5b952-195">Once the user account is found, we attempt to reset the password directly in the appropriate AD forest.</span></span>
9. <span data-ttu-id="5b952-196">If the password set operation is successful, we tell the user their password has been modified and that they can go on their merry way.</span><span class="sxs-lookup"><span data-stu-id="5b952-196">If the password set operation is successful, we tell the user their password has been modified and that they can go on their merry way.</span></span> <span data-ttu-id="5b952-197">In the case when the user's password is synchronized to Azure AD using Password Sync, there is a chance that the on-premises password policy is weaker than the cloud password policy.</span><span class="sxs-lookup"><span data-stu-id="5b952-197">In the case when the user's password is synchronized to Azure AD using Password Sync, there is a chance that the on-premises password policy is weaker than the cloud password policy.</span></span> <span data-ttu-id="5b952-198">In this case, we still enforce whatever the on-premises policy is, and instead allow password hash sync to synchronize the hash of that password.</span><span class="sxs-lookup"><span data-stu-id="5b952-198">In this case, we still enforce whatever the on-premises policy is, and instead allow password hash sync to synchronize the hash of that password.</span></span> <span data-ttu-id="5b952-199">This ensures that your on-premises policy is enforced in the cloud, no matter if you use password sync or federation to provide single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b952-199">This ensures that your on-premises policy is enforced in the cloud, no matter if you use password sync or federation to provide single sign-on.</span></span>
10. <span data-ttu-id="5b952-200">If the password set operation fails, we return the error to the user and let them try again.</span><span class="sxs-lookup"><span data-stu-id="5b952-200">If the password set operation fails, we return the error to the user and let them try again.</span></span>  <span data-ttu-id="5b952-201">The operation might fail because the service was down, because the password they selected did not meet organization policies, because we could not find the user in the local AD, or any number of reasons.</span><span class="sxs-lookup"><span data-stu-id="5b952-201">The operation might fail because the service was down, because the password they selected did not meet organization policies, because we could not find the user in the local AD, or any number of reasons.</span></span>  <span data-ttu-id="5b952-202">We have a specific message for many of these cases and tell the user what they can do to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="5b952-202">We have a specific message for many of these cases and tell the user what they can do to resolve the issue.</span></span>

## <a name="scenarios-supported-for-password-writeback"></a><span data-ttu-id="5b952-203">Scenarios supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-203">Scenarios supported for password writeback</span></span>
<span data-ttu-id="5b952-204">The section below describes which scenarios are supported for which versions of our sync capabilities.</span><span class="sxs-lookup"><span data-stu-id="5b952-204">The section below describes which scenarios are supported for which versions of our sync capabilities.</span></span>  <span data-ttu-id="5b952-205">In general, We always recommend that you use the auto-update feature of Azure AD Connect, or install the latest version of [Azure AD Connect](connect/active-directory-aadconnect.md#install-azure-ad-connect) if you want to use password writeback.</span><span class="sxs-lookup"><span data-stu-id="5b952-205">In general, We always recommend that you use the auto-update feature of Azure AD Connect, or install the latest version of [Azure AD Connect](connect/active-directory-aadconnect.md#install-azure-ad-connect) if you want to use password writeback.</span></span>

* [<span data-ttu-id="5b952-206">**Supported Azure AD Connect, Azure AD Sync, and DirSync clients**</span><span class="sxs-lookup"><span data-stu-id="5b952-206">**Supported Azure AD Connect, Azure AD Sync, and DirSync clients**</span></span>](#supported-clients)
* [<span data-ttu-id="5b952-207">**Licenses required for password writeback**</span><span class="sxs-lookup"><span data-stu-id="5b952-207">**Licenses required for password writeback**</span></span>](#licenses-required-for-password-writeback)
* [<span data-ttu-id="5b952-208">**On-premises authentication modes supported for password writeback**</span><span class="sxs-lookup"><span data-stu-id="5b952-208">**On-premises authentication modes supported for password writeback**</span></span>](#on-premises-authentication-modes-supported-for-password-writeback)
* [<span data-ttu-id="5b952-209">**User and Admin operations supported for password writeback**</span><span class="sxs-lookup"><span data-stu-id="5b952-209">**User and Admin operations supported for password writeback**</span></span>](#user-and-admin-operations-supported-for-password-writeback)
* [<span data-ttu-id="5b952-210">**User and Admin operations not supported for password writeback**</span><span class="sxs-lookup"><span data-stu-id="5b952-210">**User and Admin operations not supported for password writeback**</span></span>](#user-and-admin-operations-not-supported-for-password-writeback)

### <a name="supported-clients"></a><span data-ttu-id="5b952-211">Supported clients</span><span class="sxs-lookup"><span data-stu-id="5b952-211">Supported clients</span></span>
<span data-ttu-id="5b952-212">We always recommend that you use the auto-update feature of Azure AD Connect, or install the latest version of [Azure AD Connect](connect/active-directory-aadconnect.md#install-azure-ad-connect) if you want to use password writeback.</span><span class="sxs-lookup"><span data-stu-id="5b952-212">We always recommend that you use the auto-update feature of Azure AD Connect, or install the latest version of [Azure AD Connect](connect/active-directory-aadconnect.md#install-azure-ad-connect) if you want to use password writeback.</span></span>

* <span data-ttu-id="5b952-213">**DirSync (any version > 1.0.6862)** - _NOT SUPPORTED_ - supports only basic writeback capabilities, and is no longer supported by the product group</span><span class="sxs-lookup"><span data-stu-id="5b952-213">**DirSync (any version > 1.0.6862)** - _NOT SUPPORTED_ - supports only basic writeback capabilities, and is no longer supported by the product group</span></span>
* <span data-ttu-id="5b952-214">**Azure AD Sync** - _DEPRECATED_ - supports only basic writeback capabilities, and is missing account unlock capabilities, rich logging, and relability improvements made in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5b952-214">**Azure AD Sync** - _DEPRECATED_ - supports only basic writeback capabilities, and is missing account unlock capabilities, rich logging, and relability improvements made in Azure AD Connect.</span></span> <span data-ttu-id="5b952-215">As such, we **highly** highly recommend upgrading.</span><span class="sxs-lookup"><span data-stu-id="5b952-215">As such, we **highly** highly recommend upgrading.</span></span>
* <span data-ttu-id="5b952-216">**Azure AD Connect** - _FULLY SUPPORTED_ - supports all writeback capabiltiies - please upgrade to the latest version to get the best new features and most stability / reliability possible</span><span class="sxs-lookup"><span data-stu-id="5b952-216">**Azure AD Connect** - _FULLY SUPPORTED_ - supports all writeback capabiltiies - please upgrade to the latest version to get the best new features and most stability / reliability possible</span></span>

### <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="5b952-217">Licenses required for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-217">Licenses required for password writeback</span></span>
<span data-ttu-id="5b952-218">In order to use password writeback, you must have one of the following licenses assigned in your tenant.</span><span class="sxs-lookup"><span data-stu-id="5b952-218">In order to use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="5b952-219">**Azure AD Premium P1** - no limitations on password writeback usage</span><span class="sxs-lookup"><span data-stu-id="5b952-219">**Azure AD Premium P1** - no limitations on password writeback usage</span></span>
* <span data-ttu-id="5b952-220">**Azure AD Premium P2** - no limitations on password writeback usage</span><span class="sxs-lookup"><span data-stu-id="5b952-220">**Azure AD Premium P2** - no limitations on password writeback usage</span></span>
* <span data-ttu-id="5b952-221">**Enterprise Moblity Suite** - no limitations on password writeback usage</span><span class="sxs-lookup"><span data-stu-id="5b952-221">**Enterprise Moblity Suite** - no limitations on password writeback usage</span></span>
* <span data-ttu-id="5b952-222">**Enterprise Cloud Suite** - no limitations on password writeback usage</span><span class="sxs-lookup"><span data-stu-id="5b952-222">**Enterprise Cloud Suite** - no limitations on password writeback usage</span></span>

<span data-ttu-id="5b952-223">You may not use password writeback with any Office 365 licensing plan, whether trial or paid.</span><span class="sxs-lookup"><span data-stu-id="5b952-223">You may not use password writeback with any Office 365 licensing plan, whether trial or paid.</span></span> <span data-ttu-id="5b952-224">You must upgrade to one of the above plans in order to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5b952-224">You must upgrade to one of the above plans in order to use this feature.</span></span>

<span data-ttu-id="5b952-225">We have no plans to enable password writeback for any Office 365 SKUs.</span><span class="sxs-lookup"><span data-stu-id="5b952-225">We have no plans to enable password writeback for any Office 365 SKUs.</span></span>

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a><span data-ttu-id="5b952-226">On-premises authentication modes supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-226">On-premises authentication modes supported for password writeback</span></span>
<span data-ttu-id="5b952-227">Password writeback works for the following user password types:</span><span class="sxs-lookup"><span data-stu-id="5b952-227">Password writeback works for the following user password types:</span></span>

* <span data-ttu-id="5b952-228">**Cloud-only users**: Password writeback does not apply in this situation, because there is no on-premises password</span><span class="sxs-lookup"><span data-stu-id="5b952-228">**Cloud-only users**: Password writeback does not apply in this situation, because there is no on-premises password</span></span>
* <span data-ttu-id="5b952-229">**Password-sync'd users**: Password writeback supported</span><span class="sxs-lookup"><span data-stu-id="5b952-229">**Password-sync'd users**: Password writeback supported</span></span>
* <span data-ttu-id="5b952-230">**Federated users**: Password writeback supported</span><span class="sxs-lookup"><span data-stu-id="5b952-230">**Federated users**: Password writeback supported</span></span>
* <span data-ttu-id="5b952-231">**Pass-through authentication users**: Password writeback supported</span><span class="sxs-lookup"><span data-stu-id="5b952-231">**Pass-through authentication users**: Password writeback supported</span></span>

### <a name="user-and-admin-operations-supported-for-password-writeback"></a><span data-ttu-id="5b952-232">User and Admin operations supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-232">User and Admin operations supported for password writeback</span></span>
<span data-ttu-id="5b952-233">Passwords are written back in all of the following situations:</span><span class="sxs-lookup"><span data-stu-id="5b952-233">Passwords are written back in all of the following situations:</span></span>

* <span data-ttu-id="5b952-234">**Supported End-user operations**</span><span class="sxs-lookup"><span data-stu-id="5b952-234">**Supported End-user operations**</span></span>
 * <span data-ttu-id="5b952-235">Any end-user self-service voluntary change password operation</span><span class="sxs-lookup"><span data-stu-id="5b952-235">Any end-user self-service voluntary change password operation</span></span>
 * <span data-ttu-id="5b952-236">Any end-user self-service force change password operation (e.g. password expiry)</span><span class="sxs-lookup"><span data-stu-id="5b952-236">Any end-user self-service force change password operation (e.g. password expiry)</span></span>
 * <span data-ttu-id="5b952-237">Any end-user self-service password reset originating from the [Password Reset Portal](https://passwordreset.microsoftonline.com)</span><span class="sxs-lookup"><span data-stu-id="5b952-237">Any end-user self-service password reset originating from the [Password Reset Portal](https://passwordreset.microsoftonline.com)</span></span>
* <span data-ttu-id="5b952-238">**Supported Administrator operations**</span><span class="sxs-lookup"><span data-stu-id="5b952-238">**Supported Administrator operations**</span></span>
 * <span data-ttu-id="5b952-239">Any administrator self-service voluntary change password operation</span><span class="sxs-lookup"><span data-stu-id="5b952-239">Any administrator self-service voluntary change password operation</span></span>
 * <span data-ttu-id="5b952-240">Any administrator self-service force change password operation (e.g. password expiry)</span><span class="sxs-lookup"><span data-stu-id="5b952-240">Any administrator self-service force change password operation (e.g. password expiry)</span></span>
 * <span data-ttu-id="5b952-241">Any administrator self-service password reset originating from the [Password Reset Portal](https://passwordreset.microsoftonline.com)</span><span class="sxs-lookup"><span data-stu-id="5b952-241">Any administrator self-service password reset originating from the [Password Reset Portal](https://passwordreset.microsoftonline.com)</span></span>
 * <span data-ttu-id="5b952-242">Any administrator-initiated end-user password reset from the [Classic Azure Management Portal](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="5b952-242">Any administrator-initiated end-user password reset from the [Classic Azure Management Portal](https://manage.windowsazure.com)</span></span>
 * <span data-ttu-id="5b952-243">Any administrator-initiated end-user password reset from the [Azure Portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5b952-243">Any administrator-initiated end-user password reset from the [Azure Portal](https://portal.azure.com)</span></span>

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a><span data-ttu-id="5b952-244">User and Admin operations not supported for password writeback</span><span class="sxs-lookup"><span data-stu-id="5b952-244">User and Admin operations not supported for password writeback</span></span>
<span data-ttu-id="5b952-245">Passwords are not written back in any of the following situations:</span><span class="sxs-lookup"><span data-stu-id="5b952-245">Passwords are not written back in any of the following situations:</span></span>

* <span data-ttu-id="5b952-246">**Unsupported End-user operations**</span><span class="sxs-lookup"><span data-stu-id="5b952-246">**Unsupported End-user operations**</span></span>
 * <span data-ttu-id="5b952-247">Any end-user resetting his or her own password using PowerShell v1, v2, or the Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="5b952-247">Any end-user resetting his or her own password using PowerShell v1, v2, or the Azure AD Graph API</span></span>
* <span data-ttu-id="5b952-248">**Unsupported Administrator operations**</span><span class="sxs-lookup"><span data-stu-id="5b952-248">**Unsupported Administrator operations**</span></span>
 * <span data-ttu-id="5b952-249">Any administrator-initiated end-user password reset from the [Office Management Portal](https://portal.office.com)</span><span class="sxs-lookup"><span data-stu-id="5b952-249">Any administrator-initiated end-user password reset from the [Office Management Portal](https://portal.office.com)</span></span>
 * <span data-ttu-id="5b952-250">Any administrator-initiated end-user password reset from PowerShell v1, v2, or the Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="5b952-250">Any administrator-initiated end-user password reset from PowerShell v1, v2, or the Azure AD Graph API</span></span>

<span data-ttu-id="5b952-251">While we are working to remove these limitations, we do not have a specific timeline we can share yet.</span><span class="sxs-lookup"><span data-stu-id="5b952-251">While we are working to remove these limitations, we do not have a specific timeline we can share yet.</span></span>

## <a name="password-writeback-security-model"></a><span data-ttu-id="5b952-252">Password writeback security model</span><span class="sxs-lookup"><span data-stu-id="5b952-252">Password writeback security model</span></span>
<span data-ttu-id="5b952-253">Password writeback is a highly secure and robust service.</span><span class="sxs-lookup"><span data-stu-id="5b952-253">Password writeback is a highly secure and robust service.</span></span>  <span data-ttu-id="5b952-254">In order to ensure your information is protected, we enable a 4-tiered security model that is described below.</span><span class="sxs-lookup"><span data-stu-id="5b952-254">In order to ensure your information is protected, we enable a 4-tiered security model that is described below.</span></span>

* <span data-ttu-id="5b952-255">**Tenant specific service-bus relay** – When you set up the service, we set up a tenant-specific service bus relay that is protected by a randomly generated strong password that Microsoft never has access to.</span><span class="sxs-lookup"><span data-stu-id="5b952-255">**Tenant specific service-bus relay** – When you set up the service, we set up a tenant-specific service bus relay that is protected by a randomly generated strong password that Microsoft never has access to.</span></span>
* <span data-ttu-id="5b952-256">**Locked down, cryptographically strong, password encryption key** – After the service bus relay is created, we create a strong symmetric key which we use to encrypt the password as it comes over the wire.</span><span class="sxs-lookup"><span data-stu-id="5b952-256">**Locked down, cryptographically strong, password encryption key** – After the service bus relay is created, we create a strong symmetric key which we use to encrypt the password as it comes over the wire.</span></span>  <span data-ttu-id="5b952-257">This key lives only in your company's secret store in the cloud, which is heavily locked down and audited, just like any password in the directory.</span><span class="sxs-lookup"><span data-stu-id="5b952-257">This key lives only in your company's secret store in the cloud, which is heavily locked down and audited, just like any password in the directory.</span></span>
* <span data-ttu-id="5b952-258">**Industry standard TLS** – When a password reset or change operation occurs in the cloud, we take the plaintext password and encrypt it with your public key.</span><span class="sxs-lookup"><span data-stu-id="5b952-258">**Industry standard TLS** – When a password reset or change operation occurs in the cloud, we take the plaintext password and encrypt it with your public key.</span></span>  <span data-ttu-id="5b952-259">We then plop that into an HTTPS message which is sent over an encrypted channel using Microsoft’s SSL certs to your service bus relay.</span><span class="sxs-lookup"><span data-stu-id="5b952-259">We then plop that into an HTTPS message which is sent over an encrypted channel using Microsoft’s SSL certs to your service bus relay.</span></span>  <span data-ttu-id="5b952-260">After that message arrives into Service Bus, your on-prem agent wakes up, authenticates to Service Bus using the strong password that had been previously generated, picks up the encrypted message, decrypts it using the private key we generated, and then attempts to set the password through the AD DS SetPassword API.</span><span class="sxs-lookup"><span data-stu-id="5b952-260">After that message arrives into Service Bus, your on-prem agent wakes up, authenticates to Service Bus using the strong password that had been previously generated, picks up the encrypted message, decrypts it using the private key we generated, and then attempts to set the password through the AD DS SetPassword API.</span></span>  <span data-ttu-id="5b952-261">This step is what allows us to enforce your AD on-prem password policy (complexity, age, history, filters, etc) in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5b952-261">This step is what allows us to enforce your AD on-prem password policy (complexity, age, history, filters, etc) in the cloud.</span></span>
* <span data-ttu-id="5b952-262">**Message expiration policies** – Finally, if for some reason the message sits in Service Bus because your on-prem service is down, it will be timed out and removed after several minutes in order to increase security even further.</span><span class="sxs-lookup"><span data-stu-id="5b952-262">**Message expiration policies** – Finally, if for some reason the message sits in Service Bus because your on-prem service is down, it will be timed out and removed after several minutes in order to increase security even further.</span></span>

### <a name="password-writeback-encryption-details"></a><span data-ttu-id="5b952-263">Password writeback encryption details</span><span class="sxs-lookup"><span data-stu-id="5b952-263">Password writeback encryption details</span></span>
<span data-ttu-id="5b952-264">Below describes the encryption steps a password reset reqeust goes through after a user submits it, but before it arrives in your on-premises environment, to ensure maximum service reliability and security.</span><span class="sxs-lookup"><span data-stu-id="5b952-264">Below describes the encryption steps a password reset reqeust goes through after a user submits it, but before it arrives in your on-premises environment, to ensure maximum service reliability and security.</span></span>

* <span data-ttu-id="5b952-265">**Step 1 - Password encryption with 2048-bit RSA Key** - Once a user submits a password to be written back to on-premises, first, the submitted password itself is encrypted with a 2048-bit RSA key.</span><span class="sxs-lookup"><span data-stu-id="5b952-265">**Step 1 - Password encryption with 2048-bit RSA Key** - Once a user submits a password to be written back to on-premises, first, the submitted password itself is encrypted with a 2048-bit RSA key.</span></span>

* <span data-ttu-id="5b952-266">**Step 2 - Package-level encryption with AES-GCM** - Then the entire package (password + required metadata) is encrypted using AES-GCM.</span><span class="sxs-lookup"><span data-stu-id="5b952-266">**Step 2 - Package-level encryption with AES-GCM** - Then the entire package (password + required metadata) is encrypted using AES-GCM.</span></span> <span data-ttu-id="5b952-267">This prevents anyone with direct access to the underlying ServiceBus channel from viewing/tampering with the contents.</span><span class="sxs-lookup"><span data-stu-id="5b952-267">This prevents anyone with direct access to the underlying ServiceBus channel from viewing/tampering with the contents.</span></span>

* <span data-ttu-id="5b952-268">**Step 3 - All communication occurs over TLS / SSL** - Additionally, all the communication with ServiceBus happens in a SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="5b952-268">**Step 3 - All communication occurs over TLS / SSL** - Additionally, all the communication with ServiceBus happens in a SSL/TLS channel.</span></span> <span data-ttu-id="5b952-269">This secures the contents from unauthorized 3rd parties.</span><span class="sxs-lookup"><span data-stu-id="5b952-269">This secures the contents from unauthorized 3rd parties.</span></span>

* <span data-ttu-id="5b952-270">**Step 4 - Automatic Key Rollover every 6 months** - Finally, automatically every 6 months, or every time password writeback is disabled / re-enabled on Azure AD Connect, we roll over all of these keys to ensure maximum service security and safety.</span><span class="sxs-lookup"><span data-stu-id="5b952-270">**Step 4 - Automatic Key Rollover every 6 months** - Finally, automatically every 6 months, or every time password writeback is disabled / re-enabled on Azure AD Connect, we roll over all of these keys to ensure maximum service security and safety.</span></span>

### <a name="password-writeback-bandwidth-usage"></a><span data-ttu-id="5b952-271">Password writeback bandwidth usage</span><span class="sxs-lookup"><span data-stu-id="5b952-271">Password writeback bandwidth usage</span></span>

<span data-ttu-id="5b952-272">Password writeback is an extremely low bandwidth service that sends requests back to the on-premises agent only under the following circumstances:</span><span class="sxs-lookup"><span data-stu-id="5b952-272">Password writeback is an extremely low bandwidth service that sends requests back to the on-premises agent only under the following circumstances:</span></span>

1. <span data-ttu-id="5b952-273">Two messages sent when enabling or disabling the feature through Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5b952-273">Two messages sent when enabling or disabling the feature through Azure AD Connect.</span></span>
2. <span data-ttu-id="5b952-274">One message is sent once every 5 minutes as a service heartbeat for as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="5b952-274">One message is sent once every 5 minutes as a service heartbeat for as long as the service is running.</span></span>
3. <span data-ttu-id="5b952-275">Two messages are sent each time a new password is submitted, one message as a request to perform the operation, and a subsequent message which contains the result of the operation.</span><span class="sxs-lookup"><span data-stu-id="5b952-275">Two messages are sent each time a new password is submitted, one message as a request to perform the operation, and a subsequent message which contains the result of the operation.</span></span> <span data-ttu-id="5b952-276">These messages are sent in the following cirumstances.</span><span class="sxs-lookup"><span data-stu-id="5b952-276">These messages are sent in the following cirumstances.</span></span>
4. <span data-ttu-id="5b952-277">Each time a new password is submitted during a user self-service password reset.</span><span class="sxs-lookup"><span data-stu-id="5b952-277">Each time a new password is submitted during a user self-service password reset.</span></span>
5. <span data-ttu-id="5b952-278">Each time a new password is submitted during a user password change operation.</span><span class="sxs-lookup"><span data-stu-id="5b952-278">Each time a new password is submitted during a user password change operation.</span></span>
6. <span data-ttu-id="5b952-279">Each time a new password is submitted during an admin-initiated user password reset (from the Azure admin portals only)</span><span class="sxs-lookup"><span data-stu-id="5b952-279">Each time a new password is submitted during an admin-initiated user password reset (from the Azure admin portals only)</span></span>

#### <a name="message-size-and-bandwidth-considerations"></a><span data-ttu-id="5b952-280">Message size and bandwidth considerations</span><span class="sxs-lookup"><span data-stu-id="5b952-280">Message size and bandwidth considerations</span></span>

<span data-ttu-id="5b952-281">The size of each of the message described above is typically under 1kb, which means, even under extreme loads, the password writeback service itself will be consuming at most a few kilobits per second of bandwidth.</span><span class="sxs-lookup"><span data-stu-id="5b952-281">The size of each of the message described above is typically under 1kb, which means, even under extreme loads, the password writeback service itself will be consuming at most a few kilobits per second of bandwidth.</span></span> <span data-ttu-id="5b952-282">Since each message is sent in real time, only when required by a password update operation, and since the message size is so small, the bandwidth usage of the writeback capability is effectively too small to have any real measurable impact.</span><span class="sxs-lookup"><span data-stu-id="5b952-282">Since each message is sent in real time, only when required by a password update operation, and since the message size is so small, the bandwidth usage of the writeback capability is effectively too small to have any real measurable impact.</span></span>

## <a name="deploying-managing-and-accessing-password-reset-data-for-your-users"></a><span data-ttu-id="5b952-283">Deploying, managing, and accessing password reset data for your users</span><span class="sxs-lookup"><span data-stu-id="5b952-283">Deploying, managing, and accessing password reset data for your users</span></span>
<span data-ttu-id="5b952-284">You can manage and access password reset data for your users through Azure AD Connect, PowerShell, the Graph, or our registration experiences.</span><span class="sxs-lookup"><span data-stu-id="5b952-284">You can manage and access password reset data for your users through Azure AD Connect, PowerShell, the Graph, or our registration experiences.</span></span>  <span data-ttu-id="5b952-285">You can even deploy password reset to your whole organization without requiring users to register for it by leveraging the options described below.</span><span class="sxs-lookup"><span data-stu-id="5b952-285">You can even deploy password reset to your whole organization without requiring users to register for it by leveraging the options described below.</span></span>

  * [<span data-ttu-id="5b952-286">What data is used by password reset?</span><span class="sxs-lookup"><span data-stu-id="5b952-286">What data is used by password reset?</span></span>](#what-data-is-used-by-password-reset)
  * [<span data-ttu-id="5b952-287">Deploying password reset without requiring end user registration</span><span class="sxs-lookup"><span data-stu-id="5b952-287">Deploying password reset without requiring end user registration</span></span>](#deploying-password-reset-without-requiring-end-user-registration)
  * [<span data-ttu-id="5b952-288">What happens when a user registers for password reset?</span><span class="sxs-lookup"><span data-stu-id="5b952-288">What happens when a user registers for password reset?</span></span>](#what-happens-when-a-user-registers)
  * [<span data-ttu-id="5b952-289">How to access password reset data for your users</span><span class="sxs-lookup"><span data-stu-id="5b952-289">How to access password reset data for your users</span></span>](#how-to-access-password-reset-data-for-your-users)
  * [<span data-ttu-id="5b952-290">Setting password reset data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-290">Setting password reset data with PowerShell</span></span>](#setting-password-reset-data-with-powershell)
  * [<span data-ttu-id="5b952-291">Reading password reset data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-291">Reading password reset data with PowerShell</span></span>](#reading-password-reset-data-with-powershell)

### <a name="what-data-is-used-by-password-reset"></a><span data-ttu-id="5b952-292">What data is used by password reset?</span><span class="sxs-lookup"><span data-stu-id="5b952-292">What data is used by password reset?</span></span>
<span data-ttu-id="5b952-293">The following table outlines where and how this data is used during password reset and is designed to help you decide which authentication options are appropriate for your organization.</span><span class="sxs-lookup"><span data-stu-id="5b952-293">The following table outlines where and how this data is used during password reset and is designed to help you decide which authentication options are appropriate for your organization.</span></span> <span data-ttu-id="5b952-294">This table also shows any formatting requirements for cases where you are providing data on behalf of users from input paths that do not validate this data.</span><span class="sxs-lookup"><span data-stu-id="5b952-294">This table also shows any formatting requirements for cases where you are providing data on behalf of users from input paths that do not validate this data.</span></span>

> [!NOTE]
> <span data-ttu-id="5b952-295">Office Phone does not appear in the registration portal because users are currently not able to edit this property in the directory.</span><span class="sxs-lookup"><span data-stu-id="5b952-295">Office Phone does not appear in the registration portal because users are currently not able to edit this property in the directory.</span></span> <span data-ttu-id="5b952-296">Only administrators may set this value.</span><span class="sxs-lookup"><span data-stu-id="5b952-296">Only administrators may set this value.</span></span>
>
>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="5b952-297">
                <strong>Contact Method Name</strong>
              </span><span class="sxs-lookup"><span data-stu-id="5b952-297">
                <strong>Contact Method Name</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-298">
                <strong>Active Directory Data Element</strong>
              </span><span class="sxs-lookup"><span data-stu-id="5b952-298">
                <strong>Active Directory Data Element</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-299">
                <strong>Azure Active Directory Data Element</strong>
              </span><span class="sxs-lookup"><span data-stu-id="5b952-299">
                <strong>Azure Active Directory Data Element</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-300">
                <strong>Used / Settable Where?</strong>
              </span><span class="sxs-lookup"><span data-stu-id="5b952-300">
                <strong>Used / Settable Where?</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-301">
                <strong>Format requirements</strong>
              </span><span class="sxs-lookup"><span data-stu-id="5b952-301">
                <strong>Format requirements</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="5b952-302">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-302">Office Phone</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-303">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="5b952-303">telephoneNumber</span></span></p>
              <p><span data-ttu-id="5b952-304">This property can be synchronized to the PhoneNumber attribute in Azure Active Directory and immediately used for password reset WITHOUT requiring a user to register, first.</span><span class="sxs-lookup"><span data-stu-id="5b952-304">This property can be synchronized to the PhoneNumber attribute in Azure Active Directory and immediately used for password reset WITHOUT requiring a user to register, first.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-305">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="5b952-305">PhoneNumber</span></span></p>
              <p><span data-ttu-id="5b952-306">e.g. Set-MsolUser -UserPrincipalName JWarner@contoso.com -PhoneNumber "+1 1234567890x1234"</span><span class="sxs-lookup"><span data-stu-id="5b952-306">e.g. Set-MsolUser -UserPrincipalName JWarner@contoso.com -PhoneNumber "+1 1234567890x1234"</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-307">Used in:</span><span class="sxs-lookup"><span data-stu-id="5b952-307">Used in:</span></span></p>
              <p><span data-ttu-id="5b952-308">Password Reset Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-308">Password Reset Portal</span></span></p>
              <p><span data-ttu-id="5b952-309">Settable from:</span><span class="sxs-lookup"><span data-stu-id="5b952-309">Settable from:</span></span></p>
              <p><span data-ttu-id="5b952-310">PhoneNumber is settable from PowerShell, DirSync, Azure Management Portal, and the Office Admin Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-310">PhoneNumber is settable from PowerShell, DirSync, Azure Management Portal, and the Office Admin Portal</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-311">+ccc xxxyyyzzzz (e.g. +1 1234567890)</span><span class="sxs-lookup"><span data-stu-id="5b952-311">+ccc xxxyyyzzzz (e.g. +1 1234567890)</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-312">Must provide a country code</span><span class="sxs-lookup"><span data-stu-id="5b952-312">Must provide a country code</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-313">Must provide an area code (where applicable)</span><span class="sxs-lookup"><span data-stu-id="5b952-313">Must provide an area code (where applicable)</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-314">Must have provide a + in front of the country code</span><span class="sxs-lookup"><span data-stu-id="5b952-314">Must have provide a + in front of the country code</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-315">Must have a space between country code and the rest of the number</span><span class="sxs-lookup"><span data-stu-id="5b952-315">Must have a space between country code and the rest of the number</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-316">Extensions are not supported, if you have any extensions specified, we will strip it from the number before dispatching the phone call.</span><span class="sxs-lookup"><span data-stu-id="5b952-316">Extensions are not supported, if you have any extensions specified, we will strip it from the number before dispatching the phone call.</span></span><br><br></li>
              </ul>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="5b952-317">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-317">Mobile Phone</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-318">Mobile</span><span class="sxs-lookup"><span data-stu-id="5b952-318">Mobile</span></span></p>
              <p><span data-ttu-id="5b952-319">This property can be synchronized to the MobilePhone attribute in Azure Active Directory and immediately used for password reset WITHOUT requiring a user to register, first.</span><span class="sxs-lookup"><span data-stu-id="5b952-319">This property can be synchronized to the MobilePhone attribute in Azure Active Directory and immediately used for password reset WITHOUT requiring a user to register, first.</span></span></p>
              <p><span data-ttu-id="5b952-320">It is not possible to synchronize this property to AuthenticationPhone at this time.</span><span class="sxs-lookup"><span data-stu-id="5b952-320">It is not possible to synchronize this property to AuthenticationPhone at this time.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-321">AuthenticationPhone</span><span class="sxs-lookup"><span data-stu-id="5b952-321">AuthenticationPhone</span></span></p>
              <p><span data-ttu-id="5b952-322">OR</span><span class="sxs-lookup"><span data-stu-id="5b952-322">OR</span></span></p>
              <p><span data-ttu-id="5b952-323">MobilePhone</span><span class="sxs-lookup"><span data-stu-id="5b952-323">MobilePhone</span></span></p>
              <p><span data-ttu-id="5b952-324">(Authentication Phone is used if there is data present, otherwise this falls back to the mobile phone field).</span><span class="sxs-lookup"><span data-stu-id="5b952-324">(Authentication Phone is used if there is data present, otherwise this falls back to the mobile phone field).</span></span></p>
              <p><span data-ttu-id="5b952-325">e.g. Set-MsolUser -UserPrincipalName JWarner@contoso.com -MobilePhone "+1 1234567890x1234"</span><span class="sxs-lookup"><span data-stu-id="5b952-325">e.g. Set-MsolUser -UserPrincipalName JWarner@contoso.com -MobilePhone "+1 1234567890x1234"</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-326">Used in:</span><span class="sxs-lookup"><span data-stu-id="5b952-326">Used in:</span></span></p>
              <p><span data-ttu-id="5b952-327">Password Reset Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-327">Password Reset Portal</span></span></p>
              <p><span data-ttu-id="5b952-328">Registration Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-328">Registration Portal</span></span></p>
              <p><span data-ttu-id="5b952-329">Settable from:</span><span class="sxs-lookup"><span data-stu-id="5b952-329">Settable from:</span></span> </p>
              <p><span data-ttu-id="5b952-330">AuthenticationPhone is settable from the password reset registration portal or MFA registration portal.</span><span class="sxs-lookup"><span data-stu-id="5b952-330">AuthenticationPhone is settable from the password reset registration portal or MFA registration portal.</span></span></p>
              <p><span data-ttu-id="5b952-331">MobilePhone is settable from PowerShell, Azure AD Connect, Azure Management Portal, and the Office Admin Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-331">MobilePhone is settable from PowerShell, Azure AD Connect, Azure Management Portal, and the Office Admin Portal</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-332">+ccc xxxyyyzzzz (e.g. +1 1234567890)</span><span class="sxs-lookup"><span data-stu-id="5b952-332">+ccc xxxyyyzzzz (e.g. +1 1234567890)</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-333">Must provide a country code.</span><span class="sxs-lookup"><span data-stu-id="5b952-333">Must provide a country code.</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-334">Must provide an area code (where applicable).</span><span class="sxs-lookup"><span data-stu-id="5b952-334">Must provide an area code (where applicable).</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-335">Must have provide a + in front of the country code.</span><span class="sxs-lookup"><span data-stu-id="5b952-335">Must have provide a + in front of the country code.</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-336">Must have a space between country code and the rest of the number.</span><span class="sxs-lookup"><span data-stu-id="5b952-336">Must have a space between country code and the rest of the number.</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-337">Extensions are not supported, if you have any extensions specified, we ignore it when dispatching the phone call.</span><span class="sxs-lookup"><span data-stu-id="5b952-337">Extensions are not supported, if you have any extensions specified, we ignore it when dispatching the phone call.</span></span><br><br></li>
              </ul>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="5b952-338">Alternate Email</span><span class="sxs-lookup"><span data-stu-id="5b952-338">Alternate Email</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-339">Not available</span><span class="sxs-lookup"><span data-stu-id="5b952-339">Not available</span></span></p>
              <p><span data-ttu-id="5b952-340">It is not possible to synchronize values from Active Directory to either the AuthenticationEmail or AlternateEmailAddresses[0] property at this time.</span><span class="sxs-lookup"><span data-stu-id="5b952-340">It is not possible to synchronize values from Active Directory to either the AuthenticationEmail or AlternateEmailAddresses[0] property at this time.</span></span> </p>
              <p><span data-ttu-id="5b952-341">You may use PowerShell to set AlternateEmailAddresses[0].</span><span class="sxs-lookup"><span data-stu-id="5b952-341">You may use PowerShell to set AlternateEmailAddresses[0].</span></span> <span data-ttu-id="5b952-342">Instructions for this are in the section just below this table.</span><span class="sxs-lookup"><span data-stu-id="5b952-342">Instructions for this are in the section just below this table.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-343">AuthenticationEmail</span><span class="sxs-lookup"><span data-stu-id="5b952-343">AuthenticationEmail</span></span></p>
              <p><span data-ttu-id="5b952-344">OR</span><span class="sxs-lookup"><span data-stu-id="5b952-344">OR</span></span></p>
              <p><span data-ttu-id="5b952-345">AlternateEmailAddresses[0]</span><span class="sxs-lookup"><span data-stu-id="5b952-345">AlternateEmailAddresses[0]</span></span> </p>
              <p><span data-ttu-id="5b952-346">(Authentication Email is used if there is data present, otherwise this falls back to the Alternate Email field).</span><span class="sxs-lookup"><span data-stu-id="5b952-346">(Authentication Email is used if there is data present, otherwise this falls back to the Alternate Email field).</span></span></p>
              <p><span data-ttu-id="5b952-347">Note: the alternate email field is specified as an array of strings in the directory.</span><span class="sxs-lookup"><span data-stu-id="5b952-347">Note: the alternate email field is specified as an array of strings in the directory.</span></span>  <span data-ttu-id="5b952-348">We use the first entry in this array.</span><span class="sxs-lookup"><span data-stu-id="5b952-348">We use the first entry in this array.</span></span></p>
              <p><span data-ttu-id="5b952-349">e.g. Set-MsolUser -UserPrincipalName JWarner@contoso.com -AlternateEmailAddresses "email@live.com"</span><span class="sxs-lookup"><span data-stu-id="5b952-349">e.g. Set-MsolUser -UserPrincipalName JWarner@contoso.com -AlternateEmailAddresses "email@live.com"</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-350">Used in:</span><span class="sxs-lookup"><span data-stu-id="5b952-350">Used in:</span></span></p>
              <p><span data-ttu-id="5b952-351">Password Reset Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-351">Password Reset Portal</span></span></p>
              <p><span data-ttu-id="5b952-352">Registration Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-352">Registration Portal</span></span></p>
              <p><span data-ttu-id="5b952-353">Settable from:</span><span class="sxs-lookup"><span data-stu-id="5b952-353">Settable from:</span></span> </p>
              <p><span data-ttu-id="5b952-354">AuthenticationEmail is settable from the password reset registration portal or MFA registration portal.</span><span class="sxs-lookup"><span data-stu-id="5b952-354">AuthenticationEmail is settable from the password reset registration portal or MFA registration portal.</span></span></p>
              <p><span data-ttu-id="5b952-355">AlternateEmail is settable from PowerShell, the Azure Management Portal, and the Office Admin Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-355">AlternateEmail is settable from PowerShell, the Azure Management Portal, and the Office Admin Portal</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-356">
                <a href="mailto:user@domain.com">user@domain.com</a> or 甲斐@黒川.日本</span><span class="sxs-lookup"><span data-stu-id="5b952-356">
                <a href="mailto:user@domain.com">user@domain.com</a> or 甲斐@黒川.日本</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-357">Emails should follow standard formatting as per .</span><span class="sxs-lookup"><span data-stu-id="5b952-357">Emails should follow standard formatting as per .</span></span><br><br></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="5b952-358">Unicode emails are supported.</span><span class="sxs-lookup"><span data-stu-id="5b952-358">Unicode emails are supported.</span></span><br><br></li>
              </ul>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="5b952-359">Security Questions and Answers</span><span class="sxs-lookup"><span data-stu-id="5b952-359">Security Questions and Answers</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-360">Not available</span><span class="sxs-lookup"><span data-stu-id="5b952-360">Not available</span></span></p>
              <p><span data-ttu-id="5b952-361">It is not possible to synchronize Security Questions or Answers from Active Directory at this time.</span><span class="sxs-lookup"><span data-stu-id="5b952-361">It is not possible to synchronize Security Questions or Answers from Active Directory at this time.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-362">Not available to modify directly in the directory.</span><span class="sxs-lookup"><span data-stu-id="5b952-362">Not available to modify directly in the directory.</span></span></p>
              <p><span data-ttu-id="5b952-363">May only be set during the password reset end user registration process.</span><span class="sxs-lookup"><span data-stu-id="5b952-363">May only be set during the password reset end user registration process.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-364">Used in:</span><span class="sxs-lookup"><span data-stu-id="5b952-364">Used in:</span></span></p>
              <p><span data-ttu-id="5b952-365">Password Reset Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-365">Password Reset Portal</span></span></p>
              <p><span data-ttu-id="5b952-366">Registration Portal</span><span class="sxs-lookup"><span data-stu-id="5b952-366">Registration Portal</span></span> </p>
              <p><span data-ttu-id="5b952-367">Settable from:</span><span class="sxs-lookup"><span data-stu-id="5b952-367">Settable from:</span></span> </p>
              <p><span data-ttu-id="5b952-368">The only way to set security questions is through the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="5b952-368">The only way to set security questions is through the Azure Management Portal.</span></span></p>
              <p><span data-ttu-id="5b952-369">The only way to set answers to security questions for a given user is through the Registration Portal.</span><span class="sxs-lookup"><span data-stu-id="5b952-369">The only way to set answers to security questions for a given user is through the Registration Portal.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="5b952-370">Security questions have a max of 200 characters and a min of 3 characters</span><span class="sxs-lookup"><span data-stu-id="5b952-370">Security questions have a max of 200 characters and a min of 3 characters</span></span></p>
              <p><span data-ttu-id="5b952-371">Answers have a max of 40 characters and a min of 3 characters</span><span class="sxs-lookup"><span data-stu-id="5b952-371">Answers have a max of 40 characters and a min of 3 characters</span></span></p>
            </td>
          </tr>
        </tbody></table>


### <a name="deploying-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="5b952-372">Deploying password reset without requiring end user registration</span><span class="sxs-lookup"><span data-stu-id="5b952-372">Deploying password reset without requiring end user registration</span></span>
<span data-ttu-id="5b952-373">If you want to deploy password reset without requiring your users to register for it, you can do so easily by following one of the two below options.</span><span class="sxs-lookup"><span data-stu-id="5b952-373">If you want to deploy password reset without requiring your users to register for it, you can do so easily by following one of the two below options.</span></span> <span data-ttu-id="5b952-374">This can be a useful way to unblock large numbers of users to use SSPR while still allowing users to validate this information through the registration process.</span><span class="sxs-lookup"><span data-stu-id="5b952-374">This can be a useful way to unblock large numbers of users to use SSPR while still allowing users to validate this information through the registration process.</span></span>

<span data-ttu-id="5b952-375">Many of our largest customers use this today to get started with password reset extremely quickly.</span><span class="sxs-lookup"><span data-stu-id="5b952-375">Many of our largest customers use this today to get started with password reset extremely quickly.</span></span>

#### <a name="synchronize-phone-numbers-with-azure-ad-connect"></a><span data-ttu-id="5b952-376">Synchronize phone numbers with Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5b952-376">Synchronize phone numbers with Azure AD Connect</span></span>
<span data-ttu-id="5b952-377">If you synchronize data to one or both of the below fields, it can immediately be used for password reset, without requiring users to register first:</span><span class="sxs-lookup"><span data-stu-id="5b952-377">If you synchronize data to one or both of the below fields, it can immediately be used for password reset, without requiring users to register first:</span></span>

* <span data-ttu-id="5b952-378">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-378">Mobile Phone</span></span>
* <span data-ttu-id="5b952-379">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-379">Office Phone</span></span>

<span data-ttu-id="5b952-380">To learn about which properties need to be updated on premises, go to the [What data is used by password reset?](#what-data-is-used-by-password-reset) section and look up the fields mentioned above.</span><span class="sxs-lookup"><span data-stu-id="5b952-380">To learn about which properties need to be updated on premises, go to the [What data is used by password reset?](#what-data-is-used-by-password-reset) section and look up the fields mentioned above.</span></span>  

<span data-ttu-id="5b952-381">Make sure any phone numbers are in the format "+1 1234567890" so they work properly with our system.</span><span class="sxs-lookup"><span data-stu-id="5b952-381">Make sure any phone numbers are in the format "+1 1234567890" so they work properly with our system.</span></span>

#### <a name="set-phone-numbers-or-emails-with-powershell"></a><span data-ttu-id="5b952-382">Set phone numbers or emails with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-382">Set phone numbers or emails with PowerShell</span></span>
<span data-ttu-id="5b952-383">If you set one or more of these fields, it can immediately be used for password reset, without requiring users to register first:</span><span class="sxs-lookup"><span data-stu-id="5b952-383">If you set one or more of these fields, it can immediately be used for password reset, without requiring users to register first:</span></span>

* <span data-ttu-id="5b952-384">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-384">Mobile Phone</span></span>
* <span data-ttu-id="5b952-385">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-385">Office Phone</span></span>
* <span data-ttu-id="5b952-386">Alternate Email</span><span class="sxs-lookup"><span data-stu-id="5b952-386">Alternate Email</span></span>

<span data-ttu-id="5b952-387">To learn how to set these properties using PowerShell, go to the [Setting password reset data with PowerShell](#setting-password-reset-data-with-powershell) section.</span><span class="sxs-lookup"><span data-stu-id="5b952-387">To learn how to set these properties using PowerShell, go to the [Setting password reset data with PowerShell](#setting-password-reset-data-with-powershell) section.</span></span>

<span data-ttu-id="5b952-388">Make sure any phone numbers are in the format "+1 1234567890" so they work properly with our system.</span><span class="sxs-lookup"><span data-stu-id="5b952-388">Make sure any phone numbers are in the format "+1 1234567890" so they work properly with our system.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="5b952-389">What happens when a user registers?</span><span class="sxs-lookup"><span data-stu-id="5b952-389">What happens when a user registers?</span></span>
<span data-ttu-id="5b952-390">When a user registers, the registration page will **always** set the following fields:</span><span class="sxs-lookup"><span data-stu-id="5b952-390">When a user registers, the registration page will **always** set the following fields:</span></span>

* <span data-ttu-id="5b952-391">Authentication Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-391">Authentication Phone</span></span>
* <span data-ttu-id="5b952-392">Authentication Email</span><span class="sxs-lookup"><span data-stu-id="5b952-392">Authentication Email</span></span>
* <span data-ttu-id="5b952-393">Security Questions and Answers</span><span class="sxs-lookup"><span data-stu-id="5b952-393">Security Questions and Answers</span></span>

<span data-ttu-id="5b952-394">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those to reset their passwords, even if they haven't registered for the service.</span><span class="sxs-lookup"><span data-stu-id="5b952-394">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those to reset their passwords, even if they haven't registered for the service.</span></span>  <span data-ttu-id="5b952-395">In addition, users will see those values when registering for the first time, and modify them if they wish.</span><span class="sxs-lookup"><span data-stu-id="5b952-395">In addition, users will see those values when registering for the first time, and modify them if they wish.</span></span>  <span data-ttu-id="5b952-396">However, after they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span><span class="sxs-lookup"><span data-stu-id="5b952-396">However, after they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

### <a name="how-to-access-password-reset-data-for-your-users"></a><span data-ttu-id="5b952-397">How to access password reset data for your users</span><span class="sxs-lookup"><span data-stu-id="5b952-397">How to access password reset data for your users</span></span>
#### <a name="data-settable-via-synchronization"></a><span data-ttu-id="5b952-398">Data settable via synchronization</span><span class="sxs-lookup"><span data-stu-id="5b952-398">Data settable via synchronization</span></span>
<span data-ttu-id="5b952-399">The following fields can be synchronized from on-premises:</span><span class="sxs-lookup"><span data-stu-id="5b952-399">The following fields can be synchronized from on-premises:</span></span>

* <span data-ttu-id="5b952-400">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-400">Mobile Phone</span></span>
* <span data-ttu-id="5b952-401">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-401">Office Phone</span></span>

#### <a name="data-settable-with-azure-ad-powershell--azure-ad-graph"></a><span data-ttu-id="5b952-402">Data settable with Azure AD PowerShell & Azure AD Graph</span><span class="sxs-lookup"><span data-stu-id="5b952-402">Data settable with Azure AD PowerShell & Azure AD Graph</span></span>
<span data-ttu-id="5b952-403">The following fields can be set using Azure AD PowerShell & the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="5b952-403">The following fields can be set using Azure AD PowerShell & the Azure AD Graph API:</span></span>

* <span data-ttu-id="5b952-404">Alternate Email</span><span class="sxs-lookup"><span data-stu-id="5b952-404">Alternate Email</span></span>
* <span data-ttu-id="5b952-405">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-405">Mobile Phone</span></span>
* <span data-ttu-id="5b952-406">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-406">Office Phone</span></span>

#### <a name="data-settable-with-registration-ui-only"></a><span data-ttu-id="5b952-407">Data settable with registration UI only</span><span class="sxs-lookup"><span data-stu-id="5b952-407">Data settable with registration UI only</span></span>
<span data-ttu-id="5b952-408">The following fields are only accessible via the SSPR registration UI (https://aka.ms/ssprsetup):</span><span class="sxs-lookup"><span data-stu-id="5b952-408">The following fields are only accessible via the SSPR registration UI (https://aka.ms/ssprsetup):</span></span>

* <span data-ttu-id="5b952-409">Security Questions and Answers</span><span class="sxs-lookup"><span data-stu-id="5b952-409">Security Questions and Answers</span></span>

#### <a name="data-readable-with-azure-ad-powershell--azure-ad-graph"></a><span data-ttu-id="5b952-410">Data readable with Azure AD PowerShell & Azure AD Graph</span><span class="sxs-lookup"><span data-stu-id="5b952-410">Data readable with Azure AD PowerShell & Azure AD Graph</span></span>
<span data-ttu-id="5b952-411">The following fields are accessible with Azure AD PowerShell & the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="5b952-411">The following fields are accessible with Azure AD PowerShell & the Azure AD Graph API:</span></span>

* <span data-ttu-id="5b952-412">Alternate Email</span><span class="sxs-lookup"><span data-stu-id="5b952-412">Alternate Email</span></span>
* <span data-ttu-id="5b952-413">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-413">Mobile Phone</span></span>
* <span data-ttu-id="5b952-414">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-414">Office Phone</span></span>
* <span data-ttu-id="5b952-415">Authentication Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-415">Authentication Phone</span></span>
* <span data-ttu-id="5b952-416">Authentication Email</span><span class="sxs-lookup"><span data-stu-id="5b952-416">Authentication Email</span></span>

### <a name="setting-password-reset-data-with-powershell"></a><span data-ttu-id="5b952-417">Setting password reset data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-417">Setting password reset data with PowerShell</span></span>
<span data-ttu-id="5b952-418">You can set values for the following fields with Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b952-418">You can set values for the following fields with Azure AD PowerShell.</span></span>

* <span data-ttu-id="5b952-419">Alternate Email</span><span class="sxs-lookup"><span data-stu-id="5b952-419">Alternate Email</span></span>
* <span data-ttu-id="5b952-420">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-420">Mobile Phone</span></span>
* <span data-ttu-id="5b952-421">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-421">Office Phone</span></span>

<span data-ttu-id="5b952-422">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-422">**_PowerShell V1_**</span></span>

<span data-ttu-id="5b952-423">To get started, you'll first need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="5b952-423">To get started, you'll first need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span>  <span data-ttu-id="5b952-424">Once you have it installed, you can follow the steps below to configure each field.</span><span class="sxs-lookup"><span data-stu-id="5b952-424">Once you have it installed, you can follow the steps below to configure each field.</span></span>

<span data-ttu-id="5b952-425">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-425">**_PowerShell V2_**</span></span>

<span data-ttu-id="5b952-426">To get started, you'll first need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="5b952-426">To get started, you'll first need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="5b952-427">Once you have it installed, you can follow the steps below to configure each field.</span><span class="sxs-lookup"><span data-stu-id="5b952-427">Once you have it installed, you can follow the steps below to configure each field.</span></span>

<span data-ttu-id="5b952-428">To install quickly from recent versions of PowerShell which support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span><span class="sxs-lookup"><span data-stu-id="5b952-428">To install quickly from recent versions of PowerShell which support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="alternate-email---how-to-set-alternate-email-with-powershell"></a><span data-ttu-id="5b952-429">Alternate Email - How to Set Alternate Email with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-429">Alternate Email - How to Set Alternate Email with PowerShell</span></span>
<span data-ttu-id="5b952-430">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-430">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
```

<span data-ttu-id="5b952-431">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-431">**_PowerShell V2_**</span></span>

```
Connect-AzureAD
Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
```

#### <a name="mobile-phone---how-to-set-mobile-phone-with-powershell"></a><span data-ttu-id="5b952-432">Mobile Phone - How to Set Mobile Phone with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-432">Mobile Phone - How to Set Mobile Phone with PowerShell</span></span>
<span data-ttu-id="5b952-433">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-433">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
```

<span data-ttu-id="5b952-434">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-434">**_PowerShell V2_**</span></span>

```
Connect-AzureAD
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 1234567890"
```

#### <a name="office-phone---how-to-set-office-phone-with-powershell"></a><span data-ttu-id="5b952-435">Office Phone - How to Set Office Phone with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-435">Office Phone - How to Set Office Phone with PowerShell</span></span>
<span data-ttu-id="5b952-436">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-436">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"
```

<span data-ttu-id="5b952-437">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-437">**_PowerShell V2_**</span></span>

```
Connect-AzureAD
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"
```

### <a name="reading-password-reset-data-with-powershell"></a><span data-ttu-id="5b952-438">Reading password reset data with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-438">Reading password reset data with PowerShell</span></span>
<span data-ttu-id="5b952-439">You can read values for the following fields with Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b952-439">You can read values for the following fields with Azure AD PowerShell.</span></span>

* <span data-ttu-id="5b952-440">Alternate Email</span><span class="sxs-lookup"><span data-stu-id="5b952-440">Alternate Email</span></span>
* <span data-ttu-id="5b952-441">Mobile Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-441">Mobile Phone</span></span>
* <span data-ttu-id="5b952-442">Office Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-442">Office Phone</span></span>
* <span data-ttu-id="5b952-443">Authentication Phone</span><span class="sxs-lookup"><span data-stu-id="5b952-443">Authentication Phone</span></span>
* <span data-ttu-id="5b952-444">Authentication Email</span><span class="sxs-lookup"><span data-stu-id="5b952-444">Authentication Email</span></span>

#### <a name="alternate-email---how-to-read-alternate-email-with-powershell"></a><span data-ttu-id="5b952-445">Alternate Email - How to Read Alternate Email with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-445">Alternate Email - How to Read Alternate Email with PowerShell</span></span>
<span data-ttu-id="5b952-446">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-446">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
```

<span data-ttu-id="5b952-447">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-447">**_PowerShell V2_**</span></span>

```
Connect-AzureAD
Get-AzureADUser -ObjectID user@domain.com | select otherMails
```

#### <a name="mobile-phone---how-to-read-mobile-phone-with-powershell"></a><span data-ttu-id="5b952-448">Mobile Phone - How to Read Mobile Phone with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-448">Mobile Phone - How to Read Mobile Phone with PowerShell</span></span>
<span data-ttu-id="5b952-449">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-449">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
```

<span data-ttu-id="5b952-450">**_PowerShell v2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-450">**_PowerShell v2_**</span></span>

```
Connect-AzureAD
Get-AzureADUser -ObjectID user@domain.com | select Mobile
```

#### <a name="office-phone---how-to-read-office-phone-with-powershell"></a><span data-ttu-id="5b952-451">Office Phone - How to Read Office Phone with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-451">Office Phone - How to Read Office Phone with PowerShell</span></span>
<span data-ttu-id="5b952-452">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-452">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber
```

<span data-ttu-id="5b952-453">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-453">**_PowerShell V2_**</span></span>

```
Connect-AzureAD
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber
```

#### <a name="authentication-phone---how-to-read-authentication-phone-with-powershell"></a><span data-ttu-id="5b952-454">Authentication Phone - How to Read Authentication Phone with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-454">Authentication Phone - How to Read Authentication Phone with PowerShell</span></span>
<span data-ttu-id="5b952-455">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-455">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
```

<span data-ttu-id="5b952-456">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-456">**_PowerShell V2_**</span></span>

```
Not possible in PowerShell V2
```

#### <a name="authentication-email---how-to-read-authentication-email-with-powershell"></a><span data-ttu-id="5b952-457">Authentication Email - How to Read Authentication Email with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b952-457">Authentication Email - How to Read Authentication Email with PowerShell</span></span>
<span data-ttu-id="5b952-458">**_PowerShell V1_**</span><span class="sxs-lookup"><span data-stu-id="5b952-458">**_PowerShell V1_**</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

<span data-ttu-id="5b952-459">**_PowerShell V2_**</span><span class="sxs-lookup"><span data-stu-id="5b952-459">**_PowerShell V2_**</span></span>

```
Not possible in PowerShell V2
```
## <a name="how-does-password-reset-work-for-b2b-users"></a><span data-ttu-id="5b952-460">How does password reset work for B2B users?</span><span class="sxs-lookup"><span data-stu-id="5b952-460">How does password reset work for B2B users?</span></span>
<span data-ttu-id="5b952-461">Password reset and change is fully supported with all B2B configurations.</span><span class="sxs-lookup"><span data-stu-id="5b952-461">Password reset and change is fully supported with all B2B configurations.</span></span>  <span data-ttu-id="5b952-462">Read below for the 3 explicit B2B cases supported by password reset.</span><span class="sxs-lookup"><span data-stu-id="5b952-462">Read below for the 3 explicit B2B cases supported by password reset.</span></span>

1. <span data-ttu-id="5b952-463">**Users from a partner org with an existing Azure AD tenant** - If the organization you are partnering with has an existing Azure AD tenant, we will **respect whatever password reset policies are enabled in that tenant**.</span><span class="sxs-lookup"><span data-stu-id="5b952-463">**Users from a partner org with an existing Azure AD tenant** - If the organization you are partnering with has an existing Azure AD tenant, we will **respect whatever password reset policies are enabled in that tenant**.</span></span> <span data-ttu-id="5b952-464">For password reset to work, the partner organization just needs to make sure Azure AD SSPR is enabled, which is no additional charge for O365 customers, and can be enabled by following the steps in our [Getting Started with Password Management](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guide.</span><span class="sxs-lookup"><span data-stu-id="5b952-464">For password reset to work, the partner organization just needs to make sure Azure AD SSPR is enabled, which is no additional charge for O365 customers, and can be enabled by following the steps in our [Getting Started with Password Management](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guide.</span></span>
2. <span data-ttu-id="5b952-465">**Users who signed up using [self-service sign up](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-signup)** - If the organization you are partnering with used the [self-service sign up](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-signup) feature to get into a tenant, we will let them reset out of the box with the email they registered.</span><span class="sxs-lookup"><span data-stu-id="5b952-465">**Users who signed up using [self-service sign up](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-signup)** - If the organization you are partnering with used the [self-service sign up](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-signup) feature to get into a tenant, we will let them reset out of the box with the email they registered.</span></span>
3. <span data-ttu-id="5b952-466">**B2B users** - Any new B2B users created using the new [Azure AD B2B capabilities](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) will also be able to reset their passwords out of the box with the email they registered during the invite process.</span><span class="sxs-lookup"><span data-stu-id="5b952-466">**B2B users** - Any new B2B users created using the new [Azure AD B2B capabilities](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) will also be able to reset their passwords out of the box with the email they registered during the invite process.</span></span>

<span data-ttu-id="5b952-467">To test any of this, just go to http://passwordreset.microsoftonline.com with one of these partner users.</span><span class="sxs-lookup"><span data-stu-id="5b952-467">To test any of this, just go to http://passwordreset.microsoftonline.com with one of these partner users.</span></span>  <span data-ttu-id="5b952-468">As long as they have an alternate email or authentication email defined, password reset will work as expected.</span><span class="sxs-lookup"><span data-stu-id="5b952-468">As long as they have an alternate email or authentication email defined, password reset will work as expected.</span></span>  <span data-ttu-id="5b952-469">More info on data used by sspr here can be found in our [What data is used by Password Reset](https://azure.microsoft.com/en-us/documentation/articles/active-directory-passwords-learn-more/#what-data-is-used-by-password-reset) overview.</span><span class="sxs-lookup"><span data-stu-id="5b952-469">More info on data used by sspr here can be found in our [What data is used by Password Reset](https://azure.microsoft.com/en-us/documentation/articles/active-directory-passwords-learn-more/#what-data-is-used-by-password-reset) overview.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b952-470">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b952-470">Next steps</span></span>
<span data-ttu-id="5b952-471">Below are links to all of the Azure AD Password Reset documentation pages:</span><span class="sxs-lookup"><span data-stu-id="5b952-471">Below are links to all of the Azure AD Password Reset documentation pages:</span></span>

* <span data-ttu-id="5b952-472">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="5b952-472">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="5b952-473">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="5b952-473">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
* <span data-ttu-id="5b952-474">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span><span class="sxs-lookup"><span data-stu-id="5b952-474">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span></span>
* <span data-ttu-id="5b952-475">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="5b952-475">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span></span>
* <span data-ttu-id="5b952-476">[**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs</span><span class="sxs-lookup"><span data-stu-id="5b952-476">[**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs</span></span>
* <span data-ttu-id="5b952-477">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span><span class="sxs-lookup"><span data-stu-id="5b952-477">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span></span>
* <span data-ttu-id="5b952-478">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span><span class="sxs-lookup"><span data-stu-id="5b952-478">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span></span>
* <span data-ttu-id="5b952-479">[**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="5b952-479">[**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions</span></span>
* <span data-ttu-id="5b952-480">[**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service</span><span class="sxs-lookup"><span data-stu-id="5b952-480">[**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service</span></span>

[001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-learn-more/001.jpg "Image_001.jpg"
[002]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-learn-more/002.jpg "Image_002.jpg"


