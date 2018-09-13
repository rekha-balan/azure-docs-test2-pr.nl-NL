---
title: Configure named locations in Azure Active Directory | Microsoft Docs
description: Learn how to configure named locations.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.component: protection
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 62a55672a4326df585fc84699dfd72424be362dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870941"
---
# <a name="configure-named-locations-in-azure-active-directory"></a><span data-ttu-id="3f605-103">Configure named locations in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f605-103">Configure named locations in Azure Active Directory</span></span>

<span data-ttu-id="3f605-104">With named locations, you can label trusted IP address ranges in your organization.</span><span class="sxs-lookup"><span data-stu-id="3f605-104">With named locations, you can label trusted IP address ranges in your organization.</span></span> <span data-ttu-id="3f605-105">Azure Active Directory uses  named locations in the context of:</span><span class="sxs-lookup"><span data-stu-id="3f605-105">Azure Active Directory uses  named locations in the context of:</span></span>

- <span data-ttu-id="3f605-106">The detection of [risk events](reports-monitoring/concept-risk-events.md) to reduce the number of reported false positives.</span><span class="sxs-lookup"><span data-stu-id="3f605-106">The detection of [risk events](reports-monitoring/concept-risk-events.md) to reduce the number of reported false positives.</span></span>  

- <span data-ttu-id="3f605-107">[Location-based conditional access](conditional-access/location-condition.md).</span><span class="sxs-lookup"><span data-stu-id="3f605-107">[Location-based conditional access](conditional-access/location-condition.md).</span></span>


<span data-ttu-id="3f605-108">This article explains, how you can configure named locations in your environment.</span><span class="sxs-lookup"><span data-stu-id="3f605-108">This article explains, how you can configure named locations in your environment.</span></span>


## <a name="entry-points"></a><span data-ttu-id="3f605-109">Entry points</span><span class="sxs-lookup"><span data-stu-id="3f605-109">Entry points</span></span>

<span data-ttu-id="3f605-110">You can access the named location configuration page in the **Security** section of the Azure Active Directory page by clicking:</span><span class="sxs-lookup"><span data-stu-id="3f605-110">You can access the named location configuration page in the **Security** section of the Azure Active Directory page by clicking:</span></span>

![Entry points](./media/active-directory-named-locations/34.png)

- <span data-ttu-id="3f605-112">**Conditional access:**</span><span class="sxs-lookup"><span data-stu-id="3f605-112">**Conditional access:**</span></span>

    - <span data-ttu-id="3f605-113">In the **Manage** section, click **Named locations**.</span><span class="sxs-lookup"><span data-stu-id="3f605-113">In the **Manage** section, click **Named locations**.</span></span>
    
        ![The Named locations command](./media/active-directory-named-locations/06.png)

- <span data-ttu-id="3f605-115">**Risky sign-ins:**</span><span class="sxs-lookup"><span data-stu-id="3f605-115">**Risky sign-ins:**</span></span>

    - <span data-ttu-id="3f605-116">In the toolbar on the top, click **Add known IP address ranges**.</span><span class="sxs-lookup"><span data-stu-id="3f605-116">In the toolbar on the top, click **Add known IP address ranges**.</span></span>

       ![The Named locations command](./media/active-directory-named-locations/35.png)



## <a name="configuration-example"></a><span data-ttu-id="3f605-118">Configuration example</span><span class="sxs-lookup"><span data-stu-id="3f605-118">Configuration example</span></span>

<span data-ttu-id="3f605-119">**To configure a named location:**</span><span class="sxs-lookup"><span data-stu-id="3f605-119">**To configure a named location:**</span></span>

1. <span data-ttu-id="3f605-120">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span><span class="sxs-lookup"><span data-stu-id="3f605-120">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="3f605-121">In the left pane, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f605-121">In the left pane, click **Azure Active Directory**.</span></span>

    ![The Azure Active Directory link in the left pane](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="3f605-123">On the **Azure Active Directory** page, in the **Security** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="3f605-123">On the **Azure Active Directory** page, in the **Security** section, click **Conditional access**.</span></span>

    ![The Conditional access command](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="3f605-125">On the **Conditional Access** page, in the **Manage** section, click **Named locations**.</span><span class="sxs-lookup"><span data-stu-id="3f605-125">On the **Conditional Access** page, in the **Manage** section, click **Named locations**.</span></span>

    ![The Named locations command](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="3f605-127">On the **Named locations** page, click **New location**.</span><span class="sxs-lookup"><span data-stu-id="3f605-127">On the **Named locations** page, click **New location**.</span></span>

    ![The New location command](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="3f605-129">On the **New** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f605-129">On the **New** page, do the following:</span></span>

    ![The New blade](./media/active-directory-named-locations/61.png)

    <span data-ttu-id="3f605-131">a.</span><span class="sxs-lookup"><span data-stu-id="3f605-131">a.</span></span> <span data-ttu-id="3f605-132">In the **Name** box, type a name for your named location.</span><span class="sxs-lookup"><span data-stu-id="3f605-132">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="3f605-133">b.</span><span class="sxs-lookup"><span data-stu-id="3f605-133">b.</span></span> <span data-ttu-id="3f605-134">In the **IP ranges** box, type an IP range.</span><span class="sxs-lookup"><span data-stu-id="3f605-134">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="3f605-135">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span><span class="sxs-lookup"><span data-stu-id="3f605-135">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="3f605-136">c.</span><span class="sxs-lookup"><span data-stu-id="3f605-136">c.</span></span> <span data-ttu-id="3f605-137">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f605-137">Click **Create**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="3f605-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f605-138">Next steps</span></span>

<span data-ttu-id="3f605-139">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="3f605-139">For more information, see:</span></span>

- <span data-ttu-id="3f605-140">[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3f605-140">[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span></span>

- [<span data-ttu-id="3f605-141">Location conditions in Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="3f605-141">Location conditions in Azure Active Directory conditional access</span></span>](conditional-access/location-condition.md)

- <span data-ttu-id="3f605-142">[Azure Active Directory risk events](reports-monitoring/concept-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="3f605-142">[Azure Active Directory risk events](reports-monitoring/concept-risk-events.md).</span></span>

- <span data-ttu-id="3f605-143">[Risky sign-ins report in the Azure Active Directory portal](reports-monitoring/concept-risky-sign-ins.md).</span><span class="sxs-lookup"><span data-stu-id="3f605-143">[Risky sign-ins report in the Azure Active Directory portal](reports-monitoring/concept-risky-sign-ins.md).</span></span>  
