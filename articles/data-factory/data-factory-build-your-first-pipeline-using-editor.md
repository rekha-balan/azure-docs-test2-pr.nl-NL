---
title: Build your first data factory (Azure portal) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using Data Factory Editor in the Azure portal.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/14/2017
ms.author: spelluru
ms.openlocfilehash: a0724ae9c99f3171d3f3bb227fe9b6e9ace21ae4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553201"
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="e79fe-103">Tutorial: Build your first Azure data factory using Azure portal</span><span class="sxs-lookup"><span data-stu-id="e79fe-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="e79fe-110">In this article, you learn how to use the [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-110">In this article, you learn how to use the [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="e79fe-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e79fe-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

> [!NOTE]
> The data pipeline in this tutorial transforms input data to produce output data. It does not copy data from a source data store to a destination data store. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

## <a name="prerequisites"></a><span data-ttu-id="e79fe-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e79fe-117">Prerequisites</span></span>
1. <span data-ttu-id="e79fe-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="e79fe-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="e79fe-119">This article does not provide a conceptual overview of the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="e79fe-119">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="e79fe-120">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span><span class="sxs-lookup"><span data-stu-id="e79fe-120">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="e79fe-121">Create data factory</span><span class="sxs-lookup"><span data-stu-id="e79fe-121">Create data factory</span></span>
<span data-ttu-id="e79fe-122">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="e79fe-122">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="e79fe-123">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="e79fe-123">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="e79fe-124">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform input data to product output data.</span><span class="sxs-lookup"><span data-stu-id="e79fe-124">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform input data to product output data.</span></span> <span data-ttu-id="e79fe-125">Let's start with creating the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="e79fe-125">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="e79fe-126">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e79fe-126">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e79fe-127">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-127">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Create blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="e79fe-129">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span><span class="sxs-lookup"><span data-stu-id="e79fe-129">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![New data factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > The name of the Azure data factory must be **globally unique**. If you receive the error: **Data factory name “GetStartedDF” is not available**. Change the name of the data factory (for example, yournameGetStartedDF) and try creating again. See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.
   >
   > The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.
   >
   >
4. <span data-ttu-id="e79fe-136">Select the **Azure subscription** where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="e79fe-136">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="e79fe-137">Select existing **resource group** or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="e79fe-137">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="e79fe-138">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-138">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="e79fe-139">Click **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="e79fe-139">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.
   >
   >
7. <span data-ttu-id="e79fe-141">You see the data factory being created in the **Startboard** of the Azure portal as follows:</span><span class="sxs-lookup"><span data-stu-id="e79fe-141">You see the data factory being created in the **Startboard** of the Azure portal as follows:</span></span>   

   ![Creating data factory status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="e79fe-143">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="e79fe-143">Congratulations!</span></span> <span data-ttu-id="e79fe-144">You have successfully created your first data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-144">You have successfully created your first data factory.</span></span> <span data-ttu-id="e79fe-145">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-145">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![Data Factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="e79fe-147">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span><span class="sxs-lookup"><span data-stu-id="e79fe-147">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="e79fe-148">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span><span class="sxs-lookup"><span data-stu-id="e79fe-148">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="e79fe-149">Create linked services</span><span class="sxs-lookup"><span data-stu-id="e79fe-149">Create linked services</span></span>
<span data-ttu-id="e79fe-150">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-150">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="e79fe-151">The Azure Storage account holds the input and output data for the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="e79fe-151">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="e79fe-152">The HDInsight linked service is used to run Hive script specified in the activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="e79fe-152">The HDInsight linked service is used to run Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="e79fe-153">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span><span class="sxs-lookup"><span data-stu-id="e79fe-153">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="e79fe-154">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="e79fe-154">Create Azure Storage linked service</span></span>
<span data-ttu-id="e79fe-155">In this step, you link your Azure Storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-155">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="e79fe-156">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span><span class="sxs-lookup"><span data-stu-id="e79fe-156">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="e79fe-157">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-157">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="e79fe-158">You should see the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="e79fe-158">You should see the Data Factory Editor.</span></span>

   ![Author and deploy tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="e79fe-160">Click **New data store** and choose **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-160">Click **New data store** and choose **Azure storage**.</span></span>

   ![New data store - Azure Storage - menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="e79fe-162">You should see the JSON script for creating an Azure Storage linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="e79fe-162">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure Storage linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="e79fe-164">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e79fe-164">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="e79fe-165">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e79fe-165">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="e79fe-166">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="e79fe-166">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Deploy button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="e79fe-168">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="e79fe-168">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![Storage Linked Service in menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="e79fe-170">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="e79fe-170">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="e79fe-171">In this step, you link an on-demand HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-171">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="e79fe-172">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="e79fe-172">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="e79fe-173">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-173">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![New compute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="e79fe-175">Copy and paste the following snippet to the **Draft-1** window.</span><span class="sxs-lookup"><span data-stu-id="e79fe-175">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="e79fe-176">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span><span class="sxs-lookup"><span data-stu-id="e79fe-176">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

    ```JSON
    {
      "name": "HDInsightOnDemandLinkedService",
      "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
          "version": "3.2",
          "clusterSize": 1,
          "timeToLive": "00:30:00",
          "linkedServiceName": "AzureStorageLinkedService"
        }
      }
    }
    ```

    <span data-ttu-id="e79fe-177">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="e79fe-177">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="e79fe-178">Property</span><span class="sxs-lookup"><span data-stu-id="e79fe-178">Property</span></span> | <span data-ttu-id="e79fe-179">Description</span><span class="sxs-lookup"><span data-stu-id="e79fe-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="e79fe-180">Version</span><span class="sxs-lookup"><span data-stu-id="e79fe-180">Version</span></span> |<span data-ttu-id="e79fe-181">Specifies that the version of the HDInsight created to be 3.2.</span><span class="sxs-lookup"><span data-stu-id="e79fe-181">Specifies that the version of the HDInsight created to be 3.2.</span></span> |
   | <span data-ttu-id="e79fe-182">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="e79fe-182">ClusterSize</span></span> |<span data-ttu-id="e79fe-183">Specifies the size of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e79fe-183">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="e79fe-184">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="e79fe-184">TimeToLive</span></span> |<span data-ttu-id="e79fe-185">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="e79fe-185">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="e79fe-186">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e79fe-186">linkedServiceName</span></span> |<span data-ttu-id="e79fe-187">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e79fe-187">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="e79fe-188">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e79fe-188">Note the following points:</span></span>

   * <span data-ttu-id="e79fe-189">The Data Factory creates a **Windows-based** HDInsight cluster for you with the JSON.</span><span class="sxs-lookup"><span data-stu-id="e79fe-189">The Data Factory creates a **Windows-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="e79fe-190">You could also have it create a **Linux-based** HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e79fe-190">You could also have it create a **Linux-based** HDInsight cluster.</span></span> <span data-ttu-id="e79fe-191">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="e79fe-191">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="e79fe-192">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e79fe-192">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e79fe-193">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="e79fe-193">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="e79fe-194">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="e79fe-194">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="e79fe-195">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="e79fe-195">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="e79fe-196">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="e79fe-196">This behavior is by design.</span></span> <span data-ttu-id="e79fe-197">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="e79fe-197">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="e79fe-198">The cluster is automatically deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="e79fe-198">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="e79fe-199">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="e79fe-199">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e79fe-200">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="e79fe-200">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="e79fe-201">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="e79fe-201">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="e79fe-202">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="e79fe-202">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="e79fe-203">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="e79fe-203">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="e79fe-204">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="e79fe-204">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Deploy on-demand HDInsight linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="e79fe-206">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="e79fe-206">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Tree view with linked services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="e79fe-208">Create datasets</span><span class="sxs-lookup"><span data-stu-id="e79fe-208">Create datasets</span></span>
<span data-ttu-id="e79fe-209">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="e79fe-209">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="e79fe-210">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e79fe-210">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="e79fe-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="e79fe-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="e79fe-212">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="e79fe-212">Create input dataset</span></span>
1. <span data-ttu-id="e79fe-213">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-213">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![New dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="e79fe-215">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="e79fe-215">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="e79fe-216">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e79fe-216">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="e79fe-217">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-217">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="e79fe-218">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="e79fe-218">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="e79fe-219">Property</span><span class="sxs-lookup"><span data-stu-id="e79fe-219">Property</span></span> | <span data-ttu-id="e79fe-220">Description</span><span class="sxs-lookup"><span data-stu-id="e79fe-220">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="e79fe-221">type</span><span class="sxs-lookup"><span data-stu-id="e79fe-221">type</span></span> |<span data-ttu-id="e79fe-222">The type property is set to AzureBlob because data resides in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="e79fe-222">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="e79fe-223">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e79fe-223">linkedServiceName</span></span> |<span data-ttu-id="e79fe-224">refers to the AzureStorageLinkedService you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e79fe-224">refers to the AzureStorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="e79fe-225">fileName</span><span class="sxs-lookup"><span data-stu-id="e79fe-225">fileName</span></span> |<span data-ttu-id="e79fe-226">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="e79fe-226">This property is optional.</span></span> <span data-ttu-id="e79fe-227">If you omit this property, all the files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="e79fe-227">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="e79fe-228">In this case, only the input.log is processed.</span><span class="sxs-lookup"><span data-stu-id="e79fe-228">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="e79fe-229">type</span><span class="sxs-lookup"><span data-stu-id="e79fe-229">type</span></span> |<span data-ttu-id="e79fe-230">The log files are in text format, so we use TextFormat.</span><span class="sxs-lookup"><span data-stu-id="e79fe-230">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="e79fe-231">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="e79fe-231">columnDelimiter</span></span> |<span data-ttu-id="e79fe-232">columns in the log files are delimited by comma character (,)</span><span class="sxs-lookup"><span data-stu-id="e79fe-232">columns in the log files are delimited by comma character (,)</span></span> |
   | <span data-ttu-id="e79fe-233">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="e79fe-233">frequency/interval</span></span> |<span data-ttu-id="e79fe-234">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="e79fe-234">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="e79fe-235">external</span><span class="sxs-lookup"><span data-stu-id="e79fe-235">external</span></span> |<span data-ttu-id="e79fe-236">this property is set to true if the input data is not generated by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="e79fe-236">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
3. <span data-ttu-id="e79fe-237">Click **Deploy** on the command bar to deploy the newly created dataset.</span><span class="sxs-lookup"><span data-stu-id="e79fe-237">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="e79fe-238">You should see the dataset in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="e79fe-238">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="e79fe-239">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="e79fe-239">Create output dataset</span></span>
<span data-ttu-id="e79fe-240">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="e79fe-240">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="e79fe-241">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-241">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="e79fe-242">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="e79fe-242">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="e79fe-243">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span><span class="sxs-lookup"><span data-stu-id="e79fe-243">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="e79fe-244">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-244">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="e79fe-245">The **availability** section specifies that the output dataset is produced on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="e79fe-245">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="e79fe-246">See **Create the input dataset** section for descriptions of these properties.</span><span class="sxs-lookup"><span data-stu-id="e79fe-246">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="e79fe-247">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="e79fe-247">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="e79fe-248">Click **Deploy** on the command bar to deploy the newly created dataset.</span><span class="sxs-lookup"><span data-stu-id="e79fe-248">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="e79fe-249">Verify that the dataset is created successfully.</span><span class="sxs-lookup"><span data-stu-id="e79fe-249">Verify that the dataset is created successfully.</span></span>

    ![Tree view with linked services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="e79fe-251">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="e79fe-251">Create pipeline</span></span>
<span data-ttu-id="e79fe-252">In this step, you create your first pipeline with a **HDInsightHive** activity.</span><span class="sxs-lookup"><span data-stu-id="e79fe-252">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="e79fe-253">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span><span class="sxs-lookup"><span data-stu-id="e79fe-253">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="e79fe-254">The settings for the output dataset and the activity scheduler must match.</span><span class="sxs-lookup"><span data-stu-id="e79fe-254">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="e79fe-255">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="e79fe-255">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="e79fe-256">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="e79fe-256">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="e79fe-257">The properties used in the following JSON are explained at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="e79fe-257">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="e79fe-258">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-258">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![new pipeline button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="e79fe-260">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="e79fe-260">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > Replace **storageaccountname** with the name of your storage account in the JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    <span data-ttu-id="e79fe-262">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e79fe-262">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="e79fe-263">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-263">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="e79fe-264">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="e79fe-264">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="e79fe-265">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e79fe-265">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="e79fe-266">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-266">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.
   >
   >
3. <span data-ttu-id="e79fe-268">Confirm the following:</span><span class="sxs-lookup"><span data-stu-id="e79fe-268">Confirm the following:</span></span>

   1. <span data-ttu-id="e79fe-269">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="e79fe-269">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="e79fe-270">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="e79fe-270">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="e79fe-271">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span><span class="sxs-lookup"><span data-stu-id="e79fe-271">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="e79fe-272">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="e79fe-272">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="e79fe-273">Click **Deploy** on the command bar to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e79fe-273">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="e79fe-274">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span><span class="sxs-lookup"><span data-stu-id="e79fe-274">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="e79fe-275">Confirm that you see the pipeline in the tree view.</span><span class="sxs-lookup"><span data-stu-id="e79fe-275">Confirm that you see the pipeline in the tree view.</span></span>

    ![Tree view with pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="e79fe-277">Congratulations, you have successfully created your first pipeline!</span><span class="sxs-lookup"><span data-stu-id="e79fe-277">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="e79fe-278">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="e79fe-278">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="e79fe-279">Monitor pipeline using Diagram View</span><span class="sxs-lookup"><span data-stu-id="e79fe-279">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="e79fe-280">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-280">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="e79fe-282">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e79fe-282">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diagram View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="e79fe-284">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span><span class="sxs-lookup"><span data-stu-id="e79fe-284">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Open pipeline menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="e79fe-286">Confirm that you see the HDInsightHive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e79fe-286">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Open pipeline view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="e79fe-288">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="e79fe-288">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="e79fe-289">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-289">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="e79fe-290">Confirm that the slice is in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="e79fe-290">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="e79fe-291">It may take a couple of minutes for the slice to show up in Ready state.</span><span class="sxs-lookup"><span data-stu-id="e79fe-291">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="e79fe-292">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span><span class="sxs-lookup"><span data-stu-id="e79fe-292">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Input slice in ready state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="e79fe-294">Click **X** to close **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="e79fe-294">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="e79fe-295">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-295">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="e79fe-296">You see that the slice that is currently being processed.</span><span class="sxs-lookup"><span data-stu-id="e79fe-296">You see that the slice that is currently being processed.</span></span>

   ![Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="e79fe-298">When processing is done, you see the slice in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="e79fe-298">When processing is done, you see the slice in **Ready** state.</span></span>

   ![Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes). Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.
   >
   >

9. <span data-ttu-id="e79fe-302">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="e79fe-302">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![output data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="e79fe-304">Click the slice to see details about it in a **Data slice** blade.</span><span class="sxs-lookup"><span data-stu-id="e79fe-304">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![Data slice details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="e79fe-306">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span><span class="sxs-lookup"><span data-stu-id="e79fe-306">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Activity run details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="e79fe-308">From the log files, you can see the Hive query that was executed and status information.</span><span class="sxs-lookup"><span data-stu-id="e79fe-308">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="e79fe-309">These logs are useful for troubleshooting any issues.</span><span class="sxs-lookup"><span data-stu-id="e79fe-309">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="e79fe-310">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span><span class="sxs-lookup"><span data-stu-id="e79fe-310">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="e79fe-313">Monitor pipeline using Monitor & Manage App</span><span class="sxs-lookup"><span data-stu-id="e79fe-313">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="e79fe-314">You can also use Monitor & Manage application to monitor your pipelines.</span><span class="sxs-lookup"><span data-stu-id="e79fe-314">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="e79fe-315">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="e79fe-315">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="e79fe-316">Click **Monitor & Manage** tile on the home page for your data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-316">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![Monitor & Manage tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="e79fe-318">You should see **Monitor & Manage application**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-318">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="e79fe-319">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-319">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![Monitor & Manage App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="e79fe-321">Select an activity window in the **Activity Windows** list to see details about it.</span><span class="sxs-lookup"><span data-stu-id="e79fe-321">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![Activity window details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="e79fe-323">Summary</span><span class="sxs-lookup"><span data-stu-id="e79fe-323">Summary</span></span>
<span data-ttu-id="e79fe-324">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="e79fe-324">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="e79fe-325">You used the Data Factory Editor in the Azure portal to do the following steps:</span><span class="sxs-lookup"><span data-stu-id="e79fe-325">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="e79fe-326">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="e79fe-326">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="e79fe-327">Created two **linked services**:</span><span class="sxs-lookup"><span data-stu-id="e79fe-327">Created two **linked services**:</span></span>
   1. <span data-ttu-id="e79fe-328">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-328">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="e79fe-329">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-329">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="e79fe-330">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="e79fe-330">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="e79fe-331">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e79fe-331">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="e79fe-332">Created a **pipeline** with a **HDInsight Hive** activity.</span><span class="sxs-lookup"><span data-stu-id="e79fe-332">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e79fe-333">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e79fe-333">Next Steps</span></span>
<span data-ttu-id="e79fe-334">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e79fe-334">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e79fe-335">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e79fe-335">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e79fe-336">See Also</span><span class="sxs-lookup"><span data-stu-id="e79fe-336">See Also</span></span>
| <span data-ttu-id="e79fe-337">Topic</span><span class="sxs-lookup"><span data-stu-id="e79fe-337">Topic</span></span> | <span data-ttu-id="e79fe-338">Description</span><span class="sxs-lookup"><span data-stu-id="e79fe-338">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="e79fe-339">Pipelines</span><span class="sxs-lookup"><span data-stu-id="e79fe-339">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="e79fe-340">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="e79fe-340">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="e79fe-341">Datasets</span><span class="sxs-lookup"><span data-stu-id="e79fe-341">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="e79fe-342">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e79fe-342">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="e79fe-343">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="e79fe-343">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="e79fe-344">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="e79fe-344">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="e79fe-345">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="e79fe-345">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="e79fe-346">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="e79fe-346">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |





























