---
title: Approve or deny requests for Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to approve or deny requests for Azure AD directory roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 08/29/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 9402824540f965cb89aa00791d093bd87712a89a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869770"
---
# <a name="approve-or-deny-requests-for-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="84bc5-103">Approve or deny requests for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="84bc5-103">Approve or deny requests for Azure AD directory roles in PIM</span></span>

<span data-ttu-id="84bc5-104">With Azure AD Privileged Identity Management (PIM), you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span><span class="sxs-lookup"><span data-stu-id="84bc5-104">With Azure AD Privileged Identity Management (PIM), you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="84bc5-105">Follow the steps in this article to approve or deny requests for Azure AD directory roles.</span><span class="sxs-lookup"><span data-stu-id="84bc5-105">Follow the steps in this article to approve or deny requests for Azure AD directory roles.</span></span>

## <a name="view-pending-requests"></a><span data-ttu-id="84bc5-106">View pending requests</span><span class="sxs-lookup"><span data-stu-id="84bc5-106">View pending requests</span></span>

<span data-ttu-id="84bc5-107">As a delegated approver, you'll receive an email notification when an Azure AD directory role request is pending your approval.</span><span class="sxs-lookup"><span data-stu-id="84bc5-107">As a delegated approver, you'll receive an email notification when an Azure AD directory role request is pending your approval.</span></span> <span data-ttu-id="84bc5-108">You can view these pending requests in PIM.</span><span class="sxs-lookup"><span data-stu-id="84bc5-108">You can view these pending requests in PIM.</span></span>

1. <span data-ttu-id="84bc5-109">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="84bc5-109">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="84bc5-110">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="84bc5-110">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="84bc5-111">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="84bc5-111">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="84bc5-112">Click **Approve requests**.</span><span class="sxs-lookup"><span data-stu-id="84bc5-112">Click **Approve requests**.</span></span>

    ![PIM Azure AD directory roles - Roles](./media/azure-ad-pim-approval-workflow/pim-directory-roles-approve-requests.png)

    <span data-ttu-id="84bc5-114">You'll see a list of requests pending your approval.</span><span class="sxs-lookup"><span data-stu-id="84bc5-114">You'll see a list of requests pending your approval.</span></span>

## <a name="approve-requests"></a><span data-ttu-id="84bc5-115">Approve requests</span><span class="sxs-lookup"><span data-stu-id="84bc5-115">Approve requests</span></span>

1. <span data-ttu-id="84bc5-116">Select the requests you want to approve and then click **Approve** to open the Approve selected requests pane.</span><span class="sxs-lookup"><span data-stu-id="84bc5-116">Select the requests you want to approve and then click **Approve** to open the Approve selected requests pane.</span></span>

    ![PIM Approve requests list](./media/azure-ad-pim-approval-workflow/pim-approve-requests-list.png)

1. <span data-ttu-id="84bc5-118">In the **Approve reason** box, type a reason.</span><span class="sxs-lookup"><span data-stu-id="84bc5-118">In the **Approve reason** box, type a reason.</span></span>

    ![PIM Approve selected requests](./media/azure-ad-pim-approval-workflow/pim-approve-selected-requests.png)

1. <span data-ttu-id="84bc5-120">Click **Approve**.</span><span class="sxs-lookup"><span data-stu-id="84bc5-120">Click **Approve**.</span></span>

    <span data-ttu-id="84bc5-121">The Status symbol will be updated with your approval.</span><span class="sxs-lookup"><span data-stu-id="84bc5-121">The Status symbol will be updated with your approval.</span></span>

    ![PIM Approve selected requests](./media/azure-ad-pim-approval-workflow/pim-approve-status.png)

## <a name="deny-requests"></a><span data-ttu-id="84bc5-123">Deny requests</span><span class="sxs-lookup"><span data-stu-id="84bc5-123">Deny requests</span></span>

1. <span data-ttu-id="84bc5-124">Select the requests you want to deny and then click **Deny** to open the Deny selected requests pane.</span><span class="sxs-lookup"><span data-stu-id="84bc5-124">Select the requests you want to deny and then click **Deny** to open the Deny selected requests pane.</span></span>

    ![PIM Approve requests list](./media/azure-ad-pim-approval-workflow/pim-deny-requests-list.png)

1. <span data-ttu-id="84bc5-126">In the **Deny reason** box, type a reason.</span><span class="sxs-lookup"><span data-stu-id="84bc5-126">In the **Deny reason** box, type a reason.</span></span>

    ![PIM Deny selected requests](./media/azure-ad-pim-approval-workflow/pim-deny-selected-requests.png)

1. <span data-ttu-id="84bc5-128">Click **Deny**.</span><span class="sxs-lookup"><span data-stu-id="84bc5-128">Click **Deny**.</span></span>

    <span data-ttu-id="84bc5-129">The Status symbol will be updated with your denial.</span><span class="sxs-lookup"><span data-stu-id="84bc5-129">The Status symbol will be updated with your denial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84bc5-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="84bc5-130">Next steps</span></span>

- [<span data-ttu-id="84bc5-131">Email notifications in PIM</span><span class="sxs-lookup"><span data-stu-id="84bc5-131">Email notifications in PIM</span></span>](pim-email-notifications.md)
- [<span data-ttu-id="84bc5-132">Approve or deny requests for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="84bc5-132">Approve or deny requests for Azure resource roles in PIM</span></span>](pim-resource-roles-approval-workflow.md)
