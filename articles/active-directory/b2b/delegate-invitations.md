---
title: Delegate invitations for Azure Active Directory B2B collaboration | Microsoft Docs
description: Azure Active Directory B2B collaboration user properties are configurable
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/23/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 40f6d3cdd3ab8926e48463beaae15b2580458cc1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857858"
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="a43f9-103">Delegate invitations for Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="a43f9-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="a43f9-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span><span class="sxs-lookup"><span data-stu-id="a43f9-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="a43f9-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span><span class="sxs-lookup"><span data-stu-id="a43f9-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="a43f9-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span><span class="sxs-lookup"><span data-stu-id="a43f9-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="a43f9-107">Guest Inviter role</span><span class="sxs-lookup"><span data-stu-id="a43f9-107">Guest Inviter role</span></span>
<span data-ttu-id="a43f9-108">We can assign the user to Guest Inviter role to send invitations.</span><span class="sxs-lookup"><span data-stu-id="a43f9-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="a43f9-109">You don't have to be member of the global admin role to send invitations.</span><span class="sxs-lookup"><span data-stu-id="a43f9-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="a43f9-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span><span class="sxs-lookup"><span data-stu-id="a43f9-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="a43f9-111">A user can also invoke the API using the Azure portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a43f9-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="a43f9-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span><span class="sxs-lookup"><span data-stu-id="a43f9-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="a43f9-113">Control who can invite</span><span class="sxs-lookup"><span data-stu-id="a43f9-113">Control who can invite</span></span>

![Control how to invite](media/delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="a43f9-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span><span class="sxs-lookup"><span data-stu-id="a43f9-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="a43f9-116">Turn off invitations</span><span class="sxs-lookup"><span data-stu-id="a43f9-116">Turn off invitations</span></span>
- <span data-ttu-id="a43f9-117">Only admins and users in the Guest Inviter role can invite</span><span class="sxs-lookup"><span data-stu-id="a43f9-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="a43f9-118">Admins, the Guest Inviter role, and members can invite</span><span class="sxs-lookup"><span data-stu-id="a43f9-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="a43f9-119">All users, including guests, can invite</span><span class="sxs-lookup"><span data-stu-id="a43f9-119">All users, including guests, can invite</span></span>

<span data-ttu-id="a43f9-120">By default, tenants are set to #4.</span><span class="sxs-lookup"><span data-stu-id="a43f9-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="a43f9-121">(All users, including guests, can invite B2B users.)</span><span class="sxs-lookup"><span data-stu-id="a43f9-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a43f9-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a43f9-122">Next steps</span></span>

<span data-ttu-id="a43f9-123">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="a43f9-123">See the following articles on Azure AD B2B collaboration:</span></span>

- [<span data-ttu-id="a43f9-124">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="a43f9-124">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
- [<span data-ttu-id="a43f9-125">Add B2B collaboration guest users without an invitation</span><span class="sxs-lookup"><span data-stu-id="a43f9-125">Add B2B collaboration guest users without an invitation</span></span>](add-user-without-invite.md)
- [<span data-ttu-id="a43f9-126">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="a43f9-126">Adding a B2B collaboration user to a role</span></span>](add-guest-to-role.md)


