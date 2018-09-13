---
title: Configure security alerts for Azure resource roles in PIM | Microsoft Docs
description: Learn how to configure security alerts for Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 2fa63cf2fa05f2cde4558f0bea38bfd7f17df3ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968794"
---
# <a name="configure-security-alerts-for-azure-resource-roles-in-pim"></a><span data-ttu-id="c16bf-103">Configure security alerts for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="c16bf-103">Configure security alerts for Azure resource roles in PIM</span></span>
<span data-ttu-id="c16bf-104">Privileged Identity Management (PIM) for Azure Resources generates alerts when there is suspicious or unsafe activity in your environment.</span><span class="sxs-lookup"><span data-stu-id="c16bf-104">Privileged Identity Management (PIM) for Azure Resources generates alerts when there is suspicious or unsafe activity in your environment.</span></span> <span data-ttu-id="c16bf-105">When an alert is triggered, it shows up on the Alerts page.</span><span class="sxs-lookup"><span data-stu-id="c16bf-105">When an alert is triggered, it shows up on the Alerts page.</span></span> 

![Alerts page](media/azure-pim-resource-rbac/RBAC-alerts-home.png)

## <a name="review-alerts"></a><span data-ttu-id="c16bf-107">Review alerts</span><span class="sxs-lookup"><span data-stu-id="c16bf-107">Review alerts</span></span>
<span data-ttu-id="c16bf-108">Select an alert to see a report that lists the users or roles that triggered the alert, along with remediation advice.</span><span class="sxs-lookup"><span data-stu-id="c16bf-108">Select an alert to see a report that lists the users or roles that triggered the alert, along with remediation advice.</span></span>

![Alert report](media/azure-pim-resource-rbac/rbac-alert-info.png)

## <a name="alerts"></a><span data-ttu-id="c16bf-110">Alerts</span><span class="sxs-lookup"><span data-stu-id="c16bf-110">Alerts</span></span>
| <span data-ttu-id="c16bf-111">Alert</span><span class="sxs-lookup"><span data-stu-id="c16bf-111">Alert</span></span> | <span data-ttu-id="c16bf-112">Severity</span><span class="sxs-lookup"><span data-stu-id="c16bf-112">Severity</span></span> | <span data-ttu-id="c16bf-113">Trigger</span><span class="sxs-lookup"><span data-stu-id="c16bf-113">Trigger</span></span> | <span data-ttu-id="c16bf-114">Recommendation</span><span class="sxs-lookup"><span data-stu-id="c16bf-114">Recommendation</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c16bf-115">**Too many owners assigned to a resource**</span><span class="sxs-lookup"><span data-stu-id="c16bf-115">**Too many owners assigned to a resource**</span></span> |<span data-ttu-id="c16bf-116">Medium</span><span class="sxs-lookup"><span data-stu-id="c16bf-116">Medium</span></span> |<span data-ttu-id="c16bf-117">Too many users have the owner role.</span><span class="sxs-lookup"><span data-stu-id="c16bf-117">Too many users have the owner role.</span></span> |<span data-ttu-id="c16bf-118">Review the users in the list and reassign some to less privileged roles.</span><span class="sxs-lookup"><span data-stu-id="c16bf-118">Review the users in the list and reassign some to less privileged roles.</span></span> |
| <span data-ttu-id="c16bf-119">**Too many permanent owners assigned to a resource**</span><span class="sxs-lookup"><span data-stu-id="c16bf-119">**Too many permanent owners assigned to a resource**</span></span> |<span data-ttu-id="c16bf-120">Medium</span><span class="sxs-lookup"><span data-stu-id="c16bf-120">Medium</span></span> |<span data-ttu-id="c16bf-121">Too many users are permanently assigned to a role.</span><span class="sxs-lookup"><span data-stu-id="c16bf-121">Too many users are permanently assigned to a role.</span></span> |<span data-ttu-id="c16bf-122">Review the users in the list and re-assign some to require activation for role use.</span><span class="sxs-lookup"><span data-stu-id="c16bf-122">Review the users in the list and re-assign some to require activation for role use.</span></span> |
| <span data-ttu-id="c16bf-123">**Duplicate role created**</span><span class="sxs-lookup"><span data-stu-id="c16bf-123">**Duplicate role created**</span></span> |<span data-ttu-id="c16bf-124">Medium</span><span class="sxs-lookup"><span data-stu-id="c16bf-124">Medium</span></span> |<span data-ttu-id="c16bf-125">Multiple roles have the same criteria.</span><span class="sxs-lookup"><span data-stu-id="c16bf-125">Multiple roles have the same criteria.</span></span> |<span data-ttu-id="c16bf-126">Use only one of these roles.</span><span class="sxs-lookup"><span data-stu-id="c16bf-126">Use only one of these roles.</span></span> |


### <a name="severity"></a><span data-ttu-id="c16bf-127">Severity</span><span class="sxs-lookup"><span data-stu-id="c16bf-127">Severity</span></span>
* <span data-ttu-id="c16bf-128">**High**: Requires immediate action because of a policy violation.</span><span class="sxs-lookup"><span data-stu-id="c16bf-128">**High**: Requires immediate action because of a policy violation.</span></span> 
* <span data-ttu-id="c16bf-129">**Medium**: Does not require immediate action but signals a potential policy violation.</span><span class="sxs-lookup"><span data-stu-id="c16bf-129">**Medium**: Does not require immediate action but signals a potential policy violation.</span></span>
* <span data-ttu-id="c16bf-130">**Low**: Does not require immediate action but suggests a preferred policy change.</span><span class="sxs-lookup"><span data-stu-id="c16bf-130">**Low**: Does not require immediate action but suggests a preferred policy change.</span></span>

## <a name="configure-security-alert-settings"></a><span data-ttu-id="c16bf-131">Configure security alert settings</span><span class="sxs-lookup"><span data-stu-id="c16bf-131">Configure security alert settings</span></span>
<span data-ttu-id="c16bf-132">From the Alerts page, go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c16bf-132">From the Alerts page, go to **Settings**.</span></span>
<span data-ttu-id="c16bf-133">![Settings](media/azure-pim-resource-rbac/rbac-navigate-settings.png)</span><span class="sxs-lookup"><span data-stu-id="c16bf-133">![Settings](media/azure-pim-resource-rbac/rbac-navigate-settings.png)</span></span>

<span data-ttu-id="c16bf-134">Customize settings on the different alerts to work with your environment and security goals.</span><span class="sxs-lookup"><span data-stu-id="c16bf-134">Customize settings on the different alerts to work with your environment and security goals.</span></span>
<span data-ttu-id="c16bf-135">![Customize settings](media/azure-pim-resource-rbac/rbac-alert-settings.png)</span><span class="sxs-lookup"><span data-stu-id="c16bf-135">![Customize settings](media/azure-pim-resource-rbac/rbac-alert-settings.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c16bf-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c16bf-136">Next steps</span></span>

- [<span data-ttu-id="c16bf-137">Configure security alerts for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="c16bf-137">Configure security alerts for Azure resource roles in PIM</span></span>](pim-resource-roles-configure-alerts.md)
