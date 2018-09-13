---
title: Perform an access review of my Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to perform an access review of your Azure AD directory roles in Azure AD Privileged Identity Management (PIM).
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
ms.openlocfilehash: b4cffbd1ce240e4792fba84581dafb1933c71a62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864482"
---
# <a name="perform-an-access-review-of-my-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="11f2a-103">Perform an access review of my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="11f2a-103">Perform an access review of my Azure AD directory roles in PIM</span></span>
<span data-ttu-id="11f2a-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="11f2a-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="11f2a-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span><span class="sxs-lookup"><span data-stu-id="11f2a-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="11f2a-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11f2a-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="11f2a-107">Follow the steps in this article to perform a self-review of your assigned roles.</span><span class="sxs-lookup"><span data-stu-id="11f2a-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="11f2a-108">If you're a privileged role administrator or global administrator interested in access reviews, get more details at [How to start an access review](pim-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="11f2a-108">If you're a privileged role administrator or global administrator interested in access reviews, get more details at [How to start an access review](pim-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="11f2a-109">Add the Privileged Identity Management application</span><span class="sxs-lookup"><span data-stu-id="11f2a-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="11f2a-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span><span class="sxs-lookup"><span data-stu-id="11f2a-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="11f2a-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span><span class="sxs-lookup"><span data-stu-id="11f2a-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="11f2a-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="11f2a-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="11f2a-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span><span class="sxs-lookup"><span data-stu-id="11f2a-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="11f2a-114">Select **All services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="11f2a-114">Select **All services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="11f2a-115">Check **Pin to dashboard** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="11f2a-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="11f2a-116">The Privileged Identity Management application will open.</span><span class="sxs-lookup"><span data-stu-id="11f2a-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="11f2a-117">Approve or deny access</span><span class="sxs-lookup"><span data-stu-id="11f2a-117">Approve or deny access</span></span>
<span data-ttu-id="11f2a-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span><span class="sxs-lookup"><span data-stu-id="11f2a-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="11f2a-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span><span class="sxs-lookup"><span data-stu-id="11f2a-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="11f2a-120">Your status won't change right away, until the reviewer applies the results.</span><span class="sxs-lookup"><span data-stu-id="11f2a-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="11f2a-121">Follow these steps to find and complete the access review:</span><span class="sxs-lookup"><span data-stu-id="11f2a-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="11f2a-122">In the PIM application, select **Review privileged access**.</span><span class="sxs-lookup"><span data-stu-id="11f2a-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="11f2a-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span><span class="sxs-lookup"><span data-stu-id="11f2a-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="11f2a-124">Select the review you want to complete.</span><span class="sxs-lookup"><span data-stu-id="11f2a-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="11f2a-125">Unless you created the review, you appear as the only user in the review.</span><span class="sxs-lookup"><span data-stu-id="11f2a-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="11f2a-126">Select the check mark next to your name.</span><span class="sxs-lookup"><span data-stu-id="11f2a-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="11f2a-127">Choose either **Approve** or **Deny**.</span><span class="sxs-lookup"><span data-stu-id="11f2a-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="11f2a-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span><span class="sxs-lookup"><span data-stu-id="11f2a-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="11f2a-129">Close the **Review Azure AD roles** blade.</span><span class="sxs-lookup"><span data-stu-id="11f2a-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="11f2a-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="11f2a-130">Next steps</span></span>

- [<span data-ttu-id="11f2a-131">Perform an access review of my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="11f2a-131">Perform an access review of my Azure resource roles in PIM</span></span>](pim-resource-roles-perform-access-review.md)