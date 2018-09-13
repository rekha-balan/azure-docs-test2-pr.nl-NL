---
title: Grant user permissions to specific lab policies | Microsoft Docs
description: Learn how to grant user permissions to specific lab policies in DevTest Labs based on each user's needs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 2b81c23b5cf9ea5d4bfc47d36ae251f762ffad11
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866487"
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="8afcc-103">Grant user permissions to specific lab policies</span><span class="sxs-lookup"><span data-stu-id="8afcc-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="8afcc-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8afcc-104">Overview</span></span>
<span data-ttu-id="8afcc-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span><span class="sxs-lookup"><span data-stu-id="8afcc-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="8afcc-106">That way, permissions can be applied based on each user's needs.</span><span class="sxs-lookup"><span data-stu-id="8afcc-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="8afcc-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span><span class="sxs-lookup"><span data-stu-id="8afcc-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="8afcc-108">Policies as resources</span><span class="sxs-lookup"><span data-stu-id="8afcc-108">Policies as resources</span></span>
<span data-ttu-id="8afcc-109">As discussed in the [Azure Role-based Access Control](../role-based-access-control/role-assignments-portal.md) article, RBAC enables fine-grained access management of resources for Azure.</span><span class="sxs-lookup"><span data-stu-id="8afcc-109">As discussed in the [Azure Role-based Access Control](../role-based-access-control/role-assignments-portal.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="8afcc-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span><span class="sxs-lookup"><span data-stu-id="8afcc-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="8afcc-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="8afcc-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="8afcc-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span><span class="sxs-lookup"><span data-stu-id="8afcc-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="8afcc-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/**\* action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="8afcc-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/**\* action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="8afcc-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../role-based-access-control/custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="8afcc-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../role-based-access-control/custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="8afcc-115">Creating a lab custom role using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8afcc-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="8afcc-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="8afcc-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="8afcc-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8afcc-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="8afcc-118">List all the operations/actions for a resource provider</span><span class="sxs-lookup"><span data-stu-id="8afcc-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="8afcc-119">List actions in a particular role:</span><span class="sxs-lookup"><span data-stu-id="8afcc-119">List actions in a particular role:</span></span>
* <span data-ttu-id="8afcc-120">Create a custom role</span><span class="sxs-lookup"><span data-stu-id="8afcc-120">Create a custom role</span></span>

<span data-ttu-id="8afcc-121">The following PowerShell script illustrates examples of how to perform these tasks:</span><span class="sxs-lookup"><span data-stu-id="8afcc-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="8afcc-122">Assigning permissions to a user for a specific policy using custom roles</span><span class="sxs-lookup"><span data-stu-id="8afcc-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="8afcc-123">Once you’ve defined your custom roles, you can assign them to users.</span><span class="sxs-lookup"><span data-stu-id="8afcc-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="8afcc-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span><span class="sxs-lookup"><span data-stu-id="8afcc-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="8afcc-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8afcc-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="8afcc-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="8afcc-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="8afcc-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8afcc-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/default/policies/AllowedVmSizesInLab

<span data-ttu-id="8afcc-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span><span class="sxs-lookup"><span data-stu-id="8afcc-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="8afcc-129">You can use any of the following polices:</span><span class="sxs-lookup"><span data-stu-id="8afcc-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="8afcc-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="8afcc-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="8afcc-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="8afcc-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="8afcc-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="8afcc-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="8afcc-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="8afcc-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="8afcc-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="8afcc-134">Next steps</span></span>
<span data-ttu-id="8afcc-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span><span class="sxs-lookup"><span data-stu-id="8afcc-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* [<span data-ttu-id="8afcc-136">Secure access to a lab</span><span class="sxs-lookup"><span data-stu-id="8afcc-136">Secure access to a lab</span></span>](devtest-lab-add-devtest-user.md)
* [<span data-ttu-id="8afcc-137">Set lab policies</span><span class="sxs-lookup"><span data-stu-id="8afcc-137">Set lab policies</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="8afcc-138">Create a lab template</span><span class="sxs-lookup"><span data-stu-id="8afcc-138">Create a lab template</span></span>](devtest-lab-create-template.md)
* [<span data-ttu-id="8afcc-139">Create custom artifacts for your VMs</span><span class="sxs-lookup"><span data-stu-id="8afcc-139">Create custom artifacts for your VMs</span></span>](devtest-lab-artifact-author.md)
* [<span data-ttu-id="8afcc-140">Add a VM to a lab</span><span class="sxs-lookup"><span data-stu-id="8afcc-140">Add a VM to a lab</span></span>](devtest-lab-add-vm.md)

