---
title: How to manage role activation settings | Microsoft Docs
description: Learn how to change the default settings for privileged identities with the Azure Active Directory Privileged Identity Management extension.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 9d29faa1f7fbd9f73a7372387d5103b64ef6e761
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662758"
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="85f99-103">How to manage role activation settings in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="85f99-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="85f99-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span><span class="sxs-lookup"><span data-stu-id="85f99-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="85f99-105">Manage the role activation settings</span><span class="sxs-lookup"><span data-stu-id="85f99-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="85f99-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="85f99-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="85f99-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span><span class="sxs-lookup"><span data-stu-id="85f99-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="85f99-108">Choose the role whose settings you want to manage.</span><span class="sxs-lookup"><span data-stu-id="85f99-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="85f99-109">On the settings page for each role, there are a number of settings you can configure.</span><span class="sxs-lookup"><span data-stu-id="85f99-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="85f99-110">These settings only affect users who are eligible admins, not permanent admins.</span><span class="sxs-lookup"><span data-stu-id="85f99-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="85f99-111">**Activations**: The time, in hours, that a role stays active before it expires.</span><span class="sxs-lookup"><span data-stu-id="85f99-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="85f99-112">This can be between 1 and 72 hours.</span><span class="sxs-lookup"><span data-stu-id="85f99-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="85f99-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span><span class="sxs-lookup"><span data-stu-id="85f99-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="85f99-114">This can be useful for detecting unauthorized or illegitimate activations.</span><span class="sxs-lookup"><span data-stu-id="85f99-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="85f99-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span><span class="sxs-lookup"><span data-stu-id="85f99-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="85f99-116">This can be useful when you perform role access audits.</span><span class="sxs-lookup"><span data-stu-id="85f99-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="85f99-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span><span class="sxs-lookup"><span data-stu-id="85f99-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="85f99-118">They only have to verify this once per session, not every time they activate a role.</span><span class="sxs-lookup"><span data-stu-id="85f99-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="85f99-119">There are two tips to keep in mind when you enable MFA:</span><span class="sxs-lookup"><span data-stu-id="85f99-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="85f99-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="85f99-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="85f99-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span><span class="sxs-lookup"><span data-stu-id="85f99-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="85f99-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span><span class="sxs-lookup"><span data-stu-id="85f99-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="85f99-123">This is a safety feature because these roles should be carefully protected:</span><span class="sxs-lookup"><span data-stu-id="85f99-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="85f99-124">Application administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-124">Application administrator</span></span>
  * <span data-ttu-id="85f99-125">Application Proxy server administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="85f99-126">Billing administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-126">Billing administrator</span></span>  
  * <span data-ttu-id="85f99-127">Compliance administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-127">Compliance administrator</span></span>  
  * <span data-ttu-id="85f99-128">CRM service administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-128">CRM service administrator</span></span>
  * <span data-ttu-id="85f99-129">Customer LockBox access approver</span><span class="sxs-lookup"><span data-stu-id="85f99-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="85f99-130">Directory writer</span><span class="sxs-lookup"><span data-stu-id="85f99-130">Directory writer</span></span>  
  * <span data-ttu-id="85f99-131">Exchange administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-131">Exchange administrator</span></span>  
  * <span data-ttu-id="85f99-132">Global administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-132">Global administrator</span></span>
  * <span data-ttu-id="85f99-133">Intune service administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-133">Intune service administrator</span></span>
  * <span data-ttu-id="85f99-134">Mailbox administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="85f99-135">Partner tier1 support</span><span class="sxs-lookup"><span data-stu-id="85f99-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="85f99-136">Partner tier2 support</span><span class="sxs-lookup"><span data-stu-id="85f99-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="85f99-137">Privileged role administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="85f99-138">Security administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-138">Security administrator</span></span>  
  * <span data-ttu-id="85f99-139">SharePoint administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="85f99-140">Skype for Business administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="85f99-141">User account administrator</span><span class="sxs-lookup"><span data-stu-id="85f99-141">User account administrator</span></span>  

<span data-ttu-id="85f99-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="85f99-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="85f99-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="85f99-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

