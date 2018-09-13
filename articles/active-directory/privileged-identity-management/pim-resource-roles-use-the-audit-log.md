---
title: View audit history for Azure resource roles in PIM | Microsoft Docs
description: Learn how to view audit history for Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: c0536423e9640f78149b612ec66b0a07cdcf24bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871460"
---
# <a name="view-audit-history-for-azure-resource-roles-in-pim"></a><span data-ttu-id="2239d-103">View audit history for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="2239d-103">View audit history for Azure resource roles in PIM</span></span>

<span data-ttu-id="2239d-104">Resource audit gives you a view of all role activity for the resource.</span><span class="sxs-lookup"><span data-stu-id="2239d-104">Resource audit gives you a view of all role activity for the resource.</span></span> <span data-ttu-id="2239d-105">You can filter the information using a predefined date or custom range.</span><span class="sxs-lookup"><span data-stu-id="2239d-105">You can filter the information using a predefined date or custom range.</span></span>
<span data-ttu-id="2239d-106">![Filter information](media/azure-pim-resource-rbac/rbac-resource-audit.png)</span><span class="sxs-lookup"><span data-stu-id="2239d-106">![Filter information](media/azure-pim-resource-rbac/rbac-resource-audit.png)</span></span>

<span data-ttu-id="2239d-107">Resource audit also provides quick access to a user’s activity detail.</span><span class="sxs-lookup"><span data-stu-id="2239d-107">Resource audit also provides quick access to a user’s activity detail.</span></span> <span data-ttu-id="2239d-108">Under **Audit type**, select **Activate**.</span><span class="sxs-lookup"><span data-stu-id="2239d-108">Under **Audit type**, select **Activate**.</span></span> <span data-ttu-id="2239d-109">Select **(activity)** to see that user’s actions in Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2239d-109">Select **(activity)** to see that user’s actions in Azure resources.</span></span>
<span data-ttu-id="2239d-110">![Activity detail](media/azure-pim-resource-rbac/rbac-audit-activity.png)</span><span class="sxs-lookup"><span data-stu-id="2239d-110">![Activity detail](media/azure-pim-resource-rbac/rbac-audit-activity.png)</span></span>

![More activity detail](media/azure-pim-resource-rbac/rbac-audit-activity-details.png)

## <a name="my-audit"></a><span data-ttu-id="2239d-112">My audit</span><span class="sxs-lookup"><span data-stu-id="2239d-112">My audit</span></span>

<span data-ttu-id="2239d-113">My audit gives you a view of a user's personal role activity.</span><span class="sxs-lookup"><span data-stu-id="2239d-113">My audit gives you a view of a user's personal role activity.</span></span> <span data-ttu-id="2239d-114">You can filter the information using a predefined date or custom range.</span><span class="sxs-lookup"><span data-stu-id="2239d-114">You can filter the information using a predefined date or custom range.</span></span>
<span data-ttu-id="2239d-115">![Personal role activity](media/azure-pim-resource-rbac/my-audit-time.png)</span><span class="sxs-lookup"><span data-stu-id="2239d-115">![Personal role activity](media/azure-pim-resource-rbac/my-audit-time.png)</span></span>

## <a name="view-activation-and-azure-resource-activity"></a><span data-ttu-id="2239d-116">View activation and Azure resource activity</span><span class="sxs-lookup"><span data-stu-id="2239d-116">View activation and Azure resource activity</span></span>

<span data-ttu-id="2239d-117">To see what actions a specific user took in various resources, you can review the Azure resource activity that's associated with a given activation period.</span><span class="sxs-lookup"><span data-stu-id="2239d-117">To see what actions a specific user took in various resources, you can review the Azure resource activity that's associated with a given activation period.</span></span> <span data-ttu-id="2239d-118">Start by selecting a user from the **Members** view or from the list of members in a specific role.</span><span class="sxs-lookup"><span data-stu-id="2239d-118">Start by selecting a user from the **Members** view or from the list of members in a specific role.</span></span> <span data-ttu-id="2239d-119">The result displays a graphical view of the user’s actions in Azure resources by date.</span><span class="sxs-lookup"><span data-stu-id="2239d-119">The result displays a graphical view of the user’s actions in Azure resources by date.</span></span> <span data-ttu-id="2239d-120">It also shows the recent role activations over that same time period.</span><span class="sxs-lookup"><span data-stu-id="2239d-120">It also shows the recent role activations over that same time period.</span></span>

![User details](media/azure-pim-resource-rbac/rbac-user-details.png)

<span data-ttu-id="2239d-122">Selecting a specific role activation shows the role activation details and corresponding Azure resource activity that occurred while that user was active.</span><span class="sxs-lookup"><span data-stu-id="2239d-122">Selecting a specific role activation shows the role activation details and corresponding Azure resource activity that occurred while that user was active.</span></span>

![Select role activation](media/azure-pim-resource-rbac/rbac-user-resource-activity.png)

## <a name="next-steps"></a><span data-ttu-id="2239d-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2239d-124">Next steps</span></span>

- [<span data-ttu-id="2239d-125">View audit history for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="2239d-125">View audit history for Azure AD directory roles in PIM</span></span>](pim-how-to-use-audit-log.md)
