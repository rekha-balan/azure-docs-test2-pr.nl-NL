---
title: Build your first data factory (PowerShell) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using Azure PowerShell.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/25/2017
ms.author: spelluru
ms.openlocfilehash: 1eeebc0c5a4c45ec9da2dd8bc657cf4b7c39a372
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661207"
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="4593d-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4593d-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="4593d-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span></span> <span data-ttu-id="4593d-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4593d-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

> [!NOTE]
> The data pipeline in this tutorial transforms input data to produce output data. It does not copy data from a source data store to a destination data store. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

## <a name="prerequisites"></a><span data-ttu-id="4593d-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4593d-117">Prerequisites</span></span>
* <span data-ttu-id="4593d-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="4593d-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="4593d-119">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install latest version of Azure PowerShell on your computer.</span><span class="sxs-lookup"><span data-stu-id="4593d-119">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="4593d-120">(optional) This article does not cover all the Data Factory cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4593d-120">(optional) This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="4593d-121">See [Data Factory Cmdlet Reference](/powershell/resourcemanager/azurerm.datafactories/v2.5.0/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4593d-121">See [Data Factory Cmdlet Reference](/powershell/resourcemanager/azurerm.datafactories/v2.5.0/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="4593d-122">Create data factory</span><span class="sxs-lookup"><span data-stu-id="4593d-122">Create data factory</span></span>
<span data-ttu-id="4593d-123">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="4593d-123">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="4593d-124">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="4593d-124">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4593d-125">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="4593d-125">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4593d-126">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform input data.</span><span class="sxs-lookup"><span data-stu-id="4593d-126">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform input data.</span></span> <span data-ttu-id="4593d-127">Let's start with creating the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="4593d-127">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="4593d-128">Start Azure PowerShell and run the following command.</span><span class="sxs-lookup"><span data-stu-id="4593d-128">Start Azure PowerShell and run the following command.</span></span> <span data-ttu-id="4593d-129">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4593d-129">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="4593d-130">If you close and reopen, you need to run these commands again.</span><span class="sxs-lookup"><span data-stu-id="4593d-130">If you close and reopen, you need to run these commands again.</span></span>
   * <span data-ttu-id="4593d-131">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4593d-131">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="4593d-132">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="4593d-132">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="4593d-133">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="4593d-133">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="4593d-134">This subscription should be the same as the one you used in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4593d-134">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="4593d-135">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-135">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="4593d-136">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="4593d-136">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="4593d-137">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4593d-137">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="4593d-138">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="4593d-138">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="4593d-139">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="4593d-139">Note the following points:</span></span>

* <span data-ttu-id="4593d-140">The name of the Azure Data Factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="4593d-140">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="4593d-141">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="4593d-141">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="4593d-142">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4593d-142">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="4593d-143">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="4593d-143">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="4593d-144">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4593d-144">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="4593d-145">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span><span class="sxs-lookup"><span data-stu-id="4593d-145">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
* <span data-ttu-id="4593d-146">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="4593d-146">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="4593d-147">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="4593d-147">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="4593d-148">You can run the following command to confirm that the Data Factory provider is registered:</span><span class="sxs-lookup"><span data-stu-id="4593d-148">You can run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="4593d-149">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4593d-149">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="4593d-150">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="4593d-150">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="4593d-151">Before creating a pipeline, you need to create a few Data Factory entities first.</span><span class="sxs-lookup"><span data-stu-id="4593d-151">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="4593d-152">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span><span class="sxs-lookup"><span data-stu-id="4593d-152">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4593d-153">Create linked services</span><span class="sxs-lookup"><span data-stu-id="4593d-153">Create linked services</span></span>
<span data-ttu-id="4593d-154">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-154">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="4593d-155">The Azure Storage account holds the input and output data for the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="4593d-155">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="4593d-156">The HDInsight linked service is used to run Hive script specified in the activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="4593d-156">The HDInsight linked service is used to run Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="4593d-157">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span><span class="sxs-lookup"><span data-stu-id="4593d-157">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4593d-158">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="4593d-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="4593d-159">In this step, you link your Azure Storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="4593d-160">You use the same Azure Storage account to store input/output data and the HQL script file.</span><span class="sxs-lookup"><span data-stu-id="4593d-160">You use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="4593d-161">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="4593d-161">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span></span> <span data-ttu-id="4593d-162">Create the folder ADFGetStarted if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="4593d-162">Create the folder ADFGetStarted if it does not already exist.</span></span>

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    <span data-ttu-id="4593d-163">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="4593d-163">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="4593d-164">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4593d-164">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="4593d-165">In Azure PowerShell, switch to the ADFGetStarted folder.</span><span class="sxs-lookup"><span data-stu-id="4593d-165">In Azure PowerShell, switch to the ADFGetStarted folder.</span></span>
3. <span data-ttu-id="4593d-166">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span><span class="sxs-lookup"><span data-stu-id="4593d-166">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="4593d-167">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span><span class="sxs-lookup"><span data-stu-id="4593d-167">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="4593d-168">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4593d-168">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="4593d-169">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span><span class="sxs-lookup"><span data-stu-id="4593d-169">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="4593d-170">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span><span class="sxs-lookup"><span data-stu-id="4593d-170">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="4593d-171">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span><span class="sxs-lookup"><span data-stu-id="4593d-171">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="4593d-172">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4593d-172">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="4593d-173">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="4593d-173">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="4593d-174">In this step, you link an on-demand HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-174">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="4593d-175">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="4593d-175">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="4593d-176">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-176">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4593d-177">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span><span class="sxs-lookup"><span data-stu-id="4593d-177">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="4593d-178">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="4593d-178">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span></span>

    ```json
    {
      "name": "HDInsightOnDemandLinkedService",
      "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
          "version": "3.2",
          "clusterSize": 1,
          "timeToLive": "00:30:00",
          "linkedServiceName": "StorageLinkedService"
        }
      }
    }
    ```
    <span data-ttu-id="4593d-179">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="4593d-179">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="4593d-180">Property</span><span class="sxs-lookup"><span data-stu-id="4593d-180">Property</span></span> | <span data-ttu-id="4593d-181">Description</span><span class="sxs-lookup"><span data-stu-id="4593d-181">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4593d-182">Version</span><span class="sxs-lookup"><span data-stu-id="4593d-182">Version</span></span> |<span data-ttu-id="4593d-183">Specifies that the version of the HDInsight created to be 3.2.</span><span class="sxs-lookup"><span data-stu-id="4593d-183">Specifies that the version of the HDInsight created to be 3.2.</span></span> |
   | <span data-ttu-id="4593d-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="4593d-184">ClusterSize</span></span> |<span data-ttu-id="4593d-185">Specifies the size of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-185">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="4593d-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="4593d-186">TimeToLive</span></span> |<span data-ttu-id="4593d-187">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="4593d-187">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="4593d-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4593d-188">linkedServiceName</span></span> |<span data-ttu-id="4593d-189">Specifies the storage account that is used to store the logs that are generated by HDInsight</span><span class="sxs-lookup"><span data-stu-id="4593d-189">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="4593d-190">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="4593d-190">Note the following points:</span></span>

   * <span data-ttu-id="4593d-191">The Data Factory creates a **Windows-based** HDInsight cluster for you with the JSON.</span><span class="sxs-lookup"><span data-stu-id="4593d-191">The Data Factory creates a **Windows-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="4593d-192">You could also have it create a **Linux-based** HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-192">You could also have it create a **Linux-based** HDInsight cluster.</span></span> <span data-ttu-id="4593d-193">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="4593d-193">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="4593d-194">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-194">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4593d-195">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="4593d-195">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="4593d-196">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="4593d-196">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="4593d-197">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="4593d-197">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="4593d-198">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="4593d-198">This behavior is by design.</span></span> <span data-ttu-id="4593d-199">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="4593d-199">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="4593d-200">The cluster is automatically deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="4593d-200">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="4593d-201">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4593d-201">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="4593d-202">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="4593d-202">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="4593d-203">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="4593d-203">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="4593d-204">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4593d-204">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="4593d-205">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="4593d-205">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="4593d-206">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="4593d-206">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="4593d-207">Create datasets</span><span class="sxs-lookup"><span data-stu-id="4593d-207">Create datasets</span></span>
<span data-ttu-id="4593d-208">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="4593d-208">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="4593d-209">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4593d-209">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="4593d-210">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="4593d-210">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="4593d-211">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="4593d-211">Create input dataset</span></span>
1. <span data-ttu-id="4593d-212">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="4593d-212">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="4593d-213">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4593d-213">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="4593d-214">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="4593d-214">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    <span data-ttu-id="4593d-215">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="4593d-215">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="4593d-216">Property</span><span class="sxs-lookup"><span data-stu-id="4593d-216">Property</span></span> | <span data-ttu-id="4593d-217">Description</span><span class="sxs-lookup"><span data-stu-id="4593d-217">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4593d-218">type</span><span class="sxs-lookup"><span data-stu-id="4593d-218">type</span></span> |<span data-ttu-id="4593d-219">The type property is set to AzureBlob because data resides in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4593d-219">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="4593d-220">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4593d-220">linkedServiceName</span></span> |<span data-ttu-id="4593d-221">refers to the StorageLinkedService you created earlier.</span><span class="sxs-lookup"><span data-stu-id="4593d-221">refers to the StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="4593d-222">fileName</span><span class="sxs-lookup"><span data-stu-id="4593d-222">fileName</span></span> |<span data-ttu-id="4593d-223">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="4593d-223">This property is optional.</span></span> <span data-ttu-id="4593d-224">If you omit this property, all the files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="4593d-224">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="4593d-225">In this case, only the input.log is processed.</span><span class="sxs-lookup"><span data-stu-id="4593d-225">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="4593d-226">type</span><span class="sxs-lookup"><span data-stu-id="4593d-226">type</span></span> |<span data-ttu-id="4593d-227">The log files are in text format, so we use TextFormat.</span><span class="sxs-lookup"><span data-stu-id="4593d-227">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="4593d-228">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="4593d-228">columnDelimiter</span></span> |<span data-ttu-id="4593d-229">columns in the log files are delimited by the comma character (,).</span><span class="sxs-lookup"><span data-stu-id="4593d-229">columns in the log files are delimited by the comma character (,).</span></span> |
   | <span data-ttu-id="4593d-230">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4593d-230">frequency/interval</span></span> |<span data-ttu-id="4593d-231">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="4593d-231">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="4593d-232">external</span><span class="sxs-lookup"><span data-stu-id="4593d-232">external</span></span> |<span data-ttu-id="4593d-233">this property is set to true if the input data is not generated by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="4593d-233">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
2. <span data-ttu-id="4593d-234">Run the following command in Azure PowerShell to create the Data Factory dataset:</span><span class="sxs-lookup"><span data-stu-id="4593d-234">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="4593d-235">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="4593d-235">Create output dataset</span></span>
<span data-ttu-id="4593d-236">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4593d-236">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="4593d-237">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="4593d-237">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="4593d-238">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4593d-238">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="4593d-239">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="4593d-239">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="4593d-240">The **availability** section specifies that the output dataset is produced on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="4593d-240">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="4593d-241">Run the following command in Azure PowerShell to create the Data Factory dataset:</span><span class="sxs-lookup"><span data-stu-id="4593d-241">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="4593d-242">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="4593d-242">Create pipeline</span></span>
<span data-ttu-id="4593d-243">In this step, you create your first pipeline with a **HDInsightHive** activity.</span><span class="sxs-lookup"><span data-stu-id="4593d-243">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="4593d-244">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span><span class="sxs-lookup"><span data-stu-id="4593d-244">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="4593d-245">The settings for the output dataset and the activity scheduler must match.</span><span class="sxs-lookup"><span data-stu-id="4593d-245">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="4593d-246">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="4593d-246">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="4593d-247">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="4593d-247">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="4593d-248">The properties used in the following JSON are explained at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="4593d-248">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="4593d-249">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="4593d-249">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span></span>

   > [!IMPORTANT]
   > Replace **storageaccountname** with the name of your storage account in the JSON.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    <span data-ttu-id="4593d-251">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-251">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="4593d-252">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="4593d-252">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="4593d-253">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="4593d-253">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="4593d-254">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4593d-254">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="4593d-255">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4593d-255">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in the example.

2. <span data-ttu-id="4593d-257">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4593d-257">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="4593d-258">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span><span class="sxs-lookup"><span data-stu-id="4593d-258">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="4593d-259">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="4593d-259">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="4593d-260">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="4593d-260">Monitor pipeline</span></span>
<span data-ttu-id="4593d-261">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-261">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="4593d-262">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span><span class="sxs-lookup"><span data-stu-id="4593d-262">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="4593d-263">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4593d-263">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2016-04-01
    ```
    <span data-ttu-id="4593d-264">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="4593d-264">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> <span data-ttu-id="4593d-265">You should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="4593d-265">You should see output similar to the following.</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 4/1/2016 12:00:00 AM
    End               : 4/2/2016 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="4593d-266">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span><span class="sxs-lookup"><span data-stu-id="4593d-266">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2016-04-01
    ```

    <span data-ttu-id="4593d-267">You should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="4593d-267">You should see output similar to the following.</span></span>

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 4/1/2016 12:00:00 AM
    DataSliceEnd        : 4/2/2016 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="4593d-268">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="4593d-268">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="4593d-269">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="4593d-269">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="4593d-270">Creation of an on-demand HDInsight cluster usually takes some time.</span><span class="sxs-lookup"><span data-stu-id="4593d-270">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![output data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes). Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.
>
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.
>
>

## <a name="summary"></a><span data-ttu-id="4593d-276">Summary</span><span class="sxs-lookup"><span data-stu-id="4593d-276">Summary</span></span>
<span data-ttu-id="4593d-277">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-277">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="4593d-278">You used the Data Factory Editor in the Azure portal to do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4593d-278">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="4593d-279">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="4593d-279">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="4593d-280">Created two **linked services**:</span><span class="sxs-lookup"><span data-stu-id="4593d-280">Created two **linked services**:</span></span>
   1. <span data-ttu-id="4593d-281">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-281">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="4593d-282">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-282">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="4593d-283">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="4593d-283">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="4593d-284">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4593d-284">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="4593d-285">Created a **pipeline** with a **HDInsight Hive** activity.</span><span class="sxs-lookup"><span data-stu-id="4593d-285">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4593d-286">Next steps</span><span class="sxs-lookup"><span data-stu-id="4593d-286">Next steps</span></span>
<span data-ttu-id="4593d-287">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-287">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="4593d-288">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4593d-288">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4593d-289">See Also</span><span class="sxs-lookup"><span data-stu-id="4593d-289">See Also</span></span>
| <span data-ttu-id="4593d-290">Topic</span><span class="sxs-lookup"><span data-stu-id="4593d-290">Topic</span></span> | <span data-ttu-id="4593d-291">Description</span><span class="sxs-lookup"><span data-stu-id="4593d-291">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="4593d-292">Data Factory Cmdlet Reference</span><span class="sxs-lookup"><span data-stu-id="4593d-292">Data Factory Cmdlet Reference</span></span>](/powershell/resourcemanager/azurerm.datafactories/v2.5.0/azurerm.datafactories) |<span data-ttu-id="4593d-293">See comprehensive documentation on Data Factory cmdlets</span><span class="sxs-lookup"><span data-stu-id="4593d-293">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="4593d-294">Pipelines</span><span class="sxs-lookup"><span data-stu-id="4593d-294">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="4593d-295">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="4593d-295">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="4593d-296">Datasets</span><span class="sxs-lookup"><span data-stu-id="4593d-296">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="4593d-297">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4593d-297">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="4593d-298">Scheduling and Execution</span><span class="sxs-lookup"><span data-stu-id="4593d-298">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="4593d-299">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="4593d-299">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="4593d-300">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="4593d-300">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="4593d-301">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="4593d-301">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

