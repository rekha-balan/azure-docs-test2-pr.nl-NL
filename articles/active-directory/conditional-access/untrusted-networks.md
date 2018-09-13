---
title: How to - Configure Azure Active Directory conditional access policies for access attempts from untrusted networks | Microsoft Docs
description: Learn how to configure a conditional access policy in Azure Active Directory (Azure AD) to for access attempts from untrusted networks.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.component: conditional-access
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/23/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 5ddde65b2a68e71d86af6ce3dcd2847736cf5823
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870763"
---
# <a name="how-to-configure-conditional-access-policies-for-access-attempts-from-untrusted-networks"></a><span data-ttu-id="2ff3b-104">How to: Configure conditional access policies for access attempts from untrusted networks</span><span class="sxs-lookup"><span data-stu-id="2ff3b-104">How to: Configure conditional access policies for access attempts from untrusted networks</span></span>   

<span data-ttu-id="2ff3b-105">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-105">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="2ff3b-106">As a result of this, your users can access your cloud apps not only from your organization's network, but also from any untrusted Internet location.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-106">As a result of this, your users can access your cloud apps not only from your organization's network, but also from any untrusted Internet location.</span></span> <span data-ttu-id="2ff3b-107">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users can access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-107">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users can access your cloud apps.</span></span> <span data-ttu-id="2ff3b-108">One common requirement in this context is to control access attempts initiated from untrusted networks.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-108">One common requirement in this context is to control access attempts initiated from untrusted networks.</span></span> <span data-ttu-id="2ff3b-109">This article provides you with the information you need to configure a conditional access policy that handles this requirement.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-109">This article provides you with the information you need to configure a conditional access policy that handles this requirement.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2ff3b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ff3b-110">Prerequisites</span></span>

<span data-ttu-id="2ff3b-111">This article assumes that you are familiar with:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-111">This article assumes that you are familiar with:</span></span> 

- <span data-ttu-id="2ff3b-112">The basic concepts of Azure AD conditional access</span><span class="sxs-lookup"><span data-stu-id="2ff3b-112">The basic concepts of Azure AD conditional access</span></span> 
- <span data-ttu-id="2ff3b-113">Configuring conditional access policies in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2ff3b-113">Configuring conditional access policies in the Azure portal</span></span>

<span data-ttu-id="2ff3b-114">See:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-114">See:</span></span>

- <span data-ttu-id="2ff3b-115">[What is conditional access in Azure Active Directory](../active-directory-conditional-access-azure-portal.md) - for an overview of conditional access</span><span class="sxs-lookup"><span data-stu-id="2ff3b-115">[What is conditional access in Azure Active Directory](../active-directory-conditional-access-azure-portal.md) - for an overview of conditional access</span></span> 

- <span data-ttu-id="2ff3b-116">[Quickstart: Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md) - to get some experience with configuring conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-116">[Quickstart: Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md) - to get some experience with configuring conditional access policies.</span></span> 


## <a name="scenario-description"></a><span data-ttu-id="2ff3b-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2ff3b-117">Scenario description</span></span>

<span data-ttu-id="2ff3b-118">To master the balance between security and productivity, it might be sufficient for you to only require your user to be authenticated using a password.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-118">To master the balance between security and productivity, it might be sufficient for you to only require your user to be authenticated using a password.</span></span> <span data-ttu-id="2ff3b-119">However, when an access attempt is made from an untrusted network location, there is an increased risk that sign-ins are not performed by legitimate users.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-119">However, when an access attempt is made from an untrusted network location, there is an increased risk that sign-ins are not performed by legitimate users.</span></span> <span data-ttu-id="2ff3b-120">To address this concern, you can block access attempts from untrusted networks.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-120">To address this concern, you can block access attempts from untrusted networks.</span></span> <span data-ttu-id="2ff3b-121">Alternatively, you can also require multi-factor authentication (MFA) to gain back additional assurance that an attempt was made by the legitimate owner of the account.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-121">Alternatively, you can also require multi-factor authentication (MFA) to gain back additional assurance that an attempt was made by the legitimate owner of the account.</span></span> 

<span data-ttu-id="2ff3b-122">With Azure AD conditional access, you can address this requirement with a single policy that grants access:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-122">With Azure AD conditional access, you can address this requirement with a single policy that grants access:</span></span> 

- <span data-ttu-id="2ff3b-123">To selected cloud apps</span><span class="sxs-lookup"><span data-stu-id="2ff3b-123">To selected cloud apps</span></span>

- <span data-ttu-id="2ff3b-124">For selected users and groups</span><span class="sxs-lookup"><span data-stu-id="2ff3b-124">For selected users and groups</span></span>  

- <span data-ttu-id="2ff3b-125">Requiring multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="2ff3b-125">Requiring multi-factor authentication</span></span> 

- <span data-ttu-id="2ff3b-126">When an access attempt is made from:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-126">When an access attempt is made from:</span></span> 

    - <span data-ttu-id="2ff3b-127">A location that is not trusted</span><span class="sxs-lookup"><span data-stu-id="2ff3b-127">A location that is not trusted</span></span>


## <a name="considerations"></a><span data-ttu-id="2ff3b-128">Considerations</span><span class="sxs-lookup"><span data-stu-id="2ff3b-128">Considerations</span></span>

<span data-ttu-id="2ff3b-129">The challenge of this scenario is to translate *when an access attempt is made from a location that is not trusted* into a conditional access condition.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-129">The challenge of this scenario is to translate *when an access attempt is made from a location that is not trusted* into a conditional access condition.</span></span> <span data-ttu-id="2ff3b-130">In a conditional access policy, you can configure the [locations condition](location-condition.md) to address scenarios that are related to network locations.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-130">In a conditional access policy, you can configure the [locations condition](location-condition.md) to address scenarios that are related to network locations.</span></span> <span data-ttu-id="2ff3b-131">The locations condition enables you to select named locations, which represent logical groupings of IP address ranges, countries and regions.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-131">The locations condition enables you to select named locations, which represent logical groupings of IP address ranges, countries and regions.</span></span>  

<span data-ttu-id="2ff3b-132">Typically, your organization owns one or more address ranges, for example, 199.30.16.0 - 199.30.16.24.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-132">Typically, your organization owns one or more address ranges, for example, 199.30.16.0 - 199.30.16.24.</span></span>
<span data-ttu-id="2ff3b-133">You can configure a named location by:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-133">You can configure a named location by:</span></span>

- <span data-ttu-id="2ff3b-134">Specifying this range (199.30.16.0/24)</span><span class="sxs-lookup"><span data-stu-id="2ff3b-134">Specifying this range (199.30.16.0/24)</span></span> 

- <span data-ttu-id="2ff3b-135">Assigning a descriptive name such as **Corporate Network**</span><span class="sxs-lookup"><span data-stu-id="2ff3b-135">Assigning a descriptive name such as **Corporate Network**</span></span> 


<span data-ttu-id="2ff3b-136">Instead of trying to define what all locations are that are not trusted, you can:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-136">Instead of trying to define what all locations are that are not trusted, you can:</span></span>

- <span data-ttu-id="2ff3b-137">Include</span><span class="sxs-lookup"><span data-stu-id="2ff3b-137">Include</span></span> 

    ![Conditional access](./media/untrusted-networks/02.png)

- <span data-ttu-id="2ff3b-139">Exclude all trusted locations</span><span class="sxs-lookup"><span data-stu-id="2ff3b-139">Exclude all trusted locations</span></span> 

    ![Conditional access](./media/untrusted-networks/01.png)



## <a name="implementation"></a><span data-ttu-id="2ff3b-141">Implementation</span><span class="sxs-lookup"><span data-stu-id="2ff3b-141">Implementation</span></span>

<span data-ttu-id="2ff3b-142">With the approach outlined in this article, you can now configure a conditional access policy for untrusted locations.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-142">With the approach outlined in this article, you can now configure a conditional access policy for untrusted locations.</span></span> <span data-ttu-id="2ff3b-143">You should always test your policy before rolling it out into production to make sure that it works as expected.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-143">You should always test your policy before rolling it out into production to make sure that it works as expected.</span></span> <span data-ttu-id="2ff3b-144">Ideally, you should do your initial tests in a test tenant if possible.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-144">Ideally, you should do your initial tests in a test tenant if possible.</span></span> <span data-ttu-id="2ff3b-145">For more information, see [How should you deploy a new policy](best-practices.md#how-should-you-deploy-a-new-policy).</span><span class="sxs-lookup"><span data-stu-id="2ff3b-145">For more information, see [How should you deploy a new policy](best-practices.md#how-should-you-deploy-a-new-policy).</span></span> 



## <a name="next-steps"></a><span data-ttu-id="2ff3b-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ff3b-146">Next steps</span></span>

<span data-ttu-id="2ff3b-147">If you would like to learn more about conditional access, see [What is conditional access in Azure Active Directory?](../active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2ff3b-147">If you would like to learn more about conditional access, see [What is conditional access in Azure Active Directory?](../active-directory-conditional-access-azure-portal.md)</span></span>