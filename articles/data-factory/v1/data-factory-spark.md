---
title: Invoke Spark programs from Azure Data Factory | Microsoft Docs
description: Learn how to invoke Spark programs from an Azure data factory by using the MapReduce activity.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: ''
editor: ''
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 4c7dddcb5e39eb1f72fb59af753ab167bc44d3e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869164"
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="f73aa-103">Invoke Spark programs from Azure Data Factory pipelines</span><span class="sxs-lookup"><span data-stu-id="f73aa-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive activity](data-factory-hive-activity.md)
> * [Pig activity](data-factory-pig-activity.md)
> * [MapReduce activity](data-factory-map-reduce.md)
> * [Hadoop Streaming activity](data-factory-hadoop-streaming-activity.md)
> * [Spark activity](data-factory-spark.md)
> * [Machine Learning Batch Execution activity](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Update Resource activity](data-factory-azure-ml-update-resource-activity.md)
> * [Stored procedure activity](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md)
> * [.NET custom activity](data-factory-use-custom-activities.md)

> [!NOTE]
> This article applies to version 1 of Azure Data Factory, which is generally available. If you use the current version of the Data Factory service, see [Transform data by using the Apache Spark activity in Data Factory](../transform-data-using-spark.md).

## <a name="introduction"></a><span data-ttu-id="f73aa-116">Introduction</span><span class="sxs-lookup"><span data-stu-id="f73aa-116">Introduction</span></span>
<span data-ttu-id="f73aa-117">The Spark activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-117">The Spark activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Data Factory.</span></span> <span data-ttu-id="f73aa-118">This activity runs the specified Spark program on your Spark cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f73aa-118">This activity runs the specified Spark program on your Spark cluster in Azure HDInsight.</span></span> 

> [!IMPORTANT]
> - The Spark activity doesn't support HDInsight Spark clusters that use Azure Data Lake Store as primary storage.
> - The Spark activity supports only existing (your own) HDInsight Spark clusters. It doesn't support an on-demand HDInsight linked service.

## <a name="walkthrough-create-a-pipeline-with-a-spark-activity"></a><span data-ttu-id="f73aa-122">Walkthrough: Create a pipeline with a Spark activity</span><span class="sxs-lookup"><span data-stu-id="f73aa-122">Walkthrough: Create a pipeline with a Spark activity</span></span>
<span data-ttu-id="f73aa-123">Here are the typical steps to create a data factory pipeline with a Spark activity:</span><span class="sxs-lookup"><span data-stu-id="f73aa-123">Here are the typical steps to create a data factory pipeline with a Spark activity:</span></span> 

* <span data-ttu-id="f73aa-124">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-124">Create a data factory.</span></span>
* <span data-ttu-id="f73aa-125">Create an Azure Storage linked service to link your storage that is associated with your HDInsight Spark cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-125">Create an Azure Storage linked service to link your storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>
* <span data-ttu-id="f73aa-126">Create an HDInsight linked service to link your Spark cluster in HDInsight to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-126">Create an HDInsight linked service to link your Spark cluster in HDInsight to the data factory.</span></span>
* <span data-ttu-id="f73aa-127">Create a dataset that refers to the Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="f73aa-127">Create a dataset that refers to the Storage linked service.</span></span> <span data-ttu-id="f73aa-128">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span><span class="sxs-lookup"><span data-stu-id="f73aa-128">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span> 
* <span data-ttu-id="f73aa-129">Create a pipeline with Spark activity that refers to the HDInsight linked service you created.</span><span class="sxs-lookup"><span data-stu-id="f73aa-129">Create a pipeline with Spark activity that refers to the HDInsight linked service you created.</span></span> <span data-ttu-id="f73aa-130">The activity is configured with the dataset you created in the previous step as an output dataset.</span><span class="sxs-lookup"><span data-stu-id="f73aa-130">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="f73aa-131">The output dataset is what drives the schedule (hourly, daily).</span><span class="sxs-lookup"><span data-stu-id="f73aa-131">The output dataset is what drives the schedule (hourly, daily).</span></span> <span data-ttu-id="f73aa-132">Therefore, you must specify the output dataset even though the activity doesn't really produce an output.</span><span class="sxs-lookup"><span data-stu-id="f73aa-132">Therefore, you must specify the output dataset even though the activity doesn't really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f73aa-133">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f73aa-133">Prerequisites</span></span>
1. <span data-ttu-id="f73aa-134">Create a general-purpose storage account by following the instructions in [Create a storage account](../../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f73aa-134">Create a general-purpose storage account by following the instructions in [Create a storage account](../../storage/common/storage-quickstart-create-account.md).</span></span>

1. <span data-ttu-id="f73aa-135">Create a Spark cluster in HDInsight by following the instructions in the tutorial [Create a Spark cluster in HDInsight](../../hdinsight/spark/apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f73aa-135">Create a Spark cluster in HDInsight by following the instructions in the tutorial [Create a Spark cluster in HDInsight](../../hdinsight/spark/apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="f73aa-136">Associate the storage account you created in step 1 with this cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-136">Associate the storage account you created in step 1 with this cluster.</span></span>

1. <span data-ttu-id="f73aa-137">Download and review the Python script file **test.py** located at [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="f73aa-137">Download and review the Python script file **test.py** located at [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>

1. <span data-ttu-id="f73aa-138">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="f73aa-138">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your blob storage.</span></span> <span data-ttu-id="f73aa-139">Create the container and the folder if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="f73aa-139">Create the container and the folder if they don't exist.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="f73aa-140">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="f73aa-140">Create a data factory</span></span>
<span data-ttu-id="f73aa-141">To create a data factory, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f73aa-141">To create a data factory, follow these steps:</span></span>

1. <span data-ttu-id="f73aa-142">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f73aa-142">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="f73aa-143">Select **New** > **Data + Analytics** > **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-143">Select **New** > **Data + Analytics** > **Data Factory**.</span></span>

1. <span data-ttu-id="f73aa-144">On the **New data factory** blade, under **Name**, enter **SparkDF**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-144">On the **New data factory** blade, under **Name**, enter **SparkDF**.</span></span>

   > [!IMPORTANT]
   > The name of the Azure data factory must be globally unique. If you see the error "Data factory name SparkDF is not available," change the name of the data factory. For example, use yournameSparkDFdate, and create the data factory again. For more information on naming rules, see [Data Factory: Naming rules](data-factory-naming-rules.md).

1. <span data-ttu-id="f73aa-149">Under **Subscription**, select the Azure subscription where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="f73aa-149">Under **Subscription**, select the Azure subscription where you want the data factory to be created.</span></span>

1. <span data-ttu-id="f73aa-150">Select an existing resource group, or create an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="f73aa-150">Select an existing resource group, or create an Azure resource group.</span></span>

1. <span data-ttu-id="f73aa-151">Select the **Pin to dashboard** check box.</span><span class="sxs-lookup"><span data-stu-id="f73aa-151">Select the **Pin to dashboard** check box.</span></span>

1. <span data-ttu-id="f73aa-152">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-152">Select **Create**.</span></span>

   > [!IMPORTANT]
   > To create Data Factory instances, you must be a member of the [Data Factory contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.

1. <span data-ttu-id="f73aa-154">You see the data factory as it is created in the dashboard of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f73aa-154">You see the data factory as it is created in the dashboard of the Azure portal.</span></span>

1. <span data-ttu-id="f73aa-155">After the data factory is created, you see the **Data factory** page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-155">After the data factory is created, you see the **Data factory** page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="f73aa-156">If you don't see the **Data factory** page, select the tile for your data factory on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f73aa-156">If you don't see the **Data factory** page, select the tile for your data factory on the dashboard.</span></span>

    ![Data Factory blade](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="f73aa-158">Create linked services</span><span class="sxs-lookup"><span data-stu-id="f73aa-158">Create linked services</span></span>
<span data-ttu-id="f73aa-159">In this step, you create two linked services.</span><span class="sxs-lookup"><span data-stu-id="f73aa-159">In this step, you create two linked services.</span></span> <span data-ttu-id="f73aa-160">One service links your Spark cluster to your data factory, and the other service links your storage to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-160">One service links your Spark cluster to your data factory, and the other service links your storage to your data factory.</span></span> 

#### <a name="create-a-storage-linked-service"></a><span data-ttu-id="f73aa-161">Create a Storage linked service</span><span class="sxs-lookup"><span data-stu-id="f73aa-161">Create a Storage linked service</span></span>
<span data-ttu-id="f73aa-162">In this step, you link your storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-162">In this step, you link your storage account to your data factory.</span></span> <span data-ttu-id="f73aa-163">A dataset you create in a step later in this walkthrough refers to this linked service.</span><span class="sxs-lookup"><span data-stu-id="f73aa-163">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="f73aa-164">The HDInsight linked service that you define in the next step refers to this linked service too.</span><span class="sxs-lookup"><span data-stu-id="f73aa-164">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span> 

1. <span data-ttu-id="f73aa-165">On the **Data factory** blade, select **Author and deploy**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-165">On the **Data factory** blade, select **Author and deploy**.</span></span> <span data-ttu-id="f73aa-166">The Data Factory Editor appears.</span><span class="sxs-lookup"><span data-stu-id="f73aa-166">The Data Factory Editor appears.</span></span>

1. <span data-ttu-id="f73aa-167">Select **New data store**, and choose **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-167">Select **New data store**, and choose **Azure Storage**.</span></span>

   ![New data store](./media/data-factory-spark/new-data-store-azure-storage-menu.png)

1. <span data-ttu-id="f73aa-169">The JSON script you use to create a Storage linked service appears in the editor.</span><span class="sxs-lookup"><span data-stu-id="f73aa-169">The JSON script you use to create a Storage linked service appears in the editor.</span></span>

   ![AzureStorageLinkedService](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)

1. <span data-ttu-id="f73aa-171">Replace **account name** and **account key** with the name and access key of your storage account.</span><span class="sxs-lookup"><span data-stu-id="f73aa-171">Replace **account name** and **account key** with the name and access key of your storage account.</span></span> <span data-ttu-id="f73aa-172">To learn how to get your storage access key, see how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f73aa-172">To learn how to get your storage access key, see how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

1. <span data-ttu-id="f73aa-173">To deploy the linked service, select **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f73aa-173">To deploy the linked service, select **Deploy** on the command bar.</span></span> <span data-ttu-id="f73aa-174">After the linked service is deployed successfully, the Draft-1 window disappears.</span><span class="sxs-lookup"><span data-stu-id="f73aa-174">After the linked service is deployed successfully, the Draft-1 window disappears.</span></span> <span data-ttu-id="f73aa-175">You see **AzureStorageLinkedService** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="f73aa-175">You see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-an-hdinsight-linked-service"></a><span data-ttu-id="f73aa-176">Create an HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="f73aa-176">Create an HDInsight linked service</span></span>
<span data-ttu-id="f73aa-177">In this step, you create an HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-177">In this step, you create an HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="f73aa-178">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="f73aa-178">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span> 

1. <span data-ttu-id="f73aa-179">In the Data Factory Editor, select **More** > **New compute** > **HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-179">In the Data Factory Editor, select **More** > **New compute** > **HDInsight cluster**.</span></span>

    ![Create HDInsight linked service](media/data-factory-spark/new-hdinsight-linked-service.png)

1. <span data-ttu-id="f73aa-181">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="f73aa-181">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="f73aa-182">In the JSON editor, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f73aa-182">In the JSON editor, take the following steps:</span></span>

    <span data-ttu-id="f73aa-183">a.</span><span class="sxs-lookup"><span data-stu-id="f73aa-183">a.</span></span> <span data-ttu-id="f73aa-184">Specify the URI for the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-184">Specify the URI for the HDInsight Spark cluster.</span></span> <span data-ttu-id="f73aa-185">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="f73aa-185">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>

    <span data-ttu-id="f73aa-186">b.</span><span class="sxs-lookup"><span data-stu-id="f73aa-186">b.</span></span> <span data-ttu-id="f73aa-187">Specify the name of the user who has access to the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-187">Specify the name of the user who has access to the Spark cluster.</span></span>

    <span data-ttu-id="f73aa-188">c.</span><span class="sxs-lookup"><span data-stu-id="f73aa-188">c.</span></span> <span data-ttu-id="f73aa-189">Specify the password for the user.</span><span class="sxs-lookup"><span data-stu-id="f73aa-189">Specify the password for the user.</span></span>

    <span data-ttu-id="f73aa-190">d.</span><span class="sxs-lookup"><span data-stu-id="f73aa-190">d.</span></span> <span data-ttu-id="f73aa-191">Specify the Storage linked service that is associated with the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-191">Specify the Storage linked service that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="f73aa-192">In this example, it's AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="f73aa-192">In this example, it's AzureStorageLinkedService.</span></span>

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
    > - The Spark activity doesn't support HDInsight Spark clusters that use Azure Data Lake Store as primary storage.
    > - The Spark activity supports only existing (your own) HDInsight Spark clusters. It doesn't support an on-demand HDInsight linked service.

    <span data-ttu-id="f73aa-196">For more information about the HDInsight linked service, see [HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="f73aa-196">For more information about the HDInsight linked service, see [HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span></span>

1. <span data-ttu-id="f73aa-197">To deploy the linked service, select **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f73aa-197">To deploy the linked service, select **Deploy** on the command bar.</span></span> 

### <a name="create-the-output-dataset"></a><span data-ttu-id="f73aa-198">Create the output dataset</span><span class="sxs-lookup"><span data-stu-id="f73aa-198">Create the output dataset</span></span>
<span data-ttu-id="f73aa-199">The output dataset is what drives the schedule (hourly, daily).</span><span class="sxs-lookup"><span data-stu-id="f73aa-199">The output dataset is what drives the schedule (hourly, daily).</span></span> <span data-ttu-id="f73aa-200">Therefore, you must specify an output dataset for the Spark activity in the pipeline even though the activity doesn't produce any output.</span><span class="sxs-lookup"><span data-stu-id="f73aa-200">Therefore, you must specify an output dataset for the Spark activity in the pipeline even though the activity doesn't produce any output.</span></span> <span data-ttu-id="f73aa-201">Specifying an input dataset for the activity is optional.</span><span class="sxs-lookup"><span data-stu-id="f73aa-201">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="f73aa-202">In the Data Factory Editor, select **More** > **New dataset** > **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-202">In the Data Factory Editor, select **More** > **New dataset** > **Azure Blob storage**.</span></span>

1. <span data-ttu-id="f73aa-203">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="f73aa-203">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="f73aa-204">The JSON snippet defines a dataset called **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-204">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="f73aa-205">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-205">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="f73aa-206">As mentioned previously, this dataset is a dummy dataset.</span><span class="sxs-lookup"><span data-stu-id="f73aa-206">As mentioned previously, this dataset is a dummy dataset.</span></span> <span data-ttu-id="f73aa-207">The Spark program in this example doesn't produce any output.</span><span class="sxs-lookup"><span data-stu-id="f73aa-207">The Spark program in this example doesn't produce any output.</span></span> <span data-ttu-id="f73aa-208">The **availability** section specifies that the output dataset is produced daily.</span><span class="sxs-lookup"><span data-stu-id="f73aa-208">The **availability** section specifies that the output dataset is produced daily.</span></span> 

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
1. <span data-ttu-id="f73aa-209">To deploy the dataset, select **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f73aa-209">To deploy the dataset, select **Deploy** on the command bar.</span></span>


### <a name="create-a-pipeline"></a><span data-ttu-id="f73aa-210">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="f73aa-210">Create a pipeline</span></span>
<span data-ttu-id="f73aa-211">In this step, you create a pipeline with an HDInsightSpark activity.</span><span class="sxs-lookup"><span data-stu-id="f73aa-211">In this step, you create a pipeline with an HDInsightSpark activity.</span></span> <span data-ttu-id="f73aa-212">Currently, the output dataset is what drives the schedule, so you must create an output dataset even if the activity doesn't produce any output.</span><span class="sxs-lookup"><span data-stu-id="f73aa-212">Currently, the output dataset is what drives the schedule, so you must create an output dataset even if the activity doesn't produce any output.</span></span> <span data-ttu-id="f73aa-213">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="f73aa-213">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="f73aa-214">Therefore, no input dataset is specified in this example.</span><span class="sxs-lookup"><span data-stu-id="f73aa-214">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="f73aa-215">In the Data Factory Editor, select **More** > **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-215">In the Data Factory Editor, select **More** > **New pipeline**.</span></span>

1. <span data-ttu-id="f73aa-216">Replace the script in the Draft-1 window with the following script:</span><span class="sxs-lookup"><span data-stu-id="f73aa-216">Replace the script in the Draft-1 window with the following script:</span></span>

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
    <span data-ttu-id="f73aa-217">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="f73aa-217">Note the following points:</span></span>

    <span data-ttu-id="f73aa-218">a.</span><span class="sxs-lookup"><span data-stu-id="f73aa-218">a.</span></span> <span data-ttu-id="f73aa-219">The **type** property is set to **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-219">The **type** property is set to **HDInsightSpark**.</span></span>

    <span data-ttu-id="f73aa-220">b.</span><span class="sxs-lookup"><span data-stu-id="f73aa-220">b.</span></span> <span data-ttu-id="f73aa-221">The **rootPath** property is set to **adfspark\\pyFiles** where adfspark is the blob container and pyFiles is file folder in that container.</span><span class="sxs-lookup"><span data-stu-id="f73aa-221">The **rootPath** property is set to **adfspark\\pyFiles** where adfspark is the blob container and pyFiles is file folder in that container.</span></span> <span data-ttu-id="f73aa-222">In this example, the blob storage is the one that is associated with the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-222">In this example, the blob storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="f73aa-223">You can upload the file to a different storage account.</span><span class="sxs-lookup"><span data-stu-id="f73aa-223">You can upload the file to a different storage account.</span></span> <span data-ttu-id="f73aa-224">If you do so, create a Storage linked service to link that storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-224">If you do so, create a Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="f73aa-225">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span><span class="sxs-lookup"><span data-stu-id="f73aa-225">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="f73aa-226">For more information about this property and other properties supported by the Spark activity, see [Spark activity properties](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f73aa-226">For more information about this property and other properties supported by the Spark activity, see [Spark activity properties](#spark-activity-properties).</span></span>

    <span data-ttu-id="f73aa-227">c.</span><span class="sxs-lookup"><span data-stu-id="f73aa-227">c.</span></span> <span data-ttu-id="f73aa-228">The **entryFilePath** property is set to **test.py**, which is the Python file.</span><span class="sxs-lookup"><span data-stu-id="f73aa-228">The **entryFilePath** property is set to **test.py**, which is the Python file.</span></span>

    <span data-ttu-id="f73aa-229">d.</span><span class="sxs-lookup"><span data-stu-id="f73aa-229">d.</span></span> <span data-ttu-id="f73aa-230">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span><span class="sxs-lookup"><span data-stu-id="f73aa-230">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

    > [!IMPORTANT]
    > We recommend that you do not set this property to `Always` in a production environment unless you're troubleshooting an issue.

    <span data-ttu-id="f73aa-232">e.</span><span class="sxs-lookup"><span data-stu-id="f73aa-232">e.</span></span> <span data-ttu-id="f73aa-233">The **outputs** section has one output dataset.</span><span class="sxs-lookup"><span data-stu-id="f73aa-233">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="f73aa-234">You must specify an output dataset even if the Spark program doesn't produce any output.</span><span class="sxs-lookup"><span data-stu-id="f73aa-234">You must specify an output dataset even if the Spark program doesn't produce any output.</span></span> <span data-ttu-id="f73aa-235">The output dataset drives the schedule for the pipeline (hourly, daily).</span><span class="sxs-lookup"><span data-stu-id="f73aa-235">The output dataset drives the schedule for the pipeline (hourly, daily).</span></span> 

    <span data-ttu-id="f73aa-236">For more information about the properties supported by the Spark activity, see the section [Spark activity properties](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f73aa-236">For more information about the properties supported by the Spark activity, see the section [Spark activity properties](#spark-activity-properties).</span></span>

1. <span data-ttu-id="f73aa-237">To deploy the pipeline, select **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f73aa-237">To deploy the pipeline, select **Deploy** on the command bar.</span></span>

### <a name="monitor-a-pipeline"></a><span data-ttu-id="f73aa-238">Monitor a pipeline</span><span class="sxs-lookup"><span data-stu-id="f73aa-238">Monitor a pipeline</span></span>
1. <span data-ttu-id="f73aa-239">On the **Data factory** blade, select **Monitor & Manage** to start the monitoring application in another tab.</span><span class="sxs-lookup"><span data-stu-id="f73aa-239">On the **Data factory** blade, select **Monitor & Manage** to start the monitoring application in another tab.</span></span>

    ![Monitor & Manage tile](media/data-factory-spark/monitor-and-manage-tile.png)

1. <span data-ttu-id="f73aa-241">Change the **Start time** filter at the top to **2/1/2017**, and select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-241">Change the **Start time** filter at the top to **2/1/2017**, and select **Apply**.</span></span>

1. <span data-ttu-id="f73aa-242">Only one activity window appears because there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f73aa-242">Only one activity window appears because there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="f73aa-243">Confirm that the data slice is in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="f73aa-243">Confirm that the data slice is in the **Ready** state.</span></span>

    ![Monitor the pipeline](media/data-factory-spark/monitor-and-manage-app.png)

1. <span data-ttu-id="f73aa-245">In the **Activity windows** list, select an activity run to see details about it.</span><span class="sxs-lookup"><span data-stu-id="f73aa-245">In the **Activity windows** list, select an activity run to see details about it.</span></span> <span data-ttu-id="f73aa-246">If there is an error, you see details about it in the right pane.</span><span class="sxs-lookup"><span data-stu-id="f73aa-246">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="f73aa-247">Verify the results</span><span class="sxs-lookup"><span data-stu-id="f73aa-247">Verify the results</span></span>

1. <span data-ttu-id="f73aa-248">Start the Jupyter Notebook for your HDInsight Spark cluster by going to [this website](https://CLUSTERNAME.azurehdinsight.net/jupyter).</span><span class="sxs-lookup"><span data-stu-id="f73aa-248">Start the Jupyter Notebook for your HDInsight Spark cluster by going to [this website](https://CLUSTERNAME.azurehdinsight.net/jupyter).</span></span> <span data-ttu-id="f73aa-249">You also can open a cluster dashboard for your HDInsight Spark cluster, and then start the Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="f73aa-249">You also can open a cluster dashboard for your HDInsight Spark cluster, and then start the Jupyter Notebook.</span></span>

1. <span data-ttu-id="f73aa-250">Select **New** > **PySpark** to start a new notebook.</span><span class="sxs-lookup"><span data-stu-id="f73aa-250">Select **New** > **PySpark** to start a new notebook.</span></span>

    ![Jupyter new notebook](media/data-factory-spark/jupyter-new-book.png)

1. <span data-ttu-id="f73aa-252">Run the following command by copying and pasting the text and pressing Shift+Enter at the end of the second statement:</span><span class="sxs-lookup"><span data-stu-id="f73aa-252">Run the following command by copying and pasting the text and pressing Shift+Enter at the end of the second statement:</span></span>

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
1. <span data-ttu-id="f73aa-253">Confirm that you see the data from the hvac table.</span><span class="sxs-lookup"><span data-stu-id="f73aa-253">Confirm that you see the data from the hvac table.</span></span> 

    ![Jupyter query results](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="f73aa-255"><!-- Removed bookmark #run-a-hive-query-using-spark-sql since it doesn't exist in the target article --> For detailed instructions, see the section [Run a Spark SQL query](../../hdinsight/spark/apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f73aa-255"><!-- Removed bookmark #run-a-hive-query-using-spark-sql since it doesn't exist in the target article --> For detailed instructions, see the section [Run a Spark SQL query](../../hdinsight/spark/apache-spark-jupyter-spark-sql.md).</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="f73aa-256">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f73aa-256">Troubleshooting</span></span>
<span data-ttu-id="f73aa-257">Because you set getDebugInfo to **Always**, you see a log subfolder in the pyFiles folder in your blob container.</span><span class="sxs-lookup"><span data-stu-id="f73aa-257">Because you set getDebugInfo to **Always**, you see a log subfolder in the pyFiles folder in your blob container.</span></span> <span data-ttu-id="f73aa-258">The log file in the log folder provides additional information.</span><span class="sxs-lookup"><span data-stu-id="f73aa-258">The log file in the log folder provides additional information.</span></span> <span data-ttu-id="f73aa-259">This log file is especially useful when there is an error.</span><span class="sxs-lookup"><span data-stu-id="f73aa-259">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="f73aa-260">In a production environment, you might want to set it to **Failure**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-260">In a production environment, you might want to set it to **Failure**.</span></span>

<span data-ttu-id="f73aa-261">For further troubleshooting, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f73aa-261">For further troubleshooting, take the following steps:</span></span>


1. <span data-ttu-id="f73aa-262">Go to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="f73aa-262">Go to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN UI application](media/data-factory-spark/yarnui-application.png)

1. <span data-ttu-id="f73aa-264">Select **Logs** for one of the run attempts.</span><span class="sxs-lookup"><span data-stu-id="f73aa-264">Select **Logs** for one of the run attempts.</span></span>

    ![Application page](media/data-factory-spark/yarn-applications.png)

1. <span data-ttu-id="f73aa-266">You see the following additional error information in the log page:</span><span class="sxs-lookup"><span data-stu-id="f73aa-266">You see the following additional error information in the log page:</span></span>

    ![Log error](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="f73aa-268">The following sections provide information about the data factory entities to use Spark cluster and Spark activity in your data factory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-268">The following sections provide information about the data factory entities to use Spark cluster and Spark activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="f73aa-269">Spark activity properties</span><span class="sxs-lookup"><span data-stu-id="f73aa-269">Spark activity properties</span></span>
<span data-ttu-id="f73aa-270">Here is the sample JSON definition of a pipeline with a Spark activity:</span><span class="sxs-lookup"><span data-stu-id="f73aa-270">Here is the sample JSON definition of a pipeline with a Spark activity:</span></span> 

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

<span data-ttu-id="f73aa-271">The following table describes the JSON properties used in the JSON definition.</span><span class="sxs-lookup"><span data-stu-id="f73aa-271">The following table describes the JSON properties used in the JSON definition.</span></span>

| <span data-ttu-id="f73aa-272">Property</span><span class="sxs-lookup"><span data-stu-id="f73aa-272">Property</span></span> | <span data-ttu-id="f73aa-273">Description</span><span class="sxs-lookup"><span data-stu-id="f73aa-273">Description</span></span> | <span data-ttu-id="f73aa-274">Required</span><span class="sxs-lookup"><span data-stu-id="f73aa-274">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="f73aa-275">name</span><span class="sxs-lookup"><span data-stu-id="f73aa-275">name</span></span> | <span data-ttu-id="f73aa-276">Name of the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f73aa-276">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="f73aa-277">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-277">Yes</span></span> |
| <span data-ttu-id="f73aa-278">description</span><span class="sxs-lookup"><span data-stu-id="f73aa-278">description</span></span> | <span data-ttu-id="f73aa-279">Text that describes what the activity does.</span><span class="sxs-lookup"><span data-stu-id="f73aa-279">Text that describes what the activity does.</span></span> | <span data-ttu-id="f73aa-280">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-280">No</span></span> |
| <span data-ttu-id="f73aa-281">type</span><span class="sxs-lookup"><span data-stu-id="f73aa-281">type</span></span> | <span data-ttu-id="f73aa-282">This property must be set to HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="f73aa-282">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="f73aa-283">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-283">Yes</span></span> |
| <span data-ttu-id="f73aa-284">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f73aa-284">linkedServiceName</span></span> | <span data-ttu-id="f73aa-285">Name of the HDInsight linked service on which the Spark program runs.</span><span class="sxs-lookup"><span data-stu-id="f73aa-285">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="f73aa-286">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-286">Yes</span></span> |
| <span data-ttu-id="f73aa-287">rootPath</span><span class="sxs-lookup"><span data-stu-id="f73aa-287">rootPath</span></span> | <span data-ttu-id="f73aa-288">The blob container and folder that contains the Spark file.</span><span class="sxs-lookup"><span data-stu-id="f73aa-288">The blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="f73aa-289">The file name is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="f73aa-289">The file name is case sensitive.</span></span> | <span data-ttu-id="f73aa-290">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-290">Yes</span></span> |
| <span data-ttu-id="f73aa-291">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="f73aa-291">entryFilePath</span></span> | <span data-ttu-id="f73aa-292">Relative path to the root folder of the Spark code/package.</span><span class="sxs-lookup"><span data-stu-id="f73aa-292">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="f73aa-293">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-293">Yes</span></span> |
| <span data-ttu-id="f73aa-294">className</span><span class="sxs-lookup"><span data-stu-id="f73aa-294">className</span></span> | <span data-ttu-id="f73aa-295">Application's Java/Spark main class.</span><span class="sxs-lookup"><span data-stu-id="f73aa-295">Application's Java/Spark main class.</span></span> | <span data-ttu-id="f73aa-296">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-296">No</span></span> |
| <span data-ttu-id="f73aa-297">arguments</span><span class="sxs-lookup"><span data-stu-id="f73aa-297">arguments</span></span> | <span data-ttu-id="f73aa-298">A list of command-line arguments to the Spark program.</span><span class="sxs-lookup"><span data-stu-id="f73aa-298">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="f73aa-299">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-299">No</span></span> |
| <span data-ttu-id="f73aa-300">proxyUser</span><span class="sxs-lookup"><span data-stu-id="f73aa-300">proxyUser</span></span> | <span data-ttu-id="f73aa-301">The user account to impersonate to execute the Spark program.</span><span class="sxs-lookup"><span data-stu-id="f73aa-301">The user account to impersonate to execute the Spark program.</span></span> | <span data-ttu-id="f73aa-302">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-302">No</span></span> |
| <span data-ttu-id="f73aa-303">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="f73aa-303">sparkConfig</span></span> | <span data-ttu-id="f73aa-304">Specify values for the Spark configuration properties listed in [Spark configuration: Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="f73aa-304">Specify values for the Spark configuration properties listed in [Spark configuration: Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="f73aa-305">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-305">No</span></span> |
| <span data-ttu-id="f73aa-306">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="f73aa-306">getDebugInfo</span></span> | <span data-ttu-id="f73aa-307">Specifies when the Spark log files are copied to the storage used by the HDInsight cluster (or) specified by sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="f73aa-307">Specifies when the Spark log files are copied to the storage used by the HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="f73aa-308">Allowed values are None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="f73aa-308">Allowed values are None, Always, or Failure.</span></span> <span data-ttu-id="f73aa-309">The default value is None.</span><span class="sxs-lookup"><span data-stu-id="f73aa-309">The default value is None.</span></span> | <span data-ttu-id="f73aa-310">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-310">No</span></span> |
| <span data-ttu-id="f73aa-311">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="f73aa-311">sparkJobLinkedService</span></span> | <span data-ttu-id="f73aa-312">The Storage linked service that holds the Spark job file, dependencies, and logs.</span><span class="sxs-lookup"><span data-stu-id="f73aa-312">The Storage linked service that holds the Spark job file, dependencies, and logs.</span></span> <span data-ttu-id="f73aa-313">If you don't specify a value for this property, the storage associated with the HDInsight cluster is used.</span><span class="sxs-lookup"><span data-stu-id="f73aa-313">If you don't specify a value for this property, the storage associated with the HDInsight cluster is used.</span></span> | <span data-ttu-id="f73aa-314">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-314">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="f73aa-315">Folder structure</span><span class="sxs-lookup"><span data-stu-id="f73aa-315">Folder structure</span></span>
<span data-ttu-id="f73aa-316">The Spark activity doesn't support an inline script as Pig and Hive activities do.</span><span class="sxs-lookup"><span data-stu-id="f73aa-316">The Spark activity doesn't support an inline script as Pig and Hive activities do.</span></span> <span data-ttu-id="f73aa-317">Spark jobs are also more extensible than Pig/Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="f73aa-317">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="f73aa-318">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), Python files (placed on the PYTHONPATH), and any other files.</span><span class="sxs-lookup"><span data-stu-id="f73aa-318">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), Python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="f73aa-319">Create the following folder structure in the blob storage referenced by the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="f73aa-319">Create the following folder structure in the blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="f73aa-320">Then, upload dependent files to the appropriate subfolders in the root folder represented by **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="f73aa-320">Then, upload dependent files to the appropriate subfolders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="f73aa-321">For example, upload Python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span><span class="sxs-lookup"><span data-stu-id="f73aa-321">For example, upload Python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="f73aa-322">At runtime, the Data Factory service expects the following folder structure in the blob storage:</span><span class="sxs-lookup"><span data-stu-id="f73aa-322">At runtime, the Data Factory service expects the following folder structure in the blob storage:</span></span> 

| <span data-ttu-id="f73aa-323">Path</span><span class="sxs-lookup"><span data-stu-id="f73aa-323">Path</span></span> | <span data-ttu-id="f73aa-324">Description</span><span class="sxs-lookup"><span data-stu-id="f73aa-324">Description</span></span> | <span data-ttu-id="f73aa-325">Required</span><span class="sxs-lookup"><span data-stu-id="f73aa-325">Required</span></span> | <span data-ttu-id="f73aa-326">Type</span><span class="sxs-lookup"><span data-stu-id="f73aa-326">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="f73aa-327">.</span><span class="sxs-lookup"><span data-stu-id="f73aa-327">.</span></span> | <span data-ttu-id="f73aa-328">The root path of the Spark job in the storage linked service.</span><span class="sxs-lookup"><span data-stu-id="f73aa-328">The root path of the Spark job in the storage linked service.</span></span> | <span data-ttu-id="f73aa-329">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-329">Yes</span></span> | <span data-ttu-id="f73aa-330">Folder</span><span class="sxs-lookup"><span data-stu-id="f73aa-330">Folder</span></span> |
| <span data-ttu-id="f73aa-331">&lt;user defined &gt;</span><span class="sxs-lookup"><span data-stu-id="f73aa-331">&lt;user defined &gt;</span></span> | <span data-ttu-id="f73aa-332">The path that points to the entry file of the Spark job.</span><span class="sxs-lookup"><span data-stu-id="f73aa-332">The path that points to the entry file of the Spark job.</span></span> | <span data-ttu-id="f73aa-333">Yes</span><span class="sxs-lookup"><span data-stu-id="f73aa-333">Yes</span></span> | <span data-ttu-id="f73aa-334">File</span><span class="sxs-lookup"><span data-stu-id="f73aa-334">File</span></span> |
| <span data-ttu-id="f73aa-335">./jars</span><span class="sxs-lookup"><span data-stu-id="f73aa-335">./jars</span></span> | <span data-ttu-id="f73aa-336">All files under this folder are uploaded and placed on the Java classpath of the cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-336">All files under this folder are uploaded and placed on the Java classpath of the cluster.</span></span> | <span data-ttu-id="f73aa-337">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-337">No</span></span> | <span data-ttu-id="f73aa-338">Folder</span><span class="sxs-lookup"><span data-stu-id="f73aa-338">Folder</span></span> |
| <span data-ttu-id="f73aa-339">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="f73aa-339">./pyFiles</span></span> | <span data-ttu-id="f73aa-340">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster.</span><span class="sxs-lookup"><span data-stu-id="f73aa-340">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster.</span></span> | <span data-ttu-id="f73aa-341">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-341">No</span></span> | <span data-ttu-id="f73aa-342">Folder</span><span class="sxs-lookup"><span data-stu-id="f73aa-342">Folder</span></span> |
| <span data-ttu-id="f73aa-343">./files</span><span class="sxs-lookup"><span data-stu-id="f73aa-343">./files</span></span> | <span data-ttu-id="f73aa-344">All files under this folder are uploaded and placed on the executor working directory.</span><span class="sxs-lookup"><span data-stu-id="f73aa-344">All files under this folder are uploaded and placed on the executor working directory.</span></span> | <span data-ttu-id="f73aa-345">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-345">No</span></span> | <span data-ttu-id="f73aa-346">Folder</span><span class="sxs-lookup"><span data-stu-id="f73aa-346">Folder</span></span> |
| <span data-ttu-id="f73aa-347">./archives</span><span class="sxs-lookup"><span data-stu-id="f73aa-347">./archives</span></span> | <span data-ttu-id="f73aa-348">All files under this folder are uncompressed.</span><span class="sxs-lookup"><span data-stu-id="f73aa-348">All files under this folder are uncompressed.</span></span> | <span data-ttu-id="f73aa-349">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-349">No</span></span> | <span data-ttu-id="f73aa-350">Folder</span><span class="sxs-lookup"><span data-stu-id="f73aa-350">Folder</span></span> |
| <span data-ttu-id="f73aa-351">./logs</span><span class="sxs-lookup"><span data-stu-id="f73aa-351">./logs</span></span> | <span data-ttu-id="f73aa-352">The folder where logs from the Spark cluster are stored.</span><span class="sxs-lookup"><span data-stu-id="f73aa-352">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="f73aa-353">No</span><span class="sxs-lookup"><span data-stu-id="f73aa-353">No</span></span> | <span data-ttu-id="f73aa-354">Folder</span><span class="sxs-lookup"><span data-stu-id="f73aa-354">Folder</span></span> |

<span data-ttu-id="f73aa-355">Here is an example for storage that contains two Spark job files in the blob storage referenced by the HDInsight linked service:</span><span class="sxs-lookup"><span data-stu-id="f73aa-355">Here is an example for storage that contains two Spark job files in the blob storage referenced by the HDInsight linked service:</span></span>

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
