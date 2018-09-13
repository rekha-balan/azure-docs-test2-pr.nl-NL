---
title: Complete an access review for Azure resource roles in PIM | Microsoft Docs
description: Learn how to complete an access review for Azure resource roles in Azure AD Privileged Identity Management (PIM).
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
ms.openlocfilehash: f998c509e9bea65980367690a5e9d03f579b8e98
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857827"
---
# <a name="complete-an-access-review-for-azure-resource-roles-in-pim"></a><span data-ttu-id="2082f-103">Complete an access review for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="2082f-103">Complete an access review for Azure resource roles in PIM</span></span>
<span data-ttu-id="2082f-104">Privileged role administrators can review privileged access after an [access review has been started](pim-resource-roles-start-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="2082f-104">Privileged role administrators can review privileged access after an [access review has been started](pim-resource-roles-start-access-review.md).</span></span> <span data-ttu-id="2082f-105">Privileged Identity Management (PIM) for Azure resources automatically sends an email that prompts users to review their access.</span><span class="sxs-lookup"><span data-stu-id="2082f-105">Privileged Identity Management (PIM) for Azure resources automatically sends an email that prompts users to review their access.</span></span> <span data-ttu-id="2082f-106">If a user doesn't receive an email, you can send them the instructions for [how to perform an access review](pim-resource-roles-perform-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="2082f-106">If a user doesn't receive an email, you can send them the instructions for [how to perform an access review](pim-resource-roles-perform-access-review.md).</span></span>

<span data-ttu-id="2082f-107">After the access review period is over, or after all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span><span class="sxs-lookup"><span data-stu-id="2082f-107">After the access review period is over, or after all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-access-reviews"></a><span data-ttu-id="2082f-108">Manage access reviews</span><span class="sxs-lookup"><span data-stu-id="2082f-108">Manage access reviews</span></span>
1. <span data-ttu-id="2082f-109">Go to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2082f-109">Go to the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="2082f-110">Then, on the dashboard, select the **Azure resources** application.</span><span class="sxs-lookup"><span data-stu-id="2082f-110">Then, on the dashboard, select the **Azure resources** application.</span></span>

2. <span data-ttu-id="2082f-111">Select your resource.</span><span class="sxs-lookup"><span data-stu-id="2082f-111">Select your resource.</span></span>

3. <span data-ttu-id="2082f-112">Select the **Access reviews** section of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="2082f-112">Select the **Access reviews** section of the dashboard.</span></span>
<span data-ttu-id="2082f-113">![Access reviews](media/azure-pim-resource-rbac/rbac-access-review-home-list.png)</span><span class="sxs-lookup"><span data-stu-id="2082f-113">![Access reviews](media/azure-pim-resource-rbac/rbac-access-review-home-list.png)</span></span>

4. <span data-ttu-id="2082f-114">Select the access review that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="2082f-114">Select the access review that you want to manage.</span></span>

<span data-ttu-id="2082f-115">On the detail blade of the access review, there are a number of options for managing that review.</span><span class="sxs-lookup"><span data-stu-id="2082f-115">On the detail blade of the access review, there are a number of options for managing that review.</span></span> <span data-ttu-id="2082f-116">The options are as follows:</span><span class="sxs-lookup"><span data-stu-id="2082f-116">The options are as follows:</span></span>

![Options for managing a review](media/azure-pim-resource-rbac/rbac-access-review-menu.png)

### <a name="stop"></a><span data-ttu-id="2082f-118">Stop</span><span class="sxs-lookup"><span data-stu-id="2082f-118">Stop</span></span>
<span data-ttu-id="2082f-119">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span><span class="sxs-lookup"><span data-stu-id="2082f-119">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="2082f-120">All users who haven't finished their review by this time won't be able to finish it after you stop the review.</span><span class="sxs-lookup"><span data-stu-id="2082f-120">All users who haven't finished their review by this time won't be able to finish it after you stop the review.</span></span> <span data-ttu-id="2082f-121">You can't restart a review after it's been stopped.</span><span class="sxs-lookup"><span data-stu-id="2082f-121">You can't restart a review after it's been stopped.</span></span>

### <a name="reset"></a><span data-ttu-id="2082f-122">Reset</span><span class="sxs-lookup"><span data-stu-id="2082f-122">Reset</span></span>
<span data-ttu-id="2082f-123">You can reset an access review to remove all decisions that are made on it.</span><span class="sxs-lookup"><span data-stu-id="2082f-123">You can reset an access review to remove all decisions that are made on it.</span></span> <span data-ttu-id="2082f-124">After you've reset an access review, all users are marked as unreviewed again.</span><span class="sxs-lookup"><span data-stu-id="2082f-124">After you've reset an access review, all users are marked as unreviewed again.</span></span> 

### <a name="apply"></a><span data-ttu-id="2082f-125">Apply</span><span class="sxs-lookup"><span data-stu-id="2082f-125">Apply</span></span>
<span data-ttu-id="2082f-126">After an access review is complete, use the **Apply** button to implement the outcome of the review.</span><span class="sxs-lookup"><span data-stu-id="2082f-126">After an access review is complete, use the **Apply** button to implement the outcome of the review.</span></span> <span data-ttu-id="2082f-127">If a user's access was denied in the review, this step removes their role assignment.</span><span class="sxs-lookup"><span data-stu-id="2082f-127">If a user's access was denied in the review, this step removes their role assignment.</span></span>  

### <a name="delete"></a><span data-ttu-id="2082f-128">Delete</span><span class="sxs-lookup"><span data-stu-id="2082f-128">Delete</span></span>
<span data-ttu-id="2082f-129">If you aren't interested in the review any more, delete it.</span><span class="sxs-lookup"><span data-stu-id="2082f-129">If you aren't interested in the review any more, delete it.</span></span> <span data-ttu-id="2082f-130">The **Delete** button removes the review from the PIM application.</span><span class="sxs-lookup"><span data-stu-id="2082f-130">The **Delete** button removes the review from the PIM application.</span></span>

## <a name="results"></a><span data-ttu-id="2082f-131">Results</span><span class="sxs-lookup"><span data-stu-id="2082f-131">Results</span></span>
<span data-ttu-id="2082f-132">On the **Results** tab, view and download a list of your review results.</span><span class="sxs-lookup"><span data-stu-id="2082f-132">On the **Results** tab, view and download a list of your review results.</span></span> 
<span data-ttu-id="2082f-133">![Results tab](media/azure-pim-resource-rbac/rbac-access-review-results.png)</span><span class="sxs-lookup"><span data-stu-id="2082f-133">![Results tab](media/azure-pim-resource-rbac/rbac-access-review-results.png)</span></span>

## <a name="reviewers"></a><span data-ttu-id="2082f-134">Reviewers</span><span class="sxs-lookup"><span data-stu-id="2082f-134">Reviewers</span></span>
<span data-ttu-id="2082f-135">View and add reviewers to your existing access review.</span><span class="sxs-lookup"><span data-stu-id="2082f-135">View and add reviewers to your existing access review.</span></span> <span data-ttu-id="2082f-136">Remind reviewers to complete their reviews.</span><span class="sxs-lookup"><span data-stu-id="2082f-136">Remind reviewers to complete their reviews.</span></span>
<span data-ttu-id="2082f-137">![Add reviewers](media/azure-pim-resource-rbac/rbac-access-review-reviewers.png)</span><span class="sxs-lookup"><span data-stu-id="2082f-137">![Add reviewers](media/azure-pim-resource-rbac/rbac-access-review-reviewers.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2082f-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="2082f-138">Next steps</span></span>

- [<span data-ttu-id="2082f-139">Start an access review for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="2082f-139">Start an access review for Azure resource roles in PIM</span></span>](pim-resource-roles-start-access-review.md)
- [<span data-ttu-id="2082f-140">Perform an access review of my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="2082f-140">Perform an access review of my Azure resource roles in PIM</span></span>](pim-resource-roles-perform-access-review.md)
