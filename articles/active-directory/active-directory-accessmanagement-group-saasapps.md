---
title: Using a group to manage access to SaaS Applications | Microsoft Docs
description: How to use groups in Azure Active Directory Premium or Basic to assign access to SaaS applications that are integrated with Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 01b9108048b5d7f3aa960ec01f75a693e074beaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552692"
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="c90cd-103">Using a group to manage access to SaaS applications</span><span class="sxs-lookup"><span data-stu-id="c90cd-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="c90cd-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c90cd-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="c90cd-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span><span class="sxs-lookup"><span data-stu-id="c90cd-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="c90cd-106">This way you can save time by managing the membership of the marketing department in one place.</span><span class="sxs-lookup"><span data-stu-id="c90cd-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="c90cd-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span><span class="sxs-lookup"><span data-stu-id="c90cd-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

<span data-ttu-id="c90cd-108">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span><span class="sxs-lookup"><span data-stu-id="c90cd-108">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="c90cd-109">**To assign access for a group to a SaaS application**</span><span class="sxs-lookup"><span data-stu-id="c90cd-109">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="c90cd-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span><span class="sxs-lookup"><span data-stu-id="c90cd-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="c90cd-111">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span><span class="sxs-lookup"><span data-stu-id="c90cd-111">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="c90cd-112">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="c90cd-112">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="c90cd-113">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span><span class="sxs-lookup"><span data-stu-id="c90cd-113">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="c90cd-114">You only need to type the first part of a group's name.</span><span class="sxs-lookup"><span data-stu-id="c90cd-114">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="c90cd-115">Select the group, then then select the **Assign Access** button.</span><span class="sxs-lookup"><span data-stu-id="c90cd-115">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="c90cd-116">Select **Yes** when you see the confirmation message.</span><span class="sxs-lookup"><span data-stu-id="c90cd-116">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="c90cd-117">Nested group memberships are not supported for group-based assignment to applications at this time.</span><span class="sxs-lookup"><span data-stu-id="c90cd-117">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="c90cd-118">You can also see which users are assigned to the application, either directly or by membership in a group.</span><span class="sxs-lookup"><span data-stu-id="c90cd-118">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="c90cd-119">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span><span class="sxs-lookup"><span data-stu-id="c90cd-119">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="c90cd-120">The list shows users in the directory and whether or not each user is assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="c90cd-120">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="c90cd-121">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span><span class="sxs-lookup"><span data-stu-id="c90cd-121">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="c90cd-122">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="c90cd-122">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="c90cd-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="c90cd-123">Next steps</span></span>
<span data-ttu-id="c90cd-124">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c90cd-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c90cd-125">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="c90cd-125">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="c90cd-126">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c90cd-126">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c90cd-127">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="c90cd-127">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="c90cd-128">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c90cd-128">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="c90cd-129">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c90cd-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
