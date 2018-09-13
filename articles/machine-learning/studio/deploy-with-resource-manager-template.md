---
title: Deploy a Machine Learning workspace with Azure Resource Manager | Microsoft Docs
description: How to deploy a workspace for Azure Machine Learning using Azure Resource Manager template
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/05/2018
ms.openlocfilehash: 82d2316b3f72fbb0c5c3ee1ea9424afcc7661361
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856002"
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="619d2-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="619d2-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="619d2-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="619d2-104">Introduction</span></span>
<span data-ttu-id="619d2-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span><span class="sxs-lookup"><span data-stu-id="619d2-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="619d2-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span><span class="sxs-lookup"><span data-stu-id="619d2-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="619d2-107">Imagine doing this manually for hundreds of workspaces.</span><span class="sxs-lookup"><span data-stu-id="619d2-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="619d2-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span><span class="sxs-lookup"><span data-stu-id="619d2-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="619d2-109">This article takes you through this process step-by-step.</span><span class="sxs-lookup"><span data-stu-id="619d2-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="619d2-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="619d2-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="619d2-111">Step-by-step: create a Machine Learning Workspace</span><span class="sxs-lookup"><span data-stu-id="619d2-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="619d2-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="619d2-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="619d2-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span><span class="sxs-lookup"><span data-stu-id="619d2-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="619d2-114">Create an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="619d2-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="619d2-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span><span class="sxs-lookup"><span data-stu-id="619d2-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="619d2-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span><span class="sxs-lookup"><span data-stu-id="619d2-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="619d2-117">It also uses the storage account name as a property when creating the workspace.</span><span class="sxs-lookup"><span data-stu-id="619d2-117">It also uses the storage account name as a property when creating the workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="619d2-118">Save this template as mlworkspace.json file under c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="619d2-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="619d2-119">Deploy the resource group, based on the template</span><span class="sxs-lookup"><span data-stu-id="619d2-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="619d2-120">Open PowerShell</span><span class="sxs-lookup"><span data-stu-id="619d2-120">Open PowerShell</span></span>
* <span data-ttu-id="619d2-121">Install modules for Azure Resource Manager and Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="619d2-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="619d2-122">These steps download and install the modules necessary to complete the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="619d2-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="619d2-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="619d2-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="619d2-124">Authenticate to Azure</span><span class="sxs-lookup"><span data-stu-id="619d2-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Connect-AzureRmAccount
```
<span data-ttu-id="619d2-125">This step needs to be repeated for each session.</span><span class="sxs-lookup"><span data-stu-id="619d2-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="619d2-126">Once authenticated, your subscription information should be displayed.</span><span class="sxs-lookup"><span data-stu-id="619d2-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure Account][1]

<span data-ttu-id="619d2-128">Now that we have access to Azure, we can create the resource group.</span><span class="sxs-lookup"><span data-stu-id="619d2-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="619d2-129">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="619d2-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="619d2-130">Verify that the resource group is correctly provisioned.</span><span class="sxs-lookup"><span data-stu-id="619d2-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="619d2-131">**ProvisioningState** should be “Succeeded.”</span><span class="sxs-lookup"><span data-stu-id="619d2-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="619d2-132">The resource group name is used by the template to generate the storage account name.</span><span class="sxs-lookup"><span data-stu-id="619d2-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="619d2-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span><span class="sxs-lookup"><span data-stu-id="619d2-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Resource Group][2]

* <span data-ttu-id="619d2-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span><span class="sxs-lookup"><span data-stu-id="619d2-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="619d2-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span><span class="sxs-lookup"><span data-stu-id="619d2-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="619d2-137">For example, you can access the Primary Key Token.</span><span class="sxs-lookup"><span data-stu-id="619d2-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="619d2-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span><span class="sxs-lookup"><span data-stu-id="619d2-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="619d2-139">For example, you can list the primary and secondary tokens of all workspaces.</span><span class="sxs-lookup"><span data-stu-id="619d2-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="619d2-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="619d2-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="619d2-141">Next Steps</span><span class="sxs-lookup"><span data-stu-id="619d2-141">Next Steps</span></span>
* <span data-ttu-id="619d2-142">Learn more about [authoring Azure Resource Manager Templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="619d2-142">Learn more about [authoring Azure Resource Manager Templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="619d2-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="619d2-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="619d2-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="619d2-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ./media/deploy-with-resource-manager-template/azuresubscription.png
[2]: ./media/deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
