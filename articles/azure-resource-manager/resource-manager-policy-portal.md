---
title: Azure portal for resource policies | Microsoft Docs
description: Describes how to use Azure portal to create and manage Resource Manager policies. Policies can be applied at the subscription or resource groups.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: 523c499ed42fdaffec698f061785fc904e8c3376
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563099"
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="065ab-104">Use Azure portal to assign and manage resource policies</span><span class="sxs-lookup"><span data-stu-id="065ab-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="065ab-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="065ab-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="065ab-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span><span class="sxs-lookup"><span data-stu-id="065ab-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="065ab-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span><span class="sxs-lookup"><span data-stu-id="065ab-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="065ab-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span><span class="sxs-lookup"><span data-stu-id="065ab-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="065ab-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span><span class="sxs-lookup"><span data-stu-id="065ab-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="065ab-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="065ab-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="065ab-111">Policies are inherited by all child resources.</span><span class="sxs-lookup"><span data-stu-id="065ab-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="065ab-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="065ab-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="065ab-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span><span class="sxs-lookup"><span data-stu-id="065ab-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="065ab-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span><span class="sxs-lookup"><span data-stu-id="065ab-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="065ab-115">Assign a policy</span><span class="sxs-lookup"><span data-stu-id="065ab-115">Assign a policy</span></span>

1. <span data-ttu-id="065ab-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span><span class="sxs-lookup"><span data-stu-id="065ab-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="065ab-117">In the settings, select **Policies**.</span><span class="sxs-lookup"><span data-stu-id="065ab-117">In the settings, select **Policies**.</span></span>

   ![select policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="065ab-119">To create a policy assignment for this scope, select **Add assignment**.</span><span class="sxs-lookup"><span data-stu-id="065ab-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![add assignment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="065ab-121">Select the policy you want to assign.</span><span class="sxs-lookup"><span data-stu-id="065ab-121">Select the policy you want to assign.</span></span> <span data-ttu-id="065ab-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span><span class="sxs-lookup"><span data-stu-id="065ab-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="065ab-123">These built-in policies cover many common scenarios.</span><span class="sxs-lookup"><span data-stu-id="065ab-123">These built-in policies cover many common scenarios.</span></span>

   ![select definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="065ab-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span><span class="sxs-lookup"><span data-stu-id="065ab-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="065ab-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span><span class="sxs-lookup"><span data-stu-id="065ab-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![show parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="065ab-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span><span class="sxs-lookup"><span data-stu-id="065ab-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![select parameter values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="065ab-130">Provide values for the other parameters.</span><span class="sxs-lookup"><span data-stu-id="065ab-130">Provide values for the other parameters.</span></span> <span data-ttu-id="065ab-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="065ab-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="065ab-132">Select **OK** when done.</span><span class="sxs-lookup"><span data-stu-id="065ab-132">Select **OK** when done.</span></span>

   ![define parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="065ab-134">You have assigned the policy to the specified scope.</span><span class="sxs-lookup"><span data-stu-id="065ab-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="065ab-135">View policy assignments</span><span class="sxs-lookup"><span data-stu-id="065ab-135">View policy assignments</span></span>

<span data-ttu-id="065ab-136">After assigning a policy, you see it in the list of policies for that scope.</span><span class="sxs-lookup"><span data-stu-id="065ab-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="065ab-137">The **Details** tab shows a summary of the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="065ab-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![show details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="065ab-139">The **Assignment rule** tab shows the JSON for the policy definition.</span><span class="sxs-lookup"><span data-stu-id="065ab-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![show assignment rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="065ab-141">Change an existing policy assignment</span><span class="sxs-lookup"><span data-stu-id="065ab-141">Change an existing policy assignment</span></span>

<span data-ttu-id="065ab-142">To change a policy, select **Edit assignment** or **Delete**</span><span class="sxs-lookup"><span data-stu-id="065ab-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![edit or delete assignment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="065ab-144">Assign custom policies</span><span class="sxs-lookup"><span data-stu-id="065ab-144">Assign custom policies</span></span>

<span data-ttu-id="065ab-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span><span class="sxs-lookup"><span data-stu-id="065ab-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="065ab-146">Those policies are prefaced with **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="065ab-146">Those policies are prefaced with **[Custom]**</span></span>

![custom policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="065ab-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="065ab-148">Next steps</span></span>
* <span data-ttu-id="065ab-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="065ab-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="065ab-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="065ab-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="065ab-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="065ab-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 











