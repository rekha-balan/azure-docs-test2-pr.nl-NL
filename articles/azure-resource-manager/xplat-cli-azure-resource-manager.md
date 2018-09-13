---
title: Manage resources with the Azure CLI | Microsoft Docs
description: Use the Azure Command-Line Interface (CLI) to manage Azure resources and groups
editor: ''
manager: timlt
documentationcenter: ''
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: bd6f81ee12a7bb655166cf059236175bfb9994e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564055"
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="672f8-103">Use the Azure CLI to manage Azure resources and resource groups</span><span class="sxs-lookup"><span data-stu-id="672f8-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="672f8-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="672f8-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="672f8-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="672f8-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="672f8-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="672f8-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="672f8-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="672f8-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command. Make sure the CLI is in Resource Manager mode (run `azure config mode arm`). If you've done these things, you're ready to go.
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="672f8-115">Get resource groups and resources</span><span class="sxs-lookup"><span data-stu-id="672f8-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="672f8-116">Resource groups</span><span class="sxs-lookup"><span data-stu-id="672f8-116">Resource groups</span></span>
<span data-ttu-id="672f8-117">To get a list of all resource groups in your subscription and their locations, run this command.</span><span class="sxs-lookup"><span data-stu-id="672f8-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="672f8-118">Resources</span><span class="sxs-lookup"><span data-stu-id="672f8-118">Resources</span></span>
 <span data-ttu-id="672f8-119">To list all resources in a group, such as one with name *testRG*, use the following command.</span><span class="sxs-lookup"><span data-stu-id="672f8-119">To list all resources in a group, such as one with name *testRG*, use the following command.</span></span>

    azure resource list testRG

<span data-ttu-id="672f8-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following.</span><span class="sxs-lookup"><span data-stu-id="672f8-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="672f8-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span><span class="sxs-lookup"><span data-stu-id="672f8-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="672f8-122">This parameter indicates the type of the resource you are requesting information on.</span><span class="sxs-lookup"><span data-stu-id="672f8-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter. If you're unsure about the API version, consult the template file and find the apiVersion field for the resource. For more about API versions in Resource Manager, see [Resource Manager providers, regions, API versions, and schemas](resource-manager-supported-services.md).
> 
> 

<span data-ttu-id="672f8-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span><span class="sxs-lookup"><span data-stu-id="672f8-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="672f8-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span><span class="sxs-lookup"><span data-stu-id="672f8-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="672f8-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span><span class="sxs-lookup"><span data-stu-id="672f8-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> If you want, save the JSON data to file by using the &gt; character to direct the output to a file. For example:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="672f8-131">Tags</span><span class="sxs-lookup"><span data-stu-id="672f8-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="672f8-132">Manage resources</span><span class="sxs-lookup"><span data-stu-id="672f8-132">Manage resources</span></span>
<span data-ttu-id="672f8-133">To add a resource such as a storage account to a resource group, run a command similar to:</span><span class="sxs-lookup"><span data-stu-id="672f8-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="672f8-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span><span class="sxs-lookup"><span data-stu-id="672f8-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="672f8-135">To delete an existing resource such as a virtual machine resource, use a command like the following.</span><span class="sxs-lookup"><span data-stu-id="672f8-135">To delete an existing resource such as a virtual machine resource, use a command like the following.</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="672f8-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span><span class="sxs-lookup"><span data-stu-id="672f8-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="672f8-137">The following example shows how to move a Redis Cache to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="672f8-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="672f8-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span><span class="sxs-lookup"><span data-stu-id="672f8-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="672f8-139">Control access to resources</span><span class="sxs-lookup"><span data-stu-id="672f8-139">Control access to resources</span></span>
<span data-ttu-id="672f8-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="672f8-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="672f8-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="672f8-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="672f8-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span><span class="sxs-lookup"><span data-stu-id="672f8-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="672f8-143">Then run the **policy definition create** command:</span><span class="sxs-lookup"><span data-stu-id="672f8-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="672f8-144">This command shows output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="672f8-144">This command shows output similar to the following.</span></span>

    + <span data-ttu-id="672f8-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="672f8-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="672f8-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="672f8-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="672f8-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span><span class="sxs-lookup"><span data-stu-id="672f8-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="672f8-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span><span class="sxs-lookup"><span data-stu-id="672f8-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="672f8-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="672f8-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="672f8-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span><span class="sxs-lookup"><span data-stu-id="672f8-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="672f8-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span><span class="sxs-lookup"><span data-stu-id="672f8-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="672f8-152">Export a resource group as a template</span><span class="sxs-lookup"><span data-stu-id="672f8-152">Export a resource group as a template</span></span>
<span data-ttu-id="672f8-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span><span class="sxs-lookup"><span data-stu-id="672f8-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="672f8-154">Exporting the template offers two benefits:</span><span class="sxs-lookup"><span data-stu-id="672f8-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="672f8-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span><span class="sxs-lookup"><span data-stu-id="672f8-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="672f8-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span><span class="sxs-lookup"><span data-stu-id="672f8-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="672f8-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span><span class="sxs-lookup"><span data-stu-id="672f8-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="672f8-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span><span class="sxs-lookup"><span data-stu-id="672f8-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="672f8-159">However, the generated template contains only a minimal number of parameters and no variables.</span><span class="sxs-lookup"><span data-stu-id="672f8-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="672f8-160">Most of the values in the template are hard-coded.</span><span class="sxs-lookup"><span data-stu-id="672f8-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="672f8-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span><span class="sxs-lookup"><span data-stu-id="672f8-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="672f8-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="672f8-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="672f8-163">(Substitute a local directory appropriate for your operating system environment.)</span><span class="sxs-lookup"><span data-stu-id="672f8-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="672f8-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span><span class="sxs-lookup"><span data-stu-id="672f8-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="672f8-165">The template includes all parameters and variables defined for the original deployment.</span><span class="sxs-lookup"><span data-stu-id="672f8-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="672f8-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span><span class="sxs-lookup"><span data-stu-id="672f8-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="672f8-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span><span class="sxs-lookup"><span data-stu-id="672f8-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="672f8-168">For example:</span><span class="sxs-lookup"><span data-stu-id="672f8-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Template export is in preview, and not all resource types currently support exporting a template. When attempting to export a template, you may see an error that states some resources were not exported. If needed, manually define these resources in your template after downloading it.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="672f8-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="672f8-172">Next steps</span></span>
* <span data-ttu-id="672f8-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="672f8-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="672f8-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="672f8-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="672f8-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="672f8-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

