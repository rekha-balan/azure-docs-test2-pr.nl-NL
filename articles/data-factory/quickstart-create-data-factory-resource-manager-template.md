---
title: Create an Azure data factory using Resource Manager template | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using an Azure Resource Manager template.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 01/22/2018
ms.author: douglasl
ms.openlocfilehash: a7c11e4bd3ac30c930ec717426c43d4361e32088
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856768"
---
# <a name="tutorial-create-an-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="6b24b-103">Tutorial: Create an Azure data factory using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="6b24b-103">Tutorial: Create an Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-build-your-first-pipeline-using-arm.md)
> * [Current version](quickstart-create-data-factory-resource-manager-template.md) 

<span data-ttu-id="6b24b-106">This quickstart describes how to use an Azure Resource Manager template to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="6b24b-106">This quickstart describes how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="6b24b-107">The pipeline you create in this data factory **copies** data from one folder to another folder in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6b24b-107">The pipeline you create in this data factory **copies** data from one folder to another folder in an Azure blob storage.</span></span> <span data-ttu-id="6b24b-108">For a tutorial on how to **transform** data using Azure Data Factory, see [Tutorial: Transform data using Spark](transform-data-using-spark.md).</span><span class="sxs-lookup"><span data-stu-id="6b24b-108">For a tutorial on how to **transform** data using Azure Data Factory, see [Tutorial: Transform data using Spark](transform-data-using-spark.md).</span></span> 

> [!NOTE]
> This article does not provide a detailed introduction of the Data Factory service. For an introduction to the Azure Data Factory service, see [Introduction to Azure Data Factory](introduction.md).

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

### <a name="azure-powershell"></a><span data-ttu-id="6b24b-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b24b-111">Azure PowerShell</span></span>
<span data-ttu-id="6b24b-112">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6b24b-112">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="resource-manager-templates"></a><span data-ttu-id="6b24b-113">Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="6b24b-113">Resource Manager templates</span></span>
<span data-ttu-id="6b24b-114">To learn about Azure Resource Manager templates in general, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6b24b-114">To learn about Azure Resource Manager templates in general, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="6b24b-115">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span><span class="sxs-lookup"><span data-stu-id="6b24b-115">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="6b24b-116">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span><span class="sxs-lookup"><span data-stu-id="6b24b-116">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json"></a><span data-ttu-id="6b24b-117">Data Factory JSON</span><span class="sxs-lookup"><span data-stu-id="6b24b-117">Data Factory JSON</span></span> 
<span data-ttu-id="6b24b-118">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFTutorial** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="6b24b-118">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFTutorial** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "dataFactoryName": {
            "type": "string",
            "metadata": {
                "description": "Name of the data factory. Must be globally unique."
            }
        },
        "dataFactoryLocation": {
            "type": "string",
            "allowedValues": [
                "East US",
                "East US 2",
                "West Europe"
            ],
            "defaultValue": "East US",
            "metadata": {
                "description": "Location of the data factory. Currently, only East US, East US 2, and West Europe are supported. "
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Azure storage account that contains the input/output data."
            }
        },
        "storageAccountKey": {
            "type": "securestring",
            "metadata": {
                "description": "Key for the Azure storage account."
            }
        },
        "blobContainer": {
            "type": "string",
            "metadata": {
                "description": "Name of the blob container in the Azure Storage account."
            }
        },
        "inputBlobFolder": {
            "type": "string",
            "metadata": {
                "description": "The folder in the blob container that has the input file."
            }
        },
        "inputBlobName": {
            "type": "string",
            "metadata": {
                "description": "Name of the input file/blob."
            }
        },
        "outputBlobFolder": {
            "type": "string",
            "metadata": {
                "description": "The folder in the blob container that will hold the transformed data."
            }
        },
        "outputBlobName": {
            "type": "string",
            "metadata": {
                "description": "Name of the output file/blob."
            }
        },
        "triggerStartTime": {
            "type": "string",
            "metadata": {
                "description": "Start time for the trigger."
            }
        },
        "triggerEndTime": {
            "type": "string",
            "metadata": {
                "description": "End time for the trigger."
            }
        }
    },
    "variables": {
        "azureStorageLinkedServiceName": "ArmtemplateStorageLinkedService",
        "inputDatasetName": "ArmtemplateTestDatasetIn",
        "outputDatasetName": "ArmtemplateTestDatasetOut",
        "pipelineName": "ArmtemplateSampleCopyPipeline",
        "triggerName": "ArmTemplateTestTrigger"
    },
    "resources": [{
        "name": "[parameters('dataFactoryName')]",
        "apiVersion": "2017-09-01-preview",
        "type": "Microsoft.DataFactory/factories",
        "location": "[parameters('dataFactoryLocation')]",
        "properties": {
            "loggingStorageAccountName": "[parameters('storageAccountName')]",
            "loggingStorageAccountKey": "[parameters('storageAccountKey')]"
        },
        "resources": [{
                "type": "linkedservices",
                "name": "[variables('azureStorageLinkedServiceName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureStorage",
                    "description": "Azure Storage linked service",
                    "typeProperties": {
                        "connectionString": {
                            "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]",
                            "type": "SecureString"
                        }
                    }
                }
            },
            {
                "type": "datasets",
                "name": "[variables('inputDatasetName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureBlob",
                    "typeProperties": {
                        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'), '/')]",
                        "fileName": "[parameters('inputBlobName')]"
                    },
                    "linkedServiceName": {
                        "referenceName": "[variables('azureStorageLinkedServiceName')]",
                        "type": "LinkedServiceReference"
                    }
                }
            },
            {
                "type": "datasets",
                "name": "[variables('outputDatasetName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureBlob",
                    "typeProperties": {
                        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'), '/')]",
                        "fileName": "[parameters('outputBlobName')]"
                    },
                    "linkedServiceName": {
                        "referenceName": "[variables('azureStorageLinkedServiceName')]",
                        "type": "LinkedServiceReference"
                    }
                }
            },
            {
                "type": "pipelines",
                "name": "[variables('pipelineName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]",
                    "[variables('inputDatasetName')]",
                    "[variables('outputDatasetName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "activities": [{
                        "type": "Copy",
                        "typeProperties": {
                            "source": {
                                "type": "BlobSource"
                            },
                            "sink": {
                                "type": "BlobSink"
                            }
                        },
                        "name": "MyCopyActivity",
                        "inputs": [{
                            "referenceName": "[variables('inputDatasetName')]",
                            "type": "DatasetReference"
                        }],
                        "outputs": [{
                            "referenceName": "[variables('outputDatasetName')]",
                            "type": "DatasetReference"
                        }]
                    }]
                }
            },
            {
                "type": "triggers",
                "name": "[variables('triggerName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]",
                    "[variables('inputDatasetName')]",
                    "[variables('outputDatasetName')]",
                    "[variables('pipelineName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "ScheduleTrigger",
                    "typeProperties": {
                        "recurrence": {
                            "frequency": "Hour",
                            "interval": 1,
                            "startTime": "[parameters('triggerStartTime')]",
                            "endTime": "[parameters('triggerEndTime')]",
                            "timeZone": "UTC"
                        }
                    },
                    "pipelines": [{
                        "pipelineReference": {
                            "type": "PipelineReference",
                            "referenceName": "ArmtemplateSampleCopyPipeline"
                        },
                        "parameters": {}
                    }]
                }
            }
        ]
    }]
}
```

## <a name="parameters-json"></a><span data-ttu-id="6b24b-119">Parameters JSON</span><span class="sxs-lookup"><span data-stu-id="6b24b-119">Parameters JSON</span></span>
<span data-ttu-id="6b24b-120">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="6b24b-120">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> - Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file. You created the adftutorial container and uploaded the sample file (emp.txt) to the input folder in this Azure blob storage. 
> - Specify a globally unique name for the data factory for the **dataFactoryName** parameter. For example: ARMTutorialFactoryJohnDoe11282017. 
> - For the **triggerStartTime**, specify the current day in the format: `2017-11-28T00:00:00`.
> - For the **triggerEndTime**, specify the next day in the format: `2017-11-29T00:00:00`. You can also check the current UTC time and specify the next hour or two as the end time. For example, if the UTC time now is 1:32 AM, specify `2017-11-29:03:00:00` as the end time. In this case, the trigger runs the pipeline twice (at 2 AM and 3 AM).

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "dataFactoryName": {
      "value": "<datafactoryname>"
    },    
    "dataFactoryLocation": {
      "value": "East US"
    },
    "storageAccountName": {
      "value": "<yourstroageaccountname>"
    },
    "storageAccountKey": {
      "value": "<yourstorageaccountkey>"
    },
    "blobContainer": {
      "value": "adftutorial"
    },
    "inputBlobFolder": {
      "value": "input"
    },
    "inputBlobName": {
      "value": "emp.txt"
    },
    "outputBlobFolder": {
      "value": "output"
    },
    "outputBlobName": {
      "value": "emp.txt"
    },
    "triggerStartTime": {
        "value": "2017-11-28T00:00:00. Set to today"
    },
    "triggerEndTime": {
        "value": "2017-11-29T00:00:00. Set to tomorrow"
    }
  }
}
```

> [!IMPORTANT]
> You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template. By using a Power Shell script, you can automate deploying Data Factory entities in these environments. 

## <a name="deploy-data-factory-entities"></a><span data-ttu-id="6b24b-132">Deploy Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="6b24b-132">Deploy Data Factory entities</span></span> 
<span data-ttu-id="6b24b-133">In PowerShell, run the following command to deploy Data Factory entities using the Resource Manager template you created earlier in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="6b24b-133">In PowerShell, run the following command to deploy Data Factory entities using the Resource Manager template you created earlier in this quickstart.</span></span> 

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFTutorial\ADFTutorialARM.json -TemplateParameterFile C:\ADFTutorial\ADFTutorialARM-Parameters.json
```

<span data-ttu-id="6b24b-134">You see output similar to the following sample:</span><span class="sxs-lookup"><span data-stu-id="6b24b-134">You see output similar to the following sample:</span></span> 

```
DeploymentName          : MyARMDeployment
ResourceGroupName       : ADFTutorialResourceGroup
ProvisioningState       : Succeeded
Timestamp               : 11/29/2017 3:11:13 AM
Mode                    : Incremental
TemplateLink            :
Parameters              :
                          Name                 Type            Value
                          ===============      ============    ==========
                          dataFactoryName      String          <data factory name>
                          dataFactoryLocation  String          East US
                          storageAccountName   String          <storage account name>
                          storageAccountKey    SecureString
                          blobContainer        String          adftutorial
                          inputBlobFolder      String          input
                          inputBlobName        String          emp.txt
                          outputBlobFolder     String          output
                          outputBlobName       String          emp.txt
                          triggerStartTime     String          11/29/2017 12:00:00 AM
                          triggerEndTime       String          11/29/2017 4:00:00 AM

Outputs                 :
DeploymentDebugLogLevel :
```

## <a name="start-the-trigger"></a><span data-ttu-id="6b24b-135">Start the trigger</span><span class="sxs-lookup"><span data-stu-id="6b24b-135">Start the trigger</span></span>

<span data-ttu-id="6b24b-136">The template deploys the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="6b24b-136">The template deploys the following Data Factory entities:</span></span> 

- <span data-ttu-id="6b24b-137">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="6b24b-137">Azure Storage linked service</span></span>
- <span data-ttu-id="6b24b-138">Azure Blob datasets (input and output)</span><span class="sxs-lookup"><span data-stu-id="6b24b-138">Azure Blob datasets (input and output)</span></span>
- <span data-ttu-id="6b24b-139">Pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="6b24b-139">Pipeline with a copy activity</span></span>
- <span data-ttu-id="6b24b-140">Trigger to trigger the pipeline</span><span class="sxs-lookup"><span data-stu-id="6b24b-140">Trigger to trigger the pipeline</span></span>

<span data-ttu-id="6b24b-141">The deployed trigger is in stopped state.</span><span class="sxs-lookup"><span data-stu-id="6b24b-141">The deployed trigger is in stopped state.</span></span> <span data-ttu-id="6b24b-142">One of the ways to start the trigger is to use the **Start-AzureRmDataFactoryV2Trigger** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b24b-142">One of the ways to start the trigger is to use the **Start-AzureRmDataFactoryV2Trigger** PowerShell cmdlet.</span></span> <span data-ttu-id="6b24b-143">The following procedure provides detailed steps:</span><span class="sxs-lookup"><span data-stu-id="6b24b-143">The following procedure provides detailed steps:</span></span> 

1. <span data-ttu-id="6b24b-144">In the PowerShell window, create a variable to hold the name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="6b24b-144">In the PowerShell window, create a variable to hold the name of the resource group.</span></span> <span data-ttu-id="6b24b-145">Copy the following command into the PowerShell window, and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="6b24b-145">Copy the following command into the PowerShell window, and press ENTER.</span></span> <span data-ttu-id="6b24b-146">If you have specified a different resource group name for the New-AzureRmResourceGroupDeployment command, update the value here.</span><span class="sxs-lookup"><span data-stu-id="6b24b-146">If you have specified a different resource group name for the New-AzureRmResourceGroupDeployment command, update the value here.</span></span> 

    ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ``` 
1. <span data-ttu-id="6b24b-147">Create a variable to hold the name of the data factory.</span><span class="sxs-lookup"><span data-stu-id="6b24b-147">Create a variable to hold the name of the data factory.</span></span> <span data-ttu-id="6b24b-148">Specify the same name that you specified in the ADFTutorialARM-Parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="6b24b-148">Specify the same name that you specified in the ADFTutorialARM-Parameters.json file.</span></span>   

    ```powershell
    $dataFactoryName = "<yourdatafactoryname>"
    ```
3. <span data-ttu-id="6b24b-149">Set a variable for the name of the trigger.</span><span class="sxs-lookup"><span data-stu-id="6b24b-149">Set a variable for the name of the trigger.</span></span> <span data-ttu-id="6b24b-150">The name of the trigger is hardcoded in the Resource Manager template file (ADFTutorialARM.json).</span><span class="sxs-lookup"><span data-stu-id="6b24b-150">The name of the trigger is hardcoded in the Resource Manager template file (ADFTutorialARM.json).</span></span>

    ```powershell
    $triggerName = "ArmTemplateTestTrigger"
    ```
4. <span data-ttu-id="6b24b-151">Get the **status of the trigger** by running the following PowerShell command after specifying the name of your data factory and trigger:</span><span class="sxs-lookup"><span data-stu-id="6b24b-151">Get the **status of the trigger** by running the following PowerShell command after specifying the name of your data factory and trigger:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $triggerName
    ```

    <span data-ttu-id="6b24b-152">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="6b24b-152">Here is the sample output:</span></span> 

    ```json
    TriggerName       : ArmTemplateTestTrigger
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ARMFactory1128
    Properties        : Microsoft.Azure.Management.DataFactory.Models.ScheduleTrigger
    RuntimeState      : Stopped
    ```
    
    <span data-ttu-id="6b24b-153">Notice that the runtime state of the trigger is **Stopped**.</span><span class="sxs-lookup"><span data-stu-id="6b24b-153">Notice that the runtime state of the trigger is **Stopped**.</span></span> 
5. <span data-ttu-id="6b24b-154">**Start the trigger**.</span><span class="sxs-lookup"><span data-stu-id="6b24b-154">**Start the trigger**.</span></span> <span data-ttu-id="6b24b-155">The trigger runs the pipeline defined in the template at the hour.</span><span class="sxs-lookup"><span data-stu-id="6b24b-155">The trigger runs the pipeline defined in the template at the hour.</span></span> <span data-ttu-id="6b24b-156">That's, if you executed this command at 2:25 PM, the trigger runs the pipeline at 3 PM for the first time.</span><span class="sxs-lookup"><span data-stu-id="6b24b-156">That's, if you executed this command at 2:25 PM, the trigger runs the pipeline at 3 PM for the first time.</span></span> <span data-ttu-id="6b24b-157">Then, it runs the pipeline hourly until the  end time you specified for the trigger.</span><span class="sxs-lookup"><span data-stu-id="6b24b-157">Then, it runs the pipeline hourly until the  end time you specified for the trigger.</span></span> 

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -TriggerName $triggerName
    ```
    
    <span data-ttu-id="6b24b-158">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="6b24b-158">Here is the sample output:</span></span> 
    
    ```
    Confirm
    Are you sure you want to start trigger 'ArmTemplateTestTrigger' in data factory 'ARMFactory1128'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    True
    ```
6. <span data-ttu-id="6b24b-159">Confirm that the trigger has been started by running the Get-AzureRmDataFactoryV2Trigger command again.</span><span class="sxs-lookup"><span data-stu-id="6b24b-159">Confirm that the trigger has been started by running the Get-AzureRmDataFactoryV2Trigger command again.</span></span>  

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -TriggerName $triggerName
    ```
    
    <span data-ttu-id="6b24b-160">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="6b24b-160">Here is the sample output:</span></span>
    
    ```
    TriggerName       : ArmTemplateTestTrigger
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ARMFactory1128
    Properties        : Microsoft.Azure.Management.DataFactory.Models.ScheduleTrigger
    RuntimeState      : Started
    ```

## <a name="monitor-the-pipeline"></a><span data-ttu-id="6b24b-161">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="6b24b-161">Monitor the pipeline</span></span>
1. <span data-ttu-id="6b24b-162">After logging in to the [Azure portal](https://portal.azure.com/), Click **All services**, search with the keyword such as **data fa**, and select **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="6b24b-162">After logging in to the [Azure portal](https://portal.azure.com/), Click **All services**, search with the keyword such as **data fa**, and select **Data factories**.</span></span>

    ![Browse data factories menu](media/quickstart-create-data-factory-resource-manager-template/browse-data-factories-menu.png)
2. <span data-ttu-id="6b24b-164">In the **Data Factories** page, click the data factory you created.</span><span class="sxs-lookup"><span data-stu-id="6b24b-164">In the **Data Factories** page, click the data factory you created.</span></span> <span data-ttu-id="6b24b-165">If needed, filter the list with the name of your data factory.</span><span class="sxs-lookup"><span data-stu-id="6b24b-165">If needed, filter the list with the name of your data factory.</span></span>  

    ![Select data factory](media/quickstart-create-data-factory-resource-manager-template/select-data-factory.png)
3. <span data-ttu-id="6b24b-167">In the Data factory page, click **Monitor & Manage** tile.</span><span class="sxs-lookup"><span data-stu-id="6b24b-167">In the Data factory page, click **Monitor & Manage** tile.</span></span> 

    ![Monitor and manage tile](media/quickstart-create-data-factory-resource-manager-template/monitor-manage-tile.png)
4. <span data-ttu-id="6b24b-169">The **Data Integration Application** should open in a separate tab in the web browser.</span><span class="sxs-lookup"><span data-stu-id="6b24b-169">The **Data Integration Application** should open in a separate tab in the web browser.</span></span> <span data-ttu-id="6b24b-170">If the monitor tab is not active, switch to the **monitor tab**. Notice that the pipeline run was triggered by a **scheduler trigger**.</span><span class="sxs-lookup"><span data-stu-id="6b24b-170">If the monitor tab is not active, switch to the **monitor tab**. Notice that the pipeline run was triggered by a **scheduler trigger**.</span></span> 

    ![Monitor pipeline run](media/quickstart-create-data-factory-resource-manager-template/monitor-pipeline-run.png)    

    > [!IMPORTANT]
    > You see pipeline runs only at the hour clock (for example: 4 AM, 5 AM, 6 AM, etc.). Click **Refresh** on the toolbar to refresh the list when the time reaches the next hour. 
5. <span data-ttu-id="6b24b-174">Click the link in the **Actions** columns.</span><span class="sxs-lookup"><span data-stu-id="6b24b-174">Click the link in the **Actions** columns.</span></span> 

    ![Pipeline actions link](media/quickstart-create-data-factory-resource-manager-template/pipeline-actions-link.png)
6. <span data-ttu-id="6b24b-176">You see the activity runs associated with the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="6b24b-176">You see the activity runs associated with the pipeline run.</span></span> <span data-ttu-id="6b24b-177">In this quickstart, the pipeline has only one activity of type: Copy.</span><span class="sxs-lookup"><span data-stu-id="6b24b-177">In this quickstart, the pipeline has only one activity of type: Copy.</span></span> <span data-ttu-id="6b24b-178">Therefore, you see a run for that activity.</span><span class="sxs-lookup"><span data-stu-id="6b24b-178">Therefore, you see a run for that activity.</span></span> 

    ![Activity runs](media/quickstart-create-data-factory-resource-manager-template/activity-runs.png)
1. <span data-ttu-id="6b24b-180">Click the link under **Output** column.</span><span class="sxs-lookup"><span data-stu-id="6b24b-180">Click the link under **Output** column.</span></span> <span data-ttu-id="6b24b-181">You see the output from the copy operation in an **Output** window.</span><span class="sxs-lookup"><span data-stu-id="6b24b-181">You see the output from the copy operation in an **Output** window.</span></span> <span data-ttu-id="6b24b-182">Click the maximize button to see the full output.</span><span class="sxs-lookup"><span data-stu-id="6b24b-182">Click the maximize button to see the full output.</span></span> <span data-ttu-id="6b24b-183">You can close the maximized output window or close it.</span><span class="sxs-lookup"><span data-stu-id="6b24b-183">You can close the maximized output window or close it.</span></span> 

    ![Output window](media/quickstart-create-data-factory-resource-manager-template/output-window.png)
7. <span data-ttu-id="6b24b-185">Stop the trigger once you see a successful/failure run.</span><span class="sxs-lookup"><span data-stu-id="6b24b-185">Stop the trigger once you see a successful/failure run.</span></span> <span data-ttu-id="6b24b-186">The trigger runs the pipeline once an hour.</span><span class="sxs-lookup"><span data-stu-id="6b24b-186">The trigger runs the pipeline once an hour.</span></span> <span data-ttu-id="6b24b-187">The pipeline copies the same file from the input folder to the output folder for each run.</span><span class="sxs-lookup"><span data-stu-id="6b24b-187">The pipeline copies the same file from the input folder to the output folder for each run.</span></span> <span data-ttu-id="6b24b-188">To stop the trigger, run the following command in the PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="6b24b-188">To stop the trigger, run the following command in the PowerShell window.</span></span> 
    
    ```powershell
    Stop-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $triggerName
    ```

[!INCLUDE [data-factory-quickstart-verify-output-cleanup.md](../../includes/data-factory-quickstart-verify-output-cleanup.md)] 

## <a name="data-factory-entities-in-the-template"></a> <span data-ttu-id="6b24b-189">JSON definitions for entities</span><span class="sxs-lookup"><span data-stu-id="6b24b-189">JSON definitions for entities</span></span>
<span data-ttu-id="6b24b-190">The following Data Factory entities are defined in the JSON template:</span><span class="sxs-lookup"><span data-stu-id="6b24b-190">The following Data Factory entities are defined in the JSON template:</span></span> 

- [<span data-ttu-id="6b24b-191">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="6b24b-191">Azure Storage linked service</span></span>](#azure-storage-linked-service)
- [<span data-ttu-id="6b24b-192">Azure blob input dataset</span><span class="sxs-lookup"><span data-stu-id="6b24b-192">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
- [<span data-ttu-id="6b24b-193">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="6b24b-193">Azure Blob output dataset</span></span>](#azure-blob-output-dataset)
- [<span data-ttu-id="6b24b-194">Data pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="6b24b-194">Data pipeline with a copy activity</span></span>](#data-pipeline)
- [<span data-ttu-id="6b24b-195">Trigger</span><span class="sxs-lookup"><span data-stu-id="6b24b-195">Trigger</span></span>](#trigger)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="6b24b-196">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="6b24b-196">Azure Storage linked service</span></span>
<span data-ttu-id="6b24b-197">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="6b24b-197">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="6b24b-198">You created a container and uploaded data to this storage account as part of prerequisites.</span><span class="sxs-lookup"><span data-stu-id="6b24b-198">You created a container and uploaded data to this storage account as part of prerequisites.</span></span> <span data-ttu-id="6b24b-199">You specify the name and key of your Azure storage account in this section.</span><span class="sxs-lookup"><span data-stu-id="6b24b-199">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="6b24b-200">See [Azure Storage linked service](connector-azure-blob-storage.md#linked-service-properties) for details about JSON properties used to define an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="6b24b-200">See [Azure Storage linked service](connector-azure-blob-storage.md#linked-service-properties) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[parameters('dataFactoryName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": {
                "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]",
                "type": "SecureString"
            }
        }
    }
}
```

<span data-ttu-id="6b24b-201">The connectionString uses the storageAccountName and storageAccountKey parameters.</span><span class="sxs-lookup"><span data-stu-id="6b24b-201">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="6b24b-202">The values for these parameters passed by using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="6b24b-202">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="6b24b-203">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span><span class="sxs-lookup"><span data-stu-id="6b24b-203">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="6b24b-204">Azure blob input dataset</span><span class="sxs-lookup"><span data-stu-id="6b24b-204">Azure blob input dataset</span></span>
<span data-ttu-id="6b24b-205">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="6b24b-205">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="6b24b-206">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="6b24b-206">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="6b24b-207">See [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="6b24b-207">See [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('inputDatasetName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'), '/')]",
        "fileName": "[parameters('inputBlobName')]"
    },
    "linkedServiceName": {
        "referenceName": "[variables('azureStorageLinkedServiceName')]",
        "type": "LinkedServiceReference"
    }
    }
},

```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="6b24b-208">Azure blob output dataset</span><span class="sxs-lookup"><span data-stu-id="6b24b-208">Azure blob output dataset</span></span>
<span data-ttu-id="6b24b-209">You specify the name of the folder in the Azure Blob Storage that holds the copied data from the input folder.</span><span class="sxs-lookup"><span data-stu-id="6b24b-209">You specify the name of the folder in the Azure Blob Storage that holds the copied data from the input folder.</span></span> <span data-ttu-id="6b24b-210">See [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="6b24b-210">See [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('outputDatasetName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'), '/')]",
        "fileName": "[parameters('outputBlobName')]"
    },
    "linkedServiceName": {
        "referenceName": "[variables('azureStorageLinkedServiceName')]",
        "type": "LinkedServiceReference"
    }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="6b24b-211">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="6b24b-211">Data pipeline</span></span>
<span data-ttu-id="6b24b-212">You define a pipeline that copies data from one Azure blob dataset to another Azure blob dataset.</span><span class="sxs-lookup"><span data-stu-id="6b24b-212">You define a pipeline that copies data from one Azure blob dataset to another Azure blob dataset.</span></span> <span data-ttu-id="6b24b-213">See [Pipeline JSON](concepts-pipelines-activities.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span><span class="sxs-lookup"><span data-stu-id="6b24b-213">See [Pipeline JSON](concepts-pipelines-activities.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "pipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]",
    "[variables('inputDatasetName')]",
    "[variables('outputDatasetName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "activities": [
        {
        "type": "Copy",
        "typeProperties": {
            "source": {
            "type": "BlobSource"
            },
            "sink": {
            "type": "BlobSink"
            }
        },
        "name": "MyCopyActivity",
        "inputs": [
            {
            "referenceName": "[variables('inputDatasetName')]",
            "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
            "referenceName": "[variables('outputDatasetName')]",
            "type": "DatasetReference"
            }
        ]
        }
    ]
    }
}
```

#### <a name="trigger"></a><span data-ttu-id="6b24b-214">Trigger</span><span class="sxs-lookup"><span data-stu-id="6b24b-214">Trigger</span></span>
<span data-ttu-id="6b24b-215">You define a trigger that runs the pipeline once an hour.</span><span class="sxs-lookup"><span data-stu-id="6b24b-215">You define a trigger that runs the pipeline once an hour.</span></span> <span data-ttu-id="6b24b-216">The deployed trigger is in stopped state.</span><span class="sxs-lookup"><span data-stu-id="6b24b-216">The deployed trigger is in stopped state.</span></span> <span data-ttu-id="6b24b-217">Start the trigger by using the **Start-AzureRmDataFactoryV2Trigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b24b-217">Start the trigger by using the **Start-AzureRmDataFactoryV2Trigger** cmdlet.</span></span> <span data-ttu-id="6b24b-218">For more information about triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md#triggers) article.</span><span class="sxs-lookup"><span data-stu-id="6b24b-218">For more information about triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md#triggers) article.</span></span> 

```json
{
    "type": "triggers",
    "name": "[variables('triggerName')]",
    "dependsOn": [
        "[parameters('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('inputDatasetName')]",
        "[variables('outputDatasetName')]",
        "[variables('pipelineName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
        "type": "ScheduleTrigger",
        "typeProperties": {
            "recurrence": {
                "frequency": "Hour",
                "interval": 1,
                "startTime": "2017-11-28T00:00:00",
                "endTime": "2017-11-29T00:00:00",
                "timeZone": "UTC"               
            }
        },
        "pipelines": [{
            "pipelineReference": {
                "type": "PipelineReference",
                "referenceName": "ArmtemplateSampleCopyPipeline"
            },
            "parameters": {}
        }]
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="6b24b-219">Reuse the template</span><span class="sxs-lookup"><span data-stu-id="6b24b-219">Reuse the template</span></span>
<span data-ttu-id="6b24b-220">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span><span class="sxs-lookup"><span data-stu-id="6b24b-220">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="6b24b-221">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span><span class="sxs-lookup"><span data-stu-id="6b24b-221">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="6b24b-222">Example:</span><span class="sxs-lookup"><span data-stu-id="6b24b-222">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="6b24b-223">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span><span class="sxs-lookup"><span data-stu-id="6b24b-223">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="6b24b-224">You can also reuse the template to perform repeated tasks.</span><span class="sxs-lookup"><span data-stu-id="6b24b-224">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="6b24b-225">For example, create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="6b24b-225">For example, create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage accounts.</span></span> <span data-ttu-id="6b24b-226">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span><span class="sxs-lookup"><span data-stu-id="6b24b-226">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="6b24b-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b24b-227">Next steps</span></span>
<span data-ttu-id="6b24b-228">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6b24b-228">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="6b24b-229">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span><span class="sxs-lookup"><span data-stu-id="6b24b-229">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span></span> 
