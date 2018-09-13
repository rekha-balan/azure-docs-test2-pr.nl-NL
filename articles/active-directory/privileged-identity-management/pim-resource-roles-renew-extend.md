---
title: Extend or renew Azure resource role assignments in PIM | Microsoft Docs
description: Learn how to extend or renew Azure resource role assignments in Azure AD Privileged Identity Management (PIM).
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
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 3294bddea867e061d01e8dc72f4e47f3238b6c4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867829"
---
# <a name="extend-or-renew-azure-resource-role-assignments-in-pim"></a><span data-ttu-id="3bf1d-103">Extend or renew Azure resource role assignments in PIM</span><span class="sxs-lookup"><span data-stu-id="3bf1d-103">Extend or renew Azure resource role assignments in PIM</span></span>

<span data-ttu-id="3bf1d-104">Privileged Identity Management (PIM) for Azure resources introduces new controls to manage the access and assignment lifecycle for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-104">Privileged Identity Management (PIM) for Azure resources introduces new controls to manage the access and assignment lifecycle for Azure resources.</span></span> <span data-ttu-id="3bf1d-105">Administrators can assign membership using start and end date-time properties.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-105">Administrators can assign membership using start and end date-time properties.</span></span> <span data-ttu-id="3bf1d-106">When the assignment end approaches, PIM sends email notifications to the affected users or groups.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-106">When the assignment end approaches, PIM sends email notifications to the affected users or groups.</span></span> <span data-ttu-id="3bf1d-107">It also sends email notifications to administrators of the resource to ensure that appropriate access is maintained.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-107">It also sends email notifications to administrators of the resource to ensure that appropriate access is maintained.</span></span> <span data-ttu-id="3bf1d-108">Assignments might be renewed and remain visible in an expired state for up to 30 days, even if access is not extended.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-108">Assignments might be renewed and remain visible in an expired state for up to 30 days, even if access is not extended.</span></span>

## <a name="who-can-extend-and-renew"></a><span data-ttu-id="3bf1d-109">Who can extend and renew?</span><span class="sxs-lookup"><span data-stu-id="3bf1d-109">Who can extend and renew?</span></span>

<span data-ttu-id="3bf1d-110">Only administrators of the resource can extend or renew role assignments.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-110">Only administrators of the resource can extend or renew role assignments.</span></span> <span data-ttu-id="3bf1d-111">The affected member can request to extend roles that are about to expire and request to renew roles that are already expired.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-111">The affected member can request to extend roles that are about to expire and request to renew roles that are already expired.</span></span>

## <a name="when-are-notifications-sent"></a><span data-ttu-id="3bf1d-112">When are notifications sent?</span><span class="sxs-lookup"><span data-stu-id="3bf1d-112">When are notifications sent?</span></span>

<span data-ttu-id="3bf1d-113">PIM sends email notifications to administrators and affected members of roles that are expiring within 14 days and one day prior to expiration.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-113">PIM sends email notifications to administrators and affected members of roles that are expiring within 14 days and one day prior to expiration.</span></span> <span data-ttu-id="3bf1d-114">It sends an additional email when an assignment officially expires.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-114">It sends an additional email when an assignment officially expires.</span></span> 

<span data-ttu-id="3bf1d-115">Administrators receive notifications when a member of an expiring or expired role requests to extend or renew.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-115">Administrators receive notifications when a member of an expiring or expired role requests to extend or renew.</span></span> <span data-ttu-id="3bf1d-116">When a specific administrator resolves the request, all other administrators are notified of the resolution decision (approved or denied).</span><span class="sxs-lookup"><span data-stu-id="3bf1d-116">When a specific administrator resolves the request, all other administrators are notified of the resolution decision (approved or denied).</span></span> <span data-ttu-id="3bf1d-117">Then the requesting member is notified of the decision.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-117">Then the requesting member is notified of the decision.</span></span> 

## <a name="extend-role-assignments"></a><span data-ttu-id="3bf1d-118">Extend role assignments</span><span class="sxs-lookup"><span data-stu-id="3bf1d-118">Extend role assignments</span></span>

<span data-ttu-id="3bf1d-119">The following steps outline the process for requesting, resolving, or administering an extension or renewal of a role assignment.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-119">The following steps outline the process for requesting, resolving, or administering an extension or renewal of a role assignment.</span></span> 

### <a name="member-extend"></a><span data-ttu-id="3bf1d-120">Member extend</span><span class="sxs-lookup"><span data-stu-id="3bf1d-120">Member extend</span></span>

<span data-ttu-id="3bf1d-121">Members of a role assignment can extend expiring role assignments directly from the **Eligible** or **Active** tab on the **My roles** page of a resource and from the top level **My roles** page of the PIM portal.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-121">Members of a role assignment can extend expiring role assignments directly from the **Eligible** or **Active** tab on the **My roles** page of a resource and from the top level **My roles** page of the PIM portal.</span></span> <span data-ttu-id="3bf1d-122">Members can request to extend eligible and active (assigned) roles that expire in the next 14 days.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-122">Members can request to extend eligible and active (assigned) roles that expire in the next 14 days.</span></span>

![Extend roles](media/azure-pim-resource-rbac/aadpim_rbac_extend_ui.png)

<span data-ttu-id="3bf1d-124">When the assignment end date-time is within 14 days, the button to **Extend** becomes an active link in the user interface.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-124">When the assignment end date-time is within 14 days, the button to **Extend** becomes an active link in the user interface.</span></span> <span data-ttu-id="3bf1d-125">In the following example, assume the current date is March 27.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-125">In the following example, assume the current date is March 27.</span></span>

![The "Extend" button](media/azure-pim-resource-rbac/aadpim_rbac_extend_within_14.png)

<span data-ttu-id="3bf1d-127">To request an extension of this role assignment, select **Extend** to open the request form.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-127">To request an extension of this role assignment, select **Extend** to open the request form.</span></span>

![Open the request form](media/azure-pim-resource-rbac/aadpim_rbac_extend_role_assignment_request.png)

<span data-ttu-id="3bf1d-129">To view information about the original assignment, expand **Assignment details**.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-129">To view information about the original assignment, expand **Assignment details**.</span></span> <span data-ttu-id="3bf1d-130">Enter a reason for the extension request, and then select **Extend**.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-130">Enter a reason for the extension request, and then select **Extend**.</span></span>

>[!Note]
><span data-ttu-id="3bf1d-131">We recommend including the details of why the extension is necessary, and for how long the extension should be granted (if you have this information).</span><span class="sxs-lookup"><span data-stu-id="3bf1d-131">We recommend including the details of why the extension is necessary, and for how long the extension should be granted (if you have this information).</span></span>

![Extend role assignment](media/azure-pim-resource-rbac/aadpim_rbac_extend_form_complete.png)

<span data-ttu-id="3bf1d-133">In a matter of moments, resource administrators  receive an email notification requesting that they review the extension request.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-133">In a matter of moments, resource administrators  receive an email notification requesting that they review the extension request.</span></span> <span data-ttu-id="3bf1d-134">If a request to extend has already been submitted, a toast notification appears at the top of the Azure portal explaining the error.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-134">If a request to extend has already been submitted, a toast notification appears at the top of the Azure portal explaining the error.</span></span>

![](media/azure-pim-resource-rbac/aadpim_rbac_extend_failed_existing_request.png)

<span data-ttu-id="3bf1d-135">Go to the **Pending requests** tab in the left pane to view the status of your request or to cancel it.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-135">Go to the **Pending requests** tab in the left pane to view the status of your request or to cancel it.</span></span>

![](media/azure-pim-resource-rbac/aadpim_rbac_extend_cancel_request.png)

### <a name="admin-approve"></a><span data-ttu-id="3bf1d-136">Admin approve</span><span class="sxs-lookup"><span data-stu-id="3bf1d-136">Admin approve</span></span>

<span data-ttu-id="3bf1d-137">When a member submits a request to extend a role assignment, resource administrators receive an email notification that contains the details of the original assignment and the reason for the request.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-137">When a member submits a request to extend a role assignment, resource administrators receive an email notification that contains the details of the original assignment and the reason for the request.</span></span> <span data-ttu-id="3bf1d-138">The notification includes a direct link to the request for the administrator to approve or deny.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-138">The notification includes a direct link to the request for the administrator to approve or deny.</span></span> 

<span data-ttu-id="3bf1d-139">In addition to using following the link from email, administrators can approve or deny requests by going to the PIM administration portal and selecting **Approve requests** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-139">In addition to using following the link from email, administrators can approve or deny requests by going to the PIM administration portal and selecting **Approve requests** in the left pane.</span></span>

![Screenshot of error](media/azure-pim-resource-rbac/aadpim_rbac_extend_admin_approve_grid.png)

<span data-ttu-id="3bf1d-141">When an Administrator selects **Approve** or **Deny**, the details of the request are shown, along with a field to provide justification for the audit logs.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-141">When an Administrator selects **Approve** or **Deny**, the details of the request are shown, along with a field to provide justification for the audit logs.</span></span>

![](media/azure-pim-resource-rbac/aadpim_rbac_extend_admin_approve_blade.png)

<span data-ttu-id="3bf1d-142">When approving a request to extend role assignment, resource administrators can choose a new start date, end date, and assignment type.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-142">When approving a request to extend role assignment, resource administrators can choose a new start date, end date, and assignment type.</span></span> <span data-ttu-id="3bf1d-143">Changing assignment type might be necessary if the administrator wants to provide limited access to complete a specific task (one day, for example).</span><span class="sxs-lookup"><span data-stu-id="3bf1d-143">Changing assignment type might be necessary if the administrator wants to provide limited access to complete a specific task (one day, for example).</span></span> <span data-ttu-id="3bf1d-144">In this example, the administrator can change the assignment from **Eligible** to **Active**.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-144">In this example, the administrator can change the assignment from **Eligible** to **Active**.</span></span> <span data-ttu-id="3bf1d-145">This means they can provide access to the requestor without requiring them to activate.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-145">This means they can provide access to the requestor without requiring them to activate.</span></span>

### <a name="admin-extend"></a><span data-ttu-id="3bf1d-146">Admin extend</span><span class="sxs-lookup"><span data-stu-id="3bf1d-146">Admin extend</span></span>

<span data-ttu-id="3bf1d-147">If a role member forgets or is unable to request a role membership extension, an administrator can extend an assignment on behalf of the member.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-147">If a role member forgets or is unable to request a role membership extension, an administrator can extend an assignment on behalf of the member.</span></span> <span data-ttu-id="3bf1d-148">Administrative extensions of role membership do not require approval, but notifications are sent to all other administrators after the role has been extended.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-148">Administrative extensions of role membership do not require approval, but notifications are sent to all other administrators after the role has been extended.</span></span>

<span data-ttu-id="3bf1d-149">To extend a role membership, browse to the resource role or member view in PIM.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-149">To extend a role membership, browse to the resource role or member view in PIM.</span></span> <span data-ttu-id="3bf1d-150">Find the member that requires an extension.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-150">Find the member that requires an extension.</span></span> <span data-ttu-id="3bf1d-151">Then select **Extend** in the action column.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-151">Then select **Extend** in the action column.</span></span>

![Extend a role membership](media/azure-pim-resource-rbac/aadpim_rbac_extend_admin_extend.png)

## <a name="renew-role-assignments"></a><span data-ttu-id="3bf1d-153">Renew role assignments</span><span class="sxs-lookup"><span data-stu-id="3bf1d-153">Renew role assignments</span></span>

<span data-ttu-id="3bf1d-154">While conceptually similar to the process for requesting an extension, the process to renew an expired role assignment is different.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-154">While conceptually similar to the process for requesting an extension, the process to renew an expired role assignment is different.</span></span> <span data-ttu-id="3bf1d-155">Using the following steps, members and administrators can renew access to expired roles when necessary.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-155">Using the following steps, members and administrators can renew access to expired roles when necessary.</span></span>

### <a name="member-renew"></a><span data-ttu-id="3bf1d-156">Member renew</span><span class="sxs-lookup"><span data-stu-id="3bf1d-156">Member renew</span></span>

<span data-ttu-id="3bf1d-157">Members who can no longer access resources can access up to 30 days of expired assignment history.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-157">Members who can no longer access resources can access up to 30 days of expired assignment history.</span></span> <span data-ttu-id="3bf1d-158">To do this, they browse to **My Roles** in the left pane, and then select the **Expired roles** tab in the Azure resource roles section.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-158">To do this, they browse to **My Roles** in the left pane, and then select the **Expired roles** tab in the Azure resource roles section.</span></span>

![The "Expired roles" tab](media/azure-pim-resource-rbac/aadpim_rbac_renew_from_myroles.png)

<span data-ttu-id="3bf1d-160">The list of roles shown defaults to **Eligible roles**.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-160">The list of roles shown defaults to **Eligible roles**.</span></span> <span data-ttu-id="3bf1d-161">Use the drop-down menu to toggle between Eligible and Active assigned roles.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-161">Use the drop-down menu to toggle between Eligible and Active assigned roles.</span></span>

<span data-ttu-id="3bf1d-162">To request renewal for any of the role assignments in the list, select the **Renew** action.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-162">To request renewal for any of the role assignments in the list, select the **Renew** action.</span></span> <span data-ttu-id="3bf1d-163">Then provide a reason for the request.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-163">Then provide a reason for the request.</span></span> <span data-ttu-id="3bf1d-164">It's helpful to provide a duration in addition to any additional context that helps the resource administrator decide to approve or deny.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-164">It's helpful to provide a duration in addition to any additional context that helps the resource administrator decide to approve or deny.</span></span>

![Renew role assignment](media/azure-pim-resource-rbac/aadpim_rbac_renew_request_form.png)

<span data-ttu-id="3bf1d-166">After the request has been submitted, resource administrators are notified of a pending request to renew a role assignment.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-166">After the request has been submitted, resource administrators are notified of a pending request to renew a role assignment.</span></span>

### <a name="admin-approves"></a><span data-ttu-id="3bf1d-167">Admin approves</span><span class="sxs-lookup"><span data-stu-id="3bf1d-167">Admin approves</span></span>

<span data-ttu-id="3bf1d-168">Resource administrators can access the renewal request from the link in the email notification or by accessing PIM from the Azure portal and selecting **Approve requests** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-168">Resource administrators can access the renewal request from the link in the email notification or by accessing PIM from the Azure portal and selecting **Approve requests** from the left pane.</span></span>

![Approve requests](media/azure-pim-resource-rbac/aadpim_rbac_extend_admin_approve_grid.png)

<span data-ttu-id="3bf1d-170">When an administrator selects **Approve** or **Deny**, the details of the request are shown along with a field to provide justification for the audit logs.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-170">When an administrator selects **Approve** or **Deny**, the details of the request are shown along with a field to provide justification for the audit logs.</span></span>

![Approve role assignment](media/azure-pim-resource-rbac/aadpim_rbac_extend_admin_approve_blade.png)

<span data-ttu-id="3bf1d-172">When approving a request to renew role assignment, resource administrators must enter a new start date, end date, and assignment type.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-172">When approving a request to renew role assignment, resource administrators must enter a new start date, end date, and assignment type.</span></span> 

### <a name="admin-renew"></a><span data-ttu-id="3bf1d-173">Admin renew</span><span class="sxs-lookup"><span data-stu-id="3bf1d-173">Admin renew</span></span>

<span data-ttu-id="3bf1d-174">Resource administrators can renew expired role assignments from the **Members** tab in the left navigation menu of a resource.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-174">Resource administrators can renew expired role assignments from the **Members** tab in the left navigation menu of a resource.</span></span> <span data-ttu-id="3bf1d-175">They can also renew expired role assignments from within the **Expired** roles tab of a resource role.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-175">They can also renew expired role assignments from within the **Expired** roles tab of a resource role.</span></span>

<span data-ttu-id="3bf1d-176">To view a list of all expired role assignments, on the **Members** screen, select **Expired roles**.</span><span class="sxs-lookup"><span data-stu-id="3bf1d-176">To view a list of all expired role assignments, on the **Members** screen, select **Expired roles**.</span></span>

![Expired roles](media/azure-pim-resource-rbac/aadpim_rbac_renew_from_member_blade.png)

## <a name="next-steps"></a><span data-ttu-id="3bf1d-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="3bf1d-178">Next steps</span></span>

- [<span data-ttu-id="3bf1d-179">Approve or deny requests for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="3bf1d-179">Approve or deny requests for Azure resource roles in PIM</span></span>](pim-resource-roles-approval-workflow.md)
- [<span data-ttu-id="3bf1d-180">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="3bf1d-180">Configure Azure resource role settings in PIM</span></span>](pim-resource-roles-configure-role-settings.md)
