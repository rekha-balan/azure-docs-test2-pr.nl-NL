---
title: Build your first data factory (Visual Studio) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using Visual Studio.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/06/2017
ms.author: spelluru
ms.openlocfilehash: 6d4d5d23007ea518dfe224a4ec20eabc17a38475
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552225"
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="83d99-103">Tutorial: Create a data factory by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83d99-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="83d99-110">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83d99-110">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="83d99-111">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span><span class="sxs-lookup"><span data-stu-id="83d99-111">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span></span> 

<span data-ttu-id="83d99-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span><span class="sxs-lookup"><span data-stu-id="83d99-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="83d99-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="83d99-114">The pipeline is scheduled to run once a month between the specified start and end times.</span><span class="sxs-lookup"><span data-stu-id="83d99-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> This tutorial does not show how copy data by using Azure Data Factory. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="83d99-117">Walkthrough: Create and publish Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="83d99-117">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="83d99-118">Here are the steps you perform as part of this walkthrough:</span><span class="sxs-lookup"><span data-stu-id="83d99-118">Here are the steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="83d99-119">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="83d99-119">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="83d99-120">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="83d99-120">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span></span> <span data-ttu-id="83d99-121">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-121">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span></span> <span data-ttu-id="83d99-122">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span><span class="sxs-lookup"><span data-stu-id="83d99-122">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span></span> <span data-ttu-id="83d99-123">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span><span class="sxs-lookup"><span data-stu-id="83d99-123">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span></span> <span data-ttu-id="83d99-124">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="83d99-124">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="83d99-125">When publishing, you specify the name for the data factory to be created or an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-125">When publishing, you specify the name for the data factory to be created or an existing data factory.</span></span>  
2. <span data-ttu-id="83d99-126">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="83d99-126">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span></span> 
   
    <span data-ttu-id="83d99-127">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="83d99-127">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="83d99-128">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span><span class="sxs-lookup"><span data-stu-id="83d99-128">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span></span> <span data-ttu-id="83d99-129">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-129">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span></span> <span data-ttu-id="83d99-130">You also specify other properties such as structure, availability, and policy.</span><span class="sxs-lookup"><span data-stu-id="83d99-130">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="83d99-131">Create a pipeline named **MyFirstPipeline**.</span><span class="sxs-lookup"><span data-stu-id="83d99-131">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="83d99-132">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span><span class="sxs-lookup"><span data-stu-id="83d99-132">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="83d99-133">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-133">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="83d99-134">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="83d99-134">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="83d99-135">Create a data factory named **DataFactoryUsingVS**.</span><span class="sxs-lookup"><span data-stu-id="83d99-135">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="83d99-136">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span><span class="sxs-lookup"><span data-stu-id="83d99-136">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>
5. <span data-ttu-id="83d99-137">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-137">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="83d99-138">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="83d99-138">Prerequisites</span></span>
1. <span data-ttu-id="83d99-139">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="83d99-139">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span> <span data-ttu-id="83d99-140">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span><span class="sxs-lookup"><span data-stu-id="83d99-140">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span></span> <span data-ttu-id="83d99-141">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="83d99-141">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span></span>  
2. <span data-ttu-id="83d99-142">You must be an **administrator of the Azure subscription** to be able to publish Data Factory entities from Visual Studio to Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-142">You must be an **administrator of the Azure subscription** to be able to publish Data Factory entities from Visual Studio to Azure Data Factory.</span></span> 
3. <span data-ttu-id="83d99-143">You must have the following installed on your computer:</span><span class="sxs-lookup"><span data-stu-id="83d99-143">You must have the following installed on your computer:</span></span>
   * <span data-ttu-id="83d99-144">Visual Studio 2013 or Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="83d99-144">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="83d99-145">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="83d99-145">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="83d99-146">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span><span class="sxs-lookup"><span data-stu-id="83d99-146">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="83d99-147">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="83d99-147">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="83d99-148">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span><span class="sxs-lookup"><span data-stu-id="83d99-148">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="83d99-149">Now, let's use Visual Studio to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-149">Now, let's use Visual Studio to create an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="83d99-150">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="83d99-150">Create Visual Studio project</span></span>
1. <span data-ttu-id="83d99-151">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="83d99-151">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="83d99-152">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="83d99-152">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="83d99-153">You should see the **New Project** dialog box.</span><span class="sxs-lookup"><span data-stu-id="83d99-153">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="83d99-154">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="83d99-154">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![New project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="83d99-156">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="83d99-156">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>

    ![Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="83d99-158">Create linked services</span><span class="sxs-lookup"><span data-stu-id="83d99-158">Create linked services</span></span>
<span data-ttu-id="83d99-159">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span><span class="sxs-lookup"><span data-stu-id="83d99-159">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="83d99-160">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span><span class="sxs-lookup"><span data-stu-id="83d99-160">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span></span> <span data-ttu-id="83d99-161">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span><span class="sxs-lookup"><span data-stu-id="83d99-161">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span></span> <span data-ttu-id="83d99-162">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span><span class="sxs-lookup"><span data-stu-id="83d99-162">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span></span> 

<span data-ttu-id="83d99-163">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span><span class="sxs-lookup"><span data-stu-id="83d99-163">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span></span> <span data-ttu-id="83d99-164">The cluster is deleted after it is done processing and idle for the specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="83d99-164">The cluster is deleted after it is done processing and idle for the specified amount of time.</span></span> 

> [!NOTE]
> You create a data factory by specifying its name and settings at the time of publishing your Data Factory solution.

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="83d99-166">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="83d99-166">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="83d99-167">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="83d99-167">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="83d99-168">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-168">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span>
    <span data-ttu-id="83d99-169">![Azure Storage Linked Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="83d99-169">![Azure Storage Linked Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="83d99-170">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span><span class="sxs-lookup"><span data-stu-id="83d99-170">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span></span> <span data-ttu-id="83d99-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="83d99-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="83d99-172">![Azure Storage Linked Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="83d99-172">![Azure Storage Linked Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="83d99-173">Save the **AzureStorageLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="83d99-173">Save the **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="83d99-174">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="83d99-174">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="83d99-175">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="83d99-175">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="83d99-176">Select **HDInsight On Demand Linked Service**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-176">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="83d99-177">Replace the **JSON** with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="83d99-177">Replace the **JSON** with the following JSON:</span></span>

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.2",
                "clusterSize": 1,
                "timeToLive": "00:30:00",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="83d99-178">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="83d99-178">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="83d99-179">Property</span><span class="sxs-lookup"><span data-stu-id="83d99-179">Property</span></span> | <span data-ttu-id="83d99-180">Description</span><span class="sxs-lookup"><span data-stu-id="83d99-180">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="83d99-181">Version</span><span class="sxs-lookup"><span data-stu-id="83d99-181">Version</span></span> | <span data-ttu-id="83d99-182">Specifies that the version of the HDInsight Hadoop cluster to be created.</span><span class="sxs-lookup"><span data-stu-id="83d99-182">Specifies that the version of the HDInsight Hadoop cluster to be created.</span></span>
    <span data-ttu-id="83d99-183">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="83d99-183">ClusterSize</span></span> | <span data-ttu-id="83d99-184">Specifies the size of the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-184">Specifies the size of the HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="83d99-185">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="83d99-185">TimeToLive</span></span> | <span data-ttu-id="83d99-186">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="83d99-186">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="83d99-187">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="83d99-187">linkedServiceName</span></span> | <span data-ttu-id="83d99-188">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-188">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName). HDInsight does not delete this container when the cluster is deleted. This behavior is by design. With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive). The cluster is automatically deleted when the processing is done.
    > 
    > As more slices are processed, you see many containers in your Azure blob storage. If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost. The names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.

    <span data-ttu-id="83d99-198">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span><span class="sxs-lookup"><span data-stu-id="83d99-198">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="83d99-199">Save the **HDInsightOnDemandLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="83d99-199">Save the **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="83d99-200">Create datasets</span><span class="sxs-lookup"><span data-stu-id="83d99-200">Create datasets</span></span>
<span data-ttu-id="83d99-201">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="83d99-201">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="83d99-202">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="83d99-202">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="83d99-203">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-203">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="83d99-204">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="83d99-204">Create input dataset</span></span>
1. <span data-ttu-id="83d99-205">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="83d99-205">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="83d99-206">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-206">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="83d99-207">Replace the **JSON** in the editor with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="83d99-207">Replace the **JSON** in the editor with the following JSON snippet:</span></span>

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
    <span data-ttu-id="83d99-208">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-208">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span></span> <span data-ttu-id="83d99-209">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="83d99-209">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span></span>

    <span data-ttu-id="83d99-210">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="83d99-210">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="83d99-211">Property</span><span class="sxs-lookup"><span data-stu-id="83d99-211">Property</span></span> | <span data-ttu-id="83d99-212">Description</span><span class="sxs-lookup"><span data-stu-id="83d99-212">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="83d99-213">type</span><span class="sxs-lookup"><span data-stu-id="83d99-213">type</span></span> |<span data-ttu-id="83d99-214">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="83d99-214">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="83d99-215">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="83d99-215">linkedServiceName</span></span> | <span data-ttu-id="83d99-216">Refers to the AzureStorageLinkedService1 you created earlier.</span><span class="sxs-lookup"><span data-stu-id="83d99-216">Refers to the AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="83d99-217">fileName</span><span class="sxs-lookup"><span data-stu-id="83d99-217">fileName</span></span> |<span data-ttu-id="83d99-218">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="83d99-218">This property is optional.</span></span> <span data-ttu-id="83d99-219">If you omit this property, all the files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="83d99-219">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="83d99-220">In this case, only the input.log is processed.</span><span class="sxs-lookup"><span data-stu-id="83d99-220">In this case, only the input.log is processed.</span></span>
    <span data-ttu-id="83d99-221">type</span><span class="sxs-lookup"><span data-stu-id="83d99-221">type</span></span> | <span data-ttu-id="83d99-222">The log files are in text format, so we use TextFormat.</span><span class="sxs-lookup"><span data-stu-id="83d99-222">The log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="83d99-223">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="83d99-223">columnDelimiter</span></span> | <span data-ttu-id="83d99-224">columns in the log files are delimited by the comma character (`,`)</span><span class="sxs-lookup"><span data-stu-id="83d99-224">columns in the log files are delimited by the comma character (`,`)</span></span>
    <span data-ttu-id="83d99-225">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="83d99-225">frequency/interval</span></span> | <span data-ttu-id="83d99-226">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="83d99-226">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span>
    <span data-ttu-id="83d99-227">external</span><span class="sxs-lookup"><span data-stu-id="83d99-227">external</span></span> | <span data-ttu-id="83d99-228">This property is set to true if the input data for the activity is not generated by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-228">This property is set to true if the input data for the activity is not generated by the pipeline.</span></span> <span data-ttu-id="83d99-229">This property is only specified on input datasets.</span><span class="sxs-lookup"><span data-stu-id="83d99-229">This property is only specified on input datasets.</span></span> <span data-ttu-id="83d99-230">For the input dataset of the first activity, always set it to true.</span><span class="sxs-lookup"><span data-stu-id="83d99-230">For the input dataset of the first activity, always set it to true.</span></span>
4. <span data-ttu-id="83d99-231">Save the **InputDataset.json** file.</span><span class="sxs-lookup"><span data-stu-id="83d99-231">Save the **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="83d99-232">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="83d99-232">Create output dataset</span></span>
<span data-ttu-id="83d99-233">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="83d99-233">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="83d99-234">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="83d99-234">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="83d99-235">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-235">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="83d99-236">Replace the **JSON** in the editor with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="83d99-236">Replace the **JSON** in the editor with the following JSON:</span></span>
    
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
    <span data-ttu-id="83d99-237">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-237">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span></span> <span data-ttu-id="83d99-238">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="83d99-238">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="83d99-239">The **availability** section specifies that the output dataset is produced on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="83d99-239">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="83d99-240">The output dataset drives the schedule of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-240">The output dataset drives the schedule of the pipeline.</span></span> <span data-ttu-id="83d99-241">The pipeline runs monthly between its start and end times.</span><span class="sxs-lookup"><span data-stu-id="83d99-241">The pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="83d99-242">See **Create the input dataset** section for descriptions of these properties.</span><span class="sxs-lookup"><span data-stu-id="83d99-242">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="83d99-243">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-243">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span></span>
4. <span data-ttu-id="83d99-244">Save the **OutputDataset.json** file.</span><span class="sxs-lookup"><span data-stu-id="83d99-244">Save the **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="83d99-245">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="83d99-245">Create pipeline</span></span>
<span data-ttu-id="83d99-246">You have created the Azure Storage linked service, and input and output datasets so far.</span><span class="sxs-lookup"><span data-stu-id="83d99-246">You have created the Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="83d99-247">Now, you create a pipeline with a **HDInsightHive** activity.</span><span class="sxs-lookup"><span data-stu-id="83d99-247">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="83d99-248">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="83d99-248">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span></span> <span data-ttu-id="83d99-249">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span><span class="sxs-lookup"><span data-stu-id="83d99-249">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="83d99-250">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span><span class="sxs-lookup"><span data-stu-id="83d99-250">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="83d99-251">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-251">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span></span>
3. <span data-ttu-id="83d99-252">Replace the **JSON** with the following snippet:</span><span class="sxs-lookup"><span data-stu-id="83d99-252">Replace the **JSON** with the following snippet:</span></span>

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

    <span data-ttu-id="83d99-255">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span><span class="sxs-lookup"><span data-stu-id="83d99-255">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="83d99-256">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-256">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span></span> <span data-ttu-id="83d99-257">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="83d99-257">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span></span> 

    <span data-ttu-id="83d99-258">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span><span class="sxs-lookup"><span data-stu-id="83d99-258">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span></span> 

    <span data-ttu-id="83d99-259">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="83d99-259">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span></span>

    <span data-ttu-id="83d99-260">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span><span class="sxs-lookup"><span data-stu-id="83d99-260">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="83d99-261">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-261">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span> <span data-ttu-id="83d99-262">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span><span class="sxs-lookup"><span data-stu-id="83d99-262">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span></span>

    <span data-ttu-id="83d99-263">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="83d99-263">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="83d99-264">Save the **HiveActivity1.json** file.</span><span class="sxs-lookup"><span data-stu-id="83d99-264">Save the **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="83d99-265">Add partitionweblogs.hql and input.log as a dependency</span><span class="sxs-lookup"><span data-stu-id="83d99-265">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="83d99-266">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="83d99-266">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="83d99-267">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-267">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="83d99-268">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="83d99-268">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="83d99-269">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span><span class="sxs-lookup"><span data-stu-id="83d99-269">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="83d99-270">Publish/deploy Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="83d99-270">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="83d99-271">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="83d99-271">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span></span> <span data-ttu-id="83d99-272">In the process of publishing, you specify the name for your data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-272">In the process of publishing, you specify the name for your data factory.</span></span> 

1. <span data-ttu-id="83d99-273">Right-click project in the Solution Explorer, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="83d99-273">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="83d99-274">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span><span class="sxs-lookup"><span data-stu-id="83d99-274">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="83d99-275">You should see the following dialog box:</span><span class="sxs-lookup"><span data-stu-id="83d99-275">You should see the following dialog box:</span></span>

   ![Publish dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="83d99-277">In the **Configure data factory** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="83d99-277">In the **Configure data factory** page, do the following steps:</span></span>

    ![Publish - New data factory settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="83d99-279">select **Create New Data Factory** option.</span><span class="sxs-lookup"><span data-stu-id="83d99-279">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="83d99-280">Enter a unique **name** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-280">Enter a unique **name** for the data factory.</span></span> <span data-ttu-id="83d99-281">For example: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="83d99-281">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="83d99-282">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="83d99-282">The name must be globally unique.</span></span>
   3. <span data-ttu-id="83d99-283">Select the right subscription for the **Subscription** field.</span><span class="sxs-lookup"><span data-stu-id="83d99-283">Select the right subscription for the **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.
   4. <span data-ttu-id="83d99-285">Select the **resource group** for the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="83d99-285">Select the **resource group** for the data factory to be created.</span></span>
   5. <span data-ttu-id="83d99-286">Select the **region** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-286">Select the **region** for the data factory.</span></span>
   6. <span data-ttu-id="83d99-287">Click **Next** to switch to the **Publish Items** page.</span><span class="sxs-lookup"><span data-stu-id="83d99-287">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="83d99-288">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span><span class="sxs-lookup"><span data-stu-id="83d99-288">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > If you receive the error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change the name (for example, yournameDataFactoryUsingVS). See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.   
1. <span data-ttu-id="83d99-291">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span><span class="sxs-lookup"><span data-stu-id="83d99-291">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>

    ![Publish items page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="83d99-293">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span><span class="sxs-lookup"><span data-stu-id="83d99-293">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>

    ![Summary page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="83d99-295">In the **Deployment Status** page, you should see the status of the deployment process.</span><span class="sxs-lookup"><span data-stu-id="83d99-295">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="83d99-296">Click Finish after the deployment is done.</span><span class="sxs-lookup"><span data-stu-id="83d99-296">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="83d99-297">Important points to note:</span><span class="sxs-lookup"><span data-stu-id="83d99-297">Important points to note:</span></span>

- <span data-ttu-id="83d99-298">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="83d99-298">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span></span>
    - <span data-ttu-id="83d99-299">In Azure PowerShell, run the following command to register the Data Factory provider.</span><span class="sxs-lookup"><span data-stu-id="83d99-299">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="83d99-300">You can run the following command to confirm that the Data Factory provider is registered.</span><span class="sxs-lookup"><span data-stu-id="83d99-300">You can run the following command to confirm that the Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="83d99-301">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="83d99-301">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="83d99-302">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="83d99-302">This action automatically registers the provider for you.</span></span>
- <span data-ttu-id="83d99-303">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span><span class="sxs-lookup"><span data-stu-id="83d99-303">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
- <span data-ttu-id="83d99-304">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="83d99-304">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="83d99-305">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="83d99-305">Monitor pipeline</span></span>
<span data-ttu-id="83d99-306">In this step, you monitor the pipeline using Diagram View of the data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-306">In this step, you monitor the pipeline using Diagram View of the data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="83d99-307">Monitor pipeline using Diagram View</span><span class="sxs-lookup"><span data-stu-id="83d99-307">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="83d99-308">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span><span class="sxs-lookup"><span data-stu-id="83d99-308">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>
   1. <span data-ttu-id="83d99-309">Click **More services** and click **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="83d99-309">Click **More services** and click **Data factories**.</span></span>
       
        ![Browse data factories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="83d99-311">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span><span class="sxs-lookup"><span data-stu-id="83d99-311">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span></span>
   
       ![Select your data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="83d99-313">In the home page for your data factory, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="83d99-313">In the home page for your data factory, click **Diagram**.</span></span>

    ![Diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="83d99-315">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="83d99-315">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diagram View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="83d99-317">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-317">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Open pipeline menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="83d99-319">Confirm that you see the HDInsightHive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-319">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Open pipeline view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="83d99-321">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="83d99-321">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
6. <span data-ttu-id="83d99-322">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="83d99-322">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="83d99-323">Confirm that the slice is in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="83d99-323">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="83d99-324">It may take a couple of minutes for the slice to show up in Ready state.</span><span class="sxs-lookup"><span data-stu-id="83d99-324">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="83d99-325">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="83d99-325">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="83d99-326">And, make sure that the **external** property on the input dataset is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="83d99-326">And, make sure that the **external** property on the input dataset is set to **true**.</span></span> 

   ![Input slice in ready state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="83d99-328">Click **X** to close **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="83d99-328">Click **X** to close **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="83d99-329">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="83d99-329">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="83d99-330">You see that the slice that is currently being processed.</span><span class="sxs-lookup"><span data-stu-id="83d99-330">You see that the slice that is currently being processed.</span></span>

   ![Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="83d99-332">When processing is done, you see the slice in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="83d99-332">When processing is done, you see the slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes). Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.  
   
    ![Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="83d99-336">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-336">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span></span>  

    ![output data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="83d99-338">Click the slice to see details about it in a **Data slice** blade.</span><span class="sxs-lookup"><span data-stu-id="83d99-338">Click the slice to see details about it in a **Data slice** blade.</span></span>

    ![Data slice details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="83d99-340">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span><span class="sxs-lookup"><span data-stu-id="83d99-340">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Activity run details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="83d99-342">From the log files, you can see the Hive query that was executed and status information.</span><span class="sxs-lookup"><span data-stu-id="83d99-342">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="83d99-343">These logs are useful for troubleshooting any issues.</span><span class="sxs-lookup"><span data-stu-id="83d99-343">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="83d99-344">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="83d99-344">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="83d99-345">Monitor pipeline using Monitor & Manage App</span><span class="sxs-lookup"><span data-stu-id="83d99-345">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="83d99-346">You can also use Monitor & Manage application to monitor your pipelines.</span><span class="sxs-lookup"><span data-stu-id="83d99-346">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="83d99-347">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="83d99-347">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="83d99-348">Click Monitor & Manage tile.</span><span class="sxs-lookup"><span data-stu-id="83d99-348">Click Monitor & Manage tile.</span></span>

    ![Monitor & Manage tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="83d99-350">You should see Monitor & Manage application.</span><span class="sxs-lookup"><span data-stu-id="83d99-350">You should see Monitor & Manage application.</span></span> <span data-ttu-id="83d99-351">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="83d99-351">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![Monitor & Manage App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="83d99-353">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span><span class="sxs-lookup"><span data-stu-id="83d99-353">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span></span>
    <span data-ttu-id="83d99-354">![Activity window details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="83d99-354">![Activity window details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the `inputdata` folder of the `adfgetstarted` container.

### <a name="additional-notes"></a><span data-ttu-id="83d99-357">Additional notes</span><span class="sxs-lookup"><span data-stu-id="83d99-357">Additional notes</span></span>
- <span data-ttu-id="83d99-358">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="83d99-358">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="83d99-359">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="83d99-359">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="83d99-360">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform input data.</span><span class="sxs-lookup"><span data-stu-id="83d99-360">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform input data.</span></span> <span data-ttu-id="83d99-361">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="83d99-361">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="83d99-362">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-362">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="83d99-363">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-363">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="83d99-364">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="83d99-364">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="83d99-365">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span><span class="sxs-lookup"><span data-stu-id="83d99-365">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="83d99-366">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span><span class="sxs-lookup"><span data-stu-id="83d99-366">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span></span>
- <span data-ttu-id="83d99-367">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-367">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="83d99-368">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span><span class="sxs-lookup"><span data-stu-id="83d99-368">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="83d99-369">The Data Factory creates a **Windows-based** HDInsight cluster for you with the preceding JSON.</span><span class="sxs-lookup"><span data-stu-id="83d99-369">The Data Factory creates a **Windows-based** HDInsight cluster for you with the preceding JSON.</span></span> <span data-ttu-id="83d99-370">You could also have it create a **Linux-based** HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-370">You could also have it create a **Linux-based** HDInsight cluster.</span></span> <span data-ttu-id="83d99-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="83d99-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="83d99-372">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="83d99-372">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="83d99-373">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="83d99-373">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="83d99-374">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="83d99-374">This behavior is by design.</span></span> <span data-ttu-id="83d99-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="83d99-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="83d99-376">The cluster is automatically deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="83d99-376">The cluster is automatically deleted when the processing is done.</span></span>
    
    <span data-ttu-id="83d99-377">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="83d99-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="83d99-378">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="83d99-378">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="83d99-379">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="83d99-379">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="83d99-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="83d99-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="83d99-381">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="83d99-381">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="83d99-382">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="83d99-382">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 
- <span data-ttu-id="83d99-383">This tutorial does not show how copy data by using Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="83d99-384">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="83d99-384">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="83d99-385">Use Server Explorer to view data factories</span><span class="sxs-lookup"><span data-stu-id="83d99-385">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="83d99-386">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="83d99-386">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="83d99-387">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="83d99-387">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="83d99-388">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="83d99-388">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="83d99-389">Enter **password**, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="83d99-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="83d99-390">Visual Studio tries to get information about all Azure data factories in your subscription.</span><span class="sxs-lookup"><span data-stu-id="83d99-390">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="83d99-391">You see the status of this operation in the **Data Factory Task List** window.</span><span class="sxs-lookup"><span data-stu-id="83d99-391">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="83d99-393">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-393">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Export data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="83d99-395">Update Data Factory tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83d99-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="83d99-396">To update Azure Data Factory tools for Visual Studio, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="83d99-396">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="83d99-397">Click **Tools** on the menu and select **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="83d99-397">Click **Tools** on the menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="83d99-398">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span><span class="sxs-lookup"><span data-stu-id="83d99-398">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="83d99-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="83d99-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="83d99-400">If you do not see this entry, you already have the latest version of the tools.</span><span class="sxs-lookup"><span data-stu-id="83d99-400">If you do not see this entry, you already have the latest version of the tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="83d99-401">Use configuration files</span><span class="sxs-lookup"><span data-stu-id="83d99-401">Use configuration files</span></span>
<span data-ttu-id="83d99-402">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span><span class="sxs-lookup"><span data-stu-id="83d99-402">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="83d99-403">Consider the following JSON definition for an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="83d99-403">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="83d99-404">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="83d99-404">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="83d99-405">You can achieve this behavior by using separate configuration file for each environment.</span><span class="sxs-lookup"><span data-stu-id="83d99-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="83d99-406">Add a configuration file</span><span class="sxs-lookup"><span data-stu-id="83d99-406">Add a configuration file</span></span>
<span data-ttu-id="83d99-407">Add a configuration file for each environment by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="83d99-407">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="83d99-408">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span><span class="sxs-lookup"><span data-stu-id="83d99-408">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="83d99-409">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="83d99-409">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Add configuration file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="83d99-411">Add configuration parameters and their values in the following format:</span><span class="sxs-lookup"><span data-stu-id="83d99-411">Add configuration parameters and their values in the following format:</span></span>

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
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="83d99-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="83d99-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="83d99-413">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="83d99-413">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="83d99-414">If JSON has a property that has an array of values as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="83d99-414">If JSON has a property that has an array of values as shown in the following code:</span></span>  

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

    <span data-ttu-id="83d99-415">Configure properties as shown in the following configuration file (use zero-based indexing):</span><span class="sxs-lookup"><span data-stu-id="83d99-415">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="83d99-416">Property names with spaces</span><span class="sxs-lookup"><span data-stu-id="83d99-416">Property names with spaces</span></span>
<span data-ttu-id="83d99-417">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span><span class="sxs-lookup"><span data-stu-id="83d99-417">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="83d99-418">Deploy solution using a configuration</span><span class="sxs-lookup"><span data-stu-id="83d99-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="83d99-419">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span><span class="sxs-lookup"><span data-stu-id="83d99-419">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="83d99-420">To publish entities in an Azure Data Factory project using configuration file:</span><span class="sxs-lookup"><span data-stu-id="83d99-420">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="83d99-421">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span><span class="sxs-lookup"><span data-stu-id="83d99-421">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="83d99-422">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="83d99-422">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="83d99-423">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span><span class="sxs-lookup"><span data-stu-id="83d99-423">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Select config file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="83d99-425">Select the **configuration file** that you would like to use and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="83d99-425">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="83d99-426">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="83d99-426">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="83d99-427">Click **Finish** after the deployment operation is finished.</span><span class="sxs-lookup"><span data-stu-id="83d99-427">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="83d99-428">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="83d99-428">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="83d99-429">Use Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="83d99-429">Use Azure Key Vault</span></span>
<span data-ttu-id="83d99-430">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span><span class="sxs-lookup"><span data-stu-id="83d99-430">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="83d99-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="83d99-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="83d99-432">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span><span class="sxs-lookup"><span data-stu-id="83d99-432">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="83d99-433">These references are resolved when you publish Data Factory entities to Azure.</span><span class="sxs-lookup"><span data-stu-id="83d99-433">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="83d99-434">These files can then be committed to source repository without exposing any secrets.</span><span class="sxs-lookup"><span data-stu-id="83d99-434">These files can then be committed to source repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="83d99-435">Summary</span><span class="sxs-lookup"><span data-stu-id="83d99-435">Summary</span></span>
<span data-ttu-id="83d99-436">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-436">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="83d99-437">You used the Data Factory Editor in the Azure portal to do the following steps:</span><span class="sxs-lookup"><span data-stu-id="83d99-437">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="83d99-438">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="83d99-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="83d99-439">Created two **linked services**:</span><span class="sxs-lookup"><span data-stu-id="83d99-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="83d99-440">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-440">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="83d99-441">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-441">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="83d99-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="83d99-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="83d99-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="83d99-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="83d99-444">Created a **pipeline** with a **HDInsight Hive** activity.</span><span class="sxs-lookup"><span data-stu-id="83d99-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="83d99-445">Next Steps</span><span class="sxs-lookup"><span data-stu-id="83d99-445">Next Steps</span></span>
<span data-ttu-id="83d99-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="83d99-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="83d99-447">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="83d99-447">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="83d99-448">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="83d99-448">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="83d99-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="83d99-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="83d99-450">See Also</span><span class="sxs-lookup"><span data-stu-id="83d99-450">See Also</span></span>
| <span data-ttu-id="83d99-451">Topic</span><span class="sxs-lookup"><span data-stu-id="83d99-451">Topic</span></span> | <span data-ttu-id="83d99-452">Description</span><span class="sxs-lookup"><span data-stu-id="83d99-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="83d99-453">Pipelines</span><span class="sxs-lookup"><span data-stu-id="83d99-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="83d99-454">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="83d99-454">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="83d99-455">Datasets</span><span class="sxs-lookup"><span data-stu-id="83d99-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="83d99-456">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="83d99-457">Data Transformation Activities</span><span class="sxs-lookup"><span data-stu-id="83d99-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="83d99-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83d99-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="83d99-459">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="83d99-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="83d99-460">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="83d99-460">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="83d99-461">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="83d99-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="83d99-462">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="83d99-462">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |



























