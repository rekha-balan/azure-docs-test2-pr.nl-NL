---
title: Approve or deny requests for Azure resource roles in PIM | Microsoft Docs
description: Learn how to approve or deny requests for Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 08/31/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: c661f2662f48c5aaece142cb4a2223ab8a6d0853
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867570"
---
# <a name="approve-or-deny-requests-for-azure-resource-roles-in-pim"></a><span data-ttu-id="bf771-103">Approve or deny requests for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="bf771-103">Approve or deny requests for Azure resource roles in PIM</span></span>

<span data-ttu-id="bf771-104">With Azure AD Privileged Identity Management (PIM), you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span><span class="sxs-lookup"><span data-stu-id="bf771-104">With Azure AD Privileged Identity Management (PIM), you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="bf771-105">Follow the steps in this article to approve or deny requests for Azure resource roles.</span><span class="sxs-lookup"><span data-stu-id="bf771-105">Follow the steps in this article to approve or deny requests for Azure resource roles.</span></span>

## <a name="view-pending-requests"></a><span data-ttu-id="bf771-106">View pending requests</span><span class="sxs-lookup"><span data-stu-id="bf771-106">View pending requests</span></span>

<span data-ttu-id="bf771-107">As a delegated approver, you'll receive an email notification when an Azure resource role request is pending your approval.</span><span class="sxs-lookup"><span data-stu-id="bf771-107">As a delegated approver, you'll receive an email notification when an Azure resource role request is pending your approval.</span></span> <span data-ttu-id="bf771-108">You can view these pending requests in PIM.</span><span class="sxs-lookup"><span data-stu-id="bf771-108">You can view these pending requests in PIM.</span></span>

1. <span data-ttu-id="bf771-109">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf771-109">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="bf771-110">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="bf771-110">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="bf771-111">Click **Approve requests**.</span><span class="sxs-lookup"><span data-stu-id="bf771-111">Click **Approve requests**.</span></span>

    ![Azure resources - Approve requests](./media/pim-resource-roles-approval-workflow/resources-approve-requests.png)

    <span data-ttu-id="bf771-113">In the **Requests for role activations** section, you'll see a list of requests pending your approval.</span><span class="sxs-lookup"><span data-stu-id="bf771-113">In the **Requests for role activations** section, you'll see a list of requests pending your approval.</span></span>

## <a name="approve-requests"></a><span data-ttu-id="bf771-114">Approve requests</span><span class="sxs-lookup"><span data-stu-id="bf771-114">Approve requests</span></span>

1. <span data-ttu-id="bf771-115">Find and click the request that you want to approve.</span><span class="sxs-lookup"><span data-stu-id="bf771-115">Find and click the request that you want to approve.</span></span> <span data-ttu-id="bf771-116">An approval pane appears.</span><span class="sxs-lookup"><span data-stu-id="bf771-116">An approval pane appears.</span></span>

    ![Approve requests pane](./media/pim-resource-roles-approval-workflow/resources-approve-pane.png)

1. <span data-ttu-id="bf771-118">In the **Justification** box, type a reason.</span><span class="sxs-lookup"><span data-stu-id="bf771-118">In the **Justification** box, type a reason.</span></span>

1. <span data-ttu-id="bf771-119">Click **Approve**.</span><span class="sxs-lookup"><span data-stu-id="bf771-119">Click **Approve**.</span></span>

    <span data-ttu-id="bf771-120">A notification appears with your approval.</span><span class="sxs-lookup"><span data-stu-id="bf771-120">A notification appears with your approval.</span></span>

    ![Approve notification](./media/pim-resource-roles-approval-workflow/resources-approve-notification.png)

## <a name="deny-requests"></a><span data-ttu-id="bf771-122">Deny requests</span><span class="sxs-lookup"><span data-stu-id="bf771-122">Deny requests</span></span>

1. <span data-ttu-id="bf771-123">Find and click the request that you want to deny.</span><span class="sxs-lookup"><span data-stu-id="bf771-123">Find and click the request that you want to deny.</span></span> <span data-ttu-id="bf771-124">An approval pane appears.</span><span class="sxs-lookup"><span data-stu-id="bf771-124">An approval pane appears.</span></span>

    ![Approve requests pane](./media/pim-resource-roles-approval-workflow/resources-approve-pane.png)

1. <span data-ttu-id="bf771-126">In the **Justification** box, type a reason.</span><span class="sxs-lookup"><span data-stu-id="bf771-126">In the **Justification** box, type a reason.</span></span>

1. <span data-ttu-id="bf771-127">Click **Deny**.</span><span class="sxs-lookup"><span data-stu-id="bf771-127">Click **Deny**.</span></span>

    <span data-ttu-id="bf771-128">A notification appears with your denial.</span><span class="sxs-lookup"><span data-stu-id="bf771-128">A notification appears with your denial.</span></span>

## <a name="workflow-notifications"></a><span data-ttu-id="bf771-129">Workflow notifications</span><span class="sxs-lookup"><span data-stu-id="bf771-129">Workflow notifications</span></span>

<span data-ttu-id="bf771-130">Here's some information about workflow notifications:</span><span class="sxs-lookup"><span data-stu-id="bf771-130">Here's some information about workflow notifications:</span></span>

- <span data-ttu-id="bf771-131">All members of the approver list are notified by email when a request for a role is pending their review.</span><span class="sxs-lookup"><span data-stu-id="bf771-131">All members of the approver list are notified by email when a request for a role is pending their review.</span></span> <span data-ttu-id="bf771-132">Email notifications include a direct link to the request, where the approver can approve or deny.</span><span class="sxs-lookup"><span data-stu-id="bf771-132">Email notifications include a direct link to the request, where the approver can approve or deny.</span></span>
- <span data-ttu-id="bf771-133">Requests are resolved by the first member of the list who approves or denies.</span><span class="sxs-lookup"><span data-stu-id="bf771-133">Requests are resolved by the first member of the list who approves or denies.</span></span>
- <span data-ttu-id="bf771-134">When an approver responds to the request, all members of the approver list are notified of the action.</span><span class="sxs-lookup"><span data-stu-id="bf771-134">When an approver responds to the request, all members of the approver list are notified of the action.</span></span>
- <span data-ttu-id="bf771-135">Resource administrators are notified when an approved member becomes active in their role.</span><span class="sxs-lookup"><span data-stu-id="bf771-135">Resource administrators are notified when an approved member becomes active in their role.</span></span>

>[!Note]
><span data-ttu-id="bf771-136">A resource administrator who believes that an approved member should not be active can remove the active role assignment in PIM.</span><span class="sxs-lookup"><span data-stu-id="bf771-136">A resource administrator who believes that an approved member should not be active can remove the active role assignment in PIM.</span></span> <span data-ttu-id="bf771-137">Although resource administrators are not notified of pending requests unless they are members of the approver list, they can view and cancel pending requests of all users by viewing pending requests in PIM.</span><span class="sxs-lookup"><span data-stu-id="bf771-137">Although resource administrators are not notified of pending requests unless they are members of the approver list, they can view and cancel pending requests of all users by viewing pending requests in PIM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bf771-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf771-138">Next steps</span></span>

- [<span data-ttu-id="bf771-139">Extend or renew Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="bf771-139">Extend or renew Azure resource roles in PIM</span></span>](pim-resource-roles-renew-extend.md)
- [<span data-ttu-id="bf771-140">Email notifications in PIM</span><span class="sxs-lookup"><span data-stu-id="bf771-140">Email notifications in PIM</span></span>](pim-email-notifications.md)
- [<span data-ttu-id="bf771-141">Approve or deny requests for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="bf771-141">Approve or deny requests for Azure AD directory roles in PIM</span></span>](azure-ad-pim-approval-workflow.md)
