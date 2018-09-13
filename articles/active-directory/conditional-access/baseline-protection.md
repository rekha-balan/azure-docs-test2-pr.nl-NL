---
title: What is a baseline protection in Azure Active Directory conditional access? - preview | Microsoft Docs
description: Learn how baseline protection ensures that you have at least the baseline level of security enabled in your Azure Active Directory environment.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/08/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 57fef112186834ead76f6223e32cb358e4d6d053
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870015"
---
# <a name="what-is-baseline-protection-preview"></a><span data-ttu-id="22381-105">What is baseline protection (preview)?</span><span class="sxs-lookup"><span data-stu-id="22381-105">What is baseline protection (preview)?</span></span>  

<span data-ttu-id="22381-106">In the last year, identity attacks have increased by 300%.</span><span class="sxs-lookup"><span data-stu-id="22381-106">In the last year, identity attacks have increased by 300%.</span></span> <span data-ttu-id="22381-107">To protect your environment from the ever-increasing attacks, Azure Active Directory (Azure AD) introduces a new feature called baseline protection.</span><span class="sxs-lookup"><span data-stu-id="22381-107">To protect your environment from the ever-increasing attacks, Azure Active Directory (Azure AD) introduces a new feature called baseline protection.</span></span> <span data-ttu-id="22381-108">Baseline protection is a set of predefined [conditional access policies](../active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="22381-108">Baseline protection is a set of predefined [conditional access policies](../active-directory-conditional-access-azure-portal.md).</span></span> <span data-ttu-id="22381-109">The goal of these policies is to ensure that you have at least the baseline level of security enabled in all editions of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22381-109">The goal of these policies is to ensure that you have at least the baseline level of security enabled in all editions of Azure AD.</span></span> 

<span data-ttu-id="22381-110">This article provides you with an overview of baseline protection in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22381-110">This article provides you with an overview of baseline protection in Azure Active Directory.</span></span>


 
## <a name="require-mfa-for-admins"></a><span data-ttu-id="22381-111">Require MFA for admins</span><span class="sxs-lookup"><span data-stu-id="22381-111">Require MFA for admins</span></span>

<span data-ttu-id="22381-112">Users with access to privileged accounts have unrestricted access to your environment.</span><span class="sxs-lookup"><span data-stu-id="22381-112">Users with access to privileged accounts have unrestricted access to your environment.</span></span> <span data-ttu-id="22381-113">Due to the power these accounts have, you should treat them with special care.</span><span class="sxs-lookup"><span data-stu-id="22381-113">Due to the power these accounts have, you should treat them with special care.</span></span> <span data-ttu-id="22381-114">One common method to improve the protection of privileged accounts is to require a stronger form of account verification when they are used to sign-in.</span><span class="sxs-lookup"><span data-stu-id="22381-114">One common method to improve the protection of privileged accounts is to require a stronger form of account verification when they are used to sign-in.</span></span> <span data-ttu-id="22381-115">In Azure Active Directory, you can get a stronger account verification by requiring multi-factor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="22381-115">In Azure Active Directory, you can get a stronger account verification by requiring multi-factor authentication (MFA).</span></span>  

<span data-ttu-id="22381-116">**Require MFA for admins** is a baseline policy that requires MFA for the following directory roles:</span><span class="sxs-lookup"><span data-stu-id="22381-116">**Require MFA for admins** is a baseline policy that requires MFA for the following directory roles:</span></span> 

- <span data-ttu-id="22381-117">Global administrator</span><span class="sxs-lookup"><span data-stu-id="22381-117">Global administrator</span></span>  

- <span data-ttu-id="22381-118">SharePoint administrator</span><span class="sxs-lookup"><span data-stu-id="22381-118">SharePoint administrator</span></span>  

- <span data-ttu-id="22381-119">Exchange administrator</span><span class="sxs-lookup"><span data-stu-id="22381-119">Exchange administrator</span></span>  

- <span data-ttu-id="22381-120">Conditional access administrator</span><span class="sxs-lookup"><span data-stu-id="22381-120">Conditional access administrator</span></span>  

- <span data-ttu-id="22381-121">Security administrator</span><span class="sxs-lookup"><span data-stu-id="22381-121">Security administrator</span></span>  


![Azure Active Directory](./media/baseline-protection/01.png)

<span data-ttu-id="22381-123">This baseline policy provides you with the option to exclude users and groups.</span><span class="sxs-lookup"><span data-stu-id="22381-123">This baseline policy provides you with the option to exclude users and groups.</span></span> <span data-ttu-id="22381-124">You might want to exclude one *[emergency-access administrative account](../users-groups-roles/directory-emergency-access.md)* to ensure you are not locked out of the tenant.</span><span class="sxs-lookup"><span data-stu-id="22381-124">You might want to exclude one *[emergency-access administrative account](../users-groups-roles/directory-emergency-access.md)* to ensure you are not locked out of the tenant.</span></span>


## <a name="enable-a-baseline-policy"></a><span data-ttu-id="22381-125">Enable a baseline policy</span><span class="sxs-lookup"><span data-stu-id="22381-125">Enable a baseline policy</span></span> 

<span data-ttu-id="22381-126">While baseline policies are in preview, they are by default not activated.</span><span class="sxs-lookup"><span data-stu-id="22381-126">While baseline policies are in preview, they are by default not activated.</span></span> <span data-ttu-id="22381-127">You need to manually enable a policy if you want to activate it.</span><span class="sxs-lookup"><span data-stu-id="22381-127">You need to manually enable a policy if you want to activate it.</span></span> <span data-ttu-id="22381-128">As soon as this feature has reached general availability, the policies are by default activated.</span><span class="sxs-lookup"><span data-stu-id="22381-128">As soon as this feature has reached general availability, the policies are by default activated.</span></span> <span data-ttu-id="22381-129">The planned behavior change is the reason why you have in addition to activate and deactivate a third option to set the state of a policy: **Automatically enable policy in the future**.</span><span class="sxs-lookup"><span data-stu-id="22381-129">The planned behavior change is the reason why you have in addition to activate and deactivate a third option to set the state of a policy: **Automatically enable policy in the future**.</span></span> <span data-ttu-id="22381-130">By selecting this option, you let Microsoft decide when to activate a policy.</span><span class="sxs-lookup"><span data-stu-id="22381-130">By selecting this option, you let Microsoft decide when to activate a policy.</span></span>      


<span data-ttu-id="22381-131">**To enable a baseline policy:**</span><span class="sxs-lookup"><span data-stu-id="22381-131">**To enable a baseline policy:**</span></span>  

1. <span data-ttu-id="22381-132">Sign in to the [Azure portal](https://portal.azure.com) as global administrator, security administrator, or conditional access administrator.</span><span class="sxs-lookup"><span data-stu-id="22381-132">Sign in to the [Azure portal](https://portal.azure.com) as global administrator, security administrator, or conditional access administrator.</span></span>

2. <span data-ttu-id="22381-133">In the **Azure portal**, on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22381-133">In the **Azure portal**, on the left navbar, click **Azure Active Directory**.</span></span>

    ![Azure Active Directory](./media/baseline-protection/02.png)

3. <span data-ttu-id="22381-135">On the **Azure Active Directory** page, in the **Security** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="22381-135">On the **Azure Active Directory** page, in the **Security** section, click **Conditional access**.</span></span>

    ![Conditional access](./media/baseline-protection/05.png)

4. <span data-ttu-id="22381-137">In the list of policies, click a policy that starts with **Baseline policy:**.</span><span class="sxs-lookup"><span data-stu-id="22381-137">In the list of policies, click a policy that starts with **Baseline policy:**.</span></span> 

5. <span data-ttu-id="22381-138">To enable the policy, click **Use policy immediately**.</span><span class="sxs-lookup"><span data-stu-id="22381-138">To enable the policy, click **Use policy immediately**.</span></span>

6. <span data-ttu-id="22381-139">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="22381-139">Click **Save**.</span></span> 
 
  
 

## <a name="what-you-should-know"></a><span data-ttu-id="22381-140">What you should know</span><span class="sxs-lookup"><span data-stu-id="22381-140">What you should know</span></span> 

<span data-ttu-id="22381-141">While managing custom conditional access policies requires an Azure AD Premium license, baseline policies are available in all editions of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22381-141">While managing custom conditional access policies requires an Azure AD Premium license, baseline policies are available in all editions of Azure AD.</span></span>     

<span data-ttu-id="22381-142">The directory roles that are included in the baseline policy are the most privileged Azure AD roles.</span><span class="sxs-lookup"><span data-stu-id="22381-142">The directory roles that are included in the baseline policy are the most privileged Azure AD roles.</span></span> 

<span data-ttu-id="22381-143">If you have privileged accounts that are used in your scripts, you should replace them with [Managed Service Identity (MSI)](../managed-identities-azure-resources/overview.md) or [service principals with certificates](../../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="22381-143">If you have privileged accounts that are used in your scripts, you should replace them with [Managed Service Identity (MSI)](../managed-identities-azure-resources/overview.md) or [service principals with certificates](../../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="22381-144">As a temporary workaround, you can exclude specific user accounts from the baseline policy.</span><span class="sxs-lookup"><span data-stu-id="22381-144">As a temporary workaround, you can exclude specific user accounts from the baseline policy.</span></span> 

<span data-ttu-id="22381-145">Baseline policies apply to legacy authentication flows like POP, IMAP, older Office desktop client.</span><span class="sxs-lookup"><span data-stu-id="22381-145">Baseline policies apply to legacy authentication flows like POP, IMAP, older Office desktop client.</span></span> 




## <a name="next-steps"></a><span data-ttu-id="22381-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="22381-146">Next steps</span></span>

<span data-ttu-id="22381-147">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="22381-147">For more information, see:</span></span>

- [<span data-ttu-id="22381-148">Five steps to securing your identity infrastructure</span><span class="sxs-lookup"><span data-stu-id="22381-148">Five steps to securing your identity infrastructure</span></span>](https://docs.microsoft.com/azure/security/azure-ad-secure-steps)

- [<span data-ttu-id="22381-149">What is conditional access in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="22381-149">What is conditional access in Azure Active Directory?</span></span>](overview.md) 

