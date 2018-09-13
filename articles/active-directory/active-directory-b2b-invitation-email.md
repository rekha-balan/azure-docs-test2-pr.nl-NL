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
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a>The elements of the B2B collaboration invitation email

Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD. The primary goal for this is to increase trust in the recipient and add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation. This is a key component to reducing sharing friction. And of course, we also want the email to look great!

![Azure AD B2b invitation email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a>Explaining the email
Let's look at a few elements of the email so you know how best to make use of these capabilities.

### <a name="subject"></a>Subject
The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization

### <a name="from-address"></a>From address
We use a LinkedIn-like pattern for the From address. Our goal here is to be clear who the inviter is and from which company and also clarify that the email is coming from a Microsoft email address. The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Reply To
The reply to email is set to the inviter's email when available, so that replying to the email will send an email back to the inviter.

### <a name="branding"></a>Branding
The invitation emails from your tenant use the company branding that you may have set up for your tenant. If you want to take advantage of this, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it. The banner logo will show up in the email. Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results. In addition, the company name also shows up in the call to action.

### <a name="call-to-action"></a>Call to action
The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.
- The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization

- And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button. When the recipient has been added without the need for invitations, this button doesn't show up.

### <a name="inviters-information"></a>Inviter's information
The inviter's display name will be included in the email. And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well. Both of these are intended to increase your recipient's confidence in the email.

If the inviter hasn't yet set up their profile picture, Azure AD creates an icon with the inviter's initials in place of the picture as shown:

  ![displaying the inviter's initials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Body
This will contain the message that the inviter composes or is passed through the invitation API. This is just a text area, which will not process HTML tags for security reasons.

### <a name="footer-section"></a>Footer section
The footer contains the Microsoft company brand and will let the recipient know if the email was sent from an unmonitored alias. Special cases:

- The inviter doesn't have an email address in the inviting tenancy

  ![picture of inviter doesn't have an email address in the inviting tenancy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/inviter-no-email.png)


- The recipient doesn't need to redeem the invitation

  ![when recipient doesn't need to redeem invitation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Next steps

Browse our other articles on Azure AD B2B collaboration:

* [What is Azure AD B2B collaboration](active-directory-b2b-what-is-azure-ad-b2b.md)
* [How do Azure Active Directory admins add B2B collaboration users?](active-directory-b2b-admin-add-users.md)
* [How do information workers add B2B collaboration users?](active-directory-b2b-iw-add-users.md)
* [B2B collaboration invitation redemption](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B collaboration licensing](active-directory-b2b-licensing.md)
* [Troubleshooting Azure Active Directory B2B collaboration](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B collaboration frequently-asked questions (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B collaboration API and customization](active-directory-b2b-api.md)
* [Multi-factor authentication for B2B collaboration users](active-directory-b2b-mfa-instructions.md)
* [Add B2B collaboration users without an invitation](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)




