---
title: View who has Azure resource roles in PIM | Microsoft Docs
description: View who has Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 03/30/2018
ms.author: rolyon
ms.openlocfilehash: aee172bc6fc77aaac8d2d52037a481fdb976d308
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858069"
---
# <a name="view-who-has-azure-resource-roles-in-pim"></a><span data-ttu-id="290e1-103">View who has Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="290e1-103">View who has Azure resource roles in PIM</span></span>

<span data-ttu-id="290e1-104">With Azure Active Directory Privileged Identity Management (PIM), you can manage, control, and monitor access to Azure resources within your organization.</span><span class="sxs-lookup"><span data-stu-id="290e1-104">With Azure Active Directory Privileged Identity Management (PIM), you can manage, control, and monitor access to Azure resources within your organization.</span></span> <span data-ttu-id="290e1-105">This includes subscriptions, resource groups, and even virtual machines.</span><span class="sxs-lookup"><span data-stu-id="290e1-105">This includes subscriptions, resource groups, and even virtual machines.</span></span> <span data-ttu-id="290e1-106">Any resource within the Azure portal that leverages the Azure role-based access control (RBAC) functionality can take advantage of the security and lifecycle management capabilities in Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="290e1-106">Any resource within the Azure portal that leverages the Azure role-based access control (RBAC) functionality can take advantage of the security and lifecycle management capabilities in Azure AD PIM.</span></span> 

## <a name="pim-for-azure-resources-helps-resource-administrators"></a><span data-ttu-id="290e1-107">PIM for Azure resources helps resource administrators</span><span class="sxs-lookup"><span data-stu-id="290e1-107">PIM for Azure resources helps resource administrators</span></span>

- <span data-ttu-id="290e1-108">See which users and groups are assigned roles for the Azure resources you administer</span><span class="sxs-lookup"><span data-stu-id="290e1-108">See which users and groups are assigned roles for the Azure resources you administer</span></span>
- <span data-ttu-id="290e1-109">Enable on-demand, "just in time" access to manage resources such as Subscriptions, Resource Groups, and more</span><span class="sxs-lookup"><span data-stu-id="290e1-109">Enable on-demand, "just in time" access to manage resources such as Subscriptions, Resource Groups, and more</span></span>
- <span data-ttu-id="290e1-110">Expire assigned users/groups resource access automatically with new time-bound assignment settings</span><span class="sxs-lookup"><span data-stu-id="290e1-110">Expire assigned users/groups resource access automatically with new time-bound assignment settings</span></span>
- <span data-ttu-id="290e1-111">Assign temporary resource access for quick tasks or on-call schedules</span><span class="sxs-lookup"><span data-stu-id="290e1-111">Assign temporary resource access for quick tasks or on-call schedules</span></span>
- <span data-ttu-id="290e1-112">Enforce Multi-Factor Authentication for resource access on any built-in or custom role</span><span class="sxs-lookup"><span data-stu-id="290e1-112">Enforce Multi-Factor Authentication for resource access on any built-in or custom role</span></span> 
- <span data-ttu-id="290e1-113">Get reports about resource access correlated resource activity during a user’s active session</span><span class="sxs-lookup"><span data-stu-id="290e1-113">Get reports about resource access correlated resource activity during a user’s active session</span></span>
- <span data-ttu-id="290e1-114">Get alerts when new users or groups are assigned resource access, and when they activate eligible assignments</span><span class="sxs-lookup"><span data-stu-id="290e1-114">Get alerts when new users or groups are assigned resource access, and when they activate eligible assignments</span></span>

## <a name="view-activation-and-azure-resource-activity"></a><span data-ttu-id="290e1-115">View activation and Azure resource activity</span><span class="sxs-lookup"><span data-stu-id="290e1-115">View activation and Azure resource activity</span></span>

<span data-ttu-id="290e1-116">In the event you need to see what actions a specific user took on various resources, you can review the Azure Resource activity associated with a given activation period (for eligible users).</span><span class="sxs-lookup"><span data-stu-id="290e1-116">In the event you need to see what actions a specific user took on various resources, you can review the Azure Resource activity associated with a given activation period (for eligible users).</span></span> <span data-ttu-id="290e1-117">Start by selecting a user from the Members view or from the list of members in a specific role.</span><span class="sxs-lookup"><span data-stu-id="290e1-117">Start by selecting a user from the Members view or from the list of members in a specific role.</span></span> <span data-ttu-id="290e1-118">The result displays a graphical view of the user’s actions on Azure Resources by date, and the recent role activations over that same time period.</span><span class="sxs-lookup"><span data-stu-id="290e1-118">The result displays a graphical view of the user’s actions on Azure Resources by date, and the recent role activations over that same time period.</span></span>

![](media/azure-pim-resource-rbac/user-details.png)

<span data-ttu-id="290e1-119">Selecting a specific role activation will show the role activation details, and corresponding Azure Resource activity that occurred while that user was active.</span><span class="sxs-lookup"><span data-stu-id="290e1-119">Selecting a specific role activation will show the role activation details, and corresponding Azure Resource activity that occurred while that user was active.</span></span>

![](media/azure-pim-resource-rbac/audits.png)

## <a name="review-who-has-access-in-a-subscription"></a><span data-ttu-id="290e1-120">Review who has access in a subscription</span><span class="sxs-lookup"><span data-stu-id="290e1-120">Review who has access in a subscription</span></span>

<span data-ttu-id="290e1-121">To review role assignments in your Subscription, select the Members tab from the left navigation, or select roles, and choose a specific role to review members.</span><span class="sxs-lookup"><span data-stu-id="290e1-121">To review role assignments in your Subscription, select the Members tab from the left navigation, or select roles, and choose a specific role to review members.</span></span> 

<span data-ttu-id="290e1-122">Select Review from the action bar to view existing access reviews and select Add to create a new review.</span><span class="sxs-lookup"><span data-stu-id="290e1-122">Select Review from the action bar to view existing access reviews and select Add to create a new review.</span></span>

![](media/azure-pim-resource-rbac/owner.png)

[<span data-ttu-id="290e1-123">Learn more about access reviews</span><span class="sxs-lookup"><span data-stu-id="290e1-123">Learn more about access reviews</span></span>](pim-how-to-perform-security-review.md)

>[!NOTE]
<span data-ttu-id="290e1-124">Reviews are only supported for Subscription resource types at this time.</span><span class="sxs-lookup"><span data-stu-id="290e1-124">Reviews are only supported for Subscription resource types at this time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="290e1-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="290e1-125">Next steps</span></span>

- [<span data-ttu-id="290e1-126">Assign Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="290e1-126">Assign Azure resource roles in PIM</span></span>](pim-resource-roles-assign-roles.md)
- [<span data-ttu-id="290e1-127">Approve or deny requests for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="290e1-127">Approve or deny requests for Azure resource roles in PIM</span></span>](pim-resource-roles-approval-workflow.md)
- [<span data-ttu-id="290e1-128">Built-in roles in Azure</span><span class="sxs-lookup"><span data-stu-id="290e1-128">Built-in roles in Azure</span></span>](../../role-based-access-control/built-in-roles.md)
