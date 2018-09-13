---
title: Delegate invitations for Azure Active Directory B2B collaboration | Microsoft Docs
description: Azure Active Directory B2B collaboration user properties are configurable
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
ms.openlocfilehash: 11e5a442aafc9c0c95a6673f3f3010c225a06a9c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563426"
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="3e820-103">Delegate invitations for Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="3e820-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="3e820-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span><span class="sxs-lookup"><span data-stu-id="3e820-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="3e820-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span><span class="sxs-lookup"><span data-stu-id="3e820-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="3e820-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span><span class="sxs-lookup"><span data-stu-id="3e820-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="3e820-107">Guest Inviter role</span><span class="sxs-lookup"><span data-stu-id="3e820-107">Guest Inviter role</span></span>
<span data-ttu-id="3e820-108">We can assign the user to Guest Inviter role to send invitations.</span><span class="sxs-lookup"><span data-stu-id="3e820-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="3e820-109">You don't have to be member of the global admin role to send invitations.</span><span class="sxs-lookup"><span data-stu-id="3e820-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="3e820-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span><span class="sxs-lookup"><span data-stu-id="3e820-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="3e820-111">You can do this by using the Azure portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e820-111">You can do this by using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="3e820-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span><span class="sxs-lookup"><span data-stu-id="3e820-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="3e820-113">Control who can invite</span><span class="sxs-lookup"><span data-stu-id="3e820-113">Control who can invite</span></span>

![Control how to invite](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="3e820-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span><span class="sxs-lookup"><span data-stu-id="3e820-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="3e820-116">Turn off invitations</span><span class="sxs-lookup"><span data-stu-id="3e820-116">Turn off invitations</span></span>
- <span data-ttu-id="3e820-117">Only admins and users in the Guest Inviter role can invite</span><span class="sxs-lookup"><span data-stu-id="3e820-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="3e820-118">Admins, the Guest Inviter role, and members can invite</span><span class="sxs-lookup"><span data-stu-id="3e820-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="3e820-119">All users, including guests, can invite</span><span class="sxs-lookup"><span data-stu-id="3e820-119">All users, including guests, can invite</span></span>

<span data-ttu-id="3e820-120">By default, tenants are set to #4.</span><span class="sxs-lookup"><span data-stu-id="3e820-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="3e820-121">(All users, including guests, can invite B2B users.)</span><span class="sxs-lookup"><span data-stu-id="3e820-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e820-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="3e820-122">Next steps</span></span>

<span data-ttu-id="3e820-123">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="3e820-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="3e820-124">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="3e820-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="3e820-125">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="3e820-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="3e820-126">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="3e820-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="3e820-127">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="3e820-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="3e820-128">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="3e820-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="3e820-129">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="3e820-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="3e820-130">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="3e820-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="3e820-131">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="3e820-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="3e820-132">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="3e820-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="3e820-133">B2B collaboration current limitations</span><span class="sxs-lookup"><span data-stu-id="3e820-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

