---
title: Azure Active Directory B2B collaboration API and customization | Microsoft Docs
description: Azure Active Directory B2B collaboration supports your cross-company relationships by enabling business partners to selectively access your corporate applications
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552080"
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="d115a-103">Azure Active Directory B2B collaboration API and customization</span><span class="sxs-lookup"><span data-stu-id="d115a-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="d115a-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span><span class="sxs-lookup"><span data-stu-id="d115a-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="d115a-105">With our API, you can do just that.</span><span class="sxs-lookup"><span data-stu-id="d115a-105">With our API, you can do just that.</span></span> [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="d115a-106">Capabilities of the invitation API</span><span class="sxs-lookup"><span data-stu-id="d115a-106">Capabilities of the invitation API</span></span>
<span data-ttu-id="d115a-107">The API offers the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="d115a-107">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="d115a-108">Invite an external user with *any* email address.</span><span class="sxs-lookup"><span data-stu-id="d115a-108">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="d115a-109">Customize where you want your users to land after they accept their invitation.</span><span class="sxs-lookup"><span data-stu-id="d115a-109">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="d115a-110">Choose to send the standard invitation mail through us</span><span class="sxs-lookup"><span data-stu-id="d115a-110">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="d115a-111">with a message to the recipient that you can customize</span><span class="sxs-lookup"><span data-stu-id="d115a-111">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="d115a-112">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span><span class="sxs-lookup"><span data-stu-id="d115a-112">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="d115a-113">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d115a-113">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="d115a-114">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span><span class="sxs-lookup"><span data-stu-id="d115a-114">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="d115a-115">Finally, if you are an admin, you can choose to invite the user as member.</span><span class="sxs-lookup"><span data-stu-id="d115a-115">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="d115a-116">Authorization model</span><span class="sxs-lookup"><span data-stu-id="d115a-116">Authorization model</span></span>
<span data-ttu-id="d115a-117">The API can be run in the following authorization modes:</span><span class="sxs-lookup"><span data-stu-id="d115a-117">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="d115a-118">App + User mode</span><span class="sxs-lookup"><span data-stu-id="d115a-118">App + User mode</span></span>
<span data-ttu-id="d115a-119">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span><span class="sxs-lookup"><span data-stu-id="d115a-119">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="d115a-120">App only mode</span><span class="sxs-lookup"><span data-stu-id="d115a-120">App only mode</span></span>
<span data-ttu-id="d115a-121">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span><span class="sxs-lookup"><span data-stu-id="d115a-121">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="d115a-122">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="d115a-122">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="d115a-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d115a-123">PowerShell</span></span>
<span data-ttu-id="d115a-124">It is now possible to use PowerShell to add and invite external users to an organization easily.</span><span class="sxs-lookup"><span data-stu-id="d115a-124">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="d115a-125">Create an invitation using the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d115a-125">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="d115a-126">You can use the following options:</span><span class="sxs-lookup"><span data-stu-id="d115a-126">You can use the following options:</span></span>

* <span data-ttu-id="d115a-127">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="d115a-127">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="d115a-128">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="d115a-128">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="d115a-129">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="d115a-129">-SendInvitationMessage</span></span>
* <span data-ttu-id="d115a-130">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="d115a-130">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="d115a-131">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="d115a-131">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d115a-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="d115a-132">Next steps</span></span>

<span data-ttu-id="d115a-133">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="d115a-133">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d115a-134">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="d115a-134">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d115a-135">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="d115a-135">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="d115a-136">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="d115a-136">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="d115a-137">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="d115a-137">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="d115a-138">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="d115a-138">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="d115a-139">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="d115a-139">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="d115a-140">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="d115a-140">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="d115a-141">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="d115a-141">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="d115a-142">Multi-factor authentication for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="d115a-142">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="d115a-143">Add B2B collaboration users without an invitation</span><span class="sxs-lookup"><span data-stu-id="d115a-143">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="d115a-144">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d115a-144">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
