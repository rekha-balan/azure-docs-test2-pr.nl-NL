---
title: How to complete an access review | Microsoft Docs
description: After you started an access review in Azure AD Privileged Identity Management, learn how to complete it and view the results
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/03/2017
ms.author: kgremban
ms.openlocfilehash: 807a0a9a3a81dacd1f657c87c909d9c76efbaaca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552435"
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="ecb06-103">How to complete an access review in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ecb06-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="ecb06-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="ecb06-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="ecb06-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span><span class="sxs-lookup"><span data-stu-id="ecb06-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="ecb06-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="ecb06-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="ecb06-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span><span class="sxs-lookup"><span data-stu-id="ecb06-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="ecb06-108">Manage security reviews</span><span class="sxs-lookup"><span data-stu-id="ecb06-108">Manage security reviews</span></span>
1. <span data-ttu-id="ecb06-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="ecb06-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="ecb06-110">Select the **Access reviews** section of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="ecb06-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="ecb06-111">Select the access review that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="ecb06-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="ecb06-112">On the access review's detail blade there are a number options for managing that review.</span><span class="sxs-lookup"><span data-stu-id="ecb06-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![PIM access review buttons - screenshot][1]

### <a name="remind"></a><span data-ttu-id="ecb06-114">Remind</span><span class="sxs-lookup"><span data-stu-id="ecb06-114">Remind</span></span>
<span data-ttu-id="ecb06-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span><span class="sxs-lookup"><span data-stu-id="ecb06-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="ecb06-116">Stop</span><span class="sxs-lookup"><span data-stu-id="ecb06-116">Stop</span></span>
<span data-ttu-id="ecb06-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span><span class="sxs-lookup"><span data-stu-id="ecb06-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="ecb06-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span><span class="sxs-lookup"><span data-stu-id="ecb06-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="ecb06-119">You cannot restart a review after it's been stopped.</span><span class="sxs-lookup"><span data-stu-id="ecb06-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="ecb06-120">Apply</span><span class="sxs-lookup"><span data-stu-id="ecb06-120">Apply</span></span>
<span data-ttu-id="ecb06-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span><span class="sxs-lookup"><span data-stu-id="ecb06-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="ecb06-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span><span class="sxs-lookup"><span data-stu-id="ecb06-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="ecb06-123">Export</span><span class="sxs-lookup"><span data-stu-id="ecb06-123">Export</span></span>
<span data-ttu-id="ecb06-124">If you want to apply the results of the security review manually, you can export the review.</span><span class="sxs-lookup"><span data-stu-id="ecb06-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="ecb06-125">The **Export** button will start downloading a CSV file.</span><span class="sxs-lookup"><span data-stu-id="ecb06-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="ecb06-126">You can manage the results in Excel or other programs that open CSV files.</span><span class="sxs-lookup"><span data-stu-id="ecb06-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="ecb06-127">Delete</span><span class="sxs-lookup"><span data-stu-id="ecb06-127">Delete</span></span>
<span data-ttu-id="ecb06-128">If you are not interested in the review any further, delete it.</span><span class="sxs-lookup"><span data-stu-id="ecb06-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="ecb06-129">The **Delete** button removes the review from the PIM application.</span><span class="sxs-lookup"><span data-stu-id="ecb06-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecb06-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span><span class="sxs-lookup"><span data-stu-id="ecb06-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ecb06-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="ecb06-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png

