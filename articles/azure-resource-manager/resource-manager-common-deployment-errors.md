---
title: Troubleshoot common Azure deployment errors | Microsoft Docs
description: Describes how to resolve common errors when you deploy resources to Azure using Azure Resource Manager.
services: azure-resource-manager
documentationcenter: ''
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: deployment error, azure deployment, deploy to azure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomfitz
ms.openlocfilehash: 52f9ef3b754a9f5da139a4d26626baac271bc8f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563973"
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="e3a5f-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3a5f-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="e3a5f-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="e3a5f-106">Two types of errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-106">Two types of errors</span></span>
<span data-ttu-id="e3a5f-107">There are two types of errors you can receive:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-107">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="e3a5f-108">validation errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-108">validation errors</span></span>
* <span data-ttu-id="e3a5f-109">deployment errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-109">deployment errors</span></span>

<span data-ttu-id="e3a5f-110">The following image shows the activity log for a subscription.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-110">The following image shows the activity log for a subscription.</span></span> <span data-ttu-id="e3a5f-111">There are three operations that occurred in two deployments.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-111">There are three operations that occurred in two deployments.</span></span> <span data-ttu-id="e3a5f-112">In the first deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-112">In the first deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span></span> <span data-ttu-id="e3a5f-113">In the second deployment, the template failed validation and did not proceed to the **Write Deployments**.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-113">In the second deployment, the template failed validation and did not proceed to the **Write Deployments**.</span></span>

![show error code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/show-activity-log.png)

<span data-ttu-id="e3a5f-115">Validation errors arise from scenarios that can be pre-determined to cause a problem.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-115">Validation errors arise from scenarios that can be pre-determined to cause a problem.</span></span> <span data-ttu-id="e3a5f-116">Validation errors include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-116">Validation errors include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="e3a5f-117">Deployment errors arise from conditions that occur during the deployment process.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-117">Deployment errors arise from conditions that occur during the deployment process.</span></span> <span data-ttu-id="e3a5f-118">For example, a deployment error might arise from trying to access a resource that is being deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-118">For example, a deployment error might arise from trying to access a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="e3a5f-119">Both types of errors return an error code that you use to troubleshoot the deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-119">Both types of errors return an error code that you use to troubleshoot the deployment.</span></span> <span data-ttu-id="e3a5f-120">Both types of errors appear in the [activity log](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-120">Both types of errors appear in the [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="e3a5f-121">However, validation errors do not appear in your deployment history because the deployment never started.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-121">However, validation errors do not appear in your deployment history because the deployment never started.</span></span>


## <a name="error-codes"></a><span data-ttu-id="e3a5f-122">Error codes</span><span class="sxs-lookup"><span data-stu-id="e3a5f-122">Error codes</span></span>

<span data-ttu-id="e3a5f-123">The following error codes are described in this topic:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-123">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="e3a5f-124">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="e3a5f-124">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="e3a5f-125">Authorization failed</span><span class="sxs-lookup"><span data-stu-id="e3a5f-125">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="e3a5f-126">BadRequest</span><span class="sxs-lookup"><span data-stu-id="e3a5f-126">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="e3a5f-127">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="e3a5f-127">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="e3a5f-128">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="e3a5f-128">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="e3a5f-129">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="e3a5f-129">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="e3a5f-130">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="e3a5f-130">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="e3a5f-131">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="e3a5f-131">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="e3a5f-132">NotFound</span><span class="sxs-lookup"><span data-stu-id="e3a5f-132">NotFound</span></span>](#notfound)
* [<span data-ttu-id="e3a5f-133">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="e3a5f-133">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="e3a5f-134">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="e3a5f-134">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="e3a5f-135">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="e3a5f-135">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="e3a5f-136">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="e3a5f-136">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="e3a5f-137">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="e3a5f-137">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="e3a5f-138">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="e3a5f-138">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="e3a5f-139">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="e3a5f-139">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="e3a5f-140">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="e3a5f-140">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="e3a5f-141">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="e3a5f-141">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

### <a name="deploymentfailed"></a><span data-ttu-id="e3a5f-142">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="e3a5f-142">DeploymentFailed</span></span>

<span data-ttu-id="e3a5f-143">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-143">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="e3a5f-144">The error code that actually helps you resolve the issue is usually one level below this error.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-144">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="e3a5f-145">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-145">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![show error code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/error-code.png)

### <a name="skunotavailable"></a><span data-ttu-id="e3a5f-147">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="e3a5f-147">SkuNotAvailable</span></span>

<span data-ttu-id="e3a5f-148">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-148">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="e3a5f-149">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-149">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="e3a5f-150">To resolve this issue, you need to determine which SKUs are available in a region.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-150">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="e3a5f-151">You can use either the portal or a REST operation to find available SKUs.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-151">You can use either the portal or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="e3a5f-152">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-152">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="e3a5f-153">As you set the values, you see the available SKUs for that resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-153">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="e3a5f-154">You do not need to complete the deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-154">You do not need to complete the deployment.</span></span>

    ![available SKUs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="e3a5f-156">To use the REST API for virtual machines, send the following request:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-156">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="e3a5f-157">It returns available SKUs and regions in the following format:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-157">It returns available SKUs and regions in the following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="e3a5f-158">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, contact [Azure Support](https://portal.azure.com/#create/Microsoft.Support).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-158">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, contact [Azure Support](https://portal.azure.com/#create/Microsoft.Support).</span></span>

### <a name="disallowedoperation"></a><span data-ttu-id="e3a5f-159">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="e3a5f-159">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="e3a5f-160">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-160">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="e3a5f-161">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-161">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="e3a5f-162">To resolve this issue, you must use a subscription that has permission to deploy resources.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-162">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="e3a5f-163">To view your available subscriptions with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-163">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="e3a5f-164">And, to set the current subscription, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-164">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="e3a5f-165">To view your available subscriptions with Azure CLI 2.0, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-165">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="e3a5f-166">And, to set the current subscription, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-166">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

### <a name="invalidtemplate"></a><span data-ttu-id="e3a5f-167">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="e3a5f-167">InvalidTemplate</span></span>
<span data-ttu-id="e3a5f-168">This error can result from several different types of errors.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-168">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="e3a5f-169">Syntax error</span><span class="sxs-lookup"><span data-stu-id="e3a5f-169">Syntax error</span></span>

   <span data-ttu-id="e3a5f-170">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-170">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="e3a5f-171">This error is easy to make because template expressions can be intricate.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-171">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="e3a5f-172">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-172">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="e3a5f-173">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-173">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="e3a5f-174">When you receive this type of error, carefully review the expression syntax.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-174">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="e3a5f-175">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-175">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="e3a5f-176">Incorrect segment lengths</span><span class="sxs-lookup"><span data-stu-id="e3a5f-176">Incorrect segment lengths</span></span>

   <span data-ttu-id="e3a5f-177">Another invalid template error occurs when the resource name is not in the correct format.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-177">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="e3a5f-178">A root level resource must have one less segment in the name than in the resource type.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-178">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="e3a5f-179">Each segment is differentiated by a slash.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-179">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="e3a5f-180">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-180">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="e3a5f-181">But the next example is **not a valid name** because it has the same number of segments as the type.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-181">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="e3a5f-182">For child resources, the type and name have the same number of segments.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-182">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="e3a5f-183">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-183">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="e3a5f-184">Therefore, the full name still has one less segment than the full type.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-184">Therefore, the full name still has one less segment than the full type.</span></span>

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

   <span data-ttu-id="e3a5f-185">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-185">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="e3a5f-186">For example, applying a resource lock to a web site requires a type with four segments.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-186">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="e3a5f-187">Therefore, the name is three segments:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-187">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="e3a5f-188">Copy index is not expected</span><span class="sxs-lookup"><span data-stu-id="e3a5f-188">Copy index is not expected</span></span>

   <span data-ttu-id="e3a5f-189">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-189">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="e3a5f-190">You can only apply the copy element to a resource type.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-190">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="e3a5f-191">You cannot apply copy to a property within a resource type.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-191">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="e3a5f-192">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-192">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="e3a5f-193">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-193">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="e3a5f-194">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-194">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="e3a5f-195">Parameter is not valid</span><span class="sxs-lookup"><span data-stu-id="e3a5f-195">Parameter is not valid</span></span>

   <span data-ttu-id="e3a5f-196">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-196">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="e3a5f-197">Double check the allowed values in the template, and provide one during deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-197">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="e3a5f-198">Circular dependency detected</span><span class="sxs-lookup"><span data-stu-id="e3a5f-198">Circular dependency detected</span></span>

   <span data-ttu-id="e3a5f-199">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-199">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="e3a5f-200">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-200">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="e3a5f-201">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-201">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="e3a5f-202">You can usually solve this problem by removing unnecessary dependencies.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-202">You can usually solve this problem by removing unnecessary dependencies.</span></span> <span data-ttu-id="e3a5f-203">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-203">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="e3a5f-204">NotFound and ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="e3a5f-204">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="e3a5f-205">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-205">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="e3a5f-206">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-206">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="e3a5f-207">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-207">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="e3a5f-208">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-208">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="e3a5f-209">For example, when deploying a web app, the App Service plan must exist.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-209">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="e3a5f-210">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-210">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="e3a5f-211">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-211">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="e3a5f-212">You prevent this error by setting the dependency in the web app.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-212">You prevent this error by setting the dependency in the web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="e3a5f-213">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-213">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="e3a5f-214">You also see this error when the resource exists in a different resource group than the one being deployed to.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-214">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="e3a5f-215">In that case, use the [resourceId function](resource-group-template-functions.md#resourceid) to get the fully qualified name of the resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-215">In that case, use the [resourceId function](resource-group-template-functions.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="e3a5f-216">If you attempt to use the [reference](resource-group-template-functions.md#reference) or [listKeys](resource-group-template-functions.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-216">If you attempt to use the [reference](resource-group-template-functions.md#reference) or [listKeys](resource-group-template-functions.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="e3a5f-217">Look for an expression that includes the **reference** function.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-217">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="e3a5f-218">Double check that the parameter values are correct.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-218">Double check that the parameter values are correct.</span></span>

### <a name="parentresourcenotfound"></a><span data-ttu-id="e3a5f-219">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="e3a5f-219">ParentResourceNotFound</span></span>

<span data-ttu-id="e3a5f-220">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-220">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="e3a5f-221">If it does not yet exist, you receive the following error:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-221">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="e3a5f-222">The name of the child resource includes the parent name.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-222">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="e3a5f-223">For example, a SQL Database might be defined as:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-223">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="e3a5f-224">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-224">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="e3a5f-225">To resolve this error, include a dependency.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-225">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />
### <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="e3a5f-226">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="e3a5f-226">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="e3a5f-227">For storage accounts, you must provide a name for the resource that is unique across Azure.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-227">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="e3a5f-228">If you do not provide a unique name, you receive an error like:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-228">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="e3a5f-229">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions.md#uniquestring) function.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-229">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="e3a5f-230">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-230">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="e3a5f-231">Either delete the existing storage account, or provide the same location as the existing storage account.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-231">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

### <a name="accountnameinvalid"></a><span data-ttu-id="e3a5f-232">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="e3a5f-232">AccountNameInvalid</span></span>
<span data-ttu-id="e3a5f-233">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-233">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="e3a5f-234">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-234">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="e3a5f-235">The [uniqueString](resource-group-template-functions.md#uniquestring) function returns 13 characters.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-235">The [uniqueString](resource-group-template-functions.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="e3a5f-236">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-236">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

### <a name="badrequest"></a><span data-ttu-id="e3a5f-237">BadRequest</span><span class="sxs-lookup"><span data-stu-id="e3a5f-237">BadRequest</span></span>

<span data-ttu-id="e3a5f-238">You may encounter a BadRequest status when you provide an invalid value for a property.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-238">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="e3a5f-239">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-239">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="e3a5f-240">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-240">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />
### <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="e3a5f-241">NoRegisteredProviderFound and MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="e3a5f-241">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="e3a5f-242">When deploying resource, you may receive the following error code and message:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-242">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="e3a5f-243">Or, you may receive a similar message that states:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-243">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="e3a5f-244">You receive these errors for one of three reasons:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-244">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="e3a5f-245">The resource provider has not been registered for your subscription</span><span class="sxs-lookup"><span data-stu-id="e3a5f-245">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="e3a5f-246">API version not supported for the resource type</span><span class="sxs-lookup"><span data-stu-id="e3a5f-246">API version not supported for the resource type</span></span>
3. <span data-ttu-id="e3a5f-247">Location not supported for the resource type</span><span class="sxs-lookup"><span data-stu-id="e3a5f-247">Location not supported for the resource type</span></span>

<span data-ttu-id="e3a5f-248">The error message should give you suggestions for the supported locations and API versions.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-248">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="e3a5f-249">You can change your template to one of the suggested values.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-249">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="e3a5f-250">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-250">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="e3a5f-251">If you have not used a particular resource provider before, you may need to register that provider.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-251">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="e3a5f-252">You can discover more about resource providers through PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-252">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="e3a5f-253">**Portal**</span><span class="sxs-lookup"><span data-stu-id="e3a5f-253">**Portal**</span></span>

<span data-ttu-id="e3a5f-254">You can see the registration status and register a resource provider namespace through the portal.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-254">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="e3a5f-255">For your subscription, select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-255">For your subscription, select **Resource providers**.</span></span>

   ![select resource providers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="e3a5f-257">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-257">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![list resource providers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="e3a5f-259">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e3a5f-259">**PowerShell**</span></span>

<span data-ttu-id="e3a5f-260">To see your registration status, use **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-260">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="e3a5f-261">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-261">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="e3a5f-262">To get the supported locations for a particular type of resource, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-262">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="e3a5f-263">To get the supported API versions for a particular type of resource, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-263">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="e3a5f-264">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="e3a5f-264">**Azure CLI**</span></span>

<span data-ttu-id="e3a5f-265">To see whether the provider is registered, use the `azure provider list` command.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-265">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="e3a5f-266">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-266">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="e3a5f-267">To see the supported locations and API versions for a resource type, use:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-267">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />
### <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="e3a5f-268">QuotaExceeded and OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="e3a5f-268">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="e3a5f-269">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-269">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="e3a5f-270">For example, your subscription may be configured to limit the number of cores for a region.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-270">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="e3a5f-271">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-271">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="e3a5f-272">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-272">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="e3a5f-273">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-273">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="e3a5f-274">The following example illustrates that the core quota for a free trial account is 4:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-274">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="e3a5f-275">Which returns:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-275">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="e3a5f-276">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-276">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="e3a5f-277">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-277">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="e3a5f-278">Which returns:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-278">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="e3a5f-279">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-279">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a5f-280">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-280">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="e3a5f-281">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-281">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="e3a5f-282">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-282">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

### <a name="invalidcontentlink"></a><span data-ttu-id="e3a5f-283">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="e3a5f-283">InvalidContentLink</span></span>
<span data-ttu-id="e3a5f-284">When you receive the error message:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-284">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="e3a5f-285">You have most likely attempted to link to a nested template that is not available.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-285">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="e3a5f-286">Double check the URI you provided for the nested template.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-286">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="e3a5f-287">If the template exists in a storage account, make sure the URI is accessible.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-287">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="e3a5f-288">You may need to pass a SAS token.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-288">You may need to pass a SAS token.</span></span> <span data-ttu-id="e3a5f-289">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-289">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

### <a name="requestdisallowedbypolicy"></a><span data-ttu-id="e3a5f-290">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="e3a5f-290">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="e3a5f-291">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-291">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="e3a5f-292">In the error message, look for the policy identifier.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-292">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="e3a5f-293">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-293">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="e3a5f-294">In **Azure CLI 2.0**, provide the name of the policy definition:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-294">In **Azure CLI 2.0**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="e3a5f-295">For more information about policies, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-295">For more information about policies, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

### <a name="authorization-failed"></a><span data-ttu-id="e3a5f-296">Authorization failed</span><span class="sxs-lookup"><span data-stu-id="e3a5f-296">Authorization failed</span></span>
<span data-ttu-id="e3a5f-297">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-297">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="e3a5f-298">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-298">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="e3a5f-299">For example, if your account is assigned to the Reader role, you are not able to create resources.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-299">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="e3a5f-300">In that case, you see an error message indicating that authorization failed.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-300">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="e3a5f-301">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-301">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

## <a name="troubleshooting-tricks-and-tips"></a><span data-ttu-id="e3a5f-302">Troubleshooting tricks and tips</span><span class="sxs-lookup"><span data-stu-id="e3a5f-302">Troubleshooting tricks and tips</span></span>

### <a name="enable-debug-logging"></a><span data-ttu-id="e3a5f-303">Enable debug logging</span><span class="sxs-lookup"><span data-stu-id="e3a5f-303">Enable debug logging</span></span>
<span data-ttu-id="e3a5f-304">You can discover valuable information about how your deployment is processed by logging the request, response, or both.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-304">You can discover valuable information about how your deployment is processed by logging the request, response, or both.</span></span>

- <span data-ttu-id="e3a5f-305">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3a5f-305">PowerShell</span></span>

   <span data-ttu-id="e3a5f-306">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-306">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="e3a5f-307">Examine the request content with the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-307">Examine the request content with the following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="e3a5f-308">Or, the response content with:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-308">Or, the response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="e3a5f-309">This information can help you determine whether a value in the template is being incorrectly set.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-309">This information can help you determine whether a value in the template is being incorrectly set.</span></span>

- <span data-ttu-id="e3a5f-310">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e3a5f-310">Azure CLI 2.0</span></span>

   <span data-ttu-id="e3a5f-311">Examine the deployment operations with the following command:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-311">Examine the deployment operations with the following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="e3a5f-312">Nested template</span><span class="sxs-lookup"><span data-stu-id="e3a5f-312">Nested template</span></span>

   <span data-ttu-id="e3a5f-313">To log debug information for a nested template, use the **debugSetting** element.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-313">To log debug information for a nested template, use the **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


### <a name="create-a-troubleshooting-template"></a><span data-ttu-id="e3a5f-314">Create a troubleshooting template</span><span class="sxs-lookup"><span data-stu-id="e3a5f-314">Create a troubleshooting template</span></span>
<span data-ttu-id="e3a5f-315">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-315">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span></span> <span data-ttu-id="e3a5f-316">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-316">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span></span> <span data-ttu-id="e3a5f-317">For example, suppose you are receiving an error when referencing a resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-317">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="e3a5f-318">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-318">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span></span> <span data-ttu-id="e3a5f-319">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-319">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="e3a5f-320">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-320">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span></span> <span data-ttu-id="e3a5f-321">Test your template by breaking it into simplified templates.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-321">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="e3a5f-322">First, create a template that deploys only a single resource (like a SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-322">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="e3a5f-323">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-323">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="e3a5f-324">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-324">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="e3a5f-325">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-325">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span></span> 

### <a name="check-deployment-sequence"></a><span data-ttu-id="e3a5f-326">Check deployment sequence</span><span class="sxs-lookup"><span data-stu-id="e3a5f-326">Check deployment sequence</span></span>

<span data-ttu-id="e3a5f-327">Many deployment errors happen when resources are deployed in an unexpected sequence.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-327">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="e3a5f-328">These errors arise when dependencies are not correctly set.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-328">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="e3a5f-329">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-329">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span></span> <span data-ttu-id="e3a5f-330">You get an error stating that a resource is not found.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-330">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="e3a5f-331">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-331">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span></span> <span data-ttu-id="e3a5f-332">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-332">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="e3a5f-333">However, your second attempt fails because the required resource did not complete in time.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-333">However, your second attempt fails because the required resource did not complete in time.</span></span> 

<span data-ttu-id="e3a5f-334">But, you want to avoid setting dependencies that are not needed.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-334">But, you want to avoid setting dependencies that are not needed.</span></span> <span data-ttu-id="e3a5f-335">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-335">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="e3a5f-336">In addition, you may create circular dependencies that block the deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-336">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="e3a5f-337">The [reference](resource-group-template-functions.md#reference) function creates an implicit dependency on the resource you specify as a parameter in the function, if that resource is deployed in the same template.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-337">The [reference](resource-group-template-functions.md#reference) function creates an implicit dependency on the resource you specify as a parameter in the function, if that resource is deployed in the same template.</span></span> <span data-ttu-id="e3a5f-338">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-338">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="e3a5f-339">The [resourceId](resource-group-template-functions.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-339">The [resourceId](resource-group-template-functions.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span></span>

<span data-ttu-id="e3a5f-340">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-340">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="e3a5f-341">To view the order of deployment operations:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-341">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="e3a5f-342">Select the deployment history for your resource group.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-342">Select the deployment history for your resource group.</span></span>

   ![select deployment history](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/select-deployment.png)

2. <span data-ttu-id="e3a5f-344">Select a deployment from the history, and select **Events**.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-344">Select a deployment from the history, and select **Events**.</span></span>

   ![select deployment events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/select-deployment-events.png)

3. <span data-ttu-id="e3a5f-346">Examine the sequence of events for each resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-346">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="e3a5f-347">Pay attention to the status of each operation.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-347">Pay attention to the status of each operation.</span></span> <span data-ttu-id="e3a5f-348">For example, the following image shows three storage accounts that deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-348">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="e3a5f-349">Notice that the three storage accounts are started at the same time.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-349">Notice that the three storage accounts are started at the same time.</span></span>

   ![parallel deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/deployment-events-parallel.png)

   <span data-ttu-id="e3a5f-351">The next image shows three storage accounts that are not deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-351">The next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="e3a5f-352">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-352">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="e3a5f-353">Therefore, the first storage account is started, accepted, and completed before the next is started.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-353">Therefore, the first storage account is started, accepted, and completed before the next is started.</span></span>

   ![sequential deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-common-deployment-errors/deployment-events-sequence.png)

<span data-ttu-id="e3a5f-355">Real world scenarios can be considerably more complicated, but you can use the same technique to discover when deployment is started and completed for each resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-355">Real world scenarios can be considerably more complicated, but you can use the same technique to discover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="e3a5f-356">Look through your deployment events to see if the sequence is different than you would expect.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-356">Look through your deployment events to see if the sequence is different than you would expect.</span></span> <span data-ttu-id="e3a5f-357">If so, reevaluate the dependencies for this resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-357">If so, reevaluate the dependencies for this resource.</span></span>

<span data-ttu-id="e3a5f-358">Resource Manager identifies circular dependencies during template validation.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-358">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="e3a5f-359">It returns an error message that specifically states a circular dependency exists.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-359">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="e3a5f-360">To solve a circular dependency:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-360">To solve a circular dependency:</span></span>

1. <span data-ttu-id="e3a5f-361">In your template, find the resource identified in the circular dependency.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-361">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="e3a5f-362">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-362">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="e3a5f-363">Examine those resources to see which resources they depend on.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-363">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="e3a5f-364">Follow the dependencies until you notice a resource that depends on the original resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-364">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="e3a5f-365">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-365">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="e3a5f-366">Remove those dependencies.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-366">Remove those dependencies.</span></span> <span data-ttu-id="e3a5f-367">If you are unsure that a dependency is needed, try removing it.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-367">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="e3a5f-368">Redeploy the template.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-368">Redeploy the template.</span></span>

<span data-ttu-id="e3a5f-369">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-369">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="e3a5f-370">If you encounter an error, add the dependency back into the template.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-370">If you encounter an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="e3a5f-371">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-371">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="e3a5f-372">Configure those child resources to deploy after the resources involved in the circular dependency.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-372">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="e3a5f-373">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-373">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="e3a5f-374">You can deploy them in the following order:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-374">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="e3a5f-375">vm1</span><span class="sxs-lookup"><span data-stu-id="e3a5f-375">vm1</span></span>
2. <span data-ttu-id="e3a5f-376">vm2</span><span class="sxs-lookup"><span data-stu-id="e3a5f-376">vm2</span></span>
3. <span data-ttu-id="e3a5f-377">Extension on vm1 depends on vm1 and vm2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-377">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="e3a5f-378">The extension sets values on vm1 that it gets from vm2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-378">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="e3a5f-379">Extension on vm2 depends on vm1 and vm2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-379">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="e3a5f-380">The extension sets values on vm2 that it gets from vm1.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-380">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="e3a5f-381">The same approach works for App Service apps.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-381">The same approach works for App Service apps.</span></span> <span data-ttu-id="e3a5f-382">Consider moving configuration values into a child resource of the app resource.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-382">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="e3a5f-383">You can deploy two web apps in the following order:</span><span class="sxs-lookup"><span data-stu-id="e3a5f-383">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="e3a5f-384">webapp1</span><span class="sxs-lookup"><span data-stu-id="e3a5f-384">webapp1</span></span>
2. <span data-ttu-id="e3a5f-385">webapp2</span><span class="sxs-lookup"><span data-stu-id="e3a5f-385">webapp2</span></span>
3. <span data-ttu-id="e3a5f-386">config for webapp1 depends on webapp1 and webapp2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-386">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="e3a5f-387">It contains app settings with values from webapp2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-387">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="e3a5f-388">config for webapp2 depends on webapp1 and webapp2.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-388">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="e3a5f-389">It contains app settings with values from webapp1.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-389">It contains app settings with values from webapp1.</span></span>

## <a name="troubleshooting-other-services"></a><span data-ttu-id="e3a5f-390">Troubleshooting other services</span><span class="sxs-lookup"><span data-stu-id="e3a5f-390">Troubleshooting other services</span></span>
<span data-ttu-id="e3a5f-391">If the preceding deployment error codes did not help you troubleshoot your issue, you can find more detailed troubleshooting guidance for each Azure service.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-391">If the preceding deployment error codes did not help you troubleshoot your issue, you can find more detailed troubleshooting guidance for each Azure service.</span></span>

<span data-ttu-id="e3a5f-392">The following table lists troubleshooting topics for Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-392">The following table lists troubleshooting topics for Virtual Machines.</span></span>

| <span data-ttu-id="e3a5f-393">Error</span><span class="sxs-lookup"><span data-stu-id="e3a5f-393">Error</span></span> | <span data-ttu-id="e3a5f-394">Articles</span><span class="sxs-lookup"><span data-stu-id="e3a5f-394">Articles</span></span> |
| --- | --- |
| <span data-ttu-id="e3a5f-395">Custom script extension errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-395">Custom script extension errors</span></span> |[<span data-ttu-id="e3a5f-396">Windows VM extension failures</span><span class="sxs-lookup"><span data-stu-id="e3a5f-396">Windows VM extension failures</span></span>](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)<br /><span data-ttu-id="e3a5f-397">or</span><span class="sxs-lookup"><span data-stu-id="e3a5f-397">or</span></span><br />[<span data-ttu-id="e3a5f-398">Linux VM extension failures</span><span class="sxs-lookup"><span data-stu-id="e3a5f-398">Linux VM extension failures</span></span>](../virtual-machines/linux/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e3a5f-399">OS image provisioning errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-399">OS image provisioning errors</span></span> |[<span data-ttu-id="e3a5f-400">New Windows VM errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-400">New Windows VM errors</span></span>](../virtual-machines/windows/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)<br /><span data-ttu-id="e3a5f-401">or</span><span class="sxs-lookup"><span data-stu-id="e3a5f-401">or</span></span><br />[<span data-ttu-id="e3a5f-402">New Linux VM errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-402">New Linux VM errors</span></span>](../virtual-machines/linux/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e3a5f-403">Allocation failures</span><span class="sxs-lookup"><span data-stu-id="e3a5f-403">Allocation failures</span></span> |[<span data-ttu-id="e3a5f-404">Windows VM allocation failures</span><span class="sxs-lookup"><span data-stu-id="e3a5f-404">Windows VM allocation failures</span></span>](../virtual-machines/windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)<br /><span data-ttu-id="e3a5f-405">or</span><span class="sxs-lookup"><span data-stu-id="e3a5f-405">or</span></span><br />[<span data-ttu-id="e3a5f-406">Linux VM allocation failures</span><span class="sxs-lookup"><span data-stu-id="e3a5f-406">Linux VM allocation failures</span></span>](../virtual-machines/linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e3a5f-407">Secure Shell (SSH) errors when attempting to connect</span><span class="sxs-lookup"><span data-stu-id="e3a5f-407">Secure Shell (SSH) errors when attempting to connect</span></span> |[<span data-ttu-id="e3a5f-408">Secure Shell connections to Linux VM</span><span class="sxs-lookup"><span data-stu-id="e3a5f-408">Secure Shell connections to Linux VM</span></span>](../virtual-machines/linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e3a5f-409">Errors connecting to application running on VM</span><span class="sxs-lookup"><span data-stu-id="e3a5f-409">Errors connecting to application running on VM</span></span> |[<span data-ttu-id="e3a5f-410">Application running on Windows VM</span><span class="sxs-lookup"><span data-stu-id="e3a5f-410">Application running on Windows VM</span></span>](../virtual-machines/windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)<br /><span data-ttu-id="e3a5f-411">or</span><span class="sxs-lookup"><span data-stu-id="e3a5f-411">or</span></span><br />[<span data-ttu-id="e3a5f-412">Application running on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="e3a5f-412">Application running on a Linux VM</span></span>](../virtual-machines/linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e3a5f-413">Remote Desktop connection errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-413">Remote Desktop connection errors</span></span> |[<span data-ttu-id="e3a5f-414">Remote Desktop connections to Windows VM</span><span class="sxs-lookup"><span data-stu-id="e3a5f-414">Remote Desktop connections to Windows VM</span></span>](../virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e3a5f-415">Connection errors resolved by redeploying</span><span class="sxs-lookup"><span data-stu-id="e3a5f-415">Connection errors resolved by redeploying</span></span> |[<span data-ttu-id="e3a5f-416">Redeploy Virtual Machine to new Azure node</span><span class="sxs-lookup"><span data-stu-id="e3a5f-416">Redeploy Virtual Machine to new Azure node</span></span>](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e3a5f-417">Cloud service errors</span><span class="sxs-lookup"><span data-stu-id="e3a5f-417">Cloud service errors</span></span> |[<span data-ttu-id="e3a5f-418">Cloud service deployment problems</span><span class="sxs-lookup"><span data-stu-id="e3a5f-418">Cloud service deployment problems</span></span>](../cloud-services/cloud-services-troubleshoot-deployment-problems.md) |

<span data-ttu-id="e3a5f-419">The following table lists troubleshooting topics for other Azure services.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-419">The following table lists troubleshooting topics for other Azure services.</span></span> <span data-ttu-id="e3a5f-420">It focuses on issues related to deploying or configuring resources.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-420">It focuses on issues related to deploying or configuring resources.</span></span> <span data-ttu-id="e3a5f-421">If you need help troubleshooting run-time issues with a resource, see the documentation for that Azure service.</span><span class="sxs-lookup"><span data-stu-id="e3a5f-421">If you need help troubleshooting run-time issues with a resource, see the documentation for that Azure service.</span></span>

| <span data-ttu-id="e3a5f-422">Service</span><span class="sxs-lookup"><span data-stu-id="e3a5f-422">Service</span></span> | <span data-ttu-id="e3a5f-423">Article</span><span class="sxs-lookup"><span data-stu-id="e3a5f-423">Article</span></span> |
| --- | --- |
| <span data-ttu-id="e3a5f-424">Automation</span><span class="sxs-lookup"><span data-stu-id="e3a5f-424">Automation</span></span> |[<span data-ttu-id="e3a5f-425">Troubleshooting tips for common errors in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e3a5f-425">Troubleshooting tips for common errors in Azure Automation</span></span>](../automation/automation-troubleshooting-automation-errors.md) |
| <span data-ttu-id="e3a5f-426">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e3a5f-426">Azure Stack</span></span> |[<span data-ttu-id="e3a5f-427">Microsoft Azure Stack troubleshooting</span><span class="sxs-lookup"><span data-stu-id="e3a5f-427">Microsoft Azure Stack troubleshooting</span></span>](../azure-stack/azure-stack-troubleshooting.md) |
| <span data-ttu-id="e3a5f-428">Data Factory</span><span class="sxs-lookup"><span data-stu-id="e3a5f-428">Data Factory</span></span> |[<span data-ttu-id="e3a5f-429">Troubleshoot Data Factory issues</span><span class="sxs-lookup"><span data-stu-id="e3a5f-429">Troubleshoot Data Factory issues</span></span>](../data-factory/data-factory-troubleshoot.md) |
| <span data-ttu-id="e3a5f-430">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3a5f-430">Service Fabric</span></span> |[<span data-ttu-id="e3a5f-431">Monitor and diagnose Azure Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="e3a5f-431">Monitor and diagnose Azure Service Fabric applications</span></span>](../service-fabric/service-fabric-diagnostics-overview.md) |
| <span data-ttu-id="e3a5f-432">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e3a5f-432">Site Recovery</span></span> |[<span data-ttu-id="e3a5f-433">Monitor and troubleshoot protection for virtual machines and physical servers</span><span class="sxs-lookup"><span data-stu-id="e3a5f-433">Monitor and troubleshoot protection for virtual machines and physical servers</span></span>](../site-recovery/site-recovery-monitoring-and-troubleshooting.md) |
| <span data-ttu-id="e3a5f-434">Storage</span><span class="sxs-lookup"><span data-stu-id="e3a5f-434">Storage</span></span> |[<span data-ttu-id="e3a5f-435">Monitor, diagnose, and troubleshoot Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e3a5f-435">Monitor, diagnose, and troubleshoot Microsoft Azure Storage</span></span>](../storage/storage-monitoring-diagnosing-troubleshooting.md) |
| <span data-ttu-id="e3a5f-436">StorSimple</span><span class="sxs-lookup"><span data-stu-id="e3a5f-436">StorSimple</span></span> |[<span data-ttu-id="e3a5f-437">Troubleshoot StorSimple device deployment issues</span><span class="sxs-lookup"><span data-stu-id="e3a5f-437">Troubleshoot StorSimple device deployment issues</span></span>](../storsimple/storsimple-troubleshoot-deployment.md) |
| <span data-ttu-id="e3a5f-438">SQL Database</span><span class="sxs-lookup"><span data-stu-id="e3a5f-438">SQL Database</span></span> |[<span data-ttu-id="e3a5f-439">Troubleshoot connection issues to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e3a5f-439">Troubleshoot connection issues to Azure SQL Database</span></span>](../sql-database/sql-database-troubleshoot-common-connection-issues.md) |
| <span data-ttu-id="e3a5f-440">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e3a5f-440">SQL Data Warehouse</span></span> |[<span data-ttu-id="e3a5f-441">Troubleshooting Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e3a5f-441">Troubleshooting Azure SQL Data Warehouse</span></span>](../sql-data-warehouse/sql-data-warehouse-troubleshoot.md) |

## <a name="next-steps"></a><span data-ttu-id="e3a5f-442">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3a5f-442">Next steps</span></span>
* <span data-ttu-id="e3a5f-443">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-443">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="e3a5f-444">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="e3a5f-444">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>









