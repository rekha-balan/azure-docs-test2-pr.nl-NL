---
title: Using a group to manage access to SaaS Applications | Microsoft Docs
description: How to use groups in Azure Active Directory Premium or Basic to assign access to SaaS applications that are integrated with Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 03/14/2017
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 8c04f2723466ea7abc8ea3c3cc1f1efb953da764
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969326"
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="0c9d9-103">Using a group to manage access to SaaS applications</span><span class="sxs-lookup"><span data-stu-id="0c9d9-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="0c9d9-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="0c9d9-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="0c9d9-106">This way you can save time by managing the membership of the marketing department in one place.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="0c9d9-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span> <span data-ttu-id="0c9d9-108">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-108">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c9d9-109">You can use this feature only after you start an Azure AD Premium trial or purchase Azure AD Premium or Azure AD Basic licenses.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-109">You can use this feature only after you start an Azure AD Premium trial or purchase Azure AD Premium or Azure AD Basic licenses.</span></span> <span data-ttu-id="0c9d9-110">Group-based assignment is supported only for Security groups.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-110">Group-based assignment is supported only for Security groups.</span></span> <span data-ttu-id="0c9d9-111">Nested group memberships are not supported for group-based assignment to applications at this time.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-111">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>

<span data-ttu-id="0c9d9-112">**To assign access for a user or group to a SaaS application**</span><span class="sxs-lookup"><span data-stu-id="0c9d9-112">**To assign access for a user or group to a SaaS application**</span></span>

1. <span data-ttu-id="0c9d9-113">In the [Azure AD admin center](https://aad.portal.azure.com), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-113">In the [Azure AD admin center](https://aad.portal.azure.com), select **Enterprise applications**.</span></span>
2. <span data-ttu-id="0c9d9-114">Select an application that you added from the Application Gallery to open it.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-114">Select an application that you added from the Application Gallery to open it.</span></span>
3. <span data-ttu-id="0c9d9-115">Select **Users and groups**, and then select **Add user**.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-115">Select **Users and groups**, and then select **Add user**.</span></span>
4. <span data-ttu-id="0c9d9-116">On **Add Assignment**, select **Users and groups** to open the **Users and groups** selection list.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-116">On **Add Assignment**, select **Users and groups** to open the **Users and groups** selection list.</span></span>
6. <span data-ttu-id="0c9d9-117">Select as many groups or users as you want, then click or tap **Select** to add them to the **Add Assignment** list.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-117">Select as many groups or users as you want, then click or tap **Select** to add them to the **Add Assignment** list.</span></span> <span data-ttu-id="0c9d9-118">You can also assign a role to a user at this stage.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-118">You can also assign a role to a user at this stage.</span></span>
7. <span data-ttu-id="0c9d9-119">Select **Assign** to assign the users or groups to the selected enterprise application.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-119">Select **Assign** to assign the users or groups to the selected enterprise application.</span></span>

### <a name="next-steps"></a><span data-ttu-id="0c9d9-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c9d9-120">Next steps</span></span>
<span data-ttu-id="0c9d9-121">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c9d9-121">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0c9d9-122">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="0c9d9-122">Managing access to resources with Azure Active Directory groups</span></span>](../fundamentals/active-directory-manage-groups.md)
* [<span data-ttu-id="0c9d9-123">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c9d9-123">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="0c9d9-124">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="0c9d9-124">Azure Active Directory cmdlets for configuring group settings</span></span>](groups-settings-cmdlets.md)
* [<span data-ttu-id="0c9d9-125">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c9d9-125">What is Azure Active Directory?</span></span>](../fundamentals/active-directory-whatis.md)
* [<span data-ttu-id="0c9d9-126">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c9d9-126">Integrating your on-premises identities with Azure Active Directory</span></span>](../connect/active-directory-aadconnect.md)
