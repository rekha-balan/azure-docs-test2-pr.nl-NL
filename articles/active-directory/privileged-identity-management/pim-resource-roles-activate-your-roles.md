---
title: Activate my Azure resource roles in PIM | Microsoft Docs
description: Learn how to activate your Azure resource roles in Azure AD Privileged Identity Management (PIM).
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
ms.openlocfilehash: 59bce2c61db5838bb21a29757d4e354311ecffd5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856372"
---
# <a name="activate-my-azure-resource-roles-in-pim"></a><span data-ttu-id="c9179-103">Activate my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="c9179-103">Activate my Azure resource roles in PIM</span></span>

<span data-ttu-id="c9179-104">Using Azure AD Privileged Identity Management (PIM), eligible role members for Azure resources can schedule activation for a future date and time.</span><span class="sxs-lookup"><span data-stu-id="c9179-104">Using Azure AD Privileged Identity Management (PIM), eligible role members for Azure resources can schedule activation for a future date and time.</span></span> <span data-ttu-id="c9179-105">They can also select a specific activation duration within the maximum (configured by administrators).</span><span class="sxs-lookup"><span data-stu-id="c9179-105">They can also select a specific activation duration within the maximum (configured by administrators).</span></span>

<span data-ttu-id="c9179-106">This article is for members who need to activate their Azure resource role in PIM.</span><span class="sxs-lookup"><span data-stu-id="c9179-106">This article is for members who need to activate their Azure resource role in PIM.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="c9179-107">Activate a role</span><span class="sxs-lookup"><span data-stu-id="c9179-107">Activate a role</span></span>

<span data-ttu-id="c9179-108">When you need to take on an Azure resource role, you can request activation by using the **My roles** navigation option in PIM.</span><span class="sxs-lookup"><span data-stu-id="c9179-108">When you need to take on an Azure resource role, you can request activation by using the **My roles** navigation option in PIM.</span></span>

1. <span data-ttu-id="c9179-109">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c9179-109">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="c9179-110">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="c9179-110">Open **Azure AD Privileged Identity Management**.</span></span> <span data-ttu-id="c9179-111">For information about how to add the PIM tile to your dashboard, see [Start using PIM](pim-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9179-111">For information about how to add the PIM tile to your dashboard, see [Start using PIM](pim-getting-started.md).</span></span>

1. <span data-ttu-id="c9179-112">Click **My roles** to see a list of your eligible Azure AD directory roles and Azure resource roles.</span><span class="sxs-lookup"><span data-stu-id="c9179-112">Click **My roles** to see a list of your eligible Azure AD directory roles and Azure resource roles.</span></span>

    ![Azure AD directory roles and Azure resource roles - My roles](./media/pim-resource-roles-activate-your-roles/resources-my-roles.png)

1. <span data-ttu-id="c9179-114">In the **Azure resource roles** list, find the role you want to activate.</span><span class="sxs-lookup"><span data-stu-id="c9179-114">In the **Azure resource roles** list, find the role you want to activate.</span></span>

    ![Azure resource roles - My roles list](./media/pim-resource-roles-activate-your-roles/resources-my-roles-activate.png)

1. <span data-ttu-id="c9179-116">Click **Activate** to open the Activate pane.</span><span class="sxs-lookup"><span data-stu-id="c9179-116">Click **Activate** to open the Activate pane.</span></span>

1. <span data-ttu-id="c9179-117">If your role requires multi-factor authentication (MFA), click **Verify your identity before proceeding**.</span><span class="sxs-lookup"><span data-stu-id="c9179-117">If your role requires multi-factor authentication (MFA), click **Verify your identity before proceeding**.</span></span> <span data-ttu-id="c9179-118">You only have to authenticate once per session.</span><span class="sxs-lookup"><span data-stu-id="c9179-118">You only have to authenticate once per session.</span></span>

    ![Verify with MFA before role activation](./media/pim-resource-roles-activate-your-roles/resources-my-roles-mfa.png)

1. <span data-ttu-id="c9179-120">Click **Verify my identity** and follow the instructions to provide additional security verification.</span><span class="sxs-lookup"><span data-stu-id="c9179-120">Click **Verify my identity** and follow the instructions to provide additional security verification.</span></span>

    ![Additional security verification](./media/pim-resource-roles-activate-your-roles/resources-mfa-enter-code.png)

1. <span data-ttu-id="c9179-122">If you want to specify a reduced scope, click **Scope** to open the Resource filter pane.</span><span class="sxs-lookup"><span data-stu-id="c9179-122">If you want to specify a reduced scope, click **Scope** to open the Resource filter pane.</span></span>

    <span data-ttu-id="c9179-123">It's a best practice to only request access to the resources you need.</span><span class="sxs-lookup"><span data-stu-id="c9179-123">It's a best practice to only request access to the resources you need.</span></span> <span data-ttu-id="c9179-124">On the Resource filter pane, you can specify the resource groups or resources that you need access to.</span><span class="sxs-lookup"><span data-stu-id="c9179-124">On the Resource filter pane, you can specify the resource groups or resources that you need access to.</span></span>

    ![Activate - Resource filter](./media/pim-resource-roles-activate-your-roles/resources-my-roles-resource-filter.png)

1. <span data-ttu-id="c9179-126">If necessary, specify a custom activation start time.</span><span class="sxs-lookup"><span data-stu-id="c9179-126">If necessary, specify a custom activation start time.</span></span> <span data-ttu-id="c9179-127">The member would be activated after the selected time.</span><span class="sxs-lookup"><span data-stu-id="c9179-127">The member would be activated after the selected time.</span></span>

1. <span data-ttu-id="c9179-128">In the **Reason** box, enter the reason for the activation request.</span><span class="sxs-lookup"><span data-stu-id="c9179-128">In the **Reason** box, enter the reason for the activation request.</span></span>

    ![Completed Activate pane](./media/pim-resource-roles-activate-your-roles/resources-my-roles-activate-done.png)

1. <span data-ttu-id="c9179-130">Click **Activate**.</span><span class="sxs-lookup"><span data-stu-id="c9179-130">Click **Activate**.</span></span>

    <span data-ttu-id="c9179-131">If the role does not require approval, it is now activated, and the role appears in the list of active roles.</span><span class="sxs-lookup"><span data-stu-id="c9179-131">If the role does not require approval, it is now activated, and the role appears in the list of active roles.</span></span> <span data-ttu-id="c9179-132">If the [role requires approval](pim-resource-roles-approval-workflow.md) to activate, a notification will appear in the upper right corner of your browser informing you the request is pending approval.</span><span class="sxs-lookup"><span data-stu-id="c9179-132">If the [role requires approval](pim-resource-roles-approval-workflow.md) to activate, a notification will appear in the upper right corner of your browser informing you the request is pending approval.</span></span>

    ![Request pending notification](./media/pim-resource-roles-activate-your-roles/resources-my-roles-activate-notification.png)

## <a name="view-the-status-of-your-requests"></a><span data-ttu-id="c9179-134">View the status of your requests</span><span class="sxs-lookup"><span data-stu-id="c9179-134">View the status of your requests</span></span>

<span data-ttu-id="c9179-135">You can view the status of your pending requests to activate.</span><span class="sxs-lookup"><span data-stu-id="c9179-135">You can view the status of your pending requests to activate.</span></span>

1. <span data-ttu-id="c9179-136">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="c9179-136">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="c9179-137">Click **My requests** to see a list of your Azure AD directory role and Azure resource role requests.</span><span class="sxs-lookup"><span data-stu-id="c9179-137">Click **My requests** to see a list of your Azure AD directory role and Azure resource role requests.</span></span>

    ![Azure AD directory roles and Azure resource roles - My requests](./media/pim-resource-roles-activate-your-roles/resources-my-requests.png)

1. <span data-ttu-id="c9179-139">Scroll to the right to view the **Request Status** column.</span><span class="sxs-lookup"><span data-stu-id="c9179-139">Scroll to the right to view the **Request Status** column.</span></span>

## <a name="use-a-role-immediately-after-activation"></a><span data-ttu-id="c9179-140">Use a role immediately after activation</span><span class="sxs-lookup"><span data-stu-id="c9179-140">Use a role immediately after activation</span></span>

<span data-ttu-id="c9179-141">Because of caching, activations do not occur immediately in the Azure portal without a refresh.</span><span class="sxs-lookup"><span data-stu-id="c9179-141">Because of caching, activations do not occur immediately in the Azure portal without a refresh.</span></span> <span data-ttu-id="c9179-142">If you need to reduce the possibility of delays after activating a role, you can use the **Application access** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="c9179-142">If you need to reduce the possibility of delays after activating a role, you can use the **Application access** page in the portal.</span></span> <span data-ttu-id="c9179-143">Applications accessed from this page check for new role assignments immediately.</span><span class="sxs-lookup"><span data-stu-id="c9179-143">Applications accessed from this page check for new role assignments immediately.</span></span>

1. <span data-ttu-id="c9179-144">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="c9179-144">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="c9179-145">Click the **Application access** page.</span><span class="sxs-lookup"><span data-stu-id="c9179-145">Click the **Application access** page.</span></span>

    ![PIM Application access - screenshot](./media/pim-resource-roles-activate-your-roles/pim-application-access.png)

1. <span data-ttu-id="c9179-147">Click **Azure resources** to reopen the portal on the **All resources** page.</span><span class="sxs-lookup"><span data-stu-id="c9179-147">Click **Azure resources** to reopen the portal on the **All resources** page.</span></span>

    <span data-ttu-id="c9179-148">When you click this link, you force a refresh and there is a check for new Azure resource role assignments.</span><span class="sxs-lookup"><span data-stu-id="c9179-148">When you click this link, you force a refresh and there is a check for new Azure resource role assignments.</span></span>

## <a name="cancel-a-pending-request"></a><span data-ttu-id="c9179-149">Cancel a pending request</span><span class="sxs-lookup"><span data-stu-id="c9179-149">Cancel a pending request</span></span>

<span data-ttu-id="c9179-150">If you do not require activation of a role that requires approval, you can cancel a pending request at any time.</span><span class="sxs-lookup"><span data-stu-id="c9179-150">If you do not require activation of a role that requires approval, you can cancel a pending request at any time.</span></span>

1. <span data-ttu-id="c9179-151">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="c9179-151">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="c9179-152">Click **My requests**.</span><span class="sxs-lookup"><span data-stu-id="c9179-152">Click **My requests**.</span></span>

1. <span data-ttu-id="c9179-153">For the role that you want to cancel, click the **Cancel** link.</span><span class="sxs-lookup"><span data-stu-id="c9179-153">For the role that you want to cancel, click the **Cancel** link.</span></span>

    <span data-ttu-id="c9179-154">When you click Cancel, the request will be cancelled.</span><span class="sxs-lookup"><span data-stu-id="c9179-154">When you click Cancel, the request will be cancelled.</span></span> <span data-ttu-id="c9179-155">To activate the role again, you will have to submit a new request for activation.</span><span class="sxs-lookup"><span data-stu-id="c9179-155">To activate the role again, you will have to submit a new request for activation.</span></span>

   ![Cancel pending request](./media/pim-resource-roles-activate-your-roles/resources-my-requests-cancel.png)

## <a name="next-steps"></a><span data-ttu-id="c9179-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9179-157">Next steps</span></span>

- [<span data-ttu-id="c9179-158">Extend or renew Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="c9179-158">Extend or renew Azure resource roles in PIM</span></span>](pim-resource-roles-renew-extend.md)
- [<span data-ttu-id="c9179-159">Activate my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="c9179-159">Activate my Azure AD directory roles in PIM</span></span>](pim-how-to-activate-role.md)