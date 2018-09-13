---
title: Review access by using Azure AD access reviews | Microsoft Docs
description: Learn how to review access by using Azure Active Directory access reviews.
services: active-directory
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: compliance
ms.date: 07/16/2018
ms.author: rolyon
ms.reviewer: mwahl
ms.openlocfilehash: f9ab4f5ad863fa5460b5a7ad68f00f154a16f8f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868049"
---
# <a name="review-access-with-azure-ad-access-reviews"></a><span data-ttu-id="ef2b6-103">Review access with Azure AD access reviews</span><span class="sxs-lookup"><span data-stu-id="ef2b6-103">Review access with Azure AD access reviews</span></span>

<span data-ttu-id="ef2b6-104">Azure Active Directory (Azure AD) simplifies how enterprises manage access to applications and members of groups in Azure AD and other Microsoft Online Services with a feature called access reviews.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-104">Azure Active Directory (Azure AD) simplifies how enterprises manage access to applications and members of groups in Azure AD and other Microsoft Online Services with a feature called access reviews.</span></span> <span data-ttu-id="ef2b6-105">Perhaps you  received an email from Microsoft that asks you to review access for members of a group or users with access to an application.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-105">Perhaps you  received an email from Microsoft that asks you to review access for members of a group or users with access to an application.</span></span> 

## <a name="open-an-access-review"></a><span data-ttu-id="ef2b6-106">Open an access review</span><span class="sxs-lookup"><span data-stu-id="ef2b6-106">Open an access review</span></span>

<span data-ttu-id="ef2b6-107">To see the pending access reviews, click the review access link in the email.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-107">To see the pending access reviews, click the review access link in the email.</span></span> <span data-ttu-id="ef2b6-108">Starting in August 2018, the email notifications for Azure AD roles have an updated design.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-108">Starting in August 2018, the email notifications for Azure AD roles have an updated design.</span></span> <span data-ttu-id="ef2b6-109">The following shows an example email that is sent when a user is invited to be a reviewer.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-109">The following shows an example email that is sent when a user is invited to be a reviewer.</span></span> 

![Review access email](./media/active-directory-azure-ad-controls-perform-access-review/new-ar-email.png)

<span data-ttu-id="ef2b6-111">If you don't have the email, you can locate the access reviews by following these steps:</span><span class="sxs-lookup"><span data-stu-id="ef2b6-111">If you don't have the email, you can locate the access reviews by following these steps:</span></span>

1. <span data-ttu-id="ef2b6-112">Sign in on the [Azure AD access panel](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ef2b6-112">Sign in on the [Azure AD access panel](https://myapps.microsoft.com).</span></span>

2. <span data-ttu-id="ef2b6-113">Select the user symbol in the upper-right corner of the page, which displays your name and default organization.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-113">Select the user symbol in the upper-right corner of the page, which displays your name and default organization.</span></span> <span data-ttu-id="ef2b6-114">If more than one organization is listed, select the organization that requested an access review.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-114">If more than one organization is listed, select the organization that requested an access review.</span></span>

3. <span data-ttu-id="ef2b6-115">If a tile labeled **Access reviews** is on the right side of the page, select it.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-115">If a tile labeled **Access reviews** is on the right side of the page, select it.</span></span> <span data-ttu-id="ef2b6-116">If the tile isn't visible, there are no access reviews to perform for that organization and no action is needed at this time.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-116">If the tile isn't visible, there are no access reviews to perform for that organization and no action is needed at this time.</span></span>

## <a name="fill-out-an-access-review"></a><span data-ttu-id="ef2b6-117">Fill out an access review</span><span class="sxs-lookup"><span data-stu-id="ef2b6-117">Fill out an access review</span></span>

<span data-ttu-id="ef2b6-118">When you select an access review from the list, you see the names of users who need to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-118">When you select an access review from the list, you see the names of users who need to be reviewed.</span></span> <span data-ttu-id="ef2b6-119">You might see only one name--your own--if the request was to review your own access.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-119">You might see only one name--your own--if the request was to review your own access.</span></span>

<span data-ttu-id="ef2b6-120">For each row on the list, you can decide whether to approve or deny the user's access.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-120">For each row on the list, you can decide whether to approve or deny the user's access.</span></span> <span data-ttu-id="ef2b6-121">Select the row, and choose whether to approve or deny.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-121">Select the row, and choose whether to approve or deny.</span></span> <span data-ttu-id="ef2b6-122">(If you don't know the user, you can indicate that too.)</span><span class="sxs-lookup"><span data-stu-id="ef2b6-122">(If you don't know the user, you can indicate that too.)</span></span>

<span data-ttu-id="ef2b6-123">The reviewer might require that you supply a justification for approving continued access or group membership.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-123">The reviewer might require that you supply a justification for approving continued access or group membership.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef2b6-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef2b6-124">Next steps</span></span>

<span data-ttu-id="ef2b6-125">A user's denied access isn't removed immediately.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-125">A user's denied access isn't removed immediately.</span></span> <span data-ttu-id="ef2b6-126">It can be removed when the review is finished or when an administrator stops the review.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-126">It can be removed when the review is finished or when an administrator stops the review.</span></span> <span data-ttu-id="ef2b6-127">If you want to change your answer and approve a previously denied user or deny a previously approved user, select the row, reset the response, and select a new response.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-127">If you want to change your answer and approve a previously denied user or deny a previously approved user, select the row, reset the response, and select a new response.</span></span> <span data-ttu-id="ef2b6-128">You can do this step until the access review is finished.</span><span class="sxs-lookup"><span data-stu-id="ef2b6-128">You can do this step until the access review is finished.</span></span>



