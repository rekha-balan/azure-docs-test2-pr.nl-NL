---
title: Add B2B collaboration users to Azure Active Directory without an invitation | Microsoft Docs
description: You can let a guest user add other guest users to your Azure AD without redeeming an invitation in Azure Active Directory B2B collaboration.
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662186"
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="21483-103">Add B2B collaboration guest users without an invitation</span><span class="sxs-lookup"><span data-stu-id="21483-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="21483-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span><span class="sxs-lookup"><span data-stu-id="21483-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="21483-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span><span class="sxs-lookup"><span data-stu-id="21483-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="21483-106">Grant these privileges when:</span><span class="sxs-lookup"><span data-stu-id="21483-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="21483-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span><span class="sxs-lookup"><span data-stu-id="21483-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="21483-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span><span class="sxs-lookup"><span data-stu-id="21483-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="21483-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span><span class="sxs-lookup"><span data-stu-id="21483-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="21483-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span><span class="sxs-lookup"><span data-stu-id="21483-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="21483-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="21483-111">Next steps</span></span>

<span data-ttu-id="21483-112">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="21483-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="21483-113">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="21483-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="21483-114">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="21483-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="21483-115">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="21483-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="21483-116">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="21483-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="21483-117">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="21483-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="21483-118">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="21483-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="21483-119">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="21483-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="21483-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="21483-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="21483-121">Azure Active Directory B2B collaboration API and customization</span><span class="sxs-lookup"><span data-stu-id="21483-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="21483-122">Multi-factor authentication for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="21483-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="21483-123">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21483-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)