---
title: Grant access to other administrators to manage PIM - Azure | Microsoft Docs
description: Learn how to grant access to other administrations to manage Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 08/29/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 9d5fce5a80ac1f281fdbe6afe7f9a97816807ccc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855764"
---
# <a name="grant-access-to-other-administrators-to-manage-pim"></a><span data-ttu-id="8eef1-103">Grant access to other administrators to manage PIM</span><span class="sxs-lookup"><span data-stu-id="8eef1-103">Grant access to other administrators to manage PIM</span></span>

<span data-ttu-id="8eef1-104">The Global Administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span><span class="sxs-lookup"><span data-stu-id="8eef1-104">The Global Administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="8eef1-105">No one else gets write access by default, though, including other Global Administrators.</span><span class="sxs-lookup"><span data-stu-id="8eef1-105">No one else gets write access by default, though, including other Global Administrators.</span></span> <span data-ttu-id="8eef1-106">Other Global Administrators, Security Administrators, and Security Readers have read-only access to PIM.</span><span class="sxs-lookup"><span data-stu-id="8eef1-106">Other Global Administrators, Security Administrators, and Security Readers have read-only access to PIM.</span></span> <span data-ttu-id="8eef1-107">To grant access to PIM, the first user can assign others to the **Privileged Role Administrator** role.</span><span class="sxs-lookup"><span data-stu-id="8eef1-107">To grant access to PIM, the first user can assign others to the **Privileged Role Administrator** role.</span></span>

> [!NOTE]
> <span data-ttu-id="8eef1-108">Managing PIM requires Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="8eef1-108">Managing PIM requires Azure MFA.</span></span> <span data-ttu-id="8eef1-109">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access PIM.</span><span class="sxs-lookup"><span data-stu-id="8eef1-109">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access PIM.</span></span>

<span data-ttu-id="8eef1-110">Make sure there are always at least two users in a Privileged Role Administrator role, in case one user is locked out or their account is deleted.</span><span class="sxs-lookup"><span data-stu-id="8eef1-110">Make sure there are always at least two users in a Privileged Role Administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="grant-access-to-manage-pim"></a><span data-ttu-id="8eef1-111">Grant access to manage PIM</span><span class="sxs-lookup"><span data-stu-id="8eef1-111">Grant access to manage PIM</span></span>

1. <span data-ttu-id="8eef1-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8eef1-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="8eef1-113">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-113">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="8eef1-114">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-114">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="8eef1-115">Click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-115">Click **Roles**.</span></span>

    ![PIM Azure AD directory roles - Roles](./media/pim-how-to-give-access-to-pim/pim-directory-roles-roles.png)

1. <span data-ttu-id="8eef1-117">Click the **Privileged Role Administrator** role to open the members page.</span><span class="sxs-lookup"><span data-stu-id="8eef1-117">Click the **Privileged Role Administrator** role to open the members page.</span></span>

    ![Privileged Role Administrator - Members](./media/pim-how-to-give-access-to-pim/pim-pra-members.png)

1. <span data-ttu-id="8eef1-119">Click **Add member**  to open the Add managed members pane.</span><span class="sxs-lookup"><span data-stu-id="8eef1-119">Click **Add member**  to open the Add managed members pane.</span></span>

1. <span data-ttu-id="8eef1-120">Click **Select members** to open the Select members pane.</span><span class="sxs-lookup"><span data-stu-id="8eef1-120">Click **Select members** to open the Select members pane.</span></span>

    ![Privileged Role Administrator - Select members](./media/pim-how-to-give-access-to-pim/pim-pra-select-members.png)

1. <span data-ttu-id="8eef1-122">Select a member and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-122">Select a member and then click **Select**.</span></span>

1. <span data-ttu-id="8eef1-123">Click **OK** to make the member eligible for the **Privileged Role Administrator** role.</span><span class="sxs-lookup"><span data-stu-id="8eef1-123">Click **OK** to make the member eligible for the **Privileged Role Administrator** role.</span></span>

    <span data-ttu-id="8eef1-124">When you assign a new role to someone in PIM, they are automatically configured as **Eligible** to activate the role.</span><span class="sxs-lookup"><span data-stu-id="8eef1-124">When you assign a new role to someone in PIM, they are automatically configured as **Eligible** to activate the role.</span></span>

1. <span data-ttu-id="8eef1-125">To make the member permanent, click the user in the Privileged Role Administrator member list.</span><span class="sxs-lookup"><span data-stu-id="8eef1-125">To make the member permanent, click the user in the Privileged Role Administrator member list.</span></span>

1. <span data-ttu-id="8eef1-126">Click **More** and then **Make permanent** to make the assignment permanent.</span><span class="sxs-lookup"><span data-stu-id="8eef1-126">Click **More** and then **Make permanent** to make the assignment permanent.</span></span>

    ![Privileged Role Administrator - Make permanent](./media/pim-how-to-give-access-to-pim/pim-pra-make-permanent.png)

1. <span data-ttu-id="8eef1-128">Send the user a link to [Start using PIM](pim-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8eef1-128">Send the user a link to [Start using PIM](pim-getting-started.md).</span></span>

## <a name="remove-access-to-manage-pim"></a><span data-ttu-id="8eef1-129">Remove access to manage PIM</span><span class="sxs-lookup"><span data-stu-id="8eef1-129">Remove access to manage PIM</span></span>

<span data-ttu-id="8eef1-130">Before you remove someone from the Privileged Role Administrator role, always make sure there will still be at least two users assigned to it.</span><span class="sxs-lookup"><span data-stu-id="8eef1-130">Before you remove someone from the Privileged Role Administrator role, always make sure there will still be at least two users assigned to it.</span></span>

1. <span data-ttu-id="8eef1-131">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8eef1-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="8eef1-132">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-132">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="8eef1-133">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-133">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="8eef1-134">Click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-134">Click **Roles**.</span></span>

1. <span data-ttu-id="8eef1-135">Click the **Privileged Role Administrator** role to open the members page.</span><span class="sxs-lookup"><span data-stu-id="8eef1-135">Click the **Privileged Role Administrator** role to open the members page.</span></span>

1. <span data-ttu-id="8eef1-136">Add a checkmark next to the user you want to remove and then click **Remove member**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-136">Add a checkmark next to the user you want to remove and then click **Remove member**.</span></span>

    ![Privileged Role Administrator - Remove member](./media/pim-how-to-give-access-to-pim/pim-pra-remove-member.png)

1. <span data-ttu-id="8eef1-138">In the message that appears asking if you want to remove the member from the role, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="8eef1-138">In the message that appears asking if you want to remove the member from the role, click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8eef1-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="8eef1-139">Next steps</span></span>

- [<span data-ttu-id="8eef1-140">Start using PIM</span><span class="sxs-lookup"><span data-stu-id="8eef1-140">Start using PIM</span></span>](pim-getting-started.md)