---
title: Start using PIM - Azure | Microsoft Docs
description: Learn how to start using Azure AD Privileged Identity Management (PIM) in the Azure portal.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: pim
ms.topic: conceptual
ms.workload: identity
ms.date: 08/27/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 5b3bff27821964648713b02589c941c99e3eb03d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865412"
---
# <a name="start-using-pim"></a><span data-ttu-id="3fa37-103">Start using PIM</span><span class="sxs-lookup"><span data-stu-id="3fa37-103">Start using PIM</span></span>

<span data-ttu-id="3fa37-104">With Azure Active Directory (Azure AD) Privileged Identity Management (PIM), you can manage, control, and monitor access within your organization.</span><span class="sxs-lookup"><span data-stu-id="3fa37-104">With Azure Active Directory (Azure AD) Privileged Identity Management (PIM), you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="3fa37-105">This scope includes access to Azure resources, Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="3fa37-105">This scope includes access to Azure resources, Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="3fa37-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="3fa37-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="first-person-to-use-pim"></a><span data-ttu-id="3fa37-107">First person to use PIM</span><span class="sxs-lookup"><span data-stu-id="3fa37-107">First person to use PIM</span></span>

<span data-ttu-id="3fa37-108">If you're the first person to use PIM in your directory, you are automatically assigned the [Security administrator](../users-groups-roles/directory-assign-admin-roles.md#security-administrator) and [Privileged role administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) roles in the directory.</span><span class="sxs-lookup"><span data-stu-id="3fa37-108">If you're the first person to use PIM in your directory, you are automatically assigned the [Security administrator](../users-groups-roles/directory-assign-admin-roles.md#security-administrator) and [Privileged role administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) roles in the directory.</span></span> <span data-ttu-id="3fa37-109">Only privileged role administrators can manage Azure AD directory role assignments of users.</span><span class="sxs-lookup"><span data-stu-id="3fa37-109">Only privileged role administrators can manage Azure AD directory role assignments of users.</span></span> <span data-ttu-id="3fa37-110">In addition, you may choose to run the [security wizard.](pim-security-wizard.md)</span><span class="sxs-lookup"><span data-stu-id="3fa37-110">In addition, you may choose to run the [security wizard.](pim-security-wizard.md)</span></span> <span data-ttu-id="3fa37-111">that walks you through the initial discovery and assignment experience.</span><span class="sxs-lookup"><span data-stu-id="3fa37-111">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="add-pim-tile-to-the-dashboard"></a><span data-ttu-id="3fa37-112">Add PIM tile to the dashboard</span><span class="sxs-lookup"><span data-stu-id="3fa37-112">Add PIM tile to the dashboard</span></span>

<span data-ttu-id="3fa37-113">To make it easier to open PIM, you should add a PIM tile to your Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="3fa37-113">To make it easier to open PIM, you should add a PIM tile to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="3fa37-114">Sign in to the [Azure portal](https://portal.azure.com/) as a Global administrator of your directory.</span><span class="sxs-lookup"><span data-stu-id="3fa37-114">Sign in to the [Azure portal](https://portal.azure.com/) as a Global administrator of your directory.</span></span>

1. <span data-ttu-id="3fa37-115">Click **All services** and find the **Azure AD Privileged Identity Management** service.</span><span class="sxs-lookup"><span data-stu-id="3fa37-115">Click **All services** and find the **Azure AD Privileged Identity Management** service.</span></span>

    ![Azure AD Privileged Identity Management in All services](./media/pim-getting-started/pim-all-services-find.png)

1. <span data-ttu-id="3fa37-117">Click to open the PIM Quickstart.</span><span class="sxs-lookup"><span data-stu-id="3fa37-117">Click to open the PIM Quickstart.</span></span>

1. <span data-ttu-id="3fa37-118">Check **Pin blade to dashboard** to pin the PIM Quickstart blade to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="3fa37-118">Check **Pin blade to dashboard** to pin the PIM Quickstart blade to the dashboard.</span></span>

    ![Pin blade to dashboard](./media/pim-getting-started/pim-quickstart-pin-to-dashboard.png)

    <span data-ttu-id="3fa37-120">On the Azure dashboard, you'll see a tile like this:</span><span class="sxs-lookup"><span data-stu-id="3fa37-120">On the Azure dashboard, you'll see a tile like this:</span></span>

    ![PIM Quickstart tile](./media/pim-getting-started/pim-quickstart-dashboard-tile.png)

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="3fa37-122">Navigate to your tasks</span><span class="sxs-lookup"><span data-stu-id="3fa37-122">Navigate to your tasks</span></span>

<span data-ttu-id="3fa37-123">Once PIM is set up, you can use this blade to accomplish your identity management tasks.</span><span class="sxs-lookup"><span data-stu-id="3fa37-123">Once PIM is set up, you can use this blade to accomplish your identity management tasks.</span></span>

![Top-level tasks for PIM - screenshot](./media/pim-getting-started/pim-quickstart-tasks.png)

| <span data-ttu-id="3fa37-125">Task + Manage</span><span class="sxs-lookup"><span data-stu-id="3fa37-125">Task + Manage</span></span> | <span data-ttu-id="3fa37-126">Description</span><span class="sxs-lookup"><span data-stu-id="3fa37-126">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3fa37-127">**My roles**</span><span class="sxs-lookup"><span data-stu-id="3fa37-127">**My roles**</span></span>  | <span data-ttu-id="3fa37-128">Displays a list of eligible and active roles assigned to you.</span><span class="sxs-lookup"><span data-stu-id="3fa37-128">Displays a list of eligible and active roles assigned to you.</span></span> <span data-ttu-id="3fa37-129">This is where you can activate any assigned eligible roles.</span><span class="sxs-lookup"><span data-stu-id="3fa37-129">This is where you can activate any assigned eligible roles.</span></span> |
| <span data-ttu-id="3fa37-130">**My requests**</span><span class="sxs-lookup"><span data-stu-id="3fa37-130">**My requests**</span></span> | <span data-ttu-id="3fa37-131">Displays your pending requests to activate eligible role assignments.</span><span class="sxs-lookup"><span data-stu-id="3fa37-131">Displays your pending requests to activate eligible role assignments.</span></span> |
| <span data-ttu-id="3fa37-132">**Application access**</span><span class="sxs-lookup"><span data-stu-id="3fa37-132">**Application access**</span></span> | <span data-ttu-id="3fa37-133">Enables you to reduce potential delays and use a role immediately after activation.</span><span class="sxs-lookup"><span data-stu-id="3fa37-133">Enables you to reduce potential delays and use a role immediately after activation.</span></span> |
| <span data-ttu-id="3fa37-134">**Approve requests**</span><span class="sxs-lookup"><span data-stu-id="3fa37-134">**Approve requests**</span></span> | <span data-ttu-id="3fa37-135">Displays a list of requests to activate eligible roles by users in your directory that you are designated to approve.</span><span class="sxs-lookup"><span data-stu-id="3fa37-135">Displays a list of requests to activate eligible roles by users in your directory that you are designated to approve.</span></span> |
| <span data-ttu-id="3fa37-136">**Review access**</span><span class="sxs-lookup"><span data-stu-id="3fa37-136">**Review access**</span></span> | <span data-ttu-id="3fa37-137">Lists active access reviews you are assigned to complete, whether you're reviewing access for yourself or someone else.</span><span class="sxs-lookup"><span data-stu-id="3fa37-137">Lists active access reviews you are assigned to complete, whether you're reviewing access for yourself or someone else.</span></span> |
| <span data-ttu-id="3fa37-138">**Azure AD directory roles**</span><span class="sxs-lookup"><span data-stu-id="3fa37-138">**Azure AD directory roles**</span></span> | <span data-ttu-id="3fa37-139">Displays a dashboard and settings for privileged role administrators to manage Azure AD directory role assignments.</span><span class="sxs-lookup"><span data-stu-id="3fa37-139">Displays a dashboard and settings for privileged role administrators to manage Azure AD directory role assignments.</span></span> <span data-ttu-id="3fa37-140">This dashboard is disabled for anyone who isn't a privileged role administrator.</span><span class="sxs-lookup"><span data-stu-id="3fa37-140">This dashboard is disabled for anyone who isn't a privileged role administrator.</span></span> <span data-ttu-id="3fa37-141">These users have access to a special dashboard titled My view.</span><span class="sxs-lookup"><span data-stu-id="3fa37-141">These users have access to a special dashboard titled My view.</span></span> <span data-ttu-id="3fa37-142">The My view dashboard only displays information about the user accessing the dashboard, not the entire tenant.</span><span class="sxs-lookup"><span data-stu-id="3fa37-142">The My view dashboard only displays information about the user accessing the dashboard, not the entire tenant.</span></span> |
| <span data-ttu-id="3fa37-143">**Azure resources**</span><span class="sxs-lookup"><span data-stu-id="3fa37-143">**Azure resources**</span></span> | <span data-ttu-id="3fa37-144">Displays a dashboard and settings for privileged role administrators to manage Azure resource role assignments.</span><span class="sxs-lookup"><span data-stu-id="3fa37-144">Displays a dashboard and settings for privileged role administrators to manage Azure resource role assignments.</span></span> <span data-ttu-id="3fa37-145">This dashboard is disabled for anyone who isn't a privileged role administrator.</span><span class="sxs-lookup"><span data-stu-id="3fa37-145">This dashboard is disabled for anyone who isn't a privileged role administrator.</span></span> <span data-ttu-id="3fa37-146">These users have access to a special dashboard titled My view.</span><span class="sxs-lookup"><span data-stu-id="3fa37-146">These users have access to a special dashboard titled My view.</span></span> <span data-ttu-id="3fa37-147">The My view dashboard only displays information about the user accessing the dashboard, not the entire tenant.</span><span class="sxs-lookup"><span data-stu-id="3fa37-147">The My view dashboard only displays information about the user accessing the dashboard, not the entire tenant.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3fa37-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fa37-148">Next steps</span></span>

- [<span data-ttu-id="3fa37-149">Activate my Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="3fa37-149">Activate my Azure AD directory roles in PIM</span></span>](pim-how-to-activate-role.md)
- [<span data-ttu-id="3fa37-150">Activate my Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="3fa37-150">Activate my Azure resource roles in PIM</span></span>](pim-resource-roles-activate-your-roles.md)
