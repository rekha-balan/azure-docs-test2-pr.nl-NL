---
title: Create Azure Machine Learning Experimentation with an Azure Resource Manager template | Microsoft Docs
description: This article provides an example to create an Azure Machine Learning Experimentation account using an Azure Resource Manager template.
services: machine-learning
author: hning86
ms.author: haining
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 11/14/2017
ms.openlocfilehash: 7938eaa0e06c9a33034a7388d02845d60967774e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867083"
---
# <a name="configure-the-azure-machine-learning-experimentation-service"></a><span data-ttu-id="4d263-103">Configure the Azure Machine Learning Experimentation Service</span><span class="sxs-lookup"><span data-stu-id="4d263-103">Configure the Azure Machine Learning Experimentation Service</span></span>

## <a name="overview"></a><span data-ttu-id="4d263-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4d263-104">Overview</span></span>
<span data-ttu-id="4d263-105">Azure Machine Learning Experimentation Service account, workspace, and project are Azure Resources.</span><span class="sxs-lookup"><span data-stu-id="4d263-105">Azure Machine Learning Experimentation Service account, workspace, and project are Azure Resources.</span></span> <span data-ttu-id="4d263-106">As such, they can be deployed using Resources Manager templates.</span><span class="sxs-lookup"><span data-stu-id="4d263-106">As such, they can be deployed using Resources Manager templates.</span></span> <span data-ttu-id="4d263-107">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span><span class="sxs-lookup"><span data-stu-id="4d263-107">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="4d263-108">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="4d263-108">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="deploy-a-template"></a><span data-ttu-id="4d263-109">Deploy a template</span><span class="sxs-lookup"><span data-stu-id="4d263-109">Deploy a template</span></span>
<span data-ttu-id="4d263-110">Deploying a template requires only a couple of steps in the Azure Command Line Interface or in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4d263-110">Deploying a template requires only a couple of steps in the Azure Command Line Interface or in the Azure portal.</span></span>

### <a name="deploy-a-template-from-the-command-line"></a><span data-ttu-id="4d263-111">Deploy a template from the command line</span><span class="sxs-lookup"><span data-stu-id="4d263-111">Deploy a template from the command line</span></span>
<span data-ttu-id="4d263-112">Using the command-line interface, a single command can deploy a template to an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="4d263-112">Using the command-line interface, a single command can deploy a template to an existing resource group.</span></span>
<span data-ttu-id="4d263-113">See following for information about creating a template.</span><span class="sxs-lookup"><span data-stu-id="4d263-113">See following for information about creating a template.</span></span>

```sh
# Login and validate your are in the right subscription context
az login

# Create a new resource group (you can use an existing one)
az group create --name <resource group name> --location <supported Azure region>
az group deployment create -n testdeploy -g <resource group name> --template-file <template-file.json> --parameters <parameters.json>
```

### <a name="deploy-a-template-from-the-azure-portal"></a><span data-ttu-id="4d263-114">Deploy a template from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4d263-114">Deploy a template from the Azure portal</span></span>
<span data-ttu-id="4d263-115">If you prefer, you can also use Azure portal to create and deploy a template.</span><span class="sxs-lookup"><span data-stu-id="4d263-115">If you prefer, you can also use Azure portal to create and deploy a template.</span></span> <span data-ttu-id="4d263-116">Do as follows:</span><span class="sxs-lookup"><span data-stu-id="4d263-116">Do as follows:</span></span>

1. <span data-ttu-id="4d263-117">Navigate to [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d263-117">Navigate to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d263-118">Select **All Services** and search for "templates."</span><span class="sxs-lookup"><span data-stu-id="4d263-118">Select **All Services** and search for "templates."</span></span>
3. <span data-ttu-id="4d263-119">Select **Templates**.</span><span class="sxs-lookup"><span data-stu-id="4d263-119">Select **Templates**.</span></span>
4. <span data-ttu-id="4d263-120">Click on **+ Add** and copy your template information.</span><span class="sxs-lookup"><span data-stu-id="4d263-120">Click on **+ Add** and copy your template information.</span></span> 
5. <span data-ttu-id="4d263-121">Select the template created in step #4 and click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="4d263-121">Select the template created in step #4 and click **Deploy**.</span></span>


## <a name="create-a-template-from-an-existing-azure-resource-in-the-azure-portal"></a><span data-ttu-id="4d263-122">Create a template from an existing Azure resource in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4d263-122">Create a template from an existing Azure resource in the Azure portal</span></span>
<span data-ttu-id="4d263-123">If you already have an Azure Machine experimentation account available, in [Azure portal](https://portal.azure.com), you can generate a template from that resource.</span><span class="sxs-lookup"><span data-stu-id="4d263-123">If you already have an Azure Machine experimentation account available, in [Azure portal](https://portal.azure.com), you can generate a template from that resource.</span></span> 

1. <span data-ttu-id="4d263-124">Navigate to an Azure Experimentation Account in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d263-124">Navigate to an Azure Experimentation Account in [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d263-125">Under **settings**, click on **Automation script**.</span><span class="sxs-lookup"><span data-stu-id="4d263-125">Under **settings**, click on **Automation script**.</span></span>
3. <span data-ttu-id="4d263-126">Download the template.</span><span class="sxs-lookup"><span data-stu-id="4d263-126">Download the template.</span></span> 

<span data-ttu-id="4d263-127">Alternatively, you can manually edit the template files.</span><span class="sxs-lookup"><span data-stu-id="4d263-127">Alternatively, you can manually edit the template files.</span></span> <span data-ttu-id="4d263-128">See following for an example of a template and parameters files.</span><span class="sxs-lookup"><span data-stu-id="4d263-128">See following for an example of a template and parameters files.</span></span> 

### <a name="template-file-example"></a><span data-ttu-id="4d263-129">Template file example</span><span class="sxs-lookup"><span data-stu-id="4d263-129">Template file example</span></span>
<span data-ttu-id="4d263-130">Create a file called "template-file.json" with below content.</span><span class="sxs-lookup"><span data-stu-id="4d263-130">Create a file called "template-file.json" with below content.</span></span> 

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "accountName": {
            "type": "string",
            "metadata": {
                "description": "Name of the machine learning experimentation team account"
            }
        },
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of the machine learning experimentation account and other dependent resources."
            }
        },
        "storageAccountSku": {
            "type": "string",
            "defaultValue": "Standard_LRS",
            "metadata": {
                "description": "Sku of the storage account"
            }
        }
    },
    "variables": {
        "mlexpVersion": "2017-05-01-preview",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('accountName'))]"
    },
    "resources": [
        {
            "name": "[parameters('accountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[parameters('location')]",
            "apiVersion": "2016-12-01",
            "tags": {
                "mlteamAccount": "[parameters('accountName')]"
            },
            "sku": {
                "name": "[parameters('storageAccountSku')]"
            },
            "kind": "Storage",
            "properties": {
                "encryption": {
                    "services": {
                        "blob": {
                            "enabled": true
                        }
                    },
                    "keySource": "Microsoft.Storage"
                }
            }
        },
        {
            "apiVersion": "[variables('mlexpVersion')]",
            "type": "Microsoft.MachineLearningExperimentation/accounts",
            "name": "[parameters('accountName')]",
            "location": "[parameters('location')]",
            "dependsOn": [
                "[resourceId('Microsoft.Storage/storageAccounts', parameters('accountName'))]"
            ],
            "properties": {
                "storageAccount": {
                    "storageAccountId": "[variables('stgResourceId')]",
                    "accessKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('accountName')), '2016-12-01').keys[0].value]"
                }
            }
        }
    ]
}
```

### <a name="parameters"></a><span data-ttu-id="4d263-131">Parameters</span><span class="sxs-lookup"><span data-stu-id="4d263-131">Parameters</span></span> 
<span data-ttu-id="4d263-132">Create a file with below content and save it as <parameters.json>.</span><span class="sxs-lookup"><span data-stu-id="4d263-132">Create a file with below content and save it as <parameters.json>.</span></span> 

<span data-ttu-id="4d263-133">There are three values that you can change.</span><span class="sxs-lookup"><span data-stu-id="4d263-133">There are three values that you can change.</span></span> 
* <span data-ttu-id="4d263-134">AccountName: The name of the experimentation account.</span><span class="sxs-lookup"><span data-stu-id="4d263-134">AccountName: The name of the experimentation account.</span></span>
* <span data-ttu-id="4d263-135">Location: One of the supported Azure regions.</span><span class="sxs-lookup"><span data-stu-id="4d263-135">Location: One of the supported Azure regions.</span></span>
* <span data-ttu-id="4d263-136">Storage Account SKU: Azure ML only supports standard storage, not premium.</span><span class="sxs-lookup"><span data-stu-id="4d263-136">Storage Account SKU: Azure ML only supports standard storage, not premium.</span></span> <span data-ttu-id="4d263-137">For more information about storage, see [storage introduction](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="4d263-137">For more information about storage, see [storage introduction](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "accountName": {
         "value": "MyExperimentationAccount"
     },
     "location": {
         "value": "eastus2"
     },
     "storageAccountSku": {
         "value": "Standard_LRS"
     }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="4d263-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d263-138">Next steps</span></span>
* [<span data-ttu-id="4d263-139">Create and Install Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4d263-139">Create and Install Azure Machine Learning</span></span>](../service/quickstart-installation.md)
