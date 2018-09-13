---
title: Invoke Spark programs from Azure Data Factory | Microsoft Docs
description: Learn how to invoke Spark programs from an Azure data factory using the MapReduce Activity.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: spelluru
ms.openlocfilehash: 226d8ac1098036128d1a7e7a1b980b954d1699b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562904"
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="eadff-103">Invoke Spark programs from Azure Data Factory pipelines</span><span class="sxs-lookup"><span data-stu-id="eadff-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive Activity](data-factory-hive-activity.md) 
> * [Pig Activity](data-factory-pig-activity.md)
> * [MapReduce Activity](data-factory-map-reduce.md)
> * [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md)
> * [Spark Activity](data-factory-spark.md)
> * [Machine Learning Batch Execution Activity](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Update Resource Activity](data-factory-azure-ml-update-resource-activity.md)
> * [Stored Procedure Activity](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md)
> * [.NET Custom Activity](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="eadff-114">Introduction</span><span class="sxs-lookup"><span data-stu-id="eadff-114">Introduction</span></span>
<span data-ttu-id="eadff-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="eadff-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eadff-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.
> - Spark Activity supports only existing (your own) HDInsight Spark clusters. It does not support an on-demand HDInsight linked service. 

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="eadff-120">Walkthrough: create a pipeline with Spark activity</span><span class="sxs-lookup"><span data-stu-id="eadff-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="eadff-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span><span class="sxs-lookup"><span data-stu-id="eadff-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="eadff-122">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-122">Create a data factory.</span></span>
2. <span data-ttu-id="eadff-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="eadff-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="eadff-125">Create a dataset that refers to the Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="eadff-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="eadff-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span><span class="sxs-lookup"><span data-stu-id="eadff-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="eadff-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span><span class="sxs-lookup"><span data-stu-id="eadff-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="eadff-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span><span class="sxs-lookup"><span data-stu-id="eadff-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="eadff-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="eadff-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="eadff-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span><span class="sxs-lookup"><span data-stu-id="eadff-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eadff-131">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eadff-131">Prerequisites</span></span>
1. <span data-ttu-id="eadff-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="eadff-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="eadff-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="eadff-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="eadff-134">Associate the Azure storage account you created in step #1 with this cluster.</span><span class="sxs-lookup"><span data-stu-id="eadff-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="eadff-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="eadff-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="eadff-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="eadff-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="eadff-137">Create the container and the folder if they do not exist.</span><span class="sxs-lookup"><span data-stu-id="eadff-137">Create the container and the folder if they do not exist.</span></span> 
 
### <a name="create-data-factory"></a><span data-ttu-id="eadff-138">Create data factory</span><span class="sxs-lookup"><span data-stu-id="eadff-138">Create data factory</span></span>
<span data-ttu-id="eadff-139">Let's start with creating the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="eadff-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="eadff-140">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eadff-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eadff-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="eadff-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="eadff-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span><span class="sxs-lookup"><span data-stu-id="eadff-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > The name of the Azure data factory must be **globally unique**. If you see the error: **Data factory name “SparkDF” is not available**. Change the name of the data factory (for example, yournameSparkDFdate, and try creating again. See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.   
4. <span data-ttu-id="eadff-147">Select the **Azure subscription** where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="eadff-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="eadff-148">Select an existing **resource group** or create an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="eadff-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="eadff-149">Select **Pin to dashboard** option.</span><span class="sxs-lookup"><span data-stu-id="eadff-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="eadff-150">Click **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="eadff-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.
7. <span data-ttu-id="eadff-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span><span class="sxs-lookup"><span data-stu-id="eadff-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="eadff-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="eadff-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="eadff-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span> 

    ![Data Factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="eadff-156">Create linked services</span><span class="sxs-lookup"><span data-stu-id="eadff-156">Create linked services</span></span>
<span data-ttu-id="eadff-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="eadff-158">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="eadff-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="eadff-159">In this step, you link your Azure Storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="eadff-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span><span class="sxs-lookup"><span data-stu-id="eadff-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="eadff-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span><span class="sxs-lookup"><span data-stu-id="eadff-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  
  
1. <span data-ttu-id="eadff-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="eadff-163">You should see the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="eadff-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="eadff-164">Click **New data store** and choose **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="eadff-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![New data store - Azure Storage - menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="eadff-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="eadff-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure Storage linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="eadff-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="eadff-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="eadff-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="eadff-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="eadff-170">To deploy the linked service, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="eadff-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="eadff-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="eadff-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="eadff-172">Create HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="eadff-172">Create HDInsight linked service</span></span>
<span data-ttu-id="eadff-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="eadff-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="eadff-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="eadff-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="eadff-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Create HDInsight linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="eadff-177">Copy and paste the following snippet to the **Draft-1** window.</span><span class="sxs-lookup"><span data-stu-id="eadff-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="eadff-178">In the JSON editor, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="eadff-178">In the JSON editor, do the following steps:</span></span> 
    1. <span data-ttu-id="eadff-179">Specify the **URI** for the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="eadff-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="eadff-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="eadff-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span> 
    2. <span data-ttu-id="eadff-181">Specify the name of the **user** who has access to the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="eadff-181">Specify the name of the **user** who has access to the Spark cluster.</span></span> 
    3. <span data-ttu-id="eadff-182">Specify the **password** for user.</span><span class="sxs-lookup"><span data-stu-id="eadff-182">Specify the **password** for user.</span></span> 
    4. <span data-ttu-id="eadff-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="eadff-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="eadff-184">In this example, it is: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="eadff-184">In this example, it is: **AzureStorageLinkedService**.</span></span> 
    
    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.
    > - Spark Activity supports only existing (your own) HDInsight Spark cluster. It does not support an on-demand HDInsight linked service. 

    <span data-ttu-id="eadff-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="eadff-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span> 
3.  <span data-ttu-id="eadff-189">To deploy the linked service, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="eadff-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="eadff-190">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="eadff-190">Create output dataset</span></span>
<span data-ttu-id="eadff-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="eadff-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="eadff-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span><span class="sxs-lookup"><span data-stu-id="eadff-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="eadff-193">Specifying an input dataset for the activity is optional.</span><span class="sxs-lookup"><span data-stu-id="eadff-193">Specifying an input dataset for the activity is optional.</span></span> 

1. <span data-ttu-id="eadff-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="eadff-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="eadff-195">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="eadff-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="eadff-196">The JSON snippet defines a dataset called **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="eadff-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="eadff-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="eadff-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="eadff-198">As mentioned earlier, this dataset is a dummy dataset.</span><span class="sxs-lookup"><span data-stu-id="eadff-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="eadff-199">The Spark program in this example does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="eadff-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="eadff-200">The **availability** section specifies that the output dataset is produced daily.</span><span class="sxs-lookup"><span data-stu-id="eadff-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="eadff-201">To deploy the dataset, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="eadff-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="eadff-202">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="eadff-202">Create pipeline</span></span>
<span data-ttu-id="eadff-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span><span class="sxs-lookup"><span data-stu-id="eadff-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="eadff-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="eadff-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="eadff-205">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="eadff-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="eadff-206">Therefore, no input dataset is specified in this example.</span><span class="sxs-lookup"><span data-stu-id="eadff-206">Therefore, no input dataset is specified in this example.</span></span> 

1. <span data-ttu-id="eadff-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="eadff-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="eadff-208">Replace the script in the Draft-1 window with the following script:</span><span class="sxs-lookup"><span data-stu-id="eadff-208">Replace the script in the Draft-1 window with the following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="eadff-209">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="eadff-209">Note the following points:</span></span> 
    - <span data-ttu-id="eadff-210">The **type** property is set to **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="eadff-210">The **type** property is set to **HDInsightSpark**.</span></span> 
    - <span data-ttu-id="eadff-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span><span class="sxs-lookup"><span data-stu-id="eadff-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="eadff-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="eadff-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="eadff-213">You can upload the file to a different Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="eadff-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="eadff-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="eadff-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span><span class="sxs-lookup"><span data-stu-id="eadff-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="eadff-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span><span class="sxs-lookup"><span data-stu-id="eadff-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="eadff-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span><span class="sxs-lookup"><span data-stu-id="eadff-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
    - <span data-ttu-id="eadff-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span><span class="sxs-lookup"><span data-stu-id="eadff-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  
    
        > [!IMPORTANT]
        > We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue. 
    - <span data-ttu-id="eadff-220">The **outputs** section has one output dataset.</span><span class="sxs-lookup"><span data-stu-id="eadff-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="eadff-221">You must specify an output dataset even if the spark program does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="eadff-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="eadff-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="eadff-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  
        
        <span data-ttu-id="eadff-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="eadff-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="eadff-224">To deploy the pipeline, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="eadff-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="eadff-225">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="eadff-225">Monitor pipeline</span></span>
1. <span data-ttu-id="eadff-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span><span class="sxs-lookup"><span data-stu-id="eadff-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="eadff-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span><span class="sxs-lookup"><span data-stu-id="eadff-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span> 

    ![Monitor and Manage tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="eadff-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="eadff-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span> 
3. <span data-ttu-id="eadff-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="eadff-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="eadff-231">Confirm that the data slice is in **ready** state.</span><span class="sxs-lookup"><span data-stu-id="eadff-231">Confirm that the data slice is in **ready** state.</span></span> 

    ![Monitor the pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="eadff-233">Select the **activity window** to see details about the activity run.</span><span class="sxs-lookup"><span data-stu-id="eadff-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="eadff-234">If there is an error, you see details about it in the right pane.</span><span class="sxs-lookup"><span data-stu-id="eadff-234">If there is an error, you see details about it in the right pane.</span></span>
 
### <a name="verify-the-results"></a><span data-ttu-id="eadff-235">Verify the results</span><span class="sxs-lookup"><span data-stu-id="eadff-235">Verify the results</span></span>

1. <span data-ttu-id="eadff-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="eadff-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="eadff-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="eadff-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="eadff-238">Click **New** -> **PySpark** to start a new notebook.</span><span class="sxs-lookup"><span data-stu-id="eadff-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Jupyter new notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="eadff-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span><span class="sxs-lookup"><span data-stu-id="eadff-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="eadff-241">Confirm that you see the data from the hvac table:</span><span class="sxs-lookup"><span data-stu-id="eadff-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Jupyter query results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="eadff-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-spark-sql-query) section for detailed instructions.</span><span class="sxs-lookup"><span data-stu-id="eadff-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-spark-sql-query) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="eadff-244">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="eadff-244">Troubleshooting</span></span>
<span data-ttu-id="eadff-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span><span class="sxs-lookup"><span data-stu-id="eadff-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="eadff-246">The log file in the log folder provides additional details.</span><span class="sxs-lookup"><span data-stu-id="eadff-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="eadff-247">This log file is especially useful when there is an error.</span><span class="sxs-lookup"><span data-stu-id="eadff-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="eadff-248">In a production environment, you may want to set it to **Failure**.</span><span class="sxs-lookup"><span data-stu-id="eadff-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="eadff-249">For further troubleshooting, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="eadff-249">For further troubleshooting, do the following steps:</span></span> 


1. <span data-ttu-id="eadff-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="eadff-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN UI application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="eadff-252">Click **Logs** for one of the run attempts.</span><span class="sxs-lookup"><span data-stu-id="eadff-252">Click **Logs** for one of the run attempts.</span></span>

    ![Application page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/yarn-applications.png) 
3. <span data-ttu-id="eadff-254">You should see additional error information in the log page.</span><span class="sxs-lookup"><span data-stu-id="eadff-254">You should see additional error information in the log page.</span></span> 

    ![Log error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="eadff-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span><span class="sxs-lookup"><span data-stu-id="eadff-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="eadff-257">Spark activity properties</span><span class="sxs-lookup"><span data-stu-id="eadff-257">Spark activity properties</span></span>
<span data-ttu-id="eadff-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span><span class="sxs-lookup"><span data-stu-id="eadff-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="eadff-259">The following table describes the JSON properties used in the JSON definition:</span><span class="sxs-lookup"><span data-stu-id="eadff-259">The following table describes the JSON properties used in the JSON definition:</span></span> 

| <span data-ttu-id="eadff-260">Property</span><span class="sxs-lookup"><span data-stu-id="eadff-260">Property</span></span> | <span data-ttu-id="eadff-261">Description</span><span class="sxs-lookup"><span data-stu-id="eadff-261">Description</span></span> | <span data-ttu-id="eadff-262">Required</span><span class="sxs-lookup"><span data-stu-id="eadff-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="eadff-263">name</span><span class="sxs-lookup"><span data-stu-id="eadff-263">name</span></span> | <span data-ttu-id="eadff-264">Name of the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="eadff-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="eadff-265">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-265">Yes</span></span> |
| <span data-ttu-id="eadff-266">description</span><span class="sxs-lookup"><span data-stu-id="eadff-266">description</span></span> | <span data-ttu-id="eadff-267">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="eadff-267">Text describing what the activity does.</span></span> | <span data-ttu-id="eadff-268">No</span><span class="sxs-lookup"><span data-stu-id="eadff-268">No</span></span> |
| <span data-ttu-id="eadff-269">type</span><span class="sxs-lookup"><span data-stu-id="eadff-269">type</span></span> | <span data-ttu-id="eadff-270">This property must be set to HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="eadff-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="eadff-271">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-271">Yes</span></span> |
| <span data-ttu-id="eadff-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="eadff-272">linkedServiceName</span></span> | <span data-ttu-id="eadff-273">Name of the HDInsight linked service on which the Spark program runs.</span><span class="sxs-lookup"><span data-stu-id="eadff-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="eadff-274">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-274">Yes</span></span> |
| <span data-ttu-id="eadff-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="eadff-275">rootPath</span></span> | <span data-ttu-id="eadff-276">The Azure Blob container and folder that contains the Spark file.</span><span class="sxs-lookup"><span data-stu-id="eadff-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="eadff-277">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="eadff-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="eadff-278">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-278">Yes</span></span> |
| <span data-ttu-id="eadff-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="eadff-279">entryFilePath</span></span> | <span data-ttu-id="eadff-280">Relative path to the root folder of the Spark code/package.</span><span class="sxs-lookup"><span data-stu-id="eadff-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="eadff-281">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-281">Yes</span></span> |
| <span data-ttu-id="eadff-282">className</span><span class="sxs-lookup"><span data-stu-id="eadff-282">className</span></span> | <span data-ttu-id="eadff-283">Application's Java/Spark main class</span><span class="sxs-lookup"><span data-stu-id="eadff-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="eadff-284">No</span><span class="sxs-lookup"><span data-stu-id="eadff-284">No</span></span> | 
| <span data-ttu-id="eadff-285">arguments</span><span class="sxs-lookup"><span data-stu-id="eadff-285">arguments</span></span> | <span data-ttu-id="eadff-286">A list of command-line arguments to the Spark program.</span><span class="sxs-lookup"><span data-stu-id="eadff-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="eadff-287">No</span><span class="sxs-lookup"><span data-stu-id="eadff-287">No</span></span> | 
| <span data-ttu-id="eadff-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="eadff-288">proxyUser</span></span> | <span data-ttu-id="eadff-289">The user account to impersonate to execute the Spark program</span><span class="sxs-lookup"><span data-stu-id="eadff-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="eadff-290">No</span><span class="sxs-lookup"><span data-stu-id="eadff-290">No</span></span> | 
| <span data-ttu-id="eadff-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="eadff-291">sparkConfig</span></span> | <span data-ttu-id="eadff-292">Spark configuration properties.</span><span class="sxs-lookup"><span data-stu-id="eadff-292">Spark configuration properties.</span></span> | <span data-ttu-id="eadff-293">No</span><span class="sxs-lookup"><span data-stu-id="eadff-293">No</span></span> | 
| <span data-ttu-id="eadff-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="eadff-294">getDebugInfo</span></span> | <span data-ttu-id="eadff-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="eadff-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="eadff-296">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="eadff-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="eadff-297">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="eadff-297">Default value: None.</span></span> | <span data-ttu-id="eadff-298">No</span><span class="sxs-lookup"><span data-stu-id="eadff-298">No</span></span> | 
| <span data-ttu-id="eadff-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="eadff-299">sparkJobLinkedService</span></span> | <span data-ttu-id="eadff-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span><span class="sxs-lookup"><span data-stu-id="eadff-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="eadff-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span><span class="sxs-lookup"><span data-stu-id="eadff-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="eadff-302">No</span><span class="sxs-lookup"><span data-stu-id="eadff-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="eadff-303">Folder structure</span><span class="sxs-lookup"><span data-stu-id="eadff-303">Folder structure</span></span>
<span data-ttu-id="eadff-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span><span class="sxs-lookup"><span data-stu-id="eadff-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="eadff-305">Spark jobs are also more extensible than Pig/Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="eadff-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="eadff-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span><span class="sxs-lookup"><span data-stu-id="eadff-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="eadff-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="eadff-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="eadff-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="eadff-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="eadff-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span><span class="sxs-lookup"><span data-stu-id="eadff-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="eadff-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="eadff-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="eadff-311">Path</span><span class="sxs-lookup"><span data-stu-id="eadff-311">Path</span></span> | <span data-ttu-id="eadff-312">Description</span><span class="sxs-lookup"><span data-stu-id="eadff-312">Description</span></span> | <span data-ttu-id="eadff-313">Required</span><span class="sxs-lookup"><span data-stu-id="eadff-313">Required</span></span> | <span data-ttu-id="eadff-314">Type</span><span class="sxs-lookup"><span data-stu-id="eadff-314">Type</span></span> |
| ---- | ----------- | -------- | ---- | 
| <span data-ttu-id="eadff-315">.</span><span class="sxs-lookup"><span data-stu-id="eadff-315">.</span></span> | <span data-ttu-id="eadff-316">The root path of the Spark job in the storage linked service</span><span class="sxs-lookup"><span data-stu-id="eadff-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="eadff-317">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-317">Yes</span></span> | <span data-ttu-id="eadff-318">Folder</span><span class="sxs-lookup"><span data-stu-id="eadff-318">Folder</span></span> |
| <span data-ttu-id="eadff-319">&lt;user defined &gt;</span><span class="sxs-lookup"><span data-stu-id="eadff-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="eadff-320">The path pointing to the entry file of the Spark job</span><span class="sxs-lookup"><span data-stu-id="eadff-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="eadff-321">Yes</span><span class="sxs-lookup"><span data-stu-id="eadff-321">Yes</span></span> | <span data-ttu-id="eadff-322">File</span><span class="sxs-lookup"><span data-stu-id="eadff-322">File</span></span> | 
| <span data-ttu-id="eadff-323">./jars</span><span class="sxs-lookup"><span data-stu-id="eadff-323">./jars</span></span> | <span data-ttu-id="eadff-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span><span class="sxs-lookup"><span data-stu-id="eadff-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="eadff-325">No</span><span class="sxs-lookup"><span data-stu-id="eadff-325">No</span></span> | <span data-ttu-id="eadff-326">Folder</span><span class="sxs-lookup"><span data-stu-id="eadff-326">Folder</span></span> |
| <span data-ttu-id="eadff-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="eadff-327">./pyFiles</span></span> | <span data-ttu-id="eadff-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span><span class="sxs-lookup"><span data-stu-id="eadff-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="eadff-329">No</span><span class="sxs-lookup"><span data-stu-id="eadff-329">No</span></span> | <span data-ttu-id="eadff-330">Folder</span><span class="sxs-lookup"><span data-stu-id="eadff-330">Folder</span></span> |
| <span data-ttu-id="eadff-331">./files</span><span class="sxs-lookup"><span data-stu-id="eadff-331">./files</span></span> | <span data-ttu-id="eadff-332">All files under this folder are uploaded and placed on executor working directory</span><span class="sxs-lookup"><span data-stu-id="eadff-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="eadff-333">No</span><span class="sxs-lookup"><span data-stu-id="eadff-333">No</span></span> | <span data-ttu-id="eadff-334">Folder</span><span class="sxs-lookup"><span data-stu-id="eadff-334">Folder</span></span> |
| <span data-ttu-id="eadff-335">./archives</span><span class="sxs-lookup"><span data-stu-id="eadff-335">./archives</span></span> | <span data-ttu-id="eadff-336">All files under this folder are uncompressed</span><span class="sxs-lookup"><span data-stu-id="eadff-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="eadff-337">No</span><span class="sxs-lookup"><span data-stu-id="eadff-337">No</span></span> | <span data-ttu-id="eadff-338">Folder</span><span class="sxs-lookup"><span data-stu-id="eadff-338">Folder</span></span> |
| <span data-ttu-id="eadff-339">./logs</span><span class="sxs-lookup"><span data-stu-id="eadff-339">./logs</span></span> | <span data-ttu-id="eadff-340">The folder where logs from the Spark cluster are stored.</span><span class="sxs-lookup"><span data-stu-id="eadff-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="eadff-341">No</span><span class="sxs-lookup"><span data-stu-id="eadff-341">No</span></span> | <span data-ttu-id="eadff-342">Folder</span><span class="sxs-lookup"><span data-stu-id="eadff-342">Folder</span></span> |

<span data-ttu-id="eadff-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="eadff-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span> 

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs    
```












