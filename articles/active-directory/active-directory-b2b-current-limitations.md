---
title: Limitations of Azure Active Directory B2B collaboration | Microsoft Docs
description: Current limitations for Azure Active Directory B2B collaboration preview
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
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: cdc951d4e16e7f0df425dba7c33d86255276f526
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551094"
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="6023d-103">Limitations of Azure AD B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="6023d-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="6023d-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span><span class="sxs-lookup"><span data-stu-id="6023d-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="6023d-105">Possible double multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="6023d-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="6023d-106">With Azure AD B2B you can enforce multi-factor authentication at the resource organization (the inviting organization).</span><span class="sxs-lookup"><span data-stu-id="6023d-106">With Azure AD B2B you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="6023d-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="6023d-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="6023d-108">This means that if a partner already has multi-factor authentication set up and enforces it, the partner's users might have to perform the authentication once in their home organization and then again in yours.</span><span class="sxs-lookup"><span data-stu-id="6023d-108">This means that if a partner already has multi-factor authentication set up and enforces it, the partner's users might have to perform the authentication once in their home organization and then again in yours.</span></span>

<span data-ttu-id="6023d-109">In a future release, we plan to introduce a policy where you can avoid the double authentication issue by choosing to trust the partner's multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="6023d-109">In a future release, we plan to introduce a policy where you can avoid the double authentication issue by choosing to trust the partner's multi-factor authentication.</span></span>


## <a name="instant-on"></a><span data-ttu-id="6023d-110">Instant-on</span><span class="sxs-lookup"><span data-stu-id="6023d-110">Instant-on</span></span>
<span data-ttu-id="6023d-111">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span><span class="sxs-lookup"><span data-stu-id="6023d-111">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="6023d-112">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span><span class="sxs-lookup"><span data-stu-id="6023d-112">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="6023d-113">It can take a non-zero amount of time it can take to complete replication.</span><span class="sxs-lookup"><span data-stu-id="6023d-113">It can take a non-zero amount of time it can take to complete replication.</span></span> <span data-ttu-id="6023d-114">Sometimes when the object is written or updated in one instance of the directory and the call to retrieve this object is load balanced to another instance, this has causied authorization issues.</span><span class="sxs-lookup"><span data-stu-id="6023d-114">Sometimes when the object is written or updated in one instance of the directory and the call to retrieve this object is load balanced to another instance, this has causied authorization issues.</span></span> <span data-ttu-id="6023d-115">We have done a lot of work to eliminate or reduce these replication latencies, but it is possible that in some rare cases, they may still occur.</span><span class="sxs-lookup"><span data-stu-id="6023d-115">We have done a lot of work to eliminate or reduce these replication latencies, but it is possible that in some rare cases, they may still occur.</span></span> <span data-ttu-id="6023d-116">If that happens, refresh or retry to help.</span><span class="sxs-lookup"><span data-stu-id="6023d-116">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="6023d-117">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span><span class="sxs-lookup"><span data-stu-id="6023d-117">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6023d-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="6023d-118">Next steps</span></span>

<span data-ttu-id="6023d-119">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="6023d-119">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6023d-120">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="6023d-120">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6023d-121">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="6023d-121">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="6023d-122">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="6023d-122">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="6023d-123">Delegate B2bB collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="6023d-123">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="6023d-124">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="6023d-124">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="6023d-125">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="6023d-125">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="6023d-126">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="6023d-126">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="6023d-127">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="6023d-127">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="6023d-128">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="6023d-128">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="6023d-129">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="6023d-129">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
