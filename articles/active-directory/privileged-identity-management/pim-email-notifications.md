---
title: Email notifications in PIM - Azure | Microsoft Docs
description: Describes email notifications in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 09/07/2018
ms.author: rolyon
ms.reviewer: hanki
ms.custom: pim
ms.openlocfilehash: de1d29d3ab1b370257c3a2d6b6ff9f677197fc2a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865367"
---
# <a name="email-notifications-in-pim"></a><span data-ttu-id="de318-103">Email notifications in PIM</span><span class="sxs-lookup"><span data-stu-id="de318-103">Email notifications in PIM</span></span>

<span data-ttu-id="de318-104">When key events occur in Azure AD Privileged Identity Management (PIM), email notifications are sent.</span><span class="sxs-lookup"><span data-stu-id="de318-104">When key events occur in Azure AD Privileged Identity Management (PIM), email notifications are sent.</span></span> <span data-ttu-id="de318-105">For example, PIM sends emails for the following events:</span><span class="sxs-lookup"><span data-stu-id="de318-105">For example, PIM sends emails for the following events:</span></span>

- <span data-ttu-id="de318-106">When a privileged role activation is pending approval</span><span class="sxs-lookup"><span data-stu-id="de318-106">When a privileged role activation is pending approval</span></span>
- <span data-ttu-id="de318-107">When a privileged role activation request is completed</span><span class="sxs-lookup"><span data-stu-id="de318-107">When a privileged role activation request is completed</span></span>
- <span data-ttu-id="de318-108">When a privileged role is activated</span><span class="sxs-lookup"><span data-stu-id="de318-108">When a privileged role is activated</span></span>
- <span data-ttu-id="de318-109">When a privileged role is assigned</span><span class="sxs-lookup"><span data-stu-id="de318-109">When a privileged role is assigned</span></span>
- <span data-ttu-id="de318-110">When Azure AD PIM is enabled</span><span class="sxs-lookup"><span data-stu-id="de318-110">When Azure AD PIM is enabled</span></span>

<span data-ttu-id="de318-111">Email notifications are sent to the following administrators:</span><span class="sxs-lookup"><span data-stu-id="de318-111">Email notifications are sent to the following administrators:</span></span>

- <span data-ttu-id="de318-112">Privileged Role Administrator</span><span class="sxs-lookup"><span data-stu-id="de318-112">Privileged Role Administrator</span></span>
- <span data-ttu-id="de318-113">Security Administrator</span><span class="sxs-lookup"><span data-stu-id="de318-113">Security Administrator</span></span>

<span data-ttu-id="de318-114">Email notifications are also sent to the end user who has the privileged role for the following events:</span><span class="sxs-lookup"><span data-stu-id="de318-114">Email notifications are also sent to the end user who has the privileged role for the following events:</span></span>

- <span data-ttu-id="de318-115">When a privileged role activation request is completed</span><span class="sxs-lookup"><span data-stu-id="de318-115">When a privileged role activation request is completed</span></span>
- <span data-ttu-id="de318-116">When a privileged role is assigned</span><span class="sxs-lookup"><span data-stu-id="de318-116">When a privileged role is assigned</span></span>

<span data-ttu-id="de318-117">Starting at the end of July 2018, email notifications sent through PIM have a new sender email address and a new visual design.</span><span class="sxs-lookup"><span data-stu-id="de318-117">Starting at the end of July 2018, email notifications sent through PIM have a new sender email address and a new visual design.</span></span> <span data-ttu-id="de318-118">This update will impact both PIM for Azure AD and PIM for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="de318-118">This update will impact both PIM for Azure AD and PIM for Azure resources.</span></span> <span data-ttu-id="de318-119">All events that previously triggered an email notification will continue to send out an email.</span><span class="sxs-lookup"><span data-stu-id="de318-119">All events that previously triggered an email notification will continue to send out an email.</span></span> <span data-ttu-id="de318-120">Some emails will have updated content providing more targeted information.</span><span class="sxs-lookup"><span data-stu-id="de318-120">Some emails will have updated content providing more targeted information.</span></span>

## <a name="sender-email-address"></a><span data-ttu-id="de318-121">Sender email address</span><span class="sxs-lookup"><span data-stu-id="de318-121">Sender email address</span></span>

<span data-ttu-id="de318-122">Starting at the end of July 2018, email notifications have the following address:</span><span class="sxs-lookup"><span data-stu-id="de318-122">Starting at the end of July 2018, email notifications have the following address:</span></span>

- <span data-ttu-id="de318-123">Email address:  **azure-noreply@microsoft.com**</span><span class="sxs-lookup"><span data-stu-id="de318-123">Email address:  **azure-noreply@microsoft.com**</span></span>
- <span data-ttu-id="de318-124">Display name: Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="de318-124">Display name: Microsoft Azure</span></span>

<span data-ttu-id="de318-125">Previously, email notifications had the following address:</span><span class="sxs-lookup"><span data-stu-id="de318-125">Previously, email notifications had the following address:</span></span>

- <span data-ttu-id="de318-126">Email address:  **azureadnotifications@microsoft.com**</span><span class="sxs-lookup"><span data-stu-id="de318-126">Email address:  **azureadnotifications@microsoft.com**</span></span>
- <span data-ttu-id="de318-127">Display name: Microsoft Azure AD Notification Service</span><span class="sxs-lookup"><span data-stu-id="de318-127">Display name: Microsoft Azure AD Notification Service</span></span>

## <a name="email-subject-line"></a><span data-ttu-id="de318-128">Email subject line</span><span class="sxs-lookup"><span data-stu-id="de318-128">Email subject line</span></span>

<span data-ttu-id="de318-129">Starting at the end of July 2018, email notifications for both Azure AD and Azure resource roles will have a **PIM** prefix in the subject line.</span><span class="sxs-lookup"><span data-stu-id="de318-129">Starting at the end of July 2018, email notifications for both Azure AD and Azure resource roles will have a **PIM** prefix in the subject line.</span></span> <span data-ttu-id="de318-130">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="de318-130">Here's an example:</span></span>

- <span data-ttu-id="de318-131">PIM: Alain Charon was permanently assigned the Backup Reader role.</span><span class="sxs-lookup"><span data-stu-id="de318-131">PIM: Alain Charon was permanently assigned the Backup Reader role.</span></span>

## <a name="pim-emails-for-azure-ad-roles"></a><span data-ttu-id="de318-132">PIM emails for Azure AD roles</span><span class="sxs-lookup"><span data-stu-id="de318-132">PIM emails for Azure AD roles</span></span>

<span data-ttu-id="de318-133">Starting at the end of July 2018, the PIM email notifications for Azure AD roles have an updated design.</span><span class="sxs-lookup"><span data-stu-id="de318-133">Starting at the end of July 2018, the PIM email notifications for Azure AD roles have an updated design.</span></span> <span data-ttu-id="de318-134">The following shows an example email that is sent when a user activates a privileged role for the fictional Contoso organization.</span><span class="sxs-lookup"><span data-stu-id="de318-134">The following shows an example email that is sent when a user activates a privileged role for the fictional Contoso organization.</span></span>

![New PIM email for Azure AD roles](./media/pim-email-notifications/email-directory-new.png)

<span data-ttu-id="de318-136">Previously, when a user activated a privileged role, the email looked like the following.</span><span class="sxs-lookup"><span data-stu-id="de318-136">Previously, when a user activated a privileged role, the email looked like the following.</span></span>

![Old PIM email for Azure AD roles](./media/pim-email-notifications/email-directory-old.png)

## <a name="pim-emails-for-azure-resource-roles"></a><span data-ttu-id="de318-138">PIM emails for Azure resource roles</span><span class="sxs-lookup"><span data-stu-id="de318-138">PIM emails for Azure resource roles</span></span>

<span data-ttu-id="de318-139">Starting at the end of July 2018, the PIM email notifications for Azure resource roles have an updated design.</span><span class="sxs-lookup"><span data-stu-id="de318-139">Starting at the end of July 2018, the PIM email notifications for Azure resource roles have an updated design.</span></span> <span data-ttu-id="de318-140">The following shows an example email that is sent when a user is assigned a privileged role for the fictional Contoso organization.</span><span class="sxs-lookup"><span data-stu-id="de318-140">The following shows an example email that is sent when a user is assigned a privileged role for the fictional Contoso organization.</span></span>

![New PIM email for Azure resource roles](./media/pim-email-notifications/email-resources-new.png)

<span data-ttu-id="de318-142">Previously, when a user was assigned a privileged role, the email looked like the following.</span><span class="sxs-lookup"><span data-stu-id="de318-142">Previously, when a user was assigned a privileged role, the email looked like the following.</span></span>

![Old PIM email for Azure resource roles](./media/pim-email-notifications/email-resources-old.png)

## <a name="next-steps"></a><span data-ttu-id="de318-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="de318-144">Next steps</span></span>

- [<span data-ttu-id="de318-145">Configure Azure AD directory role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="de318-145">Configure Azure AD directory role settings in PIM</span></span>](pim-how-to-change-default-settings.md)
- [<span data-ttu-id="de318-146">Approve or deny requests for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="de318-146">Approve or deny requests for Azure AD directory roles in PIM</span></span>](azure-ad-pim-approval-workflow.md)
