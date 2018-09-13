---
title: Azure Resource Manager templates for cloud consistency | Microsoft Docs
description: Develop Azure Resource Manager templates for cloud consistency. Create new or update existing templates for Azure Stack.
services: azure-resource-manager
documentationcenter: na
author: marcvaneijk
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2018
ms.author: mavane
ms.openlocfilehash: f1ff151c0b8d89910949d961b732c10901f19293
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868120"
---
# <a name="develop-azure-resource-manager-templates-for-cloud-consistency"></a><span data-ttu-id="9831c-104">Develop Azure Resource Manager templates for cloud consistency</span><span class="sxs-lookup"><span data-stu-id="9831c-104">Develop Azure Resource Manager templates for cloud consistency</span></span>

<span data-ttu-id="9831c-105">A key benefit of Azure is consistency.</span><span class="sxs-lookup"><span data-stu-id="9831c-105">A key benefit of Azure is consistency.</span></span> <span data-ttu-id="9831c-106">Development investments for one location are reusable in another.</span><span class="sxs-lookup"><span data-stu-id="9831c-106">Development investments for one location are reusable in another.</span></span> <span data-ttu-id="9831c-107">A template makes your deployments consistent and repeatable across environments, including the global Azure, Azure sovereign clouds, and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-107">A template makes your deployments consistent and repeatable across environments, including the global Azure, Azure sovereign clouds, and Azure Stack.</span></span> <span data-ttu-id="9831c-108">To reuse templates across clouds, however, you need to consider cloud-specific dependencies as this guide explains.</span><span class="sxs-lookup"><span data-stu-id="9831c-108">To reuse templates across clouds, however, you need to consider cloud-specific dependencies as this guide explains.</span></span>

<span data-ttu-id="9831c-109">Microsoft offers intelligent, enterprise-ready cloud services in many locations, including:</span><span class="sxs-lookup"><span data-stu-id="9831c-109">Microsoft offers intelligent, enterprise-ready cloud services in many locations, including:</span></span>

* <span data-ttu-id="9831c-110">The global Azure platform supported by a growing network of Microsoft-managed datacenters in regions around the world.</span><span class="sxs-lookup"><span data-stu-id="9831c-110">The global Azure platform supported by a growing network of Microsoft-managed datacenters in regions around the world.</span></span>
* <span data-ttu-id="9831c-111">Isolated sovereign clouds like Azure Germany, Azure Government, and Azure China (Azure operated by 21Vianet).</span><span class="sxs-lookup"><span data-stu-id="9831c-111">Isolated sovereign clouds like Azure Germany, Azure Government, and Azure China (Azure operated by 21Vianet).</span></span> <span data-ttu-id="9831c-112">Sovereign clouds provide a consistent platform with most of the same great features that global Azure customers have access to.</span><span class="sxs-lookup"><span data-stu-id="9831c-112">Sovereign clouds provide a consistent platform with most of the same great features that global Azure customers have access to.</span></span>
* <span data-ttu-id="9831c-113">Azure Stack, a hybrid cloud platform that lets you deliver Azure services from your organization's datacenter.</span><span class="sxs-lookup"><span data-stu-id="9831c-113">Azure Stack, a hybrid cloud platform that lets you deliver Azure services from your organization's datacenter.</span></span> <span data-ttu-id="9831c-114">Enterprises can set up Azure Stack in their own datacenters, or consume Azure Services from service providers, running Azure Stack in their facilities (sometimes known as hosted regions).</span><span class="sxs-lookup"><span data-stu-id="9831c-114">Enterprises can set up Azure Stack in their own datacenters, or consume Azure Services from service providers, running Azure Stack in their facilities (sometimes known as hosted regions).</span></span>

<span data-ttu-id="9831c-115">At the core of all these clouds, Azure Resource Manager provides an API that allows a wide variety of user interfaces to communicate with the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="9831c-115">At the core of all these clouds, Azure Resource Manager provides an API that allows a wide variety of user interfaces to communicate with the Azure platform.</span></span> <span data-ttu-id="9831c-116">This API gives you powerful infrastructure-as-code capabilities.</span><span class="sxs-lookup"><span data-stu-id="9831c-116">This API gives you powerful infrastructure-as-code capabilities.</span></span> <span data-ttu-id="9831c-117">Any type of resource that is available on the Azure cloud platform can be deployed and configured with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9831c-117">Any type of resource that is available on the Azure cloud platform can be deployed and configured with Azure Resource Manager.</span></span> <span data-ttu-id="9831c-118">With a single template, you can deploy and configure your complete application to an operational end state.</span><span class="sxs-lookup"><span data-stu-id="9831c-118">With a single template, you can deploy and configure your complete application to an operational end state.</span></span>

![Azure environments](./media/templates-cloud-consistency/environments.png)

<span data-ttu-id="9831c-120">The consistency of global Azure, the sovereign clouds, hosted clouds, and a cloud in your datacenter helps you benefit from Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9831c-120">The consistency of global Azure, the sovereign clouds, hosted clouds, and a cloud in your datacenter helps you benefit from Azure Resource Manager.</span></span> <span data-ttu-id="9831c-121">You can reuse your development investments across these clouds when you set up template-based resource deployment and configuration.</span><span class="sxs-lookup"><span data-stu-id="9831c-121">You can reuse your development investments across these clouds when you set up template-based resource deployment and configuration.</span></span>

<span data-ttu-id="9831c-122">However, even though the global, sovereign, hosted, and hybrid clouds provide consistent services, not all clouds are identical.</span><span class="sxs-lookup"><span data-stu-id="9831c-122">However, even though the global, sovereign, hosted, and hybrid clouds provide consistent services, not all clouds are identical.</span></span> <span data-ttu-id="9831c-123">As a result, you can create a template with dependencies on features available only in a specific cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-123">As a result, you can create a template with dependencies on features available only in a specific cloud.</span></span>

<span data-ttu-id="9831c-124">The rest of this guide describes the areas to consider when planning to develop new or updating existing Azure Resource Manager templates for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-124">The rest of this guide describes the areas to consider when planning to develop new or updating existing Azure Resource Manager templates for Azure Stack.</span></span> <span data-ttu-id="9831c-125">In general, your checklist should include the following items:</span><span class="sxs-lookup"><span data-stu-id="9831c-125">In general, your checklist should include the following items:</span></span>

* <span data-ttu-id="9831c-126">Verify that the functions, endpoints, services, and other resources in your template are available in the target deployment locations.</span><span class="sxs-lookup"><span data-stu-id="9831c-126">Verify that the functions, endpoints, services, and other resources in your template are available in the target deployment locations.</span></span>
* <span data-ttu-id="9831c-127">Store nested templates and configuration artifacts in accessible locations, ensuring access across clouds.</span><span class="sxs-lookup"><span data-stu-id="9831c-127">Store nested templates and configuration artifacts in accessible locations, ensuring access across clouds.</span></span>
* <span data-ttu-id="9831c-128">Use dynamic references instead of hard-coding links and elements.</span><span class="sxs-lookup"><span data-stu-id="9831c-128">Use dynamic references instead of hard-coding links and elements.</span></span>
* <span data-ttu-id="9831c-129">Ensure the template parameters you use work in the target clouds.</span><span class="sxs-lookup"><span data-stu-id="9831c-129">Ensure the template parameters you use work in the target clouds.</span></span>
* <span data-ttu-id="9831c-130">Verify that resource-specific properties are available the target clouds.</span><span class="sxs-lookup"><span data-stu-id="9831c-130">Verify that resource-specific properties are available the target clouds.</span></span>

<span data-ttu-id="9831c-131">For an introduction to Azure Resource Manger templates, see [Template deployment](resource-group-overview.md#template-deployment).</span><span class="sxs-lookup"><span data-stu-id="9831c-131">For an introduction to Azure Resource Manger templates, see [Template deployment](resource-group-overview.md#template-deployment).</span></span>

## <a name="ensure-template-functions-work"></a><span data-ttu-id="9831c-132">Ensure template functions work</span><span class="sxs-lookup"><span data-stu-id="9831c-132">Ensure template functions work</span></span>

<span data-ttu-id="9831c-133">The basic syntax of a Resource Manager template is JSON.</span><span class="sxs-lookup"><span data-stu-id="9831c-133">The basic syntax of a Resource Manager template is JSON.</span></span> <span data-ttu-id="9831c-134">Templates use a superset of JSON, extending the syntax with expressions and functions.</span><span class="sxs-lookup"><span data-stu-id="9831c-134">Templates use a superset of JSON, extending the syntax with expressions and functions.</span></span> <span data-ttu-id="9831c-135">The template language processor is frequently updated to support additional template functions.</span><span class="sxs-lookup"><span data-stu-id="9831c-135">The template language processor is frequently updated to support additional template functions.</span></span> <span data-ttu-id="9831c-136">For a detailed explanation of the available template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="9831c-136">For a detailed explanation of the available template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span>

<span data-ttu-id="9831c-137">New template functions that are introduced to Azure Resource Manager aren't immediately available in the sovereign clouds or Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-137">New template functions that are introduced to Azure Resource Manager aren't immediately available in the sovereign clouds or Azure Stack.</span></span> <span data-ttu-id="9831c-138">To deploy a template successfully, all functions referenced in the template must be available in the target cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-138">To deploy a template successfully, all functions referenced in the template must be available in the target cloud.</span></span> 

<span data-ttu-id="9831c-139">Azure Resource Manager capabilities will always be introduced to global Azure first.</span><span class="sxs-lookup"><span data-stu-id="9831c-139">Azure Resource Manager capabilities will always be introduced to global Azure first.</span></span> <span data-ttu-id="9831c-140">You can use the following PowerShell script to verify whether newly introduced template functions are also available in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="9831c-140">You can use the following PowerShell script to verify whether newly introduced template functions are also available in Azure Stack:</span></span> 

1. <span data-ttu-id="9831c-141">Make a clone of the GitHub repository: [https://github.com/marcvaneijk/arm-template-functions](https://github.com/marcvaneijk/arm-template-functions).</span><span class="sxs-lookup"><span data-stu-id="9831c-141">Make a clone of the GitHub repository: [https://github.com/marcvaneijk/arm-template-functions](https://github.com/marcvaneijk/arm-template-functions).</span></span>

1. <span data-ttu-id="9831c-142">Once you have a local clone of the repository, connect to the destination's Azure Resource Manager with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9831c-142">Once you have a local clone of the repository, connect to the destination's Azure Resource Manager with PowerShell.</span></span>

1. <span data-ttu-id="9831c-143">Import the psm1 module and execute the Test-AzureRmTemplateFunctions cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9831c-143">Import the psm1 module and execute the Test-AzureRmTemplateFunctions cmdlet:</span></span>

  ```powershell
  # Import the module
  Import-module <path to local clone>\AzureRmTemplateFunctions.psm1

  # Execute the Test-AzureRmTemplateFunctions cmdlet
  Test-AzureRmTemplateFunctions -path <path to local clone>
  ```

<span data-ttu-id="9831c-144">The script deploys multiple, minimized templates, each containing only unique template functions.</span><span class="sxs-lookup"><span data-stu-id="9831c-144">The script deploys multiple, minimized templates, each containing only unique template functions.</span></span> <span data-ttu-id="9831c-145">The output of the script reports the supported and unavailable template functions.</span><span class="sxs-lookup"><span data-stu-id="9831c-145">The output of the script reports the supported and unavailable template functions.</span></span>

## <a name="working-with-linked-artifacts"></a><span data-ttu-id="9831c-146">Working with linked artifacts</span><span class="sxs-lookup"><span data-stu-id="9831c-146">Working with linked artifacts</span></span>

<span data-ttu-id="9831c-147">A template can contain references to linked artifacts and contain a deployment resource that links to another template.</span><span class="sxs-lookup"><span data-stu-id="9831c-147">A template can contain references to linked artifacts and contain a deployment resource that links to another template.</span></span> <span data-ttu-id="9831c-148">The linked templates (also referred to as nested template) are retrieved by Resource Manager at runtime.</span><span class="sxs-lookup"><span data-stu-id="9831c-148">The linked templates (also referred to as nested template) are retrieved by Resource Manager at runtime.</span></span> <span data-ttu-id="9831c-149">A template can also contain references to artifacts for virtual machine (VM) extensions.</span><span class="sxs-lookup"><span data-stu-id="9831c-149">A template can also contain references to artifacts for virtual machine (VM) extensions.</span></span> <span data-ttu-id="9831c-150">These artifacts are retrieved by the VM extension running inside of the VM for configuration of the VM extension during the template deployment.</span><span class="sxs-lookup"><span data-stu-id="9831c-150">These artifacts are retrieved by the VM extension running inside of the VM for configuration of the VM extension during the template deployment.</span></span> 

<span data-ttu-id="9831c-151">The following sections describe considerations for cloud consistency when developing templates that include artifacts that are external to the main deployment template.</span><span class="sxs-lookup"><span data-stu-id="9831c-151">The following sections describe considerations for cloud consistency when developing templates that include artifacts that are external to the main deployment template.</span></span>

### <a name="use-nested-templates-across-regions"></a><span data-ttu-id="9831c-152">Use nested templates across regions</span><span class="sxs-lookup"><span data-stu-id="9831c-152">Use nested templates across regions</span></span>

<span data-ttu-id="9831c-153">Templates can be decomposed into small, reusable templates, each of which has a specific purpose and can be reused across deployment scenarios.</span><span class="sxs-lookup"><span data-stu-id="9831c-153">Templates can be decomposed into small, reusable templates, each of which has a specific purpose and can be reused across deployment scenarios.</span></span> <span data-ttu-id="9831c-154">To execute a deployment, you specify a single template known as the main or master template.</span><span class="sxs-lookup"><span data-stu-id="9831c-154">To execute a deployment, you specify a single template known as the main or master template.</span></span> <span data-ttu-id="9831c-155">It specifies the resources to deploy, such as virtual networks, VMs, and web apps.</span><span class="sxs-lookup"><span data-stu-id="9831c-155">It specifies the resources to deploy, such as virtual networks, VMs, and web apps.</span></span> <span data-ttu-id="9831c-156">The main template can also contain a link to another template, meaning you can nest templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-156">The main template can also contain a link to another template, meaning you can nest templates.</span></span> <span data-ttu-id="9831c-157">Likewise, a nested template can contain links to other templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-157">Likewise, a nested template can contain links to other templates.</span></span> <span data-ttu-id="9831c-158">You can nest up to five levels deep.</span><span class="sxs-lookup"><span data-stu-id="9831c-158">You can nest up to five levels deep.</span></span>

<span data-ttu-id="9831c-159">The following code shows how the templateLink parameter refers to a nested template:</span><span class="sxs-lookup"><span data-stu-id="9831c-159">The following code shows how the templateLink parameter refers to a nested template:</span></span>

```json
"resources": [
  {
     "apiVersion": "2017-05-10",
     "name": "linkedTemplate",
     "type": "Microsoft.Resources/deployments",
     "properties": {
       "mode": "incremental",
       "templateLink": {
          "uri":"https://mystorageaccount.blob.core.windows.net/AzureTemplates/vNet.json",
          "contentVersion":"1.0.0.0"
       }
     }
  }
]
```

<span data-ttu-id="9831c-160">Azure Resource Manager evaluates the main template at runtime and retrieves and evaluates each nested template.</span><span class="sxs-lookup"><span data-stu-id="9831c-160">Azure Resource Manager evaluates the main template at runtime and retrieves and evaluates each nested template.</span></span> <span data-ttu-id="9831c-161">After all nested templates are retrieved, the template is flattened, and further processing is initiated.</span><span class="sxs-lookup"><span data-stu-id="9831c-161">After all nested templates are retrieved, the template is flattened, and further processing is initiated.</span></span>

### <a name="make-linked-templates-accessible-across-clouds"></a><span data-ttu-id="9831c-162">Make linked templates accessible across clouds</span><span class="sxs-lookup"><span data-stu-id="9831c-162">Make linked templates accessible across clouds</span></span>

<span data-ttu-id="9831c-163">Consider where and how to store any linked templates you use.</span><span class="sxs-lookup"><span data-stu-id="9831c-163">Consider where and how to store any linked templates you use.</span></span> <span data-ttu-id="9831c-164">At runtime, Azure Resource Manager fetches—and therefore requires direct access to—any linked templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-164">At runtime, Azure Resource Manager fetches—and therefore requires direct access to—any linked templates.</span></span> <span data-ttu-id="9831c-165">A common practice is to use GitHub to store the nested templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-165">A common practice is to use GitHub to store the nested templates.</span></span> <span data-ttu-id="9831c-166">A GitHub repository can contain files that are accessible publicly through a URL.</span><span class="sxs-lookup"><span data-stu-id="9831c-166">A GitHub repository can contain files that are accessible publicly through a URL.</span></span> <span data-ttu-id="9831c-167">Although this technique works well for the public cloud and the sovereign clouds, an Azure Stack environment might be located on a corporate network or on a disconnected remote location, without any outbound Internet access.</span><span class="sxs-lookup"><span data-stu-id="9831c-167">Although this technique works well for the public cloud and the sovereign clouds, an Azure Stack environment might be located on a corporate network or on a disconnected remote location, without any outbound Internet access.</span></span> <span data-ttu-id="9831c-168">In those cases, Azure Resource Manager would fail to retrieve the nested templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-168">In those cases, Azure Resource Manager would fail to retrieve the nested templates.</span></span> 

<span data-ttu-id="9831c-169">A better practice for cross-cloud deployments is to store your linked templates in a location that is accessible for the target cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-169">A better practice for cross-cloud deployments is to store your linked templates in a location that is accessible for the target cloud.</span></span> <span data-ttu-id="9831c-170">Ideally all deployment artifacts are maintained in and deployed from a continuous integration/continuous development (CI/CD) pipeline.</span><span class="sxs-lookup"><span data-stu-id="9831c-170">Ideally all deployment artifacts are maintained in and deployed from a continuous integration/continuous development (CI/CD) pipeline.</span></span> <span data-ttu-id="9831c-171">Alternatively, you can store nested templates in a blob storage container, from which Azure Resource Manager can retrieve them.</span><span class="sxs-lookup"><span data-stu-id="9831c-171">Alternatively, you can store nested templates in a blob storage container, from which Azure Resource Manager can retrieve them.</span></span> 

<span data-ttu-id="9831c-172">Since the blob storage on each cloud uses a different endpoint fully qualified domain name (FQDN), configure the template with the location of the linked templates with two parameters.</span><span class="sxs-lookup"><span data-stu-id="9831c-172">Since the blob storage on each cloud uses a different endpoint fully qualified domain name (FQDN), configure the template with the location of the linked templates with two parameters.</span></span> <span data-ttu-id="9831c-173">Parameters can accept user input at deployment time.</span><span class="sxs-lookup"><span data-stu-id="9831c-173">Parameters can accept user input at deployment time.</span></span> <span data-ttu-id="9831c-174">Templates are typically authored and shared by multiple people, so a best practice is to use a standard name for these parameters.</span><span class="sxs-lookup"><span data-stu-id="9831c-174">Templates are typically authored and shared by multiple people, so a best practice is to use a standard name for these parameters.</span></span> <span data-ttu-id="9831c-175">Naming conventions help make templates more reusable across regions, clouds, and authors.</span><span class="sxs-lookup"><span data-stu-id="9831c-175">Naming conventions help make templates more reusable across regions, clouds, and authors.</span></span>

<span data-ttu-id="9831c-176">In the following code, `_artifactsLocation` is used to point to a single location, containing all deployment-related artifacts.</span><span class="sxs-lookup"><span data-stu-id="9831c-176">In the following code, `_artifactsLocation` is used to point to a single location, containing all deployment-related artifacts.</span></span> <span data-ttu-id="9831c-177">Notice that a default value is provided.</span><span class="sxs-lookup"><span data-stu-id="9831c-177">Notice that a default value is provided.</span></span> <span data-ttu-id="9831c-178">At deployment time, if no input value is specified for `_artifactsLocation`, the default value is used.</span><span class="sxs-lookup"><span data-stu-id="9831c-178">At deployment time, if no input value is specified for `_artifactsLocation`, the default value is used.</span></span> <span data-ttu-id="9831c-179">The `_artifactsLocationSasToken` is used as input for the `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="9831c-179">The `_artifactsLocationSasToken` is used as input for the `sasToken`.</span></span> <span data-ttu-id="9831c-180">The default value should be an empty string for scenarios where the `_artifactsLocation` isn't secured — for example, a public GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="9831c-180">The default value should be an empty string for scenarios where the `_artifactsLocation` isn't secured — for example, a public GitHub repository.</span></span>

```json
"parameters": {
  "_artifactsLocation": {
    "type": "string",
    "metadata": {
      "description": "The base URI where artifacts required by this template are located."
    },
    "defaultValue": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-custom-script-windows/"
  },
  "_artifactsLocationSasToken": {
    "type": "securestring",
    "metadata": {
      "description": "The sasToken required to access _artifactsLocation."
    },
    "defaultValue": ""
  }
}
```

<span data-ttu-id="9831c-181">Throughout the template, links are generated by combining the base URI (from the `_artifactsLocation` parameter) with an artifact-relative path and the `_artifactsLocationSasToken`.</span><span class="sxs-lookup"><span data-stu-id="9831c-181">Throughout the template, links are generated by combining the base URI (from the `_artifactsLocation` parameter) with an artifact-relative path and the `_artifactsLocationSasToken`.</span></span> <span data-ttu-id="9831c-182">The following code shows how to specify the link to the nested template using the uri template function:</span><span class="sxs-lookup"><span data-stu-id="9831c-182">The following code shows how to specify the link to the nested template using the uri template function:</span></span>

```json
"resources": [
  {
    "name": "shared",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "properties": {
      "mode": "Incremental",
      "templateLink": {
        "uri": "[uri(parameters('_artifactsLocation'), concat('nested/vnet.json', parameters('_artifactsLocationSasToken')))]",
        "contentVersion": "1.0.0.0"
      }
    }
  }
]
```

<span data-ttu-id="9831c-183">By using this approach, the default value for the `_artifactsLocation` parameter is used.</span><span class="sxs-lookup"><span data-stu-id="9831c-183">By using this approach, the default value for the `_artifactsLocation` parameter is used.</span></span> <span data-ttu-id="9831c-184">If the linked templates need to be retrieved from a different location, the parameter input can be used at deployment time to override the default value—no change to the template itself is needed.</span><span class="sxs-lookup"><span data-stu-id="9831c-184">If the linked templates need to be retrieved from a different location, the parameter input can be used at deployment time to override the default value—no change to the template itself is needed.</span></span>

### <a name="use-artifactslocation-instead-of-hardcoding-links"></a><span data-ttu-id="9831c-185">Use _artifactsLocation instead of hardcoding links</span><span class="sxs-lookup"><span data-stu-id="9831c-185">Use _artifactsLocation instead of hardcoding links</span></span>

<span data-ttu-id="9831c-186">Besides being used for nested templates, the URL in the `_artifactsLocation` parameter is used as a base for all related artifacts of a deployment template.</span><span class="sxs-lookup"><span data-stu-id="9831c-186">Besides being used for nested templates, the URL in the `_artifactsLocation` parameter is used as a base for all related artifacts of a deployment template.</span></span> <span data-ttu-id="9831c-187">Some VM extensions include a link to a script stored outside the template.</span><span class="sxs-lookup"><span data-stu-id="9831c-187">Some VM extensions include a link to a script stored outside the template.</span></span> <span data-ttu-id="9831c-188">For these extensions, you should not hardcode the links.</span><span class="sxs-lookup"><span data-stu-id="9831c-188">For these extensions, you should not hardcode the links.</span></span> <span data-ttu-id="9831c-189">For example, the Custom Script and PowerShell DSC extensions may link to an external script on GitHub as shown:</span><span class="sxs-lookup"><span data-stu-id="9831c-189">For example, the Custom Script and PowerShell DSC extensions may link to an external script on GitHub as shown:</span></span> 

```json
"properties": {
  "publisher": "Microsoft.Compute",
  "type": "CustomScriptExtension",
  "typeHandlerVersion": "1.9",
  "autoUpgradeMinorVersion": true,
  "settings": {
    "fileUris": [
      "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
    ]
  }
}
```

<span data-ttu-id="9831c-190">Hardcoding the links to the script potentially prevents the template from deploying successfully to another location.</span><span class="sxs-lookup"><span data-stu-id="9831c-190">Hardcoding the links to the script potentially prevents the template from deploying successfully to another location.</span></span> <span data-ttu-id="9831c-191">During configuration of the VM resource, the VM agent running inside the VM initiates a download of all the scripts linked in the VM extension, and then stores the scripts on the VM's local disk.</span><span class="sxs-lookup"><span data-stu-id="9831c-191">During configuration of the VM resource, the VM agent running inside the VM initiates a download of all the scripts linked in the VM extension, and then stores the scripts on the VM's local disk.</span></span> <span data-ttu-id="9831c-192">This approach functions like the nested template links explained earlier in the "Use nested templates across regions" section.</span><span class="sxs-lookup"><span data-stu-id="9831c-192">This approach functions like the nested template links explained earlier in the "Use nested templates across regions" section.</span></span>

<span data-ttu-id="9831c-193">Resource Manager retrieves nested templates at runtime.</span><span class="sxs-lookup"><span data-stu-id="9831c-193">Resource Manager retrieves nested templates at runtime.</span></span> <span data-ttu-id="9831c-194">For VM extensions, the retrieval of any external artifacts is performed by the VM agent.</span><span class="sxs-lookup"><span data-stu-id="9831c-194">For VM extensions, the retrieval of any external artifacts is performed by the VM agent.</span></span> <span data-ttu-id="9831c-195">Besides the different initiator of the artifact retrieval, the solution in the template definition is the same.</span><span class="sxs-lookup"><span data-stu-id="9831c-195">Besides the different initiator of the artifact retrieval, the solution in the template definition is the same.</span></span> <span data-ttu-id="9831c-196">Use the _artifactsLocation parameter with a default value of the base path where all the artifacts are stored (including the VM extension scripts) and the `_artifactsLocationSasToken` parameter for the input for the sasToken.</span><span class="sxs-lookup"><span data-stu-id="9831c-196">Use the _artifactsLocation parameter with a default value of the base path where all the artifacts are stored (including the VM extension scripts) and the `_artifactsLocationSasToken` parameter for the input for the sasToken.</span></span>

```json
"parameters": {
  "_artifactsLocation": {
    "type": "string",
    "metadata": {
      "description": "The base URI where artifacts required by this template are located."
    },
    "defaultValue": "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/"
  },
  "_artifactsLocationSasToken": {
    "type": "securestring",
    "metadata": {
      "description": "The sasToken required to access _artifactsLocation."
    },
    "defaultValue": ""
  }
}
```

<span data-ttu-id="9831c-197">To construct the absolute URI of an artifact, the preferred method is to use the uri template function, instead of the concat template function.</span><span class="sxs-lookup"><span data-stu-id="9831c-197">To construct the absolute URI of an artifact, the preferred method is to use the uri template function, instead of the concat template function.</span></span> <span data-ttu-id="9831c-198">By replacing hardcoded links to the scripts in the VM extension with the uri template function, this functionality in the template is configured for cloud consistency.</span><span class="sxs-lookup"><span data-stu-id="9831c-198">By replacing hardcoded links to the scripts in the VM extension with the uri template function, this functionality in the template is configured for cloud consistency.</span></span>

```json
"properties": {
  "publisher": "Microsoft.Compute",
  "type": "CustomScriptExtension",
  "typeHandlerVersion": "1.9",
  "autoUpgradeMinorVersion": true,
  "settings": {
    "fileUris": [
      "[uri(parameters('_artifactsLocation'), concat('scripts/configure-music-app.ps1', parameters('_artifactsLocationSasToken')))]"
    ]
  }
}
```

<span data-ttu-id="9831c-199">With this approach, all deployment artifacts, including configuration scripts, can be stored in the same location with the template itself.</span><span class="sxs-lookup"><span data-stu-id="9831c-199">With this approach, all deployment artifacts, including configuration scripts, can be stored in the same location with the template itself.</span></span> <span data-ttu-id="9831c-200">To change the location of all the links, you only need to specify a different base URL for the _artifactsLocation parameters.</span><span class="sxs-lookup"><span data-stu-id="9831c-200">To change the location of all the links, you only need to specify a different base URL for the _artifactsLocation parameters.</span></span>

## <a name="factor-in-differing-regional-capabilities"></a><span data-ttu-id="9831c-201">Factor in differing regional capabilities</span><span class="sxs-lookup"><span data-stu-id="9831c-201">Factor in differing regional capabilities</span></span>

<span data-ttu-id="9831c-202">With the agile development and continuous flow of updates and new services introduced to Azure, [regions can differ](https://azure.microsoft.com/regions/services/) in availability of services or updates.</span><span class="sxs-lookup"><span data-stu-id="9831c-202">With the agile development and continuous flow of updates and new services introduced to Azure, [regions can differ](https://azure.microsoft.com/regions/services/) in availability of services or updates.</span></span> <span data-ttu-id="9831c-203">After rigorous internal testing, new services or updates to existing services are usually introduced to a small audience of customers participating in a validation program.</span><span class="sxs-lookup"><span data-stu-id="9831c-203">After rigorous internal testing, new services or updates to existing services are usually introduced to a small audience of customers participating in a validation program.</span></span> <span data-ttu-id="9831c-204">After successful customer validation, the services or updates are made available within a subset of Azure regions, then introduced to more regions, rolled out to the sovereign clouds, and potentially made available for Azure Stack customers as well.</span><span class="sxs-lookup"><span data-stu-id="9831c-204">After successful customer validation, the services or updates are made available within a subset of Azure regions, then introduced to more regions, rolled out to the sovereign clouds, and potentially made available for Azure Stack customers as well.</span></span>

<span data-ttu-id="9831c-205">Knowing that Azure regions and clouds may differ in their available services, you can make some proactive decisions about your templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-205">Knowing that Azure regions and clouds may differ in their available services, you can make some proactive decisions about your templates.</span></span> <span data-ttu-id="9831c-206">A good place to start is by examining the available resource providers for a cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-206">A good place to start is by examining the available resource providers for a cloud.</span></span> <span data-ttu-id="9831c-207">A resource provider tells you the set of resources and operations that are available for an Azure service.</span><span class="sxs-lookup"><span data-stu-id="9831c-207">A resource provider tells you the set of resources and operations that are available for an Azure service.</span></span>

<span data-ttu-id="9831c-208">A template deploys and configures resources.</span><span class="sxs-lookup"><span data-stu-id="9831c-208">A template deploys and configures resources.</span></span> <span data-ttu-id="9831c-209">A resource type is provided by a resource provider.</span><span class="sxs-lookup"><span data-stu-id="9831c-209">A resource type is provided by a resource provider.</span></span> <span data-ttu-id="9831c-210">For example, the compute resource provider (Microsoft.Compute), provides multiple resource types such as virtualMachines and availabilitySets.</span><span class="sxs-lookup"><span data-stu-id="9831c-210">For example, the compute resource provider (Microsoft.Compute), provides multiple resource types such as virtualMachines and availabilitySets.</span></span> <span data-ttu-id="9831c-211">Each resource provider provides an API to Azure Resource Manager defined by a common contract, enabling a consistent, unified authoring experience across all resource providers.</span><span class="sxs-lookup"><span data-stu-id="9831c-211">Each resource provider provides an API to Azure Resource Manager defined by a common contract, enabling a consistent, unified authoring experience across all resource providers.</span></span> <span data-ttu-id="9831c-212">However, a resource provider that is available in global Azure may not be available in a sovereign cloud or an Azure Stack region.</span><span class="sxs-lookup"><span data-stu-id="9831c-212">However, a resource provider that is available in global Azure may not be available in a sovereign cloud or an Azure Stack region.</span></span>

![Resource providers](./media/templates-cloud-consistency/resource-providers.png) 

<span data-ttu-id="9831c-214">To verify the resource providers that are available in a given cloud, run the following script in the Azure command line interface ([CLI](/cli/azure/install-azure-cli)):</span><span class="sxs-lookup"><span data-stu-id="9831c-214">To verify the resource providers that are available in a given cloud, run the following script in the Azure command line interface ([CLI](/cli/azure/install-azure-cli)):</span></span>

```azurecli-interactive
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="9831c-215">You can also use the following PowerShell cmdlet to see available resource providers:</span><span class="sxs-lookup"><span data-stu-id="9831c-215">You can also use the following PowerShell cmdlet to see available resource providers:</span></span>

```azurepowershell-interactive
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

### <a name="verify-the-version-of-all-resource-types"></a><span data-ttu-id="9831c-216">Verify the version of all resource types</span><span class="sxs-lookup"><span data-stu-id="9831c-216">Verify the version of all resource types</span></span>

<span data-ttu-id="9831c-217">A set of properties is common for all resource types, but each resource also has its own specific properties.</span><span class="sxs-lookup"><span data-stu-id="9831c-217">A set of properties is common for all resource types, but each resource also has its own specific properties.</span></span> <span data-ttu-id="9831c-218">New features and related properties are added to existing resource types at times through a new API version.</span><span class="sxs-lookup"><span data-stu-id="9831c-218">New features and related properties are added to existing resource types at times through a new API version.</span></span> <span data-ttu-id="9831c-219">A resource in a template has its own API version property - `apiVersion`.</span><span class="sxs-lookup"><span data-stu-id="9831c-219">A resource in a template has its own API version property - `apiVersion`.</span></span> <span data-ttu-id="9831c-220">This versioning ensures that an existing resource configuration in a template is not affected by changes on the platform.</span><span class="sxs-lookup"><span data-stu-id="9831c-220">This versioning ensures that an existing resource configuration in a template is not affected by changes on the platform.</span></span>

<span data-ttu-id="9831c-221">New API versions introduced to existing resource types in global Azure might not immediately be available in all regions, sovereign clouds, or Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-221">New API versions introduced to existing resource types in global Azure might not immediately be available in all regions, sovereign clouds, or Azure Stack.</span></span> <span data-ttu-id="9831c-222">To view a list of the available resource providers, resource types, and API versions for a cloud, you can use Resource Explorer in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9831c-222">To view a list of the available resource providers, resource types, and API versions for a cloud, you can use Resource Explorer in Azure portal.</span></span> <span data-ttu-id="9831c-223">Search for Resource Explorer in the All Services menu.</span><span class="sxs-lookup"><span data-stu-id="9831c-223">Search for Resource Explorer in the All Services menu.</span></span> <span data-ttu-id="9831c-224">Expand the Providers node in Resource Explorer to return all the available resource providers, their resource types, and API versions in that cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-224">Expand the Providers node in Resource Explorer to return all the available resource providers, their resource types, and API versions in that cloud.</span></span>

<span data-ttu-id="9831c-225">To list the available API version for all resource types in a given cloud in Azure CLI, run the following script:</span><span class="sxs-lookup"><span data-stu-id="9831c-225">To list the available API version for all resource types in a given cloud in Azure CLI, run the following script:</span></span>

```azurecli-interactive
az provider list --query "[].{namespace:namespace, resourceType:resourceType[]}"
```

<span data-ttu-id="9831c-226">You can also use the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9831c-226">You can also use the following PowerShell cmdlet:</span></span>

```azurepowershell-interactive
Get-AzureRmResourceProvider | select-object ProviderNamespace -ExpandProperty ResourceTypes | ft ProviderNamespace, ResourceTypeName, ApiVersions
```

### <a name="refer-to-resource-locations-with-a-parameter"></a><span data-ttu-id="9831c-227">Refer to resource locations with a parameter</span><span class="sxs-lookup"><span data-stu-id="9831c-227">Refer to resource locations with a parameter</span></span>

<span data-ttu-id="9831c-228">A template is always deployed into a resource group that resides in a region.</span><span class="sxs-lookup"><span data-stu-id="9831c-228">A template is always deployed into a resource group that resides in a region.</span></span> <span data-ttu-id="9831c-229">Besides the deployment itself, each resource in a template also has a location property that you use to specify the region to deploy in.</span><span class="sxs-lookup"><span data-stu-id="9831c-229">Besides the deployment itself, each resource in a template also has a location property that you use to specify the region to deploy in.</span></span> <span data-ttu-id="9831c-230">To develop your template for cloud consistency, you need a dynamic way to refer to resource locations, because each Azure Stack can contain unique location names.</span><span class="sxs-lookup"><span data-stu-id="9831c-230">To develop your template for cloud consistency, you need a dynamic way to refer to resource locations, because each Azure Stack can contain unique location names.</span></span> <span data-ttu-id="9831c-231">Usually resources are deployed in the same region as the resource group, but to support scenarios such as cross-region application availability, it can be useful to spread resources across regions.</span><span class="sxs-lookup"><span data-stu-id="9831c-231">Usually resources are deployed in the same region as the resource group, but to support scenarios such as cross-region application availability, it can be useful to spread resources across regions.</span></span>

<span data-ttu-id="9831c-232">Even though you could hardcode the region names when specifying the resource properties in a template, this approach doesn't guarantee that the template can be deployed to other Azure Stack environments, because the region name most likely doesn't exist there.</span><span class="sxs-lookup"><span data-stu-id="9831c-232">Even though you could hardcode the region names when specifying the resource properties in a template, this approach doesn't guarantee that the template can be deployed to other Azure Stack environments, because the region name most likely doesn't exist there.</span></span>

<span data-ttu-id="9831c-233">To accommodate different regions, add an input parameter location to the template with a default value.</span><span class="sxs-lookup"><span data-stu-id="9831c-233">To accommodate different regions, add an input parameter location to the template with a default value.</span></span> <span data-ttu-id="9831c-234">The default value will be used if no value is specified during deployment.</span><span class="sxs-lookup"><span data-stu-id="9831c-234">The default value will be used if no value is specified during deployment.</span></span> 

<span data-ttu-id="9831c-235">The template function `[resourceGroup()]` returns an object that contains the following key/value pairs:</span><span class="sxs-lookup"><span data-stu-id="9831c-235">The template function `[resourceGroup()]` returns an object that contains the following key/value pairs:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

<span data-ttu-id="9831c-236">By referencing the location key of the object in the defaultValue of the input parameter, Azure Resource Manager will, at runtime, replace the `[resourceGroup().location]` template function with the name of the location of the resource group the template is deployed to.</span><span class="sxs-lookup"><span data-stu-id="9831c-236">By referencing the location key of the object in the defaultValue of the input parameter, Azure Resource Manager will, at runtime, replace the `[resourceGroup().location]` template function with the name of the location of the resource group the template is deployed to.</span></span>

```json
"parameters": {
  "location": {
    "type": "string",
    "metadata": {
      "description": "Location the resources will be deployed to."
    },
    "defaultValue": "[resourceGroup().location]"
  }
},
"resources": [
  {
    "name": "storageaccount1",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2015-06-15",
    "location": "[parameters('location')]",
    ...
```

<span data-ttu-id="9831c-237">With this template function, you can deploy your template to any cloud without even knowing the region names in advance.</span><span class="sxs-lookup"><span data-stu-id="9831c-237">With this template function, you can deploy your template to any cloud without even knowing the region names in advance.</span></span> <span data-ttu-id="9831c-238">In addition, a location for a specific resource in the template can differ from the resource group location.</span><span class="sxs-lookup"><span data-stu-id="9831c-238">In addition, a location for a specific resource in the template can differ from the resource group location.</span></span> <span data-ttu-id="9831c-239">In this case, you can configure it by using additional input parameters for that specific resource, while the other resources in the same template still use the initial location input parameter.</span><span class="sxs-lookup"><span data-stu-id="9831c-239">In this case, you can configure it by using additional input parameters for that specific resource, while the other resources in the same template still use the initial location input parameter.</span></span>

### <a name="track-versions-using-api-profiles"></a><span data-ttu-id="9831c-240">Track versions using API profiles</span><span class="sxs-lookup"><span data-stu-id="9831c-240">Track versions using API profiles</span></span>

<span data-ttu-id="9831c-241">It can be very challenging to keep track of all the available resource providers and related API versions that are present in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-241">It can be very challenging to keep track of all the available resource providers and related API versions that are present in Azure Stack.</span></span> <span data-ttu-id="9831c-242">For example, at the time of writing, the latest API version for **Microsoft.Compute/availabilitySets** in Azure is `2018-04-01`, while the available API version common to Azure and Azure Stack is `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="9831c-242">For example, at the time of writing, the latest API version for **Microsoft.Compute/availabilitySets** in Azure is `2018-04-01`, while the available API version common to Azure and Azure Stack is `2016-03-30`.</span></span> <span data-ttu-id="9831c-243">The common API version for **Microsoft.Storage/storageAccounts** shared among all Azure and Azure Stack locations is `2016-01-01`, while the latest API version in Azure is `2018-02-01`.</span><span class="sxs-lookup"><span data-stu-id="9831c-243">The common API version for **Microsoft.Storage/storageAccounts** shared among all Azure and Azure Stack locations is `2016-01-01`, while the latest API version in Azure is `2018-02-01`.</span></span>

<span data-ttu-id="9831c-244">For this reason, Resource Manager introduced the concept of API profiles to templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-244">For this reason, Resource Manager introduced the concept of API profiles to templates.</span></span> <span data-ttu-id="9831c-245">Without API profiles, each resource in a template is configured with an `apiVersion` element that describes the API version for that specific resource.</span><span class="sxs-lookup"><span data-stu-id="9831c-245">Without API profiles, each resource in a template is configured with an `apiVersion` element that describes the API version for that specific resource.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location the resources will be deployed to."
            },
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {},
    "resources": [
        {
            "name": "mystorageaccount",
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2016-01-01",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "Standard_LRS"
            }
        },
        {
            "name": "myavailabilityset",
            "type": "Microsoft.Compute/availabilitySets",
            "apiVersion": "2016-03-30",
            "location": "[parameters('location')]",
            "properties": {
                "platformFaultDomainCount": 2,
                "platformUpdateDomainCount": 2
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="9831c-246">An API profile version acts as an alias for a single API version per resource type common to Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-246">An API profile version acts as an alias for a single API version per resource type common to Azure and Azure Stack.</span></span> <span data-ttu-id="9831c-247">Instead of specifying an API version for each resource in a template, you specify only the API profile version in a new root element called `apiProfile` and omit the `apiVersion` element for the individual resources.</span><span class="sxs-lookup"><span data-stu-id="9831c-247">Instead of specifying an API version for each resource in a template, you specify only the API profile version in a new root element called `apiProfile` and omit the `apiVersion` element for the individual resources.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "apiProfile": "2018–03-01-hybrid",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location the resources will be deployed to."
            },
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {},
    "resources": [
        {
            "name": "mystorageaccount",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "Standard_LRS"
            }
        },
        {
            "name": "myavailabilityset",
            "type": "Microsoft.Compute/availabilitySets",
            "location": "[parameters('location')]",
            "properties": {
                "platformFaultDomainCount": 2,
                "platformUpdateDomainCount": 2
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="9831c-248">The API profile ensures that the API versions are available across locations, so you do not have to manually verify the apiVersions that are available in a specific location.</span><span class="sxs-lookup"><span data-stu-id="9831c-248">The API profile ensures that the API versions are available across locations, so you do not have to manually verify the apiVersions that are available in a specific location.</span></span> <span data-ttu-id="9831c-249">To ensure the API versions referenced by your API profile are present in an Azure Stack environment, the Azure Stack operators must keep the solution up-to-date based on the policy for support.</span><span class="sxs-lookup"><span data-stu-id="9831c-249">To ensure the API versions referenced by your API profile are present in an Azure Stack environment, the Azure Stack operators must keep the solution up-to-date based on the policy for support.</span></span> <span data-ttu-id="9831c-250">If a system is more than six months out of date, it is considered out of compliance, and the environment must be updated.</span><span class="sxs-lookup"><span data-stu-id="9831c-250">If a system is more than six months out of date, it is considered out of compliance, and the environment must be updated.</span></span>

<span data-ttu-id="9831c-251">The API profile isn't a required element in a template.</span><span class="sxs-lookup"><span data-stu-id="9831c-251">The API profile isn't a required element in a template.</span></span> <span data-ttu-id="9831c-252">Even if you add the element, it will only be used for resources for which no `apiVersion` is specified.</span><span class="sxs-lookup"><span data-stu-id="9831c-252">Even if you add the element, it will only be used for resources for which no `apiVersion` is specified.</span></span> <span data-ttu-id="9831c-253">This element allows for gradual changes but doesn't require any changes to existing templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-253">This element allows for gradual changes but doesn't require any changes to existing templates.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "apiProfile": "2018–03-01-hybrid",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location the resources will be deployed to."
            },
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {},
    "resources": [
        {
            "name": "mystorageaccount",
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2016-01-01",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "Standard_LRS"
            }
        },
        {
            "name": "myavailabilityset",
            "type": "Microsoft.Compute/availabilitySets",
            "location": "[parameters('location')]",
            "properties": {
                "platformFaultDomainCount": 2,
                "platformUpdateDomainCount": 2
            }
        }
    ],
    "outputs": {}
}
```

## <a name="check-endpoint-references"></a><span data-ttu-id="9831c-254">Check endpoint references</span><span class="sxs-lookup"><span data-stu-id="9831c-254">Check endpoint references</span></span>

<span data-ttu-id="9831c-255">Resources can have references to other services on the platform.</span><span class="sxs-lookup"><span data-stu-id="9831c-255">Resources can have references to other services on the platform.</span></span> <span data-ttu-id="9831c-256">For example, a public IP can have a public DNS name assigned to it.</span><span class="sxs-lookup"><span data-stu-id="9831c-256">For example, a public IP can have a public DNS name assigned to it.</span></span> <span data-ttu-id="9831c-257">The public cloud, the sovereign clouds, and Azure Stack solutions have their own distinct endpoint namespaces.</span><span class="sxs-lookup"><span data-stu-id="9831c-257">The public cloud, the sovereign clouds, and Azure Stack solutions have their own distinct endpoint namespaces.</span></span> <span data-ttu-id="9831c-258">In most cases, a resource requires only a prefix as input in the template.</span><span class="sxs-lookup"><span data-stu-id="9831c-258">In most cases, a resource requires only a prefix as input in the template.</span></span> <span data-ttu-id="9831c-259">During runtime, Azure Resource Manager appends the endpoint value to it.</span><span class="sxs-lookup"><span data-stu-id="9831c-259">During runtime, Azure Resource Manager appends the endpoint value to it.</span></span> <span data-ttu-id="9831c-260">Some endpoint values need to be explicitly specified in the template.</span><span class="sxs-lookup"><span data-stu-id="9831c-260">Some endpoint values need to be explicitly specified in the template.</span></span> 

> [!NOTE]
> <span data-ttu-id="9831c-261">To develop templates for cloud consistency, don't hardcode endpoint namespaces.</span><span class="sxs-lookup"><span data-stu-id="9831c-261">To develop templates for cloud consistency, don't hardcode endpoint namespaces.</span></span>

<span data-ttu-id="9831c-262">The following two examples are common endpoint namespaces that need to be explicitly specified when creating a resource:</span><span class="sxs-lookup"><span data-stu-id="9831c-262">The following two examples are common endpoint namespaces that need to be explicitly specified when creating a resource:</span></span>

* <span data-ttu-id="9831c-263">Storage accounts (blob, queue, table and file)</span><span class="sxs-lookup"><span data-stu-id="9831c-263">Storage accounts (blob, queue, table and file)</span></span>
* <span data-ttu-id="9831c-264">Connection strings for databases and Redis Cache</span><span class="sxs-lookup"><span data-stu-id="9831c-264">Connection strings for databases and Redis Cache</span></span>

<span data-ttu-id="9831c-265">Endpoint namespaces can also be used in the output of a template as information for the user when the deployment completes.</span><span class="sxs-lookup"><span data-stu-id="9831c-265">Endpoint namespaces can also be used in the output of a template as information for the user when the deployment completes.</span></span> <span data-ttu-id="9831c-266">The following are common examples:</span><span class="sxs-lookup"><span data-stu-id="9831c-266">The following are common examples:</span></span>

* <span data-ttu-id="9831c-267">Storage accounts (blob, queue, table and file)</span><span class="sxs-lookup"><span data-stu-id="9831c-267">Storage accounts (blob, queue, table and file)</span></span>
* <span data-ttu-id="9831c-268">Connection strings (MySql, SQLServer, SQLAzure, Custom, NotificationHub, ServiceBus, EventHub, ApiHub, DocDb, RedisCache, PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="9831c-268">Connection strings (MySql, SQLServer, SQLAzure, Custom, NotificationHub, ServiceBus, EventHub, ApiHub, DocDb, RedisCache, PostgreSQL)</span></span>
* <span data-ttu-id="9831c-269">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="9831c-269">Traffic Manager</span></span>
* <span data-ttu-id="9831c-270">domainNameLabel of a public IP address</span><span class="sxs-lookup"><span data-stu-id="9831c-270">domainNameLabel of a public IP address</span></span>
* <span data-ttu-id="9831c-271">Cloud services</span><span class="sxs-lookup"><span data-stu-id="9831c-271">Cloud services</span></span>

<span data-ttu-id="9831c-272">In general, avoid hardcoded endpoints in a template.</span><span class="sxs-lookup"><span data-stu-id="9831c-272">In general, avoid hardcoded endpoints in a template.</span></span> <span data-ttu-id="9831c-273">The best practice is to use the reference template function to retrieve the endpoints dynamically.</span><span class="sxs-lookup"><span data-stu-id="9831c-273">The best practice is to use the reference template function to retrieve the endpoints dynamically.</span></span> <span data-ttu-id="9831c-274">For example, the endpoint most commonly hardcoded is the endpoint namespace for storage accounts.</span><span class="sxs-lookup"><span data-stu-id="9831c-274">For example, the endpoint most commonly hardcoded is the endpoint namespace for storage accounts.</span></span> <span data-ttu-id="9831c-275">Each storage account has a unique FQDN that is constructed by concatenating the name of the storage account with the endpoint namespace.</span><span class="sxs-lookup"><span data-stu-id="9831c-275">Each storage account has a unique FQDN that is constructed by concatenating the name of the storage account with the endpoint namespace.</span></span> <span data-ttu-id="9831c-276">A blob storage account named mystorageaccount1 results in different FQDNs depending on the cloud:</span><span class="sxs-lookup"><span data-stu-id="9831c-276">A blob storage account named mystorageaccount1 results in different FQDNs depending on the cloud:</span></span>

* <span data-ttu-id="9831c-277">**mystorageaccount1.blob.core.windows.net** when created on the global Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-277">**mystorageaccount1.blob.core.windows.net** when created on the global Azure cloud.</span></span>
* <span data-ttu-id="9831c-278">**mystorageaccount1.blob.core.chinacloudapi.cn** when created in the Azure China cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-278">**mystorageaccount1.blob.core.chinacloudapi.cn** when created in the Azure China cloud.</span></span>

<span data-ttu-id="9831c-279">The following reference template function retrieves the endpoint namespace from the storage resource provider:</span><span class="sxs-lookup"><span data-stu-id="9831c-279">The following reference template function retrieves the endpoint namespace from the storage resource provider:</span></span>

```json
"diskUri":"[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, 'container/myosdisk.vhd')]"
```

<span data-ttu-id="9831c-280">By replacing the hardcoded value of the storage account endpoint with the `reference` template function, you can use the same template to deploy to different environments successfully without making any changes to the endpoint reference.</span><span class="sxs-lookup"><span data-stu-id="9831c-280">By replacing the hardcoded value of the storage account endpoint with the `reference` template function, you can use the same template to deploy to different environments successfully without making any changes to the endpoint reference.</span></span>

### <a name="refer-to-existing-resources-by-unique-id"></a><span data-ttu-id="9831c-281">Refer to existing resources by unique ID</span><span class="sxs-lookup"><span data-stu-id="9831c-281">Refer to existing resources by unique ID</span></span>

<span data-ttu-id="9831c-282">You can also refer to an existing resource from the same or another resource group, and within the same subscription or another subscription, within the same tenant in the same cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-282">You can also refer to an existing resource from the same or another resource group, and within the same subscription or another subscription, within the same tenant in the same cloud.</span></span> <span data-ttu-id="9831c-283">To retrieve the resource properties, you must use the unique identifier for the resource itself.</span><span class="sxs-lookup"><span data-stu-id="9831c-283">To retrieve the resource properties, you must use the unique identifier for the resource itself.</span></span> <span data-ttu-id="9831c-284">The `resourceId` template function retrieves the unique ID of a resource such as SQL Server as the following code shows:</span><span class="sxs-lookup"><span data-stu-id="9831c-284">The `resourceId` template function retrieves the unique ID of a resource such as SQL Server as the following code shows:</span></span> 

```json
"outputs": {
  "resourceId":{
    "type": "string",
    "value": "[resourceId('otherResourceGroup', 'Microsoft.Sql/servers', parameters('serverName'))]"
  }
}
```

<span data-ttu-id="9831c-285">You can then use the `resourceId` function inside the `reference` template function to retrieve the properties of a database.</span><span class="sxs-lookup"><span data-stu-id="9831c-285">You can then use the `resourceId` function inside the `reference` template function to retrieve the properties of a database.</span></span> <span data-ttu-id="9831c-286">The return object contains the `fullyQualifiedDomainName` property that holds the full endpoint value.</span><span class="sxs-lookup"><span data-stu-id="9831c-286">The return object contains the `fullyQualifiedDomainName` property that holds the full endpoint value.</span></span> <span data-ttu-id="9831c-287">This value is retrieved at runtime and provides the cloud environment-specific endpoint namespace.</span><span class="sxs-lookup"><span data-stu-id="9831c-287">This value is retrieved at runtime and provides the cloud environment-specific endpoint namespace.</span></span> <span data-ttu-id="9831c-288">To define the connection string without hardcoding the endpoint namespace, you can refer to the property of the return object directly in the connection string as shown:</span><span class="sxs-lookup"><span data-stu-id="9831c-288">To define the connection string without hardcoding the endpoint namespace, you can refer to the property of the return object directly in the connection string as shown:</span></span>

```json
"[concat('Server=tcp:', reference(resourceId('sql', 'Microsoft.Sql/servers', parameters('test')), '2015-05-01-preview').fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('database'),';User ID=', parameters('username'), ';Password=', parameters('pass'), ';Encrypt=True;')]"
```

## <a name="consider-resource-properties"></a><span data-ttu-id="9831c-289">Consider resource properties</span><span class="sxs-lookup"><span data-stu-id="9831c-289">Consider resource properties</span></span>

<span data-ttu-id="9831c-290">Specific resources within Azure Stack environments have unique properties you must consider in your template.</span><span class="sxs-lookup"><span data-stu-id="9831c-290">Specific resources within Azure Stack environments have unique properties you must consider in your template.</span></span>

### <a name="ensure-vm-images-are-available"></a><span data-ttu-id="9831c-291">Ensure VM images are available</span><span class="sxs-lookup"><span data-stu-id="9831c-291">Ensure VM images are available</span></span>

<span data-ttu-id="9831c-292">Azure provides a rich selection of VM images.</span><span class="sxs-lookup"><span data-stu-id="9831c-292">Azure provides a rich selection of VM images.</span></span> <span data-ttu-id="9831c-293">These images are created and prepared for deployment by Microsoft and partners.</span><span class="sxs-lookup"><span data-stu-id="9831c-293">These images are created and prepared for deployment by Microsoft and partners.</span></span> <span data-ttu-id="9831c-294">The images form the foundation for VMs on the platform.</span><span class="sxs-lookup"><span data-stu-id="9831c-294">The images form the foundation for VMs on the platform.</span></span> <span data-ttu-id="9831c-295">However, a cloud-consistent template should refer to available parameters only — in particular, the publisher, offer, and SKU of the VM images available to the global Azure, Azure sovereign clouds, or an Azure Stack solution.</span><span class="sxs-lookup"><span data-stu-id="9831c-295">However, a cloud-consistent template should refer to available parameters only — in particular, the publisher, offer, and SKU of the VM images available to the global Azure, Azure sovereign clouds, or an Azure Stack solution.</span></span>

<span data-ttu-id="9831c-296">To retrieve a list of the available VM images in a location, run the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="9831c-296">To retrieve a list of the available VM images in a location, run the following Azure CLI command:</span></span>

```azurecli-interactive
az vm image list -all
```

<span data-ttu-id="9831c-297">You can retrieve the same list with the Azure PowerShell cmdlet [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) and specify the location you want with the `-Location` parameter.</span><span class="sxs-lookup"><span data-stu-id="9831c-297">You can retrieve the same list with the Azure PowerShell cmdlet [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) and specify the location you want with the `-Location` parameter.</span></span> <span data-ttu-id="9831c-298">For example:</span><span class="sxs-lookup"><span data-stu-id="9831c-298">For example:</span></span>

```azurepowershell-interactive
Get-AzureRmVMImagePublisher -Location "West Europe" | Get-AzureRmVMImageOffer | Get-AzureRmVMImageSku | Get-AzureRMVMImage
```

<span data-ttu-id="9831c-299">This command takes a couple of minutes to return all the available images in the West Europe region of the global Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-299">This command takes a couple of minutes to return all the available images in the West Europe region of the global Azure cloud.</span></span>

<span data-ttu-id="9831c-300">If you made these VM images available to Azure Stack, all the available storage would be consumed.</span><span class="sxs-lookup"><span data-stu-id="9831c-300">If you made these VM images available to Azure Stack, all the available storage would be consumed.</span></span> <span data-ttu-id="9831c-301">To accommodate even the smallest scale unit, Azure Stack allows you to select the images you want to add to an environment.</span><span class="sxs-lookup"><span data-stu-id="9831c-301">To accommodate even the smallest scale unit, Azure Stack allows you to select the images you want to add to an environment.</span></span>

<span data-ttu-id="9831c-302">The following code sample shows a consistent approach to refer to the publisher, offer, and SKU parameters in your Azure Resource Manager templates:</span><span class="sxs-lookup"><span data-stu-id="9831c-302">The following code sample shows a consistent approach to refer to the publisher, offer, and SKU parameters in your Azure Resource Manager templates:</span></span>

```json
"storageProfile": {
    "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2016-Datacenter",
    "version": "latest"
    }
}
```

### <a name="check-local-vm-sizes"></a><span data-ttu-id="9831c-303">Check local VM sizes</span><span class="sxs-lookup"><span data-stu-id="9831c-303">Check local VM sizes</span></span>

<span data-ttu-id="9831c-304">To develop your template for cloud consistency, you need to make sure the VM size you want is available in all target environments.</span><span class="sxs-lookup"><span data-stu-id="9831c-304">To develop your template for cloud consistency, you need to make sure the VM size you want is available in all target environments.</span></span> <span data-ttu-id="9831c-305">VM sizes are a grouping of performance characteristics and capabilities.</span><span class="sxs-lookup"><span data-stu-id="9831c-305">VM sizes are a grouping of performance characteristics and capabilities.</span></span> <span data-ttu-id="9831c-306">Some VM sizes depend on the hardware that the VM runs on.</span><span class="sxs-lookup"><span data-stu-id="9831c-306">Some VM sizes depend on the hardware that the VM runs on.</span></span> <span data-ttu-id="9831c-307">For example, if you want to deploy a GPU-optimized VM, the hardware that runs the hypervisor needs to have the hardware GPUs.</span><span class="sxs-lookup"><span data-stu-id="9831c-307">For example, if you want to deploy a GPU-optimized VM, the hardware that runs the hypervisor needs to have the hardware GPUs.</span></span>

<span data-ttu-id="9831c-308">When Microsoft introduces a new size of VM that has certain hardware dependencies, the VM size is usually made available first in a small subset of regions in the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="9831c-308">When Microsoft introduces a new size of VM that has certain hardware dependencies, the VM size is usually made available first in a small subset of regions in the Azure cloud.</span></span> <span data-ttu-id="9831c-309">Later, it is made available to other regions and clouds.</span><span class="sxs-lookup"><span data-stu-id="9831c-309">Later, it is made available to other regions and clouds.</span></span> <span data-ttu-id="9831c-310">To make sure the VM size exists in each cloud you deploy to, you can retrieve the available sizes with the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="9831c-310">To make sure the VM size exists in each cloud you deploy to, you can retrieve the available sizes with the following Azure CLI command:</span></span>

```azurecli-interactive
az vm list-sizes --location "West Europe"
```

<span data-ttu-id="9831c-311">For Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="9831c-311">For Azure PowerShell, use:</span></span>

```azurepowershell-interactive
Get-AzureRmVMSize -Location "West Europe"
```

<span data-ttu-id="9831c-312">For a full list of available services, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?cdn=disable).</span><span class="sxs-lookup"><span data-stu-id="9831c-312">For a full list of available services, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?cdn=disable).</span></span>

### <a name="check-use-of-azure-managed-disks-in-azure-stack"></a><span data-ttu-id="9831c-313">Check use of Azure Managed Disks in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9831c-313">Check use of Azure Managed Disks in Azure Stack</span></span>

<span data-ttu-id="9831c-314">Managed disks handle the storage for an Azure tenant.</span><span class="sxs-lookup"><span data-stu-id="9831c-314">Managed disks handle the storage for an Azure tenant.</span></span> <span data-ttu-id="9831c-315">Instead of explicitly creating a storage account and specifying the URI for a virtual hard disk (VHD), you can use managed disks to implicitly perform these actions when you deploy a VM.</span><span class="sxs-lookup"><span data-stu-id="9831c-315">Instead of explicitly creating a storage account and specifying the URI for a virtual hard disk (VHD), you can use managed disks to implicitly perform these actions when you deploy a VM.</span></span> <span data-ttu-id="9831c-316">Managed disks enhance availability by placing all the disks from VMs in the same availability set into different storage units.</span><span class="sxs-lookup"><span data-stu-id="9831c-316">Managed disks enhance availability by placing all the disks from VMs in the same availability set into different storage units.</span></span> <span data-ttu-id="9831c-317">Additionally, existing VHDs can be converted from Standard to Premium storage with significantly less downtime.</span><span class="sxs-lookup"><span data-stu-id="9831c-317">Additionally, existing VHDs can be converted from Standard to Premium storage with significantly less downtime.</span></span>

<span data-ttu-id="9831c-318">Although managed disks are on the roadmap for Azure Stack, they are currently not supported.</span><span class="sxs-lookup"><span data-stu-id="9831c-318">Although managed disks are on the roadmap for Azure Stack, they are currently not supported.</span></span> <span data-ttu-id="9831c-319">Until they are, you can develop cloud-consistent templates for Azure Stack by explicitly specifying VHDs using the `vhd` element in the template for the VM resource as shown:</span><span class="sxs-lookup"><span data-stu-id="9831c-319">Until they are, you can develop cloud-consistent templates for Azure Stack by explicitly specifying VHDs using the `vhd` element in the template for the VM resource as shown:</span></span>

```json
"storageProfile": {
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "[parameters('windowsOSVersion')]",
    "version": "latest"
  },
  "osDisk": {
    "name": "osdisk",
    "vhd": {
      "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
    },
    "caching": "ReadWrite",
    "createOption": "FromImage"
  }
}
```

<span data-ttu-id="9831c-320">In contrast, to specify a managed disk configuration in a template, remove the `vhd` element from the disk configuration.</span><span class="sxs-lookup"><span data-stu-id="9831c-320">In contrast, to specify a managed disk configuration in a template, remove the `vhd` element from the disk configuration.</span></span>

```json
"storageProfile": {
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "[parameters('windowsOSVersion')]",
    "version": "latest"
  },
  "osDisk": {
    "caching": "ReadWrite",
    "createOption": "FromImage"
  }
}
```

<span data-ttu-id="9831c-321">The same changes also apply [data disks](../virtual-machines/windows/using-managed-disks-template-deployments.md).</span><span class="sxs-lookup"><span data-stu-id="9831c-321">The same changes also apply [data disks](../virtual-machines/windows/using-managed-disks-template-deployments.md).</span></span>

### <a name="verify-that-vm-extensions-are-available-in-azure-stack"></a><span data-ttu-id="9831c-322">Verify that VM extensions are available in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9831c-322">Verify that VM extensions are available in Azure Stack</span></span>

<span data-ttu-id="9831c-323">Another consideration for cloud consistency is the use of [virtual machine extensions](../virtual-machines/windows/extensions-features.md) to configure the resources inside a VM.</span><span class="sxs-lookup"><span data-stu-id="9831c-323">Another consideration for cloud consistency is the use of [virtual machine extensions](../virtual-machines/windows/extensions-features.md) to configure the resources inside a VM.</span></span> <span data-ttu-id="9831c-324">Not all VM extensions are available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9831c-324">Not all VM extensions are available in Azure Stack.</span></span> <span data-ttu-id="9831c-325">A template can specify the resources dedicated to the VM extension, creating dependencies and conditions within the template.</span><span class="sxs-lookup"><span data-stu-id="9831c-325">A template can specify the resources dedicated to the VM extension, creating dependencies and conditions within the template.</span></span>

<span data-ttu-id="9831c-326">For example, if you want to configure a VM running Microsoft SQL Server, the VM extension can configure SQL Server as part the template deployment.</span><span class="sxs-lookup"><span data-stu-id="9831c-326">For example, if you want to configure a VM running Microsoft SQL Server, the VM extension can configure SQL Server as part the template deployment.</span></span> <span data-ttu-id="9831c-327">Consider what happens if the deployment template also contains an application server configured to create a database on the VM running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9831c-327">Consider what happens if the deployment template also contains an application server configured to create a database on the VM running SQL Server.</span></span> <span data-ttu-id="9831c-328">Besides also using a VM extension for the application servers, you can configure the dependency of the application server on the successful return of the SQL Server VM extension resource.</span><span class="sxs-lookup"><span data-stu-id="9831c-328">Besides also using a VM extension for the application servers, you can configure the dependency of the application server on the successful return of the SQL Server VM extension resource.</span></span> <span data-ttu-id="9831c-329">This approach ensures the VM running SQL Server is configured and available when the application server is instructed to create the database.</span><span class="sxs-lookup"><span data-stu-id="9831c-329">This approach ensures the VM running SQL Server is configured and available when the application server is instructed to create the database.</span></span>

<span data-ttu-id="9831c-330">The declarative approach of the template allows you to define the end state of the resources and their inter-dependencies, while the platform takes care of the logic required for the dependencies.</span><span class="sxs-lookup"><span data-stu-id="9831c-330">The declarative approach of the template allows you to define the end state of the resources and their inter-dependencies, while the platform takes care of the logic required for the dependencies.</span></span>

#### <a name="check-that-vm-extensions-are-available"></a><span data-ttu-id="9831c-331">Check that VM extensions are available</span><span class="sxs-lookup"><span data-stu-id="9831c-331">Check that VM extensions are available</span></span>

<span data-ttu-id="9831c-332">Many types of VM extensions exist.</span><span class="sxs-lookup"><span data-stu-id="9831c-332">Many types of VM extensions exist.</span></span> <span data-ttu-id="9831c-333">When developing template for cloud consistency, make sure to use only the extensions that are available in all the regions the template targets.</span><span class="sxs-lookup"><span data-stu-id="9831c-333">When developing template for cloud consistency, make sure to use only the extensions that are available in all the regions the template targets.</span></span>

<span data-ttu-id="9831c-334">To retrieve a list of the VM extensions that are available for a specific region (in this example, `myLocation`), run the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="9831c-334">To retrieve a list of the VM extensions that are available for a specific region (in this example, `myLocation`), run the following Azure CLI command:</span></span>

```azurecli-interactive
az vm extension image list --location myLocation
```

<span data-ttu-id="9831c-335">You can also execute the Azure PowerShell [Get-AzureRmVmImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) cmdlet and use `-Location` to specify the location of the virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="9831c-335">You can also execute the Azure PowerShell [Get-AzureRmVmImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) cmdlet and use `-Location` to specify the location of the virtual machine image.</span></span> <span data-ttu-id="9831c-336">For example:</span><span class="sxs-lookup"><span data-stu-id="9831c-336">For example:</span></span>

```azurepowershell-interactive
Get-AzureRmVmImagePublisher -Location myLocation | Get-AzureRmVMExtensionImageType | Get-AzureRmVMExtensionImage | Select Type, Version
```

#### <a name="ensure-that-versions-are-available"></a><span data-ttu-id="9831c-337">Ensure that versions are available</span><span class="sxs-lookup"><span data-stu-id="9831c-337">Ensure that versions are available</span></span>

<span data-ttu-id="9831c-338">Since VM extensions are first-party Resource Manager resources, they have their own API versions.</span><span class="sxs-lookup"><span data-stu-id="9831c-338">Since VM extensions are first-party Resource Manager resources, they have their own API versions.</span></span> <span data-ttu-id="9831c-339">As the following code shows, the VM extension type is a nested resource in the Microsoft.Compute resource provider.</span><span class="sxs-lookup"><span data-stu-id="9831c-339">As the following code shows, the VM extension type is a nested resource in the Microsoft.Compute resource provider.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "myExtension",
    "location": "[parameters('location')]",
    ...
```

<span data-ttu-id="9831c-340">The API version of the VM extension resource must be present in all the locations you plan to target with your template.</span><span class="sxs-lookup"><span data-stu-id="9831c-340">The API version of the VM extension resource must be present in all the locations you plan to target with your template.</span></span> <span data-ttu-id="9831c-341">The location dependency works like the resource provider API version availability discussed earlier in the "Verify the version of all resource types" section.</span><span class="sxs-lookup"><span data-stu-id="9831c-341">The location dependency works like the resource provider API version availability discussed earlier in the "Verify the version of all resource types" section.</span></span>

<span data-ttu-id="9831c-342">To retrieve a list of the available API versions for the VM extension resource, use the [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider) cmdlet with the **Microsoft.Compute** resource provider as shown:</span><span class="sxs-lookup"><span data-stu-id="9831c-342">To retrieve a list of the available API versions for the VM extension resource, use the [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider) cmdlet with the **Microsoft.Compute** resource provider as shown:</span></span>

```azurepowershell-interactive
Get-AzureRmResourceProvider -ProviderNamespace "Microsoft.Compute" | Select-Object -ExpandProperty ResourceTypes | Select ResourceTypeName, Locations, ApiVersions | where {$_.ResourceTypeName -eq "virtualMachines/extensions"}
```

<span data-ttu-id="9831c-343">You can also use VM extensions in virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="9831c-343">You can also use VM extensions in virtual machine scale sets.</span></span> <span data-ttu-id="9831c-344">The same location conditions apply.</span><span class="sxs-lookup"><span data-stu-id="9831c-344">The same location conditions apply.</span></span> <span data-ttu-id="9831c-345">To develop your template for cloud consistency, make sure the API versions are available in all the locations you plan on deploying to.</span><span class="sxs-lookup"><span data-stu-id="9831c-345">To develop your template for cloud consistency, make sure the API versions are available in all the locations you plan on deploying to.</span></span> <span data-ttu-id="9831c-346">To retrieve the API versions of the VM extension resource for scale sets, use the same cmdlet as before, but specify the virtual machine scale sets resource type as shown:</span><span class="sxs-lookup"><span data-stu-id="9831c-346">To retrieve the API versions of the VM extension resource for scale sets, use the same cmdlet as before, but specify the virtual machine scale sets resource type as shown:</span></span>

```azurepowershell-interactive
Get-AzureRmResourceProvider -ProviderNamespace "Microsoft.Compute" | Select-Object -ExpandProperty ResourceTypes | Select ResourceTypeName, Locations, ApiVersions | where {$_.ResourceTypeName -eq "virtualMachineScaleSets/extensions"}
```

<span data-ttu-id="9831c-347">Each specific extension is also versioned.</span><span class="sxs-lookup"><span data-stu-id="9831c-347">Each specific extension is also versioned.</span></span> <span data-ttu-id="9831c-348">This version is shown in the `typeHandlerVersion` property of the VM extension.</span><span class="sxs-lookup"><span data-stu-id="9831c-348">This version is shown in the `typeHandlerVersion` property of the VM extension.</span></span> <span data-ttu-id="9831c-349">Make sure that the version specified in the `typeHandlerVersion` element of your template's VM extensions are available in the locations where you plan to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="9831c-349">Make sure that the version specified in the `typeHandlerVersion` element of your template's VM extensions are available in the locations where you plan to deploy the template.</span></span> <span data-ttu-id="9831c-350">For example, the following code specifies version 1.7:</span><span class="sxs-lookup"><span data-stu-id="9831c-350">For example, the following code specifies version 1.7:</span></span>

```json
{
    "name": "MyCustomScriptExtension",
    "type": "extensions",
    "apiVersion": "2016-03-30",
    "location": "[parameters('location')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
    ],
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.7",
        ...   
```

<span data-ttu-id="9831c-351">To retrieve a list of the available versions for a specific VM extension, use the [Get-AzureRmVMExtensionImage](/powershell/module/azurerm.compute/get-azurermvmextensionimage) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9831c-351">To retrieve a list of the available versions for a specific VM extension, use the [Get-AzureRmVMExtensionImage](/powershell/module/azurerm.compute/get-azurermvmextensionimage) cmdlet.</span></span> <span data-ttu-id="9831c-352">The following example retrieves the available versions for the PowerShell DSC (Desired State Configuration) VM extension from **myLocation**:</span><span class="sxs-lookup"><span data-stu-id="9831c-352">The following example retrieves the available versions for the PowerShell DSC (Desired State Configuration) VM extension from **myLocation**:</span></span>

```azurepowershell-interactive
Get-AzureRmVMExtensionImage -Location myLocation -PublisherName Microsoft.PowerShell -Type DSC | FT
```

<span data-ttu-id="9831c-353">To get a list of publishers, use the [Get-AzureRmVmImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command.</span><span class="sxs-lookup"><span data-stu-id="9831c-353">To get a list of publishers, use the [Get-AzureRmVmImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command.</span></span> <span data-ttu-id="9831c-354">To request type, use the [Get-AzureRmVMExtensionImageType](/powershell/module/azurerm.compute/get-azurermvmextensionimagetype) commend.</span><span class="sxs-lookup"><span data-stu-id="9831c-354">To request type, use the [Get-AzureRmVMExtensionImageType](/powershell/module/azurerm.compute/get-azurermvmextensionimagetype) commend.</span></span>

## <a name="tips-for-testing-and-automation"></a><span data-ttu-id="9831c-355">Tips for testing and automation</span><span class="sxs-lookup"><span data-stu-id="9831c-355">Tips for testing and automation</span></span>

<span data-ttu-id="9831c-356">It's a challenge to keep track of all related settings, capabilities, and limitations while authoring a template.</span><span class="sxs-lookup"><span data-stu-id="9831c-356">It's a challenge to keep track of all related settings, capabilities, and limitations while authoring a template.</span></span> <span data-ttu-id="9831c-357">The common approach is to develop and test templates against a single cloud before other locations are targeted.</span><span class="sxs-lookup"><span data-stu-id="9831c-357">The common approach is to develop and test templates against a single cloud before other locations are targeted.</span></span> <span data-ttu-id="9831c-358">However, the earlier that tests are performed in the authoring process, the less troubleshooting and code rewriting your development team will have to do.</span><span class="sxs-lookup"><span data-stu-id="9831c-358">However, the earlier that tests are performed in the authoring process, the less troubleshooting and code rewriting your development team will have to do.</span></span> <span data-ttu-id="9831c-359">Deployments that fail because of location dependencies can be time-consuming to troubleshoot.</span><span class="sxs-lookup"><span data-stu-id="9831c-359">Deployments that fail because of location dependencies can be time-consuming to troubleshoot.</span></span> <span data-ttu-id="9831c-360">That’s why we recommend automated testing as early as possible in the authoring cycle.</span><span class="sxs-lookup"><span data-stu-id="9831c-360">That’s why we recommend automated testing as early as possible in the authoring cycle.</span></span> <span data-ttu-id="9831c-361">Ultimately, you'll need less development time and fewer resources, and your cloud-consistent artifacts will become even more valuable.</span><span class="sxs-lookup"><span data-stu-id="9831c-361">Ultimately, you'll need less development time and fewer resources, and your cloud-consistent artifacts will become even more valuable.</span></span>

<span data-ttu-id="9831c-362">The following image shows a typical example of a development process for a team using an integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="9831c-362">The following image shows a typical example of a development process for a team using an integrated development environment (IDE).</span></span> <span data-ttu-id="9831c-363">At different stages in the timeline, different test types are executed.</span><span class="sxs-lookup"><span data-stu-id="9831c-363">At different stages in the timeline, different test types are executed.</span></span> <span data-ttu-id="9831c-364">Here, two developers are working on the same solution, but this scenario applies equally to a single developer or a large team.</span><span class="sxs-lookup"><span data-stu-id="9831c-364">Here, two developers are working on the same solution, but this scenario applies equally to a single developer or a large team.</span></span> <span data-ttu-id="9831c-365">Each developer typically creates a local copy of a central repository, enabling each one to work on the local copy without impacting the others who may be working on the same files.</span><span class="sxs-lookup"><span data-stu-id="9831c-365">Each developer typically creates a local copy of a central repository, enabling each one to work on the local copy without impacting the others who may be working on the same files.</span></span>

![Workflow](./media/templates-cloud-consistency/workflow.png) 

<span data-ttu-id="9831c-367">Consider the following tips for testing and automation:</span><span class="sxs-lookup"><span data-stu-id="9831c-367">Consider the following tips for testing and automation:</span></span>

* <span data-ttu-id="9831c-368">Do make use of testing tools.</span><span class="sxs-lookup"><span data-stu-id="9831c-368">Do make use of testing tools.</span></span> <span data-ttu-id="9831c-369">For example, Visual Studio Code and Visual Studio include IntelliSense and other features that can help you validate your templates.</span><span class="sxs-lookup"><span data-stu-id="9831c-369">For example, Visual Studio Code and Visual Studio include IntelliSense and other features that can help you validate your templates.</span></span>
* <span data-ttu-id="9831c-370">To improve the code quality during development on the local IDE, perform static code analysis with unit tests and integration tests.</span><span class="sxs-lookup"><span data-stu-id="9831c-370">To improve the code quality during development on the local IDE, perform static code analysis with unit tests and integration tests.</span></span> 
* <span data-ttu-id="9831c-371">For an even better experience during initial development, unit tests and integration tests should only warn when an issue is found and proceed with the tests.</span><span class="sxs-lookup"><span data-stu-id="9831c-371">For an even better experience during initial development, unit tests and integration tests should only warn when an issue is found and proceed with the tests.</span></span> <span data-ttu-id="9831c-372">That way, you can identify the issues to addressed and prioritize the order of the changes, also referred to as test-driven deployment (TDD).</span><span class="sxs-lookup"><span data-stu-id="9831c-372">That way, you can identify the issues to addressed and prioritize the order of the changes, also referred to as test-driven deployment (TDD).</span></span>
* <span data-ttu-id="9831c-373">Be aware that some tests can be performed without being connected to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9831c-373">Be aware that some tests can be performed without being connected to Azure Resource Manager.</span></span> <span data-ttu-id="9831c-374">Others, like testing template deployment, require Resource Manager to perform certain actions that cannot be performed offline.</span><span class="sxs-lookup"><span data-stu-id="9831c-374">Others, like testing template deployment, require Resource Manager to perform certain actions that cannot be performed offline.</span></span>
* <span data-ttu-id="9831c-375">Testing a deployment template against the validation API isn't equal to an actual deployment.</span><span class="sxs-lookup"><span data-stu-id="9831c-375">Testing a deployment template against the validation API isn't equal to an actual deployment.</span></span> <span data-ttu-id="9831c-376">Also, even if you deploy a template from a local file, any references to nested templates in the template are retrieved by Resource Manager directly, and artifacts referenced by VM extensions are retrieved by the VM agent running inside the deployed VM.</span><span class="sxs-lookup"><span data-stu-id="9831c-376">Also, even if you deploy a template from a local file, any references to nested templates in the template are retrieved by Resource Manager directly, and artifacts referenced by VM extensions are retrieved by the VM agent running inside the deployed VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9831c-377">Next steps</span><span class="sxs-lookup"><span data-stu-id="9831c-377">Next steps</span></span>

* [<span data-ttu-id="9831c-378">Azure Resource Manager template considerations</span><span class="sxs-lookup"><span data-stu-id="9831c-378">Azure Resource Manager template considerations</span></span>](../azure-stack/user/azure-stack-develop-templates.md)
* [<span data-ttu-id="9831c-379">Best practices for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="9831c-379">Best practices for Azure Resource Manager templates</span></span>](resource-group-authoring-templates.md)
