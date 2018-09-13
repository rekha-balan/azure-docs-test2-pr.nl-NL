---
title: Activate my Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to activate Azure AD directory roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 08/27/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 59dab4651366c3ad6579e0da660baee0c653d1a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856204"
---
# <a name="activate-my-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="b1669-103">Activate my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="b1669-103">Activate my Azure AD directory roles in PIM</span></span>

<span data-ttu-id="b1669-104">Azure Active Directory (Azure AD) Privileged Identity Management (PIM) simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="b1669-104">Azure Active Directory (Azure AD) Privileged Identity Management (PIM) simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="b1669-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform privileged actions.</span><span class="sxs-lookup"><span data-stu-id="b1669-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform privileged actions.</span></span> <span data-ttu-id="b1669-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span><span class="sxs-lookup"><span data-stu-id="b1669-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span></span> <span data-ttu-id="b1669-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span><span class="sxs-lookup"><span data-stu-id="b1669-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span></span> <span data-ttu-id="b1669-108">You can request to activate that role when you need its privileges, and then you'll have administrator control for a predetermined time period.</span><span class="sxs-lookup"><span data-stu-id="b1669-108">You can request to activate that role when you need its privileges, and then you'll have administrator control for a predetermined time period.</span></span>

<span data-ttu-id="b1669-109">This article is for administrators who need to activate their Azure AD directory role in PIM.</span><span class="sxs-lookup"><span data-stu-id="b1669-109">This article is for administrators who need to activate their Azure AD directory role in PIM.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="b1669-110">Activate a role</span><span class="sxs-lookup"><span data-stu-id="b1669-110">Activate a role</span></span>

<span data-ttu-id="b1669-111">When you need to take on an Azure AD directory role, you can request activation by using the **My roles** navigation option in PIM.</span><span class="sxs-lookup"><span data-stu-id="b1669-111">When you need to take on an Azure AD directory role, you can request activation by using the **My roles** navigation option in PIM.</span></span>

1. <span data-ttu-id="b1669-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b1669-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="b1669-113">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="b1669-113">Open **Azure AD Privileged Identity Management**.</span></span> <span data-ttu-id="b1669-114">For information about how to add the PIM tile to your dashboard, see [Start using PIM](pim-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b1669-114">For information about how to add the PIM tile to your dashboard, see [Start using PIM](pim-getting-started.md).</span></span>

1. <span data-ttu-id="b1669-115">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="b1669-115">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="b1669-116">Click **My roles** to see a list of your eligible Azure AD directory roles.</span><span class="sxs-lookup"><span data-stu-id="b1669-116">Click **My roles** to see a list of your eligible Azure AD directory roles.</span></span>

    ![Azure AD directory roles - My roles](./media/pim-how-to-activate-role/directory-roles-my-roles.png)

1. <span data-ttu-id="b1669-118">Find a role that you want to activate.</span><span class="sxs-lookup"><span data-stu-id="b1669-118">Find a role that you want to activate.</span></span>

    ![Azure AD directory roles - My roles list](./media/pim-how-to-activate-role/directory-roles-my-roles-activate.png)

1. <span data-ttu-id="b1669-120">Click **Activate** to open the Role activation details pane.</span><span class="sxs-lookup"><span data-stu-id="b1669-120">Click **Activate** to open the Role activation details pane.</span></span>

1. <span data-ttu-id="b1669-121">If your role requires multi-factor authentication (MFA), click **Verify your identity before proceeding**.</span><span class="sxs-lookup"><span data-stu-id="b1669-121">If your role requires multi-factor authentication (MFA), click **Verify your identity before proceeding**.</span></span> <span data-ttu-id="b1669-122">You only have to authenticate once per session.</span><span class="sxs-lookup"><span data-stu-id="b1669-122">You only have to authenticate once per session.</span></span>

    ![Verify with MFA before role activation](./media/pim-how-to-activate-role/directory-roles-my-roles-mfa.png)

1. <span data-ttu-id="b1669-124">Click **Verify my identity** and follow the instructions to provide additional security verification.</span><span class="sxs-lookup"><span data-stu-id="b1669-124">Click **Verify my identity** and follow the instructions to provide additional security verification.</span></span>

    ![Additional security verification](./media/pim-how-to-activate-role/additional-security-verification.png)

1. <span data-ttu-id="b1669-126">Click **Activate** to open the Activation pane.</span><span class="sxs-lookup"><span data-stu-id="b1669-126">Click **Activate** to open the Activation pane.</span></span>

    ![Activation pane](./media/pim-how-to-activate-role/directory-roles-activate.png)

1. <span data-ttu-id="b1669-128">If necessary, specify a custom activation start time.</span><span class="sxs-lookup"><span data-stu-id="b1669-128">If necessary, specify a custom activation start time.</span></span>

1. <span data-ttu-id="b1669-129">Specify the activation duration.</span><span class="sxs-lookup"><span data-stu-id="b1669-129">Specify the activation duration.</span></span>

1. <span data-ttu-id="b1669-130">In the **Activation reason** box, enter the reason for the activation request.</span><span class="sxs-lookup"><span data-stu-id="b1669-130">In the **Activation reason** box, enter the reason for the activation request.</span></span> <span data-ttu-id="b1669-131">Some roles require you to supply a trouble ticket number.</span><span class="sxs-lookup"><span data-stu-id="b1669-131">Some roles require you to supply a trouble ticket number.</span></span>

    ![Completed Activation pane](./media/pim-how-to-activate-role/directory-roles-activation-pane.png)

1. <span data-ttu-id="b1669-133">Click **Activate**.</span><span class="sxs-lookup"><span data-stu-id="b1669-133">Click **Activate**.</span></span>

    <span data-ttu-id="b1669-134">If the role does not require approval, it is now activated, and the role appears in the list of active roles.</span><span class="sxs-lookup"><span data-stu-id="b1669-134">If the role does not require approval, it is now activated, and the role appears in the list of active roles.</span></span> <span data-ttu-id="b1669-135">If the [role requires approval](./azure-ad-pim-approval-workflow.md) to activate, a notification will appear in the upper right corner of your browser informing you the request is pending approval.</span><span class="sxs-lookup"><span data-stu-id="b1669-135">If the [role requires approval](./azure-ad-pim-approval-workflow.md) to activate, a notification will appear in the upper right corner of your browser informing you the request is pending approval.</span></span>

    ![Request pending notification](./media/pim-how-to-activate-role/directory-roles-activate-notification.png)

## <a name="view-the-status-of-your-requests"></a><span data-ttu-id="b1669-137">View the status of your requests</span><span class="sxs-lookup"><span data-stu-id="b1669-137">View the status of your requests</span></span>

<span data-ttu-id="b1669-138">You can view the status of your pending requests to activate.</span><span class="sxs-lookup"><span data-stu-id="b1669-138">You can view the status of your pending requests to activate.</span></span>

1. <span data-ttu-id="b1669-139">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="b1669-139">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="b1669-140">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="b1669-140">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="b1669-141">Click **My requests** to see a list of your requests.</span><span class="sxs-lookup"><span data-stu-id="b1669-141">Click **My requests** to see a list of your requests.</span></span>

    ![Azure AD directory roles - My requests](./media/pim-how-to-activate-role/directory-roles-my-requests.png)

## <a name="use-a-role-immediately-after-activation"></a><span data-ttu-id="b1669-143">Use a role immediately after activation</span><span class="sxs-lookup"><span data-stu-id="b1669-143">Use a role immediately after activation</span></span>

<span data-ttu-id="b1669-144">Because of caching, activations do not occur immediately in the Azure portal without a refresh.</span><span class="sxs-lookup"><span data-stu-id="b1669-144">Because of caching, activations do not occur immediately in the Azure portal without a refresh.</span></span> <span data-ttu-id="b1669-145">If you need to reduce the possibility of delays after activating a role, you can use the **Application access** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="b1669-145">If you need to reduce the possibility of delays after activating a role, you can use the **Application access** page in the portal.</span></span> <span data-ttu-id="b1669-146">Applications accessed from this page check for new role assignments immediately.</span><span class="sxs-lookup"><span data-stu-id="b1669-146">Applications accessed from this page check for new role assignments immediately.</span></span>

1. <span data-ttu-id="b1669-147">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="b1669-147">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="b1669-148">Click the **Application access** page.</span><span class="sxs-lookup"><span data-stu-id="b1669-148">Click the **Application access** page.</span></span>

    ![PIM Application access](./media/pim-how-to-activate-role/pim-application-access.png)

1. <span data-ttu-id="b1669-150">Click **Azure Active Directory** to reopen the portal on the **All Users** page.</span><span class="sxs-lookup"><span data-stu-id="b1669-150">Click **Azure Active Directory** to reopen the portal on the **All Users** page.</span></span>

    <span data-ttu-id="b1669-151">When you click this link, you force a refresh and there is a check for new Azure AD role assignments.</span><span class="sxs-lookup"><span data-stu-id="b1669-151">When you click this link, you force a refresh and there is a check for new Azure AD role assignments.</span></span>

## <a name="deactivate-a-role"></a><span data-ttu-id="b1669-152">Deactivate a role</span><span class="sxs-lookup"><span data-stu-id="b1669-152">Deactivate a role</span></span>

<span data-ttu-id="b1669-153">Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.</span><span class="sxs-lookup"><span data-stu-id="b1669-153">Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.</span></span>

<span data-ttu-id="b1669-154">If you complete your administrator tasks early, you can also deactivate a role manually in Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="b1669-154">If you complete your administrator tasks early, you can also deactivate a role manually in Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="b1669-155">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="b1669-155">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="b1669-156">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="b1669-156">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="b1669-157">Click **My roles**.</span><span class="sxs-lookup"><span data-stu-id="b1669-157">Click **My roles**.</span></span>

1. <span data-ttu-id="b1669-158">Click **Active roles** to see your list of active roles.</span><span class="sxs-lookup"><span data-stu-id="b1669-158">Click **Active roles** to see your list of active roles.</span></span>

1. <span data-ttu-id="b1669-159">Find the role you're done using and then click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="b1669-159">Find the role you're done using and then click **Deactivate**.</span></span>

## <a name="cancel-a-pending-request"></a><span data-ttu-id="b1669-160">Cancel a pending request</span><span class="sxs-lookup"><span data-stu-id="b1669-160">Cancel a pending request</span></span>

<span data-ttu-id="b1669-161">If you do not require activation of a role that requires approval, you can cancel a pending request at any time.</span><span class="sxs-lookup"><span data-stu-id="b1669-161">If you do not require activation of a role that requires approval, you can cancel a pending request at any time.</span></span>

1. <span data-ttu-id="b1669-162">Open Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="b1669-162">Open Azure AD Privileged Identity Management.</span></span>

1. <span data-ttu-id="b1669-163">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="b1669-163">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="b1669-164">Click **My requests**.</span><span class="sxs-lookup"><span data-stu-id="b1669-164">Click **My requests**.</span></span>

1. <span data-ttu-id="b1669-165">For the role that you want to cancel, click the **Cancel** button.</span><span class="sxs-lookup"><span data-stu-id="b1669-165">For the role that you want to cancel, click the **Cancel** button.</span></span>

    <span data-ttu-id="b1669-166">When you click Cancel, the request will be cancelled.</span><span class="sxs-lookup"><span data-stu-id="b1669-166">When you click Cancel, the request will be cancelled.</span></span> <span data-ttu-id="b1669-167">To activate the role again, you will have to submit a new request for activation.</span><span class="sxs-lookup"><span data-stu-id="b1669-167">To activate the role again, you will have to submit a new request for activation.</span></span>

   ![Cancel pending request](./media/pim-how-to-activate-role/directory-role-cancel.png)

## <a name="next-steps"></a><span data-ttu-id="b1669-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1669-169">Next steps</span></span>

- [<span data-ttu-id="b1669-170">Activate my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="b1669-170">Activate my Azure resource roles in PIM</span></span>](pim-resource-roles-activate-your-roles.md)
