---
title: Create a Log Analytics workspace using Azure PowerShell| Microsoft Docs
description: Learn how to create a Log Analytics workspace to enable management solutions and data collection from your cloud and on-premises environments with Azure PowerShell.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptal
ms.date: 08/27/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 8bbe6411f60d755afcc568040b870bc85be88044
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870660"
---
# <a name="create-a-log-analytics-workspace-with-azure-powershell"></a><span data-ttu-id="3233f-103">Create a Log Analytics workspace with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3233f-103">Create a Log Analytics workspace with Azure PowerShell</span></span>

<span data-ttu-id="3233f-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="3233f-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="3233f-105">This quickstart shows you how to use the Azure PowerShell module to to deploy a Log Analytics workspace in Azure, which is a unique environment with its own data repository, data sources, and solutions.</span><span class="sxs-lookup"><span data-stu-id="3233f-105">This quickstart shows you how to use the Azure PowerShell module to to deploy a Log Analytics workspace in Azure, which is a unique environment with its own data repository, data sources, and solutions.</span></span>  <span data-ttu-id="3233f-106">The steps described in this article are required if you intend on collecting data from the following sources:</span><span class="sxs-lookup"><span data-stu-id="3233f-106">The steps described in this article are required if you intend on collecting data from the following sources:</span></span>

* <span data-ttu-id="3233f-107">Azure resources in your subscription</span><span class="sxs-lookup"><span data-stu-id="3233f-107">Azure resources in your subscription</span></span>  
* <span data-ttu-id="3233f-108">On-premises computers monitored by System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3233f-108">On-premises computers monitored by System Center Operations Manager</span></span>  
* <span data-ttu-id="3233f-109">Device collections from System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="3233f-109">Device collections from System Center Configuration Manager</span></span>  
* <span data-ttu-id="3233f-110">Diagnostic or log data from Azure storage</span><span class="sxs-lookup"><span data-stu-id="3233f-110">Diagnostic or log data from Azure storage</span></span>  
 
<span data-ttu-id="3233f-111">For other sources, such as Azure VMs and Windows or Linux VMs in your environment, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="3233f-111">For other sources, such as Azure VMs and Windows or Linux VMs in your environment, see the following topics:</span></span>

* [<span data-ttu-id="3233f-112">Collect data from Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="3233f-112">Collect data from Azure virtual machines</span></span>](log-analytics-quick-collect-azurevm.md)
* [<span data-ttu-id="3233f-113">Collect data from hybrid Linux computer</span><span class="sxs-lookup"><span data-stu-id="3233f-113">Collect data from hybrid Linux computer</span></span>](log-analytics-quick-collect-linux-computer.md)
* [<span data-ttu-id="3233f-114">Collect data from hybrid Windows computer</span><span class="sxs-lookup"><span data-stu-id="3233f-114">Collect data from hybrid Windows computer</span></span>](log-analytics-quick-collect-windows-computer.md)

<span data-ttu-id="3233f-115">If you don't have an Azure subscription, create [a free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3233f-115">If you don't have an Azure subscription, create [a free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3233f-116">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="3233f-116">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="3233f-117">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="3233f-117">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="3233f-118">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3233f-118">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="3233f-119">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="3233f-119">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="3233f-120">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="3233f-120">Create a workspace</span></span>
<span data-ttu-id="3233f-121">Create a worksapce with [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="3233f-121">Create a worksapce with [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span></span> <span data-ttu-id="3233f-122">The following example creates a workspace named *TestWorkspace* in the resource group *Lab* in the *eastus* location using a Resource Manager template from your local machine.</span><span class="sxs-lookup"><span data-stu-id="3233f-122">The following example creates a workspace named *TestWorkspace* in the resource group *Lab* in the *eastus* location using a Resource Manager template from your local machine.</span></span> <span data-ttu-id="3233f-123">The  JSON template is configured to only prompt you for the name of the workspace, and specifies a default value for the other parameters that would likely be used as a standard configuration in your environment.</span><span class="sxs-lookup"><span data-stu-id="3233f-123">The  JSON template is configured to only prompt you for the name of the workspace, and specifies a default value for the other parameters that would likely be used as a standard configuration in your environment.</span></span> 

<span data-ttu-id="3233f-124">The following parameters set a default value:</span><span class="sxs-lookup"><span data-stu-id="3233f-124">The following parameters set a default value:</span></span>

* <span data-ttu-id="3233f-125">location - defaults to East US</span><span class="sxs-lookup"><span data-stu-id="3233f-125">location - defaults to East US</span></span>
* <span data-ttu-id="3233f-126">sku - defaults to the new Per-GB pricing tier released in the April 2018 pricing model</span><span class="sxs-lookup"><span data-stu-id="3233f-126">sku - defaults to the new Per-GB pricing tier released in the April 2018 pricing model</span></span>

>[!WARNING]
><span data-ttu-id="3233f-127">If creating or configuring a Log Analytics workspace in a subscription that has opted into the new April 2018 pricing model, the only valid Log Analytics pricing tier is **PerGB2018**.</span><span class="sxs-lookup"><span data-stu-id="3233f-127">If creating or configuring a Log Analytics workspace in a subscription that has opted into the new April 2018 pricing model, the only valid Log Analytics pricing tier is **PerGB2018**.</span></span> 
>

### <a name="create-and-deploy-template"></a><span data-ttu-id="3233f-128">Create and deploy template</span><span class="sxs-lookup"><span data-stu-id="3233f-128">Create and deploy template</span></span>

1. <span data-ttu-id="3233f-129">Copy and paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="3233f-129">Copy and paste the following JSON syntax into your file:</span></span>

    ```json
    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "workspaceName": {
            "type": "String",
            "metadata": {
              "description": "Specifies the name of the workspace."
            }
        },
        "location": {
            "type": "String",
            "allowedValues": [
              "eastus",
              "westus"
            ],
            "defaultValue": "eastus",
            "metadata": {
              "description": "Specifies the location in which to create the workspace."
            }
        },
        "sku": {
            "type": "String",
            "allowedValues": [
              "Standalone",
              "PerNode",
              "PerGB2018"
            ],
            "defaultValue": "PerGB2018",
            "metadata": {
            "description": "Specifies the service tier of the workspace: Standalone, PerNode, Per-GB"
        }
          },
    },
    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "name": "[parameters('workspaceName')]",
            "apiVersion": "2017-03-15-preview",
            "location": "[parameters('location')]",
            "properties": {
                "sku": {
                    "Name": "[parameters('sku')]"
                },
                "features": {
                    "searchVersion": 1
                }
            }
          }
       ]
    }
    ```

2. <span data-ttu-id="3233f-130">Edit the template to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="3233f-130">Edit the template to meet your requirements.</span></span>  <span data-ttu-id="3233f-131">Review [Microsoft.OperationalInsights/workspaces template](https://docs.microsoft.com/azure/templates/microsoft.operationalinsights/workspaces) reference to learn what properties and values are supported.</span><span class="sxs-lookup"><span data-stu-id="3233f-131">Review [Microsoft.OperationalInsights/workspaces template](https://docs.microsoft.com/azure/templates/microsoft.operationalinsights/workspaces) reference to learn what properties and values are supported.</span></span> 
3. <span data-ttu-id="3233f-132">Save this file as **deploylaworkspacetemplate.json** to a local folder.</span><span class="sxs-lookup"><span data-stu-id="3233f-132">Save this file as **deploylaworkspacetemplate.json** to a local folder.</span></span>   
4. <span data-ttu-id="3233f-133">You are ready to deploy this template.</span><span class="sxs-lookup"><span data-stu-id="3233f-133">You are ready to deploy this template.</span></span> <span data-ttu-id="3233f-134">Use the following commands from the folder containing the template:</span><span class="sxs-lookup"><span data-stu-id="3233f-134">Use the following commands from the folder containing the template:</span></span>

    ```powershell
        New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile deploylaworkspacetemplate.json
    ```

<span data-ttu-id="3233f-135">The deployment can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="3233f-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="3233f-136">When it finishes, you see a message similar to the following that includes the result:</span><span class="sxs-lookup"><span data-stu-id="3233f-136">When it finishes, you see a message similar to the following that includes the result:</span></span>

![Example result when deployment is complete](./media/log-analytics-template-workspace-configuration/template-output-01.png)

## <a name="next-steps"></a><span data-ttu-id="3233f-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="3233f-138">Next steps</span></span>
<span data-ttu-id="3233f-139">Now that you have a workspace available, you can configure collection of monitoring telemetry, run log searches to analyze that data, and add a management solution to provide additional data and analytic insights.</span><span class="sxs-lookup"><span data-stu-id="3233f-139">Now that you have a workspace available, you can configure collection of monitoring telemetry, run log searches to analyze that data, and add a management solution to provide additional data and analytic insights.</span></span>  

* <span data-ttu-id="3233f-140">To enable data collection from Azure resources with Azure Diagnostics or Azure storage, see [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3233f-140">To enable data collection from Azure resources with Azure Diagnostics or Azure storage, see [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md).</span></span>  
* <span data-ttu-id="3233f-141">Add [System Center Operations Manager as a data source](log-analytics-om-agents.md) to collect data from agents reporting your Operations Manager management group and store it in your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="3233f-141">Add [System Center Operations Manager as a data source](log-analytics-om-agents.md) to collect data from agents reporting your Operations Manager management group and store it in your Log Analytics workspace.</span></span>  
* <span data-ttu-id="3233f-142">Connect [Configuration Manager](log-analytics-sccm.md) to import computers that are members of collections in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="3233f-142">Connect [Configuration Manager](log-analytics-sccm.md) to import computers that are members of collections in the hierarchy.</span></span>  
* <span data-ttu-id="3233f-143">Review the [management solutions](log-analytics-add-solutions.md) available and how to add or remove a solution from your workspace.</span><span class="sxs-lookup"><span data-stu-id="3233f-143">Review the [management solutions](log-analytics-add-solutions.md) available and how to add or remove a solution from your workspace.</span></span>