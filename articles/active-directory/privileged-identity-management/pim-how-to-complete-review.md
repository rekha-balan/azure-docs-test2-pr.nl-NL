---
title: Complete an access review for Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to complete an access review for Azure AD directory roles in Azure AD Privileged Identity Management (PIM) and view the results
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 06/06/2017
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 3955f4bf9b579ae40424c2650f9d3b4c2ac4f030
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866734"
---
# <a name="complete-an-access-review-for-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="a0f04-103">Complete an access review for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="a0f04-103">Complete an access review for Azure AD directory roles in PIM</span></span>
<span data-ttu-id="a0f04-104">Privileged role administrators can review privileged access once an [access review has been started](pim-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="a0f04-104">Privileged role administrators can review privileged access once an [access review has been started](pim-how-to-start-security-review.md).</span></span> <span data-ttu-id="a0f04-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span><span class="sxs-lookup"><span data-stu-id="a0f04-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="a0f04-106">If a user did not get an email, you can send them the instructions in [how to perform an access review](pim-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="a0f04-106">If a user did not get an email, you can send them the instructions in [how to perform an access review](pim-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="a0f04-107">After the access review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span><span class="sxs-lookup"><span data-stu-id="a0f04-107">After the access review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-access-reviews"></a><span data-ttu-id="a0f04-108">Manage access reviews</span><span class="sxs-lookup"><span data-stu-id="a0f04-108">Manage access reviews</span></span>
1. <span data-ttu-id="a0f04-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="a0f04-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="a0f04-110">Select the **Access reviews** section of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a0f04-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="a0f04-111">Select the access review that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="a0f04-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="a0f04-112">On the access review's detail blade, there are a number options for managing that review.</span><span class="sxs-lookup"><span data-stu-id="a0f04-112">On the access review's detail blade, there are a number options for managing that review.</span></span>

![PIM access review buttons - screenshot](./media/pim-how-to-complete-review/PIM_review_buttons.png)

### <a name="remind"></a><span data-ttu-id="a0f04-114">Remind</span><span class="sxs-lookup"><span data-stu-id="a0f04-114">Remind</span></span>
<span data-ttu-id="a0f04-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span><span class="sxs-lookup"><span data-stu-id="a0f04-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="a0f04-116">Stop</span><span class="sxs-lookup"><span data-stu-id="a0f04-116">Stop</span></span>
<span data-ttu-id="a0f04-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span><span class="sxs-lookup"><span data-stu-id="a0f04-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="a0f04-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span><span class="sxs-lookup"><span data-stu-id="a0f04-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="a0f04-119">You cannot restart a review after it's been stopped.</span><span class="sxs-lookup"><span data-stu-id="a0f04-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="a0f04-120">Apply</span><span class="sxs-lookup"><span data-stu-id="a0f04-120">Apply</span></span>
<span data-ttu-id="a0f04-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span><span class="sxs-lookup"><span data-stu-id="a0f04-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="a0f04-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span><span class="sxs-lookup"><span data-stu-id="a0f04-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="a0f04-123">Export</span><span class="sxs-lookup"><span data-stu-id="a0f04-123">Export</span></span>
<span data-ttu-id="a0f04-124">If you want to apply the results of the access review manually, you can export the review.</span><span class="sxs-lookup"><span data-stu-id="a0f04-124">If you want to apply the results of the access review manually, you can export the review.</span></span> <span data-ttu-id="a0f04-125">The **Export** button will start downloading a CSV file.</span><span class="sxs-lookup"><span data-stu-id="a0f04-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="a0f04-126">You can manage the results in Excel or other programs that open CSV files.</span><span class="sxs-lookup"><span data-stu-id="a0f04-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="a0f04-127">Delete</span><span class="sxs-lookup"><span data-stu-id="a0f04-127">Delete</span></span>
<span data-ttu-id="a0f04-128">If you are not interested in the review any further, delete it.</span><span class="sxs-lookup"><span data-stu-id="a0f04-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="a0f04-129">The **Delete** button removes the review from the PIM application.</span><span class="sxs-lookup"><span data-stu-id="a0f04-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0f04-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span><span class="sxs-lookup"><span data-stu-id="a0f04-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a0f04-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0f04-131">Next steps</span></span>

- [<span data-ttu-id="a0f04-132">Start an access review for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="a0f04-132">Start an access review for Azure AD directory roles in PIM</span></span>](pim-how-to-start-security-review.md)
- [<span data-ttu-id="a0f04-133">Perform an access review of my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="a0f04-133">Perform an access review of my Azure AD directory roles in PIM</span></span>](pim-how-to-perform-security-review.md)
