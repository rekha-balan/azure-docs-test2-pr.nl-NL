---
title: Transform data using Spark in Azure Data Factory | Microsoft Docs
description: This tutorial provides step-by-step instructions for transforming data by using Spark Activity in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: douglasl
ms.openlocfilehash: c01da1b667f5a57e9597b77e21dcd9cc95340cb1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857917"
---
# <a name="transform-data-in-the-cloud-by-using-spark-activity-in-azure-data-factory"></a><span data-ttu-id="302ab-103">Transform data in the cloud by using Spark activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="302ab-103">Transform data in the cloud by using Spark activity in Azure Data Factory</span></span>
<span data-ttu-id="302ab-104">In this tutorial, you use Azure PowerShell to create a Data Factory pipeline that transforms data using Spark Activity and an on-demand HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="302ab-104">In this tutorial, you use Azure PowerShell to create a Data Factory pipeline that transforms data using Spark Activity and an on-demand HDInsight linked service.</span></span> <span data-ttu-id="302ab-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="302ab-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="302ab-106">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="302ab-106">Create a data factory.</span></span> 
> * <span data-ttu-id="302ab-107">Author and deploy linked services.</span><span class="sxs-lookup"><span data-stu-id="302ab-107">Author and deploy linked services.</span></span>
> * <span data-ttu-id="302ab-108">Author and deploy a pipeline.</span><span class="sxs-lookup"><span data-stu-id="302ab-108">Author and deploy a pipeline.</span></span> 
> * <span data-ttu-id="302ab-109">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="302ab-109">Start a pipeline run.</span></span>
> * <span data-ttu-id="302ab-110">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="302ab-110">Monitor the pipeline run.</span></span>

<span data-ttu-id="302ab-111">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="302ab-111">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="302ab-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="302ab-112">Prerequisites</span></span>
* <span data-ttu-id="302ab-113">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="302ab-113">**Azure Storage account**.</span></span> <span data-ttu-id="302ab-114">You create a python script and an input file, and upload them to the Azure storage.</span><span class="sxs-lookup"><span data-stu-id="302ab-114">You create a python script and an input file, and upload them to the Azure storage.</span></span> <span data-ttu-id="302ab-115">The output from the spark program is stored in this storage account.</span><span class="sxs-lookup"><span data-stu-id="302ab-115">The output from the spark program is stored in this storage account.</span></span> <span data-ttu-id="302ab-116">The on-demand Spark cluster uses the same storage account as its primary storage.</span><span class="sxs-lookup"><span data-stu-id="302ab-116">The on-demand Spark cluster uses the same storage account as its primary storage.</span></span>  
* <span data-ttu-id="302ab-117">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="302ab-117">**Azure PowerShell**.</span></span> <span data-ttu-id="302ab-118">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="302ab-118">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>


### <a name="upload-python-script-to-your-blob-storage-account"></a><span data-ttu-id="302ab-119">Upload python script to your Blob Storage account</span><span class="sxs-lookup"><span data-stu-id="302ab-119">Upload python script to your Blob Storage account</span></span>
1. <span data-ttu-id="302ab-120">Create a python file named **WordCount_Spark.py** with the following content:</span><span class="sxs-lookup"><span data-stu-id="302ab-120">Create a python file named **WordCount_Spark.py** with the following content:</span></span> 

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
2. <span data-ttu-id="302ab-121">Replace **&lt;storageAccountName&gt;** with the name of your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="302ab-121">Replace **&lt;storageAccountName&gt;** with the name of your Azure Storage account.</span></span> <span data-ttu-id="302ab-122">Then, save the file.</span><span class="sxs-lookup"><span data-stu-id="302ab-122">Then, save the file.</span></span> 
3. <span data-ttu-id="302ab-123">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="302ab-123">In your Azure Blob Storage, create a container named **adftutorial** if it does not exist.</span></span> 
4. <span data-ttu-id="302ab-124">Create a folder named **spark**.</span><span class="sxs-lookup"><span data-stu-id="302ab-124">Create a folder named **spark**.</span></span>
5. <span data-ttu-id="302ab-125">Create a subfolder named **script** under **spark** folder.</span><span class="sxs-lookup"><span data-stu-id="302ab-125">Create a subfolder named **script** under **spark** folder.</span></span> 
6. <span data-ttu-id="302ab-126">Upload the **WordCount_Spark.py** file to the **script** subfolder.</span><span class="sxs-lookup"><span data-stu-id="302ab-126">Upload the **WordCount_Spark.py** file to the **script** subfolder.</span></span> 


### <a name="upload-the-input-file"></a><span data-ttu-id="302ab-127">Upload the input file</span><span class="sxs-lookup"><span data-stu-id="302ab-127">Upload the input file</span></span>
1. <span data-ttu-id="302ab-128">Create a file named **minecraftstory.txt** with some text.</span><span class="sxs-lookup"><span data-stu-id="302ab-128">Create a file named **minecraftstory.txt** with some text.</span></span> <span data-ttu-id="302ab-129">The spark program counts the number of words in this text.</span><span class="sxs-lookup"><span data-stu-id="302ab-129">The spark program counts the number of words in this text.</span></span> 
2. <span data-ttu-id="302ab-130">Create a subfolder named `inputfiles` in the `spark` folder.</span><span class="sxs-lookup"><span data-stu-id="302ab-130">Create a subfolder named `inputfiles` in the `spark` folder.</span></span> 
3. <span data-ttu-id="302ab-131">Upload the `minecraftstory.txt` to the `inputfiles` subfolder.</span><span class="sxs-lookup"><span data-stu-id="302ab-131">Upload the `minecraftstory.txt` to the `inputfiles` subfolder.</span></span> 

## <a name="author-linked-services"></a><span data-ttu-id="302ab-132">Author linked services</span><span class="sxs-lookup"><span data-stu-id="302ab-132">Author linked services</span></span>
<span data-ttu-id="302ab-133">You author two Linked Services in this section:</span><span class="sxs-lookup"><span data-stu-id="302ab-133">You author two Linked Services in this section:</span></span> 
    
- <span data-ttu-id="302ab-134">An Azure Storage Linked Service that links an Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="302ab-134">An Azure Storage Linked Service that links an Azure Storage account to the data factory.</span></span> <span data-ttu-id="302ab-135">This storage is used by the on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="302ab-135">This storage is used by the on-demand HDInsight cluster.</span></span> <span data-ttu-id="302ab-136">It also contains the Spark script to be executed.</span><span class="sxs-lookup"><span data-stu-id="302ab-136">It also contains the Spark script to be executed.</span></span> 
- <span data-ttu-id="302ab-137">An On-Demand HDInsight Linked Service.</span><span class="sxs-lookup"><span data-stu-id="302ab-137">An On-Demand HDInsight Linked Service.</span></span> <span data-ttu-id="302ab-138">Azure Data Factory automatically creates a HDInsight cluster, run the Spark program, and then deletes the HDInsight cluster after it's idle for a pre-configured time.</span><span class="sxs-lookup"><span data-stu-id="302ab-138">Azure Data Factory automatically creates a HDInsight cluster, run the Spark program, and then deletes the HDInsight cluster after it's idle for a pre-configured time.</span></span> 

### <a name="azure-storage-linked-service"></a><span data-ttu-id="302ab-139">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="302ab-139">Azure Storage linked service</span></span>
<span data-ttu-id="302ab-140">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure Storage linked service, and then save the file as **MyStorageLinkedService.json**.</span><span class="sxs-lookup"><span data-stu-id="302ab-140">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure Storage linked service, and then save the file as **MyStorageLinkedService.json**.</span></span>  

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
          "type": "SecureString"
        }
      }
    }
}
```
<span data-ttu-id="302ab-141">Update the &lt;storageAccountName&gt; and &lt;storageAccountKey&gt; with the name and key of your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="302ab-141">Update the &lt;storageAccountName&gt; and &lt;storageAccountKey&gt; with the name and key of your Azure Storage account.</span></span> 


### <a name="on-demand-hdinsight-linked-service"></a><span data-ttu-id="302ab-142">On-demand HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="302ab-142">On-demand HDInsight linked service</span></span>
<span data-ttu-id="302ab-143">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure HDInsight linked service, and save the file as **MyOnDemandSparkLinkedService.json**.</span><span class="sxs-lookup"><span data-stu-id="302ab-143">Create a JSON file using your preferred editor, copy the following JSON definition of an Azure HDInsight linked service, and save the file as **MyOnDemandSparkLinkedService.json**.</span></span>  

```json
{
    "name": "MyOnDemandSparkLinkedService",
    "properties": {
      "type": "HDInsightOnDemand",
      "typeProperties": {
        "clusterSize": 2,
        "clusterType": "spark",
        "timeToLive": "00:15:00",
        "hostSubscriptionId": "<subscriptionID> ",
        "servicePrincipalId": "<servicePrincipalID>",
        "servicePrincipalKey": {
          "value": "<servicePrincipalKey>",
          "type": "SecureString"
        },
        "tenant": "<tenant ID>",
        "clusterResourceGroup": "<resourceGroupofHDICluster>",
        "version": "3.6",
        "osType": "Linux",
        "clusterNamePrefix":"ADFSparkSample",
        "linkedServiceName": {
          "referenceName": "MyStorageLinkedService",
          "type": "LinkedServiceReference"
        }
      }
    }
}
```
<span data-ttu-id="302ab-144">Update values for the following properties in the linked service definition:</span><span class="sxs-lookup"><span data-stu-id="302ab-144">Update values for the following properties in the linked service definition:</span></span> 

- <span data-ttu-id="302ab-145">**hostSubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="302ab-145">**hostSubscriptionId**.</span></span> <span data-ttu-id="302ab-146">Replace &lt;subscriptionID&gt; with the ID of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="302ab-146">Replace &lt;subscriptionID&gt; with the ID of your Azure subscription.</span></span> <span data-ttu-id="302ab-147">The on-demand HDInsight cluster is created in this subscription.</span><span class="sxs-lookup"><span data-stu-id="302ab-147">The on-demand HDInsight cluster is created in this subscription.</span></span> 
- <span data-ttu-id="302ab-148">**tenant**.</span><span class="sxs-lookup"><span data-stu-id="302ab-148">**tenant**.</span></span> <span data-ttu-id="302ab-149">Replace &lt;tenantID&gt; with ID of your Azure tenant.</span><span class="sxs-lookup"><span data-stu-id="302ab-149">Replace &lt;tenantID&gt; with ID of your Azure tenant.</span></span> 
- <span data-ttu-id="302ab-150">**servicePrincipalId**, **servicePrincipalKey**.</span><span class="sxs-lookup"><span data-stu-id="302ab-150">**servicePrincipalId**, **servicePrincipalKey**.</span></span> <span data-ttu-id="302ab-151">Replace &lt;servicePrincipalID&gt; and &lt;servicePrincipalKey&gt; with ID and key of your service principal in the Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="302ab-151">Replace &lt;servicePrincipalID&gt; and &lt;servicePrincipalKey&gt; with ID and key of your service principal in the Azure Active Directory.</span></span> <span data-ttu-id="302ab-152">This service principal needs to be a member of the Contributor role of the subscription or the resource Group in which the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="302ab-152">This service principal needs to be a member of the Contributor role of the subscription or the resource Group in which the cluster is created.</span></span> <span data-ttu-id="302ab-153">See [create Azure Active Directory application and service principal](../azure-resource-manager/resource-group-create-service-principal-portal.md) for details.</span><span class="sxs-lookup"><span data-stu-id="302ab-153">See [create Azure Active Directory application and service principal](../azure-resource-manager/resource-group-create-service-principal-portal.md) for details.</span></span> 
- <span data-ttu-id="302ab-154">**clusterResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="302ab-154">**clusterResourceGroup**.</span></span> <span data-ttu-id="302ab-155">Replace &lt;resourceGroupOfHDICluster&gt; with the name of the resource group in which the HDInsight cluster needs to be created.</span><span class="sxs-lookup"><span data-stu-id="302ab-155">Replace &lt;resourceGroupOfHDICluster&gt; with the name of the resource group in which the HDInsight cluster needs to be created.</span></span> 

> [!NOTE]
> <span data-ttu-id="302ab-156">Azure HDInsight has limitation on the total number of cores you can use in each Azure region it supports.</span><span class="sxs-lookup"><span data-stu-id="302ab-156">Azure HDInsight has limitation on the total number of cores you can use in each Azure region it supports.</span></span> <span data-ttu-id="302ab-157">For On-Demand HDInsight Linked Service, the HDInsight cluster will be created in the same location of the Azure Storage used as its primary storage.</span><span class="sxs-lookup"><span data-stu-id="302ab-157">For On-Demand HDInsight Linked Service, the HDInsight cluster will be created in the same location of the Azure Storage used as its primary storage.</span></span> <span data-ttu-id="302ab-158">Ensure that you have enough core quotas for the cluster to be created successfully.</span><span class="sxs-lookup"><span data-stu-id="302ab-158">Ensure that you have enough core quotas for the cluster to be created successfully.</span></span> <span data-ttu-id="302ab-159">For more information, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="302ab-159">For more information, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span> 


## <a name="author-a-pipeline"></a><span data-ttu-id="302ab-160">Author a pipeline</span><span class="sxs-lookup"><span data-stu-id="302ab-160">Author a pipeline</span></span> 
<span data-ttu-id="302ab-161">In this step, you create a new pipeline with a Spark activity.</span><span class="sxs-lookup"><span data-stu-id="302ab-161">In this step, you create a new pipeline with a Spark activity.</span></span> <span data-ttu-id="302ab-162">The activity uses the **word count** sample.</span><span class="sxs-lookup"><span data-stu-id="302ab-162">The activity uses the **word count** sample.</span></span> <span data-ttu-id="302ab-163">Download the contents from this location if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="302ab-163">Download the contents from this location if you haven't already done so.</span></span>

<span data-ttu-id="302ab-164">Create a JSON file in your preferred editor, copy the following JSON definition of a pipeline definition, and save it as **MySparkOnDemandPipeline.json**.</span><span class="sxs-lookup"><span data-stu-id="302ab-164">Create a JSON file in your preferred editor, copy the following JSON definition of a pipeline definition, and save it as **MySparkOnDemandPipeline.json**.</span></span> 

```json
{
  "name": "MySparkOnDemandPipeline",
  "properties": {
    "activities": [
      {
        "name": "MySparkActivity",
        "type": "HDInsightSpark",
        "linkedServiceName": {
            "referenceName": "MyOnDemandSparkLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "rootPath": "adftutorial/spark",
          "entryFilePath": "script/WordCount_Spark.py",
          "getDebugInfo": "Failure",
          "sparkJobLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="302ab-165">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="302ab-165">Note the following points:</span></span> 

- <span data-ttu-id="302ab-166">rootPath points to the spark folder of the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="302ab-166">rootPath points to the spark folder of the adftutorial container.</span></span> 
- <span data-ttu-id="302ab-167">entryFilePath points to the WordCount_Spark.py file in the script sub folder of the spark folder.</span><span class="sxs-lookup"><span data-stu-id="302ab-167">entryFilePath points to the WordCount_Spark.py file in the script sub folder of the spark folder.</span></span> 


## <a name="create-a-data-factory"></a><span data-ttu-id="302ab-168">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="302ab-168">Create a data factory</span></span> 
<span data-ttu-id="302ab-169">You have authored linked service and pipeline definitions in JSON files.</span><span class="sxs-lookup"><span data-stu-id="302ab-169">You have authored linked service and pipeline definitions in JSON files.</span></span> <span data-ttu-id="302ab-170">Now, let’s create a data factory, and deploy the linked Service and pipeline JSON files by using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="302ab-170">Now, let’s create a data factory, and deploy the linked Service and pipeline JSON files by using PowerShell cmdlets.</span></span> <span data-ttu-id="302ab-171">Run the following PowerShell commands one by one:</span><span class="sxs-lookup"><span data-stu-id="302ab-171">Run the following PowerShell commands one by one:</span></span> 

1. <span data-ttu-id="302ab-172">Set variables one by one.</span><span class="sxs-lookup"><span data-stu-id="302ab-172">Set variables one by one.</span></span>

    <span data-ttu-id="302ab-173">**Resource Group Name**</span><span class="sxs-lookup"><span data-stu-id="302ab-173">**Resource Group Name**</span></span>
    ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup" 
    ```

    <span data-ttu-id="302ab-174">**Data Factory Name. Must be globally unique**</span><span class="sxs-lookup"><span data-stu-id="302ab-174">**Data Factory Name. Must be globally unique**</span></span> 
    ```powershell
    $dataFactoryName = "MyDataFactory09102017"
    ```
    
    <span data-ttu-id="302ab-175">**Pipeline name**</span><span class="sxs-lookup"><span data-stu-id="302ab-175">**Pipeline name**</span></span>
    ```powershell
    $pipelineName = "MySparkOnDemandPipeline" # Name of the pipeline
    ```
2. <span data-ttu-id="302ab-176">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="302ab-176">Launch **PowerShell**.</span></span> <span data-ttu-id="302ab-177">Keep Azure PowerShell open until the end of this quickstart.</span><span class="sxs-lookup"><span data-stu-id="302ab-177">Keep Azure PowerShell open until the end of this quickstart.</span></span> <span data-ttu-id="302ab-178">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="302ab-178">If you close and reopen, you need to run the commands again.</span></span> <span data-ttu-id="302ab-179">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="302ab-179">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="302ab-180">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="302ab-180">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

    <span data-ttu-id="302ab-181">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="302ab-181">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>
        
    ```powershell
    Connect-AzureRmAccount
    ```        
    <span data-ttu-id="302ab-182">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="302ab-182">Run the following command to view all the subscriptions for this account:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```
    <span data-ttu-id="302ab-183">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="302ab-183">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="302ab-184">Replace **SubscriptionId** with the ID of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="302ab-184">Replace **SubscriptionId** with the ID of your Azure subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"    
    ```  
3. <span data-ttu-id="302ab-185">Create the resource group: ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="302ab-185">Create the resource group: ADFTutorialResourceGroup.</span></span> 

    ```powershell
    New-AzureRmResourceGroup -Name $resourceGroupName -Location "East Us" 
    ```
4. <span data-ttu-id="302ab-186">Create the data factory.</span><span class="sxs-lookup"><span data-stu-id="302ab-186">Create the data factory.</span></span> 

    ```powershell
     $df = Set-AzureRmDataFactoryV2 -Location EastUS -Name $dataFactoryName -ResourceGroupName $resourceGroupName
    ```

    <span data-ttu-id="302ab-187">Execute the following command to see the output:</span><span class="sxs-lookup"><span data-stu-id="302ab-187">Execute the following command to see the output:</span></span> 

    ```powershell
    $df
    ```
5. <span data-ttu-id="302ab-188">Switch to the folder where you created JSON files, and run the following command to deploy an Azure Storage linked service:</span><span class="sxs-lookup"><span data-stu-id="302ab-188">Switch to the folder where you created JSON files, and run the following command to deploy an Azure Storage linked service:</span></span> 
       
    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyStorageLinkedService" -File "MyStorageLinkedService.json"
    ```
6. <span data-ttu-id="302ab-189">Run the following command to deploy an on-demand Spark linked service:</span><span class="sxs-lookup"><span data-stu-id="302ab-189">Run the following command to deploy an on-demand Spark linked service:</span></span> 
       
    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyOnDemandSparkLinkedService" -File "MyOnDemandSparkLinkedService.json"
    ```
7. <span data-ttu-id="302ab-190">Run the following command to deploy a pipeline:</span><span class="sxs-lookup"><span data-stu-id="302ab-190">Run the following command to deploy a pipeline:</span></span> 
       
    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name $pipelineName -File "MySparkOnDemandPipeline.json"
    ```
    
## <a name="start-and-monitor-a-pipeline-run"></a><span data-ttu-id="302ab-191">Start and monitor a pipeline run</span><span class="sxs-lookup"><span data-stu-id="302ab-191">Start and monitor a pipeline run</span></span>  

1. <span data-ttu-id="302ab-192">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="302ab-192">Start a pipeline run.</span></span> <span data-ttu-id="302ab-193">It also captures the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="302ab-193">It also captures the pipeline run ID for future monitoring.</span></span>

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName  
    ```
2. <span data-ttu-id="302ab-194">Run the following script to continuously check the pipeline run status until it finishes.</span><span class="sxs-lookup"><span data-stu-id="302ab-194">Run the following script to continuously check the pipeline run status until it finishes.</span></span>

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    
        if(!$result) {
            Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
        }
        elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
        }
        else {
            Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
        ($result | Format-List | Out-String)
        Start-Sleep -Seconds 15
    }

    Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
    $result.Output -join "`r`n"

    Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
    $result.Error -join "`r`n" 
    ```  
3. <span data-ttu-id="302ab-195">Here is the output of the sample run:</span><span class="sxs-lookup"><span data-stu-id="302ab-195">Here is the output of the sample run:</span></span> 

    ```
    Pipeline run status: In Progress
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : 
    ActivityName      : MySparkActivity
    PipelineRunId     : 94e71d08-a6fa-4191-b7d1-cf8c71cb4794
    PipelineName      : MySparkOnDemandPipeline
    Input             : {rootPath, entryFilePath, getDebugInfo, sparkJobLinkedService}
    Output            : 
    LinkedServiceName : 
    ActivityRunStart  : 9/20/2017 6:33:47 AM
    ActivityRunEnd    : 
    DurationInMs      : 
    Status            : InProgress
    Error             :
    …
    
    Pipeline ' MySparkOnDemandPipeline' run finished. Result:
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : MyDataFactory09102017
    ActivityName      : MySparkActivity
    PipelineRunId     : 94e71d08-a6fa-4191-b7d1-cf8c71cb4794
    PipelineName      : MySparkOnDemandPipeline
    Input             : {rootPath, entryFilePath, getDebugInfo, sparkJobLinkedService}
    Output            : {clusterInUse, jobId, ExecutionProgress, effectiveIntegrationRuntime}
    LinkedServiceName : 
    ActivityRunStart  : 9/20/2017 6:33:47 AM
    ActivityRunEnd    : 9/20/2017 6:46:30 AM
    DurationInMs      : 763466
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    Activity Output section:
    "clusterInUse": "https://ADFSparkSamplexxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.azurehdinsight.net/"
    "jobId": "0"
    "ExecutionProgress": "Succeeded"
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)"
    Activity Error section:
    "errorCode": ""
    "message": ""
    "failureType": ""
    "target": "MySparkActivity"
    ```
4. <span data-ttu-id="302ab-196">Confirm that a folder named `outputfiles` is created in the `spark` folder of adftutorial container with the output from the spark program.</span><span class="sxs-lookup"><span data-stu-id="302ab-196">Confirm that a folder named `outputfiles` is created in the `spark` folder of adftutorial container with the output from the spark program.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="302ab-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="302ab-197">Next steps</span></span>
<span data-ttu-id="302ab-198">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="302ab-198">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="302ab-199">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="302ab-199">You learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="302ab-200">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="302ab-200">Create a data factory.</span></span> 
> * <span data-ttu-id="302ab-201">Author and deploy linked services.</span><span class="sxs-lookup"><span data-stu-id="302ab-201">Author and deploy linked services.</span></span>
> * <span data-ttu-id="302ab-202">Author and deploy a pipeline.</span><span class="sxs-lookup"><span data-stu-id="302ab-202">Author and deploy a pipeline.</span></span> 
> * <span data-ttu-id="302ab-203">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="302ab-203">Start a pipeline run.</span></span>
> * <span data-ttu-id="302ab-204">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="302ab-204">Monitor the pipeline run.</span></span>

<span data-ttu-id="302ab-205">Advance to the next tutorial to learn how to transform data by running Hive script on an Azure HDInsight cluster that is in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="302ab-205">Advance to the next tutorial to learn how to transform data by running Hive script on an Azure HDInsight cluster that is in a virtual network.</span></span> 

> [!div class="nextstepaction"]
> <span data-ttu-id="302ab-206">[Tutorial: transform data using Hive in Azure Virtual Network](tutorial-transform-data-hive-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="302ab-206">[Tutorial: transform data using Hive in Azure Virtual Network](tutorial-transform-data-hive-virtual-network.md).</span></span>





