---
title: Dynamic groups and Azure Active Directory B2B collaboration | Microsoft Docs
description: Azure Active Directory B2B collaboration can be used with Azure AD dynamic groups
services: active-directory
documentationcenter: ''
author: sasubram
manager: femila
editor: ''
tags: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: a770473f86d113be0f590046dc0ed57c424bc4bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662642"
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="ebd68-103">Dynamic groups and Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="ebd68-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="ebd68-104">What are dynamic groups?</span><span class="sxs-lookup"><span data-stu-id="ebd68-104">What are dynamic groups?</span></span>
<span data-ttu-id="ebd68-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebd68-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ebd68-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span><span class="sxs-lookup"><span data-stu-id="ebd68-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="ebd68-107">This allows members to be automatically added to or removed from a security group based on changes to their attributes.</span><span class="sxs-lookup"><span data-stu-id="ebd68-107">This allows members to be automatically added to or removed from a security group based on changes to their attributes.</span></span> <span data-ttu-id="ebd68-108">These groups can be used to provide access to applications or cloud resources (such as SharePoint sites and documents) and to assign licenses to members.</span><span class="sxs-lookup"><span data-stu-id="ebd68-108">These groups can be used to provide access to applications or cloud resources (such as SharePoint sites and documents) and to assign licenses to members.</span></span> <span data-ttu-id="ebd68-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="ebd68-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="ebd68-110">With an AAD Premium P1 or P2 subscription, the Azure portal now provides you with the ability to create advanced rules to enable more complex attribute-based dynamic memberships for Azure Active Directory groups.</span><span class="sxs-lookup"><span data-stu-id="ebd68-110">With an AAD Premium P1 or P2 subscription, the Azure portal now provides you with the ability to create advanced rules to enable more complex attribute-based dynamic memberships for Azure Active Directory groups.</span></span> <span data-ttu-id="ebd68-111">Learn more about creating advanced rules in [Using attributes to create advanced rules for group membership in Azure Active Directory preview](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ebd68-111">Learn more about creating advanced rules in [Using attributes to create advanced rules for group membership in Azure Active Directory preview](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="ebd68-112">What are the built-in dynamic groups?</span><span class="sxs-lookup"><span data-stu-id="ebd68-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="ebd68-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span><span class="sxs-lookup"><span data-stu-id="ebd68-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="ebd68-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span><span class="sxs-lookup"><span data-stu-id="ebd68-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="ebd68-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span><span class="sxs-lookup"><span data-stu-id="ebd68-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![built-in groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-dynamic-groups/built-in-groups.png)

<span data-ttu-id="ebd68-117">Hardening the All users dynamic group By default, the **All users** group contains your B2B collaboration (guest) users as well.</span><span class="sxs-lookup"><span data-stu-id="ebd68-117">Hardening the All users dynamic group By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="ebd68-118">If you want to further secure your **All users** group by removing guest users, you can accomplish this easily by modifying the **All users** group's attribute-based rule.</span><span class="sxs-lookup"><span data-stu-id="ebd68-118">If you want to further secure your **All users** group by removing guest users, you can accomplish this easily by modifying the **All users** group's attribute-based rule.</span></span> <span data-ttu-id="ebd68-119">The illustration below shows the **All users** group modified to exclude guests.</span><span class="sxs-lookup"><span data-stu-id="ebd68-119">The illustration below shows the **All users** group modified to exclude guests.</span></span>

![enable all users group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="ebd68-121">You might also find it useful to create a new dynamic group that only contains Guest users.</span><span class="sxs-lookup"><span data-stu-id="ebd68-121">You might also find it useful to create a new dynamic group that only contains Guest users.</span></span> <span data-ttu-id="ebd68-122">This can be quite handy in targeting policies (such as Conditional Access policies) to Guest users.</span><span class="sxs-lookup"><span data-stu-id="ebd68-122">This can be quite handy in targeting policies (such as Conditional Access policies) to Guest users.</span></span>
<span data-ttu-id="ebd68-123">Here's an illustration of what such a group might look like:</span><span class="sxs-lookup"><span data-stu-id="ebd68-123">Here's an illustration of what such a group might look like:</span></span>

![exclude guest users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="ebd68-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="ebd68-125">Next steps</span></span>

<span data-ttu-id="ebd68-126">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="ebd68-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ebd68-127">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="ebd68-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ebd68-128">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="ebd68-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="ebd68-129">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="ebd68-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="ebd68-130">Delegate B2bB collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="ebd68-130">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="ebd68-131">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="ebd68-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="ebd68-132">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="ebd68-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="ebd68-133">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="ebd68-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="ebd68-134">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="ebd68-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="ebd68-135">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="ebd68-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="ebd68-136">B2B collaboration current limitations</span><span class="sxs-lookup"><span data-stu-id="ebd68-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)



