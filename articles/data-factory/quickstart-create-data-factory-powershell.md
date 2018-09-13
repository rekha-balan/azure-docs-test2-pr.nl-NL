---
title: Copy data in Blob Storage using Azure Data Factory | Microsoft Docs
description: Create an Azure data factory to copy data from one location in Azure Blob storage to another location.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: quickstart
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 04fd3be1bde6f640e5966b445ff2aeb8f3c27458
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866725"
---
# <a name="create-an-azure-data-factory-using-powershell"></a><span data-ttu-id="9e248-103">Create an Azure data factory using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e248-103">Create an Azure data factory using PowerShell</span></span> 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](quickstart-create-data-factory-powershell.md)

<span data-ttu-id="9e248-106">This quickstart describes how to use PowerShell to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="9e248-106">This quickstart describes how to use PowerShell to create an Azure data factory.</span></span> <span data-ttu-id="9e248-107">The pipeline you create in this data factory **copies** data from one folder to another folder in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="9e248-107">The pipeline you create in this data factory **copies** data from one folder to another folder in an Azure blob storage.</span></span> <span data-ttu-id="9e248-108">For a tutorial on how to **transform** data using Azure Data Factory, see [Tutorial: Transform data using Spark](transform-data-using-spark.md).</span><span class="sxs-lookup"><span data-stu-id="9e248-108">For a tutorial on how to **transform** data using Azure Data Factory, see [Tutorial: Transform data using Spark](transform-data-using-spark.md).</span></span> 

> [!NOTE]
> This article does not provide a detailed introduction of the Data Factory service. For an introduction to the Azure Data Factory service, see [Introduction to Azure Data Factory](introduction.md).

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

### <a name="azure-powershell"></a><span data-ttu-id="9e248-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e248-111">Azure PowerShell</span></span>
<span data-ttu-id="9e248-112">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9e248-112">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

#### <a name="log-in-to-powershell"></a><span data-ttu-id="9e248-113">Log in to PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e248-113">Log in to PowerShell</span></span>

1. <span data-ttu-id="9e248-114">Launch **PowerShell** on your machine.</span><span class="sxs-lookup"><span data-stu-id="9e248-114">Launch **PowerShell** on your machine.</span></span> <span data-ttu-id="9e248-115">Keep PowerShell open until the end of this quickstart.</span><span class="sxs-lookup"><span data-stu-id="9e248-115">Keep PowerShell open until the end of this quickstart.</span></span> <span data-ttu-id="9e248-116">If you close and reopen, you need to run these commands again.</span><span class="sxs-lookup"><span data-stu-id="9e248-116">If you close and reopen, you need to run these commands again.</span></span>
2. <span data-ttu-id="9e248-117">Run the following command, and enter the same Azure user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="9e248-117">Run the following command, and enter the same Azure user name and password that you use to sign in to the Azure portal:</span></span>
       
    ```powershell
    Connect-AzureRmAccount
    ```        
3. <span data-ttu-id="9e248-118">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="9e248-118">Run the following command to view all the subscriptions for this account:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="9e248-119">If you see multiple subscriptions associated with your account, run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="9e248-119">If you see multiple subscriptions associated with your account, run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="9e248-120">Replace **SubscriptionId** with the ID of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="9e248-120">Replace **SubscriptionId** with the ID of your Azure subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```

## <a name="create-a-data-factory"></a><span data-ttu-id="9e248-121">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="9e248-121">Create a data factory</span></span>
1. <span data-ttu-id="9e248-122">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="9e248-122">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="9e248-123">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="9e248-123">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span></span> <span data-ttu-id="9e248-124">For example: `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="9e248-124">For example: `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFQuickStartRG";
    ```

    <span data-ttu-id="9e248-125">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="9e248-125">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="9e248-126">Assign a different value to the `$ResourceGroupName` variable and run the command again</span><span class="sxs-lookup"><span data-stu-id="9e248-126">Assign a different value to the `$ResourceGroupName` variable and run the command again</span></span>
2. <span data-ttu-id="9e248-127">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="9e248-127">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    $ResGrp = New-AzureRmResourceGroup $resourceGroupName -location 'East US'
    ``` 
    <span data-ttu-id="9e248-128">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="9e248-128">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="9e248-129">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span><span class="sxs-lookup"><span data-stu-id="9e248-129">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span></span> 
3. <span data-ttu-id="9e248-130">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="9e248-130">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  Update the data factory name to be globally unique. For example, ADFTutorialFactorySP1127. 

    ```powershell
    $dataFactoryName = "ADFQuickStartFactory";
    ```

5. <span data-ttu-id="9e248-133">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span><span class="sxs-lookup"><span data-stu-id="9e248-133">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span></span> 
    
    ```powershell       
    $DataFactory = Set-AzureRmDataFactoryV2 -ResourceGroupName $ResGrp.ResourceGroupName -Location $ResGrp.Location -Name $dataFactoryName 
    ```

<span data-ttu-id="9e248-134">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="9e248-134">Note the following points:</span></span>

* <span data-ttu-id="9e248-135">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="9e248-135">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="9e248-136">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="9e248-136">If you receive the following error, change the name and try again.</span></span>

    ```
    The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
    ```
* <span data-ttu-id="9e248-137">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9e248-137">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span></span>
* <span data-ttu-id="9e248-138">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="9e248-138">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="9e248-139">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="9e248-139">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

## <a name="create-a-linked-service"></a><span data-ttu-id="9e248-140">Create a linked service</span><span class="sxs-lookup"><span data-stu-id="9e248-140">Create a linked service</span></span>

<span data-ttu-id="9e248-141">Create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="9e248-141">Create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="9e248-142">In this quickstart, you create an Azure Storage linked service that is used as both the source and sink stores.</span><span class="sxs-lookup"><span data-stu-id="9e248-142">In this quickstart, you create an Azure Storage linked service that is used as both the source and sink stores.</span></span> <span data-ttu-id="9e248-143">The linked service has the connection information that the Data Factory service uses at runtime to connect to it.</span><span class="sxs-lookup"><span data-stu-id="9e248-143">The linked service has the connection information that the Data Factory service uses at runtime to connect to it.</span></span>

1. <span data-ttu-id="9e248-144">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFv2QuickStartPSH** folder with the following content: (Create the folder ADFv2QuickStartPSH if it does not already exist.).</span><span class="sxs-lookup"><span data-stu-id="9e248-144">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFv2QuickStartPSH** folder with the following content: (Create the folder ADFv2QuickStartPSH if it does not already exist.).</span></span> 

    > [!IMPORTANT]
    > Replace &lt;accountName&gt; and &lt;accountKey&gt; with name and key of your Azure storage account before saving the file.

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>;EndpointSuffix=core.windows.net",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
    <span data-ttu-id="9e248-146">If you are using Notepad, select **All files** for the **Save as type** filed in the **Save as** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9e248-146">If you are using Notepad, select **All files** for the **Save as type** filed in the **Save as** dialog box.</span></span> <span data-ttu-id="9e248-147">Otherwise, it may add `.txt` extension to the file.</span><span class="sxs-lookup"><span data-stu-id="9e248-147">Otherwise, it may add `.txt` extension to the file.</span></span> <span data-ttu-id="9e248-148">For example, `AzureStorageLinkedService.json.txt`.</span><span class="sxs-lookup"><span data-stu-id="9e248-148">For example, `AzureStorageLinkedService.json.txt`.</span></span> <span data-ttu-id="9e248-149">If you create the file in File Explorer before opening it in Notepad, you may not see the `.txt` extension since the **Hide extensions for known files types** option is set by default.</span><span class="sxs-lookup"><span data-stu-id="9e248-149">If you create the file in File Explorer before opening it in Notepad, you may not see the `.txt` extension since the **Hide extensions for known files types** option is set by default.</span></span> <span data-ttu-id="9e248-150">Remove the `.txt` extension before proceeding to the next step.</span><span class="sxs-lookup"><span data-stu-id="9e248-150">Remove the `.txt` extension before proceeding to the next step.</span></span>
2. <span data-ttu-id="9e248-151">In **PowerShell**, switch to the **ADFv2QuickStartPSH** folder.</span><span class="sxs-lookup"><span data-stu-id="9e248-151">In **PowerShell**, switch to the **ADFv2QuickStartPSH** folder.</span></span>

    ```powershell
    Set-Location 'C:\ADFv2QuickStartPSH'
    ```
3. <span data-ttu-id="9e248-152">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="9e248-152">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -Name "AzureStorageLinkedService" -DefinitionFile ".\AzureStorageLinkedService.json"
    ```

    <span data-ttu-id="9e248-153">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="9e248-153">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

## <a name="create-a-dataset"></a><span data-ttu-id="9e248-154">Create a dataset</span><span class="sxs-lookup"><span data-stu-id="9e248-154">Create a dataset</span></span>
<span data-ttu-id="9e248-155">In this step, you define a dataset that represents the data to copy from a source to a sink.</span><span class="sxs-lookup"><span data-stu-id="9e248-155">In this step, you define a dataset that represents the data to copy from a source to a sink.</span></span> <span data-ttu-id="9e248-156">The dataset is of type **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="9e248-156">The dataset is of type **AzureBlob**.</span></span> <span data-ttu-id="9e248-157">It refers to the **Azure Storage linked service** you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9e248-157">It refers to the **Azure Storage linked service** you created in the previous step.</span></span> <span data-ttu-id="9e248-158">It takes a parameter to construct the **folderPath** property.</span><span class="sxs-lookup"><span data-stu-id="9e248-158">It takes a parameter to construct the **folderPath** property.</span></span> <span data-ttu-id="9e248-159">For an input dataset, the copy activity in the pipeline passes the input path as a value for this parameter.</span><span class="sxs-lookup"><span data-stu-id="9e248-159">For an input dataset, the copy activity in the pipeline passes the input path as a value for this parameter.</span></span> <span data-ttu-id="9e248-160">Similarly, for an output dataset, the copy activity passes the output path as a value for this parameter.</span><span class="sxs-lookup"><span data-stu-id="9e248-160">Similarly, for an output dataset, the copy activity passes the output path as a value for this parameter.</span></span> 

1. <span data-ttu-id="9e248-161">Create a JSON file named **BlobDataset.json** in the **C:\ADFv2QuickStartPSH** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="9e248-161">Create a JSON file named **BlobDataset.json** in the **C:\ADFv2QuickStartPSH** folder, with the following content:</span></span>

    ```json
    {
        "name": "BlobDataset",
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "@{dataset().path}"
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            },
            "parameters": {
                "path": {
                    "type": "String"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="9e248-162">To create the dataset: **BlobDataset**, run the **Set-AzureRmDataFactoryV2Dataset** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9e248-162">To create the dataset: **BlobDataset**, run the **Set-AzureRmDataFactoryV2Dataset** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -Name "BlobDataset" -DefinitionFile ".\BlobDataset.json"
    ```

    <span data-ttu-id="9e248-163">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="9e248-163">Here is the sample output:</span></span>

    ```
    DatasetName       : BlobDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="9e248-164">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="9e248-164">Create a pipeline</span></span>
  
<span data-ttu-id="9e248-165">In this quickstart, you create a pipeline with one activity that takes two parameters - input blob path and output blob path.</span><span class="sxs-lookup"><span data-stu-id="9e248-165">In this quickstart, you create a pipeline with one activity that takes two parameters - input blob path and output blob path.</span></span> <span data-ttu-id="9e248-166">The values for these parameters are set when the pipeline is triggered/run.</span><span class="sxs-lookup"><span data-stu-id="9e248-166">The values for these parameters are set when the pipeline is triggered/run.</span></span> <span data-ttu-id="9e248-167">The copy activity uses the same blob dataset created in the previous step as input and output.</span><span class="sxs-lookup"><span data-stu-id="9e248-167">The copy activity uses the same blob dataset created in the previous step as input and output.</span></span> <span data-ttu-id="9e248-168">When the dataset is used as an input dataset, input path is specified.</span><span class="sxs-lookup"><span data-stu-id="9e248-168">When the dataset is used as an input dataset, input path is specified.</span></span> <span data-ttu-id="9e248-169">And, when the dataset is used as an output dataset, the output path is specified.</span><span class="sxs-lookup"><span data-stu-id="9e248-169">And, when the dataset is used as an output dataset, the output path is specified.</span></span> 

1. <span data-ttu-id="9e248-170">Create a JSON file named **Adfv2QuickStartPipeline.json** in the **C:\ADFv2QuickStartPSH** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="9e248-170">Create a JSON file named **Adfv2QuickStartPipeline.json** in the **C:\ADFv2QuickStartPSH** folder with the following content:</span></span>

    ```json
    {
        "name": "Adfv2QuickStartPipeline",
        "properties": {
            "activities": [
                {
                    "name": "CopyFromBlobToBlob",
                    "type": "Copy",
                    "inputs": [
                        {
                            "referenceName": "BlobDataset",
                            "parameters": {
                                "path": "@pipeline().parameters.inputPath"
                            },
                            "type": "DatasetReference"
                        }
                    ],
                    "outputs": [
                        {
                            "referenceName": "BlobDataset",
                            "parameters": {
                                "path": "@pipeline().parameters.outputPath"
                            },
                            "type": "DatasetReference"
                        }
                    ],
                    "typeProperties": {
                        "source": {
                            "type": "BlobSource"
                        },
                        "sink": {
                            "type": "BlobSink"
                        }
                    }
                }
            ],
            "parameters": {
                "inputPath": {
                    "type": "String"
                },
                "outputPath": {
                    "type": "String"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="9e248-171">To create the pipeline: **Adfv2QuickStartPipeline**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9e248-171">To create the pipeline: **Adfv2QuickStartPipeline**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span>

    ```powershell
    $DFPipeLine = Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -Name "Adfv2QuickStartPipeline" -DefinitionFile ".\Adfv2QuickStartPipeline.json"
    ```

    <span data-ttu-id="9e248-172">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="9e248-172">Here is the sample output:</span></span>

    ```
    PipelineName      : Adfv2QuickStartPipeline
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {CopyFromBlobToBlob}
    Parameters        : {[inputPath, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification], [outputPath, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
    ```

## <a name="create-a-pipeline-run"></a><span data-ttu-id="9e248-173">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="9e248-173">Create a pipeline run</span></span>

<span data-ttu-id="9e248-174">In this step, you set values for the pipeline parameters:  **inputPath** and **outputPath** with actual values of source and sink blob paths.</span><span class="sxs-lookup"><span data-stu-id="9e248-174">In this step, you set values for the pipeline parameters:  **inputPath** and **outputPath** with actual values of source and sink blob paths.</span></span> <span data-ttu-id="9e248-175">Then, you create a pipeline run by using these arguments.</span><span class="sxs-lookup"><span data-stu-id="9e248-175">Then, you create a pipeline run by using these arguments.</span></span> 

1. <span data-ttu-id="9e248-176">Create a JSON file named **PipelineParameters.json** in the **C:\ADFv2QuickStartPSH** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="9e248-176">Create a JSON file named **PipelineParameters.json** in the **C:\ADFv2QuickStartPSH** folder with the following content:</span></span>

    ```json
    {
        "inputPath": "adftutorial/input",
        "outputPath": "adftutorial/output"
    }
    ```
2. <span data-ttu-id="9e248-177">Run the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet to create a pipeline run and pass in the parameter values.</span><span class="sxs-lookup"><span data-stu-id="9e248-177">Run the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet to create a pipeline run and pass in the parameter values.</span></span> <span data-ttu-id="9e248-178">The cmdlet returns the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="9e248-178">The cmdlet returns the pipeline run ID for future monitoring.</span></span>

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -PipelineName $DFPipeLine.Name -ParameterFile .\PipelineParameters.json
    ```

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="9e248-179">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="9e248-179">Monitor the pipeline run</span></span>

1. <span data-ttu-id="9e248-180">Run the following PowerShell script to continuously check the pipeline run status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="9e248-180">Run the following PowerShell script to continuously check the pipeline run status until it finishes copying the data.</span></span> <span data-ttu-id="9e248-181">Copy/paste the following script in the PowerShell window, and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="9e248-181">Copy/paste the following script in the PowerShell window, and press ENTER.</span></span> 

    ```powershell
    while ($True) {
        $Run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $ResGrp.ResourceGroupName -DataFactoryName $DataFactory.DataFactoryName -PipelineRunId $RunId

        if ($Run) {
            if ($run.Status -ne 'InProgress') {
                Write-Output ("Pipeline run finished. The status is: " +  $Run.Status)
                $Run
                break
            }
            Write-Output  "Pipeline is running...status: InProgress"
        }

        Start-Sleep -Seconds 10
    }   
    ```

    <span data-ttu-id="9e248-182">Here is the sample output of pipeline run:</span><span class="sxs-lookup"><span data-stu-id="9e248-182">Here is the sample output of pipeline run:</span></span>

    ```
    Pipeline is running...status: InProgress
    Pipeline run finished. The status is:  Succeeded
    
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : SPTestFactory0928
    RunId             : 0000000000-0000-0000-0000-0000000000000
    PipelineName      : Adfv2QuickStartPipeline
    LastUpdated       : 9/28/2017 8:28:38 PM
    Parameters        : {[inputPath, adftutorial/input], [outputPath, adftutorial/output]}
    RunStart          : 9/28/2017 8:28:14 PM
    RunEnd            : 9/28/2017 8:28:38 PM
    DurationInMs      : 24151
    Status            : Succeeded
    Message           :
    ```

    <span data-ttu-id="9e248-183">If you see the error:</span><span class="sxs-lookup"><span data-stu-id="9e248-183">If you see the error:</span></span>
    ```
    Activity CopyFromBlobToBlob failed: Failed to detect region of linked service 'AzureStorage' : 'AzureStorageLinkedService' with error '[Region Resolver] Azure Storage failed to get address for DNS. Warning: System.Net.Sockets.SocketException (0x80004005): No such host is known
    ```
    <span data-ttu-id="9e248-184">do the following steps:</span><span class="sxs-lookup"><span data-stu-id="9e248-184">do the following steps:</span></span> 
    1. <span data-ttu-id="9e248-185">In the AzureStorageLinkedService.json, confirm that the name and key of your Azure Storage Account are correct.</span><span class="sxs-lookup"><span data-stu-id="9e248-185">In the AzureStorageLinkedService.json, confirm that the name and key of your Azure Storage Account are correct.</span></span> 
    2. <span data-ttu-id="9e248-186">Verify that the format of the connection string is correct.</span><span class="sxs-lookup"><span data-stu-id="9e248-186">Verify that the format of the connection string is correct.</span></span> <span data-ttu-id="9e248-187">The properties, for example, AccountName and AccountKey are separated by semi-colon (`;`) character.</span><span class="sxs-lookup"><span data-stu-id="9e248-187">The properties, for example, AccountName and AccountKey are separated by semi-colon (`;`) character.</span></span> 
    3. <span data-ttu-id="9e248-188">If you have angled brackets surrounding the account name and account key, remove them.</span><span class="sxs-lookup"><span data-stu-id="9e248-188">If you have angled brackets surrounding the account name and account key, remove them.</span></span> 
    4. <span data-ttu-id="9e248-189">Here is an example connection string:</span><span class="sxs-lookup"><span data-stu-id="9e248-189">Here is an example connection string:</span></span> 

        ```json
        "connectionString": {
            "value": "DefaultEndpointsProtocol=https;AccountName=mystorageaccountname;AccountKey=mystorageacountkey;EndpointSuffix=core.windows.net",
            "type": "SecureString"
        }
        ```
    5. <span data-ttu-id="9e248-190">Recreate the linked service by following steps in the [Create a linked service](#create-a-linked-service) section.</span><span class="sxs-lookup"><span data-stu-id="9e248-190">Recreate the linked service by following steps in the [Create a linked service](#create-a-linked-service) section.</span></span> 
    6. <span data-ttu-id="9e248-191">Rerun the pipeline by following steps in the [Create a pipeline run](#create-a-pipeline-run) section.</span><span class="sxs-lookup"><span data-stu-id="9e248-191">Rerun the pipeline by following steps in the [Create a pipeline run](#create-a-pipeline-run) section.</span></span> 
    7. <span data-ttu-id="9e248-192">Run the current monitoring command again to monitor the new pipeline run.</span><span class="sxs-lookup"><span data-stu-id="9e248-192">Run the current monitoring command again to monitor the new pipeline run.</span></span> 
1. <span data-ttu-id="9e248-193">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="9e248-193">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span></span>

    ```powershell
    Write-Output "Activity run details:"
    $Result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -PipelineRunId $RunId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    $Result

    Write-Output "Activity 'Output' section:"
    $Result.Output -join "`r`n"

    Write-Output "Activity 'Error' section:"
    $Result.Error -join "`r`n"
    ```
3. <span data-ttu-id="9e248-194">Confirm that you see the output similar to the following sample output of activity run result:</span><span class="sxs-lookup"><span data-stu-id="9e248-194">Confirm that you see the output similar to the following sample output of activity run result:</span></span>

    ```json
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : SPTestFactory0928
    ActivityName      : CopyFromBlobToBlob
    PipelineRunId     : 00000000000-0000-0000-0000-000000000000
    PipelineName      : Adfv2QuickStartPipeline
    Input             : {source, sink}
    Output            : {dataRead, dataWritten, copyDuration, throughput...}
    LinkedServiceName :
    ActivityRunStart  : 9/28/2017 8:28:18 PM
    ActivityRunEnd    : 9/28/2017 8:28:36 PM
    DurationInMs      : 18095
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    Activity 'Output' section:
    "dataRead": 38
    "dataWritten": 38
    "copyDuration": 7
    "throughput": 0.01
    "errors": []
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (West US)"
    "usedDataIntegrationUnits": 2
    "billedDuration": 14
    ```

[!INCLUDE [data-factory-quickstart-verify-output-cleanup.md](../../includes/data-factory-quickstart-verify-output-cleanup.md)] 

## <a name="next-steps"></a><span data-ttu-id="9e248-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e248-195">Next steps</span></span>
<span data-ttu-id="9e248-196">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="9e248-196">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="9e248-197">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span><span class="sxs-lookup"><span data-stu-id="9e248-197">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span></span> 
