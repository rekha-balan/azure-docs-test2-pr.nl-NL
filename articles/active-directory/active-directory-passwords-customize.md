---
title: 'Customize: Azure Active Directory password management | Microsoft Docs'
description: How to customize password management look and feel, behavior, and notifications in Azure AD to meet your needs.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
editor: curtand
ms.assetid: 2cddd150-8747-447a-a7cf-1d7d5775c0b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: joflore
ms.openlocfilehash: 158777301e2ed8108b4e1d21c1a571bdae7502bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564066"
---
# <a name="customizing-password-management-to-fit-your-organizations-needs"></a><span data-ttu-id="a7698-103">Customizing password management to fit your organization's needs</span><span class="sxs-lookup"><span data-stu-id="a7698-103">Customizing password management to fit your organization's needs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a7698-104">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="a7698-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="a7698-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="a7698-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
>
>

<span data-ttu-id="a7698-106">In order to give your users the best possible experience, we recommend that you explore and play with all of the password management configuration options available to you.</span><span class="sxs-lookup"><span data-stu-id="a7698-106">In order to give your users the best possible experience, we recommend that you explore and play with all of the password management configuration options available to you.</span></span> <span data-ttu-id="a7698-107">In fact, you can start exploring this right away by going to the configuration tab of the **Active Directory extension** in the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a7698-107">In fact, you can start exploring this right away by going to the configuration tab of the **Active Directory extension** in the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="a7698-108">This topic walks you through all of the different password management customizations you can make as an administrator from within **Configure** tab of your directory within the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a7698-108">This topic walks you through all of the different password management customizations you can make as an administrator from within **Configure** tab of your directory within the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="what-customization-options-are-available"></a><span data-ttu-id="a7698-109">What customization options are available?</span><span class="sxs-lookup"><span data-stu-id="a7698-109">What customization options are available?</span></span>
<span data-ttu-id="a7698-110">The below table outlines all of the customization options available to you with Azure Active Directory Password Reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-110">The below table outlines all of the customization options available to you with Azure Active Directory Password Reset.</span></span>

| <span data-ttu-id="a7698-111">Topic</span><span class="sxs-lookup"><span data-stu-id="a7698-111">Topic</span></span> | <span data-ttu-id="a7698-112">Setting</span><span class="sxs-lookup"><span data-stu-id="a7698-112">Setting</span></span> | <span data-ttu-id="a7698-113">Licenses Required</span><span class="sxs-lookup"><span data-stu-id="a7698-113">Licenses Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7698-114">How do I enable or disable password reset?</span><span class="sxs-lookup"><span data-stu-id="a7698-114">How do I enable or disable password reset?</span></span> |[<span data-ttu-id="a7698-115">Setting: users enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="a7698-115">Setting: users enabled for password reset</span></span>](#users-enabled-for-password-reset) | <ul><li><span data-ttu-id="a7698-116">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-116">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-117">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-117">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-118">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-118">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-119">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-119">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-120">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-120">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-121">How do I scope password reset to a specific set of users?</span><span class="sxs-lookup"><span data-stu-id="a7698-121">How do I scope password reset to a specific set of users?</span></span> |[<span data-ttu-id="a7698-122">Restrict password reset to specific users</span><span class="sxs-lookup"><span data-stu-id="a7698-122">Restrict password reset to specific users</span></span>](#restrict-access-to-password-reset) | <ul><li><span data-ttu-id="a7698-123">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-123">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-124">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-124">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-125">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-125">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-126">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-126">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-127">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-127">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-128">How do I change what authentication methods are supported?</span><span class="sxs-lookup"><span data-stu-id="a7698-128">How do I change what authentication methods are supported?</span></span> |[<span data-ttu-id="a7698-129">Setting: authentication methods available to users</span><span class="sxs-lookup"><span data-stu-id="a7698-129">Setting: authentication methods available to users</span></span>](#authentication-methods-available-to-users) | <ul><li><span data-ttu-id="a7698-130">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-130">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-131">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-131">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-132">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-132">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-133">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-133">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-134">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-134">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-135">How do I change number of authentication methods required?</span><span class="sxs-lookup"><span data-stu-id="a7698-135">How do I change number of authentication methods required?</span></span> |[<span data-ttu-id="a7698-136">Setting: number of authentication methods required</span><span class="sxs-lookup"><span data-stu-id="a7698-136">Setting: number of authentication methods required</span></span>](#number-of-authentication-methods-required) | <ul><li><span data-ttu-id="a7698-137">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-137">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-138">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-138">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-139">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-139">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-140">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-140">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-141">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-141">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-142">How do I set up custom security questions?</span><span class="sxs-lookup"><span data-stu-id="a7698-142">How do I set up custom security questions?</span></span> |[<span data-ttu-id="a7698-143">Setting: custom security questions</span><span class="sxs-lookup"><span data-stu-id="a7698-143">Setting: custom security questions</span></span>](#custom-security-questions) | <ul><li><span data-ttu-id="a7698-144">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-144">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-145">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-145">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-146">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-146">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-147">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-147">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-148">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-148">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-149">How do I set up pre-canned localized security questions?</span><span class="sxs-lookup"><span data-stu-id="a7698-149">How do I set up pre-canned localized security questions?</span></span> |[<span data-ttu-id="a7698-150">Setting: knowledge-based security questions</span><span class="sxs-lookup"><span data-stu-id="a7698-150">Setting: knowledge-based security questions</span></span>](#knowledge-based-security-questions) | <ul><li><span data-ttu-id="a7698-151">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-151">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-152">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-152">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-153">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-153">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-154">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-154">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-155">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-155">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-156">How can I change how many security questions are required?</span><span class="sxs-lookup"><span data-stu-id="a7698-156">How can I change how many security questions are required?</span></span> |[<span data-ttu-id="a7698-157">Setting: number of security questions for registration or reset</span><span class="sxs-lookup"><span data-stu-id="a7698-157">Setting: number of security questions for registration or reset</span></span>](#number-of-questions-required-to-register) | <ul><li><span data-ttu-id="a7698-158">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-158">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-159">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-159">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-160">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-160">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-161">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-161">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-162">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-162">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-163">How can I force my users to register when signing in?</span><span class="sxs-lookup"><span data-stu-id="a7698-163">How can I force my users to register when signing in?</span></span> |[<span data-ttu-id="a7698-164">Enforced registration-based rollout of password reset</span><span class="sxs-lookup"><span data-stu-id="a7698-164">Enforced registration-based rollout of password reset</span></span>](#require-users-to-register-when-signing-in) | <ul><li><span data-ttu-id="a7698-165">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-165">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-166">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-166">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-167">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-167">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-168">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-168">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-169">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-169">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-170">How can I force my users to re-confirm their registered periodically?</span><span class="sxs-lookup"><span data-stu-id="a7698-170">How can I force my users to re-confirm their registered periodically?</span></span> |[<span data-ttu-id="a7698-171">Setting: number of days before users must re-confirm their authentication data</span><span class="sxs-lookup"><span data-stu-id="a7698-171">Setting: number of days before users must re-confirm their authentication data</span></span>](#number-of-days-before-users-must-confirm-their-contact-data) | <ul><li><span data-ttu-id="a7698-172">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-172">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-173">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-173">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-174">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-174">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-175">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-175">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-176">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-176">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-177">How can I customize how a user gets in touch with an admin?</span><span class="sxs-lookup"><span data-stu-id="a7698-177">How can I customize how a user gets in touch with an admin?</span></span> |[<span data-ttu-id="a7698-178">Setting: customize the "contact your administrator" link</span><span class="sxs-lookup"><span data-stu-id="a7698-178">Setting: customize the "contact your administrator" link</span></span>](#customize-the-contact-your-administrator-link) | <ul><li><span data-ttu-id="a7698-179">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-179">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-180">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-180">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-181">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-181">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-182">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-182">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-183">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-183">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-184">How can I enable or disable password writeback from the cloud admin experience?</span><span class="sxs-lookup"><span data-stu-id="a7698-184">How can I enable or disable password writeback from the cloud admin experience?</span></span> |[<span data-ttu-id="a7698-185">Setting: enable or disable password writeback</span><span class="sxs-lookup"><span data-stu-id="a7698-185">Setting: enable or disable password writeback</span></span>](#write-back-passwords-to-on-premises-directory) | <ul><li><span data-ttu-id="a7698-186">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-186">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-187">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-187">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-188">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-188">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-189">How can I allow users to unlock on-premises AD accounts without resetting a password?</span><span class="sxs-lookup"><span data-stu-id="a7698-189">How can I allow users to unlock on-premises AD accounts without resetting a password?</span></span> |[<span data-ttu-id="a7698-190">Setting: enable users to unlock their AD accounts without resetting a password</span><span class="sxs-lookup"><span data-stu-id="a7698-190">Setting: enable users to unlock their AD accounts without resetting a password</span></span>](#allow-users-to-unlock-accounts-without-resetting-their-password) | <ul><li><span data-ttu-id="a7698-191">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-191">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-192">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-192">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-193">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-193">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-194">How can I enable password reset notifications for users?</span><span class="sxs-lookup"><span data-stu-id="a7698-194">How can I enable password reset notifications for users?</span></span> |[<span data-ttu-id="a7698-195">Setting: notify users when their passwords have been reset</span><span class="sxs-lookup"><span data-stu-id="a7698-195">Setting: notify users when their passwords have been reset</span></span>](#notify-users-and-admins-when-their-own-password-has-been-reset) |  <ul><li><span data-ttu-id="a7698-196">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-196">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-197">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-197">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-198">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-198">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-199">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-199">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-200">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-200">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-201">How can I enable password reset notifications for admins?</span><span class="sxs-lookup"><span data-stu-id="a7698-201">How can I enable password reset notifications for admins?</span></span> |[<span data-ttu-id="a7698-202">Setting: notify other admins when an admin reset their own password</span><span class="sxs-lookup"><span data-stu-id="a7698-202">Setting: notify other admins when an admin reset their own password</span></span>](#notify-admins-when-other-admins-reset-their-own-passwords) | <ul><li><span data-ttu-id="a7698-203">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-203">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-204">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-204">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-205">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-205">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-206">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-206">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-207">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-207">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |
| <span data-ttu-id="a7698-208">How can I customize password reset look and feel?</span><span class="sxs-lookup"><span data-stu-id="a7698-208">How can I customize password reset look and feel?</span></span> |[<span data-ttu-id="a7698-209">Setting: company name, branding, and logo </span><span class="sxs-lookup"><span data-stu-id="a7698-209">Setting: company name, branding, and logo </span></span>](#password-management-look-and-feel) |  <ul><li><span data-ttu-id="a7698-210">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-210">O365 (any paid SKU) [cloud users only]</span></span></li><li><span data-ttu-id="a7698-211">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-211">Azure AD Basic [cloud users only]</span></span></li><li><span data-ttu-id="a7698-212">Azure AD Premium P1 or P2 [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-212">Azure AD Premium P1 or P2 [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-213">Enterprise Mobility Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-213">Enterprise Mobility Suite [cloud or on-prem users]</span></span></li><li><span data-ttu-id="a7698-214">Enterprise Cloud Suite [cloud or on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-214">Enterprise Cloud Suite [cloud or on-prem users]</span></span></li></ul> |

## <a name="password-management-look-and-feel"></a><span data-ttu-id="a7698-215">Password management look and feel</span><span class="sxs-lookup"><span data-stu-id="a7698-215">Password management look and feel</span></span>
<span data-ttu-id="a7698-216">The following table describes how each control affects the experience for users registering for password reset and resetting their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-216">The following table describes how each control affects the experience for users registering for password reset and resetting their passwords.</span></span>  <span data-ttu-id="a7698-217">You can configure these options under the **Directory Properties** section of your directory’s **Configure** tab within the [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a7698-217">You can configure these options under the **Directory Properties** section of your directory’s **Configure** tab within the [Azure Management Portal](https://manage.windowsazure.com).</span></span>

<table>
            <tbody><tr>
              <td>
                <p><span data-ttu-id="a7698-218">
                  <strong>Policy Control</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-218">
                  <strong>Policy Control</strong>
                </span></span></p>
              </td>
              <td>
                <p><span data-ttu-id="a7698-219">
                  <strong>Description</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-219">
                  <strong>Description</strong>
                </span></span></p>
              </td>
              <td>
                <p><span data-ttu-id="a7698-220">
                  <strong>Affects?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-220">
                  <strong>Affects?</strong>
                </span></span></p>
              </td>
            </tr>
            <tr>
              <td>
                <div id="directory-name">
                  <p><span data-ttu-id="a7698-221">Directory Name</span><span class="sxs-lookup"><span data-stu-id="a7698-221">Directory Name</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-222">Determines what organizational name users or admins see on password reset email communications</span><span class="sxs-lookup"><span data-stu-id="a7698-222">Determines what organizational name users or admins see on password reset email communications</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-223"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-223"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-224">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-224">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-225">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-225">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-226">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-226">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-227">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-227">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-228">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-228">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-229">
                  <strong>"Contact your administrator" emails:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-229">
                  <strong>"Contact your administrator" emails:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-230">Determines the from address friendly name, e.g. “Microsoft on behalf of <strong>Wingtip Toys</strong>”</span><span class="sxs-lookup"><span data-stu-id="a7698-230">Determines the from address friendly name, e.g. “Microsoft on behalf of <strong>Wingtip Toys</strong>”</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-231">Determines the subject name of the email, e.g. “<strong>Wingtip Toys</strong> account email verification code”</span><span class="sxs-lookup"><span data-stu-id="a7698-231">Determines the subject name of the email, e.g. “<strong>Wingtip Toys</strong> account email verification code”</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-232">
                  <strong>Password reset emails:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-232">
                  <strong>Password reset emails:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-233">Determines the from address friendly name, e.g. “Microsoft on behalf of <strong>Wingtip Toys</strong>”</span><span class="sxs-lookup"><span data-stu-id="a7698-233">Determines the from address friendly name, e.g. “Microsoft on behalf of <strong>Wingtip Toys</strong>”</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="sign-in-and-access-panel-page-appearance">
                  <p><span data-ttu-id="a7698-234">Sign in and access panel page appearance</span><span class="sxs-lookup"><span data-stu-id="a7698-234">Sign in and access panel page appearance</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-235">Determines if users visiting the password reset page see the Microsoft logo or your own custom logo.</span><span class="sxs-lookup"><span data-stu-id="a7698-235">Determines if users visiting the password reset page see the Microsoft logo or your own custom logo.</span></span>  <span data-ttu-id="a7698-236">This configuration item also adds your branding to the access panel and sign in page.</span><span class="sxs-lookup"><span data-stu-id="a7698-236">This configuration item also adds your branding to the access panel and sign in page.</span></span></p>
                <p><span data-ttu-id="a7698-237">You can learn more about the tenant branding and customization feature at <a href="https://technet.microsoft.com/library/dn532270.aspx">Add company branding to your Sign In and Access Panel pages</a>.</span><span class="sxs-lookup"><span data-stu-id="a7698-237">You can learn more about the tenant branding and customization feature at <a href="https://technet.microsoft.com/library/dn532270.aspx">Add company branding to your Sign In and Access Panel pages</a>.</span></span></p>
                                <br>
                <p><span data-ttu-id="a7698-238"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-238"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-239">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-239">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-240">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-240">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-241">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-241">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-242">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-242">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-243">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-243">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-244">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-244">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-245">Determines whether or not your logo is shown at the top of the password reset portal instead of the default Microsoft logo.</span><span class="sxs-lookup"><span data-stu-id="a7698-245">Determines whether or not your logo is shown at the top of the password reset portal instead of the default Microsoft logo.</span></span><br><br><span data-ttu-id="a7698-246">
                    <strong>Note:</strong> you may not see your logo on the first page of the password reset portal if you come to the password reset page directly.</span><span class="sxs-lookup"><span data-stu-id="a7698-246">
                    <strong>Note:</strong> you may not see your logo on the first page of the password reset portal if you come to the password reset page directly.</span></span> <span data-ttu-id="a7698-247">Once a user enters his or her username and clicks next, your logo will appear.</span><span class="sxs-lookup"><span data-stu-id="a7698-247">Once a user enters his or her username and clicks next, your logo will appear.</span></span><br><br>
<span data-ttu-id="a7698-248">You can force your logo to appear on page load by passing the <code>whr</code> parameter to the password reset page, like this: <code><a href="https://passwordreset.microsoftonline.com?whr=wingtiptoysonline.com">https://passwordreset.microsoftonline.com?whr=wingtiptoysonline.com</a></code></span><span class="sxs-lookup"><span data-stu-id="a7698-248">You can force your logo to appear on page load by passing the <code>whr</code> parameter to the password reset page, like this: <code><a href="https://passwordreset.microsoftonline.com?whr=wingtiptoysonline.com">https://passwordreset.microsoftonline.com?whr=wingtiptoysonline.com</a></code></span></span><br><br>
<span data-ttu-id="a7698-249">You can generate a link that pre-populates the username field, by passing the <code>username</code> parameter.</span><span class="sxs-lookup"><span data-stu-id="a7698-249">You can generate a link that pre-populates the username field, by passing the <code>username</code> parameter.</span></span> <span data-ttu-id="a7698-250">This will also load you organization's logo (if one is configured): <code><a href="https://passwordreset.microsoftonline.com?username=user%40wingtiptoysonline.com">https://passwordreset.microsoftonline.com?username=user%40wingtiptoysonline.com</a></code></span><span class="sxs-lookup"><span data-stu-id="a7698-250">This will also load you organization's logo (if one is configured): <code><a href="https://passwordreset.microsoftonline.com?username=user%40wingtiptoysonline.com">https://passwordreset.microsoftonline.com?username=user%40wingtiptoysonline.com</a></code></span></span></li>
                </ul>
                <p><span data-ttu-id="a7698-251">
                  <strong>”Contact your administrator” emails:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-251">
                  <strong>”Contact your administrator” emails:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-252">Determines whether or not your logo is shown at the bottom of the emails sent to admins when users choose to contact you by clicking the “contact your administrator” link on the password reset UI.</span><span class="sxs-lookup"><span data-stu-id="a7698-252">Determines whether or not your logo is shown at the bottom of the emails sent to admins when users choose to contact you by clicking the “contact your administrator” link on the password reset UI.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-253">
                  <strong>Password reset emails:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-253">
                  <strong>Password reset emails:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-254">Determines whether or not your logo is shown at the bottom of the emails sent to users when they reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-254">Determines whether or not your logo is shown at the bottom of the emails sent to users when they reset their passwords.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
          </tbody></table>

## <a name="password-management-behavior"></a><span data-ttu-id="a7698-255">Password management behavior</span><span class="sxs-lookup"><span data-stu-id="a7698-255">Password management behavior</span></span>
<span data-ttu-id="a7698-256">The following table describes how each control affects the experience for users registering for password reset and resetting their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-256">The following table describes how each control affects the experience for users registering for password reset and resetting their passwords.</span></span>  <span data-ttu-id="a7698-257">You can configure these options under the **User Password Reset Policy** section of your directory’s **Configure** tab in the [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a7698-257">You can configure these options under the **User Password Reset Policy** section of your directory’s **Configure** tab in the [Azure Management Portal](https://manage.windowsazure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a7698-258">The administrator account you are using must have an AAD Premium license assigned in order to see these policy controls.</span><span class="sxs-lookup"><span data-stu-id="a7698-258">The administrator account you are using must have an AAD Premium license assigned in order to see these policy controls.</span></span><br><br><span data-ttu-id="a7698-259">These policy controls only apply to end users resetting their passwords, not administrators.</span><span class="sxs-lookup"><span data-stu-id="a7698-259">These policy controls only apply to end users resetting their passwords, not administrators.</span></span>  <span data-ttu-id="a7698-260">**Administrators have a default policy of alternate email and/or mobile phone that is specified for them by Microsoft which cannot be changed.**</span><span class="sxs-lookup"><span data-stu-id="a7698-260">**Administrators have a default policy of alternate email and/or mobile phone that is specified for them by Microsoft which cannot be changed.**</span></span>
>
>

<table>
            <tbody><tr>
              <td>
                <p><span data-ttu-id="a7698-261">
                  <strong>Policy Control</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-261">
                  <strong>Policy Control</strong>
                </span></span></p>
              </td>
              <td>
                <p><span data-ttu-id="a7698-262">
                  <strong>Description</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-262">
                  <strong>Description</strong>
                </span></span></p>
              </td>
              <td>
                <p><span data-ttu-id="a7698-263">
                  <strong>Affects?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-263">
                  <strong>Affects?</strong>
                </span></span></p>
              </td>
            </tr>
            <tr>
              <td>
                <div id="users-enabled-for-password-reset">
                  <p><span data-ttu-id="a7698-264">Users enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="a7698-264">Users enabled for password reset</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-265">Determines if password reset is enabled for users in this directory.</span><span class="sxs-lookup"><span data-stu-id="a7698-265">Determines if password reset is enabled for users in this directory.</span></span> </p>
                <br>
                <p><span data-ttu-id="a7698-266"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-266"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-267">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-267">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-268">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-268">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-269">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-269">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-270">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-270">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-271">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-271">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-272">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-272">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-273">If set to no, no users can register their own challenge data.</span><span class="sxs-lookup"><span data-stu-id="a7698-273">If set to no, no users can register their own challenge data.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-274">If set to yes, any end user in the directory can register challenge data by going to the registration portal at <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a>.</span><span class="sxs-lookup"><span data-stu-id="a7698-274">If set to yes, any end user in the directory can register challenge data by going to the registration portal at <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a>.</span></span><br><br></li>
                  <li class="unordered"><span data-ttu-id="a7698-275">
                    <strong>Note:</strong> users must have an Azure AD Premium or Basic license assigned before they can register for password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-275">
                    <strong>Note:</strong> users must have an Azure AD Premium or Basic license assigned before they can register for password reset.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-276">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-276">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-277">If set to no, users see a message saying the must contact their admin to reset their password.</span><span class="sxs-lookup"><span data-stu-id="a7698-277">If set to no, users see a message saying the must contact their admin to reset their password.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-278">If set to yes, users are able to reset their passwords automatically by going to  <a href="http://passwordreset.microsoftonline.com">http://passwordreset.microsoftonline.com</a>, or clicking on the <strong>can’t access your account</strong> link on any Organizational ID sign-in page.</span><span class="sxs-lookup"><span data-stu-id="a7698-278">If set to yes, users are able to reset their passwords automatically by going to  <a href="http://passwordreset.microsoftonline.com">http://passwordreset.microsoftonline.com</a>, or clicking on the <strong>can’t access your account</strong> link on any Organizational ID sign-in page.</span></span><br><br></li>
                  <li class="unordered"><span data-ttu-id="a7698-279">
                    <strong>Note:</strong> users must have an Azure AD Premium or Basic license assigned before they can reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-279">
                    <strong>Note:</strong> users must have an Azure AD Premium or Basic license assigned before they can reset their passwords.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="restrict-access-to-password-reset">
                  <p><span data-ttu-id="a7698-280">Restrict access to password reset</span><span class="sxs-lookup"><span data-stu-id="a7698-280">Restrict access to password reset</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-281">Determines whether only a particular group of users is allowed to use password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-281">Determines whether only a particular group of users is allowed to use password reset.</span></span> <span data-ttu-id="a7698-282">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-282">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-283"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-283"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-284">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-284">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-285">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-285">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-286">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-286">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-287">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-287">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-288">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-288">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-289">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-289">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-290">This setting does not affect users' access to the password reset registration portal.</span><span class="sxs-lookup"><span data-stu-id="a7698-290">This setting does not affect users' access to the password reset registration portal.</span></span> <span data-ttu-id="a7698-291">If <strong>Users enabled for password reset</strong> is set to <strong>yes</strong>, all end users in your directory can register for password reset at <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a>.</span><span class="sxs-lookup"><span data-stu-id="a7698-291">If <strong>Users enabled for password reset</strong> is set to <strong>yes</strong>, all end users in your directory can register for password reset at <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a>.</span></span>
                  </li>
                </ul>
                <p><span data-ttu-id="a7698-292">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-292">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-293">If set to no, then all end users in your directory can reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-293">If set to no, then all end users in your directory can reset their passwords.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-294">If set to yes, then only end users specified in the <strong>group that can perform password reset</strong> control can reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-294">If set to yes, then only end users specified in the <strong>group that can perform password reset</strong> control can reset their passwords.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="group-that-can-perform-password-reset">
                  <p><span data-ttu-id="a7698-295">Group that can perform password reset</span><span class="sxs-lookup"><span data-stu-id="a7698-295">Group that can perform password reset</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-296">Determines what group of end users is allowed to use password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-296">Determines what group of end users is allowed to use password reset.</span></span> </p>
                <p><span data-ttu-id="a7698-297">(Only visible if <strong>restrict access to password reset</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-297">(Only visible if <strong>restrict access to password reset</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-298"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-298"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-299">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-299">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-300">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-300">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-301">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-301">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-302">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-302">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-303">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-303">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-304">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-304">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-305">If no group is specified and you click <strong>Save</strong>, an empty group called <strong>SSPRSecurityGroupUsers</strong> will be created for you.</span><span class="sxs-lookup"><span data-stu-id="a7698-305">If no group is specified and you click <strong>Save</strong>, an empty group called <strong>SSPRSecurityGroupUsers</strong> will be created for you.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-306">If you’d like to specify your own group, you can provide your own display name.</span><span class="sxs-lookup"><span data-stu-id="a7698-306">If you’d like to specify your own group, you can provide your own display name.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-307">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-307">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-308">This setting does not affect users' access to the password reset registration portal.</span><span class="sxs-lookup"><span data-stu-id="a7698-308">This setting does not affect users' access to the password reset registration portal.</span></span> <span data-ttu-id="a7698-309">If <strong>Users enabled for password reset</strong> is set to <strong>yes</strong>, all end users in your directory can register for password reset at <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a>.</span><span class="sxs-lookup"><span data-stu-id="a7698-309">If <strong>Users enabled for password reset</strong> is set to <strong>yes</strong>, all end users in your directory can register for password reset at <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a>.</span></span>
                  </li>
                </ul>
                <p><span data-ttu-id="a7698-310">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-310">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-311">If <strong>restrict access to password reset</strong> is set to <strong>yes</strong>, then only end users in this group will be able to reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-311">If <strong>restrict access to password reset</strong> is set to <strong>yes</strong>, then only end users in this group will be able to reset their passwords.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="authentication-methods-available-to-users">
                  <p><span data-ttu-id="a7698-312">Authentication methods available to users</span><span class="sxs-lookup"><span data-stu-id="a7698-312">Authentication methods available to users</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-313">Determines which challenges a user is allowed to use to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="a7698-313">Determines which challenges a user is allowed to use to reset his or her password.</span></span></p>
                <p><span data-ttu-id="a7698-314">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-314">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-315"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-315"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-316">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-316">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-317">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-317">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-318">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-318">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-319">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-319">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-320">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-320">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-321">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-321">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-322">At least one option must be selected.</span><span class="sxs-lookup"><span data-stu-id="a7698-322">At least one option must be selected.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-323">We highly recommend enabling at least 2 options to give your users the most flexibility when resetting their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-323">We highly recommend enabling at least 2 options to give your users the most flexibility when resetting their passwords.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-324">If you are using security questions, we highly recommend you use them in conjunction with another authentication method, as security questions can be less secure than phone or email-based password reset methods.</span><span class="sxs-lookup"><span data-stu-id="a7698-324">If you are using security questions, we highly recommend you use them in conjunction with another authentication method, as security questions can be less secure than phone or email-based password reset methods.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-325">
                  <strong>Which directory fields are used?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-325">
                  <strong>Which directory fields are used?</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-326">Office Phone corresponds to the <strong>Office Phone</strong> attribute on a user object in the directory.</span><span class="sxs-lookup"><span data-stu-id="a7698-326">Office Phone corresponds to the <strong>Office Phone</strong> attribute on a user object in the directory.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-327">Mobile Phone corresponds to either the <strong>Authentication Mobile</strong> attribute (which is not publically visible) or the <strong>Mobile Phone</strong> attribute (which is publically visible) on a user object in the directory.</span><span class="sxs-lookup"><span data-stu-id="a7698-327">Mobile Phone corresponds to either the <strong>Authentication Mobile</strong> attribute (which is not publically visible) or the <strong>Mobile Phone</strong> attribute (which is publically visible) on a user object in the directory.</span></span>  <span data-ttu-id="a7698-328">The service first checks <strong>Authentication Phone</strong> for data, and if there is none present, falls back to the <strong>Mobile Phone</strong> attribute.</span><span class="sxs-lookup"><span data-stu-id="a7698-328">The service first checks <strong>Authentication Phone</strong> for data, and if there is none present, falls back to the <strong>Mobile Phone</strong> attribute.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-329">Alternate Email Address corresponds to either the <strong>Authentication Email</strong> attribute (which is not publically visible) or the <strong>Alternate Email</strong> attribute on a user object in the directory.</span><span class="sxs-lookup"><span data-stu-id="a7698-329">Alternate Email Address corresponds to either the <strong>Authentication Email</strong> attribute (which is not publically visible) or the <strong>Alternate Email</strong> attribute on a user object in the directory.</span></span>  <span data-ttu-id="a7698-330">The service first checks <strong>Authentication Email</strong> for data, and if there is none present, falls back to the <strong>Alternate Email</strong> attribute.</span><span class="sxs-lookup"><span data-stu-id="a7698-330">The service first checks <strong>Authentication Email</strong> for data, and if there is none present, falls back to the <strong>Alternate Email</strong> attribute.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-331">Security Questions are stored privately and securely on a user object in the directory and can only be answered by users during registration.</span><span class="sxs-lookup"><span data-stu-id="a7698-331">Security Questions are stored privately and securely on a user object in the directory and can only be answered by users during registration.</span></span>  <span data-ttu-id="a7698-332">For security purposes, there is currently no way for an administrator to edit or see these answers.</span><span class="sxs-lookup"><span data-stu-id="a7698-332">For security purposes, there is currently no way for an administrator to edit or see these answers.</span></span><br><br></li>
                  <li class="unordered"><span data-ttu-id="a7698-333">
                    <strong>Note: </strong>by default, only the cloud attributes Office Phone and Mobile Phone are synchronized to your cloud directory from your on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="a7698-333">
                    <strong>Note: </strong>by default, only the cloud attributes Office Phone and Mobile Phone are synchronized to your cloud directory from your on-premises directory.</span></span>  <span data-ttu-id="a7698-334">To learn more about which on-premises attributes are synced to the cloud, see <a href="https://msdn.microsoft.com/library/azure/dn764938.aspx">Attributes synchronized to Azure AD.</a></span><span class="sxs-lookup"><span data-stu-id="a7698-334">To learn more about which on-premises attributes are synced to the cloud, see <a href="https://msdn.microsoft.com/library/azure/dn764938.aspx">Attributes synchronized to Azure AD.</a></span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-335">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-335">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-336">Affects which authentication methods are displayed when users are registering.</span><span class="sxs-lookup"><span data-stu-id="a7698-336">Affects which authentication methods are displayed when users are registering.</span></span>  <span data-ttu-id="a7698-337">If you do not enable a given authentication method, users will not be able to self-register for that authentication method.</span><span class="sxs-lookup"><span data-stu-id="a7698-337">If you do not enable a given authentication method, users will not be able to self-register for that authentication method.</span></span><br><br></li>
                  <li class="unordered"><span data-ttu-id="a7698-338">
                    <strong>Note: </strong>users are currently not able to register their own office phone numbers; that authentication method must be defined by their administrator.</span><span class="sxs-lookup"><span data-stu-id="a7698-338">
                    <strong>Note: </strong>users are currently not able to register their own office phone numbers; that authentication method must be defined by their administrator.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-339">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-339">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-340">Determines which authentication methods a user can use as challenges for a given verification step.</span><span class="sxs-lookup"><span data-stu-id="a7698-340">Determines which authentication methods a user can use as challenges for a given verification step.</span></span>  <span data-ttu-id="a7698-341">For example, if a user has data in both the <strong>Office Phone</strong> and <strong>Authentication Phone</strong> fields in Azure Active Directory, then he or she can use either of these authentication methods to recover his or her password.</span><span class="sxs-lookup"><span data-stu-id="a7698-341">For example, if a user has data in both the <strong>Office Phone</strong> and <strong>Authentication Phone</strong> fields in Azure Active Directory, then he or she can use either of these authentication methods to recover his or her password.</span></span><br><br></li>
                  <li class="unordered"><span data-ttu-id="a7698-342">
                    <strong>Note: </strong>users will be able to reset their password if and only if they have data present in the authentication methods you have enabled as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a7698-342">
                    <strong>Note: </strong>users will be able to reset their password if and only if they have data present in the authentication methods you have enabled as an administrator.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="number-of-authentication-methods-required">
                  <p><span data-ttu-id="a7698-343">Number of authentication methods required</span><span class="sxs-lookup"><span data-stu-id="a7698-343">Number of authentication methods required</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-344">Determines the minimum number of the available authentication methods a user must go through to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="a7698-344">Determines the minimum number of the available authentication methods a user must go through to reset his or her password.</span></span></p>
                <p><span data-ttu-id="a7698-345">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-345">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-346"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-346"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-347">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-347">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-348">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-348">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-349">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-349">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-350">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-350">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-351">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-351">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-352">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-352">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-353">Can be set to 1 or 2 authentication methods required.</span><span class="sxs-lookup"><span data-stu-id="a7698-353">Can be set to 1 or 2 authentication methods required.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-354">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-354">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-355">Determines the minimum number of authentication methods a user must register before being able to finish the registration experience.</span><span class="sxs-lookup"><span data-stu-id="a7698-355">Determines the minimum number of authentication methods a user must register before being able to finish the registration experience.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-356">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-356">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-357">Affects number of verification steps a user must go through before being able to reset a password.</span><span class="sxs-lookup"><span data-stu-id="a7698-357">Affects number of verification steps a user must go through before being able to reset a password.</span></span>  <span data-ttu-id="a7698-358">A verification step is defined to be a user using one piece of authentication information (such as a call to their office phone, or an email to their alternate email) to verify their account.</span><span class="sxs-lookup"><span data-stu-id="a7698-358">A verification step is defined to be a user using one piece of authentication information (such as a call to their office phone, or an email to their alternate email) to verify their account.</span></span><br><br></li>
                  <li class="unordered"><span data-ttu-id="a7698-359">
                    <strong>Note:</strong> If a user does not have the required amount of authentication information defined on his or her account in order to be successful resetting his or her password in accordance with the policy you’ve set, he or she will see an error page which will direct them to request an administrator to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="a7698-359">
                    <strong>Note:</strong> If a user does not have the required amount of authentication information defined on his or her account in order to be successful resetting his or her password in accordance with the policy you’ve set, he or she will see an error page which will direct them to request an administrator to reset his or her password.</span></span>  <br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="number-of-questions-required-to-register">
                  <p><span data-ttu-id="a7698-360">Number of questions required to register</span><span class="sxs-lookup"><span data-stu-id="a7698-360">Number of questions required to register</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-361">Determines the minimum number of questions a user must answer when registering for the security questions option.</span><span class="sxs-lookup"><span data-stu-id="a7698-361">Determines the minimum number of questions a user must answer when registering for the security questions option.</span></span></p>
                <p><span data-ttu-id="a7698-362">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span><span class="sxs-lookup"><span data-stu-id="a7698-362">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-363"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-363"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-364">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-364">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-365">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-365">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-366">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-366">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-367">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-367">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-368">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-368">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-369">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-369">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-370">Can be set to 3 – 5 questions required to register.</span><span class="sxs-lookup"><span data-stu-id="a7698-370">Can be set to 3 – 5 questions required to register.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-371">Number of questions required to register must be greater than or equal to the number of questions required to reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-371">Number of questions required to register must be greater than or equal to the number of questions required to reset.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-372">We recommend you set the number of questions required to register to be higher than the number required to reset so users have more flexibility when resetting their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-372">We recommend you set the number of questions required to register to be higher than the number required to reset so users have more flexibility when resetting their passwords.</span></span>  <span data-ttu-id="a7698-373">This is also a more secure configuration because we will randomly select questions for the user to answer from the pool of all of the questions they have registered.</span><span class="sxs-lookup"><span data-stu-id="a7698-373">This is also a more secure configuration because we will randomly select questions for the user to answer from the pool of all of the questions they have registered.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-374">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-374">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-375">Determines the minimum number of questions a user must answer before the user is considered fully registered for password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-375">Determines the minimum number of questions a user must answer before the user is considered fully registered for password reset.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="number-of-questions-required-to-reset">
                  <p><span data-ttu-id="a7698-376">Number of questions required to reset</span><span class="sxs-lookup"><span data-stu-id="a7698-376">Number of questions required to reset</span></span> </p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-377">Determines the minimum number of questions a user must answer when resetting a password.</span><span class="sxs-lookup"><span data-stu-id="a7698-377">Determines the minimum number of questions a user must answer when resetting a password.</span></span></p>
                <p><span data-ttu-id="a7698-378">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span><span class="sxs-lookup"><span data-stu-id="a7698-378">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-379"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-379"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-380">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-380">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-381">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-381">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-382">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-382">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-383">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-383">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-384">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-384">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-385">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-385">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-386">Can be set to 3 – 5 questions required to reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-386">Can be set to 3 – 5 questions required to reset.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-387">Number of questions required to reset must be less than or equal to the number of questions required to register.</span><span class="sxs-lookup"><span data-stu-id="a7698-387">Number of questions required to reset must be less than or equal to the number of questions required to register.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-388">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-388">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-389">Determines the minimum number of questions a user must answer before the user’s password can be reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-389">Determines the minimum number of questions a user must answer before the user’s password can be reset.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-390">At the time of password reset, this number of questions will be selected at random from the user’s total list of registered questions.</span><span class="sxs-lookup"><span data-stu-id="a7698-390">At the time of password reset, this number of questions will be selected at random from the user’s total list of registered questions.</span></span>  <span data-ttu-id="a7698-391">For example, if the user has 5 questions registered, 3 of those 5 questions will be selected at random when the user comes to reset a password.</span><span class="sxs-lookup"><span data-stu-id="a7698-391">For example, if the user has 5 questions registered, 3 of those 5 questions will be selected at random when the user comes to reset a password.</span></span>  <span data-ttu-id="a7698-392">The user must then answer all of these questions correctly before the password can be reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-392">The user must then answer all of these questions correctly before the password can be reset.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="knowledge-based-security-questions">
                  <p><span data-ttu-id="a7698-393">Knowledge based security questions</span><span class="sxs-lookup"><span data-stu-id="a7698-393">Knowledge based security questions</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-394">Defines the pre-canned security questions your users may choose from when registering for password reset and when resetting their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-394">Defines the pre-canned security questions your users may choose from when registering for password reset and when resetting their passwords.</span></span></p>
                <p><span data-ttu-id="a7698-395">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span><span class="sxs-lookup"><span data-stu-id="a7698-395">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-396"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-396"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-397">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-397">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-398">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-398">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-399">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-399">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-400">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-400">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-401">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-401">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-402">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-402">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-403">All knowledge-based questions will be localized into the full set of O365 languages based off of the user's browser locale.</span><span class="sxs-lookup"><span data-stu-id="a7698-403">All knowledge-based questions will be localized into the full set of O365 languages based off of the user's browser locale.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-404">Up to 20 total questions can be defined (the sum of your custom and knowledge-based questions).</span><span class="sxs-lookup"><span data-stu-id="a7698-404">Up to 20 total questions can be defined (the sum of your custom and knowledge-based questions).</span></span><br><br></li>
                 <li class="unordered">
<span data-ttu-id="a7698-405">Min answer character limit is 3 characters.</span><span class="sxs-lookup"><span data-stu-id="a7698-405">Min answer character limit is 3 characters.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-406">Max answer character limit is 40 characters.</span><span class="sxs-lookup"><span data-stu-id="a7698-406">Max answer character limit is 40 characters.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-407">Users may not answer the same question twice.</span><span class="sxs-lookup"><span data-stu-id="a7698-407">Users may not answer the same question twice.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-408">Users may not provide the same answer to two different questions twice.</span><span class="sxs-lookup"><span data-stu-id="a7698-408">Users may not provide the same answer to two different questions twice.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-409">Any character set may be used to define answers (including Unicode characters).</span><span class="sxs-lookup"><span data-stu-id="a7698-409">Any character set may be used to define answers (including Unicode characters).</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-410">The number of questions defined must be greater than or equal to the number of questions required to register.</span><span class="sxs-lookup"><span data-stu-id="a7698-410">The number of questions defined must be greater than or equal to the number of questions required to register.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-411">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-411">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-412">Determines which questions a user is able to provide answers for when registering for password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-412">Determines which questions a user is able to provide answers for when registering for password reset.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-413">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-413">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-414">Determines which questions a user is able to use to reset a password.</span><span class="sxs-lookup"><span data-stu-id="a7698-414">Determines which questions a user is able to use to reset a password.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="custom-security-questions">
                  <p><span data-ttu-id="a7698-415">Custom Security questions</span><span class="sxs-lookup"><span data-stu-id="a7698-415">Custom Security questions</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-416">Defines the security questions your users may choose from when registering for password reset and when resetting their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-416">Defines the security questions your users may choose from when registering for password reset and when resetting their passwords.</span></span></p>
                <p><span data-ttu-id="a7698-417">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span><span class="sxs-lookup"><span data-stu-id="a7698-417">(Only visible if the <strong>Security Questions</strong> checkbox is enabled).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-418"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-418"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-419">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-419">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-420">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-420">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-421">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-421">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-422">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-422">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-423">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-423">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-424">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-424">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-425">Up to 20 total questions can be defined (the sum of your custom and knowledge-based questions).</span><span class="sxs-lookup"><span data-stu-id="a7698-425">Up to 20 total questions can be defined (the sum of your custom and knowledge-based questions).</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-426">Max question character limit is 200 characters.</span><span class="sxs-lookup"><span data-stu-id="a7698-426">Max question character limit is 200 characters.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-427">Min answer character limit is 3 characters.</span><span class="sxs-lookup"><span data-stu-id="a7698-427">Min answer character limit is 3 characters.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-428">Max answer character limit is 40 characters.</span><span class="sxs-lookup"><span data-stu-id="a7698-428">Max answer character limit is 40 characters.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-429">Users may not answer the same question twice.</span><span class="sxs-lookup"><span data-stu-id="a7698-429">Users may not answer the same question twice.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-430">Users may not provide the same answer to two different questions twice.</span><span class="sxs-lookup"><span data-stu-id="a7698-430">Users may not provide the same answer to two different questions twice.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-431">Any character set may be used to define questions and answers (including Unicode characters).</span><span class="sxs-lookup"><span data-stu-id="a7698-431">Any character set may be used to define questions and answers (including Unicode characters).</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-432">The number of questions defined must be greater than or equal to the number of questions required to register.</span><span class="sxs-lookup"><span data-stu-id="a7698-432">The number of questions defined must be greater than or equal to the number of questions required to register.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-433">Defining different questions for different locales is not supported for custom questions.</span><span class="sxs-lookup"><span data-stu-id="a7698-433">Defining different questions for different locales is not supported for custom questions.</span></span>  <span data-ttu-id="a7698-434">All custom questions will be displayed in the language in which you enter them in the administrative UI, even if the user's browser locale is different.</span><span class="sxs-lookup"><span data-stu-id="a7698-434">All custom questions will be displayed in the language in which you enter them in the administrative UI, even if the user's browser locale is different.</span></span>  <span data-ttu-id="a7698-435">If you need these questions to be localized, please use the "knowledge based" questions instead.</span><span class="sxs-lookup"><span data-stu-id="a7698-435">If you need these questions to be localized, please use the "knowledge based" questions instead.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-436">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-436">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-437">Determines which questions a user is able to provide answers for when registering for password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-437">Determines which questions a user is able to provide answers for when registering for password reset.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-438">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-438">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-439">Determines which questions a user is able to use to reset a password.</span><span class="sxs-lookup"><span data-stu-id="a7698-439">Determines which questions a user is able to use to reset a password.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="require-users-to-register-when-signing-in">
                  <p><span data-ttu-id="a7698-440">Require users to register when signing in?</span><span class="sxs-lookup"><span data-stu-id="a7698-440">Require users to register when signing in?</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-441">Determines if a user is required to register contact data for password reset the next time he or she signs in.</span><span class="sxs-lookup"><span data-stu-id="a7698-441">Determines if a user is required to register contact data for password reset the next time he or she signs in.</span></span>  
                </p>
                <p><span data-ttu-id="a7698-442">This capability works on any sign-in page that uses a work or school account.</span><span class="sxs-lookup"><span data-stu-id="a7698-442">This capability works on any sign-in page that uses a work or school account.</span></span>  <span data-ttu-id="a7698-443">Such pages include all of Office 365, the Azure Management Portal, the Access Panel, and any federated or custom-developed applications that use Azure AD to sign in.</span><span class="sxs-lookup"><span data-stu-id="a7698-443">Such pages include all of Office 365, the Azure Management Portal, the Access Panel, and any federated or custom-developed applications that use Azure AD to sign in.</span></span>
                </p>
                <p><span data-ttu-id="a7698-444">Enforced registration will only apply to users who are enabled for password reset, so if you have used the "restrict access to password reset" feature and scoped password reset to a specific group of users, then only users in that group will be required to register for password reset when signing in.</span><span class="sxs-lookup"><span data-stu-id="a7698-444">Enforced registration will only apply to users who are enabled for password reset, so if you have used the "restrict access to password reset" feature and scoped password reset to a specific group of users, then only users in that group will be required to register for password reset when signing in.</span></span></p>
                <p><span data-ttu-id="a7698-445">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-445">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-446"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-446"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-447">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-447">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-448">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-448">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-449">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-449">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-450">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-450">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-451">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-451">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-452">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-452">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-453">If you disable this feature, you can also manually send users to <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a> to register their contact data.</span><span class="sxs-lookup"><span data-stu-id="a7698-453">If you disable this feature, you can also manually send users to <a href="http://aka.ms/ssprsetup">http://aka.ms/ssprsetup</a> to register their contact data.</span></span>  <br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-454">Users can also reach the registration portal by clicking the <strong>register for password reset</strong> link under the profile tab in the access panel.</span><span class="sxs-lookup"><span data-stu-id="a7698-454">Users can also reach the registration portal by clicking the <strong>register for password reset</strong> link under the profile tab in the access panel.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-455">Registration via this method can be dismissed by clicking the cancel button or closing the window, but users will be nagged every time they sign in if they do not register.</span><span class="sxs-lookup"><span data-stu-id="a7698-455">Registration via this method can be dismissed by clicking the cancel button or closing the window, but users will be nagged every time they sign in if they do not register.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-456">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-456">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-457">This setting does not affect the behavior of the registration portal itself, rather, it determines whether or not the registration portal is shown to users when they sign in to the access panel.</span><span class="sxs-lookup"><span data-stu-id="a7698-457">This setting does not affect the behavior of the registration portal itself, rather, it determines whether or not the registration portal is shown to users when they sign in to the access panel.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="number-of-days-before-users-must-confirm-their-contact-data">
                  <p><span data-ttu-id="a7698-458">Number of days before users must confirm their contact data</span><span class="sxs-lookup"><span data-stu-id="a7698-458">Number of days before users must confirm their contact data</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-459">When <strong>require users to register</strong> is turned on, this setting determines the period of time which can elapse before a user must re-confirm their data.</span><span class="sxs-lookup"><span data-stu-id="a7698-459">When <strong>require users to register</strong> is turned on, this setting determines the period of time which can elapse before a user must re-confirm their data.</span></span> </p>
                <p><span data-ttu-id="a7698-460">(Only visible if <strong>require users to register when signing in to the access panel</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-460">(Only visible if <strong>require users to register when signing in to the access panel</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-461"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-461"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-462">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-462">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-463">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-463">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-464">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-464">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-465">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-465">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-466">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-466">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-467">
                  <strong>Note: </strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-467">
                  <strong>Note: </strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-468">Values between 0-730 days are accepted, with 0 days meaning that users will never be asked to re-confirm their contact data.</span><span class="sxs-lookup"><span data-stu-id="a7698-468">Values between 0-730 days are accepted, with 0 days meaning that users will never be asked to re-confirm their contact data.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-469">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-469">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-470">This setting does not affect the behavior of the registration portal itself, rather, it determines whether or not the registration portal is shown to users when their contact data needs to be reconfirmed.</span><span class="sxs-lookup"><span data-stu-id="a7698-470">This setting does not affect the behavior of the registration portal itself, rather, it determines whether or not the registration portal is shown to users when their contact data needs to be reconfirmed.</span></span> <br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="customize-the-contact-your-administrator-link">
                  <p><span data-ttu-id="a7698-471">Customize the contact your administrator link?</span><span class="sxs-lookup"><span data-stu-id="a7698-471">Customize the contact your administrator link?</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-472">Controls whether or not the contact your administrator link (shown to the left) that appears on the password reset portal when an error occurs or a user waits too long on an operation points to a custom URL or email address.</span><span class="sxs-lookup"><span data-stu-id="a7698-472">Controls whether or not the contact your administrator link (shown to the left) that appears on the password reset portal when an error occurs or a user waits too long on an operation points to a custom URL or email address.</span></span></p>
                <p><span data-ttu-id="a7698-473">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-473">(Only visible if <strong>users enabled for password reset</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-474"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-474"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-475">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-475">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-476">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-476">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-477">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-477">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-478">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-478">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-479">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-479">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-480">
                  <strong>Note: </strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-480">
                  <strong>Note: </strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-481">If you enable this setting, you must choose a custom URL or email address by filling out the <strong>custom email address or url</strong> field immediately below this setting.</span><span class="sxs-lookup"><span data-stu-id="a7698-481">If you enable this setting, you must choose a custom URL or email address by filling out the <strong>custom email address or url</strong> field immediately below this setting.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-482">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-482">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-483">If set to no, users clicking the highlighted link will dispatch an email to the primary email address of all tenant administrators requesting that his or her password be reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-483">If set to no, users clicking the highlighted link will dispatch an email to the primary email address of all tenant administrators requesting that his or her password be reset.</span></span>  <span data-ttu-id="a7698-484">This email is dispatched by following the logic below:</span><span class="sxs-lookup"><span data-stu-id="a7698-484">This email is dispatched by following the logic below:</span></span><br><br></li>
                  <li class="unordered">
                    <ul>
                      <li class="unordered">
<span data-ttu-id="a7698-485">If there are password administrators, send the email to all password administrators, up to a maximum of 100 total recipients.</span><span class="sxs-lookup"><span data-stu-id="a7698-485">If there are password administrators, send the email to all password administrators, up to a maximum of 100 total recipients.</span></span><br><br></li>
                      <li class="unordered">
<span data-ttu-id="a7698-486">If there are no password administrators, send the email to all user administrators, up to a maximum of 100 total recipients.</span><span class="sxs-lookup"><span data-stu-id="a7698-486">If there are no password administrators, send the email to all user administrators, up to a maximum of 100 total recipients.</span></span><br><br></li>
                      <li class="unordered">
<span data-ttu-id="a7698-487">If there are no user administrators, send the email to all global administrators, up to a maximum of 100 total recipients.</span><span class="sxs-lookup"><span data-stu-id="a7698-487">If there are no user administrators, send the email to all global administrators, up to a maximum of 100 total recipients.</span></span><br><br></li>
                    </ul>
                  </li>
                  <li class="unordered">
<span data-ttu-id="a7698-488">If set to yes, this setting will customize the behavior of the highlighted link above to point to a custom URL or email address to which your users can navigate to get help with password reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-488">If set to yes, this setting will customize the behavior of the highlighted link above to point to a custom URL or email address to which your users can navigate to get help with password reset.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-489">If you specify a URL, it will be opened in a new tab.</span><span class="sxs-lookup"><span data-stu-id="a7698-489">If you specify a URL, it will be opened in a new tab.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-490">If you specify an email address, we’ll create a mailto link to that email address.</span><span class="sxs-lookup"><span data-stu-id="a7698-490">If you specify an email address, we’ll create a mailto link to that email address.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="custom-email-address-or-URL">
                  <p><span data-ttu-id="a7698-491">Custom email address or URL</span><span class="sxs-lookup"><span data-stu-id="a7698-491">Custom email address or URL</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-492">Controls the email address or URL to which the <strong>contact your administrator</strong> link points.</span><span class="sxs-lookup"><span data-stu-id="a7698-492">Controls the email address or URL to which the <strong>contact your administrator</strong> link points.</span></span> </p>
                <p><span data-ttu-id="a7698-493">(Only visible if <strong>customize contact your administrator link</strong> is set to <strong>yes</strong>).</span><span class="sxs-lookup"><span data-stu-id="a7698-493">(Only visible if <strong>customize contact your administrator link</strong> is set to <strong>yes</strong>).</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-494"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-494"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-495">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-495">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-496">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-496">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-497">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-497">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-498">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-498">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-499">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-499">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-500">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-500">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-501">Must be a valid intranet or extranet URL or email address.</span><span class="sxs-lookup"><span data-stu-id="a7698-501">Must be a valid intranet or extranet URL or email address.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-502">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-502">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-503">Changes where the <strong>contact your administrator</strong> link points.</span><span class="sxs-lookup"><span data-stu-id="a7698-503">Changes where the <strong>contact your administrator</strong> link points.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-504">If you provide an email address, the link will become a “mailto” link to that email address.</span><span class="sxs-lookup"><span data-stu-id="a7698-504">If you provide an email address, the link will become a “mailto” link to that email address.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-505">If you provide a URL, the link will become a standard href pointing to that URL which will open in a new tab.</span><span class="sxs-lookup"><span data-stu-id="a7698-505">If you provide a URL, the link will become a standard href pointing to that URL which will open in a new tab.</span></span>  <br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="write-back-passwords-to-on-premises-directory">
                  <p><span data-ttu-id="a7698-506">Write back passwords to on-premises directory</span><span class="sxs-lookup"><span data-stu-id="a7698-506">Write back passwords to on-premises directory</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-507">Controls whether or not Password Writeback is enabled for this directory and, if writeback is on, indicates the status of the on-premises writeback service.</span><span class="sxs-lookup"><span data-stu-id="a7698-507">Controls whether or not Password Writeback is enabled for this directory and, if writeback is on, indicates the status of the on-premises writeback service.</span></span></p>
                <p><span data-ttu-id="a7698-508">This is setting is useful if you want to temporarily disable the service without re-configuring Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a7698-508">This is setting is useful if you want to temporarily disable the service without re-configuring Azure AD Connect.</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-509"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-509"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-510">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-510">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-511">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-511">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-512">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-512">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-513">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-513">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-514">This control only appears if you have installed Password Writeback by downloading the latest version of Azure AD Connect and enabling the <strong>Password Writeback</strong> option under the <strong>optional features</strong> selection screen.</span><span class="sxs-lookup"><span data-stu-id="a7698-514">This control only appears if you have installed Password Writeback by downloading the latest version of Azure AD Connect and enabling the <strong>Password Writeback</strong> option under the <strong>optional features</strong> selection screen.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-515">If you have enabled Password Writeback and feel there is a configuration issue with the service, you can come to this tab and look at the <strong>password write back service status</strong> label to see if something is wrong.</span><span class="sxs-lookup"><span data-stu-id="a7698-515">If you have enabled Password Writeback and feel there is a configuration issue with the service, you can come to this tab and look at the <strong>password write back service status</strong> label to see if something is wrong.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-516">Statuses that can be shown are:</span><span class="sxs-lookup"><span data-stu-id="a7698-516">Statuses that can be shown are:</span></span><br><br><ul><li class="unordered"><span data-ttu-id="a7698-517"><strong>Configured </strong>– everything is working as expected</span><span class="sxs-lookup"><span data-stu-id="a7698-517"><strong>Configured </strong>– everything is working as expected</span></span><br><br></li><li class="unordered"><span data-ttu-id="a7698-518"><strong>Not configured</strong> – you have writeback installed, but we can’t reach the service, check to make sure you are not blocking outbound connections to 443 and try re-installing the service if you still have problems.</span><span class="sxs-lookup"><span data-stu-id="a7698-518"><strong>Not configured</strong> – you have writeback installed, but we can’t reach the service, check to make sure you are not blocking outbound connections to 443 and try re-installing the service if you still have problems.</span></span><br><br></li></ul></li>
                </ul>
                <p><span data-ttu-id="a7698-519">
                  <strong>Registration portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-519">
                  <strong>Registration portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-520">If writeback is deployed and configured and this switch is set to <strong>no</strong>, then writeback will be disabled, and federated and password hash sync’d users will not be able to register for password reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-520">If writeback is deployed and configured and this switch is set to <strong>no</strong>, then writeback will be disabled, and federated and password hash sync’d users will not be able to register for password reset their passwords.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-521">If the switch is set to <strong>yes</strong>, then writeback will be enabled, and federated and password hash sync’d users will be able to reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-521">If the switch is set to <strong>yes</strong>, then writeback will be enabled, and federated and password hash sync’d users will be able to reset their passwords.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-522">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-522">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-523">If writeback is deployed and configured and this switch is set to <strong>no</strong>, then writeback will be disabled, and federated and password hash sync’d users will not be able to reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-523">If writeback is deployed and configured and this switch is set to <strong>no</strong>, then writeback will be disabled, and federated and password hash sync’d users will not be able to reset their passwords.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-524">If the switch is set to <strong>yes</strong>, then writeback will be enabled, and federated and password hash sync’d users will be able to reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="a7698-524">If the switch is set to <strong>yes</strong>, then writeback will be enabled, and federated and password hash sync’d users will be able to reset their passwords.</span></span><br><br></li>
                </ul>
              </td
            </tr>
             <tr>
              <td>
                <div id="allow-users-to-unlock-accounts-without-resetting-their-password">
                  <p><span data-ttu-id="a7698-525">Allow users to unlock on-premises Active Directory accounts without resetting their password</span><span class="sxs-lookup"><span data-stu-id="a7698-525">Allow users to unlock on-premises Active Directory accounts without resetting their password</span></span></p>
                </div>
              </td>
              <td>
              <p><span data-ttu-id="a7698-526">Designates whether or not users who visit the password reset portal should be given the option to unlock their on-premises Active Directory accounts without resetting their password.</span><span class="sxs-lookup"><span data-stu-id="a7698-526">Designates whether or not users who visit the password reset portal should be given the option to unlock their on-premises Active Directory accounts without resetting their password.</span></span> <span data-ttu-id="a7698-527">By default, Azure AD will always unlock accounts when performing a password reset, this setting allows you to separate those two operations.</span><span class="sxs-lookup"><span data-stu-id="a7698-527">By default, Azure AD will always unlock accounts when performing a password reset, this setting allows you to separate those two operations.</span></span></p>
              <p><span data-ttu-id="a7698-528">If set to “yes”, then users will be given the option to reset their password and unlock the account, or to unlock without resetting the password.</span><span class="sxs-lookup"><span data-stu-id="a7698-528">If set to “yes”, then users will be given the option to reset their password and unlock the account, or to unlock without resetting the password.</span></span> </p>
              <p><span data-ttu-id="a7698-529">If set to “no”, then users will only be able to perform a combined password reset and account unlock operation.</span><span class="sxs-lookup"><span data-stu-id="a7698-529">If set to “no”, then users will only be able to perform a combined password reset and account unlock operation.</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-530"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-530"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-531">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-531">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-532">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-532">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-533">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-533">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-534">
                  <strong>Note:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-534">
                  <strong>Note:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-535">In order to use this feature, you must install the August 2015 or later release of Azure AD Connect (v.</span><span class="sxs-lookup"><span data-stu-id="a7698-535">In order to use this feature, you must install the August 2015 or later release of Azure AD Connect (v.</span></span> <span data-ttu-id="a7698-536">1.0.8667.0 or greater).</span><span class="sxs-lookup"><span data-stu-id="a7698-536">1.0.8667.0 or greater).</span></span><br><br><span data-ttu-id="a7698-537"><a href="http://www.microsoft.com/download/details.aspx?id=47594">Click here to download the latest version of Azure AD Connect.</a></span><span class="sxs-lookup"><span data-stu-id="a7698-537"><a href="http://www.microsoft.com/download/details.aspx?id=47594">Click here to download the latest version of Azure AD Connect.</a></span></span></li>
                  <li class="unordered"><span data-ttu-id="a7698-538">
                    <strong>Note:</strong> In order to test this feature, you will need enable password writeback, and  use an account that is sourced from on-premises (like a federated or password synchronized user) and has a locked account.</span><span class="sxs-lookup"><span data-stu-id="a7698-538">
                    <strong>Note:</strong> In order to test this feature, you will need enable password writeback, and  use an account that is sourced from on-premises (like a federated or password synchronized user) and has a locked account.</span></span>  <span data-ttu-id="a7698-539">Users who do not come from on premises and do not have a locked account will not see the option to unlock their accounts.</span><span class="sxs-lookup"><span data-stu-id="a7698-539">Users who do not come from on premises and do not have a locked account will not see the option to unlock their accounts.</span></span></li>
                </ul>
                <p><span data-ttu-id="a7698-540">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-540">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-541">After enabling this option, when a user with an on-premises account that is locked arrives at the password reset portal, he or she will be given the option to unlock their account without resetting their password.</span><span class="sxs-lookup"><span data-stu-id="a7698-541">After enabling this option, when a user with an on-premises account that is locked arrives at the password reset portal, he or she will be given the option to unlock their account without resetting their password.</span></span><br><br><span data-ttu-id="a7698-542">Note that if you are using password writeback, accounts are already automatically unlocked when the password is reset, and that this option simply decouples those operations.</span><span class="sxs-lookup"><span data-stu-id="a7698-542">Note that if you are using password writeback, accounts are already automatically unlocked when the password is reset, and that this option simply decouples those operations.</span></span><br><br><span data-ttu-id="a7698-543">This is an especially useful option to enable if you find that many of your helpdesk calls are generated by account unlock requests.</span><span class="sxs-lookup"><span data-stu-id="a7698-543">This is an especially useful option to enable if you find that many of your helpdesk calls are generated by account unlock requests.</span></span></li>
                </ul>
              </td>
            </tr>
          </tbody></table>

## <a name="password-management-notifications"></a><span data-ttu-id="a7698-544">Password management notifications</span><span class="sxs-lookup"><span data-stu-id="a7698-544">Password management notifications</span></span>
<span data-ttu-id="a7698-545">The following table describes how each control affects the experience for users and admins who receive password reset notifications.</span><span class="sxs-lookup"><span data-stu-id="a7698-545">The following table describes how each control affects the experience for users and admins who receive password reset notifications.</span></span>  <span data-ttu-id="a7698-546">You can configure these options under the **Notifications** section of your directory’s **Configure** tab in the [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a7698-546">You can configure these options under the **Notifications** section of your directory’s **Configure** tab in the [Azure Management Portal](https://manage.windowsazure.com).</span></span>

<table>
            <tbody><tr>
              <td>
                <p><span data-ttu-id="a7698-547">
                  <strong>Policy Control</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-547">
                  <strong>Policy Control</strong>
                </span></span></p>
              </td>
              <td>
                <p><span data-ttu-id="a7698-548">
                  <strong>Description</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-548">
                  <strong>Description</strong>
                </span></span></p>
              </td>
              <td>
                <p><span data-ttu-id="a7698-549">
                  <strong>Affects?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-549">
                  <strong>Affects?</strong>
                </span></span></p>
              </td>
            </tr>
            <tr>
              <td>
                <div id="notify-admins-when-other-admins-reset-their-own-passwords">
                  <p><span data-ttu-id="a7698-550">Notify admins when other admins reset their own passwords</span><span class="sxs-lookup"><span data-stu-id="a7698-550">Notify admins when other admins reset their own passwords</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-551">Determines whether or not all global admins will be notified via an email to their primary email address when another admin of any type resets his or her own password.</span><span class="sxs-lookup"><span data-stu-id="a7698-551">Determines whether or not all global admins will be notified via an email to their primary email address when another admin of any type resets his or her own password.</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-552"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-552"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-553">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-553">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-554">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-554">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-555">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-555">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-556">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-556">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-557">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-557">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-558">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-558">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-559">If set to no, then no notifications will be sent.</span><span class="sxs-lookup"><span data-stu-id="a7698-559">If set to no, then no notifications will be sent.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-560">If set to yes, then all other global administrators will be notified when any single admin resets his or her own password.</span><span class="sxs-lookup"><span data-stu-id="a7698-560">If set to yes, then all other global administrators will be notified when any single admin resets his or her own password.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-561">This notification is sent via an email to the primary email addresses of all other global admins in the organization.</span><span class="sxs-lookup"><span data-stu-id="a7698-561">This notification is sent via an email to the primary email addresses of all other global admins in the organization.</span></span><br><br></li>
                </ul>
                <p><span data-ttu-id="a7698-562">
                  <strong>Example:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-562">
                  <strong>Example:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-563">If this option was enabled when admin A resets his password, and there are 3 other admins in the tenant, B, C, and D, then admins B, C, and D would receive an email indicating admin A reset his password.</span><span class="sxs-lookup"><span data-stu-id="a7698-563">If this option was enabled when admin A resets his password, and there are 3 other admins in the tenant, B, C, and D, then admins B, C, and D would receive an email indicating admin A reset his password.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
            <tr>
              <td>
                <div id="notify-users-and-admins-when-their-own-password-has-been-reset">
                  <p><span data-ttu-id="a7698-564">Notify users and admins when their own password has been reset</span><span class="sxs-lookup"><span data-stu-id="a7698-564">Notify users and admins when their own password has been reset</span></span></p>
                </div>
              </td>
              <td>
                <p><span data-ttu-id="a7698-565">Determines whether or not end users or admins who reset their own passwords will receive an email notification that their password has been reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-565">Determines whether or not end users or admins who reset their own passwords will receive an email notification that their password has been reset.</span></span></p>
                <br>
                <p><span data-ttu-id="a7698-566"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span><span class="sxs-lookup"><span data-stu-id="a7698-566"><b><u>Requires one of the following licenses <a href="https://docs.microsoft.com/azure/active-directory/active-directory-passwords#pricing-and-availability">learn more</a></u></b></span></span></p>
                 <ul>
                   <li><span data-ttu-id="a7698-567">O365 (any paid SKU) [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-567">O365 (any paid SKU) [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-568">Azure AD Basic [cloud users only]</span><span class="sxs-lookup"><span data-stu-id="a7698-568">Azure AD Basic [cloud users only]</span></span></li>
                   <li><span data-ttu-id="a7698-569">Azure AD Premium P1 or P2 [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-569">Azure AD Premium P1 or P2 [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-570">Enterprise Mobility Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-570">Enterprise Mobility Suite [cloud and on-prem users]</span></span></li>
                   <li><span data-ttu-id="a7698-571">Enterprise Cloud Suite [cloud and on-prem users]</span><span class="sxs-lookup"><span data-stu-id="a7698-571">Enterprise Cloud Suite [cloud and on-prem users]</span></span></li>
                 </ul>
              </td>
              <td>
                <p><span data-ttu-id="a7698-572">
                  <strong>Password reset portal:</strong>
                </span><span class="sxs-lookup"><span data-stu-id="a7698-572">
                  <strong>Password reset portal:</strong>
                </span></span></p>
                <ul>
                  <li class="unordered">
<span data-ttu-id="a7698-573">If set to no, then no notifications will be sent.</span><span class="sxs-lookup"><span data-stu-id="a7698-573">If set to no, then no notifications will be sent.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-574">If set to yes, then whenever a user or admin resets his own password, he or she will receive a notification indicating his or her password has been reset.</span><span class="sxs-lookup"><span data-stu-id="a7698-574">If set to yes, then whenever a user or admin resets his own password, he or she will receive a notification indicating his or her password has been reset.</span></span><br><br></li>
                  <li class="unordered">
<span data-ttu-id="a7698-575">This notification is sent via an email to the user’s User Principal Name, and alternate (or authentication) email address of the user who reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="a7698-575">This notification is sent via an email to the user’s User Principal Name, and alternate (or authentication) email address of the user who reset his or her password.</span></span><br><br></li>
                </ul>
              </td>
            </tr>
          </tbody></table>


<br/>
<br/>
<br/>

## <a name="next-steps"></a><span data-ttu-id="a7698-576">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7698-576">Next steps</span></span>
<span data-ttu-id="a7698-577">Below are links to all of the Azure AD Password Reset documentation pages:</span><span class="sxs-lookup"><span data-stu-id="a7698-577">Below are links to all of the Azure AD Password Reset documentation pages:</span></span>

* <span data-ttu-id="a7698-578">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="a7698-578">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="a7698-579">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="a7698-579">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
* <span data-ttu-id="a7698-580">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span><span class="sxs-lookup"><span data-stu-id="a7698-580">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span></span>
* <span data-ttu-id="a7698-581">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="a7698-581">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span></span>
* <span data-ttu-id="a7698-582">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span><span class="sxs-lookup"><span data-stu-id="a7698-582">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span></span>
* <span data-ttu-id="a7698-583">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span><span class="sxs-lookup"><span data-stu-id="a7698-583">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span></span>
* <span data-ttu-id="a7698-584">[**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="a7698-584">[**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions</span></span>
* <span data-ttu-id="a7698-585">[**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service</span><span class="sxs-lookup"><span data-stu-id="a7698-585">[**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service</span></span>
* <span data-ttu-id="a7698-586">[**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works</span><span class="sxs-lookup"><span data-stu-id="a7698-586">[**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works</span></span>

[001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-customize/001.jpg "Image_001.jpg"

