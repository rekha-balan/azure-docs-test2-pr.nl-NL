---
title: Azure Resource Manager template outputs | Microsoft Docs
description: Describes how to define outputs for an Azure Resource Manager templates using declarative JSON syntax.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/14/2017
ms.author: tomfitz
ms.openlocfilehash: e3c5a581b02f1dd7b7415ebd93de0e425ac2f8ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966157"
---
# <a name="outputs-section-in-azure-resource-manager-templates"></a><span data-ttu-id="b845f-103">Outputs section in Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="b845f-103">Outputs section in Azure Resource Manager templates</span></span>
<span data-ttu-id="b845f-104">In the Outputs section, you specify values that are returned from deployment.</span><span class="sxs-lookup"><span data-stu-id="b845f-104">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="b845f-105">For example, you could return the URI to access a deployed resource.</span><span class="sxs-lookup"><span data-stu-id="b845f-105">For example, you could return the URI to access a deployed resource.</span></span>

## <a name="define-and-use-output-values"></a><span data-ttu-id="b845f-106">Define and use output values</span><span class="sxs-lookup"><span data-stu-id="b845f-106">Define and use output values</span></span>

<span data-ttu-id="b845f-107">The following example shows how to return the resource ID for a public IP address:</span><span class="sxs-lookup"><span data-stu-id="b845f-107">The following example shows how to return the resource ID for a public IP address:</span></span>

```json
"outputs": {
  "resourceID": {
    "type": "string",
    "value": "[resourceId('Microsoft.Network/publicIPAddresses', parameters('publicIPAddresses_name'))]"
  }
}
```

<span data-ttu-id="b845f-108">After the deployment, you can retrieve the value with script.</span><span class="sxs-lookup"><span data-stu-id="b845f-108">After the deployment, you can retrieve the value with script.</span></span> <span data-ttu-id="b845f-109">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="b845f-109">For PowerShell, use:</span></span>

```powershell
(Get-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -Name <deployment-name>).Outputs.resourceID.value
```

<span data-ttu-id="b845f-110">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="b845f-110">For Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment show -g <resource-group-name> -n <deployment-name> --query properties.outputs.resourceID.value
```

<span data-ttu-id="b845f-111">You can retrieve the output value from a linked template by using the [reference](resource-group-template-functions-resource.md#reference) function.</span><span class="sxs-lookup"><span data-stu-id="b845f-111">You can retrieve the output value from a linked template by using the [reference](resource-group-template-functions-resource.md#reference) function.</span></span> <span data-ttu-id="b845f-112">To get an output value from a linked template, retrieve the property value with syntax like: `"[reference('<name-of-deployment>').outputs.<property-name>.value]"`.</span><span class="sxs-lookup"><span data-stu-id="b845f-112">To get an output value from a linked template, retrieve the property value with syntax like: `"[reference('<name-of-deployment>').outputs.<property-name>.value]"`.</span></span>

<span data-ttu-id="b845f-113">For example, you can set the IP address on a load balancer by retrieving a value from a linked template.</span><span class="sxs-lookup"><span data-stu-id="b845f-113">For example, you can set the IP address on a load balancer by retrieving a value from a linked template.</span></span>

```json
"publicIPAddress": {
    "id": "[reference('linkedTemplate').outputs.resourceID.value]"
}
```

<span data-ttu-id="b845f-114">You cannot use the `reference` function in the outputs section of a [nested template](resource-group-linked-templates.md#link-or-nest-a-template).</span><span class="sxs-lookup"><span data-stu-id="b845f-114">You cannot use the `reference` function in the outputs section of a [nested template](resource-group-linked-templates.md#link-or-nest-a-template).</span></span> <span data-ttu-id="b845f-115">To return the values for a deployed resource in a nested template, convert your nested template to a linked template.</span><span class="sxs-lookup"><span data-stu-id="b845f-115">To return the values for a deployed resource in a nested template, convert your nested template to a linked template.</span></span>

## <a name="available-properties"></a><span data-ttu-id="b845f-116">Available properties</span><span class="sxs-lookup"><span data-stu-id="b845f-116">Available properties</span></span>

<span data-ttu-id="b845f-117">The following example shows the structure of an output definition:</span><span class="sxs-lookup"><span data-stu-id="b845f-117">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="b845f-118">Element name</span><span class="sxs-lookup"><span data-stu-id="b845f-118">Element name</span></span> | <span data-ttu-id="b845f-119">Required</span><span class="sxs-lookup"><span data-stu-id="b845f-119">Required</span></span> | <span data-ttu-id="b845f-120">Description</span><span class="sxs-lookup"><span data-stu-id="b845f-120">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b845f-121">outputName</span><span class="sxs-lookup"><span data-stu-id="b845f-121">outputName</span></span> |<span data-ttu-id="b845f-122">Yes</span><span class="sxs-lookup"><span data-stu-id="b845f-122">Yes</span></span> |<span data-ttu-id="b845f-123">Name of the output value.</span><span class="sxs-lookup"><span data-stu-id="b845f-123">Name of the output value.</span></span> <span data-ttu-id="b845f-124">Must be a valid JavaScript identifier.</span><span class="sxs-lookup"><span data-stu-id="b845f-124">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="b845f-125">type</span><span class="sxs-lookup"><span data-stu-id="b845f-125">type</span></span> |<span data-ttu-id="b845f-126">Yes</span><span class="sxs-lookup"><span data-stu-id="b845f-126">Yes</span></span> |<span data-ttu-id="b845f-127">Type of the output value.</span><span class="sxs-lookup"><span data-stu-id="b845f-127">Type of the output value.</span></span> <span data-ttu-id="b845f-128">Output values support the same types as template input parameters.</span><span class="sxs-lookup"><span data-stu-id="b845f-128">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="b845f-129">value</span><span class="sxs-lookup"><span data-stu-id="b845f-129">value</span></span> |<span data-ttu-id="b845f-130">Yes</span><span class="sxs-lookup"><span data-stu-id="b845f-130">Yes</span></span> |<span data-ttu-id="b845f-131">Template language expression that is evaluated and returned as output value.</span><span class="sxs-lookup"><span data-stu-id="b845f-131">Template language expression that is evaluated and returned as output value.</span></span> |

## <a name="recommendations"></a><span data-ttu-id="b845f-132">Recommendations</span><span class="sxs-lookup"><span data-stu-id="b845f-132">Recommendations</span></span>

<span data-ttu-id="b845f-133">If you use a template to create public IP addresses, include an outputs section that returns details of the IP address and the fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="b845f-133">If you use a template to create public IP addresses, include an outputs section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="b845f-134">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span><span class="sxs-lookup"><span data-stu-id="b845f-134">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span>

```json
"outputs": {
    "fqdn": {
        "value": "[reference(parameters('publicIPAddresses_name')).dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(parameters('publicIPAddresses_name')).ipAddress]",
        "type": "string"
    }
}
```

## <a name="example-templates"></a><span data-ttu-id="b845f-135">Example templates</span><span class="sxs-lookup"><span data-stu-id="b845f-135">Example templates</span></span>


|<span data-ttu-id="b845f-136">Template</span><span class="sxs-lookup"><span data-stu-id="b845f-136">Template</span></span>  |<span data-ttu-id="b845f-137">Description</span><span class="sxs-lookup"><span data-stu-id="b845f-137">Description</span></span>  |
|---------|---------|
|[<span data-ttu-id="b845f-138">Copy variables</span><span class="sxs-lookup"><span data-stu-id="b845f-138">Copy variables</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/copyvariables.json) | <span data-ttu-id="b845f-139">Creates complex variables and outputs those values.</span><span class="sxs-lookup"><span data-stu-id="b845f-139">Creates complex variables and outputs those values.</span></span> <span data-ttu-id="b845f-140">Does not deploy any resources.</span><span class="sxs-lookup"><span data-stu-id="b845f-140">Does not deploy any resources.</span></span> |
|[<span data-ttu-id="b845f-141">Public IP address</span><span class="sxs-lookup"><span data-stu-id="b845f-141">Public IP address</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/linkedtemplates/public-ip.json) | <span data-ttu-id="b845f-142">Creates a public IP address and outputs the resource ID.</span><span class="sxs-lookup"><span data-stu-id="b845f-142">Creates a public IP address and outputs the resource ID.</span></span> |
|[<span data-ttu-id="b845f-143">Load balancer</span><span class="sxs-lookup"><span data-stu-id="b845f-143">Load balancer</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/linkedtemplates/public-ip-parentloadbalancer.json) | <span data-ttu-id="b845f-144">Links to the preceding template.</span><span class="sxs-lookup"><span data-stu-id="b845f-144">Links to the preceding template.</span></span> <span data-ttu-id="b845f-145">Uses the resource ID in the output when creating the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b845f-145">Uses the resource ID in the output when creating the load balancer.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b845f-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="b845f-146">Next steps</span></span>
* <span data-ttu-id="b845f-147">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="b845f-147">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="b845f-148">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="b845f-148">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="b845f-149">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b845f-149">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="b845f-150">You may need to use resources that exist within a different resource group.</span><span class="sxs-lookup"><span data-stu-id="b845f-150">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="b845f-151">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span><span class="sxs-lookup"><span data-stu-id="b845f-151">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="b845f-152">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="b845f-152">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>