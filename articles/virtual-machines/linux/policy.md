---
title: Enforce security with policies on Linux VMs in Azure | Microsoft Docs
description: How to apply a policy to an Azure Resource Manager Linux Virtual Machine
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/13/2016
ms.author: singhkay
ms.openlocfilehash: bde2bcc335db33301fa474331043086b8b282052
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563079"
---
# <a name="apply-security-and-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="0fc0e-103">Apply security and policies to Linux VMs with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0fc0e-103">Apply security and policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="0fc0e-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="0fc0e-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="0fc0e-106">In this article, we will describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-106">In this article, we will describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="0fc0e-107">The outline for the steps to accomplish this is as below</span><span class="sxs-lookup"><span data-stu-id="0fc0e-107">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="0fc0e-108">Azure Resource Manager Policy 101</span><span class="sxs-lookup"><span data-stu-id="0fc0e-108">Azure Resource Manager Policy 101</span></span>
2. <span data-ttu-id="0fc0e-109">Define a policy for your Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="0fc0e-109">Define a policy for your Virtual Machine</span></span>
3. <span data-ttu-id="0fc0e-110">Create the policy</span><span class="sxs-lookup"><span data-stu-id="0fc0e-110">Create the policy</span></span>
4. <span data-ttu-id="0fc0e-111">Apply the policy</span><span class="sxs-lookup"><span data-stu-id="0fc0e-111">Apply the policy</span></span>

## <a name="azure-resource-manager-policy-101"></a><span data-ttu-id="0fc0e-112">Azure Resource Manager Policy 101</span><span class="sxs-lookup"><span data-stu-id="0fc0e-112">Azure Resource Manager Policy 101</span></span>
<span data-ttu-id="0fc0e-113">For getting started with Azure Resource Manager policies, we recommend reading the article below and then continuing with the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-113">For getting started with Azure Resource Manager policies, we recommend reading the article below and then continuing with the steps in this article.</span></span> <span data-ttu-id="0fc0e-114">The article below describes the basic definition and structure of a policy, how policies get evaluated and gives various examples of policy definitions.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-114">The article below describes the basic definition and structure of a policy, how policies get evaluated and gives various examples of policy definitions.</span></span>

* [<span data-ttu-id="0fc0e-115">Use Policy to manage resources and control access</span><span class="sxs-lookup"><span data-stu-id="0fc0e-115">Use Policy to manage resources and control access</span></span>](../../azure-resource-manager/resource-manager-policy.md)

## <a name="define-a-policy-for-your-virtual-machine"></a><span data-ttu-id="0fc0e-116">Define a policy for your Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="0fc0e-116">Define a policy for your Virtual Machine</span></span>
<span data-ttu-id="0fc0e-117">One of the common scenarios for an enterprise might be to only allow their users to create Virtual Machines from specific operating systems that have been tested to be compatible with a LOB application.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-117">One of the common scenarios for an enterprise might be to only allow their users to create Virtual Machines from specific operating systems that have been tested to be compatible with a LOB application.</span></span> <span data-ttu-id="0fc0e-118">Using an Azure Resource Manager policy this task can be accomplished in a few steps.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-118">Using an Azure Resource Manager policy this task can be accomplished in a few steps.</span></span>
<span data-ttu-id="0fc0e-119">In this policy example, we are going to allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-119">In this policy example, we are going to allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span> <span data-ttu-id="0fc0e-120">The policy definition looks like below</span><span class="sxs-lookup"><span data-stu-id="0fc0e-120">The policy definition looks like below</span></span>

```
"if": {
  "allOf": [
    {
      "field": "type",
      "equals": "Microsoft.Compute/virtualMachines"
    },
    {
      "not": {
        "allOf": [
          {
            "field": "Microsoft.Compute/virtualMachines/imagePublisher",
            "equals": "Canonical"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageOffer",
            "equals": "UbuntuServer"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageSku",
            "equals": "14.04.2-LTS"
          }
        ]
      }
    }
  ]
},
"then": {
  "effect": "deny"
}
```

<span data-ttu-id="0fc0e-121">The above policy can easily be modified to a scenario where you might want to allow any Ubuntu LTS image to be used for a Virtual Machine deployment with the below change</span><span class="sxs-lookup"><span data-stu-id="0fc0e-121">The above policy can easily be modified to a scenario where you might want to allow any Ubuntu LTS image to be used for a Virtual Machine deployment with the below change</span></span>

```
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

#### <a name="virtual-machine-property-fields"></a><span data-ttu-id="0fc0e-122">Virtual Machine Property Fields</span><span class="sxs-lookup"><span data-stu-id="0fc0e-122">Virtual Machine Property Fields</span></span>
<span data-ttu-id="0fc0e-123">The table below describes the Virtual Machine properties that can be used as fields in your policy definition.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-123">The table below describes the Virtual Machine properties that can be used as fields in your policy definition.</span></span> <span data-ttu-id="0fc0e-124">For more information about policy fields, see [Use policy to manage resources and control access](../../resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0fc0e-124">For more information about policy fields, see [Use policy to manage resources and control access](../../resource-manager-policy.md).</span></span>

| <span data-ttu-id="0fc0e-125">Field Name</span><span class="sxs-lookup"><span data-stu-id="0fc0e-125">Field Name</span></span> | <span data-ttu-id="0fc0e-126">Description</span><span class="sxs-lookup"><span data-stu-id="0fc0e-126">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0fc0e-127">imagePublisher</span><span class="sxs-lookup"><span data-stu-id="0fc0e-127">imagePublisher</span></span> |<span data-ttu-id="0fc0e-128">Specifies the publisher of the image</span><span class="sxs-lookup"><span data-stu-id="0fc0e-128">Specifies the publisher of the image</span></span> |
| <span data-ttu-id="0fc0e-129">imageOffer</span><span class="sxs-lookup"><span data-stu-id="0fc0e-129">imageOffer</span></span> |<span data-ttu-id="0fc0e-130">Specifies the offer for the chosen image publisher</span><span class="sxs-lookup"><span data-stu-id="0fc0e-130">Specifies the offer for the chosen image publisher</span></span> |
| <span data-ttu-id="0fc0e-131">imageSku</span><span class="sxs-lookup"><span data-stu-id="0fc0e-131">imageSku</span></span> |<span data-ttu-id="0fc0e-132">Specifies the SKU for the chosen offer</span><span class="sxs-lookup"><span data-stu-id="0fc0e-132">Specifies the SKU for the chosen offer</span></span> |
| <span data-ttu-id="0fc0e-133">imageVersion</span><span class="sxs-lookup"><span data-stu-id="0fc0e-133">imageVersion</span></span> |<span data-ttu-id="0fc0e-134">Specifies the image version for the chosen SKU</span><span class="sxs-lookup"><span data-stu-id="0fc0e-134">Specifies the image version for the chosen SKU</span></span> |

## <a name="create-the-policy"></a><span data-ttu-id="0fc0e-135">Create the Policy</span><span class="sxs-lookup"><span data-stu-id="0fc0e-135">Create the Policy</span></span>
<span data-ttu-id="0fc0e-136">A policy can easily be created using the REST API directly or the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-136">A policy can easily be created using the REST API directly or the PowerShell cmdlets.</span></span> <span data-ttu-id="0fc0e-137">You can read more about [creating and assigning a policy](../../resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0fc0e-137">You can read more about [creating and assigning a policy](../../resource-manager-policy.md).</span></span>

## <a name="apply-the-policy"></a><span data-ttu-id="0fc0e-138">Apply the Policy</span><span class="sxs-lookup"><span data-stu-id="0fc0e-138">Apply the Policy</span></span>
<span data-ttu-id="0fc0e-139">After creating the policy you’ll need to apply it on a defined scope.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-139">After creating the policy you’ll need to apply it on a defined scope.</span></span> <span data-ttu-id="0fc0e-140">The scope can be a subscription, resource group or even the resource.</span><span class="sxs-lookup"><span data-stu-id="0fc0e-140">The scope can be a subscription, resource group or even the resource.</span></span> <span data-ttu-id="0fc0e-141">You can read more about [creating and assigning a policy](../../resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0fc0e-141">You can read more about [creating and assigning a policy](../../resource-manager-policy.md).</span></span>
