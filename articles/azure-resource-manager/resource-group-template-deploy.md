---
title: Deploy resources with PowerShell and template | Microsoft Docs
description: Use Azure Resource Manager and Azure PowerShell to deploy a resources to Azure. The resources are defined in a Resource Manager template.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomfitz
ms.openlocfilehash: 894a50d4dbad017537c4b5e05d8a405f59ce84a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660954"
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="fc27b-104">Deploy resources with Resource Manager templates and Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc27b-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="fc27b-109">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span><span class="sxs-lookup"><span data-stu-id="fc27b-109">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="fc27b-110">Your template can be either a local file or an external file that is available through a URI.</span><span class="sxs-lookup"><span data-stu-id="fc27b-110">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="fc27b-111">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span><span class="sxs-lookup"><span data-stu-id="fc27b-111">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

## <a name="deploy"></a><span data-ttu-id="fc27b-112">Deploy</span><span class="sxs-lookup"><span data-stu-id="fc27b-112">Deploy</span></span>
* <span data-ttu-id="fc27b-113">To quickly get started with deployment, use the following commands to deploy a local template with inline parameters:</span><span class="sxs-lookup"><span data-stu-id="fc27b-113">To quickly get started with deployment, use the following commands to deploy a local template with inline parameters:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {your-subscription-ID}
  New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json -storageNamePrefix contoso -storageSKU Standard_GRS
  ```

  <span data-ttu-id="fc27b-114">The deployment can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="fc27b-114">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="fc27b-115">When it finishes, you see a message that includes the result:</span><span class="sxs-lookup"><span data-stu-id="fc27b-115">When it finishes, you see a message that includes the result:</span></span>

  ```powershell
  ProvisioningState       : Succeeded
  ```

* <span data-ttu-id="fc27b-116">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span><span class="sxs-lookup"><span data-stu-id="fc27b-116">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="fc27b-117">To see all your subscriptions and their IDs, use:</span><span class="sxs-lookup"><span data-stu-id="fc27b-117">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

* <span data-ttu-id="fc27b-118">To deploy an external template, use the **TemplateUri** parameter:</span><span class="sxs-lookup"><span data-stu-id="fc27b-118">To deploy an external template, use the **TemplateUri** parameter:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateUri https://raw.githubusercontent.com/exampleuser/MyTemplates/master/storage.json -storageNamePrefix contoso -storageSKU Standard_GRS
  ```

* <span data-ttu-id="fc27b-119">To pass the parameter values in a file, use the **TemplateParameterFile** parameter:</span><span class="sxs-lookup"><span data-stu-id="fc27b-119">To pass the parameter values in a file, use the **TemplateParameterFile** parameter:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json -TemplateParameterFile c:\MyTemplates\storage.parameters.json
  ```

  <span data-ttu-id="fc27b-120">The parameter file must be in the following format:</span><span class="sxs-lookup"><span data-stu-id="fc27b-120">The parameter file must be in the following format:</span></span>

   ```json
   {
     "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
        "storageNamePrefix": {
            "value": "contoso"
        },
        "storageSKU": {
            "value": "Standard_GRS"
        }
     }
   }
   ```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="fc27b-121">To use complete mode, use the **Mode** parameter:</span><span class="sxs-lookup"><span data-stu-id="fc27b-121">To use complete mode, use the **Mode** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="deploy-private-template-with-sas-token"></a><span data-ttu-id="fc27b-122">Deploy private template with SAS token</span><span class="sxs-lookup"><span data-stu-id="fc27b-122">Deploy private template with SAS token</span></span>
<span data-ttu-id="fc27b-123">You can add your templates to a storage account and link to them during deployment with a SAS token.</span><span class="sxs-lookup"><span data-stu-id="fc27b-123">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> By following the steps below, the blob containing the template is accessible to only the account owner. However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI. If another user intercepts the URI, that user is able to access the template. Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.
> 
> 

### <a name="add-private-template-to-storage-account"></a><span data-ttu-id="fc27b-128">Add private template to storage account</span><span class="sxs-lookup"><span data-stu-id="fc27b-128">Add private template to storage account</span></span>
<span data-ttu-id="fc27b-129">The following example sets up a private storage account container and uploads a template:</span><span class="sxs-lookup"><span data-stu-id="fc27b-129">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="fc27b-130">Provide SAS token during deployment</span><span class="sxs-lookup"><span data-stu-id="fc27b-130">Provide SAS token during deployment</span></span>
<span data-ttu-id="fc27b-131">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span><span class="sxs-lookup"><span data-stu-id="fc27b-131">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="fc27b-132">Set the expiry time to allow enough time to complete the deployment.</span><span class="sxs-lookup"><span data-stu-id="fc27b-132">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r -ExpiryTime (Get-Date).AddHours(2.0) -FullUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="fc27b-133">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fc27b-133">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="parameters"></a><span data-ttu-id="fc27b-134">Parameters</span><span class="sxs-lookup"><span data-stu-id="fc27b-134">Parameters</span></span>
   
<span data-ttu-id="fc27b-135">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, you are prompted to provide a value for that parameter.</span><span class="sxs-lookup"><span data-stu-id="fc27b-135">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, you are prompted to provide a value for that parameter.</span></span> <span data-ttu-id="fc27b-136">Azure PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="fc27b-136">Azure PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="fc27b-137">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.3.0/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc27b-137">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.3.0/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="fc27b-138">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="fc27b-138">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="fc27b-139">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span><span class="sxs-lookup"><span data-stu-id="fc27b-139">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

<span data-ttu-id="fc27b-140">You can use inline parameters and a local parameter file in the same deployment operation.</span><span class="sxs-lookup"><span data-stu-id="fc27b-140">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="fc27b-141">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span><span class="sxs-lookup"><span data-stu-id="fc27b-141">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="fc27b-142">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span><span class="sxs-lookup"><span data-stu-id="fc27b-142">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="fc27b-143">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span><span class="sxs-lookup"><span data-stu-id="fc27b-143">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="fc27b-144">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span><span class="sxs-lookup"><span data-stu-id="fc27b-144">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="fc27b-145">Provide all parameter values in the external file.</span><span class="sxs-lookup"><span data-stu-id="fc27b-145">Provide all parameter values in the external file.</span></span> <span data-ttu-id="fc27b-146">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span><span class="sxs-lookup"><span data-stu-id="fc27b-146">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

## <a name="debug"></a><span data-ttu-id="fc27b-147">Debug</span><span class="sxs-lookup"><span data-stu-id="fc27b-147">Debug</span></span>

<span data-ttu-id="fc27b-148">If you want to log additional information about the deployment that may help you troubleshoot any deployment errors, use the **DeploymentDebugLogLevel** parameter.</span><span class="sxs-lookup"><span data-stu-id="fc27b-148">If you want to log additional information about the deployment that may help you troubleshoot any deployment errors, use the **DeploymentDebugLogLevel** parameter.</span></span> <span data-ttu-id="fc27b-149">You can specify that request content, response content, or both be logged with the deployment operation.</span><span class="sxs-lookup"><span data-stu-id="fc27b-149">You can specify that request content, response content, or both be logged with the deployment operation.</span></span>
   
```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -DeploymentDebugLogLevel All -ResourceGroupName ExampleGroup -TemplateFile storage.json
```

<span data-ttu-id="fc27b-150">To get details about a failed deployment operation, use:</span><span class="sxs-lookup"><span data-stu-id="fc27b-150">To get details about a failed deployment operation, use:</span></span>

```powershell
(Get-AzureRmResourceGroupDeploymentOperation -DeploymentName ExampleDeployment -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
```

<span data-ttu-id="fc27b-151">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="fc27b-151">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="complete-deployment-script"></a><span data-ttu-id="fc27b-152">Complete deployment script</span><span class="sxs-lookup"><span data-stu-id="fc27b-152">Complete deployment script</span></span>

<span data-ttu-id="fc27b-153">The following example shows the PowerShell script for deploying a template that is generated by the [export template](resource-manager-export-template.md) feature:</span><span class="sxs-lookup"><span data-stu-id="fc27b-153">The following example shows the PowerShell script for deploying a template that is generated by the [export template](resource-manager-export-template.md) feature:</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template to Azure

 .DESCRIPTION
    Deploys an Azure Resource Manager template

 .PARAMETER subscriptionId
    The subscription id where the template will be deployed.

 .PARAMETER resourceGroupName
    The resource group where the template will be deployed. Can be the name of an existing or a new resource group.

 .PARAMETER resourceGroupLocation
    Optional, a resource group location. If specified, will try to create a new resource group in this location. If not specified, assumes resource group is existing.

 .PARAMETER deploymentName
    The deployment name.

 .PARAMETER templateFilePath
    Optional, path to the template file. Defaults to template.json.

 .PARAMETER parametersFilePath
    Optional, path to the parameters file. Defaults to parameters.json. If file is not found, will prompt for parameter values based on template.
#>

param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @();
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
``` 

## <a name="next-steps"></a><span data-ttu-id="fc27b-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc27b-154">Next steps</span></span>
* <span data-ttu-id="fc27b-155">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc27b-155">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="fc27b-156">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fc27b-156">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="fc27b-157">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="fc27b-157">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="fc27b-158">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fc27b-158">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="fc27b-159">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc27b-159">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fc27b-160">This series covers application architecture, access and security, availability and scale, and application deployment.</span><span class="sxs-lookup"><span data-stu-id="fc27b-160">This series covers application architecture, access and security, availability and scale, and application deployment.</span></span>

