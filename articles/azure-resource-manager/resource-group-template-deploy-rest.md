---
title: Deploy resources with REST API and template | Microsoft Docs
description: Use Azure Resource Manager and Resource Manager REST API to deploy a resources to Azure. The resources are defined in a Resource Manager template.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: d2d9cff50d6ba5dc990140059536786fb7281827
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556515"
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="2c5f8-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span><span class="sxs-lookup"><span data-stu-id="2c5f8-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="2c5f8-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> For help with debugging an error during deployment, see:
> 
> * [View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error
> * [Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors
> 
> 

<span data-ttu-id="2c5f8-113">Your template can be either a local file or an external file that is available through a URI.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="2c5f8-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="2c5f8-115">Deploy with the REST API</span><span class="sxs-lookup"><span data-stu-id="2c5f8-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="2c5f8-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="2c5f8-117">If you do not have an existing resource group, create a resource group.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="2c5f8-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="2c5f8-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="2c5f8-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="2c5f8-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="2c5f8-122">Create a deployment.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-122">Create a deployment.</span></span> <span data-ttu-id="2c5f8-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="2c5f8-124">For information about the template file, see [Parameter file](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="2c5f8-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="2c5f8-126">Notice the **mode** is set to **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="2c5f8-127">To run a complete deployment, set **mode** to **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="2c5f8-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="2c5f8-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="2c5f8-130">You can set up your storage account to use a shared access signature (SAS) token.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="2c5f8-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/fileservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/fileservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="2c5f8-132">Get the status of the template deployment.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-132">Get the status of the template deployment.</span></span> <span data-ttu-id="2c5f8-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="2c5f8-134">Parameter file</span><span class="sxs-lookup"><span data-stu-id="2c5f8-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="2c5f8-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c5f8-135">Next steps</span></span>
* <span data-ttu-id="2c5f8-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="2c5f8-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="2c5f8-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2c5f8-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="2c5f8-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="2c5f8-141">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c5f8-141">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2c5f8-142">This series covers application architecture, access and security, availability and scale, and application deployment.</span><span class="sxs-lookup"><span data-stu-id="2c5f8-142">This series covers application architecture, access and security, availability and scale, and application deployment.</span></span>

