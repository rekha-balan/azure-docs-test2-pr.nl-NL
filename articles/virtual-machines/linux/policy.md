---
title: Enforce security with policies on Linux VMs in Azure | Microsoft Docs
description: How to apply a policy to an Azure Resource Manager Linux Virtual Machine
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 1456c3b48e044bd264a9d9bdb39c1c2408407923
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779407"
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="c7e16-103">Apply policies to Linux VMs with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7e16-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="c7e16-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span><span class="sxs-lookup"><span data-stu-id="c7e16-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="c7e16-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span><span class="sxs-lookup"><span data-stu-id="c7e16-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="c7e16-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="c7e16-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="c7e16-107">For an introduction to policies, see [What is Azure Policy?](../../azure-policy/azure-policy-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7e16-107">For an introduction to policies, see [What is Azure Policy?](../../azure-policy/azure-policy-introduction.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="c7e16-108">Permitted Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c7e16-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="c7e16-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span><span class="sxs-lookup"><span data-stu-id="c7e16-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="c7e16-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span><span class="sxs-lookup"><span data-stu-id="c7e16-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="c7e16-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span><span class="sxs-lookup"><span data-stu-id="c7e16-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="c7e16-112">For information about policy fields, see [Policy aliases](../../azure-policy/policy-definition.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="c7e16-112">For information about policy fields, see [Policy aliases](../../azure-policy/policy-definition.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="c7e16-113">Managed disks</span><span class="sxs-lookup"><span data-stu-id="c7e16-113">Managed disks</span></span>

<span data-ttu-id="c7e16-114">To require the use of managed disks, use the following policy:</span><span class="sxs-lookup"><span data-stu-id="c7e16-114">To require the use of managed disks, use the following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="c7e16-115">Images for Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c7e16-115">Images for Virtual Machines</span></span>

<span data-ttu-id="c7e16-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span><span class="sxs-lookup"><span data-stu-id="c7e16-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="c7e16-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span><span class="sxs-lookup"><span data-stu-id="c7e16-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="c7e16-118">The following example requires images from an approved resource group:</span><span class="sxs-lookup"><span data-stu-id="c7e16-118">The following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="c7e16-119">The following example specifies the approved image IDs:</span><span class="sxs-lookup"><span data-stu-id="c7e16-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="c7e16-120">Virtual Machine extensions</span><span class="sxs-lookup"><span data-stu-id="c7e16-120">Virtual Machine extensions</span></span>

<span data-ttu-id="c7e16-121">You may want to forbid usage of certain types of extensions.</span><span class="sxs-lookup"><span data-stu-id="c7e16-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="c7e16-122">For example, an extension may not be compatible with certain custom virtual machine images.</span><span class="sxs-lookup"><span data-stu-id="c7e16-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="c7e16-123">The following example shows how to block a specific extension.</span><span class="sxs-lookup"><span data-stu-id="c7e16-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="c7e16-124">It uses publisher and type to determine which extension to block.</span><span class="sxs-lookup"><span data-stu-id="c7e16-124">It uses publisher and type to determine which extension to block.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="c7e16-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7e16-125">Next steps</span></span>
* <span data-ttu-id="c7e16-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span><span class="sxs-lookup"><span data-stu-id="c7e16-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="c7e16-127">The scope can be a subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="c7e16-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="c7e16-128">To assign policies, see [Use Azure portal to assign and manage resource policies](../../azure-policy/assign-policy-definition.md), [Use PowerShell to assign policies](../../azure-policy/assign-policy-definition-ps.md), or [Use Azure CLI to assign policies](../../azure-policy/assign-policy-definition-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c7e16-128">To assign policies, see [Use Azure portal to assign and manage resource policies](../../azure-policy/assign-policy-definition.md), [Use PowerShell to assign policies](../../azure-policy/assign-policy-definition-ps.md), or [Use Azure CLI to assign policies](../../azure-policy/assign-policy-definition-cli.md).</span></span>
* <span data-ttu-id="c7e16-129">For an introduction to resource policies, see [What is Azure Policy?](../../azure-policy/azure-policy-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7e16-129">For an introduction to resource policies, see [What is Azure Policy?](../../azure-policy/azure-policy-introduction.md).</span></span>
* <span data-ttu-id="c7e16-130">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span><span class="sxs-lookup"><span data-stu-id="c7e16-130">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span></span>
