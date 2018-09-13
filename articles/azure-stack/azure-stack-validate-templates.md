---
title: Use Template Validator to check templates for Azure Stack | Microsoft Docs
description: Check templates for deployment to Azure Stack
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/1/2016
ms.author: helaw
ms.openlocfilehash: d84bdb3e21d9ba29672948f87953dfca81cb7722
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554044"
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="38090-103">Check your templates for Azure Stack with Template Validator</span><span class="sxs-lookup"><span data-stu-id="38090-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="38090-104">You can use the template validation tool to check if your Azure Resource Manager [templates](azure-stack-arm-templates.md) work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="38090-104">You can use the template validation tool to check if your Azure Resource Manager [templates](azure-stack-arm-templates.md) work with Azure Stack.</span></span> <span data-ttu-id="38090-105">The template validation tool is available as a part of the Azure Stack tools.</span><span class="sxs-lookup"><span data-stu-id="38090-105">The template validation tool is available as a part of the Azure Stack tools.</span></span> <span data-ttu-id="38090-106">Download the Azure Stack tools by using the steps descibed in the [download tools from GitHub](azure-stack-powershell-download.md) article.</span><span class="sxs-lookup"><span data-stu-id="38090-106">Download the Azure Stack tools by using the steps descibed in the [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="38090-107">To validate templates, you will use the following PowerShell modules and the JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span><span class="sxs-lookup"><span data-stu-id="38090-107">To validate templates, you will use the following PowerShell modules and the JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="38090-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing the services and versions in a cloud like Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="38090-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing the services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="38090-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file to test templates for deployment in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="38090-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file to test templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="38090-110">AzureStackCapabilities_TP2.json is a default cloud capabilities file.</span><span class="sxs-lookup"><span data-stu-id="38090-110">AzureStackCapabilities_TP2.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="38090-111">You can create your own, or use this file to get started.</span><span class="sxs-lookup"><span data-stu-id="38090-111">You can create your own, or use this file to get started.</span></span> 

<span data-ttu-id="38090-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span><span class="sxs-lookup"><span data-stu-id="38090-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="38090-113">Validate templates</span><span class="sxs-lookup"><span data-stu-id="38090-113">Validate templates</span></span>
<span data-ttu-id="38090-114">In these steps, you validate templates by using the AzureRM.TemplateValidator PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="38090-114">In these steps, you validate templates by using the AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="38090-115">You can use your own templates, or validate the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="38090-115">You can use your own templates, or validate the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="38090-116">Import the AzureRM.TemplateValidator.psm1 PowerShell module:</span><span class="sxs-lookup"><span data-stu-id="38090-116">Import the AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    import-module .\TemplateValidator\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="38090-117">Run the template validator:</span><span class="sxs-lookup"><span data-stu-id="38090-117">Run the template validator:</span></span>

    ```PowerShell
    test-azureRMTemplate -TemplatePath <path to template.json or template folder>`
    -CapabilitiesPath <path to cloudcapabilities.json>`
    -Verbose
    ```

<span data-ttu-id="38090-118">Any template validation warnings or errors are logged to the PowerShell console, and are also logged to an HTML file in the source directory.</span><span class="sxs-lookup"><span data-stu-id="38090-118">Any template validation warnings or errors are logged to the PowerShell console, and are also logged to an HTML file in the source directory.</span></span>  

### <a name="parameters"></a><span data-ttu-id="38090-119">Parameters</span><span class="sxs-lookup"><span data-stu-id="38090-119">Parameters</span></span>

| <span data-ttu-id="38090-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="38090-120">Parameter</span></span> | <span data-ttu-id="38090-121">Description</span><span class="sxs-lookup"><span data-stu-id="38090-121">Description</span></span> | <span data-ttu-id="38090-122">Required</span><span class="sxs-lookup"><span data-stu-id="38090-122">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="38090-123">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="38090-123">TemplatePath</span></span> | <span data-ttu-id="38090-124">Specifies the path to recursively find Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="38090-124">Specifies the path to recursively find Resource Manager templates</span></span> | <span data-ttu-id="38090-125">Yes</span><span class="sxs-lookup"><span data-stu-id="38090-125">Yes</span></span> | 
| <span data-ttu-id="38090-126">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="38090-126">TemplatePattern</span></span> | <span data-ttu-id="38090-127">Specifies the name of template files to match.</span><span class="sxs-lookup"><span data-stu-id="38090-127">Specifies the name of template files to match.</span></span> | <span data-ttu-id="38090-128">No</span><span class="sxs-lookup"><span data-stu-id="38090-128">No</span></span> |
| <span data-ttu-id="38090-129">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="38090-129">CapabilitiesPath</span></span> | <span data-ttu-id="38090-130">Specifies the path to cloud capabilities JSON file</span><span class="sxs-lookup"><span data-stu-id="38090-130">Specifies the path to cloud capabilities JSON file</span></span> | <span data-ttu-id="38090-131">Yes</span><span class="sxs-lookup"><span data-stu-id="38090-131">Yes</span></span> | 
| <span data-ttu-id="38090-132">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="38090-132">IncludeComputeCapabilities</span></span> | <span data-ttu-id="38090-133">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span><span class="sxs-lookup"><span data-stu-id="38090-133">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="38090-134">No</span><span class="sxs-lookup"><span data-stu-id="38090-134">No</span></span> |
| <span data-ttu-id="38090-135">Report</span><span class="sxs-lookup"><span data-stu-id="38090-135">Report</span></span> | <span data-ttu-id="38090-136">Specifies name of the generated HTML report</span><span class="sxs-lookup"><span data-stu-id="38090-136">Specifies name of the generated HTML report</span></span> | <span data-ttu-id="38090-137">No</span><span class="sxs-lookup"><span data-stu-id="38090-137">No</span></span> |
| <span data-ttu-id="38090-138">Verbose</span><span class="sxs-lookup"><span data-stu-id="38090-138">Verbose</span></span> | <span data-ttu-id="38090-139">Logs errors and warnings to the console</span><span class="sxs-lookup"><span data-stu-id="38090-139">Logs errors and warnings to the console</span></span> | <span data-ttu-id="38090-140">No</span><span class="sxs-lookup"><span data-stu-id="38090-140">No</span></span>|


### <a name="examples"></a><span data-ttu-id="38090-141">Examples</span><span class="sxs-lookup"><span data-stu-id="38090-141">Examples</span></span>
<span data-ttu-id="38090-142">This example validates all the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates the VM sizes and extensions against Azure Stack TP2 capabilities.</span><span class="sxs-lookup"><span data-stu-id="38090-142">This example validates all the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates the VM sizes and extensions against Azure Stack TP2 capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates`
-CapabilitiesPath .\TemplateValidator\AzureStackCapabilities_TP3.json`
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="38090-143">Build cloud capabilities file</span><span class="sxs-lookup"><span data-stu-id="38090-143">Build cloud capabilities file</span></span>
<span data-ttu-id="38090-144">The downloaded files include a default AzureStackCapabilities_TP2.json file, which describes the service versions available in a default installation of Azure Stack TP2.</span><span class="sxs-lookup"><span data-stu-id="38090-144">The downloaded files include a default AzureStackCapabilities_TP2.json file, which describes the service versions available in a default installation of Azure Stack TP2.</span></span>  <span data-ttu-id="38090-145">As you install additional Resource Providers, you can use the AzureRM.CloudCapabilities PowerShell module to build a JSON file including the new services.</span><span class="sxs-lookup"><span data-stu-id="38090-145">As you install additional Resource Providers, you can use the AzureRM.CloudCapabilities PowerShell module to build a JSON file including the new services.</span></span>  

1.  <span data-ttu-id="38090-146">Make sure you have connectivity to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="38090-146">Make sure you have connectivity to Azure Stack.</span></span>  <span data-ttu-id="38090-147">These steps can be performed from [MAS-CON01](azure-stack-connect-azure-stack.md#connect-with-remote-desktop), or you can use [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn) to connect from your workstation.</span><span class="sxs-lookup"><span data-stu-id="38090-147">These steps can be performed from [MAS-CON01](azure-stack-connect-azure-stack.md#connect-with-remote-desktop), or you can use [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn) to connect from your workstation.</span></span> 
2.  <span data-ttu-id="38090-148">Import the AzureRM.CloudCapabilities PowerShell module:</span><span class="sxs-lookup"><span data-stu-id="38090-148">Import the AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    import-module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="38090-149">Use the Get-CloudCapabilities cmdlet to retrieve service versions and create a cloud capabilities JSON file:</span><span class="sxs-lookup"><span data-stu-id="38090-149">Use the Get-CloudCapabilities cmdlet to retrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="38090-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="38090-150">Next steps</span></span>
 - [<span data-ttu-id="38090-151">Deploy templates to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="38090-151">Deploy templates to Azure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="38090-152">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span><span class="sxs-lookup"><span data-stu-id="38090-152">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>

