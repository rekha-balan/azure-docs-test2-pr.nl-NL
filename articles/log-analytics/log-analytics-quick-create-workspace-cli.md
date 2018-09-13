---
title: Create a Log Analytics workspace using Azure CLI | Microsoft Docs
description: Learn how to create a Log Analytics workspace to enable management solutions and data collection from your cloud and on-premises environments with Azure CLI.
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
ms.openlocfilehash: a36702d13e32b9629b09ef88200d3e383693b67b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866342"
---
# <a name="create-a-log-analytics-workspace-with-azure-cli-20"></a><span data-ttu-id="dbf21-103">Create a Log Analytics workspace with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dbf21-103">Create a Log Analytics workspace with Azure CLI 2.0</span></span>

<span data-ttu-id="dbf21-104">The Azure CLI 2.0 is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="dbf21-104">The Azure CLI 2.0 is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="dbf21-105">This quickstart shows you how to use Azure CLI 2.0 to deploy a Log Analytics workspace in Azure, which is a unique environment with its own data repository, data sources, and solutions.</span><span class="sxs-lookup"><span data-stu-id="dbf21-105">This quickstart shows you how to use Azure CLI 2.0 to deploy a Log Analytics workspace in Azure, which is a unique environment with its own data repository, data sources, and solutions.</span></span>  <span data-ttu-id="dbf21-106">The steps described in this article are required if you intend on collecting data from the following sources:</span><span class="sxs-lookup"><span data-stu-id="dbf21-106">The steps described in this article are required if you intend on collecting data from the following sources:</span></span>

* <span data-ttu-id="dbf21-107">Azure resources in your subscription</span><span class="sxs-lookup"><span data-stu-id="dbf21-107">Azure resources in your subscription</span></span>  
* <span data-ttu-id="dbf21-108">On-premises computers monitored by System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="dbf21-108">On-premises computers monitored by System Center Operations Manager</span></span>  
* <span data-ttu-id="dbf21-109">Device collections from System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="dbf21-109">Device collections from System Center Configuration Manager</span></span>  
* <span data-ttu-id="dbf21-110">Diagnostic or log data from Azure storage</span><span class="sxs-lookup"><span data-stu-id="dbf21-110">Diagnostic or log data from Azure storage</span></span>  
 
<span data-ttu-id="dbf21-111">For other sources, such as Azure VMs and Windows or Linux VMs in your environment, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="dbf21-111">For other sources, such as Azure VMs and Windows or Linux VMs in your environment, see the following topics:</span></span>

* [<span data-ttu-id="dbf21-112">Collect data from Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="dbf21-112">Collect data from Azure virtual machines</span></span>](log-analytics-quick-collect-azurevm.md)
* [<span data-ttu-id="dbf21-113">Collect data from hybrid Linux computer</span><span class="sxs-lookup"><span data-stu-id="dbf21-113">Collect data from hybrid Linux computer</span></span>](log-analytics-quick-collect-linux-computer.md)
* [<span data-ttu-id="dbf21-114">Collect data from hybrid Windows computer</span><span class="sxs-lookup"><span data-stu-id="dbf21-114">Collect data from hybrid Windows computer</span></span>](log-analytics-quick-collect-windows-computer.md)

<span data-ttu-id="dbf21-115">If you don't have an Azure subscription, create [a free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="dbf21-115">If you don't have an Azure subscription, create [a free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dbf21-116">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.30 or later.</span><span class="sxs-lookup"><span data-stu-id="dbf21-116">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.30 or later.</span></span> <span data-ttu-id="dbf21-117">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="dbf21-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="dbf21-118">If you need to install or upgrade, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="dbf21-118">If you need to install or upgrade, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="dbf21-119">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="dbf21-119">Create a workspace</span></span>
<span data-ttu-id="dbf21-120">Create a worksapce with [az group deployment create](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create).</span><span class="sxs-lookup"><span data-stu-id="dbf21-120">Create a worksapce with [az group deployment create](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create).</span></span> <span data-ttu-id="dbf21-121">The following example creates a workspace named *TestWorkspace* in the resource group *Lab* in the *eastus* location using a Resource Manager template from your local machine.</span><span class="sxs-lookup"><span data-stu-id="dbf21-121">The following example creates a workspace named *TestWorkspace* in the resource group *Lab* in the *eastus* location using a Resource Manager template from your local machine.</span></span> <span data-ttu-id="dbf21-122">The  JSON template is configured to only prompt you for the name of the workspace, and specifies a default value for the other parameters that would likely be used as a standard configuration in your environment.</span><span class="sxs-lookup"><span data-stu-id="dbf21-122">The  JSON template is configured to only prompt you for the name of the workspace, and specifies a default value for the other parameters that would likely be used as a standard configuration in your environment.</span></span> <span data-ttu-id="dbf21-123">Or you can store the template in an Azure storage account for shared access in your organization.</span><span class="sxs-lookup"><span data-stu-id="dbf21-123">Or you can store the template in an Azure storage account for shared access in your organization.</span></span> <span data-ttu-id="dbf21-124">For further information about working with templates, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)</span><span class="sxs-lookup"><span data-stu-id="dbf21-124">For further information about working with templates, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)</span></span>

<span data-ttu-id="dbf21-125">The following parameters set a default value:</span><span class="sxs-lookup"><span data-stu-id="dbf21-125">The following parameters set a default value:</span></span>

* <span data-ttu-id="dbf21-126">location - defaults to East US</span><span class="sxs-lookup"><span data-stu-id="dbf21-126">location - defaults to East US</span></span>
* <span data-ttu-id="dbf21-127">sku - defaults to the new Per-GB pricing tier released in the April 2018 pricing model</span><span class="sxs-lookup"><span data-stu-id="dbf21-127">sku - defaults to the new Per-GB pricing tier released in the April 2018 pricing model</span></span>

>[!WARNING]
><span data-ttu-id="dbf21-128">If creating or configuring a Log Analytics workspace in a subscription that has opted into the new April 2018 pricing model, the only valid Log Analytics pricing tier is **PerGB2018**.</span><span class="sxs-lookup"><span data-stu-id="dbf21-128">If creating or configuring a Log Analytics workspace in a subscription that has opted into the new April 2018 pricing model, the only valid Log Analytics pricing tier is **PerGB2018**.</span></span> 
>

### <a name="create-and-deploy-template"></a><span data-ttu-id="dbf21-129">Create and deploy template</span><span class="sxs-lookup"><span data-stu-id="dbf21-129">Create and deploy template</span></span>

1. <span data-ttu-id="dbf21-130">Copy and paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="dbf21-130">Copy and paste the following JSON syntax into your file:</span></span>

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

2. <span data-ttu-id="dbf21-131">Edit the template to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="dbf21-131">Edit the template to meet your requirements.</span></span>  <span data-ttu-id="dbf21-132">Review [Microsoft.OperationalInsights/workspaces template](https://docs.microsoft.com/azure/templates/microsoft.operationalinsights/workspaces) reference to learn what properties and values are supported.</span><span class="sxs-lookup"><span data-stu-id="dbf21-132">Review [Microsoft.OperationalInsights/workspaces template](https://docs.microsoft.com/azure/templates/microsoft.operationalinsights/workspaces) reference to learn what properties and values are supported.</span></span> 
3. <span data-ttu-id="dbf21-133">Save this file as **deploylaworkspacetemplate.json** to a local folder.</span><span class="sxs-lookup"><span data-stu-id="dbf21-133">Save this file as **deploylaworkspacetemplate.json** to a local folder.</span></span>   
4. <span data-ttu-id="dbf21-134">You are ready to deploy this template.</span><span class="sxs-lookup"><span data-stu-id="dbf21-134">You are ready to deploy this template.</span></span> <span data-ttu-id="dbf21-135">Use the following commands from the folder containing the template:</span><span class="sxs-lookup"><span data-stu-id="dbf21-135">Use the following commands from the folder containing the template:</span></span>

    ```azurecli
    azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile deploylaworkspacetemplate.json
    ```

<span data-ttu-id="dbf21-136">The deployment can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="dbf21-136">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="dbf21-137">When it finishes, you see a message similar to the following that includes the result:</span><span class="sxs-lookup"><span data-stu-id="dbf21-137">When it finishes, you see a message similar to the following that includes the result:</span></span>

![Example result when deployment is complete](./media/log-analytics-template-workspace-configuration/template-output-01.png)

## <a name="next-steps"></a><span data-ttu-id="dbf21-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbf21-139">Next steps</span></span>
<span data-ttu-id="dbf21-140">Now that you have a workspace available, you can configure collection of monitoring telemetry, run log searches to analyze that data, and add a management solution to provide additional data and analytic insights.</span><span class="sxs-lookup"><span data-stu-id="dbf21-140">Now that you have a workspace available, you can configure collection of monitoring telemetry, run log searches to analyze that data, and add a management solution to provide additional data and analytic insights.</span></span>  

* <span data-ttu-id="dbf21-141">To enable data collection from Azure resources with Azure Diagnostics or Azure storage, see [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dbf21-141">To enable data collection from Azure resources with Azure Diagnostics or Azure storage, see [Collect Azure service logs and metrics for use in Log Analytics](log-analytics-azure-storage.md).</span></span>  
* <span data-ttu-id="dbf21-142">Add [System Center Operations Manager as a data source](log-analytics-om-agents.md) to collect data from agents reporting your Operations Manager management group and store it in your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="dbf21-142">Add [System Center Operations Manager as a data source](log-analytics-om-agents.md) to collect data from agents reporting your Operations Manager management group and store it in your Log Analytics workspace.</span></span>  
* <span data-ttu-id="dbf21-143">Connect [Configuration Manager](log-analytics-sccm.md) to import computers that are members of collections in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="dbf21-143">Connect [Configuration Manager](log-analytics-sccm.md) to import computers that are members of collections in the hierarchy.</span></span>  
* <span data-ttu-id="dbf21-144">Review the [management solutions](log-analytics-add-solutions.md) available and how to add or remove a solution from your workspace.</span><span class="sxs-lookup"><span data-stu-id="dbf21-144">Review the [management solutions](log-analytics-add-solutions.md) available and how to add or remove a solution from your workspace.</span></span>