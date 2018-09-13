---
title: Start an access review for Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to start an access review for for Azure AD directory roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 06/21/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: a431a0a0000cc8b0838bbe05c703cc548c8977c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871169"
---
# <a name="start-an-access-review-for-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="d0b68-103">Start an access review for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="d0b68-103">Start an access review for Azure AD directory roles in PIM</span></span>
<span data-ttu-id="d0b68-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span><span class="sxs-lookup"><span data-stu-id="d0b68-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="d0b68-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators or global administrators should regularly create access reviews to ask admins to review the roles that users have been given.</span><span class="sxs-lookup"><span data-stu-id="d0b68-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators or global administrators should regularly create access reviews to ask admins to review the roles that users have been given.</span></span> <span data-ttu-id="d0b68-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="d0b68-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="d0b68-107">Start an access review</span><span class="sxs-lookup"><span data-stu-id="d0b68-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="d0b68-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](pim-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="d0b68-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](pim-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="d0b68-109">From the PIM application main page, there are three ways to start an access review:</span><span class="sxs-lookup"><span data-stu-id="d0b68-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="d0b68-110">**Access reviews** > **Add**</span><span class="sxs-lookup"><span data-stu-id="d0b68-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="d0b68-111">**Roles** > **Review** button</span><span class="sxs-lookup"><span data-stu-id="d0b68-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="d0b68-112">Select the specific role to be reviewed from the roles list > **Review** button</span><span class="sxs-lookup"><span data-stu-id="d0b68-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="d0b68-113">When you click on the **Review** button, the **Start an access review** blade appears.</span><span class="sxs-lookup"><span data-stu-id="d0b68-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="d0b68-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span><span class="sxs-lookup"><span data-stu-id="d0b68-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Start an access review - screenshot](./media/pim-how-to-start-security-review/PIM_start_review.png)

### <a name="configure-the-review"></a><span data-ttu-id="d0b68-116">Configure the review</span><span class="sxs-lookup"><span data-stu-id="d0b68-116">Configure the review</span></span>
<span data-ttu-id="d0b68-117">To create an access review, you need to name it and set a start and end date.</span><span class="sxs-lookup"><span data-stu-id="d0b68-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Configure review - screenshot](./media/pim-how-to-start-security-review/PIM_review_configure.png)

<span data-ttu-id="d0b68-119">Make the length of the review long enough for users to complete it.</span><span class="sxs-lookup"><span data-stu-id="d0b68-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="d0b68-120">If you finish before the end date, you can always stop the review early.</span><span class="sxs-lookup"><span data-stu-id="d0b68-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="d0b68-121">Choose a role to review</span><span class="sxs-lookup"><span data-stu-id="d0b68-121">Choose a role to review</span></span>
<span data-ttu-id="d0b68-122">Each review focuses on only one role.</span><span class="sxs-lookup"><span data-stu-id="d0b68-122">Each review focuses on only one role.</span></span> <span data-ttu-id="d0b68-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span><span class="sxs-lookup"><span data-stu-id="d0b68-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="d0b68-124">Navigate to **Review role membership**</span><span class="sxs-lookup"><span data-stu-id="d0b68-124">Navigate to **Review role membership**</span></span>
   
    ![Review role membership - screenshot](./media/pim-how-to-start-security-review/PIM_review_role.png)
2. <span data-ttu-id="d0b68-126">Choose one role from the list.</span><span class="sxs-lookup"><span data-stu-id="d0b68-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="d0b68-127">Decide who will perform the review</span><span class="sxs-lookup"><span data-stu-id="d0b68-127">Decide who will perform the review</span></span>
<span data-ttu-id="d0b68-128">There are three options for performing a review.</span><span class="sxs-lookup"><span data-stu-id="d0b68-128">There are three options for performing a review.</span></span> <span data-ttu-id="d0b68-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span><span class="sxs-lookup"><span data-stu-id="d0b68-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="d0b68-130">Navigate to **Select reviewers**</span><span class="sxs-lookup"><span data-stu-id="d0b68-130">Navigate to **Select reviewers**</span></span>
   
    ![Select reviewers - screenshot](./media/pim-how-to-start-security-review/PIM_review_reviewers.png)
2. <span data-ttu-id="d0b68-132">Choose one of the options:</span><span class="sxs-lookup"><span data-stu-id="d0b68-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="d0b68-133">**Select reviewer**: Use this option when you don't know who needs access.</span><span class="sxs-lookup"><span data-stu-id="d0b68-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="d0b68-134">With this option, you can assign the review to a resource owner or group manager to complete.</span><span class="sxs-lookup"><span data-stu-id="d0b68-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="d0b68-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span><span class="sxs-lookup"><span data-stu-id="d0b68-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="d0b68-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span><span class="sxs-lookup"><span data-stu-id="d0b68-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="d0b68-137">Start the review</span><span class="sxs-lookup"><span data-stu-id="d0b68-137">Start the review</span></span>
<span data-ttu-id="d0b68-138">Finally, you have the option to require that users provide a reason if they approve their access.</span><span class="sxs-lookup"><span data-stu-id="d0b68-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="d0b68-139">Add a description of the review if you like, and select **Start**.</span><span class="sxs-lookup"><span data-stu-id="d0b68-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="d0b68-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](pim-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="d0b68-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](pim-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="d0b68-141">Manage the access review</span><span class="sxs-lookup"><span data-stu-id="d0b68-141">Manage the access review</span></span>
<span data-ttu-id="d0b68-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span><span class="sxs-lookup"><span data-stu-id="d0b68-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="d0b68-143">No access rights will be changed in the directory until [the review completes](pim-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="d0b68-143">No access rights will be changed in the directory until [the review completes](pim-how-to-complete-review.md).</span></span>

<span data-ttu-id="d0b68-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span><span class="sxs-lookup"><span data-stu-id="d0b68-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d0b68-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0b68-145">Next steps</span></span>

- [<span data-ttu-id="d0b68-146">Complete an access review for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="d0b68-146">Complete an access review for Azure AD directory roles in PIM</span></span>](pim-how-to-complete-review.md)
- [<span data-ttu-id="d0b68-147">Perform an access review of my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="d0b68-147">Perform an access review of my Azure AD directory roles in PIM</span></span>](pim-how-to-perform-security-review.md)
- [<span data-ttu-id="d0b68-148">Start an access review for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="d0b68-148">Start an access review for Azure resource roles in PIM</span></span>](pim-resource-roles-start-access-review.md)
