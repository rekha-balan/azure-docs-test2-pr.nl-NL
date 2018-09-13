---
title: Manage user access with Azure AD access reviews| Microsoft Docs
description: Learn how to manage users' access as membership of a group or assignment to an application with Azure Active Directory access reviews
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
ms.date: 06/21/2018
ms.author: rolyon
ms.reviewer: mwahl
ms.openlocfilehash: 7b4d3baac791012e18e65c9e2e42272410e73fc1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867665"
---
# <a name="manage-user-access-with-azure-ad-access-reviews"></a><span data-ttu-id="aca84-103">Manage user access with Azure AD access reviews</span><span class="sxs-lookup"><span data-stu-id="aca84-103">Manage user access with Azure AD access reviews</span></span>

<span data-ttu-id="aca84-104">With Azure Active Directory (Azure AD), you can easily ensure that users have appropriate access.</span><span class="sxs-lookup"><span data-stu-id="aca84-104">With Azure Active Directory (Azure AD), you can easily ensure that users have appropriate access.</span></span> <span data-ttu-id="aca84-105">You can ask the users themselves or a decision maker to participate in an access review and recertify (or attest) to users' access.</span><span class="sxs-lookup"><span data-stu-id="aca84-105">You can ask the users themselves or a decision maker to participate in an access review and recertify (or attest) to users' access.</span></span> <span data-ttu-id="aca84-106">The reviewers can give their input on each user's need for continued access based on suggestions from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aca84-106">The reviewers can give their input on each user's need for continued access based on suggestions from Azure AD.</span></span> <span data-ttu-id="aca84-107">When an access review is finished, you can then make changes and remove access from users who no longer need it.</span><span class="sxs-lookup"><span data-stu-id="aca84-107">When an access review is finished, you can then make changes and remove access from users who no longer need it.</span></span>

> [!NOTE]
> <span data-ttu-id="aca84-108">If you want to review only guest users' access and not review all types of users' access, see [Manage guest user access with access reviews](active-directory-azure-ad-controls-manage-guest-access-with-access-reviews.md).</span><span class="sxs-lookup"><span data-stu-id="aca84-108">If you want to review only guest users' access and not review all types of users' access, see [Manage guest user access with access reviews](active-directory-azure-ad-controls-manage-guest-access-with-access-reviews.md).</span></span> <span data-ttu-id="aca84-109">If you want to review users' membership in administrative roles such as global administrator, see [Start an access review in Azure AD Privileged Identity Management](privileged-identity-management/pim-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="aca84-109">If you want to review users' membership in administrative roles such as global administrator, see [Start an access review in Azure AD Privileged Identity Management](privileged-identity-management/pim-how-to-start-security-review.md).</span></span> 
>
>

## <a name="prerequisites"></a><span data-ttu-id="aca84-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aca84-110">Prerequisites</span></span> 


<span data-ttu-id="aca84-111">Access reviews are available with the Premium P2 edition of Azure AD, which is included in Microsoft Enterprise Mobility + Security, E5.</span><span class="sxs-lookup"><span data-stu-id="aca84-111">Access reviews are available with the Premium P2 edition of Azure AD, which is included in Microsoft Enterprise Mobility + Security, E5.</span></span> <span data-ttu-id="aca84-112">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="aca84-112">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span> <span data-ttu-id="aca84-113">Each user who interacts with this feature, including to create a review, fill out a review or confirm their access, requires a license.</span><span class="sxs-lookup"><span data-stu-id="aca84-113">Each user who interacts with this feature, including to create a review, fill out a review or confirm their access, requires a license.</span></span> 

## <a name="create-and-perform-an-access-review"></a><span data-ttu-id="aca84-114">Create and perform an access review</span><span class="sxs-lookup"><span data-stu-id="aca84-114">Create and perform an access review</span></span>

<span data-ttu-id="aca84-115">You can have one or more users as reviewers in an access review.</span><span class="sxs-lookup"><span data-stu-id="aca84-115">You can have one or more users as reviewers in an access review.</span></span>  

1. <span data-ttu-id="aca84-116">Select a group in Azure AD that has one or more members.</span><span class="sxs-lookup"><span data-stu-id="aca84-116">Select a group in Azure AD that has one or more members.</span></span> <span data-ttu-id="aca84-117">Or select an application connected to Azure AD that has one or more users assigned to it.</span><span class="sxs-lookup"><span data-stu-id="aca84-117">Or select an application connected to Azure AD that has one or more users assigned to it.</span></span> 

2. <span data-ttu-id="aca84-118">Decide whether to have each user review their own access or to have one or more users review everyone's access.</span><span class="sxs-lookup"><span data-stu-id="aca84-118">Decide whether to have each user review their own access or to have one or more users review everyone's access.</span></span>

3. <span data-ttu-id="aca84-119">Enable access reviews to appear on the reviewers' access panels.</span><span class="sxs-lookup"><span data-stu-id="aca84-119">Enable access reviews to appear on the reviewers' access panels.</span></span> <span data-ttu-id="aca84-120">As a global administrator or user account administrator, go to the [access reviews page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/).</span><span class="sxs-lookup"><span data-stu-id="aca84-120">As a global administrator or user account administrator, go to the [access reviews page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/).</span></span>

4. <span data-ttu-id="aca84-121">Start the access review.</span><span class="sxs-lookup"><span data-stu-id="aca84-121">Start the access review.</span></span> <span data-ttu-id="aca84-122">For more information, see [Create an access review](active-directory-azure-ad-controls-create-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="aca84-122">For more information, see [Create an access review](active-directory-azure-ad-controls-create-access-review.md).</span></span>

5. <span data-ttu-id="aca84-123">Ask the reviewers to give input.</span><span class="sxs-lookup"><span data-stu-id="aca84-123">Ask the reviewers to give input.</span></span> <span data-ttu-id="aca84-124">By default, they each receive an email from Azure AD with a link to the access panel, where they [perform their access review](active-directory-azure-ad-controls-perform-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="aca84-124">By default, they each receive an email from Azure AD with a link to the access panel, where they [perform their access review](active-directory-azure-ad-controls-perform-access-review.md).</span></span>

6. <span data-ttu-id="aca84-125">If the reviewers haven't given input, you can ask Azure AD to send them a reminder.</span><span class="sxs-lookup"><span data-stu-id="aca84-125">If the reviewers haven't given input, you can ask Azure AD to send them a reminder.</span></span> <span data-ttu-id="aca84-126">By default, Azure AD automatically sends a reminder halfway to the end date to reviewers who haven't yet responded.</span><span class="sxs-lookup"><span data-stu-id="aca84-126">By default, Azure AD automatically sends a reminder halfway to the end date to reviewers who haven't yet responded.</span></span>

7. <span data-ttu-id="aca84-127">After the reviewers give input, stop the access review and apply the changes.</span><span class="sxs-lookup"><span data-stu-id="aca84-127">After the reviewers give input, stop the access review and apply the changes.</span></span> <span data-ttu-id="aca84-128">For more information, see [Complete an access review](active-directory-azure-ad-controls-complete-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="aca84-128">For more information, see [Complete an access review](active-directory-azure-ad-controls-complete-access-review.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="aca84-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="aca84-129">Next steps</span></span>

[<span data-ttu-id="aca84-130">Create an access review for members of a group or access to an application</span><span class="sxs-lookup"><span data-stu-id="aca84-130">Create an access review for members of a group or access to an application</span></span>](active-directory-azure-ad-controls-create-access-review.md)




