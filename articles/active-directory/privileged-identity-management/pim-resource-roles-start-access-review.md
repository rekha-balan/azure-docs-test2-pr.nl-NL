---
title: Start an access review for Azure resource roles in PIM | Microsoft Docs
description: Learn how to start an access review for Azure resource roles in Azure AD Privileged Identity Management (PIM).
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
ms.openlocfilehash: 9a35d32d89931a03b33f232ba4f79226fc3f57e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857633"
---
# <a name="start-an-access-review-for-azure-resource-roles-in-pim"></a><span data-ttu-id="67689-103">Start an access review for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="67689-103">Start an access review for Azure resource roles in PIM</span></span>
<span data-ttu-id="67689-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span><span class="sxs-lookup"><span data-stu-id="67689-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="67689-105">To reduce the risk that's associated with these stale role assignments, privileged role administrators should regularly review roles.</span><span class="sxs-lookup"><span data-stu-id="67689-105">To reduce the risk that's associated with these stale role assignments, privileged role administrators should regularly review roles.</span></span> <span data-ttu-id="67689-106">This document covers the steps for starting an access review in Privileged Identity Management (PIM) for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="67689-106">This document covers the steps for starting an access review in Privileged Identity Management (PIM) for Azure resources.</span></span>

<span data-ttu-id="67689-107">From the PIM application main page, go to:</span><span class="sxs-lookup"><span data-stu-id="67689-107">From the PIM application main page, go to:</span></span>

* <span data-ttu-id="67689-108">**Access reviews** > **Add**</span><span class="sxs-lookup"><span data-stu-id="67689-108">**Access reviews** > **Add**</span></span>

![Add access reviews](media/azure-pim-resource-rbac/rbac-access-review-home.png)

<span data-ttu-id="67689-110">When you select the **Add** button, the **Create an access review** blade appears.</span><span class="sxs-lookup"><span data-stu-id="67689-110">When you select the **Add** button, the **Create an access review** blade appears.</span></span> <span data-ttu-id="67689-111">On this blade, configure the review with a name and time limit, choose a role to review, and then decide who does the review.</span><span class="sxs-lookup"><span data-stu-id="67689-111">On this blade, configure the review with a name and time limit, choose a role to review, and then decide who does the review.</span></span>

![Create an access review](media/azure-pim-resource-rbac/rbac-create-access-review.png)

### <a name="configure-the-review"></a><span data-ttu-id="67689-113">Configure the review</span><span class="sxs-lookup"><span data-stu-id="67689-113">Configure the review</span></span>
<span data-ttu-id="67689-114">To create an access review, first name it, and then set a start and end date.</span><span class="sxs-lookup"><span data-stu-id="67689-114">To create an access review, first name it, and then set a start and end date.</span></span>

![Configure review - screenshot](media/azure-pim-resource-rbac/rbac-access-review-setting-1.png)

<span data-ttu-id="67689-116">Make the length of the review long enough for users to complete it.</span><span class="sxs-lookup"><span data-stu-id="67689-116">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="67689-117">If they finish before the end date, they can always stop the review early.</span><span class="sxs-lookup"><span data-stu-id="67689-117">If they finish before the end date, they can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="67689-118">Choose a role to review</span><span class="sxs-lookup"><span data-stu-id="67689-118">Choose a role to review</span></span>
<span data-ttu-id="67689-119">Each review focuses on only one role.</span><span class="sxs-lookup"><span data-stu-id="67689-119">Each review focuses on only one role.</span></span> <span data-ttu-id="67689-120">Unless you started the access review from a specific role blade, you need to choose a role now.</span><span class="sxs-lookup"><span data-stu-id="67689-120">Unless you started the access review from a specific role blade, you need to choose a role now.</span></span>

1. <span data-ttu-id="67689-121">Go to **Review role membership**</span><span class="sxs-lookup"><span data-stu-id="67689-121">Go to **Review role membership**</span></span>
   
    ![Review role membership - screenshot](media/azure-pim-resource-rbac/rbac-access-review-setting-2.png)
2. <span data-ttu-id="67689-123">Choose one role from the list.</span><span class="sxs-lookup"><span data-stu-id="67689-123">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="67689-124">Decide who will perform the review</span><span class="sxs-lookup"><span data-stu-id="67689-124">Decide who will perform the review</span></span>
<span data-ttu-id="67689-125">There are three options for performing a review.</span><span class="sxs-lookup"><span data-stu-id="67689-125">There are three options for performing a review.</span></span> <span data-ttu-id="67689-126">You can assign the review to someone else to complete, you can do it yourself, or each user can review their own access.</span><span class="sxs-lookup"><span data-stu-id="67689-126">You can assign the review to someone else to complete, you can do it yourself, or each user can review their own access.</span></span>

1. <span data-ttu-id="67689-127">Choose one of the options:</span><span class="sxs-lookup"><span data-stu-id="67689-127">Choose one of the options:</span></span>
   
   * <span data-ttu-id="67689-128">**Selected users**: Use this option when you don't know who needs access.</span><span class="sxs-lookup"><span data-stu-id="67689-128">**Selected users**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="67689-129">With this option, you can assign the review to a resource owner or group manager to complete.</span><span class="sxs-lookup"><span data-stu-id="67689-129">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="67689-130">**Assigned (self)**: Use this option to have the users review their own role assignments.</span><span class="sxs-lookup"><span data-stu-id="67689-130">**Assigned (self)**: Use this option to have the users review their own role assignments.</span></span>
   
2. <span data-ttu-id="67689-131">Go to **Select reviewers**.</span><span class="sxs-lookup"><span data-stu-id="67689-131">Go to **Select reviewers**.</span></span>
   
    ![Select reviewers - screenshot](media/azure-pim-resource-rbac/rbac-access-review-setting-3.png)

### <a name="start-the-review"></a><span data-ttu-id="67689-133">Start the review</span><span class="sxs-lookup"><span data-stu-id="67689-133">Start the review</span></span>
<span data-ttu-id="67689-134">Finally, you can require that users provide a reason for approving access.</span><span class="sxs-lookup"><span data-stu-id="67689-134">Finally, you can require that users provide a reason for approving access.</span></span> <span data-ttu-id="67689-135">Add a description of the review if you like.</span><span class="sxs-lookup"><span data-stu-id="67689-135">Add a description of the review if you like.</span></span> <span data-ttu-id="67689-136">Then select **Start**.</span><span class="sxs-lookup"><span data-stu-id="67689-136">Then select **Start**.</span></span>

<span data-ttu-id="67689-137">Make sure you let your users know that there's an access review waiting for them, and show them [how to perform an access review](pim-resource-roles-perform-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="67689-137">Make sure you let your users know that there's an access review waiting for them, and show them [how to perform an access review](pim-resource-roles-perform-access-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="67689-138">Manage the access review</span><span class="sxs-lookup"><span data-stu-id="67689-138">Manage the access review</span></span>
<span data-ttu-id="67689-139">In the PIM Azure resources dashboard, you can track the progress as the reviewers complete their reviews.</span><span class="sxs-lookup"><span data-stu-id="67689-139">In the PIM Azure resources dashboard, you can track the progress as the reviewers complete their reviews.</span></span> <span data-ttu-id="67689-140">No access rights are changed in the directory until [the review has been completed](pim-resource-roles-complete-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="67689-140">No access rights are changed in the directory until [the review has been completed](pim-resource-roles-complete-access-review.md).</span></span>

<span data-ttu-id="67689-141">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span><span class="sxs-lookup"><span data-stu-id="67689-141">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67689-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="67689-142">Next steps</span></span>

- [<span data-ttu-id="67689-143">Complete an access review for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="67689-143">Complete an access review for Azure resource roles in PIM</span></span>](pim-resource-roles-complete-access-review.md)
- [<span data-ttu-id="67689-144">Perform an access review of my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="67689-144">Perform an access review of my Azure resource roles in PIM</span></span>](pim-resource-roles-perform-access-review.md)
- [<span data-ttu-id="67689-145">Start an access review for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="67689-145">Start an access review for Azure AD directory roles in PIM</span></span>](pim-how-to-start-security-review.md)
