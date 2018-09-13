---
title: PowerShell script- transform data in cloud using Data Factory | Microsoft Docs
description: This PowerShell script transforms data in the cloud by running Spark program on an Azure HDInsight Spark cluster.
services: data-factory
author: sharonlo101
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2017
ms.author: shlo
ms.openlocfilehash: d885ffc531c24e8116da991f49ba5f8591e966d1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855702"
---
# <a name="powershell-script---transform-data-in-cloud-using-azure-data-factory"></a><span data-ttu-id="1f8cf-103">PowerShell script - transform data in cloud using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1f8cf-103">PowerShell script - transform data in cloud using Azure Data Factory</span></span>

<span data-ttu-id="1f8cf-104">This sample PowerShell script creates a pipeline that transforms data in the cloud by running Spark program on an Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-104">This sample PowerShell script creates a pipeline that transforms data in the cloud by running Spark program on an Azure HDInsight Spark cluster.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="1f8cf-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f8cf-105">Prerequisites</span></span>
* <span data-ttu-id="1f8cf-106">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-106">**Azure Storage account**.</span></span> <span data-ttu-id="1f8cf-107">Create a python script and an input file, and upload them to the Azure storage.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-107">Create a python script and an input file, and upload them to the Azure storage.</span></span> <span data-ttu-id="1f8cf-108">The output from the spark program is stored in this storage account.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-108">The output from the spark program is stored in this storage account.</span></span> <span data-ttu-id="1f8cf-109">The on-demand Spark cluster uses the same storage account as its primary storage.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-109">The on-demand Spark cluster uses the same storage account as its primary storage.</span></span>  

### <a name="upload-python-script-to-your-blob-storage-account"></a><span data-ttu-id="1f8cf-110">Upload python script to your Blob Storage account</span><span class="sxs-lookup"><span data-stu-id="1f8cf-110">Upload python script to your Blob Storage account</span></span>
1. <span data-ttu-id="1f8cf-111">Create a python file named **WordCount_Spark.py** with the following content:</span><span class="sxs-lookup"><span data-stu-id="1f8cf-111">Create a python file named **WordCount_Spark.py** with the following content:</span></span> 

    ```python
    import sys
    from operator import add
    
    from pyspark.sql import SparkSession
    
    def main():
        spark = SparkSession\
            .builder\
            .appName("PythonWordCount")\
            .getOrCreate()
            
        lines = spark.read.text("wasbs://adftutorial@<storageaccountname>.blob.core.windows.net/spark/inputfiles/minecraftstory.txt").rdd.map(lambda r: r[0])
        counts = lines.flatMap(lambda x: x.split(' ')) \
            .map(lambda x: (x, 1)) \
            .reduceByKey(add)
        counts.saveAsTextFile("wasbs://adftutorial@<storageaccountname>.blob.core.windows.net/spark/outputfiles/wordcount")
        
        spark.stop()
    
    if __name__ == "__main__":
        main()
    ```
2. <span data-ttu-id="1f8cf-112">Replace **&lt;storageAccountName&gt;** with the name of your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-112">Replace **&lt;storageAccountName&gt;** with the name of your Azure Storage account.</span></span> <span data-ttu-id="1f8cf-113">Then, save the file.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-113">Then, save the file.</span></span> 
3. <span data-ttu-id="1f8cf-114">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-114">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span></span> 
4. <span data-ttu-id="1f8cf-115">Create a folder named **spark**.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-115">Create a folder named **spark**.</span></span>
5. <span data-ttu-id="1f8cf-116">Create a subfolder named **script** under **spark** folder.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-116">Create a subfolder named **script** under **spark** folder.</span></span> 
6. <span data-ttu-id="1f8cf-117">Upload the **WordCount_Spark.py** file to the **script** subfolder.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-117">Upload the **WordCount_Spark.py** file to the **script** subfolder.</span></span> 


### <a name="upload-the-input-file"></a><span data-ttu-id="1f8cf-118">Upload the input file</span><span class="sxs-lookup"><span data-stu-id="1f8cf-118">Upload the input file</span></span>
1. <span data-ttu-id="1f8cf-119">Create a file named **minecraftstory.txt** with some text.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-119">Create a file named **minecraftstory.txt** with some text.</span></span> <span data-ttu-id="1f8cf-120">The spark program counts the number of words in this text.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-120">The spark program counts the number of words in this text.</span></span> 
2. <span data-ttu-id="1f8cf-121">Create a subfolder named `inputfiles` in the `spark` folder of the blob container.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-121">Create a subfolder named `inputfiles` in the `spark` folder of the blob container.</span></span> 
3. <span data-ttu-id="1f8cf-122">Upload the `minecraftstory.txt` to the `inputfiles` subfolder.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-122">Upload the `minecraftstory.txt` to the `inputfiles` subfolder.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1f8cf-123">Sample script</span><span class="sxs-lookup"><span data-stu-id="1f8cf-123">Sample script</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1f8cf-124">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-124">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span></span>

[!code-powershell[main](../../../powershell_scripts/data-factory/transform-data-using-spark/transform-data-using-spark.ps1 "Transform data using Spark")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1f8cf-125">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1f8cf-125">Clean up deployment</span></span>

<span data-ttu-id="1f8cf-126">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="1f8cf-126">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="1f8cf-127">To remove the data factory from the resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="1f8cf-127">To remove the data factory from the resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="1f8cf-128">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1f8cf-128">Script explanation</span></span>

<span data-ttu-id="1f8cf-129">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="1f8cf-129">This script uses the following commands:</span></span>

| <span data-ttu-id="1f8cf-130">Command</span><span class="sxs-lookup"><span data-stu-id="1f8cf-130">Command</span></span> | <span data-ttu-id="1f8cf-131">Notes</span><span class="sxs-lookup"><span data-stu-id="1f8cf-131">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1f8cf-132">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f8cf-132">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1f8cf-133">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-133">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1f8cf-134">Set-AzureRmDataFactoryV2</span><span class="sxs-lookup"><span data-stu-id="1f8cf-134">Set-AzureRmDataFactoryV2</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2) | <span data-ttu-id="1f8cf-135">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-135">Create a data factory.</span></span> |
| [<span data-ttu-id="1f8cf-136">Set-AzureRmDataFactoryV2LinkedService</span><span class="sxs-lookup"><span data-stu-id="1f8cf-136">Set-AzureRmDataFactoryV2LinkedService</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2linkedservice) | <span data-ttu-id="1f8cf-137">Creates a linked service in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-137">Creates a linked service in the data factory.</span></span> <span data-ttu-id="1f8cf-138">A linked service links a data store or compute to a data factory.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-138">A linked service links a data store or compute to a data factory.</span></span> |
| [<span data-ttu-id="1f8cf-139">Set-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="1f8cf-139">Set-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2pipeline) | <span data-ttu-id="1f8cf-140">Creates a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-140">Creates a pipeline in the data factory.</span></span> <span data-ttu-id="1f8cf-141">A pipeline contains one or more activities that performs a certain operation.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-141">A pipeline contains one or more activities that performs a certain operation.</span></span> <span data-ttu-id="1f8cf-142">In this pipeline, a spark activity transforms data by running a program on an Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-142">In this pipeline, a spark activity transforms data by running a program on an Azure HDInsight Spark cluster.</span></span> |
| [<span data-ttu-id="1f8cf-143">Invoke-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="1f8cf-143">Invoke-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/invoke-azurermdatafactoryv2pipeline) | <span data-ttu-id="1f8cf-144">Creates a run for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-144">Creates a run for the pipeline.</span></span> <span data-ttu-id="1f8cf-145">In other words, runs the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-145">In other words, runs the pipeline.</span></span> |
| [<span data-ttu-id="1f8cf-146">Get-AzureRmDataFactoryV2ActivityRun</span><span class="sxs-lookup"><span data-stu-id="1f8cf-146">Get-AzureRmDataFactoryV2ActivityRun</span></span>](/powershell/module/azurerm.datafactoryv2/get-azurermdatafactoryv2activityrun) | <span data-ttu-id="1f8cf-147">Gets details about the run of the activity (activity run) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-147">Gets details about the run of the activity (activity run) in the pipeline.</span></span> 
| [<span data-ttu-id="1f8cf-148">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f8cf-148">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1f8cf-149">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="1f8cf-149">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1f8cf-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f8cf-150">Next steps</span></span>

<span data-ttu-id="1f8cf-151">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="1f8cf-151">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="1f8cf-152">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1f8cf-152">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span></span>
