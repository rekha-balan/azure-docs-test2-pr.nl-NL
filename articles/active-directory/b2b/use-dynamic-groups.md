---
title: Dynamic groups and Azure Active Directory B2B collaboration | Microsoft Docs
description: Shows how to use Azure AD dynamic groups with Azure Active Directory B2B collaboration
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 12/14/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: e91418e2e0620c7ded63150d95cc32e4cc8c34d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868591"
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="a8dd2-103">Dynamic groups and Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="a8dd2-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="a8dd2-104">What are dynamic groups?</span><span class="sxs-lookup"><span data-stu-id="a8dd2-104">What are dynamic groups?</span></span>
<span data-ttu-id="a8dd2-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8dd2-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a8dd2-106">Administrators can set rules to populate groups that are created in Azure AD based on user attributes (such as userType, department, or country).</span><span class="sxs-lookup"><span data-stu-id="a8dd2-106">Administrators can set rules to populate groups that are created in Azure AD based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="a8dd2-107">Members can be automatically added to or removed from a security group based on their attributes.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="a8dd2-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="a8dd2-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](../active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="a8dd2-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](../active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="a8dd2-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="a8dd2-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](../users-groups-roles/groups-dynamic-membership.md).</span><span class="sxs-lookup"><span data-stu-id="a8dd2-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](../users-groups-roles/groups-dynamic-membership.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="a8dd2-112">What are the built-in dynamic groups?</span><span class="sxs-lookup"><span data-stu-id="a8dd2-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="a8dd2-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="a8dd2-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="a8dd2-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![Shows enable the All Users group set to Yes](media/use-dynamic-groups/enable-all-users-group.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="a8dd2-117">Hardening the All users dynamic group</span><span class="sxs-lookup"><span data-stu-id="a8dd2-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="a8dd2-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="a8dd2-119">You can further secure your **All users** group by using a rule to remove guest users.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="a8dd2-120">The following illustration shows the **All users** group modified to exclude guests.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![Shows rule where user type not equals guest](media/use-dynamic-groups/exclude-guest-users.png)

<span data-ttu-id="a8dd2-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span><span class="sxs-lookup"><span data-stu-id="a8dd2-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="a8dd2-123">What such a group might look like:</span><span class="sxs-lookup"><span data-stu-id="a8dd2-123">What such a group might look like:</span></span>

![Shows rule where user type equals guest](media/use-dynamic-groups/only-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="a8dd2-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8dd2-125">Next steps</span></span>

- [<span data-ttu-id="a8dd2-126">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="a8dd2-126">B2B collaboration user properties</span></span>](user-properties.md)
- [<span data-ttu-id="a8dd2-127">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="a8dd2-127">Adding a B2B collaboration user to a role</span></span>](add-guest-to-role.md)
- [<span data-ttu-id="a8dd2-128">Conditional access for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="a8dd2-128">Conditional access for B2B collaboration users</span></span>](conditional-access.md)

