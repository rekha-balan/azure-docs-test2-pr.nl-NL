---
title: Complete an access review of members of a group or users' access to an application with Azure AD| Microsoft Docs
description: Learn how to complete an access review for members of a group or users with access to an application in Azure Active Directory.
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
ms.component: compliance
ms.date: 05/02/2018
ms.author: rolyon
ms.reviewer: mwahl
ms.openlocfilehash: ad85c8d64d6cc160c1f3e75bf2288a4efc6d281c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870313"
---
# <a name="complete-an-access-review-of-members-of-a-group-or-users-access-to-an-application-in-azure-ad"></a><span data-ttu-id="13c61-103">Complete an access review of members of a group or users' access to an application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="13c61-103">Complete an access review of members of a group or users' access to an application in Azure AD</span></span>

<span data-ttu-id="13c61-104">Administrators can use Azure Active Directory (Azure AD) to [create an access review](active-directory-azure-ad-controls-create-access-review.md) for group members or users assigned to an application.</span><span class="sxs-lookup"><span data-stu-id="13c61-104">Administrators can use Azure Active Directory (Azure AD) to [create an access review](active-directory-azure-ad-controls-create-access-review.md) for group members or users assigned to an application.</span></span> <span data-ttu-id="13c61-105">Azure AD automatically sends reviewers an email that prompts them to review access.</span><span class="sxs-lookup"><span data-stu-id="13c61-105">Azure AD automatically sends reviewers an email that prompts them to review access.</span></span> <span data-ttu-id="13c61-106">If a user didn't get an email, you can send them the instructions in [Review your access](active-directory-azure-ad-controls-perform-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="13c61-106">If a user didn't get an email, you can send them the instructions in [Review your access](active-directory-azure-ad-controls-perform-access-review.md).</span></span> <span data-ttu-id="13c61-107">(Note that guests who are assigned as reviewers but have not accepted the invite will not receive an email from access reviews, as they must first accept an invite prior to reviewing.) After the access review period is over or if an administrator stops the access review, follow the steps in this article to see and apply the results.</span><span class="sxs-lookup"><span data-stu-id="13c61-107">(Note that guests who are assigned as reviewers but have not accepted the invite will not receive an email from access reviews, as they must first accept an invite prior to reviewing.) After the access review period is over or if an administrator stops the access review, follow the steps in this article to see and apply the results.</span></span>

## <a name="view-an-access-review-in-the-azure-portal"></a><span data-ttu-id="13c61-108">View an access review in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="13c61-108">View an access review in the Azure portal</span></span>

1. <span data-ttu-id="13c61-109">Go to the [access reviews page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/), select **Programs**, and select the program that contains the access review control.</span><span class="sxs-lookup"><span data-stu-id="13c61-109">Go to the [access reviews page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/), select **Programs**, and select the program that contains the access review control.</span></span>

2. <span data-ttu-id="13c61-110">Select **Manage**, and select the access review control.</span><span class="sxs-lookup"><span data-stu-id="13c61-110">Select **Manage**, and select the access review control.</span></span> <span data-ttu-id="13c61-111">If there are many controls in the program, you can filter for controls of a specific type and sort by their status.</span><span class="sxs-lookup"><span data-stu-id="13c61-111">If there are many controls in the program, you can filter for controls of a specific type and sort by their status.</span></span> <span data-ttu-id="13c61-112">You also can search by the name of the access review control or the display name of the owner who created it.</span><span class="sxs-lookup"><span data-stu-id="13c61-112">You also can search by the name of the access review control or the display name of the owner who created it.</span></span> 

## <a name="stop-a-review-that-hasnt-finished"></a><span data-ttu-id="13c61-113">Stop a review that hasn't finished</span><span class="sxs-lookup"><span data-stu-id="13c61-113">Stop a review that hasn't finished</span></span>

<span data-ttu-id="13c61-114">If the review hasn't reached the scheduled end date, an administrator can select **Stop** to end the review early.</span><span class="sxs-lookup"><span data-stu-id="13c61-114">If the review hasn't reached the scheduled end date, an administrator can select **Stop** to end the review early.</span></span> <span data-ttu-id="13c61-115">After you stop the review, users can no longer be reviewed.</span><span class="sxs-lookup"><span data-stu-id="13c61-115">After you stop the review, users can no longer be reviewed.</span></span> <span data-ttu-id="13c61-116">You can't restart a review after it's stopped.</span><span class="sxs-lookup"><span data-stu-id="13c61-116">You can't restart a review after it's stopped.</span></span>

## <a name="apply-the-changes"></a><span data-ttu-id="13c61-117">Apply the changes</span><span class="sxs-lookup"><span data-stu-id="13c61-117">Apply the changes</span></span> 

<span data-ttu-id="13c61-118">After an access review is finished, either because it reached the end date or an administrator stopped it manually, and auto-apply wasn't configured for the review, you can select **Apply** to manually apply the changes.</span><span class="sxs-lookup"><span data-stu-id="13c61-118">After an access review is finished, either because it reached the end date or an administrator stopped it manually, and auto-apply wasn't configured for the review, you can select **Apply** to manually apply the changes.</span></span> <span data-ttu-id="13c61-119">The outcome of the review is implemented by updating the group or application.</span><span class="sxs-lookup"><span data-stu-id="13c61-119">The outcome of the review is implemented by updating the group or application.</span></span> <span data-ttu-id="13c61-120">If a user's access was denied in the review, when an administrator selects this option, Azure AD removes their membership or application assignment.</span><span class="sxs-lookup"><span data-stu-id="13c61-120">If a user's access was denied in the review, when an administrator selects this option, Azure AD removes their membership or application assignment.</span></span> 

<span data-ttu-id="13c61-121">After an access review is finished, and auto-apply was configured, then the status of the review will change from Completed through intermediate states and finally will change to state Applied.</span><span class="sxs-lookup"><span data-stu-id="13c61-121">After an access review is finished, and auto-apply was configured, then the status of the review will change from Completed through intermediate states and finally will change to state Applied.</span></span> <span data-ttu-id="13c61-122">You should expect to see denied users, if any, being removed from the resource group membership or app assignment in a few minutes.</span><span class="sxs-lookup"><span data-stu-id="13c61-122">You should expect to see denied users, if any, being removed from the resource group membership or app assignment in a few minutes.</span></span>

<span data-ttu-id="13c61-123">A configured auto applying review, or selecting **Apply** doesn't have an effect on a group that originates in an on-premises directory or a dynamic group.</span><span class="sxs-lookup"><span data-stu-id="13c61-123">A configured auto applying review, or selecting **Apply** doesn't have an effect on a group that originates in an on-premises directory or a dynamic group.</span></span> <span data-ttu-id="13c61-124">If you want to change a group that originates on-premises, download the results and apply those changes to the representation of the group in that directory.</span><span class="sxs-lookup"><span data-stu-id="13c61-124">If you want to change a group that originates on-premises, download the results and apply those changes to the representation of the group in that directory.</span></span>

## <a name="download-the-results-of-the-review"></a><span data-ttu-id="13c61-125">Download the results of the review</span><span class="sxs-lookup"><span data-stu-id="13c61-125">Download the results of the review</span></span>

<span data-ttu-id="13c61-126">To retrieve the results of the review, select **Approvals** and then select **Download**.</span><span class="sxs-lookup"><span data-stu-id="13c61-126">To retrieve the results of the review, select **Approvals** and then select **Download**.</span></span> <span data-ttu-id="13c61-127">The resulting CSV file can be viewed in Excel or in other programs that open UTF-8 encoded CSV files.</span><span class="sxs-lookup"><span data-stu-id="13c61-127">The resulting CSV file can be viewed in Excel or in other programs that open UTF-8 encoded CSV files.</span></span>

## <a name="optional-delete-a-review"></a><span data-ttu-id="13c61-128">Optional: Delete a review</span><span class="sxs-lookup"><span data-stu-id="13c61-128">Optional: Delete a review</span></span>
<span data-ttu-id="13c61-129">If you're no longer interested in the review, you can delete it.</span><span class="sxs-lookup"><span data-stu-id="13c61-129">If you're no longer interested in the review, you can delete it.</span></span> <span data-ttu-id="13c61-130">Select **Delete** to remove the review from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13c61-130">Select **Delete** to remove the review from Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13c61-131">There's no warning before deletion occurs, so be sure that you want to delete the review.</span><span class="sxs-lookup"><span data-stu-id="13c61-131">There's no warning before deletion occurs, so be sure that you want to delete the review.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="13c61-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="13c61-132">Next steps</span></span>

- [<span data-ttu-id="13c61-133">Manage user access with Azure AD access reviews</span><span class="sxs-lookup"><span data-stu-id="13c61-133">Manage user access with Azure AD access reviews</span></span>](active-directory-azure-ad-controls-manage-user-access-with-access-reviews.md)
- [<span data-ttu-id="13c61-134">Manage guest access with Azure AD access reviews</span><span class="sxs-lookup"><span data-stu-id="13c61-134">Manage guest access with Azure AD access reviews</span></span>](active-directory-azure-ad-controls-manage-guest-access-with-access-reviews.md)
- [<span data-ttu-id="13c61-135">Manage programs and controls for Azure AD access reviews</span><span class="sxs-lookup"><span data-stu-id="13c61-135">Manage programs and controls for Azure AD access reviews</span></span>](active-directory-azure-ad-controls-manage-programs-controls.md)
- [<span data-ttu-id="13c61-136">Create an access review for members of a group or access to an application</span><span class="sxs-lookup"><span data-stu-id="13c61-136">Create an access review for members of a group or access to an application</span></span>](active-directory-azure-ad-controls-create-access-review.md)
- [<span data-ttu-id="13c61-137">Create an access review of users in an Azure AD administrative role</span><span class="sxs-lookup"><span data-stu-id="13c61-137">Create an access review of users in an Azure AD administrative role</span></span>](privileged-identity-management/pim-how-to-start-security-review.md)
