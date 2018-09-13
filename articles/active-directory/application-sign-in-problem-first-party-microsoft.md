---
title: Problems signing in to a Microsoft application | Microsoft Docs
description: Troubleshoot common problems faced when signing in to first-party Microsoft Applications using Azure AD (like Office 365)
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: c4e4316c38cc568bb5a8dbbd2db353ee75f9af4c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662947"
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="4394e-103">Problems signing in to a Microsoft application</span><span class="sxs-lookup"><span data-stu-id="4394e-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="4394e-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span><span class="sxs-lookup"><span data-stu-id="4394e-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="4394e-105">There are three main ways that a user can get access to a Microsoft-published application.</span><span class="sxs-lookup"><span data-stu-id="4394e-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="4394e-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span><span class="sxs-lookup"><span data-stu-id="4394e-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="4394e-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span><span class="sxs-lookup"><span data-stu-id="4394e-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="4394e-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span><span class="sxs-lookup"><span data-stu-id="4394e-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="4394e-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span><span class="sxs-lookup"><span data-stu-id="4394e-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="4394e-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span><span class="sxs-lookup"><span data-stu-id="4394e-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="4394e-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span><span class="sxs-lookup"><span data-stu-id="4394e-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="4394e-112">General Problem Areas with Application Access to consider</span><span class="sxs-lookup"><span data-stu-id="4394e-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="4394e-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="4394e-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="4394e-114">Problems with the user’s account</span><span class="sxs-lookup"><span data-stu-id="4394e-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="4394e-115">Problems with groups</span><span class="sxs-lookup"><span data-stu-id="4394e-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="4394e-116">Problems with conditional access policies</span><span class="sxs-lookup"><span data-stu-id="4394e-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="4394e-117">Problems with application consent</span><span class="sxs-lookup"><span data-stu-id="4394e-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="4394e-118">Steps to troubleshoot Microsoft Application access</span><span class="sxs-lookup"><span data-stu-id="4394e-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="4394e-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="4394e-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="4394e-120">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="4394e-120">General issues to check first</span></span>

  * <span data-ttu-id="4394e-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span><span class="sxs-lookup"><span data-stu-id="4394e-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="4394e-122">Make sure the user’s account is **not locked out.**</span><span class="sxs-lookup"><span data-stu-id="4394e-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="4394e-123">Make sure the **user’s account exists** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4394e-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="4394e-124">Check if a user account exists in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4394e-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="4394e-125">Make sure the user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="4394e-125">Make sure the user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="4394e-126">Make sure the user’s **password is not expired or forgotten.**</span><span class="sxs-lookup"><span data-stu-id="4394e-126">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="4394e-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="4394e-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="4394e-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="4394e-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="4394e-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="4394e-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="4394e-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="4394e-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="4394e-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="4394e-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="4394e-132">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span><span class="sxs-lookup"><span data-stu-id="4394e-132">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="4394e-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="4394e-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="4394e-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span><span class="sxs-lookup"><span data-stu-id="4394e-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="4394e-135">Ensure the user or has a **license assigned.**</span><span class="sxs-lookup"><span data-stu-id="4394e-135">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="4394e-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="4394e-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="4394e-137">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span><span class="sxs-lookup"><span data-stu-id="4394e-137">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="4394e-138">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="4394e-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="4394e-139">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span><span class="sxs-lookup"><span data-stu-id="4394e-139">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="4394e-140">Check a dynamic group’s membership criteria</span><span class="sxs-lookup"><span data-stu-id="4394e-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="4394e-141">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span><span class="sxs-lookup"><span data-stu-id="4394e-141">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="4394e-142">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="4394e-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="4394e-143">Once you make sure the license is assigned, make sure the license is **not expired**.</span><span class="sxs-lookup"><span data-stu-id="4394e-143">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="4394e-144">Make sure the license is **for the application** they are accessing.</span><span class="sxs-lookup"><span data-stu-id="4394e-144">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="4394e-145">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span><span class="sxs-lookup"><span data-stu-id="4394e-145">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="4394e-146">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span><span class="sxs-lookup"><span data-stu-id="4394e-146">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="4394e-147">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span><span class="sxs-lookup"><span data-stu-id="4394e-147">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="4394e-148">Problems with the user’s account</span><span class="sxs-lookup"><span data-stu-id="4394e-148">Problems with the user’s account</span></span>

<span data-ttu-id="4394e-149">Application access can be blocked due to a problem with a user that is assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="4394e-149">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="4394e-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span><span class="sxs-lookup"><span data-stu-id="4394e-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="4394e-151">Check if a user account exists in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4394e-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="4394e-152">Check a user’s account status</span><span class="sxs-lookup"><span data-stu-id="4394e-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="4394e-153">Reset a user’s password</span><span class="sxs-lookup"><span data-stu-id="4394e-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="4394e-154">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="4394e-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="4394e-155">Check a user’s multi-factor authentication status</span><span class="sxs-lookup"><span data-stu-id="4394e-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="4394e-156">Check a user’s authentication contact info</span><span class="sxs-lookup"><span data-stu-id="4394e-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="4394e-157">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="4394e-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="4394e-158">Check a user’s assigned licenses</span><span class="sxs-lookup"><span data-stu-id="4394e-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="4394e-159">Assign a user a license</span><span class="sxs-lookup"><span data-stu-id="4394e-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="4394e-160">Check if a user account exists in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4394e-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="4394e-161">To check if a user’s account is present, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-161">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-162">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-162">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-163">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-163">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-164">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-164">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-165">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-165">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-166">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-166">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-167">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-167">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-168">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span><span class="sxs-lookup"><span data-stu-id="4394e-168">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="4394e-169">Check a user’s account status</span><span class="sxs-lookup"><span data-stu-id="4394e-169">Check a user’s account status</span></span>

<span data-ttu-id="4394e-170">To check a user’s account status, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-170">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-171">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-171">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-172">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-172">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-173">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-173">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-174">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-174">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-175">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-175">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-176">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-176">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-177">click **Profile**.</span><span class="sxs-lookup"><span data-stu-id="4394e-177">click **Profile**.</span></span>

8.  <span data-ttu-id="4394e-178">Under **Settings** ensure that **Block sign in** is set to **No**.</span><span class="sxs-lookup"><span data-stu-id="4394e-178">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="4394e-179">Reset a user’s password</span><span class="sxs-lookup"><span data-stu-id="4394e-179">Reset a user’s password</span></span>

<span data-ttu-id="4394e-180">To reset a user’s password, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-180">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-181">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-181">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-182">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-182">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-183">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-183">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-184">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-184">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-185">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-185">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-186">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-186">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-187">click the **Reset password** button at the top of the user blade.</span><span class="sxs-lookup"><span data-stu-id="4394e-187">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="4394e-188">click the **Reset password** button on the **Reset password** blade that appears.</span><span class="sxs-lookup"><span data-stu-id="4394e-188">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="4394e-189">Copy the **temporary password** or **enter a new password** for the user.</span><span class="sxs-lookup"><span data-stu-id="4394e-189">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="4394e-190">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4394e-190">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="4394e-191">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="4394e-191">Enable self-service password reset</span></span>

<span data-ttu-id="4394e-192">To enable self-service password reset, follow the deployment steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-192">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="4394e-193">Enable users to reset their Azure Active Directory passwords</span><span class="sxs-lookup"><span data-stu-id="4394e-193">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="4394e-194">Enable users to reset or change their Active Directory on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="4394e-194">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="4394e-195">Check a user’s multi-factor authentication status</span><span class="sxs-lookup"><span data-stu-id="4394e-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="4394e-196">To check a user’s multi-factor authentication status, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-196">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-197">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-197">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-198">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-198">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-199">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-199">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-200">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-200">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-201">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-201">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-202">click the **Multi-Factor Authentication** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="4394e-202">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="4394e-203">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="4394e-203">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="4394e-204">Find the user in the list of users by searching, filtering, or sorting.</span><span class="sxs-lookup"><span data-stu-id="4394e-204">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="4394e-205">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span><span class="sxs-lookup"><span data-stu-id="4394e-205">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="4394e-206">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span><span class="sxs-lookup"><span data-stu-id="4394e-206">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="4394e-207">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span><span class="sxs-lookup"><span data-stu-id="4394e-207">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="4394e-208">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span><span class="sxs-lookup"><span data-stu-id="4394e-208">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="4394e-209">Check a user’s authentication contact info</span><span class="sxs-lookup"><span data-stu-id="4394e-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="4394e-210">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-210">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-211">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-211">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-212">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-212">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-213">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-213">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-214">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-214">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-215">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-215">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-216">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-216">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-217">click **Profile**.</span><span class="sxs-lookup"><span data-stu-id="4394e-217">click **Profile**.</span></span>

8.  <span data-ttu-id="4394e-218">Scroll down to **Authentication contact info**.</span><span class="sxs-lookup"><span data-stu-id="4394e-218">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="4394e-219">**Review** the data registered for the user and update as needed.</span><span class="sxs-lookup"><span data-stu-id="4394e-219">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="4394e-220">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="4394e-220">Check a user’s group memberships</span></span>

<span data-ttu-id="4394e-221">To check a user’s group memberships, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-221">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-222">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-222">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-223">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-223">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-224">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-224">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-225">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-225">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-226">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-226">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-227">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-227">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-228">click **Groups** to see which groups the user is a member of.</span><span class="sxs-lookup"><span data-stu-id="4394e-228">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="4394e-229">Check a user’s assigned licenses</span><span class="sxs-lookup"><span data-stu-id="4394e-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="4394e-230">To check a user’s assigned licenses, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-230">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-231">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-231">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-232">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-232">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-233">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-233">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-234">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-234">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-235">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-235">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-236">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-236">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-237">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="4394e-237">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="4394e-238">Assign a user a license</span><span class="sxs-lookup"><span data-stu-id="4394e-238">Assign a user a license</span></span> 

<span data-ttu-id="4394e-239">To assign a license to a user, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-239">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-240">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-240">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-241">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-241">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-242">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-242">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-243">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-243">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-244">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4394e-244">click **All users**.</span></span>

6.  <span data-ttu-id="4394e-245">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-245">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-246">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="4394e-246">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="4394e-247">click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="4394e-247">click the **Assign** button.</span></span>

9.  <span data-ttu-id="4394e-248">Select **one or more products** from the list of available products.</span><span class="sxs-lookup"><span data-stu-id="4394e-248">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="4394e-249">**Optional** click the **assignment options** item to granularly assign products.</span><span class="sxs-lookup"><span data-stu-id="4394e-249">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="4394e-250">Click **Ok** when this is completed.</span><span class="sxs-lookup"><span data-stu-id="4394e-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4394e-251">Click the **Assign** button to assign these licenses to this user.</span><span class="sxs-lookup"><span data-stu-id="4394e-251">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="4394e-252">Problems with groups</span><span class="sxs-lookup"><span data-stu-id="4394e-252">Problems with groups</span></span>

<span data-ttu-id="4394e-253">Application access can be blocked due to a problem with a group that is assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="4394e-253">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="4394e-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span><span class="sxs-lookup"><span data-stu-id="4394e-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="4394e-255">Check a group’s membership</span><span class="sxs-lookup"><span data-stu-id="4394e-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="4394e-256">Check a dynamic group’s membership criteria</span><span class="sxs-lookup"><span data-stu-id="4394e-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="4394e-257">Check a group’s assigned licenses</span><span class="sxs-lookup"><span data-stu-id="4394e-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="4394e-258">Reprocess a group’s licenses</span><span class="sxs-lookup"><span data-stu-id="4394e-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="4394e-259">Assign a group a license</span><span class="sxs-lookup"><span data-stu-id="4394e-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="4394e-260">Check a group’s membership</span><span class="sxs-lookup"><span data-stu-id="4394e-260">Check a group’s membership</span></span>

<span data-ttu-id="4394e-261">To check a group’s membership, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-261">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-262">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-262">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-263">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-263">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-264">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-264">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-265">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-265">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-266">click **All groups**.</span><span class="sxs-lookup"><span data-stu-id="4394e-266">click **All groups**.</span></span>

6.  <span data-ttu-id="4394e-267">**Search** for the group you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-267">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-268">click **Members** to review the list of users assigned to this group.</span><span class="sxs-lookup"><span data-stu-id="4394e-268">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="4394e-269">Check a dynamic group’s membership criteria</span><span class="sxs-lookup"><span data-stu-id="4394e-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="4394e-270">To check a dynamic group’s membership criteria, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-270">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-271">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-271">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-272">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-272">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-273">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-273">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-274">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-274">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-275">click **All groups**.</span><span class="sxs-lookup"><span data-stu-id="4394e-275">click **All groups**.</span></span>

6.  <span data-ttu-id="4394e-276">**Search** for the group you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-276">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-277">click **Dynamic membership rules.**</span><span class="sxs-lookup"><span data-stu-id="4394e-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="4394e-278">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span><span class="sxs-lookup"><span data-stu-id="4394e-278">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="4394e-279">Check a group’s assigned licenses</span><span class="sxs-lookup"><span data-stu-id="4394e-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="4394e-280">To check a group’s assigned licenses, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-280">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-281">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-281">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-282">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-282">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-283">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-283">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-284">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-284">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-285">click **All groups**.</span><span class="sxs-lookup"><span data-stu-id="4394e-285">click **All groups**.</span></span>

6.  <span data-ttu-id="4394e-286">**Search** for the group you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-286">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-287">click **Licenses** to see which licenses the group currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="4394e-287">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="4394e-288">Reprocess a group’s licenses</span><span class="sxs-lookup"><span data-stu-id="4394e-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="4394e-289">To reprocess a group’s assigned licenses, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-289">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-290">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-290">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-291">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-291">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-292">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-292">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-293">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-293">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-294">click **All groups**.</span><span class="sxs-lookup"><span data-stu-id="4394e-294">click **All groups**.</span></span>

6.  <span data-ttu-id="4394e-295">**Search** for the group you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-295">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-296">click **Licenses** to see which licenses the group currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="4394e-296">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="4394e-297">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span><span class="sxs-lookup"><span data-stu-id="4394e-297">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="4394e-298">This may take a long time, depending on the size and complexity of the group.</span><span class="sxs-lookup"><span data-stu-id="4394e-298">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4394e-299">To do this faster, consider temporarily assigning a license to the user directly.</span><span class="sxs-lookup"><span data-stu-id="4394e-299">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="4394e-300">[Assign a user a license](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="4394e-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="4394e-301">Assign a group a license</span><span class="sxs-lookup"><span data-stu-id="4394e-301">Assign a group a license</span></span>

<span data-ttu-id="4394e-302">To assign a license to a group, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4394e-302">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="4394e-303">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-303">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-304">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-304">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-305">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-305">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-306">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-306">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-307">click **All groups**.</span><span class="sxs-lookup"><span data-stu-id="4394e-307">click **All groups**.</span></span>

6.  <span data-ttu-id="4394e-308">**Search** for the group you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="4394e-308">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4394e-309">click **Licenses** to see which licenses the group currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="4394e-309">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="4394e-310">click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="4394e-310">click the **Assign** button.</span></span>

9.  <span data-ttu-id="4394e-311">Select **one or more products** from the list of available products.</span><span class="sxs-lookup"><span data-stu-id="4394e-311">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="4394e-312">**Optional** click the **assignment options** item to granularly assign products.</span><span class="sxs-lookup"><span data-stu-id="4394e-312">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="4394e-313">Click **Ok** when this is completed.</span><span class="sxs-lookup"><span data-stu-id="4394e-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4394e-314">Click the **Assign** button to assign these licenses to this group.</span><span class="sxs-lookup"><span data-stu-id="4394e-314">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="4394e-315">This may take a long time, depending on the size and complexity of the group.</span><span class="sxs-lookup"><span data-stu-id="4394e-315">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4394e-316">To do this faster, consider temporarily assigning a license to the user directly.</span><span class="sxs-lookup"><span data-stu-id="4394e-316">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="4394e-317">[Assign a user a license](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="4394e-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="4394e-318">Problems with conditional access policies</span><span class="sxs-lookup"><span data-stu-id="4394e-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="4394e-319">Check a specific conditional access policy</span><span class="sxs-lookup"><span data-stu-id="4394e-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="4394e-320">To check or validate a single conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="4394e-320">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="4394e-321">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-321">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-322">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-322">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-323">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-323">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-324">click **Enterprise applications** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-324">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-325">click the **Conditional access** navigation item.</span><span class="sxs-lookup"><span data-stu-id="4394e-325">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="4394e-326">click the policy you are interested in inspecting.</span><span class="sxs-lookup"><span data-stu-id="4394e-326">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="4394e-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span><span class="sxs-lookup"><span data-stu-id="4394e-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4394e-328">You may wish to temporarily disable this policy to ensure it is not affecting sign ins. To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4394e-328">You may wish to temporarily disable this policy to ensure it is not affecting sign ins. To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="4394e-329">Check a specific application’s conditional access policy</span><span class="sxs-lookup"><span data-stu-id="4394e-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="4394e-330">To check or validate a single application’s currently configured conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="4394e-330">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="4394e-331">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-331">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-332">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-332">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-333">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-333">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-334">click **Enterprise applications** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-334">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-335">click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4394e-335">click **All applications**.</span></span>

6.  <span data-ttu-id="4394e-336">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span><span class="sxs-lookup"><span data-stu-id="4394e-336">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="4394e-337">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4394e-337">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="4394e-338">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span><span class="sxs-lookup"><span data-stu-id="4394e-338">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="4394e-339">click the **Conditional access** navigation item.</span><span class="sxs-lookup"><span data-stu-id="4394e-339">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="4394e-340">click the policy you are interested in inspecting.</span><span class="sxs-lookup"><span data-stu-id="4394e-340">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="4394e-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span><span class="sxs-lookup"><span data-stu-id="4394e-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="4394e-342">You may wish to temporarily disable this policy to ensure it is not affecting sign ins. To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4394e-342">You may wish to temporarily disable this policy to ensure it is not affecting sign ins. To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="4394e-343">Disable a specific conditional access policy</span><span class="sxs-lookup"><span data-stu-id="4394e-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="4394e-344">To check or validate a single conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="4394e-344">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="4394e-345">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="4394e-345">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4394e-346">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-346">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4394e-347">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4394e-347">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4394e-348">click **Enterprise applications** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4394e-348">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="4394e-349">click the **Conditional access** navigation item.</span><span class="sxs-lookup"><span data-stu-id="4394e-349">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="4394e-350">click the policy you are interested in inspecting.</span><span class="sxs-lookup"><span data-stu-id="4394e-350">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="4394e-351">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4394e-351">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="4394e-352">Problems with application consent</span><span class="sxs-lookup"><span data-stu-id="4394e-352">Problems with application consent</span></span>

<span data-ttu-id="4394e-353">Application access can be blocked because the proper permissions consent operation has not occurred.</span><span class="sxs-lookup"><span data-stu-id="4394e-353">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="4394e-354">Below are some ways you can troubleshoot and solve application consent issues:</span><span class="sxs-lookup"><span data-stu-id="4394e-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="4394e-355">Perform a user-level consent operation</span><span class="sxs-lookup"><span data-stu-id="4394e-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="4394e-356">Perform administrator-level consent operation for any application</span><span class="sxs-lookup"><span data-stu-id="4394e-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="4394e-357">Perform administrator-level consent for a single-tenant application</span><span class="sxs-lookup"><span data-stu-id="4394e-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="4394e-358">Perform administrator-level consent for a multi-tenant application</span><span class="sxs-lookup"><span data-stu-id="4394e-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="4394e-359">Perform a user-level consent operation</span><span class="sxs-lookup"><span data-stu-id="4394e-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="4394e-360">For any application, navigating to the application’s sign in screen perform a user level consent to the application for the signed-in user.</span><span class="sxs-lookup"><span data-stu-id="4394e-360">For any application, navigating to the application’s sign in screen perform a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="4394e-361">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="4394e-361">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="4394e-362">Perform administrator-level consent operation for any application</span><span class="sxs-lookup"><span data-stu-id="4394e-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="4394e-363">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span><span class="sxs-lookup"><span data-stu-id="4394e-363">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="4394e-364">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="4394e-364">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="4394e-365">Perform administrator-level consent for a single-tenant application</span><span class="sxs-lookup"><span data-stu-id="4394e-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="4394e-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span><span class="sxs-lookup"><span data-stu-id="4394e-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="4394e-367">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="4394e-367">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="4394e-368">Perform administrator-level consent for a multi-tenant application</span><span class="sxs-lookup"><span data-stu-id="4394e-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="4394e-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span><span class="sxs-lookup"><span data-stu-id="4394e-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="4394e-370">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span><span class="sxs-lookup"><span data-stu-id="4394e-370">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="4394e-371">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="4394e-371">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4394e-372">Next steps</span><span class="sxs-lookup"><span data-stu-id="4394e-372">Next steps</span></span>
[<span data-ttu-id="4394e-373">Using the admin consent endpoint</span><span class="sxs-lookup"><span data-stu-id="4394e-373">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

