---
title: Perform an access review of my Azure resource roles in PIM | Microsoft Docs
description: Learn how to perform an access review of your Azure resource roles in Azure AD Privileged Identity Management (PIM).
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
ms.component: pim
ms.date: 03/30/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: a96a1de7828797f1124280fca95a3358210b55b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870307"
---
# <a name="perform-an-access-review-of-my-azure-resource-roles-in-pim"></a><span data-ttu-id="4ce1e-103">Perform an access review of my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="4ce1e-103">Perform an access review of my Azure resource roles in PIM</span></span>
<span data-ttu-id="4ce1e-104">Privileged Identity Management (PIM) for Azure resources simplifies how enterprises manage privileged access to resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-104">Privileged Identity Management (PIM) for Azure resources simplifies how enterprises manage privileged access to resources in Azure.</span></span> 

<span data-ttu-id="4ce1e-105">If you are assigned to an administrative role, your organization's privileged role administrator might ask you to regularly confirm that you still need that role for your job.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-105">If you are assigned to an administrative role, your organization's privileged role administrator might ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="4ce1e-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ce1e-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4ce1e-107">Follow the steps in this article to perform a self-review of your assigned roles.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="4ce1e-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](pim-resource-roles-start-access-review.md).</span><span class="sxs-lookup"><span data-stu-id="4ce1e-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](pim-resource-roles-start-access-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="4ce1e-109">Add the Privileged Identity Management application</span><span class="sxs-lookup"><span data-stu-id="4ce1e-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="4ce1e-110">You can use the Azure Active Directory (Azure AD) PIM application in the [Azure portal](https://portal.azure.com/) to perform your review.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-110">You can use the Azure Active Directory (Azure AD) PIM application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span> <span data-ttu-id="4ce1e-111">If you don't have the application in your portal, follow these steps to get started.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-111">If you don't have the application in your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="4ce1e-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4ce1e-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4ce1e-113">Select your user name in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-113">Select your user name in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="4ce1e-114">Select **All services**, and use the **Filter** box to search for *Azure AD Privileged Identity Management*.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-114">Select **All services**, and use the **Filter** box to search for *Azure AD Privileged Identity Management*.</span></span>
4. <span data-ttu-id="4ce1e-115">Check **Pin to dashboard**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-115">Check **Pin to dashboard**, and then select **Create**.</span></span> <span data-ttu-id="4ce1e-116">The PIM application opens.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-116">The PIM application opens.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="4ce1e-117">Approve or deny access</span><span class="sxs-lookup"><span data-stu-id="4ce1e-117">Approve or deny access</span></span>
<span data-ttu-id="4ce1e-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="4ce1e-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="4ce1e-120">Your status changes only when the reviewer applies the results.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-120">Your status changes only when the reviewer applies the results.</span></span>

<span data-ttu-id="4ce1e-121">Follow these steps to find and complete the access review:</span><span class="sxs-lookup"><span data-stu-id="4ce1e-121">Follow these steps to find and complete the access review:</span></span>
1. <span data-ttu-id="4ce1e-122">Browse to the Azure AD PIM application.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-122">Browse to the Azure AD PIM application.</span></span>
2. <span data-ttu-id="4ce1e-123">Select the **Review access** blade.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-123">Select the **Review access** blade.</span></span>

   ![Screenshot of PIM application, with Review access blade selected](media/azure-pim-resource-rbac/rbac-access-review-complete.png)

3. <span data-ttu-id="4ce1e-125">Select the review you want to complete.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-125">Select the review you want to complete.</span></span> 
4. <span data-ttu-id="4ce1e-126">Choose either **Approve** or **Deny**.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-126">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="4ce1e-127">In the **Provide a reason box**, you might need to include a reason for your decision.</span><span class="sxs-lookup"><span data-stu-id="4ce1e-127">In the **Provide a reason box**, you might need to include a reason for your decision.</span></span>

   ![Screenshot of Review details page](media/azure-pim-resource-rbac/rbac-access-review-choice.png)

## <a name="next-steps"></a><span data-ttu-id="4ce1e-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ce1e-129">Next steps</span></span>

- [<span data-ttu-id="4ce1e-130">Perform an access review of my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="4ce1e-130">Perform an access review of my Azure AD directory roles in PIM</span></span>](pim-how-to-perform-security-review.md)