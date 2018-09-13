---
title: Azure Resource Manager deployment modes | Microsoft Docs
description: Describes how to specify whether to use a complete or incremental deployment mode with Azure Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2018
ms.author: tomfitz
ms.openlocfilehash: c8c6c5499e1cea04bc5bdffbb5c07b53b96182e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867757"
---
# <a name="azure-resource-manager-deployment-modes"></a><span data-ttu-id="c8fa7-103">Azure Resource Manager deployment modes</span><span class="sxs-lookup"><span data-stu-id="c8fa7-103">Azure Resource Manager deployment modes</span></span>
<span data-ttu-id="c8fa7-104">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-104">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span></span>  <span data-ttu-id="c8fa7-105">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that aren't in the template.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-105">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that aren't in the template.</span></span>
<span data-ttu-id="c8fa7-106">The default mode is incremental.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-106">The default mode is incremental.</span></span>

## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="c8fa7-107">Incremental and complete deployments</span><span class="sxs-lookup"><span data-stu-id="c8fa7-107">Incremental and complete deployments</span></span>
<span data-ttu-id="c8fa7-108">When deploying resources:</span><span class="sxs-lookup"><span data-stu-id="c8fa7-108">When deploying resources:</span></span>

* <span data-ttu-id="c8fa7-109">In complete mode, Resource Manager **deletes** resources that exist in the resource group but aren't specified in the template.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-109">In complete mode, Resource Manager **deletes** resources that exist in the resource group but aren't specified in the template.</span></span> 
* <span data-ttu-id="c8fa7-110">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but aren't specified in the template.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-110">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but aren't specified in the template.</span></span>

<span data-ttu-id="c8fa7-111">For both modes, Resource Manager attempts to provision all resources specified in the template.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-111">For both modes, Resource Manager attempts to provision all resources specified in the template.</span></span> <span data-ttu-id="c8fa7-112">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-112">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span></span> <span data-ttu-id="c8fa7-113">If you change the settings for a resource, the resource is provisioned with those new settings.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-113">If you change the settings for a resource, the resource is provisioned with those new settings.</span></span> <span data-ttu-id="c8fa7-114">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-114">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span></span> <span data-ttu-id="c8fa7-115">Instead, deploy a new resource with the location or type that you need.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-115">Instead, deploy a new resource with the location or type that you need.</span></span>

## <a name="example-result"></a><span data-ttu-id="c8fa7-116">Example result</span><span class="sxs-lookup"><span data-stu-id="c8fa7-116">Example result</span></span>

<span data-ttu-id="c8fa7-117">To illustrate the difference between incremental and complete modes, consider the following scenario.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-117">To illustrate the difference between incremental and complete modes, consider the following scenario.</span></span>

<span data-ttu-id="c8fa7-118">**Existing Resource Group** contains:</span><span class="sxs-lookup"><span data-stu-id="c8fa7-118">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="c8fa7-119">Resource A</span><span class="sxs-lookup"><span data-stu-id="c8fa7-119">Resource A</span></span>
* <span data-ttu-id="c8fa7-120">Resource B</span><span class="sxs-lookup"><span data-stu-id="c8fa7-120">Resource B</span></span>
* <span data-ttu-id="c8fa7-121">Resource C</span><span class="sxs-lookup"><span data-stu-id="c8fa7-121">Resource C</span></span>

<span data-ttu-id="c8fa7-122">**Template** defines:</span><span class="sxs-lookup"><span data-stu-id="c8fa7-122">**Template** defines:</span></span>

* <span data-ttu-id="c8fa7-123">Resource A</span><span class="sxs-lookup"><span data-stu-id="c8fa7-123">Resource A</span></span>
* <span data-ttu-id="c8fa7-124">Resource B</span><span class="sxs-lookup"><span data-stu-id="c8fa7-124">Resource B</span></span>
* <span data-ttu-id="c8fa7-125">Resource D</span><span class="sxs-lookup"><span data-stu-id="c8fa7-125">Resource D</span></span>

<span data-ttu-id="c8fa7-126">When deployed in **incremental** mode, the resource group has:</span><span class="sxs-lookup"><span data-stu-id="c8fa7-126">When deployed in **incremental** mode, the resource group has:</span></span>

* <span data-ttu-id="c8fa7-127">Resource A</span><span class="sxs-lookup"><span data-stu-id="c8fa7-127">Resource A</span></span>
* <span data-ttu-id="c8fa7-128">Resource B</span><span class="sxs-lookup"><span data-stu-id="c8fa7-128">Resource B</span></span>
* <span data-ttu-id="c8fa7-129">Resource C</span><span class="sxs-lookup"><span data-stu-id="c8fa7-129">Resource C</span></span>
* <span data-ttu-id="c8fa7-130">Resource D</span><span class="sxs-lookup"><span data-stu-id="c8fa7-130">Resource D</span></span>

<span data-ttu-id="c8fa7-131">When deployed in **complete** mode, Resource C is deleted.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-131">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="c8fa7-132">The resource group has:</span><span class="sxs-lookup"><span data-stu-id="c8fa7-132">The resource group has:</span></span>

* <span data-ttu-id="c8fa7-133">Resource A</span><span class="sxs-lookup"><span data-stu-id="c8fa7-133">Resource A</span></span>
* <span data-ttu-id="c8fa7-134">Resource B</span><span class="sxs-lookup"><span data-stu-id="c8fa7-134">Resource B</span></span>
* <span data-ttu-id="c8fa7-135">Resource D</span><span class="sxs-lookup"><span data-stu-id="c8fa7-135">Resource D</span></span>

## <a name="set-deployment-mode"></a><span data-ttu-id="c8fa7-136">Set deployment mode</span><span class="sxs-lookup"><span data-stu-id="c8fa7-136">Set deployment mode</span></span>

<span data-ttu-id="c8fa7-137">To set the deployment mode when deploying with PowerShell, use the `Mode` parameter.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-137">To set the deployment mode when deploying with PowerShell, use the `Mode` parameter.</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Mode Complete `
  -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json 
```

<span data-ttu-id="c8fa7-138">To set the deployment mode when deploying with Azure CLI, use the `mode` parameter.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-138">To set the deployment mode when deploying with Azure CLI, use the `mode` parameter.</span></span>

```azurecli-interactive
az group deployment create \
  --name ExampleDeployment \
  --mode Complete \
  --resource-group ExampleGroup \
  --template-file storage.json \
  --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="c8fa7-139">When using a [linked or nested template](resource-group-linked-templates.md), you must set the `mode` property to `Incremental`.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-139">When using a [linked or nested template](resource-group-linked-templates.md), you must set the `mode` property to `Incremental`.</span></span> <span data-ttu-id="c8fa7-140">Only root-level templates support the complete deployment mode.</span><span class="sxs-lookup"><span data-stu-id="c8fa7-140">Only root-level templates support the complete deployment mode.</span></span>

```json
"resources": [
  {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          <nested-template-or-external-template>
      }
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="c8fa7-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8fa7-141">Next steps</span></span>
* <span data-ttu-id="c8fa7-142">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c8fa7-142">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c8fa7-143">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c8fa7-143">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="c8fa7-144">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="c8fa7-144">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

