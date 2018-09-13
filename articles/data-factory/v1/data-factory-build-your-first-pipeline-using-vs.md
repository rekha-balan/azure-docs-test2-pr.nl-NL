---
title: Build your first data factory (Visual Studio) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using Visual Studio.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.custom: vs-azure
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: ba12f22a7f0ac26ac2b9f29bb3a33a54d2705df3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865555"
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="d7bf5-103">Tutorial: Create a data factory by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d7bf5-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Quickstart: Create a data factory using Azure Data Factory](../quickstart-create-data-factory-dot-net.md).

<span data-ttu-id="d7bf5-112">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-112">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="d7bf5-113">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-113">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span></span> 

<span data-ttu-id="d7bf5-114">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-114">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="d7bf5-115">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-115">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="d7bf5-116">The pipeline is scheduled to run once a month between the specified start and end times.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-116">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> This tutorial does not show how copy data by using Azure Data Factory. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> A pipeline can have more than one activity. And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="d7bf5-122">Walkthrough: Create and publish Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="d7bf5-122">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="d7bf5-123">Here are the steps you perform as part of this walkthrough:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-123">Here are the steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="d7bf5-124">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-124">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="d7bf5-125">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-125">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span></span> <span data-ttu-id="d7bf5-126">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-126">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span></span> <span data-ttu-id="d7bf5-127">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-127">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span></span> <span data-ttu-id="d7bf5-128">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-128">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span></span> <span data-ttu-id="d7bf5-129">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-129">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="d7bf5-130">When publishing, you specify the name for the data factory to be created or an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-130">When publishing, you specify the name for the data factory to be created or an existing data factory.</span></span>  
2. <span data-ttu-id="d7bf5-131">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-131">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span></span> 
   
    <span data-ttu-id="d7bf5-132">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-132">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="d7bf5-133">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-133">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span></span> <span data-ttu-id="d7bf5-134">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-134">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span></span> <span data-ttu-id="d7bf5-135">You also specify other properties such as structure, availability, and policy.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-135">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="d7bf5-136">Create a pipeline named **MyFirstPipeline**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-136">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="d7bf5-137">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-137">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="d7bf5-138">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-138">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d7bf5-139">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="d7bf5-139">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="d7bf5-140">Create a data factory named **DataFactoryUsingVS**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-140">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="d7bf5-141">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-141">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>
5. <span data-ttu-id="d7bf5-142">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-142">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="d7bf5-143">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d7bf5-143">Prerequisites</span></span>
1. <span data-ttu-id="d7bf5-144">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-144">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span> <span data-ttu-id="d7bf5-145">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-145">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span></span> <span data-ttu-id="d7bf5-146">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-146">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span></span>
2. <span data-ttu-id="d7bf5-147">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-147">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>  
3. <span data-ttu-id="d7bf5-148">You must have the following installed on your computer:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-148">You must have the following installed on your computer:</span></span>
   * <span data-ttu-id="d7bf5-149">Visual Studio 2013 or Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d7bf5-149">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="d7bf5-150">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-150">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="d7bf5-151">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-151">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="d7bf5-152">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-152">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="d7bf5-153">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-153">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="d7bf5-154">Now, let's use Visual Studio to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-154">Now, let's use Visual Studio to create an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="d7bf5-155">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="d7bf5-155">Create Visual Studio project</span></span>
1. <span data-ttu-id="d7bf5-156">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-156">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="d7bf5-157">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-157">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="d7bf5-158">You should see the **New Project** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-158">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="d7bf5-159">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-159">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![New project dialog box](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="d7bf5-161">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-161">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>

    ![Solution Explorer](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="d7bf5-163">Create linked services</span><span class="sxs-lookup"><span data-stu-id="d7bf5-163">Create linked services</span></span>
<span data-ttu-id="d7bf5-164">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-164">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="d7bf5-165">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-165">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span></span> <span data-ttu-id="d7bf5-166">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-166">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span></span> <span data-ttu-id="d7bf5-167">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-167">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span></span> 

<span data-ttu-id="d7bf5-168">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-168">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span></span> <span data-ttu-id="d7bf5-169">The cluster is deleted after it is done processing and idle for the specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-169">The cluster is deleted after it is done processing and idle for the specified amount of time.</span></span> 

> [!NOTE]
> You create a data factory by specifying its name and settings at the time of publishing your Data Factory solution.

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="d7bf5-171">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="d7bf5-171">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="d7bf5-172">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-172">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="d7bf5-173">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-173">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span>
    <span data-ttu-id="d7bf5-174">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="d7bf5-174">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="d7bf5-175">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-175">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span></span> <span data-ttu-id="d7bf5-176">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-176">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="d7bf5-177">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="d7bf5-177">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="d7bf5-178">Save the **AzureStorageLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-178">Save the **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="d7bf5-179">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="d7bf5-179">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="d7bf5-180">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-180">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="d7bf5-181">Select **HDInsight On Demand Linked Service**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-181">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="d7bf5-182">Replace the **JSON** with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-182">Replace the **JSON** with the following JSON:</span></span>

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="d7bf5-183">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="d7bf5-184">Property</span><span class="sxs-lookup"><span data-stu-id="d7bf5-184">Property</span></span> | <span data-ttu-id="d7bf5-185">Description</span><span class="sxs-lookup"><span data-stu-id="d7bf5-185">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="d7bf5-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="d7bf5-186">ClusterSize</span></span> | <span data-ttu-id="d7bf5-187">Specifies the size of the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-187">Specifies the size of the HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="d7bf5-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="d7bf5-188">TimeToLive</span></span> | <span data-ttu-id="d7bf5-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="d7bf5-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d7bf5-190">linkedServiceName</span></span> | <span data-ttu-id="d7bf5-191">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-191">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName). HDInsight does not delete this container when the cluster is deleted. This behavior is by design. With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive). The cluster is automatically deleted when the processing is done.
    > 
    > As more slices are processed, you see many containers in your Azure blob storage. If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost. The names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.

    <span data-ttu-id="d7bf5-201">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-201">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="d7bf5-202">Save the **HDInsightOnDemandLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-202">Save the **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="d7bf5-203">Create datasets</span><span class="sxs-lookup"><span data-stu-id="d7bf5-203">Create datasets</span></span>
<span data-ttu-id="d7bf5-204">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-204">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="d7bf5-205">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-205">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="d7bf5-206">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-206">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="d7bf5-207">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="d7bf5-207">Create input dataset</span></span>
1. <span data-ttu-id="d7bf5-208">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-208">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="d7bf5-209">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-209">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="d7bf5-210">Replace the **JSON** in the editor with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-210">Replace the **JSON** in the editor with the following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="d7bf5-211">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-211">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span></span> <span data-ttu-id="d7bf5-212">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-212">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span></span>

    <span data-ttu-id="d7bf5-213">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-213">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="d7bf5-214">Property</span><span class="sxs-lookup"><span data-stu-id="d7bf5-214">Property</span></span> | <span data-ttu-id="d7bf5-215">Description</span><span class="sxs-lookup"><span data-stu-id="d7bf5-215">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="d7bf5-216">type</span><span class="sxs-lookup"><span data-stu-id="d7bf5-216">type</span></span> |<span data-ttu-id="d7bf5-217">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-217">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="d7bf5-218">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d7bf5-218">linkedServiceName</span></span> | <span data-ttu-id="d7bf5-219">Refers to the AzureStorageLinkedService1 you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-219">Refers to the AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="d7bf5-220">fileName</span><span class="sxs-lookup"><span data-stu-id="d7bf5-220">fileName</span></span> |<span data-ttu-id="d7bf5-221">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-221">This property is optional.</span></span> <span data-ttu-id="d7bf5-222">If you omit this property, all the files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-222">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="d7bf5-223">In this case, only the input.log is processed.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-223">In this case, only the input.log is processed.</span></span>
    <span data-ttu-id="d7bf5-224">type</span><span class="sxs-lookup"><span data-stu-id="d7bf5-224">type</span></span> | <span data-ttu-id="d7bf5-225">The log files are in text format, so we use TextFormat.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-225">The log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="d7bf5-226">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="d7bf5-226">columnDelimiter</span></span> | <span data-ttu-id="d7bf5-227">columns in the log files are delimited by the comma character (`,`)</span><span class="sxs-lookup"><span data-stu-id="d7bf5-227">columns in the log files are delimited by the comma character (`,`)</span></span>
    <span data-ttu-id="d7bf5-228">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="d7bf5-228">frequency/interval</span></span> | <span data-ttu-id="d7bf5-229">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-229">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span>
    <span data-ttu-id="d7bf5-230">external</span><span class="sxs-lookup"><span data-stu-id="d7bf5-230">external</span></span> | <span data-ttu-id="d7bf5-231">This property is set to true if the input data for the activity is not generated by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-231">This property is set to true if the input data for the activity is not generated by the pipeline.</span></span> <span data-ttu-id="d7bf5-232">This property is only specified on input datasets.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-232">This property is only specified on input datasets.</span></span> <span data-ttu-id="d7bf5-233">For the input dataset of the first activity, always set it to true.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-233">For the input dataset of the first activity, always set it to true.</span></span>
4. <span data-ttu-id="d7bf5-234">Save the **InputDataset.json** file.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-234">Save the **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="d7bf5-235">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="d7bf5-235">Create output dataset</span></span>
<span data-ttu-id="d7bf5-236">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-236">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="d7bf5-237">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-237">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="d7bf5-238">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-238">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="d7bf5-239">Replace the **JSON** in the editor with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-239">Replace the **JSON** in the editor with the following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="d7bf5-240">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-240">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span></span> <span data-ttu-id="d7bf5-241">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-241">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="d7bf5-242">The **availability** section specifies that the output dataset is produced on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-242">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="d7bf5-243">The output dataset drives the schedule of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-243">The output dataset drives the schedule of the pipeline.</span></span> <span data-ttu-id="d7bf5-244">The pipeline runs monthly between its start and end times.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-244">The pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="d7bf5-245">See **Create the input dataset** section for descriptions of these properties.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-245">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="d7bf5-246">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-246">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span></span>
4. <span data-ttu-id="d7bf5-247">Save the **OutputDataset.json** file.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-247">Save the **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="d7bf5-248">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="d7bf5-248">Create pipeline</span></span>
<span data-ttu-id="d7bf5-249">You have created the Azure Storage linked service, and input and output datasets so far.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-249">You have created the Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="d7bf5-250">Now, you create a pipeline with a **HDInsightHive** activity.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-250">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="d7bf5-251">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-251">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span></span> <span data-ttu-id="d7bf5-252">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-252">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="d7bf5-253">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span><span class="sxs-lookup"><span data-stu-id="d7bf5-253">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="d7bf5-254">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-254">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span></span>
3. <span data-ttu-id="d7bf5-255">Replace the **JSON** with the following snippet:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-255">Replace the **JSON** with the following snippet:</span></span>

    > [!IMPORTANT]
    > Replace `<storageaccountname>` with the name of your storage account.

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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

    > [!IMPORTANT]
    > Replace `<storageaccountname>` with the name of your storage account.

    <span data-ttu-id="d7bf5-258">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-258">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="d7bf5-259">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-259">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span></span> <span data-ttu-id="d7bf5-260">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-260">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span></span> 

    <span data-ttu-id="d7bf5-261">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-261">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span></span> 

    <span data-ttu-id="d7bf5-262">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-262">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span></span>

    <span data-ttu-id="d7bf5-263">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-263">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="d7bf5-264">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-264">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span> <span data-ttu-id="d7bf5-265">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-265">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span></span>

    <span data-ttu-id="d7bf5-266">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-266">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="d7bf5-267">Save the **HiveActivity1.json** file.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-267">Save the **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="d7bf5-268">Add partitionweblogs.hql and input.log as a dependency</span><span class="sxs-lookup"><span data-stu-id="d7bf5-268">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="d7bf5-269">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-269">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="d7bf5-270">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-270">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="d7bf5-271">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-271">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="d7bf5-272">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-272">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="d7bf5-273">Publish/deploy Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="d7bf5-273">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="d7bf5-274">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-274">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span></span> <span data-ttu-id="d7bf5-275">In the process of publishing, you specify the name for your data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-275">In the process of publishing, you specify the name for your data factory.</span></span> 

1. <span data-ttu-id="d7bf5-276">Right-click project in the Solution Explorer, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-276">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="d7bf5-277">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-277">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="d7bf5-278">You should see the following dialog box:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-278">You should see the following dialog box:</span></span>

   ![Publish dialog box](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="d7bf5-280">In the **Configure data factory** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-280">In the **Configure data factory** page, do the following steps:</span></span>

    ![Publish - New data factory settings](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="d7bf5-282">select **Create New Data Factory** option.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-282">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="d7bf5-283">Enter a unique **name** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-283">Enter a unique **name** for the data factory.</span></span> <span data-ttu-id="d7bf5-284">For example: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-284">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="d7bf5-285">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-285">The name must be globally unique.</span></span>
   3. <span data-ttu-id="d7bf5-286">Select the right subscription for the **Subscription** field.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-286">Select the right subscription for the **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.
   4. <span data-ttu-id="d7bf5-288">Select the **resource group** for the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-288">Select the **resource group** for the data factory to be created.</span></span>
   5. <span data-ttu-id="d7bf5-289">Select the **region** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-289">Select the **region** for the data factory.</span></span>
   6. <span data-ttu-id="d7bf5-290">Click **Next** to switch to the **Publish Items** page.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-290">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="d7bf5-291">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span><span class="sxs-lookup"><span data-stu-id="d7bf5-291">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > If you receive the error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change the name (for example, yournameDataFactoryUsingVS). See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.   
1. <span data-ttu-id="d7bf5-294">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-294">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>

    ![Publish items page](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="d7bf5-296">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-296">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>

    ![Summary page](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="d7bf5-298">In the **Deployment Status** page, you should see the status of the deployment process.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-298">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="d7bf5-299">Click Finish after the deployment is done.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-299">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="d7bf5-300">Important points to note:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-300">Important points to note:</span></span>

- <span data-ttu-id="d7bf5-301">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-301">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span></span>
    - <span data-ttu-id="d7bf5-302">In Azure PowerShell, run the following command to register the Data Factory provider.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-302">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="d7bf5-303">You can run the following command to confirm that the Data Factory provider is registered.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-303">You can run the following command to confirm that the Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="d7bf5-304">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-304">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="d7bf5-305">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-305">This action automatically registers the provider for you.</span></span>
- <span data-ttu-id="d7bf5-306">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-306">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
- <span data-ttu-id="d7bf5-307">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d7bf5-307">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="d7bf5-308">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="d7bf5-308">Monitor pipeline</span></span>
<span data-ttu-id="d7bf5-309">In this step, you monitor the pipeline using Diagram View of the data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-309">In this step, you monitor the pipeline using Diagram View of the data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="d7bf5-310">Monitor pipeline using Diagram View</span><span class="sxs-lookup"><span data-stu-id="d7bf5-310">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="d7bf5-311">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-311">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>
   1. <span data-ttu-id="d7bf5-312">Click **More services** and click **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-312">Click **More services** and click **Data factories**.</span></span>
       
        ![Browse data factories](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="d7bf5-314">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-314">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span></span>
   
       ![Select your data factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="d7bf5-316">In the home page for your data factory, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-316">In the home page for your data factory, click **Diagram**.</span></span>

    ![Diagram tile](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="d7bf5-318">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-318">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diagram View](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="d7bf5-320">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-320">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Open pipeline menu](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="d7bf5-322">Confirm that you see the HDInsightHive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-322">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Open pipeline view](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="d7bf5-324">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-324">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
6. <span data-ttu-id="d7bf5-325">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-325">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="d7bf5-326">Confirm that the slice is in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-326">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="d7bf5-327">It may take a couple of minutes for the slice to show up in Ready state.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-327">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="d7bf5-328">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-328">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="d7bf5-329">And, make sure that the **external** property on the input dataset is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-329">And, make sure that the **external** property on the input dataset is set to **true**.</span></span> 

   ![Input slice in ready state](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="d7bf5-331">Click **X** to close **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-331">Click **X** to close **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="d7bf5-332">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-332">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="d7bf5-333">You see that the slice that is currently being processed.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-333">You see that the slice that is currently being processed.</span></span>

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="d7bf5-335">When processing is done, you see the slice in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-335">When processing is done, you see the slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes). Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.  
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="d7bf5-339">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-339">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span></span>  

    ![output data](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="d7bf5-341">Click the slice to see details about it in a **Data slice** blade.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-341">Click the slice to see details about it in a **Data slice** blade.</span></span>

    ![Data slice details](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="d7bf5-343">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-343">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Activity run details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="d7bf5-345">From the log files, you can see the Hive query that was executed and status information.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-345">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="d7bf5-346">These logs are useful for troubleshooting any issues.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-346">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="d7bf5-347">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-347">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="d7bf5-348">Monitor pipeline using Monitor & Manage App</span><span class="sxs-lookup"><span data-stu-id="d7bf5-348">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="d7bf5-349">You can also use Monitor & Manage application to monitor your pipelines.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-349">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="d7bf5-350">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-350">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="d7bf5-351">Click Monitor & Manage tile.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-351">Click Monitor & Manage tile.</span></span>

    ![Monitor & Manage tile](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="d7bf5-353">You should see Monitor & Manage application.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-353">You should see Monitor & Manage application.</span></span> <span data-ttu-id="d7bf5-354">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-354">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![Monitor & Manage App](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="d7bf5-356">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-356">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span></span>
    <span data-ttu-id="d7bf5-357">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="d7bf5-357">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the `inputdata` folder of the `adfgetstarted` container.

### <a name="additional-notes"></a><span data-ttu-id="d7bf5-360">Additional notes</span><span class="sxs-lookup"><span data-stu-id="d7bf5-360">Additional notes</span></span>
- <span data-ttu-id="d7bf5-361">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-361">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="d7bf5-362">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-362">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="d7bf5-363">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-363">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="d7bf5-364">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-364">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="d7bf5-365">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-365">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="d7bf5-366">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-366">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="d7bf5-367">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-367">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="d7bf5-368">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-368">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="d7bf5-369">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-369">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span></span>
- <span data-ttu-id="d7bf5-370">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-370">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d7bf5-371">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-371">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="d7bf5-372">The Data Factory creates a **Linux-based** HDInsight cluster for you with the preceding JSON.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-372">The Data Factory creates a **Linux-based** HDInsight cluster for you with the preceding JSON.</span></span> <span data-ttu-id="d7bf5-373">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-373">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="d7bf5-374">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-374">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="d7bf5-375">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-375">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="d7bf5-376">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-376">This behavior is by design.</span></span> <span data-ttu-id="d7bf5-377">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-377">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="d7bf5-378">The cluster is automatically deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-378">The cluster is automatically deleted when the processing is done.</span></span>
    
    <span data-ttu-id="d7bf5-379">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-379">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="d7bf5-380">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-380">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="d7bf5-381">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-381">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="d7bf5-382">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-382">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="d7bf5-383">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-383">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="d7bf5-384">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-384">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 
- <span data-ttu-id="d7bf5-385">This tutorial does not show how copy data by using Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-385">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="d7bf5-386">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-386">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="d7bf5-387">Use Server Explorer to view data factories</span><span class="sxs-lookup"><span data-stu-id="d7bf5-387">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="d7bf5-388">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-388">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="d7bf5-389">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-389">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="d7bf5-390">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-390">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="d7bf5-391">Enter **password**, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-391">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="d7bf5-392">Visual Studio tries to get information about all Azure data factories in your subscription.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-392">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="d7bf5-393">You see the status of this operation in the **Data Factory Task List** window.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-393">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="d7bf5-395">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-395">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Export data factory](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="d7bf5-397">Update Data Factory tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d7bf5-397">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="d7bf5-398">To update Azure Data Factory tools for Visual Studio, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-398">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="d7bf5-399">Click **Tools** on the menu and select **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-399">Click **Tools** on the menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="d7bf5-400">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-400">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="d7bf5-401">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-401">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="d7bf5-402">If you do not see this entry, you already have the latest version of the tools.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-402">If you do not see this entry, you already have the latest version of the tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="d7bf5-403">Use configuration files</span><span class="sxs-lookup"><span data-stu-id="d7bf5-403">Use configuration files</span></span>
<span data-ttu-id="d7bf5-404">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-404">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="d7bf5-405">Consider the following JSON definition for an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-405">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="d7bf5-406">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-406">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="d7bf5-407">You can achieve this behavior by using separate configuration file for each environment.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-407">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="d7bf5-408">Add a configuration file</span><span class="sxs-lookup"><span data-stu-id="d7bf5-408">Add a configuration file</span></span>
<span data-ttu-id="d7bf5-409">Add a configuration file for each environment by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-409">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="d7bf5-410">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-410">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="d7bf5-411">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-411">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Add configuration file](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="d7bf5-413">Add configuration parameters and their values in the following format:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-413">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:<Azure sql server name>.database.windows.net,1433;Database=<Azure Sql database>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="d7bf5-414">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-414">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="d7bf5-415">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-415">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="d7bf5-416">If JSON has a property that has an array of values as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-416">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="d7bf5-417">Configure properties as shown in the following configuration file (use zero-based indexing):</span><span class="sxs-lookup"><span data-stu-id="d7bf5-417">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="d7bf5-418">Property names with spaces</span><span class="sxs-lookup"><span data-stu-id="d7bf5-418">Property names with spaces</span></span>
<span data-ttu-id="d7bf5-419">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span><span class="sxs-lookup"><span data-stu-id="d7bf5-419">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="d7bf5-420">Deploy solution using a configuration</span><span class="sxs-lookup"><span data-stu-id="d7bf5-420">Deploy solution using a configuration</span></span>
<span data-ttu-id="d7bf5-421">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-421">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="d7bf5-422">To publish entities in an Azure Data Factory project using configuration file:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-422">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="d7bf5-423">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-423">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="d7bf5-424">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-424">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="d7bf5-425">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-425">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Select config file](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="d7bf5-427">Select the **configuration file** that you would like to use and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-427">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="d7bf5-428">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-428">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="d7bf5-429">Click **Finish** after the deployment operation is finished.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-429">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="d7bf5-430">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-430">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="d7bf5-431">Use Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d7bf5-431">Use Azure Key Vault</span></span>
<span data-ttu-id="d7bf5-432">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-432">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="d7bf5-433">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-433">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="d7bf5-434">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-434">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="d7bf5-435">These references are resolved when you publish Data Factory entities to Azure.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-435">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="d7bf5-436">These files can then be committed to source repository without exposing any secrets.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-436">These files can then be committed to source repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="d7bf5-437">Summary</span><span class="sxs-lookup"><span data-stu-id="d7bf5-437">Summary</span></span>
<span data-ttu-id="d7bf5-438">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-438">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="d7bf5-439">You used the Data Factory Editor in the Azure portal to do the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-439">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="d7bf5-440">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-440">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="d7bf5-441">Created two **linked services**:</span><span class="sxs-lookup"><span data-stu-id="d7bf5-441">Created two **linked services**:</span></span>
   1. <span data-ttu-id="d7bf5-442">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-442">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="d7bf5-443">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-443">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="d7bf5-444">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-444">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="d7bf5-445">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-445">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="d7bf5-446">Created a **pipeline** with a **HDInsight Hive** activity.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-446">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d7bf5-447">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d7bf5-447">Next Steps</span></span>
<span data-ttu-id="d7bf5-448">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-448">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d7bf5-449">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d7bf5-449">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="d7bf5-450">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-450">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="d7bf5-451">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-451">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="d7bf5-452">See Also</span><span class="sxs-lookup"><span data-stu-id="d7bf5-452">See Also</span></span>
| <span data-ttu-id="d7bf5-453">Topic</span><span class="sxs-lookup"><span data-stu-id="d7bf5-453">Topic</span></span> | <span data-ttu-id="d7bf5-454">Description</span><span class="sxs-lookup"><span data-stu-id="d7bf5-454">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="d7bf5-455">Pipelines</span><span class="sxs-lookup"><span data-stu-id="d7bf5-455">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="d7bf5-456">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-456">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="d7bf5-457">Datasets</span><span class="sxs-lookup"><span data-stu-id="d7bf5-457">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="d7bf5-458">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-458">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="d7bf5-459">Data Transformation Activities</span><span class="sxs-lookup"><span data-stu-id="d7bf5-459">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="d7bf5-460">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-460">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="d7bf5-461">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="d7bf5-461">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="d7bf5-462">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-462">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="d7bf5-463">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="d7bf5-463">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="d7bf5-464">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="d7bf5-464">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
