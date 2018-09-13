---
title: How to start an access review | Microsoft Docs
description: Learn how to create an access review for privileged identities with the Azure Privileged Identity Management application.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: bc0552d1bc296268f63fb2de0fddfe2e70e78bfc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555615"
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="b9a34-103">How to start an access review in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b9a34-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b9a34-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span><span class="sxs-lookup"><span data-stu-id="b9a34-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="b9a34-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span><span class="sxs-lookup"><span data-stu-id="b9a34-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="b9a34-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="b9a34-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="b9a34-107">Start an access review</span><span class="sxs-lookup"><span data-stu-id="b9a34-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="b9a34-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="b9a34-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="b9a34-109">From the PIM application main page, there are three ways to start an access review:</span><span class="sxs-lookup"><span data-stu-id="b9a34-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="b9a34-110">**Access reviews** > **Add**</span><span class="sxs-lookup"><span data-stu-id="b9a34-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="b9a34-111">**Roles** > **Review** button</span><span class="sxs-lookup"><span data-stu-id="b9a34-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="b9a34-112">Select the specific role to be reviewed from the roles list > **Review** button</span><span class="sxs-lookup"><span data-stu-id="b9a34-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="b9a34-113">When you click on the **Review** button, the **Start an access review** blade appears.</span><span class="sxs-lookup"><span data-stu-id="b9a34-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="b9a34-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span><span class="sxs-lookup"><span data-stu-id="b9a34-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Start an access review - screenshot][1]

### <a name="configure-the-review"></a><span data-ttu-id="b9a34-116">Configure the review</span><span class="sxs-lookup"><span data-stu-id="b9a34-116">Configure the review</span></span>
<span data-ttu-id="b9a34-117">To create an access review, you need to name it and set a start and end date.</span><span class="sxs-lookup"><span data-stu-id="b9a34-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Configure review - screenshot][2]

<span data-ttu-id="b9a34-119">Make the length of the review long enough for users to complete it.</span><span class="sxs-lookup"><span data-stu-id="b9a34-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="b9a34-120">If you finish before the end date, you can always stop the review early.</span><span class="sxs-lookup"><span data-stu-id="b9a34-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="b9a34-121">Choose a role to review</span><span class="sxs-lookup"><span data-stu-id="b9a34-121">Choose a role to review</span></span>
<span data-ttu-id="b9a34-122">Each review focuses on only one role.</span><span class="sxs-lookup"><span data-stu-id="b9a34-122">Each review focuses on only one role.</span></span> <span data-ttu-id="b9a34-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span><span class="sxs-lookup"><span data-stu-id="b9a34-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="b9a34-124">Navigate to **Review role membership**</span><span class="sxs-lookup"><span data-stu-id="b9a34-124">Navigate to **Review role membership**</span></span>
   
    ![Review role membership - screenshot][3]
2. <span data-ttu-id="b9a34-126">Choose one role from the list.</span><span class="sxs-lookup"><span data-stu-id="b9a34-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="b9a34-127">Decide who will perform the review</span><span class="sxs-lookup"><span data-stu-id="b9a34-127">Decide who will perform the review</span></span>
<span data-ttu-id="b9a34-128">There are three options for performing a review.</span><span class="sxs-lookup"><span data-stu-id="b9a34-128">There are three options for performing a review.</span></span> <span data-ttu-id="b9a34-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span><span class="sxs-lookup"><span data-stu-id="b9a34-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="b9a34-130">Navigate to **Select reviewers**</span><span class="sxs-lookup"><span data-stu-id="b9a34-130">Navigate to **Select reviewers**</span></span>
   
    ![Select reviewers - screenshot][4]
2. <span data-ttu-id="b9a34-132">Choose one of the options:</span><span class="sxs-lookup"><span data-stu-id="b9a34-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="b9a34-133">**Select reviewer**: Use this option when you don't know who needs access.</span><span class="sxs-lookup"><span data-stu-id="b9a34-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="b9a34-134">With this option, you can assign the review to a resource owner or group manager to complete.</span><span class="sxs-lookup"><span data-stu-id="b9a34-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="b9a34-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span><span class="sxs-lookup"><span data-stu-id="b9a34-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="b9a34-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span><span class="sxs-lookup"><span data-stu-id="b9a34-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="b9a34-137">Start the review</span><span class="sxs-lookup"><span data-stu-id="b9a34-137">Start the review</span></span>
<span data-ttu-id="b9a34-138">Finally, you have the option to require that users provide a reason if they approve their access.</span><span class="sxs-lookup"><span data-stu-id="b9a34-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="b9a34-139">Add a description of the review if you like, and select **Start**.</span><span class="sxs-lookup"><span data-stu-id="b9a34-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="b9a34-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="b9a34-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="b9a34-141">Manage the access review</span><span class="sxs-lookup"><span data-stu-id="b9a34-141">Manage the access review</span></span>
<span data-ttu-id="b9a34-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span><span class="sxs-lookup"><span data-stu-id="b9a34-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="b9a34-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="b9a34-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="b9a34-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span><span class="sxs-lookup"><span data-stu-id="b9a34-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="b9a34-145">PIM Table of Contents</span><span class="sxs-lookup"><span data-stu-id="b9a34-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png




