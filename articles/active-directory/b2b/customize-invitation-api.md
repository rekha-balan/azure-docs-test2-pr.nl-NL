---
title: Azure Active Directory B2B collaboration API and customization | Microsoft Docs
description: Azure Active Directory B2B collaboration supports your cross-company relationships by enabling business partners to selectively access your corporate applications
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 04/11/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: a41eadaecc203f9371da3eee05367a4f77747253
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868763"
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="fd763-103">Azure Active Directory B2B collaboration API and customization</span><span class="sxs-lookup"><span data-stu-id="fd763-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="fd763-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span><span class="sxs-lookup"><span data-stu-id="fd763-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="fd763-105">With our API, you can do just that.</span><span class="sxs-lookup"><span data-stu-id="fd763-105">With our API, you can do just that.</span></span> [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="fd763-106">Capabilities of the invitation API</span><span class="sxs-lookup"><span data-stu-id="fd763-106">Capabilities of the invitation API</span></span>
<span data-ttu-id="fd763-107">The API offers the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="fd763-107">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="fd763-108">Invite an external user with *any* email address.</span><span class="sxs-lookup"><span data-stu-id="fd763-108">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="fd763-109">Customize where you want your users to land after they accept their invitation.</span><span class="sxs-lookup"><span data-stu-id="fd763-109">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="fd763-110">Choose to send the standard invitation mail through us</span><span class="sxs-lookup"><span data-stu-id="fd763-110">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="fd763-111">with a message to the recipient that you can customize</span><span class="sxs-lookup"><span data-stu-id="fd763-111">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="fd763-112">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span><span class="sxs-lookup"><span data-stu-id="fd763-112">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="fd763-113">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd763-113">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="fd763-114">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span><span class="sxs-lookup"><span data-stu-id="fd763-114">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="fd763-115">Finally, if you are an admin, you can choose to invite the user as member.</span><span class="sxs-lookup"><span data-stu-id="fd763-115">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="fd763-116">Authorization model</span><span class="sxs-lookup"><span data-stu-id="fd763-116">Authorization model</span></span>
<span data-ttu-id="fd763-117">The API can be run in the following authorization modes:</span><span class="sxs-lookup"><span data-stu-id="fd763-117">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="fd763-118">App + User mode</span><span class="sxs-lookup"><span data-stu-id="fd763-118">App + User mode</span></span>
<span data-ttu-id="fd763-119">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span><span class="sxs-lookup"><span data-stu-id="fd763-119">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="fd763-120">App only mode</span><span class="sxs-lookup"><span data-stu-id="fd763-120">App only mode</span></span>
<span data-ttu-id="fd763-121">In app only context, the app needs the User.Invite.All scope for the invitation to succeed.</span><span class="sxs-lookup"><span data-stu-id="fd763-121">In app only context, the app needs the User.Invite.All scope for the invitation to succeed.</span></span>

<span data-ttu-id="fd763-122">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="fd763-122">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="fd763-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd763-123">PowerShell</span></span>
<span data-ttu-id="fd763-124">It is now possible to use PowerShell to add and invite external users to an organization easily.</span><span class="sxs-lookup"><span data-stu-id="fd763-124">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="fd763-125">Create an invitation using the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fd763-125">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="fd763-126">You can use the following options:</span><span class="sxs-lookup"><span data-stu-id="fd763-126">You can use the following options:</span></span>

* <span data-ttu-id="fd763-127">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="fd763-127">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="fd763-128">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="fd763-128">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="fd763-129">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="fd763-129">-SendInvitationMessage</span></span>
* <span data-ttu-id="fd763-130">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="fd763-130">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="fd763-131">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="fd763-131">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd763-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd763-132">Next steps</span></span>

- [<span data-ttu-id="fd763-133">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="fd763-133">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
- [<span data-ttu-id="fd763-134">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="fd763-134">The elements of the B2B collaboration invitation email</span></span>](invitation-email-elements.md)
- [<span data-ttu-id="fd763-135">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="fd763-135">B2B collaboration invitation redemption</span></span>](redemption-experience.md)
- [<span data-ttu-id="fd763-136">Add B2B collaboration users without an invitation</span><span class="sxs-lookup"><span data-stu-id="fd763-136">Add B2B collaboration users without an invitation</span></span>](add-user-without-invite.md)

