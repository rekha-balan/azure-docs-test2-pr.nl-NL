---
title: Enforce security with policies on Windows VMs in Azure | Microsoft Docs
description: How to apply a policy to an Azure Resource Manager Windows Virtual Machine
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/13/2016
ms.author: kasing
ms.openlocfilehash: 6c91d47b11fa18ead0076c470930e8c4e5537784
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553791"
---
# <a name="apply-security-and-policies-to-windows-vms-with-azure-resource-manager"></a><span data-ttu-id="8f742-103">Apply security and policies to Windows VMs with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f742-103">Apply security and policies to Windows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="8f742-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span><span class="sxs-lookup"><span data-stu-id="8f742-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="8f742-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span><span class="sxs-lookup"><span data-stu-id="8f742-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="8f742-106">In this article, we will describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="8f742-106">In this article, we will describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="8f742-107">The outline for the steps to accomplish this is as below</span><span class="sxs-lookup"><span data-stu-id="8f742-107">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="8f742-108">Azure Resource Manager Policy 101</span><span class="sxs-lookup"><span data-stu-id="8f742-108">Azure Resource Manager Policy 101</span></span>
2. <span data-ttu-id="8f742-109">Define a policy for your Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="8f742-109">Define a policy for your Virtual Machine</span></span>
3. <span data-ttu-id="8f742-110">Create the policy</span><span class="sxs-lookup"><span data-stu-id="8f742-110">Create the policy</span></span>
4. <span data-ttu-id="8f742-111">Apply the policy</span><span class="sxs-lookup"><span data-stu-id="8f742-111">Apply the policy</span></span>

## <a name="azure-resource-manager-policy-101"></a><span data-ttu-id="8f742-112">Azure Resource Manager Policy 101</span><span class="sxs-lookup"><span data-stu-id="8f742-112">Azure Resource Manager Policy 101</span></span>
<span data-ttu-id="8f742-113">For getting started with Azure Resource Manager policies, we recommend reading the article below and then continuing with the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="8f742-113">For getting started with Azure Resource Manager policies, we recommend reading the article below and then continuing with the steps in this article.</span></span> <span data-ttu-id="8f742-114">The article below describes the basic definition and structure of a policy, how policies get evaluated and gives various examples of policy definitions.</span><span class="sxs-lookup"><span data-stu-id="8f742-114">The article below describes the basic definition and structure of a policy, how policies get evaluated and gives various examples of policy definitions.</span></span>

* [<span data-ttu-id="8f742-115">Use Policy to manage resources and control access</span><span class="sxs-lookup"><span data-stu-id="8f742-115">Use Policy to manage resources and control access</span></span>](../../resource-manager-policy.md)

## <a name="define-a-policy-for-your-virtual-machine"></a><span data-ttu-id="8f742-116">Define a policy for your Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="8f742-116">Define a policy for your Virtual Machine</span></span>
<span data-ttu-id="8f742-117">One of the common scenarios for an enterprise might be to only allow their users to create Virtual Machines from specific operating systems that have been tested to be compatible with a LOB application.</span><span class="sxs-lookup"><span data-stu-id="8f742-117">One of the common scenarios for an enterprise might be to only allow their users to create Virtual Machines from specific operating systems that have been tested to be compatible with a LOB application.</span></span> <span data-ttu-id="8f742-118">Using an Azure Resource Manager policy this task can be accomplished in a few steps.</span><span class="sxs-lookup"><span data-stu-id="8f742-118">Using an Azure Resource Manager policy this task can be accomplished in a few steps.</span></span>
<span data-ttu-id="8f742-119">In this policy example, we are going to allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created.</span><span class="sxs-lookup"><span data-stu-id="8f742-119">In this policy example, we are going to allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created.</span></span> <span data-ttu-id="8f742-120">The policy definition looks like below</span><span class="sxs-lookup"><span data-stu-id="8f742-120">The policy definition looks like below</span></span>

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
            "equals": "MicrosoftWindowsServer"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageOffer",
            "equals": "WindowsServer"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageSku",
            "equals": "2012-R2-Datacenter"
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

<span data-ttu-id="8f742-121">The above policy can easily be modified to a scenario where you might want to allow any Windows Server Datacenter image to be used for a Virtual Machine deployment with the below change</span><span class="sxs-lookup"><span data-stu-id="8f742-121">The above policy can easily be modified to a scenario where you might want to allow any Windows Server Datacenter image to be used for a Virtual Machine deployment with the below change</span></span>

```
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*Datacenter"
}
```

#### <a name="virtual-machine-property-fields"></a><span data-ttu-id="8f742-122">Virtual Machine Property Fields</span><span class="sxs-lookup"><span data-stu-id="8f742-122">Virtual Machine Property Fields</span></span>
<span data-ttu-id="8f742-123">The table below describes the Virtual Machine properties that can be used as fields in your policy definition.</span><span class="sxs-lookup"><span data-stu-id="8f742-123">The table below describes the Virtual Machine properties that can be used as fields in your policy definition.</span></span> <span data-ttu-id="8f742-124">For more on policy fields, see the article below:</span><span class="sxs-lookup"><span data-stu-id="8f742-124">For more on policy fields, see the article below:</span></span>

* [<span data-ttu-id="8f742-125">Fields and Sources</span><span class="sxs-lookup"><span data-stu-id="8f742-125">Fields and Sources</span></span>](../../azure-resource-manager/resource-manager-policy.md#conditions)

| <span data-ttu-id="8f742-126">Field Name</span><span class="sxs-lookup"><span data-stu-id="8f742-126">Field Name</span></span> | <span data-ttu-id="8f742-127">Description</span><span class="sxs-lookup"><span data-stu-id="8f742-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f742-128">imagePublisher</span><span class="sxs-lookup"><span data-stu-id="8f742-128">imagePublisher</span></span> |<span data-ttu-id="8f742-129">Specifies the publisher of the image</span><span class="sxs-lookup"><span data-stu-id="8f742-129">Specifies the publisher of the image</span></span> |
| <span data-ttu-id="8f742-130">imageOffer</span><span class="sxs-lookup"><span data-stu-id="8f742-130">imageOffer</span></span> |<span data-ttu-id="8f742-131">Specifies the offer for the chosen image publisher</span><span class="sxs-lookup"><span data-stu-id="8f742-131">Specifies the offer for the chosen image publisher</span></span> |
| <span data-ttu-id="8f742-132">imageSku</span><span class="sxs-lookup"><span data-stu-id="8f742-132">imageSku</span></span> |<span data-ttu-id="8f742-133">Specifies the SKU for the chosen offer</span><span class="sxs-lookup"><span data-stu-id="8f742-133">Specifies the SKU for the chosen offer</span></span> |
| <span data-ttu-id="8f742-134">imageVersion</span><span class="sxs-lookup"><span data-stu-id="8f742-134">imageVersion</span></span> |<span data-ttu-id="8f742-135">Specifies the image version for the chosen SKU</span><span class="sxs-lookup"><span data-stu-id="8f742-135">Specifies the image version for the chosen SKU</span></span> |

## <a name="create-the-policy"></a><span data-ttu-id="8f742-136">Create the Policy</span><span class="sxs-lookup"><span data-stu-id="8f742-136">Create the Policy</span></span>
<span data-ttu-id="8f742-137">A policy can easily be created using the REST API directly or the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8f742-137">A policy can easily be created using the REST API directly or the PowerShell cmdlets.</span></span> <span data-ttu-id="8f742-138">For creating the policy, see the article below:</span><span class="sxs-lookup"><span data-stu-id="8f742-138">For creating the policy, see the article below:</span></span>

* [<span data-ttu-id="8f742-139">Creating a Policy</span><span class="sxs-lookup"><span data-stu-id="8f742-139">Creating a Policy</span></span>](../../resource-manager-policy.md)

## <a name="apply-the-policy"></a><span data-ttu-id="8f742-140">Apply the Policy</span><span class="sxs-lookup"><span data-stu-id="8f742-140">Apply the Policy</span></span>
<span data-ttu-id="8f742-141">After creating the policy you’ll need to apply it on a defined scope.</span><span class="sxs-lookup"><span data-stu-id="8f742-141">After creating the policy you’ll need to apply it on a defined scope.</span></span> <span data-ttu-id="8f742-142">The scope can be a subscription, resource group or even the resource.</span><span class="sxs-lookup"><span data-stu-id="8f742-142">The scope can be a subscription, resource group or even the resource.</span></span> <span data-ttu-id="8f742-143">For applying the policy, see the article below:</span><span class="sxs-lookup"><span data-stu-id="8f742-143">For applying the policy, see the article below:</span></span>

* [<span data-ttu-id="8f742-144">Creating a Policy</span><span class="sxs-lookup"><span data-stu-id="8f742-144">Creating a Policy</span></span>](../../resource-manager-policy.md)
