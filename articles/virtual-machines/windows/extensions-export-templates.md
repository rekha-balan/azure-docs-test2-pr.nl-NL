---
title: Exporting Azure Resource Groups that contain VM extensions | Microsoft Docs
description: Export Resource Manager templates that include virtual machine extensions.
services: virtual-machines-windows
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: 69d3485068c79978db099c6d034dfe0f054dc4ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564152"
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="00aaa-103">Exporting Resource Groups that contain VM extensions</span><span class="sxs-lookup"><span data-stu-id="00aaa-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="00aaa-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span><span class="sxs-lookup"><span data-stu-id="00aaa-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="00aaa-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span><span class="sxs-lookup"><span data-stu-id="00aaa-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="00aaa-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span><span class="sxs-lookup"><span data-stu-id="00aaa-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="00aaa-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span><span class="sxs-lookup"><span data-stu-id="00aaa-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="00aaa-108">Supported Virtual Machine Extensions</span><span class="sxs-lookup"><span data-stu-id="00aaa-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="00aaa-109">Many Virtual Machine extensions are available.</span><span class="sxs-lookup"><span data-stu-id="00aaa-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="00aaa-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span><span class="sxs-lookup"><span data-stu-id="00aaa-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span></span> <span data-ttu-id="00aaa-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span><span class="sxs-lookup"><span data-stu-id="00aaa-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span></span>

<span data-ttu-id="00aaa-112">The following extensions can be exported with the automation script feature.</span><span class="sxs-lookup"><span data-stu-id="00aaa-112">The following extensions can be exported with the automation script feature.</span></span>

| <span data-ttu-id="00aaa-113">Extension</span><span class="sxs-lookup"><span data-stu-id="00aaa-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="00aaa-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="00aaa-114">Acronis Backup</span></span> | <span data-ttu-id="00aaa-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="00aaa-115">Datadog Windows Agent</span></span> | <span data-ttu-id="00aaa-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-116">OS Patching For Linux</span></span> | <span data-ttu-id="00aaa-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="00aaa-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-118">Acronis Backup Linux</span></span> | <span data-ttu-id="00aaa-119">Docker Extension</span><span class="sxs-lookup"><span data-stu-id="00aaa-119">Docker Extension</span></span> | <span data-ttu-id="00aaa-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="00aaa-120">Puppet Agent</span></span> |
| <span data-ttu-id="00aaa-121">Bg Info</span><span class="sxs-lookup"><span data-stu-id="00aaa-121">Bg Info</span></span> | <span data-ttu-id="00aaa-122">DSC Extension</span><span class="sxs-lookup"><span data-stu-id="00aaa-122">DSC Extension</span></span> | <span data-ttu-id="00aaa-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="00aaa-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="00aaa-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="00aaa-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-125">Dynatrace Linux</span></span> | <span data-ttu-id="00aaa-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="00aaa-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="00aaa-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="00aaa-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="00aaa-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="00aaa-128">Dynatrace Windows</span></span> | <span data-ttu-id="00aaa-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="00aaa-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="00aaa-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="00aaa-130">Chef Client</span></span> | <span data-ttu-id="00aaa-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="00aaa-131">HPE Security Application Defender</span></span> | <span data-ttu-id="00aaa-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="00aaa-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="00aaa-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="00aaa-133">Custom Script</span></span> | <span data-ttu-id="00aaa-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="00aaa-134">IaaS Antimalware</span></span> | <span data-ttu-id="00aaa-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="00aaa-136">Custom Script Extension</span><span class="sxs-lookup"><span data-stu-id="00aaa-136">Custom Script Extension</span></span> | <span data-ttu-id="00aaa-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="00aaa-137">IaaS Diagnostics</span></span> | <span data-ttu-id="00aaa-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-138">VM Access For Linux</span></span> |
| <span data-ttu-id="00aaa-139">Custom Script for Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-139">Custom Script for Linux</span></span> | <span data-ttu-id="00aaa-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="00aaa-140">Linux Chef Client</span></span> | <span data-ttu-id="00aaa-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="00aaa-141">VM Access For Linux</span></span> |
| <span data-ttu-id="00aaa-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="00aaa-142">Datadog Linux Agent</span></span> | <span data-ttu-id="00aaa-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="00aaa-143">Linux Diagnostic</span></span> | <span data-ttu-id="00aaa-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="00aaa-144">VM Snapshot</span></span> |

## <a name="export-the-resource-group"></a><span data-ttu-id="00aaa-145">Export the Resource Group</span><span class="sxs-lookup"><span data-stu-id="00aaa-145">Export the Resource Group</span></span>

<span data-ttu-id="00aaa-146">To export a Resource Group into a reusable template, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="00aaa-146">To export a Resource Group into a reusable template, complete the following steps:</span></span>

1. <span data-ttu-id="00aaa-147">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="00aaa-147">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="00aaa-148">On the Hub Menu, click Resource Groups</span><span class="sxs-lookup"><span data-stu-id="00aaa-148">On the Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="00aaa-149">Select the target resource group from the list</span><span class="sxs-lookup"><span data-stu-id="00aaa-149">Select the target resource group from the list</span></span>
4. <span data-ttu-id="00aaa-150">In the Resource Group blade, click Automation Script</span><span class="sxs-lookup"><span data-stu-id="00aaa-150">In the Resource Group blade, click Automation Script</span></span>

![Template Export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/extensions-export-templates/template-export.png)

<span data-ttu-id="00aaa-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="00aaa-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="00aaa-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span><span class="sxs-lookup"><span data-stu-id="00aaa-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="00aaa-154">Configure protected settings</span><span class="sxs-lookup"><span data-stu-id="00aaa-154">Configure protected settings</span></span>

<span data-ttu-id="00aaa-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span><span class="sxs-lookup"><span data-stu-id="00aaa-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="00aaa-156">Protected settings are not exported with the automation script.</span><span class="sxs-lookup"><span data-stu-id="00aaa-156">Protected settings are not exported with the automation script.</span></span> <span data-ttu-id="00aaa-157">If necessary, protected settings need to be reinserted into the exported templated.</span><span class="sxs-lookup"><span data-stu-id="00aaa-157">If necessary, protected settings need to be reinserted into the exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="00aaa-158">Step 1 - Remove template parameter</span><span class="sxs-lookup"><span data-stu-id="00aaa-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="00aaa-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span><span class="sxs-lookup"><span data-stu-id="00aaa-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span></span> <span data-ttu-id="00aaa-160">This parameter can be removed.</span><span class="sxs-lookup"><span data-stu-id="00aaa-160">This parameter can be removed.</span></span> <span data-ttu-id="00aaa-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span><span class="sxs-lookup"><span data-stu-id="00aaa-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="00aaa-162">Step 2 - Get protected settings properties</span><span class="sxs-lookup"><span data-stu-id="00aaa-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="00aaa-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span><span class="sxs-lookup"><span data-stu-id="00aaa-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span></span> <span data-ttu-id="00aaa-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="00aaa-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="00aaa-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span><span class="sxs-lookup"><span data-stu-id="00aaa-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span></span> 

<span data-ttu-id="00aaa-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="00aaa-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="00aaa-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span><span class="sxs-lookup"><span data-stu-id="00aaa-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="00aaa-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="00aaa-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-the-protected-configuration"></a><span data-ttu-id="00aaa-169">Step 3 - Re-create the protected configuration</span><span class="sxs-lookup"><span data-stu-id="00aaa-169">Step 3 - Re-create the protected configuration</span></span>

<span data-ttu-id="00aaa-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span><span class="sxs-lookup"><span data-stu-id="00aaa-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span></span>

<span data-ttu-id="00aaa-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span><span class="sxs-lookup"><span data-stu-id="00aaa-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="00aaa-172">The final extension resource looks similar to the following JSON example:</span><span class="sxs-lookup"><span data-stu-id="00aaa-172">The final extension resource looks similar to the following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="00aaa-173">If using template parameters to provide property values, these need to be created.</span><span class="sxs-lookup"><span data-stu-id="00aaa-173">If using template parameters to provide property values, these need to be created.</span></span> <span data-ttu-id="00aaa-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span><span class="sxs-lookup"><span data-stu-id="00aaa-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="00aaa-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="00aaa-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="00aaa-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="00aaa-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="00aaa-177">At this point, the template can be deployed using any template deployment method.</span><span class="sxs-lookup"><span data-stu-id="00aaa-177">At this point, the template can be deployed using any template deployment method.</span></span>

