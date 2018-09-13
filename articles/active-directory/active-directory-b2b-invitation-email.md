---
title: The elements of the Azure Active Directory B2B collaboration invitation email | Microsoft Docs
description: Azure Active Directory B2B collaboration invitation email template
services: active-directory
documentationcenter: ''
author: sasubram
manager: femila
editor: ''
tags: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 02/09/2017
ms.author: sasubram
ms.openlocfilehash: e82e1d656297ed437c573f6c6895375364563e1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550149"
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="aec20-103">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="aec20-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="aec20-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aec20-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="aec20-105">The primary goal for this is to increase trust in the recipient and add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span><span class="sxs-lookup"><span data-stu-id="aec20-105">The primary goal for this is to increase trust in the recipient and add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="aec20-106">This is a key component to reducing sharing friction.</span><span class="sxs-lookup"><span data-stu-id="aec20-106">This is a key component to reducing sharing friction.</span></span> <span data-ttu-id="aec20-107">And of course, we also want the email to look great!</span><span class="sxs-lookup"><span data-stu-id="aec20-107">And of course, we also want the email to look great!</span></span>

![Azure AD B2b invitation email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="aec20-109">Explaining the email</span><span class="sxs-lookup"><span data-stu-id="aec20-109">Explaining the email</span></span>
<span data-ttu-id="aec20-110">Let's look at a few elements of the email so you know how best to make use of these capabilities.</span><span class="sxs-lookup"><span data-stu-id="aec20-110">Let's look at a few elements of the email so you know how best to make use of these capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="aec20-111">Subject</span><span class="sxs-lookup"><span data-stu-id="aec20-111">Subject</span></span>
<span data-ttu-id="aec20-112">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span><span class="sxs-lookup"><span data-stu-id="aec20-112">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="aec20-113">From address</span><span class="sxs-lookup"><span data-stu-id="aec20-113">From address</span></span>
<span data-ttu-id="aec20-114">We use a LinkedIn-like pattern for the From address.</span><span class="sxs-lookup"><span data-stu-id="aec20-114">We use a LinkedIn-like pattern for the From address.</span></span> <span data-ttu-id="aec20-115">Our goal here is to be clear who the inviter is and from which company and also clarify that the email is coming from a Microsoft email address.</span><span class="sxs-lookup"><span data-stu-id="aec20-115">Our goal here is to be clear who the inviter is and from which company and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="aec20-116">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="aec20-116">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="aec20-117">Reply To</span><span class="sxs-lookup"><span data-stu-id="aec20-117">Reply To</span></span>
<span data-ttu-id="aec20-118">The reply to email is set to the inviter's email when available, so that replying to the email will send an email back to the inviter.</span><span class="sxs-lookup"><span data-stu-id="aec20-118">The reply to email is set to the inviter's email when available, so that replying to the email will send an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="aec20-119">Branding</span><span class="sxs-lookup"><span data-stu-id="aec20-119">Branding</span></span>
<span data-ttu-id="aec20-120">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span><span class="sxs-lookup"><span data-stu-id="aec20-120">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="aec20-121">If you want to take advantage of this, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span><span class="sxs-lookup"><span data-stu-id="aec20-121">If you want to take advantage of this, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="aec20-122">The banner logo will show up in the email.</span><span class="sxs-lookup"><span data-stu-id="aec20-122">The banner logo will show up in the email.</span></span> <span data-ttu-id="aec20-123">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span><span class="sxs-lookup"><span data-stu-id="aec20-123">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="aec20-124">In addition, the company name also shows up in the call to action.</span><span class="sxs-lookup"><span data-stu-id="aec20-124">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="aec20-125">Call to action</span><span class="sxs-lookup"><span data-stu-id="aec20-125">Call to action</span></span>
<span data-ttu-id="aec20-126">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span><span class="sxs-lookup"><span data-stu-id="aec20-126">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="aec20-127">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span><span class="sxs-lookup"><span data-stu-id="aec20-127">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="aec20-128">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span><span class="sxs-lookup"><span data-stu-id="aec20-128">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="aec20-129">When the recipient has been added without the need for invitations, this button doesn't show up.</span><span class="sxs-lookup"><span data-stu-id="aec20-129">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="aec20-130">Inviter's information</span><span class="sxs-lookup"><span data-stu-id="aec20-130">Inviter's information</span></span>
<span data-ttu-id="aec20-131">The inviter's display name will be included in the email.</span><span class="sxs-lookup"><span data-stu-id="aec20-131">The inviter's display name will be included in the email.</span></span> <span data-ttu-id="aec20-132">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span><span class="sxs-lookup"><span data-stu-id="aec20-132">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="aec20-133">Both of these are intended to increase your recipient's confidence in the email.</span><span class="sxs-lookup"><span data-stu-id="aec20-133">Both of these are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="aec20-134">If the inviter hasn't yet set up their profile picture, Azure AD creates an icon with the inviter's initials in place of the picture as shown:</span><span class="sxs-lookup"><span data-stu-id="aec20-134">If the inviter hasn't yet set up their profile picture, Azure AD creates an icon with the inviter's initials in place of the picture as shown:</span></span>

  ![displaying the inviter's initials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="aec20-136">Body</span><span class="sxs-lookup"><span data-stu-id="aec20-136">Body</span></span>
<span data-ttu-id="aec20-137">This will contain the message that the inviter composes or is passed through the invitation API.</span><span class="sxs-lookup"><span data-stu-id="aec20-137">This will contain the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="aec20-138">This is just a text area, which will not process HTML tags for security reasons.</span><span class="sxs-lookup"><span data-stu-id="aec20-138">This is just a text area, which will not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="aec20-139">Footer section</span><span class="sxs-lookup"><span data-stu-id="aec20-139">Footer section</span></span>
<span data-ttu-id="aec20-140">The footer contains the Microsoft company brand and will let the recipient know if the email was sent from an unmonitored alias.</span><span class="sxs-lookup"><span data-stu-id="aec20-140">The footer contains the Microsoft company brand and will let the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="aec20-141">Special cases:</span><span class="sxs-lookup"><span data-stu-id="aec20-141">Special cases:</span></span>

- <span data-ttu-id="aec20-142">The inviter doesn't have an email address in the inviting tenancy</span><span class="sxs-lookup"><span data-stu-id="aec20-142">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![picture of inviter doesn't have an email address in the inviting tenancy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="aec20-144">The recipient doesn't need to redeem the invitation</span><span class="sxs-lookup"><span data-stu-id="aec20-144">The recipient doesn't need to redeem the invitation</span></span>

  ![when recipient doesn't need to redeem invitation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="aec20-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="aec20-146">Next steps</span></span>

<span data-ttu-id="aec20-147">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="aec20-147">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="aec20-148">What is Azure AD B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="aec20-148">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="aec20-149">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="aec20-149">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="aec20-150">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="aec20-150">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="aec20-151">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="aec20-151">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="aec20-152">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="aec20-152">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="aec20-153">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="aec20-153">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="aec20-154">Azure Active Directory B2B collaboration frequently-asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="aec20-154">Azure Active Directory B2B collaboration frequently-asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="aec20-155">Azure Active Directory B2B collaboration API and customization</span><span class="sxs-lookup"><span data-stu-id="aec20-155">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="aec20-156">Multi-factor authentication for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="aec20-156">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="aec20-157">Add B2B collaboration users without an invitation</span><span class="sxs-lookup"><span data-stu-id="aec20-157">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="aec20-158">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aec20-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)




