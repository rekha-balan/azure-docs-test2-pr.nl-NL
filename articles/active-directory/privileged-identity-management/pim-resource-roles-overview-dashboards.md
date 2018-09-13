---
title: Use a resource dashboard to perform an access review - Azure | Microsoft Docs
description: Describes how to use a resource dashboard to perform an access review in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 03/30/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 20172cf7413397aedc4b3c32d0f1419531a2588a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868209"
---
# <a name="use-a-resource-dashboard-to-perform-an-access-review"></a><span data-ttu-id="2e42d-103">Use a resource dashboard to perform an access review</span><span class="sxs-lookup"><span data-stu-id="2e42d-103">Use a resource dashboard to perform an access review</span></span>

<span data-ttu-id="2e42d-104">You can use a resource dashboard to perform an access review in Privileged Identity Management (PIM) for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2e42d-104">You can use a resource dashboard to perform an access review in Privileged Identity Management (PIM) for Azure resources.</span></span> <span data-ttu-id="2e42d-105">The Admin View dashboard has three primary components:</span><span class="sxs-lookup"><span data-stu-id="2e42d-105">The Admin View dashboard has three primary components:</span></span>

- <span data-ttu-id="2e42d-106">A graphical representation of resource role activations.</span><span class="sxs-lookup"><span data-stu-id="2e42d-106">A graphical representation of resource role activations.</span></span>
- <span data-ttu-id="2e42d-107">Two charts that display the distribution of role assignments by assignment type.</span><span class="sxs-lookup"><span data-stu-id="2e42d-107">Two charts that display the distribution of role assignments by assignment type.</span></span>
- <span data-ttu-id="2e42d-108">A data area pertaining to new role assignments.</span><span class="sxs-lookup"><span data-stu-id="2e42d-108">A data area pertaining to new role assignments.</span></span>

![Screenshot of the Admin View dashboard, showing graphs and charts](media/azure-pim-resource-rbac/rbac-overview-top.png)

![Screenshot of the Admin View dashboard, showing data lists](media/azure-pim-resource-rbac/role-settings.png)

<span data-ttu-id="2e42d-111">The graphical representation of resource role activations covers the past seven days.</span><span class="sxs-lookup"><span data-stu-id="2e42d-111">The graphical representation of resource role activations covers the past seven days.</span></span> <span data-ttu-id="2e42d-112">This data is scoped to the selected resource, and displays activations for the most common roles (owner, contributor, user access administrator), and for all roles combined.</span><span class="sxs-lookup"><span data-stu-id="2e42d-112">This data is scoped to the selected resource, and displays activations for the most common roles (owner, contributor, user access administrator), and for all roles combined.</span></span>

<span data-ttu-id="2e42d-113">To the right of the activations graph, two charts display the distribution of role assignments by assignment type, for both users and groups.</span><span class="sxs-lookup"><span data-stu-id="2e42d-113">To the right of the activations graph, two charts display the distribution of role assignments by assignment type, for both users and groups.</span></span> <span data-ttu-id="2e42d-114">You can change the value to a percentage (or vice versa), by selecting a slice of the chart.</span><span class="sxs-lookup"><span data-stu-id="2e42d-114">You can change the value to a percentage (or vice versa), by selecting a slice of the chart.</span></span>

<span data-ttu-id="2e42d-115">Below the charts, you see the number of users and groups with new role assignments over the last 30 days, and a list of roles sorted by total assignments (in descending order).</span><span class="sxs-lookup"><span data-stu-id="2e42d-115">Below the charts, you see the number of users and groups with new role assignments over the last 30 days, and a list of roles sorted by total assignments (in descending order).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e42d-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="2e42d-116">Next steps</span></span>

- [<span data-ttu-id="2e42d-117">Start an access review for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="2e42d-117">Start an access review for Azure resource roles in PIM</span></span>](pim-resource-roles-start-access-review.md) 
