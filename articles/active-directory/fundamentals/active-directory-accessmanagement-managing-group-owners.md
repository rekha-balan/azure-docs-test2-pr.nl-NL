---
title: Next steps for access management using groups - Azure AD | Microsoft Docs
description: Advanced How-to's for managing security groups and how to use these groups to manage access to a resource.
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: conceptual
ms.date: 09/12/2017
ms.author: lizross
ms.custom: it-pro
ms.openlocfilehash: bdc8754253ce2567d957b4d6240fe52242aea2ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864741"
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="0a70b-103">Managing owners for a group</span><span class="sxs-lookup"><span data-stu-id="0a70b-103">Managing owners for a group</span></span>
<span data-ttu-id="0a70b-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span><span class="sxs-lookup"><span data-stu-id="0a70b-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="0a70b-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span><span class="sxs-lookup"><span data-stu-id="0a70b-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

## <a name="add-an-owner-to-a-group"></a><span data-ttu-id="0a70b-106">Add an owner to a group</span><span class="sxs-lookup"><span data-stu-id="0a70b-106">Add an owner to a group</span></span>

1. <span data-ttu-id="0a70b-107">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0a70b-107">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users and groups**.</span></span>
2. <span data-ttu-id="0a70b-108">Select **All groups**, and then open the group that you want to add owners to.</span><span class="sxs-lookup"><span data-stu-id="0a70b-108">Select **All groups**, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="0a70b-109">Select **Add Owners**.</span><span class="sxs-lookup"><span data-stu-id="0a70b-109">Select **Add Owners**.</span></span>
4. <span data-ttu-id="0a70b-110">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span><span class="sxs-lookup"><span data-stu-id="0a70b-110">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

## <a name="remove-an-owner-from-a-group"></a><span data-ttu-id="0a70b-111">Remove an owner from a group</span><span class="sxs-lookup"><span data-stu-id="0a70b-111">Remove an owner from a group</span></span>

1. <span data-ttu-id="0a70b-112">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0a70b-112">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users and groups**.</span></span>
2. <span data-ttu-id="0a70b-113">Select **All groups**, and then open the group from which you want to remove owners.</span><span class="sxs-lookup"><span data-stu-id="0a70b-113">Select **All groups**, and then open the group from which you want to remove owners.</span></span>
3. <span data-ttu-id="0a70b-114">Select the **Owners** tab.</span><span class="sxs-lookup"><span data-stu-id="0a70b-114">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="0a70b-115">Select the owner that you want to remove from this group, and then select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="0a70b-115">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="0a70b-116">Additional information</span><span class="sxs-lookup"><span data-stu-id="0a70b-116">Additional information</span></span>
<span data-ttu-id="0a70b-117">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a70b-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0a70b-118">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="0a70b-118">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="0a70b-119">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="0a70b-119">Azure Active Directory cmdlets for configuring group settings</span></span>](../users-groups-roles/groups-settings-cmdlets.md)
* [<span data-ttu-id="0a70b-120">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a70b-120">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="0a70b-121">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a70b-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="0a70b-122">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a70b-122">Integrating your on-premises identities with Azure Active Directory</span></span>](../connect/active-directory-aadconnect.md)
