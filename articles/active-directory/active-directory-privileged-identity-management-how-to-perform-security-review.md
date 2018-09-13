---
title: How to perform an access review | Microsoft Docs
description: Learn how to perform a review with the Azure Privileged Identity Management application.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 6d38057ad1f960e182c1b83abd8509774d81c1a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552282"
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="c4ed1-103">How to perform an access review in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="c4ed1-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="c4ed1-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="c4ed1-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="c4ed1-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4ed1-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c4ed1-107">Follow the steps in this article to perform a self-review of your assigned roles.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="c4ed1-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="c4ed1-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="c4ed1-109">Add the Privileged Identity Management application</span><span class="sxs-lookup"><span data-stu-id="c4ed1-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="c4ed1-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="c4ed1-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="c4ed1-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4ed1-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4ed1-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="c4ed1-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="c4ed1-115">Check **Pin to dashboard** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="c4ed1-116">The Privileged Identity Management application will open.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="c4ed1-117">Approve or deny access</span><span class="sxs-lookup"><span data-stu-id="c4ed1-117">Approve or deny access</span></span>
<span data-ttu-id="c4ed1-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="c4ed1-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="c4ed1-120">Your status won't change right away, until the reviewer applies the results.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="c4ed1-121">Follow these steps to find and complete the access review:</span><span class="sxs-lookup"><span data-stu-id="c4ed1-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="c4ed1-122">In the PIM application, select **Review privileged access**.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="c4ed1-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="c4ed1-124">Select the review you want to complete.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="c4ed1-125">Unless you created the review, you appear as the only user in the review.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="c4ed1-126">Select the check mark next to your name.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="c4ed1-127">Choose either **Approve** or **Deny**.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="c4ed1-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="c4ed1-129">Close the **Review Azure AD roles** blade.</span><span class="sxs-lookup"><span data-stu-id="c4ed1-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="c4ed1-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4ed1-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png

