---
title: Deploy an Azure Resource Manager template in an Azure Automation runbook
description: How to deploy an Azure Resource Manager template stored in Azure Storage from a runbook
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 03/16/2018
ms.topic: conceptual
manager: carmonm
keywords: powershell,  runbook, json, azure automation
ms.openlocfilehash: fe7a3632936e13a0762ebc0afcc357965e019146
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869615"
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="2bf1e-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span><span class="sxs-lookup"><span data-stu-id="2bf1e-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="2bf1e-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="2bf1e-106">By doing this, you can automate deployment of Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="2bf1e-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="2bf1e-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bf1e-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2bf1e-109">Prerequisites</span></span>

<span data-ttu-id="2bf1e-110">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="2bf1e-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2bf1e-111">Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-111">Azure subscription.</span></span> <span data-ttu-id="2bf1e-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or [sign up for a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or [sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="2bf1e-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="2bf1e-114">This account must have permission to start and stop the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="2bf1e-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="2bf1e-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="2bf1e-116">Azure Powershell installed on a local machine.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="2bf1e-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="2bf1e-118">Create the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="2bf1e-118">Create the Resource Manager template</span></span>

<span data-ttu-id="2bf1e-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="2bf1e-120">In a text editor, copy the following text:</span><span class="sxs-lookup"><span data-stu-id="2bf1e-120">In a text editor, copy the following text:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2018-02-01",
      "location": "[parameters('location')]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

<span data-ttu-id="2bf1e-121">Save the file locally as `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="2bf1e-122">Save the Resource Manager template in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2bf1e-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="2bf1e-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="2bf1e-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="2bf1e-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Connect-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="2bf1e-126">Create the PowerShell runbook script</span><span class="sxs-lookup"><span data-stu-id="2bf1e-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="2bf1e-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="2bf1e-128">In a text editor, paste the following text:</span><span class="sxs-lookup"><span data-stu-id="2bf1e-128">In a text editor, paste the following text:</span></span>

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Connect-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="2bf1e-129">Save the file locally as `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="2bf1e-130">Import and publish the runbook into your Azure Automation account</span><span class="sxs-lookup"><span data-stu-id="2bf1e-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="2bf1e-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="2bf1e-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="2bf1e-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="2bf1e-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @importParams

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="2bf1e-134">Start the runbook</span><span class="sxs-lookup"><span data-stu-id="2bf1e-134">Start the runbook</span></span>

<span data-ttu-id="2bf1e-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="2bf1e-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="2bf1e-137">Run the following commands in the PowerShell console:</span><span class="sxs-lookup"><span data-stu-id="2bf1e-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="2bf1e-138">The runbook runs, and you can check its status by running `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="2bf1e-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="2bf1e-140">You can see that the new storage account was created by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2bf1e-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="2bf1e-141">Summary</span><span class="sxs-lookup"><span data-stu-id="2bf1e-141">Summary</span></span>

<span data-ttu-id="2bf1e-142">That's it!</span><span class="sxs-lookup"><span data-stu-id="2bf1e-142">That's it!</span></span> <span data-ttu-id="2bf1e-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2bf1e-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bf1e-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="2bf1e-144">Next steps</span></span>

* <span data-ttu-id="2bf1e-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2bf1e-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="2bf1e-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="2bf1e-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="2bf1e-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="2bf1e-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="2bf1e-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

