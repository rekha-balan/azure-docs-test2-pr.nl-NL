---
title: Limitations of Azure Active Directory B2B collaboration | Microsoft Docs
description: Current limitations for Azure Active Directory B2B collaboration
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/23/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 34713f4bf43f047bdee8d87f2e4410d13ba3492d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866250"
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="b4dd5-103">Limitations of Azure AD B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="b4dd5-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="b4dd5-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="b4dd5-105">Possible double multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="b4dd5-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="b4dd5-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="b4dd5-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](conditional-access.md).</span></span> <span data-ttu-id="b4dd5-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="b4dd5-109">Instant-on</span><span class="sxs-lookup"><span data-stu-id="b4dd5-109">Instant-on</span></span>
<span data-ttu-id="b4dd5-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="b4dd5-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="b4dd5-112">Replication is completed once all instances are updated.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="b4dd5-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="b4dd5-114">If that happens, refresh or retry to help.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="b4dd5-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="azure-ad-directories"></a><span data-ttu-id="b4dd5-116">Azure AD directories</span><span class="sxs-lookup"><span data-stu-id="b4dd5-116">Azure AD directories</span></span>
<span data-ttu-id="b4dd5-117">Azure AD B2B is subject to Azure AD service directory limits.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-117">Azure AD B2B is subject to Azure AD service directory limits.</span></span> <span data-ttu-id="b4dd5-118">For details about the number of directories a user can create and the number of directories to which a user or guest user can belong, see [Azure AD service limits and restrictions](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-service-limits-restrictions).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-118">For details about the number of directories a user can create and the number of directories to which a user or guest user can belong, see [Azure AD service limits and restrictions](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-service-limits-restrictions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4dd5-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4dd5-119">Next steps</span></span>

<span data-ttu-id="b4dd5-120">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-120">See the following articles on Azure AD B2B collaboration:</span></span>

- [<span data-ttu-id="b4dd5-121">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="b4dd5-121">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
- [<span data-ttu-id="b4dd5-122">Delegate B2B collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="b4dd5-122">Delegate B2B collaboration invitations</span></span>](delegate-invitations.md)

