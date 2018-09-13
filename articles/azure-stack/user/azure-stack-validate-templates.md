---
title: Use a template validation tool to check templates for Azure Stack | Microsoft Docs
description: Check templates for deployment to Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: jeffgo
ms.openlocfilehash: 73a0766baee8da782f0192fbc17fb2898a8360ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866912"
---
# <a name="check-your-templates-for-azure-stack-with-the-template-validation-tool"></a><span data-ttu-id="98928-103">Check your templates for Azure Stack with the template validation tool</span><span class="sxs-lookup"><span data-stu-id="98928-103">Check your templates for Azure Stack with the template validation tool</span></span>

<span data-ttu-id="98928-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="98928-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="98928-105">You can use the template validation tool to check if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for deploying to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="98928-105">You can use the template validation tool to check if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for deploying to Azure Stack.</span></span> <span data-ttu-id="98928-106">The template validation tool is available as a part of the Azure Stack tools.</span><span class="sxs-lookup"><span data-stu-id="98928-106">The template validation tool is available as a part of the Azure Stack tools.</span></span> <span data-ttu-id="98928-107">Download the Azure Stack tools by using the steps described in the [download tools from GitHub](azure-stack-powershell-download.md) article.</span><span class="sxs-lookup"><span data-stu-id="98928-107">Download the Azure Stack tools by using the steps described in the [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span>

## <a name="overview"></a><span data-ttu-id="98928-108">Overview</span><span class="sxs-lookup"><span data-stu-id="98928-108">Overview</span></span>

<span data-ttu-id="98928-109">To validate a template, you have to build a cloud capabilities file first and then run the validation tool.</span><span class="sxs-lookup"><span data-stu-id="98928-109">To validate a template, you have to build a cloud capabilities file first and then run the validation tool.</span></span> <span data-ttu-id="98928-110">You use the following PowerShell modules from Azure Stack tools:</span><span class="sxs-lookup"><span data-stu-id="98928-110">You use the following PowerShell modules from Azure Stack tools:</span></span>

- <span data-ttu-id="98928-111">In the **CloudCapabilities** folder:</span><span class="sxs-lookup"><span data-stu-id="98928-111">In the **CloudCapabilities** folder:</span></span><br>         <span data-ttu-id="98928-112">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing the services and versions in an Azure Stack cloud.</span><span class="sxs-lookup"><span data-stu-id="98928-112">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing the services and versions in an Azure Stack cloud.</span></span>
- <span data-ttu-id="98928-113">In the **TemplateValidator** folder:</span><span class="sxs-lookup"><span data-stu-id="98928-113">In the **TemplateValidator** folder:</span></span><br>
<span data-ttu-id="98928-114">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file to test templates for deployment in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="98928-114">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file to test templates for deployment in Azure Stack.</span></span>

## <a name="build-the-cloud-capabilities-file"></a><span data-ttu-id="98928-115">Build the cloud capabilities file</span><span class="sxs-lookup"><span data-stu-id="98928-115">Build the cloud capabilities file</span></span>

<span data-ttu-id="98928-116">Before you use the template validator, run the AzureRM.CloudCapabilities PowerShell module to build a JSON file.</span><span class="sxs-lookup"><span data-stu-id="98928-116">Before you use the template validator, run the AzureRM.CloudCapabilities PowerShell module to build a JSON file.</span></span>

>[!NOTE]
><span data-ttu-id="98928-117">If you update your integrated system, or add any new services or virtual extensions, you should run this module again.</span><span class="sxs-lookup"><span data-stu-id="98928-117">If you update your integrated system, or add any new services or virtual extensions, you should run this module again.</span></span>

1. <span data-ttu-id="98928-118">Make sure you have connectivity to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="98928-118">Make sure you have connectivity to Azure Stack.</span></span> <span data-ttu-id="98928-119">These steps can be performed from the Azure Stack development kit host, or you can use a [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) to connect from your workstation.</span><span class="sxs-lookup"><span data-stu-id="98928-119">These steps can be performed from the Azure Stack development kit host, or you can use a [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) to connect from your workstation.</span></span>
2. <span data-ttu-id="98928-120">Import the AzureRM.CloudCapabilities PowerShell module:</span><span class="sxs-lookup"><span data-stu-id="98928-120">Import the AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ```

3. <span data-ttu-id="98928-121">Use the Get-CloudCapabilities cmdlet to retrieve service versions and create a cloud capabilities JSON file.</span><span class="sxs-lookup"><span data-stu-id="98928-121">Use the Get-CloudCapabilities cmdlet to retrieve service versions and create a cloud capabilities JSON file.</span></span> <span data-ttu-id="98928-122">If you don't specify **-OutputPath**, the file AzureCloudCapabilities.Json is created in the current directory.</span><span class="sxs-lookup"><span data-stu-id="98928-122">If you don't specify **-OutputPath**, the file AzureCloudCapabilities.Json is created in the current directory.</span></span> <span data-ttu-id="98928-123">Use your actual location:</span><span class="sxs-lookup"><span data-stu-id="98928-123">Use your actual location:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapability -Location <your location> -Verbose
    ```

## <a name="validate-templates"></a><span data-ttu-id="98928-124">Validate templates</span><span class="sxs-lookup"><span data-stu-id="98928-124">Validate templates</span></span>

<span data-ttu-id="98928-125">Use these steps to validate templates by using the AzureRM.TemplateValidator PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="98928-125">Use these steps to validate templates by using the AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="98928-126">You can use your own templates, or validate the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="98928-126">You can use your own templates, or validate the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1. <span data-ttu-id="98928-127">Import the AzureRM.TemplateValidator.psm1 PowerShell module:</span><span class="sxs-lookup"><span data-stu-id="98928-127">Import the AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>

    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2. <span data-ttu-id="98928-128">Run the template validator:</span><span class="sxs-lookup"><span data-stu-id="98928-128">Run the template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path to template.json or template folder> `
    -CapabilitiesPath <path to cloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="98928-129">Template validation warnings or errors are logged to the PowerShell console and an HTML file in the source directory.</span><span class="sxs-lookup"><span data-stu-id="98928-129">Template validation warnings or errors are logged to the PowerShell console and an HTML file in the source directory.</span></span> <span data-ttu-id="98928-130">The following screen capture shows an example of a validation report:</span><span class="sxs-lookup"><span data-stu-id="98928-130">The following screen capture shows an example of a validation report:</span></span>

![Template validation report](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="98928-132">Parameters</span><span class="sxs-lookup"><span data-stu-id="98928-132">Parameters</span></span>

<span data-ttu-id="98928-133">The template validator supports the following parameters.</span><span class="sxs-lookup"><span data-stu-id="98928-133">The template validator supports the following parameters.</span></span>

| <span data-ttu-id="98928-134">Parameter</span><span class="sxs-lookup"><span data-stu-id="98928-134">Parameter</span></span> | <span data-ttu-id="98928-135">Description</span><span class="sxs-lookup"><span data-stu-id="98928-135">Description</span></span> | <span data-ttu-id="98928-136">Required</span><span class="sxs-lookup"><span data-stu-id="98928-136">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="98928-137">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="98928-137">TemplatePath</span></span> | <span data-ttu-id="98928-138">Specifies the path to recursively find Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="98928-138">Specifies the path to recursively find Azure Resource Manager templates</span></span> | <span data-ttu-id="98928-139">Yes</span><span class="sxs-lookup"><span data-stu-id="98928-139">Yes</span></span> | 
| <span data-ttu-id="98928-140">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="98928-140">TemplatePattern</span></span> | <span data-ttu-id="98928-141">Specifies the name of template files to match.</span><span class="sxs-lookup"><span data-stu-id="98928-141">Specifies the name of template files to match.</span></span> | <span data-ttu-id="98928-142">No</span><span class="sxs-lookup"><span data-stu-id="98928-142">No</span></span> |
| <span data-ttu-id="98928-143">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="98928-143">CapabilitiesPath</span></span> | <span data-ttu-id="98928-144">Specifies the path to cloud capabilities JSON file</span><span class="sxs-lookup"><span data-stu-id="98928-144">Specifies the path to cloud capabilities JSON file</span></span> | <span data-ttu-id="98928-145">Yes</span><span class="sxs-lookup"><span data-stu-id="98928-145">Yes</span></span> | 
| <span data-ttu-id="98928-146">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="98928-146">IncludeComputeCapabilities</span></span> | <span data-ttu-id="98928-147">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span><span class="sxs-lookup"><span data-stu-id="98928-147">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="98928-148">No</span><span class="sxs-lookup"><span data-stu-id="98928-148">No</span></span> |
| <span data-ttu-id="98928-149">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="98928-149">IncludeStorageCapabilities</span></span> | <span data-ttu-id="98928-150">Includes evaluation of storage resources like SKU types</span><span class="sxs-lookup"><span data-stu-id="98928-150">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="98928-151">No</span><span class="sxs-lookup"><span data-stu-id="98928-151">No</span></span> |
| <span data-ttu-id="98928-152">Report</span><span class="sxs-lookup"><span data-stu-id="98928-152">Report</span></span> | <span data-ttu-id="98928-153">Specifies name of the generated HTML report</span><span class="sxs-lookup"><span data-stu-id="98928-153">Specifies name of the generated HTML report</span></span> | <span data-ttu-id="98928-154">No</span><span class="sxs-lookup"><span data-stu-id="98928-154">No</span></span> |
| <span data-ttu-id="98928-155">Verbose</span><span class="sxs-lookup"><span data-stu-id="98928-155">Verbose</span></span> | <span data-ttu-id="98928-156">Logs errors and warnings to the console</span><span class="sxs-lookup"><span data-stu-id="98928-156">Logs errors and warnings to the console</span></span> | <span data-ttu-id="98928-157">No</span><span class="sxs-lookup"><span data-stu-id="98928-157">No</span></span>|

### <a name="examples"></a><span data-ttu-id="98928-158">Examples</span><span class="sxs-lookup"><span data-stu-id="98928-158">Examples</span></span>

<span data-ttu-id="98928-159">This example validates all of the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded to local storage.</span><span class="sxs-lookup"><span data-stu-id="98928-159">This example validates all of the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded to local storage.</span></span> <span data-ttu-id="98928-160">The example also validates virtual machine sizes and extensions against Azure Stack Development Kit capabilities.</span><span class="sxs-lookup"><span data-stu-id="98928-160">The example also validates virtual machine sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="next-steps"></a><span data-ttu-id="98928-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="98928-161">Next steps</span></span>

- [<span data-ttu-id="98928-162">Deploy templates to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="98928-162">Deploy templates to Azure Stack</span></span>](azure-stack-arm-templates.md)
- [<span data-ttu-id="98928-163">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="98928-163">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
