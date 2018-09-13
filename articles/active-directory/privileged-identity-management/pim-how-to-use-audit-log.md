---
title: View audit history for Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to view the audit history for Azure AD directory roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 02/14/2017
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: ab5a072d845bfdbaafabe1e0e7bdce2dfce6184d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864766"
---
# <a name="view-audit-history-for-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="4b30c-103">View audit history for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="4b30c-103">View audit history for Azure AD directory roles in PIM</span></span>
<span data-ttu-id="4b30c-104">You can use the Privileged Identity Management (PIM) audit history to see all the user assignments and activations within a given time period for all privileged roles.</span><span class="sxs-lookup"><span data-stu-id="4b30c-104">You can use the Privileged Identity Management (PIM) audit history to see all the user assignments and activations within a given time period for all privileged roles.</span></span> <span data-ttu-id="4b30c-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](../reports-monitoring/overview-reports.md)</span><span class="sxs-lookup"><span data-stu-id="4b30c-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](../reports-monitoring/overview-reports.md)</span></span>

## <a name="navigate-to-audit-history"></a><span data-ttu-id="4b30c-106">Navigate to audit history</span><span class="sxs-lookup"><span data-stu-id="4b30c-106">Navigate to audit history</span></span>
<span data-ttu-id="4b30c-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span><span class="sxs-lookup"><span data-stu-id="4b30c-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="4b30c-108">From there, access the audit history by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span><span class="sxs-lookup"><span data-stu-id="4b30c-108">From there, access the audit history by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="4b30c-109">You can sort the data by Action, and look for “Activation Approved”</span><span class="sxs-lookup"><span data-stu-id="4b30c-109">You can sort the data by Action, and look for “Activation Approved”</span></span>


## <a name="audit-history-graph"></a><span data-ttu-id="4b30c-110">Audit history graph</span><span class="sxs-lookup"><span data-stu-id="4b30c-110">Audit history graph</span></span>
<span data-ttu-id="4b30c-111">You can use the audit history to view the total activations, max activations per day, and average activations per day in a line graph.</span><span class="sxs-lookup"><span data-stu-id="4b30c-111">You can use the audit history to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="4b30c-112">You can also filter the data by role if there is more than one role in the audit history.</span><span class="sxs-lookup"><span data-stu-id="4b30c-112">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="4b30c-113">Use the **time**, **action**, and **role** buttons to sort the history.</span><span class="sxs-lookup"><span data-stu-id="4b30c-113">Use the **time**, **action**, and **role** buttons to sort the history.</span></span>

## <a name="audit-history-list"></a><span data-ttu-id="4b30c-114">Audit history list</span><span class="sxs-lookup"><span data-stu-id="4b30c-114">Audit history list</span></span>
<span data-ttu-id="4b30c-115">The columns in the audit history list are:</span><span class="sxs-lookup"><span data-stu-id="4b30c-115">The columns in the audit history list are:</span></span>

* <span data-ttu-id="4b30c-116">**Requestor** - the user who requested the role activation or change.</span><span class="sxs-lookup"><span data-stu-id="4b30c-116">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="4b30c-117">If the value is "Azure System", check the Azure audit history for more information.</span><span class="sxs-lookup"><span data-stu-id="4b30c-117">If the value is "Azure System", check the Azure audit history for more information.</span></span>
* <span data-ttu-id="4b30c-118">**User** - the user who is activating or assigned to a role.</span><span class="sxs-lookup"><span data-stu-id="4b30c-118">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="4b30c-119">**Role** - the role assigned or activated by the user.</span><span class="sxs-lookup"><span data-stu-id="4b30c-119">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="4b30c-120">**Action** - the actions taken by the requestor.</span><span class="sxs-lookup"><span data-stu-id="4b30c-120">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="4b30c-121">This can include assignment, unassignment, activation, or deactivation.</span><span class="sxs-lookup"><span data-stu-id="4b30c-121">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="4b30c-122">**Time** - when the action occurred.</span><span class="sxs-lookup"><span data-stu-id="4b30c-122">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="4b30c-123">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span><span class="sxs-lookup"><span data-stu-id="4b30c-123">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="4b30c-124">**Expiration** - only relevant for activation of roles.</span><span class="sxs-lookup"><span data-stu-id="4b30c-124">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-audit-history"></a><span data-ttu-id="4b30c-125">Filter audit history</span><span class="sxs-lookup"><span data-stu-id="4b30c-125">Filter audit history</span></span>
<span data-ttu-id="4b30c-126">You can filter the information that shows up in the audit history by clicking the **Filter** button.</span><span class="sxs-lookup"><span data-stu-id="4b30c-126">You can filter the information that shows up in the audit history by clicking the **Filter** button.</span></span>  <span data-ttu-id="4b30c-127">The **Update chart parameters blade** will appear.</span><span class="sxs-lookup"><span data-stu-id="4b30c-127">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="4b30c-128">After you set the filters, click **Update** to filter the data in the history.</span><span class="sxs-lookup"><span data-stu-id="4b30c-128">After you set the filters, click **Update** to filter the data in the history.</span></span>  <span data-ttu-id="4b30c-129">If the data doesn't appear right away, refresh the page.</span><span class="sxs-lookup"><span data-stu-id="4b30c-129">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="4b30c-130">Change the date range</span><span class="sxs-lookup"><span data-stu-id="4b30c-130">Change the date range</span></span>
<span data-ttu-id="4b30c-131">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit history.</span><span class="sxs-lookup"><span data-stu-id="4b30c-131">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit history.</span></span>

<span data-ttu-id="4b30c-132">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the history.</span><span class="sxs-lookup"><span data-stu-id="4b30c-132">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the history.</span></span>  <span data-ttu-id="4b30c-133">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span><span class="sxs-lookup"><span data-stu-id="4b30c-133">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-history"></a><span data-ttu-id="4b30c-134">Change the roles included in the history</span><span class="sxs-lookup"><span data-stu-id="4b30c-134">Change the roles included in the history</span></span>
<span data-ttu-id="4b30c-135">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the history.</span><span class="sxs-lookup"><span data-stu-id="4b30c-135">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the history.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="4b30c-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b30c-136">Next steps</span></span>

- [<span data-ttu-id="4b30c-137">View audit history for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="4b30c-137">View audit history for Azure resource roles in PIM</span></span>](pim-resource-roles-use-the-audit-log.md)
