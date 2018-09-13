---
title: How to use the audit log in Azure AD Privileged Identity Management | Microsoft Docs
description: Learn how to use the audit log in the Azure Privileged Identity Management extension.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: d523f8c65ac6f959c39f58b58cdf4eb8e44ea891
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556390"
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="fcd9d-103">Using the audit log in PIM</span><span class="sxs-lookup"><span data-stu-id="fcd9d-103">Using the audit log in PIM</span></span>
<span data-ttu-id="fcd9d-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="fcd9d-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="fcd9d-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="fcd9d-106">Navigate to the audit log</span><span class="sxs-lookup"><span data-stu-id="fcd9d-106">Navigate to the audit log</span></span>
<span data-ttu-id="fcd9d-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="fcd9d-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="fcd9d-109">The audit log graph</span><span class="sxs-lookup"><span data-stu-id="fcd9d-109">The audit log graph</span></span>
<span data-ttu-id="fcd9d-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="fcd9d-111">You can also filter the data by role if there is more than one role in the audit history.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="fcd9d-112">Use the **time**, **action**, and **role** buttons to sort the log.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="fcd9d-113">The audit log list</span><span class="sxs-lookup"><span data-stu-id="fcd9d-113">The audit log list</span></span>
<span data-ttu-id="fcd9d-114">The columns in the audit log list are:</span><span class="sxs-lookup"><span data-stu-id="fcd9d-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="fcd9d-115">**Requestor** - the user who requested the role activation or change.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="fcd9d-116">If the value is "Azure System", check the Azure audit log for more information.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="fcd9d-117">**User** - the user who is activating or assigned to a role.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="fcd9d-118">**Role** - the role assigned or activated by the user.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="fcd9d-119">**Action** - the actions taken by the requestor.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="fcd9d-120">This can include assignment, unassignment, activation, or deactivation.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="fcd9d-121">**Time** - when the action occurred.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="fcd9d-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="fcd9d-123">**Expiration** - only relevant for activation of roles.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="fcd9d-124">Filter the audit log</span><span class="sxs-lookup"><span data-stu-id="fcd9d-124">Filter the audit log</span></span>
<span data-ttu-id="fcd9d-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="fcd9d-126">The **Update chart parameters blade** will appear.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="fcd9d-127">After you set the filters, click **Update** to filter the data in the log.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="fcd9d-128">If the data doesn't appear right away, refresh the page.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="fcd9d-129">Change the date range</span><span class="sxs-lookup"><span data-stu-id="fcd9d-129">Change the date range</span></span>
<span data-ttu-id="fcd9d-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="fcd9d-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="fcd9d-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="fcd9d-133">Change the roles included in the log</span><span class="sxs-lookup"><span data-stu-id="fcd9d-133">Change the roles included in the log</span></span>
<span data-ttu-id="fcd9d-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span><span class="sxs-lookup"><span data-stu-id="fcd9d-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="fcd9d-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="fcd9d-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

