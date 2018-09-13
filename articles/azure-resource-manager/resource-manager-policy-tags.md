---
title: Azure resource policies for tags | Microsoft Docs
description: Provides examples of resource policies for managing tags on resources
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
ms.openlocfilehash: 6e71fd9eda822478fa0555aa44908a4094fe8de2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662338"
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="777dd-103">Apply resource policies for tags</span><span class="sxs-lookup"><span data-stu-id="777dd-103">Apply resource policies for tags</span></span>

<span data-ttu-id="777dd-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span><span class="sxs-lookup"><span data-stu-id="777dd-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="777dd-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span><span class="sxs-lookup"><span data-stu-id="777dd-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="777dd-106">To enforce the policies on those resources, trigger an update to the existing resources, as shown in [Trigger updates to existing resources](#trigger-updates-to-existing-resources).</span><span class="sxs-lookup"><span data-stu-id="777dd-106">To enforce the policies on those resources, trigger an update to the existing resources, as shown in [Trigger updates to existing resources](#trigger-updates-to-existing-resources).</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="777dd-107">Ensure all resources in a resource group have a tag/value</span><span class="sxs-lookup"><span data-stu-id="777dd-107">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="777dd-108">A common requirement is that all resources in a resource group have a particular tag and value.</span><span class="sxs-lookup"><span data-stu-id="777dd-108">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="777dd-109">This requirement is often needed to track costs by department.</span><span class="sxs-lookup"><span data-stu-id="777dd-109">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="777dd-110">The following conditions must be met:</span><span class="sxs-lookup"><span data-stu-id="777dd-110">The following conditions must be met:</span></span>

* <span data-ttu-id="777dd-111">The required tag and value are appended to new and updated resources that do not have any existing tags.</span><span class="sxs-lookup"><span data-stu-id="777dd-111">The required tag and value are appended to new and updated resources that do not have any existing tags.</span></span>
* <span data-ttu-id="777dd-112">The required tag and value are appended to new and updated resources that have other tags, but not the required tag and value.</span><span class="sxs-lookup"><span data-stu-id="777dd-112">The required tag and value are appended to new and updated resources that have other tags, but not the required tag and value.</span></span>
* <span data-ttu-id="777dd-113">The required tag and value cannot be removed from any existing resources.</span><span class="sxs-lookup"><span data-stu-id="777dd-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="777dd-114">You accomplish this requirement by applying to a resource group the following three policies:</span><span class="sxs-lookup"><span data-stu-id="777dd-114">You accomplish this requirement by applying to a resource group the following three policies:</span></span>

* [<span data-ttu-id="777dd-115">Append tag</span><span class="sxs-lookup"><span data-stu-id="777dd-115">Append tag</span></span>](#append-tag) 
* [<span data-ttu-id="777dd-116">Append tag with other tags</span><span class="sxs-lookup"><span data-stu-id="777dd-116">Append tag with other tags</span></span>](#append-tag-with-other-tags)
* [<span data-ttu-id="777dd-117">Require tag and value</span><span class="sxs-lookup"><span data-stu-id="777dd-117">Require tag and value</span></span>](#require-tag-and-value)

### <a name="append-tag"></a><span data-ttu-id="777dd-118">Append tag</span><span class="sxs-lookup"><span data-stu-id="777dd-118">Append tag</span></span>

<span data-ttu-id="777dd-119">The following policy rule appends costCenter tag with a predefined value when no tags are present:</span><span class="sxs-lookup"><span data-stu-id="777dd-119">The following policy rule appends costCenter tag with a predefined value when no tags are present:</span></span>

```json
{
  "if": {
    "field": "tags",
    "exists": "false"
  },
  "then": {
    "effect": "append",
    "details": [
      {
        "field": "tags",
        "value": {"costCenter":"myDepartment" }
      }
    ]
  }
}
```

### <a name="append-tag-with-other-tags"></a><span data-ttu-id="777dd-120">Append tag with other tags</span><span class="sxs-lookup"><span data-stu-id="777dd-120">Append tag with other tags</span></span>

<span data-ttu-id="777dd-121">The following policy rule appends costCenter tag with a predefined value when tags are present, but the costCenter tag is not defined:</span><span class="sxs-lookup"><span data-stu-id="777dd-121">The following policy rule appends costCenter tag with a predefined value when tags are present, but the costCenter tag is not defined:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "tags",
        "exists": "true"
      },
      {
        "field": "tags.costCenter",
        "exists": "false"
      }
    ]
  },
  "then": {
    "effect": "append",
    "details": [
      {
        "field": "tags.costCenter",
        "value": "myDepartment"
      }
    ]
  }
}
```

### <a name="require-tag-and-value"></a><span data-ttu-id="777dd-122">Require tag and value</span><span class="sxs-lookup"><span data-stu-id="777dd-122">Require tag and value</span></span>

<span data-ttu-id="777dd-123">The following policy rule denies update or creation of resources that do not have the costCenter tag assigned to the predefined value.</span><span class="sxs-lookup"><span data-stu-id="777dd-123">The following policy rule denies update or creation of resources that do not have the costCenter tag assigned to the predefined value.</span></span>

```json
{
  "if": {
    "not": {
      "field": "tags.costCenter",
      "equals": "myDepartment"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="777dd-124">Require tags for a resource type</span><span class="sxs-lookup"><span data-stu-id="777dd-124">Require tags for a resource type</span></span>
<span data-ttu-id="777dd-125">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span><span class="sxs-lookup"><span data-stu-id="777dd-125">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="777dd-126">Require tag</span><span class="sxs-lookup"><span data-stu-id="777dd-126">Require tag</span></span>
<span data-ttu-id="777dd-127">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span><span class="sxs-lookup"><span data-stu-id="777dd-127">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="trigger-updates-to-existing-resources"></a><span data-ttu-id="777dd-128">Trigger updates to existing resources</span><span class="sxs-lookup"><span data-stu-id="777dd-128">Trigger updates to existing resources</span></span>

<span data-ttu-id="777dd-129">The following PowerShell script triggers an update to existing resources to enforce tag policies you have added.</span><span class="sxs-lookup"><span data-stu-id="777dd-129">The following PowerShell script triggers an update to existing resources to enforce tag policies you have added.</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($_.Tags -eq $NULL) { @{}} else {$_.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="777dd-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="777dd-130">Next steps</span></span>
* <span data-ttu-id="777dd-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span><span class="sxs-lookup"><span data-stu-id="777dd-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="777dd-132">The scope can be a subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="777dd-132">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="777dd-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="777dd-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="777dd-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="777dd-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="777dd-135">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="777dd-135">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="777dd-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="777dd-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

