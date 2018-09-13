---
title: Azure invalid template errors | Microsoft Docs
description: Describes how to resolve invalid template errors.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/08/2018
ms.author: tomfitz
ms.openlocfilehash: 59f07b9ba8116cb1a4b5ab50382d89d01a78853b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866387"
---
# <a name="resolve-errors-for-invalid-template"></a><span data-ttu-id="d8c3c-103">Resolve errors for invalid template</span><span class="sxs-lookup"><span data-stu-id="d8c3c-103">Resolve errors for invalid template</span></span>

<span data-ttu-id="d8c3c-104">This article describes how to resolve invalid template errors.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-104">This article describes how to resolve invalid template errors.</span></span>

## <a name="symptom"></a><span data-ttu-id="d8c3c-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="d8c3c-105">Symptom</span></span>

<span data-ttu-id="d8c3c-106">When deploying a template, you receive an error indicating:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-106">When deploying a template, you receive an error indicating:</span></span>

```
Code=InvalidTemplate
Message=<varies>
```

<span data-ttu-id="d8c3c-107">The error message depends on the type of error.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-107">The error message depends on the type of error.</span></span>

## <a name="cause"></a><span data-ttu-id="d8c3c-108">Cause</span><span class="sxs-lookup"><span data-stu-id="d8c3c-108">Cause</span></span>

<span data-ttu-id="d8c3c-109">This error can result from several different types of errors.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-109">This error can result from several different types of errors.</span></span> <span data-ttu-id="d8c3c-110">They usually involve a syntax or structural error in the template.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-110">They usually involve a syntax or structural error in the template.</span></span>

<a id="syntax-error" />

## <a name="solution-1---syntax-error"></a><span data-ttu-id="d8c3c-111">Solution 1 - syntax error</span><span class="sxs-lookup"><span data-stu-id="d8c3c-111">Solution 1 - syntax error</span></span>

<span data-ttu-id="d8c3c-112">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-112">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

```
Code=InvalidTemplate
Message=Deployment template validation failed
```

<span data-ttu-id="d8c3c-113">This error is easy to make because template expressions can be intricate.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-113">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="d8c3c-114">For example, the following name assignment for a storage account has one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-114">For example, the following name assignment for a storage account has one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
```

<span data-ttu-id="d8c3c-115">If you don't provide the matching syntax, the template produces a value that is different than your intention.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-115">If you don't provide the matching syntax, the template produces a value that is different than your intention.</span></span>

<span data-ttu-id="d8c3c-116">When you receive this type of error, carefully review the expression syntax.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-116">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="d8c3c-117">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-117">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

<a id="incorrect-segment-lengths" />

## <a name="solution-2---incorrect-segment-lengths"></a><span data-ttu-id="d8c3c-118">Solution 2 - incorrect segment lengths</span><span class="sxs-lookup"><span data-stu-id="d8c3c-118">Solution 2 - incorrect segment lengths</span></span>

<span data-ttu-id="d8c3c-119">Another invalid template error occurs when the resource name isn't in the correct format.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-119">Another invalid template error occurs when the resource name isn't in the correct format.</span></span>

```
Code=InvalidTemplate
Message=Deployment template validation failed: 'The template resource {resource-name}'
for type {resource-type} has incorrect segment lengths.
```

<span data-ttu-id="d8c3c-120">A root level resource must have one less segment in the name than in the resource type.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-120">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="d8c3c-121">Each segment is differentiated by a slash.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-121">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="d8c3c-122">In the following example, the type has two segments and the name has one segment, so it's a **valid name**.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-122">In the following example, the type has two segments and the name has one segment, so it's a **valid name**.</span></span>

```json
{
  "type": "Microsoft.Web/serverfarms",
  "name": "myHostingPlanName",
  ...
}
```

<span data-ttu-id="d8c3c-123">But the next example is **not a valid name** because it has the same number of segments as the type.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-123">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

```json
{
  "type": "Microsoft.Web/serverfarms",
  "name": "appPlan/myHostingPlanName",
  ...
}
```

<span data-ttu-id="d8c3c-124">For child resources, the type and name have the same number of segments.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-124">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="d8c3c-125">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-125">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="d8c3c-126">Therefore, the full name still has one less segment than the full type.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-126">Therefore, the full name still has one less segment than the full type.</span></span>

```json
"resources": [
    {
        "type": "Microsoft.KeyVault/vaults",
        "name": "contosokeyvault",
        ...
        "resources": [
            {
                "type": "secrets",
                "name": "appPassword",
                ...
            }
        ]
    }
]
```

<span data-ttu-id="d8c3c-127">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-127">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="d8c3c-128">For example, applying a resource lock to a web site requires a type with four segments.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-128">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="d8c3c-129">Therefore, the name is three segments:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-129">Therefore, the name is three segments:</span></span>

```json
{
    "type": "Microsoft.Web/sites/providers/locks",
    "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
    ...
}
```

<a id="parameter-not-valid" />

## <a name="solution-3---parameter-is-not-valid"></a><span data-ttu-id="d8c3c-130">Solution 3 - parameter is not valid</span><span class="sxs-lookup"><span data-stu-id="d8c3c-130">Solution 3 - parameter is not valid</span></span>

<span data-ttu-id="d8c3c-131">If you provide a parameter value that is not one of the allowed values, you receive a message similar to the following error:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-131">If you provide a parameter value that is not one of the allowed values, you receive a message similar to the following error:</span></span>

```
Code=InvalidTemplate;
Message=Deployment template validation failed: 'The provided value {parameter value}
for the template parameter {parameter name} is not valid. The parameter value is not
part of the allowed values
```

<span data-ttu-id="d8c3c-132">Double check the allowed values in the template, and provide one during deployment.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-132">Double check the allowed values in the template, and provide one during deployment.</span></span> <span data-ttu-id="d8c3c-133">For more information about allowed parameter values, see [Parameters section of Azure Resource Manager templates](resource-manager-templates-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="d8c3c-133">For more information about allowed parameter values, see [Parameters section of Azure Resource Manager templates](resource-manager-templates-parameters.md).</span></span>

<a id="too-many-resource-groups" />

## <a name="solution-4---too-many-target-resource-groups"></a><span data-ttu-id="d8c3c-134">Solution 4 - Too many target resource groups</span><span class="sxs-lookup"><span data-stu-id="d8c3c-134">Solution 4 - Too many target resource groups</span></span>

<span data-ttu-id="d8c3c-135">If you specify more than five target resource groups in a single deployment, you receive this error.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-135">If you specify more than five target resource groups in a single deployment, you receive this error.</span></span> <span data-ttu-id="d8c3c-136">Consider either consolidating the number of resource groups in your deployment, or deploying some of the templates as separate deployments.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-136">Consider either consolidating the number of resource groups in your deployment, or deploying some of the templates as separate deployments.</span></span> <span data-ttu-id="d8c3c-137">For more information, see [Deploy Azure resources to more than one subscription or resource group](resource-manager-cross-resource-group-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d8c3c-137">For more information, see [Deploy Azure resources to more than one subscription or resource group](resource-manager-cross-resource-group-deployment.md).</span></span>

<a id="circular-dependency" />

## <a name="solution-5---circular-dependency-detected"></a><span data-ttu-id="d8c3c-138">Solution 5 - circular dependency detected</span><span class="sxs-lookup"><span data-stu-id="d8c3c-138">Solution 5 - circular dependency detected</span></span>

<span data-ttu-id="d8c3c-139">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-139">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="d8c3c-140">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-140">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="d8c3c-141">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-141">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="d8c3c-142">You can usually solve this problem by removing unnecessary dependencies.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-142">You can usually solve this problem by removing unnecessary dependencies.</span></span>

<span data-ttu-id="d8c3c-143">To solve a circular dependency:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-143">To solve a circular dependency:</span></span>

1. <span data-ttu-id="d8c3c-144">In your template, find the resource identified in the circular dependency.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-144">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="d8c3c-145">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-145">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="d8c3c-146">Examine those resources to see which resources they depend on.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-146">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="d8c3c-147">Follow the dependencies until you notice a resource that depends on the original resource.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-147">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="d8c3c-148">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-148">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="d8c3c-149">Remove those dependencies.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-149">Remove those dependencies.</span></span> <span data-ttu-id="d8c3c-150">If you are unsure that a dependency is needed, try removing it.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-150">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="d8c3c-151">Redeploy the template.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-151">Redeploy the template.</span></span>

<span data-ttu-id="d8c3c-152">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-152">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="d8c3c-153">If you get an error, add the dependency back into the template.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-153">If you get an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="d8c3c-154">If that approach doesn't solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span><span class="sxs-lookup"><span data-stu-id="d8c3c-154">If that approach doesn't solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="d8c3c-155">Configure those child resources to deploy after the resources involved in the circular dependency.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-155">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="d8c3c-156">For example, suppose you're deploying two virtual machines but you must set properties on each one that refer to the other.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-156">For example, suppose you're deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="d8c3c-157">You can deploy them in the following order:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-157">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="d8c3c-158">vm1</span><span class="sxs-lookup"><span data-stu-id="d8c3c-158">vm1</span></span>
2. <span data-ttu-id="d8c3c-159">vm2</span><span class="sxs-lookup"><span data-stu-id="d8c3c-159">vm2</span></span>
3. <span data-ttu-id="d8c3c-160">Extension on vm1 depends on vm1 and vm2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-160">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="d8c3c-161">The extension sets values on vm1 that it gets from vm2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-161">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="d8c3c-162">Extension on vm2 depends on vm1 and vm2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-162">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="d8c3c-163">The extension sets values on vm2 that it gets from vm1.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-163">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="d8c3c-164">The same approach works for App Service apps.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-164">The same approach works for App Service apps.</span></span> <span data-ttu-id="d8c3c-165">Consider moving configuration values into a child resource of the app resource.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-165">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="d8c3c-166">You can deploy two web apps in the following order:</span><span class="sxs-lookup"><span data-stu-id="d8c3c-166">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="d8c3c-167">webapp1</span><span class="sxs-lookup"><span data-stu-id="d8c3c-167">webapp1</span></span>
2. <span data-ttu-id="d8c3c-168">webapp2</span><span class="sxs-lookup"><span data-stu-id="d8c3c-168">webapp2</span></span>
3. <span data-ttu-id="d8c3c-169">config for webapp1 depends on webapp1 and webapp2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-169">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="d8c3c-170">It contains app settings with values from webapp2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-170">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="d8c3c-171">config for webapp2 depends on webapp1 and webapp2.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-171">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="d8c3c-172">It contains app settings with values from webapp1.</span><span class="sxs-lookup"><span data-stu-id="d8c3c-172">It contains app settings with values from webapp1.</span></span>
