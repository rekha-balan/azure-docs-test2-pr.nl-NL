---
title: Next steps for access management using groups | Microsoft Docs
description: Advanced How-to's for managing security groups and how to use these groups to manage access to a resource.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: curtand
ms.openlocfilehash: aaf064b6c7db86f287ac50e4e381e661297c1e37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662183"
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="bea60-103">Managing owners for a group</span><span class="sxs-lookup"><span data-stu-id="bea60-103">Managing owners for a group</span></span>
<span data-ttu-id="bea60-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span><span class="sxs-lookup"><span data-stu-id="bea60-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="bea60-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span><span class="sxs-lookup"><span data-stu-id="bea60-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

## <a name="assigning-group-ownership"></a><span data-ttu-id="bea60-106">Assigning group ownership</span><span class="sxs-lookup"><span data-stu-id="bea60-106">Assigning group ownership</span></span>
<span data-ttu-id="bea60-107">**To add an owner to a group**</span><span class="sxs-lookup"><span data-stu-id="bea60-107">**To add an owner to a group**</span></span>

1. <span data-ttu-id="bea60-108">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span><span class="sxs-lookup"><span data-stu-id="bea60-108">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="bea60-109">Select the **Groups** tab, and then open the group that you want to add owners to.</span><span class="sxs-lookup"><span data-stu-id="bea60-109">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="bea60-110">Select **Add Owners**.</span><span class="sxs-lookup"><span data-stu-id="bea60-110">Select **Add Owners**.</span></span>
4. <span data-ttu-id="bea60-111">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span><span class="sxs-lookup"><span data-stu-id="bea60-111">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="bea60-112">**To remove an owner from a group**</span><span class="sxs-lookup"><span data-stu-id="bea60-112">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="bea60-113">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span><span class="sxs-lookup"><span data-stu-id="bea60-113">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="bea60-114">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span><span class="sxs-lookup"><span data-stu-id="bea60-114">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="bea60-115">Select the **Owners** tab.</span><span class="sxs-lookup"><span data-stu-id="bea60-115">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="bea60-116">Select the owner that you want to remove from this group, and then select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="bea60-116">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="bea60-117">Additional information</span><span class="sxs-lookup"><span data-stu-id="bea60-117">Additional information</span></span>
<span data-ttu-id="bea60-118">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bea60-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="bea60-119">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="bea60-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="bea60-120">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="bea60-120">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="bea60-121">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bea60-121">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="bea60-122">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bea60-122">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="bea60-123">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bea60-123">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
