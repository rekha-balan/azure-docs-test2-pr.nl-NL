---
title: What is a policy migration in Azure Active Directory conditional access? | Microsoft Docs
description: Learn what you need to know to migrate classic policies in the Azure portal.
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
ms.date: 07/24/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: c8431ee305c8a266a79f58e8b4ba4e6541f79f9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870993"
---
# <a name="what-is-a-policy-migration-in-azure-active-directory-conditional-access"></a><span data-ttu-id="0ec37-105">What is a policy migration in Azure Active Directory conditional access?</span><span class="sxs-lookup"><span data-stu-id="0ec37-105">What is a policy migration in Azure Active Directory conditional access?</span></span> 


<span data-ttu-id="0ec37-106">[Conditional access](../active-directory-conditional-access-azure-portal.md) is a capability of Azure Active directory (Azure AD) that enables you to control how authorized users access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="0ec37-106">[Conditional access](../active-directory-conditional-access-azure-portal.md) is a capability of Azure Active directory (Azure AD) that enables you to control how authorized users access your cloud apps.</span></span> <span data-ttu-id="0ec37-107">While the purpose is still the same, the release of the new Azure portal has introduced significant improvements to how conditional access works.</span><span class="sxs-lookup"><span data-stu-id="0ec37-107">While the purpose is still the same, the release of the new Azure portal has introduced significant improvements to how conditional access works.</span></span>

<span data-ttu-id="0ec37-108">You should consider migrating the policies you have not created in the Azure portal because:</span><span class="sxs-lookup"><span data-stu-id="0ec37-108">You should consider migrating the policies you have not created in the Azure portal because:</span></span>

- <span data-ttu-id="0ec37-109">You can now address scenarios you could not handle before.</span><span class="sxs-lookup"><span data-stu-id="0ec37-109">You can now address scenarios you could not handle before.</span></span>

- <span data-ttu-id="0ec37-110">You can reduce the number of policies you have to manage by consolidating them.</span><span class="sxs-lookup"><span data-stu-id="0ec37-110">You can reduce the number of policies you have to manage by consolidating them.</span></span>   

- <span data-ttu-id="0ec37-111">You can manage all your conditional access policies in one central location.</span><span class="sxs-lookup"><span data-stu-id="0ec37-111">You can manage all your conditional access policies in one central location.</span></span>

- <span data-ttu-id="0ec37-112">The Azure classic portal will be retired.</span><span class="sxs-lookup"><span data-stu-id="0ec37-112">The Azure classic portal will be retired.</span></span>   

<span data-ttu-id="0ec37-113">This article explains what you need to know to migrate your existing conditional access policies to the new framework.</span><span class="sxs-lookup"><span data-stu-id="0ec37-113">This article explains what you need to know to migrate your existing conditional access policies to the new framework.</span></span>
 
## <a name="classic-policies"></a><span data-ttu-id="0ec37-114">Classic policies</span><span class="sxs-lookup"><span data-stu-id="0ec37-114">Classic policies</span></span>

<span data-ttu-id="0ec37-115">In the [Azure portal](https://portal.azure.com), the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page is your entry point to your conditional access polices.</span><span class="sxs-lookup"><span data-stu-id="0ec37-115">In the [Azure portal](https://portal.azure.com), the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page is your entry point to your conditional access polices.</span></span> <span data-ttu-id="0ec37-116">However, in your environment, you might also have conditional access policies you have not created using this page.</span><span class="sxs-lookup"><span data-stu-id="0ec37-116">However, in your environment, you might also have conditional access policies you have not created using this page.</span></span> <span data-ttu-id="0ec37-117">These policies are known as *classic policies*.</span><span class="sxs-lookup"><span data-stu-id="0ec37-117">These policies are known as *classic policies*.</span></span> <span data-ttu-id="0ec37-118">Classic policies are conditional access policies, you have created in:</span><span class="sxs-lookup"><span data-stu-id="0ec37-118">Classic policies are conditional access policies, you have created in:</span></span>

- <span data-ttu-id="0ec37-119">The Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="0ec37-119">The Azure classic portal</span></span>
- <span data-ttu-id="0ec37-120">The Intune classic portal</span><span class="sxs-lookup"><span data-stu-id="0ec37-120">The Intune classic portal</span></span>
- <span data-ttu-id="0ec37-121">The Intune App Protection portal</span><span class="sxs-lookup"><span data-stu-id="0ec37-121">The Intune App Protection portal</span></span>


<span data-ttu-id="0ec37-122">On the **Conditional access** page, you can access your classic policies by clicking [**Classic policies (preview)**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies) in the **Manage** section.</span><span class="sxs-lookup"><span data-stu-id="0ec37-122">On the **Conditional access** page, you can access your classic policies by clicking [**Classic policies (preview)**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies) in the **Manage** section.</span></span> 


![Azure Active Directory](./media/policy-migration/71.png)


<span data-ttu-id="0ec37-124">The **Classic policies** view provides you with an option to:</span><span class="sxs-lookup"><span data-stu-id="0ec37-124">The **Classic policies** view provides you with an option to:</span></span>

- <span data-ttu-id="0ec37-125">Filter your classic policies.</span><span class="sxs-lookup"><span data-stu-id="0ec37-125">Filter your classic policies.</span></span>
 
    ![Azure Active Directory](./media/policy-migration/72.png)

- <span data-ttu-id="0ec37-127">Disable classic policies.</span><span class="sxs-lookup"><span data-stu-id="0ec37-127">Disable classic policies.</span></span>

    ![Azure Active Directory](./media/policy-migration/73.png)
   
- <span data-ttu-id="0ec37-129">Review the settings of a classic policies (and to disable it).</span><span class="sxs-lookup"><span data-stu-id="0ec37-129">Review the settings of a classic policies (and to disable it).</span></span>

    ![Azure Active Directory](./media/policy-migration/74.png)


<span data-ttu-id="0ec37-131">If you have disabled a classic policy, you can't revert this step anymore.</span><span class="sxs-lookup"><span data-stu-id="0ec37-131">If you have disabled a classic policy, you can't revert this step anymore.</span></span> <span data-ttu-id="0ec37-132">This is why you can modify the group membership in a classic policy using the **Details** view.</span><span class="sxs-lookup"><span data-stu-id="0ec37-132">This is why you can modify the group membership in a classic policy using the **Details** view.</span></span> 

![Azure Active Directory](./media/policy-migration/75.png)

<span data-ttu-id="0ec37-134">By either changing the selected groups or by excluding specific groups, you can test the effect of a disabled classic policy for a few test users before disabling the policy for all included users and groups.</span><span class="sxs-lookup"><span data-stu-id="0ec37-134">By either changing the selected groups or by excluding specific groups, you can test the effect of a disabled classic policy for a few test users before disabling the policy for all included users and groups.</span></span> 



## <a name="azure-ad-conditional-access-policies"></a><span data-ttu-id="0ec37-135">Azure AD conditional access policies</span><span class="sxs-lookup"><span data-stu-id="0ec37-135">Azure AD conditional access policies</span></span>

<span data-ttu-id="0ec37-136">With conditional access in the Azure portal, you can manage all your policies in one central location.</span><span class="sxs-lookup"><span data-stu-id="0ec37-136">With conditional access in the Azure portal, you can manage all your policies in one central location.</span></span> <span data-ttu-id="0ec37-137">Because the implementation of how conditional access has significantly changed, you should familiarize yourself with the basic concepts before migrating your classic policies.</span><span class="sxs-lookup"><span data-stu-id="0ec37-137">Because the implementation of how conditional access has significantly changed, you should familiarize yourself with the basic concepts before migrating your classic policies.</span></span>

<span data-ttu-id="0ec37-138">See:</span><span class="sxs-lookup"><span data-stu-id="0ec37-138">See:</span></span>

- <span data-ttu-id="0ec37-139">[What is conditional access in Azure Active Directory](../active-directory-conditional-access-azure-portal.md) to learn about the basic concepts and the terminology.</span><span class="sxs-lookup"><span data-stu-id="0ec37-139">[What is conditional access in Azure Active Directory](../active-directory-conditional-access-azure-portal.md) to learn about the basic concepts and the terminology.</span></span>

- <span data-ttu-id="0ec37-140">[Best practices for conditional access in Azure Active Directory](best-practices.md) to get some guidance on deploying conditional access in your organization.</span><span class="sxs-lookup"><span data-stu-id="0ec37-140">[Best practices for conditional access in Azure Active Directory](best-practices.md) to get some guidance on deploying conditional access in your organization.</span></span>

- <span data-ttu-id="0ec37-141">[Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md) to familiarize yourself with the user interface in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ec37-141">[Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md) to familiarize yourself with the user interface in the Azure portal.</span></span>


 
## <a name="migration-considerations"></a><span data-ttu-id="0ec37-142">Migration considerations</span><span class="sxs-lookup"><span data-stu-id="0ec37-142">Migration considerations</span></span>

<span data-ttu-id="0ec37-143">In this article, Azure AD conditional access policies are also referred to as *new policies*.</span><span class="sxs-lookup"><span data-stu-id="0ec37-143">In this article, Azure AD conditional access policies are also referred to as *new policies*.</span></span>
<span data-ttu-id="0ec37-144">Your classic policies continue to work side by side with your new policies until you disable or delete them.</span><span class="sxs-lookup"><span data-stu-id="0ec37-144">Your classic policies continue to work side by side with your new policies until you disable or delete them.</span></span> 

<span data-ttu-id="0ec37-145">The following aspects are important in the context of a policy consolidation:</span><span class="sxs-lookup"><span data-stu-id="0ec37-145">The following aspects are important in the context of a policy consolidation:</span></span>

- <span data-ttu-id="0ec37-146">While classic policies are tied to a specific cloud app, you can select as many cloud apps as you need to in a new policy.</span><span class="sxs-lookup"><span data-stu-id="0ec37-146">While classic policies are tied to a specific cloud app, you can select as many cloud apps as you need to in a new policy.</span></span>

- <span data-ttu-id="0ec37-147">Controls of a classic policy and a new policy for a cloud app require all controls (*AND*) to be fulfilled.</span><span class="sxs-lookup"><span data-stu-id="0ec37-147">Controls of a classic policy and a new policy for a cloud app require all controls (*AND*) to be fulfilled.</span></span> 


- <span data-ttu-id="0ec37-148">In a new policy, you can:</span><span class="sxs-lookup"><span data-stu-id="0ec37-148">In a new policy, you can:</span></span>
 
    - <span data-ttu-id="0ec37-149">Combine multiple conditions if required by your scenario.</span><span class="sxs-lookup"><span data-stu-id="0ec37-149">Combine multiple conditions if required by your scenario.</span></span> 

    - <span data-ttu-id="0ec37-150">Select several grant requirements as access control and combine them with a logical *OR* (require one of the selected controls) or with a logical *AND* (require all of the selected controls).</span><span class="sxs-lookup"><span data-stu-id="0ec37-150">Select several grant requirements as access control and combine them with a logical *OR* (require one of the selected controls) or with a logical *AND* (require all of the selected controls).</span></span>

        ![Azure Active Directory](./media/policy-migration/25.png)




### <a name="office-365-exchange-online"></a><span data-ttu-id="0ec37-152">Office 365 Exchange online</span><span class="sxs-lookup"><span data-stu-id="0ec37-152">Office 365 Exchange online</span></span>

<span data-ttu-id="0ec37-153">If you want to migrate classic policies for **Office 365 Exchange online** that include **Exchange Active Sync** as client apps condition, you might not be able to consolidate them into one new policy.</span><span class="sxs-lookup"><span data-stu-id="0ec37-153">If you want to migrate classic policies for **Office 365 Exchange online** that include **Exchange Active Sync** as client apps condition, you might not be able to consolidate them into one new policy.</span></span> 

<span data-ttu-id="0ec37-154">This is, for example, the case if you want to support all client app types.</span><span class="sxs-lookup"><span data-stu-id="0ec37-154">This is, for example, the case if you want to support all client app types.</span></span> <span data-ttu-id="0ec37-155">In a new policy that has **Exchange Active Sync** as client apps condition, you can't select other client apps.</span><span class="sxs-lookup"><span data-stu-id="0ec37-155">In a new policy that has **Exchange Active Sync** as client apps condition, you can't select other client apps.</span></span>

![Azure Active Directory](./media/policy-migration/64.png)

<span data-ttu-id="0ec37-157">A consolidation into one new policy is also not possible if your classic policies contain several conditions.</span><span class="sxs-lookup"><span data-stu-id="0ec37-157">A consolidation into one new policy is also not possible if your classic policies contain several conditions.</span></span> <span data-ttu-id="0ec37-158">A new policy that has **Exchange Active Sync** as client apps condition configured does not support other conditions:</span><span class="sxs-lookup"><span data-stu-id="0ec37-158">A new policy that has **Exchange Active Sync** as client apps condition configured does not support other conditions:</span></span>   

![Azure Active Directory](./media/policy-migration/08.png)

<span data-ttu-id="0ec37-160">If you have a new policy that has **Exchange Active Sync** as client apps condition configured, you need to make sure that all other conditions are not configured.</span><span class="sxs-lookup"><span data-stu-id="0ec37-160">If you have a new policy that has **Exchange Active Sync** as client apps condition configured, you need to make sure that all other conditions are not configured.</span></span> 

![Azure Active Directory](./media/policy-migration/16.png)
 

<span data-ttu-id="0ec37-162">[App-based](technical-reference.md#approved-client-app-requirement) classic policies for Office 365 Exchange Online that include **Exchange Active Sync** as client apps condition allow **supported** and **unsupported** [device platforms](technical-reference.md#device-platform-condition).</span><span class="sxs-lookup"><span data-stu-id="0ec37-162">[App-based](technical-reference.md#approved-client-app-requirement) classic policies for Office 365 Exchange Online that include **Exchange Active Sync** as client apps condition allow **supported** and **unsupported** [device platforms](technical-reference.md#device-platform-condition).</span></span> <span data-ttu-id="0ec37-163">While you can't configure individual device platforms in a related new policy, you can limit the support to [supported device platforms](technical-reference.md#device-platform-condition) only.</span><span class="sxs-lookup"><span data-stu-id="0ec37-163">While you can't configure individual device platforms in a related new policy, you can limit the support to [supported device platforms](technical-reference.md#device-platform-condition) only.</span></span> 

![Azure Active Directory](./media/policy-migration/65.png)

<span data-ttu-id="0ec37-165">You can consolidate multiple classic policies that include **Exchange Active Sync** as client apps condition if they have:</span><span class="sxs-lookup"><span data-stu-id="0ec37-165">You can consolidate multiple classic policies that include **Exchange Active Sync** as client apps condition if they have:</span></span>

- <span data-ttu-id="0ec37-166">Only **Exchange Active Sync** as condition</span><span class="sxs-lookup"><span data-stu-id="0ec37-166">Only **Exchange Active Sync** as condition</span></span> 

- <span data-ttu-id="0ec37-167">Several requirements for granting access configured</span><span class="sxs-lookup"><span data-stu-id="0ec37-167">Several requirements for granting access configured</span></span>

<span data-ttu-id="0ec37-168">One common scenario is the consolidation of:</span><span class="sxs-lookup"><span data-stu-id="0ec37-168">One common scenario is the consolidation of:</span></span>

- <span data-ttu-id="0ec37-169">A device-based classic policy from the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="0ec37-169">A device-based classic policy from the Azure classic portal</span></span> 
- <span data-ttu-id="0ec37-170">An app-based classic policy in the Intune app protection portal</span><span class="sxs-lookup"><span data-stu-id="0ec37-170">An app-based classic policy in the Intune app protection portal</span></span> 
 
<span data-ttu-id="0ec37-171">In this case, you can consolidate your classic policies into one new policy that has both requirements selected.</span><span class="sxs-lookup"><span data-stu-id="0ec37-171">In this case, you can consolidate your classic policies into one new policy that has both requirements selected.</span></span>

![Azure Active Directory](./media/policy-migration/62.png)



### <a name="device-platforms"></a><span data-ttu-id="0ec37-173">Device platforms</span><span class="sxs-lookup"><span data-stu-id="0ec37-173">Device platforms</span></span>

<span data-ttu-id="0ec37-174">Classic policies with [app-based controls](technical-reference.md#approved-client-app-requirement) are pre-configured with iOS and Android as the [device platform condition](technical-reference.md#device-platform-condition).</span><span class="sxs-lookup"><span data-stu-id="0ec37-174">Classic policies with [app-based controls](technical-reference.md#approved-client-app-requirement) are pre-configured with iOS and Android as the [device platform condition](technical-reference.md#device-platform-condition).</span></span> 

<span data-ttu-id="0ec37-175">In a new policy, you need to select the [device platforms](technical-reference.md#device-platform-condition) you want to support individually.</span><span class="sxs-lookup"><span data-stu-id="0ec37-175">In a new policy, you need to select the [device platforms](technical-reference.md#device-platform-condition) you want to support individually.</span></span>

![Azure Active Directory](./media/policy-migration/41.png)



 
 


## <a name="next-steps"></a><span data-ttu-id="0ec37-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ec37-177">Next steps</span></span>

- <span data-ttu-id="0ec37-178">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="0ec37-178">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

- <span data-ttu-id="0ec37-179">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="0ec37-179">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 
