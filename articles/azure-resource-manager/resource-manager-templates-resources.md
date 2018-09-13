---
title: Azure Resource Manager template resources | Microsoft Docs
description: Describes the resources section of Azure Resource Manager templates using declarative JSON syntax.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2018
ms.author: tomfitz
ms.openlocfilehash: 6723cf8cc18637c157b295361425357e1c47ec2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968170"
---
# <a name="resources-section-of-azure-resource-manager-templates"></a><span data-ttu-id="400d8-103">Resources section of Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="400d8-103">Resources section of Azure Resource Manager templates</span></span>

<span data-ttu-id="400d8-104">In the resources section, you define the resources that are deployed or updated.</span><span class="sxs-lookup"><span data-stu-id="400d8-104">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="400d8-105">This section can get complicated because you must understand the types you're deploying to provide the right values.</span><span class="sxs-lookup"><span data-stu-id="400d8-105">This section can get complicated because you must understand the types you're deploying to provide the right values.</span></span>

## <a name="available-properties"></a><span data-ttu-id="400d8-106">Available properties</span><span class="sxs-lookup"><span data-stu-id="400d8-106">Available properties</span></span>

<span data-ttu-id="400d8-107">You define resources with the following structure:</span><span class="sxs-lookup"><span data-stu-id="400d8-107">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<true-to-deploy-this-resource>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": <number-of-iterations>,
          "mode": "<serial-or-parallel>",
          "batchSize": <number-to-deploy-serially>
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "sku": {
          "name": "<sku-name>",
          "tier": "<sku-tier>",
          "size": "<sku-size>",
          "family": "<sku-family>",
          "capacity": <sku-capacity>
      },
      "kind": "<type-of-resource>",
      "plan": {
          "name": "<plan-name>",
          "promotionCode": "<plan-promotion-code>",
          "publisher": "<plan-publisher>",
          "product": "<plan-product>",
          "version": "<plan-version>"
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="400d8-108">Element name</span><span class="sxs-lookup"><span data-stu-id="400d8-108">Element name</span></span> | <span data-ttu-id="400d8-109">Required</span><span class="sxs-lookup"><span data-stu-id="400d8-109">Required</span></span> | <span data-ttu-id="400d8-110">Description</span><span class="sxs-lookup"><span data-stu-id="400d8-110">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="400d8-111">condition</span><span class="sxs-lookup"><span data-stu-id="400d8-111">condition</span></span> | <span data-ttu-id="400d8-112">No</span><span class="sxs-lookup"><span data-stu-id="400d8-112">No</span></span> | <span data-ttu-id="400d8-113">Boolean value that indicates whether the resource will be provisioned during this deployment.</span><span class="sxs-lookup"><span data-stu-id="400d8-113">Boolean value that indicates whether the resource will be provisioned during this deployment.</span></span> <span data-ttu-id="400d8-114">When `true`, the resource is created during the deployment.</span><span class="sxs-lookup"><span data-stu-id="400d8-114">When `true`, the resource is created during the deployment.</span></span> <span data-ttu-id="400d8-115">When `false`, the resource is skipped for this deployment.</span><span class="sxs-lookup"><span data-stu-id="400d8-115">When `false`, the resource is skipped for this deployment.</span></span> |
| <span data-ttu-id="400d8-116">apiVersion</span><span class="sxs-lookup"><span data-stu-id="400d8-116">apiVersion</span></span> |<span data-ttu-id="400d8-117">Yes</span><span class="sxs-lookup"><span data-stu-id="400d8-117">Yes</span></span> |<span data-ttu-id="400d8-118">Version of the REST API to use for creating the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-118">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="400d8-119">type</span><span class="sxs-lookup"><span data-stu-id="400d8-119">type</span></span> |<span data-ttu-id="400d8-120">Yes</span><span class="sxs-lookup"><span data-stu-id="400d8-120">Yes</span></span> |<span data-ttu-id="400d8-121">Type of the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-121">Type of the resource.</span></span> <span data-ttu-id="400d8-122">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="400d8-122">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="400d8-123">name</span><span class="sxs-lookup"><span data-stu-id="400d8-123">name</span></span> |<span data-ttu-id="400d8-124">Yes</span><span class="sxs-lookup"><span data-stu-id="400d8-124">Yes</span></span> |<span data-ttu-id="400d8-125">Name of the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-125">Name of the resource.</span></span> <span data-ttu-id="400d8-126">The name must follow URI component restrictions defined in RFC3986.</span><span class="sxs-lookup"><span data-stu-id="400d8-126">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="400d8-127">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it isn't an attempt to spoof another identity.</span><span class="sxs-lookup"><span data-stu-id="400d8-127">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it isn't an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="400d8-128">location</span><span class="sxs-lookup"><span data-stu-id="400d8-128">location</span></span> |<span data-ttu-id="400d8-129">Varies</span><span class="sxs-lookup"><span data-stu-id="400d8-129">Varies</span></span> |<span data-ttu-id="400d8-130">Supported geo-locations of the provided resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-130">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="400d8-131">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span><span class="sxs-lookup"><span data-stu-id="400d8-131">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="400d8-132">Usually, it also makes sense to place resources that interact with each other in the same region.</span><span class="sxs-lookup"><span data-stu-id="400d8-132">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="400d8-133">Most resource types require a location, but some types (such as a role assignment) don't require a location.</span><span class="sxs-lookup"><span data-stu-id="400d8-133">Most resource types require a location, but some types (such as a role assignment) don't require a location.</span></span> |
| <span data-ttu-id="400d8-134">tags</span><span class="sxs-lookup"><span data-stu-id="400d8-134">tags</span></span> |<span data-ttu-id="400d8-135">No</span><span class="sxs-lookup"><span data-stu-id="400d8-135">No</span></span> |<span data-ttu-id="400d8-136">Tags that are associated with the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-136">Tags that are associated with the resource.</span></span> <span data-ttu-id="400d8-137">Apply tags to logically organize resources across your subscription.</span><span class="sxs-lookup"><span data-stu-id="400d8-137">Apply tags to logically organize resources across your subscription.</span></span> |
| <span data-ttu-id="400d8-138">comments</span><span class="sxs-lookup"><span data-stu-id="400d8-138">comments</span></span> |<span data-ttu-id="400d8-139">No</span><span class="sxs-lookup"><span data-stu-id="400d8-139">No</span></span> |<span data-ttu-id="400d8-140">Your notes for documenting the resources in your template</span><span class="sxs-lookup"><span data-stu-id="400d8-140">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="400d8-141">copy</span><span class="sxs-lookup"><span data-stu-id="400d8-141">copy</span></span> |<span data-ttu-id="400d8-142">No</span><span class="sxs-lookup"><span data-stu-id="400d8-142">No</span></span> |<span data-ttu-id="400d8-143">If more than one instance is needed, the number of resources to create.</span><span class="sxs-lookup"><span data-stu-id="400d8-143">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="400d8-144">The default mode is parallel.</span><span class="sxs-lookup"><span data-stu-id="400d8-144">The default mode is parallel.</span></span> <span data-ttu-id="400d8-145">Specify serial mode when you don't want all or the resources to deploy at the same time.</span><span class="sxs-lookup"><span data-stu-id="400d8-145">Specify serial mode when you don't want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="400d8-146">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="400d8-146">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="400d8-147">dependsOn</span><span class="sxs-lookup"><span data-stu-id="400d8-147">dependsOn</span></span> |<span data-ttu-id="400d8-148">No</span><span class="sxs-lookup"><span data-stu-id="400d8-148">No</span></span> |<span data-ttu-id="400d8-149">Resources that must be deployed before this resource is deployed.</span><span class="sxs-lookup"><span data-stu-id="400d8-149">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="400d8-150">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span><span class="sxs-lookup"><span data-stu-id="400d8-150">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="400d8-151">When resources aren't dependent on each other, they're deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="400d8-151">When resources aren't dependent on each other, they're deployed in parallel.</span></span> <span data-ttu-id="400d8-152">The value can be a comma-separated list of a resource names or resource unique identifiers.</span><span class="sxs-lookup"><span data-stu-id="400d8-152">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="400d8-153">Only list resources that are deployed in this template.</span><span class="sxs-lookup"><span data-stu-id="400d8-153">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="400d8-154">Resources that aren't defined in this template must already exist.</span><span class="sxs-lookup"><span data-stu-id="400d8-154">Resources that aren't defined in this template must already exist.</span></span> <span data-ttu-id="400d8-155">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span><span class="sxs-lookup"><span data-stu-id="400d8-155">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="400d8-156">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="400d8-156">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="400d8-157">properties</span><span class="sxs-lookup"><span data-stu-id="400d8-157">properties</span></span> |<span data-ttu-id="400d8-158">No</span><span class="sxs-lookup"><span data-stu-id="400d8-158">No</span></span> |<span data-ttu-id="400d8-159">Resource-specific configuration settings.</span><span class="sxs-lookup"><span data-stu-id="400d8-159">Resource-specific configuration settings.</span></span> <span data-ttu-id="400d8-160">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-160">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="400d8-161">You can also specify a copy array to create several instances of a property.</span><span class="sxs-lookup"><span data-stu-id="400d8-161">You can also specify a copy array to create several instances of a property.</span></span> |
| <span data-ttu-id="400d8-162">sku</span><span class="sxs-lookup"><span data-stu-id="400d8-162">sku</span></span> | <span data-ttu-id="400d8-163">No</span><span class="sxs-lookup"><span data-stu-id="400d8-163">No</span></span> | <span data-ttu-id="400d8-164">Some resources allow values that define the SKU to deploy.</span><span class="sxs-lookup"><span data-stu-id="400d8-164">Some resources allow values that define the SKU to deploy.</span></span> <span data-ttu-id="400d8-165">For example, you can specify the type of redundancy for a storage account.</span><span class="sxs-lookup"><span data-stu-id="400d8-165">For example, you can specify the type of redundancy for a storage account.</span></span> |
| <span data-ttu-id="400d8-166">kind</span><span class="sxs-lookup"><span data-stu-id="400d8-166">kind</span></span> | <span data-ttu-id="400d8-167">No</span><span class="sxs-lookup"><span data-stu-id="400d8-167">No</span></span> | <span data-ttu-id="400d8-168">Some resources allow a value that defines the type of resource you deploy.</span><span class="sxs-lookup"><span data-stu-id="400d8-168">Some resources allow a value that defines the type of resource you deploy.</span></span> <span data-ttu-id="400d8-169">For example, you can specify the type of Cosmos DB to create.</span><span class="sxs-lookup"><span data-stu-id="400d8-169">For example, you can specify the type of Cosmos DB to create.</span></span> |
| <span data-ttu-id="400d8-170">plan</span><span class="sxs-lookup"><span data-stu-id="400d8-170">plan</span></span> | <span data-ttu-id="400d8-171">No</span><span class="sxs-lookup"><span data-stu-id="400d8-171">No</span></span> | <span data-ttu-id="400d8-172">Some resources allow values that define the plan to deploy.</span><span class="sxs-lookup"><span data-stu-id="400d8-172">Some resources allow values that define the plan to deploy.</span></span> <span data-ttu-id="400d8-173">For example, you can specify the marketplace image for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="400d8-173">For example, you can specify the marketplace image for a virtual machine.</span></span> | 
| <span data-ttu-id="400d8-174">resources</span><span class="sxs-lookup"><span data-stu-id="400d8-174">resources</span></span> |<span data-ttu-id="400d8-175">No</span><span class="sxs-lookup"><span data-stu-id="400d8-175">No</span></span> |<span data-ttu-id="400d8-176">Child resources that depend on the resource being defined.</span><span class="sxs-lookup"><span data-stu-id="400d8-176">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="400d8-177">Only provide resource types that are permitted by the schema of the parent resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-177">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="400d8-178">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="400d8-178">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="400d8-179">Dependency on the parent resource isn't implied.</span><span class="sxs-lookup"><span data-stu-id="400d8-179">Dependency on the parent resource isn't implied.</span></span> <span data-ttu-id="400d8-180">You must explicitly define that dependency.</span><span class="sxs-lookup"><span data-stu-id="400d8-180">You must explicitly define that dependency.</span></span> |

## <a name="condition"></a><span data-ttu-id="400d8-181">Condition</span><span class="sxs-lookup"><span data-stu-id="400d8-181">Condition</span></span>

<span data-ttu-id="400d8-182">When you must decide during deployment whether or not to create a resource, use the `condition` element.</span><span class="sxs-lookup"><span data-stu-id="400d8-182">When you must decide during deployment whether or not to create a resource, use the `condition` element.</span></span> <span data-ttu-id="400d8-183">The value for this element resolves to true or false.</span><span class="sxs-lookup"><span data-stu-id="400d8-183">The value for this element resolves to true or false.</span></span> <span data-ttu-id="400d8-184">When the value is true, the resource will be created.</span><span class="sxs-lookup"><span data-stu-id="400d8-184">When the value is true, the resource will be created.</span></span> <span data-ttu-id="400d8-185">When the value is false, the resource will not be created.</span><span class="sxs-lookup"><span data-stu-id="400d8-185">When the value is false, the resource will not be created.</span></span> <span data-ttu-id="400d8-186">Typically, you use this value when you want to create a new resource or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="400d8-186">Typically, you use this value when you want to create a new resource or use an existing one.</span></span> <span data-ttu-id="400d8-187">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span><span class="sxs-lookup"><span data-stu-id="400d8-187">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="400d8-188">For a complete example template that uses the `condition` element, see [VM with a new or existing Virtual Network, Storage, and Public IP](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-new-or-existing-conditions).</span><span class="sxs-lookup"><span data-stu-id="400d8-188">For a complete example template that uses the `condition` element, see [VM with a new or existing Virtual Network, Storage, and Public IP](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-new-or-existing-conditions).</span></span>

## <a name="resource-specific-values"></a><span data-ttu-id="400d8-189">Resource-specific values</span><span class="sxs-lookup"><span data-stu-id="400d8-189">Resource-specific values</span></span>

<span data-ttu-id="400d8-190">The **apiVersion**, **type**, and **properties** elements are different for each resource type.</span><span class="sxs-lookup"><span data-stu-id="400d8-190">The **apiVersion**, **type**, and **properties** elements are different for each resource type.</span></span> <span data-ttu-id="400d8-191">The **sku**, **kind**, and **plan** elements are available for some resource types, but not all.</span><span class="sxs-lookup"><span data-stu-id="400d8-191">The **sku**, **kind**, and **plan** elements are available for some resource types, but not all.</span></span> <span data-ttu-id="400d8-192">To determine values for these properties, see [template reference](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="400d8-192">To determine values for these properties, see [template reference](/azure/templates/).</span></span>

## <a name="resource-names"></a><span data-ttu-id="400d8-193">Resource names</span><span class="sxs-lookup"><span data-stu-id="400d8-193">Resource names</span></span>

<span data-ttu-id="400d8-194">Generally, you work with three types of resource names in Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="400d8-194">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="400d8-195">Resource names that must be unique.</span><span class="sxs-lookup"><span data-stu-id="400d8-195">Resource names that must be unique.</span></span>
* <span data-ttu-id="400d8-196">Resource names that aren't required to be unique, but you choose to provide a name that can help you identify the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-196">Resource names that aren't required to be unique, but you choose to provide a name that can help you identify the resource.</span></span>
* <span data-ttu-id="400d8-197">Resource names that can be generic.</span><span class="sxs-lookup"><span data-stu-id="400d8-197">Resource names that can be generic.</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="400d8-198">Unique resource names</span><span class="sxs-lookup"><span data-stu-id="400d8-198">Unique resource names</span></span>

<span data-ttu-id="400d8-199">Provide a unique resource name for any resource type that has a data access endpoint.</span><span class="sxs-lookup"><span data-stu-id="400d8-199">Provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="400d8-200">Some common resource types that require a unique name include:</span><span class="sxs-lookup"><span data-stu-id="400d8-200">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="400d8-201">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="400d8-201">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="400d8-202">Web Apps feature of Azure App Service</span><span class="sxs-lookup"><span data-stu-id="400d8-202">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="400d8-203">SQL Server</span><span class="sxs-lookup"><span data-stu-id="400d8-203">SQL Server</span></span>
* <span data-ttu-id="400d8-204">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="400d8-204">Azure Key Vault</span></span>
* <span data-ttu-id="400d8-205">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="400d8-205">Azure Redis Cache</span></span>
* <span data-ttu-id="400d8-206">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="400d8-206">Azure Batch</span></span>
* <span data-ttu-id="400d8-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="400d8-207">Azure Traffic Manager</span></span>
* <span data-ttu-id="400d8-208">Azure Search</span><span class="sxs-lookup"><span data-stu-id="400d8-208">Azure Search</span></span>
* <span data-ttu-id="400d8-209">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="400d8-209">Azure HDInsight</span></span>

<span data-ttu-id="400d8-210"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span><span class="sxs-lookup"><span data-stu-id="400d8-210"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="400d8-211">When setting the name, you can either manually create a unique name or use the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span><span class="sxs-lookup"><span data-stu-id="400d8-211">When setting the name, you can either manually create a unique name or use the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> <span data-ttu-id="400d8-212">You also might want to add a prefix or suffix to the **uniqueString** result.</span><span class="sxs-lookup"><span data-stu-id="400d8-212">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="400d8-213">Modifying the unique name can help you more easily identify the resource type from the name.</span><span class="sxs-lookup"><span data-stu-id="400d8-213">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="400d8-214">For example, you can generate a unique name for a storage account by using the following variable:</span><span class="sxs-lookup"><span data-stu-id="400d8-214">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="400d8-215">Resource names for identification</span><span class="sxs-lookup"><span data-stu-id="400d8-215">Resource names for identification</span></span>
<span data-ttu-id="400d8-216">Some resource types you might want to name, but their names do not have to be unique.</span><span class="sxs-lookup"><span data-stu-id="400d8-216">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="400d8-217">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span><span class="sxs-lookup"><span data-stu-id="400d8-217">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="400d8-218">Generic resource names</span><span class="sxs-lookup"><span data-stu-id="400d8-218">Generic resource names</span></span>
<span data-ttu-id="400d8-219">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span><span class="sxs-lookup"><span data-stu-id="400d8-219">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="400d8-220">For example, you can set a standard, generic name for firewall rules on a SQL server:</span><span class="sxs-lookup"><span data-stu-id="400d8-220">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="location"></a><span data-ttu-id="400d8-221">Location</span><span class="sxs-lookup"><span data-stu-id="400d8-221">Location</span></span>
<span data-ttu-id="400d8-222">When deploying a template, you must provide a location for each resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-222">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="400d8-223">Different resource types are supported in different locations.</span><span class="sxs-lookup"><span data-stu-id="400d8-223">Different resource types are supported in different locations.</span></span> <span data-ttu-id="400d8-224">To see a list of locations that are available to your subscription for a particular resource type, use Azure PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="400d8-224">To see a list of locations that are available to your subscription for a particular resource type, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="400d8-225">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span><span class="sxs-lookup"><span data-stu-id="400d8-225">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="400d8-226">The following example uses Azure CLI to get the locations for the `Microsoft.Web\sites` resource type:</span><span class="sxs-lookup"><span data-stu-id="400d8-226">The following example uses Azure CLI to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<span data-ttu-id="400d8-227">After determining the supported locations for your resources, set that location in your template.</span><span class="sxs-lookup"><span data-stu-id="400d8-227">After determining the supported locations for your resources, set that location in your template.</span></span> <span data-ttu-id="400d8-228">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="400d8-228">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="400d8-229">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span><span class="sxs-lookup"><span data-stu-id="400d8-229">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="400d8-230">The following example shows a storage account that is deployed to the same location as the resource group:</span><span class="sxs-lookup"><span data-stu-id="400d8-230">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="400d8-231">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span><span class="sxs-lookup"><span data-stu-id="400d8-231">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="400d8-232">The following example shows a storage account that is always deployed to North Central US:</span><span class="sxs-lookup"><span data-stu-id="400d8-232">The following example shows a storage account that is always deployed to North Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="tags"></a><span data-ttu-id="400d8-233">Tags</span><span class="sxs-lookup"><span data-stu-id="400d8-233">Tags</span></span>
[!INCLUDE [resource-manager-governance-tags](../../includes/resource-manager-governance-tags.md)]

### <a name="add-tags-to-your-template"></a><span data-ttu-id="400d8-234">Add tags to your template</span><span class="sxs-lookup"><span data-stu-id="400d8-234">Add tags to your template</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="child-resources"></a><span data-ttu-id="400d8-235">Child resources</span><span class="sxs-lookup"><span data-stu-id="400d8-235">Child resources</span></span>

<span data-ttu-id="400d8-236">Within some resource types, you can also define an array of child resources.</span><span class="sxs-lookup"><span data-stu-id="400d8-236">Within some resource types, you can also define an array of child resources.</span></span> <span data-ttu-id="400d8-237">Child resources are resources that only exist within the context of another resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-237">Child resources are resources that only exist within the context of another resource.</span></span> <span data-ttu-id="400d8-238">For example, a SQL database can't exist without a SQL server so the database is a child of the server.</span><span class="sxs-lookup"><span data-stu-id="400d8-238">For example, a SQL database can't exist without a SQL server so the database is a child of the server.</span></span> <span data-ttu-id="400d8-239">You can define the database within the definition for the server.</span><span class="sxs-lookup"><span data-stu-id="400d8-239">You can define the database within the definition for the server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="400d8-240">When nested, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="400d8-240">When nested, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="400d8-241">You don't provide `Microsoft.Sql/servers/` because it's assumed from the parent resource type.</span><span class="sxs-lookup"><span data-stu-id="400d8-241">You don't provide `Microsoft.Sql/servers/` because it's assumed from the parent resource type.</span></span> <span data-ttu-id="400d8-242">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span><span class="sxs-lookup"><span data-stu-id="400d8-242">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="400d8-243">You don't provide `exampleserver` because it's assumed from the parent resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-243">You don't provide `exampleserver` because it's assumed from the parent resource.</span></span>

<span data-ttu-id="400d8-244">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="400d8-244">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="400d8-245">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="400d8-245">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="400d8-246">But, you don't have to define the database within the server.</span><span class="sxs-lookup"><span data-stu-id="400d8-246">But, you don't have to define the database within the server.</span></span> <span data-ttu-id="400d8-247">You can define the child resource at the top level.</span><span class="sxs-lookup"><span data-stu-id="400d8-247">You can define the child resource at the top level.</span></span> <span data-ttu-id="400d8-248">You might use this approach if the parent resource isn't deployed in the same template, or if want to use `copy` to create multiple child resources.</span><span class="sxs-lookup"><span data-stu-id="400d8-248">You might use this approach if the parent resource isn't deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="400d8-249">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span><span class="sxs-lookup"><span data-stu-id="400d8-249">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="400d8-250">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name isn't simply a concatenation of the two.</span><span class="sxs-lookup"><span data-stu-id="400d8-250">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name isn't simply a concatenation of the two.</span></span> <span data-ttu-id="400d8-251">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span><span class="sxs-lookup"><span data-stu-id="400d8-251">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="400d8-252">For example:</span><span class="sxs-lookup"><span data-stu-id="400d8-252">For example:</span></span>

<span data-ttu-id="400d8-253">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span><span class="sxs-lookup"><span data-stu-id="400d8-253">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="recommendations"></a><span data-ttu-id="400d8-254">Recommendations</span><span class="sxs-lookup"><span data-stu-id="400d8-254">Recommendations</span></span>
<span data-ttu-id="400d8-255">The following information can be helpful when you work with resources:</span><span class="sxs-lookup"><span data-stu-id="400d8-255">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="400d8-256">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span><span class="sxs-lookup"><span data-stu-id="400d8-256">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="400d8-257">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span><span class="sxs-lookup"><span data-stu-id="400d8-257">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="400d8-258">Use the **reference** function to dynamically retrieve the namespace.</span><span class="sxs-lookup"><span data-stu-id="400d8-258">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="400d8-259">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span><span class="sxs-lookup"><span data-stu-id="400d8-259">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="400d8-260">Set the API version to the same version that you're using for the storage account in your template:</span><span class="sxs-lookup"><span data-stu-id="400d8-260">Set the API version to the same version that you're using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="400d8-261">If the storage account is deployed in the same template that you're creating, you don't need to specify the provider namespace when you reference the resource.</span><span class="sxs-lookup"><span data-stu-id="400d8-261">If the storage account is deployed in the same template that you're creating, you don't need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="400d8-262">The following example shows the simplified syntax:</span><span class="sxs-lookup"><span data-stu-id="400d8-262">The following example shows the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="400d8-263">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span><span class="sxs-lookup"><span data-stu-id="400d8-263">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="400d8-264">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span><span class="sxs-lookup"><span data-stu-id="400d8-264">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="400d8-265">You also can reference an existing storage account that is in a different resource group:</span><span class="sxs-lookup"><span data-stu-id="400d8-265">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="400d8-266">Assign public IP addresses to a virtual machine only when an application requires it.</span><span class="sxs-lookup"><span data-stu-id="400d8-266">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="400d8-267">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span><span class="sxs-lookup"><span data-stu-id="400d8-267">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="400d8-268">For more information about connecting to virtual machines, see:</span><span class="sxs-lookup"><span data-stu-id="400d8-268">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="400d8-269">Run VMs for an N-tier architecture in Azure</span><span class="sxs-lookup"><span data-stu-id="400d8-269">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="400d8-270">Set up WinRM access for VMs in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="400d8-270">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="400d8-271">Allow external access to your VM by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="400d8-271">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="400d8-272">Allow external access to your VM by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="400d8-272">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="400d8-273">Allow external access to your Linux VM by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="400d8-273">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="400d8-274">The **domainNameLabel** property for public IP addresses must be unique.</span><span class="sxs-lookup"><span data-stu-id="400d8-274">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="400d8-275">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="400d8-275">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="400d8-276">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span><span class="sxs-lookup"><span data-stu-id="400d8-276">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="400d8-277">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span><span class="sxs-lookup"><span data-stu-id="400d8-277">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="400d8-278">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span><span class="sxs-lookup"><span data-stu-id="400d8-278">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 


## <a name="next-steps"></a><span data-ttu-id="400d8-279">Next steps</span><span class="sxs-lookup"><span data-stu-id="400d8-279">Next steps</span></span>
* <span data-ttu-id="400d8-280">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="400d8-280">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="400d8-281">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="400d8-281">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="400d8-282">To use more than one template during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="400d8-282">To use more than one template during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="400d8-283">You may need to use resources that exist within a different resource group.</span><span class="sxs-lookup"><span data-stu-id="400d8-283">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="400d8-284">This scenario is common when working with storage accounts or virtual networks that are shared across several resource groups.</span><span class="sxs-lookup"><span data-stu-id="400d8-284">This scenario is common when working with storage accounts or virtual networks that are shared across several resource groups.</span></span> <span data-ttu-id="400d8-285">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="400d8-285">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
* <span data-ttu-id="400d8-286">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="400d8-286">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>