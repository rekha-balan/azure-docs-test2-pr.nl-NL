---
title: Dedicated groups in Azure Active Directory | Microsoft Docs
description: Overview of how dedicated groups work in Azure Active Directory and how they are created.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 92b9c88ec49424c96c3bd21bc5c4ce390352c17b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661558"
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="40381-103">Dedicated groups in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40381-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="40381-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span><span class="sxs-lookup"><span data-stu-id="40381-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="40381-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span><span class="sxs-lookup"><span data-stu-id="40381-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="40381-106">Dedicated groups require that an Azure AD Premium license is assigned to</span><span class="sxs-lookup"><span data-stu-id="40381-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="40381-107">the administrator who manages the rule on a group</span><span class="sxs-lookup"><span data-stu-id="40381-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="40381-108">all users who are selected by the rule to be a member of the group</span><span class="sxs-lookup"><span data-stu-id="40381-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="40381-109">**To enable dedicated groups**</span><span class="sxs-lookup"><span data-stu-id="40381-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="40381-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span><span class="sxs-lookup"><span data-stu-id="40381-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="40381-111">Select the **Groups** tab, and then open the group you want to edit.</span><span class="sxs-lookup"><span data-stu-id="40381-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="40381-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="40381-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="40381-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="40381-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="40381-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span><span class="sxs-lookup"><span data-stu-id="40381-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="40381-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span><span class="sxs-lookup"><span data-stu-id="40381-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="40381-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span><span class="sxs-lookup"><span data-stu-id="40381-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="40381-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span><span class="sxs-lookup"><span data-stu-id="40381-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="40381-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span><span class="sxs-lookup"><span data-stu-id="40381-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="40381-119">For a group that excludes all Guests, use a rule such as the following:</span><span class="sxs-lookup"><span data-stu-id="40381-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="40381-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="40381-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="40381-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="40381-121">Next steps</span></span>
<span data-ttu-id="40381-122">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40381-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="40381-123">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="40381-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="40381-124">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40381-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="40381-125">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40381-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="40381-126">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40381-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
