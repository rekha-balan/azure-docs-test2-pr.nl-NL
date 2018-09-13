---
title: Build your first data factory (Azure portal) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline by using the Data Factory Editor in the Azure portal.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: ''
editor: ''
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 332ba810aa9da611f998e5865344655c3c87c5d1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870296"
---
# <a name="tutorial-build-your-first-data-factory-by-using-the-azure-portal"></a><span data-ttu-id="06f74-103">Tutorial: Build your first data factory by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="06f74-103">Tutorial: Build your first data factory by using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Azure Resource Manager template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


> [!NOTE]
> This article applies to version 1 of Azure Data Factory, which is generally available. If you use the current version of the Data Factory service, see [Quickstart: Create a data factory by using Data Factory](../quickstart-create-data-factory-dot-net.md).

<span data-ttu-id="06f74-112">In this article, you learn how to use the [Azure portal](https://portal.azure.com/) to create your first data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-112">In this article, you learn how to use the [Azure portal](https://portal.azure.com/) to create your first data factory.</span></span> <span data-ttu-id="06f74-113">To do the tutorial by using other tools/SDKs, select one of the options from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="06f74-113">To do the tutorial by using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="06f74-114">The pipeline in this tutorial has one activity: an Azure HDInsight Hive activity.</span><span class="sxs-lookup"><span data-stu-id="06f74-114">The pipeline in this tutorial has one activity: an Azure HDInsight Hive activity.</span></span> <span data-ttu-id="06f74-115">This activity runs a Hive script on an HDInsight cluster that transforms input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="06f74-115">This activity runs a Hive script on an HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="06f74-116">The pipeline is scheduled to run once a month between the specified start and end times.</span><span class="sxs-lookup"><span data-stu-id="06f74-116">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> The data pipeline in this tutorial transforms input data to produce output data. For a tutorial on how to copy data by using Data Factory, see [Tutorial: Copy data from Azure Blob storage to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> A pipeline can have more than one activity. And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. For more information, see [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a><span data-ttu-id="06f74-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="06f74-122">Prerequisites</span></span>
<span data-ttu-id="06f74-123">Read [Tutorial overview](data-factory-build-your-first-pipeline.md), and follow the steps in the "Prerequisites" section.</span><span class="sxs-lookup"><span data-stu-id="06f74-123">Read [Tutorial overview](data-factory-build-your-first-pipeline.md), and follow the steps in the "Prerequisites" section.</span></span>

<span data-ttu-id="06f74-124">This article doesn't provide a conceptual overview of the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="06f74-124">This article doesn't provide a conceptual overview of the Data Factory service.</span></span> <span data-ttu-id="06f74-125">For more information about the service, read [Introduction to Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06f74-125">For more information about the service, read [Introduction to Azure Data Factory](data-factory-introduction.md).</span></span>  

## <a name="create-a-data-factory"></a><span data-ttu-id="06f74-126">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="06f74-126">Create a data factory</span></span>
<span data-ttu-id="06f74-127">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="06f74-127">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="06f74-128">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="06f74-128">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="06f74-129">An example is a Copy activity that copies data from a source to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="06f74-129">An example is a Copy activity that copies data from a source to a destination data store.</span></span> <span data-ttu-id="06f74-130">Another example is an HDInsight Hive activity that runs a Hive script to transform input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="06f74-130">Another example is an HDInsight Hive activity that runs a Hive script to transform input data to produce output data.</span></span> 

<span data-ttu-id="06f74-131">To create a data factory, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="06f74-131">To create a data factory, follow these steps:</span></span>

1. <span data-ttu-id="06f74-132">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="06f74-132">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="06f74-133">Select **New** > **Data + Analytics** > **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="06f74-133">Select **New** > **Data + Analytics** > **Data Factory**.</span></span>

   ![Create blade](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)

1. <span data-ttu-id="06f74-135">On the **New data factory** blade, under **Name**, enter **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="06f74-135">On the **New data factory** blade, under **Name**, enter **GetStartedDF**.</span></span>

   ![New data factory blade](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > The name of the data factory must be globally unique. If you receive the error "Data factory name GetStartedDF is not available," change the name of the data factory. For example, use  yournameGetStartedDF, and create the data factory again. For more information on naming rules, see [Data Factory: Naming rules](data-factory-naming-rules.md).
   >
   > The name of the data factory might be registered as a DNS name in the future, and it might become publicly visible.
   >
   >
1. <span data-ttu-id="06f74-142">Under **Subscription**, select the Azure subscription where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="06f74-142">Under **Subscription**, select the Azure subscription where you want the data factory to be created.</span></span>

1. <span data-ttu-id="06f74-143">Select an existing resource group, or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="06f74-143">Select an existing resource group, or create a resource group.</span></span> <span data-ttu-id="06f74-144">For the tutorial, create a resource group named **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="06f74-144">For the tutorial, create a resource group named **ADFGetStartedRG**.</span></span>

1. <span data-ttu-id="06f74-145">Under **Location**, select a location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-145">Under **Location**, select a location for the data factory.</span></span> <span data-ttu-id="06f74-146">Only regions supported by the Data Factory service are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="06f74-146">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>

1. <span data-ttu-id="06f74-147">Select the **Pin to dashboard** check box.</span><span class="sxs-lookup"><span data-stu-id="06f74-147">Select the **Pin to dashboard** check box.</span></span>

1. <span data-ttu-id="06f74-148">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="06f74-148">Select **Create**.</span></span>

   > [!IMPORTANT]
   > To create Data Factory instances, you must be a member of the [Data Factory contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.
   >
   >
1. <span data-ttu-id="06f74-150">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="06f74-150">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span>    

   ![Deploying Data Factory status](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)

1. <span data-ttu-id="06f74-152">After the data factory is created, you see the **Data factory** page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-152">After the data factory is created, you see the **Data factory** page, which shows you the contents of the data factory.</span></span>     

    ![Data factory blade](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="06f74-154">Before you create a pipeline in the data factory, you need to create a few data factory entities first.</span><span class="sxs-lookup"><span data-stu-id="06f74-154">Before you create a pipeline in the data factory, you need to create a few data factory entities first.</span></span> <span data-ttu-id="06f74-155">You first create linked services to link data stores/computes to your data store.</span><span class="sxs-lookup"><span data-stu-id="06f74-155">You first create linked services to link data stores/computes to your data store.</span></span> <span data-ttu-id="06f74-156">Then you define input and output datasets to represent input/output data in linked data stores.</span><span class="sxs-lookup"><span data-stu-id="06f74-156">Then you define input and output datasets to represent input/output data in linked data stores.</span></span> <span data-ttu-id="06f74-157">Finally, you create the pipeline with an activity that uses these datasets.</span><span class="sxs-lookup"><span data-stu-id="06f74-157">Finally, you create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="06f74-158">Create linked services</span><span class="sxs-lookup"><span data-stu-id="06f74-158">Create linked services</span></span>
<span data-ttu-id="06f74-159">In this step, you link your Azure Storage account and an on-demand HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-159">In this step, you link your Azure Storage account and an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="06f74-160">The storage account holds the input and output data for the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="06f74-160">The storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="06f74-161">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="06f74-161">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="06f74-162">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario.</span><span class="sxs-lookup"><span data-stu-id="06f74-162">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario.</span></span> <span data-ttu-id="06f74-163">Then link those services to the data factory by creating linked services.</span><span class="sxs-lookup"><span data-stu-id="06f74-163">Then link those services to the data factory by creating linked services.</span></span>  

### <a name="create-a-storage-linked-service"></a><span data-ttu-id="06f74-164">Create a Storage linked service</span><span class="sxs-lookup"><span data-stu-id="06f74-164">Create a Storage linked service</span></span>
<span data-ttu-id="06f74-165">In this step, you link your storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-165">In this step, you link your storage account to your data factory.</span></span> <span data-ttu-id="06f74-166">In this tutorial, you use the same storage account to store input/output data and the HQL script file.</span><span class="sxs-lookup"><span data-stu-id="06f74-166">In this tutorial, you use the same storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="06f74-167">On the **Data factory** blade for **GetStartedDF**, select **Author and deploy**.</span><span class="sxs-lookup"><span data-stu-id="06f74-167">On the **Data factory** blade for **GetStartedDF**, select **Author and deploy**.</span></span> <span data-ttu-id="06f74-168">You see the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="06f74-168">You see the Data Factory Editor.</span></span>

   ![Author and deploy tile](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)

1. <span data-ttu-id="06f74-170">Select **New data store**, and choose **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="06f74-170">Select **New data store**, and choose **Azure Storage**.</span></span>

   ![New data store blade](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)

1. <span data-ttu-id="06f74-172">You see the JSON script for creating a Storage linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="06f74-172">You see the JSON script for creating a Storage linked service in the editor.</span></span>

   ![Storage linked service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)

1. <span data-ttu-id="06f74-174">Replace **account name** with the name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="06f74-174">Replace **account name** with the name of your storage account.</span></span> <span data-ttu-id="06f74-175">Replace **account key** with the access key of the storage account.</span><span class="sxs-lookup"><span data-stu-id="06f74-175">Replace **account key** with the access key of the storage account.</span></span> <span data-ttu-id="06f74-176">To learn how to get your storage access key, see how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="06f74-176">To learn how to get your storage access key, see how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

1. <span data-ttu-id="06f74-177">Select **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="06f74-177">Select **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Deploy button](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="06f74-179">After the linked service is deployed successfully, the Draft-1 window disappears.</span><span class="sxs-lookup"><span data-stu-id="06f74-179">After the linked service is deployed successfully, the Draft-1 window disappears.</span></span> <span data-ttu-id="06f74-180">You see **AzureStorageLinkedService** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="06f74-180">You see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![AzureStorageLinkedService](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-an-hdinsight-linked-service"></a><span data-ttu-id="06f74-182">Create an HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="06f74-182">Create an HDInsight linked service</span></span>
<span data-ttu-id="06f74-183">In this step, you link an on-demand HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-183">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="06f74-184">The HDInsight cluster is automatically created at runtime.</span><span class="sxs-lookup"><span data-stu-id="06f74-184">The HDInsight cluster is automatically created at runtime.</span></span> <span data-ttu-id="06f74-185">After it's done processing and idle for the specified amount of time, it's deleted.</span><span class="sxs-lookup"><span data-stu-id="06f74-185">After it's done processing and idle for the specified amount of time, it's deleted.</span></span>

1. <span data-ttu-id="06f74-186">In the Data Factory Editor, select **More** > **New compute** > **On-demand HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="06f74-186">In the Data Factory Editor, select **More** > **New compute** > **On-demand HDInsight cluster**.</span></span>

    ![New compute](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)

1. <span data-ttu-id="06f74-188">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="06f74-188">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="06f74-189">The JSON snippet describes the properties that are used to create the HDInsight cluster on demand.</span><span class="sxs-lookup"><span data-stu-id="06f74-189">The JSON snippet describes the properties that are used to create the HDInsight cluster on demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="06f74-190">The following table provides descriptions for the JSON properties used in the snippet.</span><span class="sxs-lookup"><span data-stu-id="06f74-190">The following table provides descriptions for the JSON properties used in the snippet.</span></span>

   | <span data-ttu-id="06f74-191">Property</span><span class="sxs-lookup"><span data-stu-id="06f74-191">Property</span></span> | <span data-ttu-id="06f74-192">Description</span><span class="sxs-lookup"><span data-stu-id="06f74-192">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="06f74-193">clusterSize</span><span class="sxs-lookup"><span data-stu-id="06f74-193">clusterSize</span></span> |<span data-ttu-id="06f74-194">Specifies the size of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="06f74-194">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="06f74-195">timeToLive</span><span class="sxs-lookup"><span data-stu-id="06f74-195">timeToLive</span></span> | <span data-ttu-id="06f74-196">Specifies the idle time for the HDInsight cluster before it's deleted.</span><span class="sxs-lookup"><span data-stu-id="06f74-196">Specifies the idle time for the HDInsight cluster before it's deleted.</span></span> |
   | <span data-ttu-id="06f74-197">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="06f74-197">linkedServiceName</span></span> | <span data-ttu-id="06f74-198">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06f74-198">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="06f74-199">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="06f74-199">Note the following points:</span></span>

     <span data-ttu-id="06f74-200">a.</span><span class="sxs-lookup"><span data-stu-id="06f74-200">a.</span></span> <span data-ttu-id="06f74-201">The data factory creates a Linux-based HDInsight cluster for you with the JSON properties.</span><span class="sxs-lookup"><span data-stu-id="06f74-201">The data factory creates a Linux-based HDInsight cluster for you with the JSON properties.</span></span> <span data-ttu-id="06f74-202">For more information, see [On-demand HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="06f74-202">For more information, see [On-demand HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span>

     <span data-ttu-id="06f74-203">b.</span><span class="sxs-lookup"><span data-stu-id="06f74-203">b.</span></span> <span data-ttu-id="06f74-204">You can use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="06f74-204">You can use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="06f74-205">For more information, see [HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="06f74-205">For more information, see [HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span></span>

     <span data-ttu-id="06f74-206">c.</span><span class="sxs-lookup"><span data-stu-id="06f74-206">c.</span></span> <span data-ttu-id="06f74-207">The HDInsight cluster creates a default container in the blob storage you specified in the JSON property (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="06f74-207">The HDInsight cluster creates a default container in the blob storage you specified in the JSON property (**linkedServiceName**).</span></span> <span data-ttu-id="06f74-208">HDInsight doesn't delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="06f74-208">HDInsight doesn't delete this container when the cluster is deleted.</span></span> <span data-ttu-id="06f74-209">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="06f74-209">This behavior is by design.</span></span> <span data-ttu-id="06f74-210">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="06f74-210">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="06f74-211">The cluster is automatically deleted when the processing is finished.</span><span class="sxs-lookup"><span data-stu-id="06f74-211">The cluster is automatically deleted when the processing is finished.</span></span>

     <span data-ttu-id="06f74-212">As more slices are processed, you see many containers in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="06f74-212">As more slices are processed, you see many containers in your blob storage.</span></span> <span data-ttu-id="06f74-213">If you don't need them for troubleshooting of the jobs, you might want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="06f74-213">If you don't need them for troubleshooting of the jobs, you might want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="06f74-214">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp."</span><span class="sxs-lookup"><span data-stu-id="06f74-214">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp."</span></span> <span data-ttu-id="06f74-215">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to delete containers in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="06f74-215">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to delete containers in your blob storage.</span></span>

     <span data-ttu-id="06f74-216">For more information, see [On-demand HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="06f74-216">For more information, see [On-demand HDInsight linked service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span>

1. <span data-ttu-id="06f74-217">Select **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="06f74-217">Select **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Deploy option](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)

1. <span data-ttu-id="06f74-219">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="06f74-219">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Tree view with linked services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="06f74-221">Create datasets</span><span class="sxs-lookup"><span data-stu-id="06f74-221">Create datasets</span></span>
<span data-ttu-id="06f74-222">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="06f74-222">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="06f74-223">These datasets refer to AzureStorageLinkedService that you created previously in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="06f74-223">These datasets refer to AzureStorageLinkedService that you created previously in this tutorial.</span></span> <span data-ttu-id="06f74-224">The linked service points to a storage account.</span><span class="sxs-lookup"><span data-stu-id="06f74-224">The linked service points to a storage account.</span></span> <span data-ttu-id="06f74-225">Datasets specify the container, folder, and file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="06f74-225">Datasets specify the container, folder, and file name in the storage that holds input and output data.</span></span>   

### <a name="create-the-input-dataset"></a><span data-ttu-id="06f74-226">Create the input dataset</span><span class="sxs-lookup"><span data-stu-id="06f74-226">Create the input dataset</span></span>
1. <span data-ttu-id="06f74-227">In the Data Factory Editor, select **More** > **New dataset** > **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="06f74-227">In the Data Factory Editor, select **More** > **New dataset** > **Azure Blob storage**.</span></span>

    ![New dataset](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)

1. <span data-ttu-id="06f74-229">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="06f74-229">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="06f74-230">In the JSON snippet, you create a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-230">In the JSON snippet, you create a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="06f74-231">In addition, you specify that the input data is in the blob container called **adfgetstarted** and the folder called **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="06f74-231">In addition, you specify that the input data is in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

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
    <span data-ttu-id="06f74-232">The following table provides descriptions for the JSON properties used in the snippet.</span><span class="sxs-lookup"><span data-stu-id="06f74-232">The following table provides descriptions for the JSON properties used in the snippet.</span></span>

   | <span data-ttu-id="06f74-233">Property</span><span class="sxs-lookup"><span data-stu-id="06f74-233">Property</span></span> | <span data-ttu-id="06f74-234">Description</span><span class="sxs-lookup"><span data-stu-id="06f74-234">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="06f74-235">type</span><span class="sxs-lookup"><span data-stu-id="06f74-235">type</span></span> |<span data-ttu-id="06f74-236">The type property is set to **AzureBlob** because data resides in blob storage.</span><span class="sxs-lookup"><span data-stu-id="06f74-236">The type property is set to **AzureBlob** because data resides in blob storage.</span></span> |
   | <span data-ttu-id="06f74-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="06f74-237">linkedServiceName</span></span> |<span data-ttu-id="06f74-238">Refers to AzureStorageLinkedService that you created previously.</span><span class="sxs-lookup"><span data-stu-id="06f74-238">Refers to AzureStorageLinkedService that you created previously.</span></span> |
   | <span data-ttu-id="06f74-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="06f74-239">folderPath</span></span> | <span data-ttu-id="06f74-240">Specifies the blob container and the folder that contains input blobs.</span><span class="sxs-lookup"><span data-stu-id="06f74-240">Specifies the blob container and the folder that contains input blobs.</span></span> | 
   | <span data-ttu-id="06f74-241">fileName</span><span class="sxs-lookup"><span data-stu-id="06f74-241">fileName</span></span> |<span data-ttu-id="06f74-242">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="06f74-242">This property is optional.</span></span> <span data-ttu-id="06f74-243">If you omit this property, all the files from folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="06f74-243">If you omit this property, all the files from folderPath are picked.</span></span> <span data-ttu-id="06f74-244">In this tutorial, only the input.log file is processed.</span><span class="sxs-lookup"><span data-stu-id="06f74-244">In this tutorial, only the input.log file is processed.</span></span> |
   | <span data-ttu-id="06f74-245">type</span><span class="sxs-lookup"><span data-stu-id="06f74-245">type</span></span> |<span data-ttu-id="06f74-246">The log files are in text format, so use **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="06f74-246">The log files are in text format, so use **TextFormat**.</span></span> |
   | <span data-ttu-id="06f74-247">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="06f74-247">columnDelimiter</span></span> |<span data-ttu-id="06f74-248">Columns in the log files are delimited by the comma character (`,`).</span><span class="sxs-lookup"><span data-stu-id="06f74-248">Columns in the log files are delimited by the comma character (`,`).</span></span> |
   | <span data-ttu-id="06f74-249">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="06f74-249">frequency/interval</span></span> |<span data-ttu-id="06f74-250">Frequency is set to **Month** and the interval is **1**, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="06f74-250">Frequency is set to **Month** and the interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="06f74-251">external</span><span class="sxs-lookup"><span data-stu-id="06f74-251">external</span></span> | <span data-ttu-id="06f74-252">This property is set to **true** if the input data isn't generated by this pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-252">This property is set to **true** if the input data isn't generated by this pipeline.</span></span> <span data-ttu-id="06f74-253">In this tutorial, the input.log file isn't generated by this pipeline, so the property is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="06f74-253">In this tutorial, the input.log file isn't generated by this pipeline, so the property is set to **true**.</span></span> |

    <span data-ttu-id="06f74-254">For more information about these JSON properties, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06f74-254">For more information about these JSON properties, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

1. <span data-ttu-id="06f74-255">Select **Deploy** on the command bar to deploy the newly created dataset.</span><span class="sxs-lookup"><span data-stu-id="06f74-255">Select **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="06f74-256">You see the dataset in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="06f74-256">You see the dataset in the tree view on the left.</span></span>

### <a name="create-the-output-dataset"></a><span data-ttu-id="06f74-257">Create the output dataset</span><span class="sxs-lookup"><span data-stu-id="06f74-257">Create the output dataset</span></span>
<span data-ttu-id="06f74-258">Now, you create the output dataset to represent the output data stored in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="06f74-258">Now, you create the output dataset to represent the output data stored in the blob storage.</span></span>

1. <span data-ttu-id="06f74-259">In the Data Factory Editor, select **More** > **New dataset** > **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="06f74-259">In the Data Factory Editor, select **More** > **New dataset** > **Azure Blob storage**.</span></span>

1. <span data-ttu-id="06f74-260">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="06f74-260">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="06f74-261">In the JSON snippet, you create a dataset called **AzureBlobOutput** to specify the structure of the data that is produced by the Hive script.</span><span class="sxs-lookup"><span data-stu-id="06f74-261">In the JSON snippet, you create a dataset called **AzureBlobOutput** to specify the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="06f74-262">You also specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="06f74-262">You also specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="06f74-263">The **availability** section specifies that the output dataset is produced monthly.</span><span class="sxs-lookup"><span data-stu-id="06f74-263">The **availability** section specifies that the output dataset is produced monthly.</span></span>

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
    <span data-ttu-id="06f74-264">For descriptions of these properties, see the section "Create the input dataset."</span><span class="sxs-lookup"><span data-stu-id="06f74-264">For descriptions of these properties, see the section "Create the input dataset."</span></span> <span data-ttu-id="06f74-265">You do not set the external property on an output dataset because the dataset is produced by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="06f74-265">You do not set the external property on an output dataset because the dataset is produced by the Data Factory service.</span></span>

1. <span data-ttu-id="06f74-266">Select **Deploy** on the command bar to deploy the newly created dataset.</span><span class="sxs-lookup"><span data-stu-id="06f74-266">Select **Deploy** on the command bar to deploy the newly created dataset.</span></span>

1. <span data-ttu-id="06f74-267">Verify that the dataset is created successfully.</span><span class="sxs-lookup"><span data-stu-id="06f74-267">Verify that the dataset is created successfully.</span></span>

    ![Tree view with linked services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-a-pipeline"></a><span data-ttu-id="06f74-269">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="06f74-269">Create a pipeline</span></span>
<span data-ttu-id="06f74-270">In this step, you create your first pipeline with an HDInsight Hive activity.</span><span class="sxs-lookup"><span data-stu-id="06f74-270">In this step, you create your first pipeline with an HDInsight Hive activity.</span></span> <span data-ttu-id="06f74-271">The input slice is available monthly (frequency is Month, interval is 1).</span><span class="sxs-lookup"><span data-stu-id="06f74-271">The input slice is available monthly (frequency is Month, interval is 1).</span></span> <span data-ttu-id="06f74-272">The output slice is produced monthly.</span><span class="sxs-lookup"><span data-stu-id="06f74-272">The output slice is produced monthly.</span></span> <span data-ttu-id="06f74-273">The scheduler property for the activity is also set to monthly.</span><span class="sxs-lookup"><span data-stu-id="06f74-273">The scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="06f74-274">The settings for the output dataset and the activity scheduler must match.</span><span class="sxs-lookup"><span data-stu-id="06f74-274">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="06f74-275">Currently, the output dataset is what drives the schedule, so you must create an output dataset even if the activity doesn't produce any output.</span><span class="sxs-lookup"><span data-stu-id="06f74-275">Currently, the output dataset is what drives the schedule, so you must create an output dataset even if the activity doesn't produce any output.</span></span> <span data-ttu-id="06f74-276">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="06f74-276">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="06f74-277">The properties used in the following JSON snippet are explained at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="06f74-277">The properties used in the following JSON snippet are explained at the end of this section.</span></span>

1. <span data-ttu-id="06f74-278">In the Data Factory Editor, select **More** > **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="06f74-278">In the Data Factory Editor, select **More** > **New pipeline**.</span></span>

    ![New pipeline option](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)

1. <span data-ttu-id="06f74-280">Copy and paste the following snippet to the Draft-1 window.</span><span class="sxs-lookup"><span data-stu-id="06f74-280">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > Replace **storageaccountname** with the name of your storage account in the JSON snippet.
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="06f74-282">In the JSON snippet, you create a pipeline that consists of a single activity that uses Hive to process data on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="06f74-282">In the JSON snippet, you create a pipeline that consists of a single activity that uses Hive to process data on an HDInsight cluster.</span></span>

    <span data-ttu-id="06f74-283">The Hive script file, **partitionweblogs.hql**, is stored in the storage account, which is specified by scriptLinkedService that is called **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="06f74-283">The Hive script file, **partitionweblogs.hql**, is stored in the storage account, which is specified by scriptLinkedService that is called **AzureStorageLinkedService**.</span></span> <span data-ttu-id="06f74-284">You can find it in the **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="06f74-284">You can find it in the **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="06f74-285">The **defines** section is used to specify the runtime settings that are passed to the Hive script as Hive configuration values.</span><span class="sxs-lookup"><span data-stu-id="06f74-285">The **defines** section is used to specify the runtime settings that are passed to the Hive script as Hive configuration values.</span></span> <span data-ttu-id="06f74-286">Examples are ${hiveconf:inputtable} and ${hiveconf:partitionedtable}.</span><span class="sxs-lookup"><span data-stu-id="06f74-286">Examples are ${hiveconf:inputtable} and ${hiveconf:partitionedtable}.</span></span>

    <span data-ttu-id="06f74-287">The **start** and **end** properties of the pipeline specify the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-287">The **start** and **end** properties of the pipeline specify the active period of the pipeline.</span></span>

    <span data-ttu-id="06f74-288">In the activity JSON, you specify that the Hive script runs on the compute specified by **linkedServiceName**: **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="06f74-288">In the activity JSON, you specify that the Hive script runs on the compute specified by **linkedServiceName**: **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > For more information about the JSON properties used in the example, see the "Pipeline JSON" section in [Pipelines and activities in Data Factory](data-factory-create-pipelines.md).
   >
   >
1. <span data-ttu-id="06f74-290">Confirm the following:</span><span class="sxs-lookup"><span data-stu-id="06f74-290">Confirm the following:</span></span>

   <span data-ttu-id="06f74-291">a.</span><span class="sxs-lookup"><span data-stu-id="06f74-291">a.</span></span> <span data-ttu-id="06f74-292">The **input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="06f74-292">The **input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the blob storage.</span></span>

   <span data-ttu-id="06f74-293">b.</span><span class="sxs-lookup"><span data-stu-id="06f74-293">b.</span></span> <span data-ttu-id="06f74-294">The **partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="06f74-294">The **partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the blob storage.</span></span> <span data-ttu-id="06f74-295">If you don't see these files, follow the steps in the "Prerequisites" section in [Tutorial overview](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="06f74-295">If you don't see these files, follow the steps in the "Prerequisites" section in [Tutorial overview](data-factory-build-your-first-pipeline.md).</span></span>

   <span data-ttu-id="06f74-296">c.</span><span class="sxs-lookup"><span data-stu-id="06f74-296">c.</span></span> <span data-ttu-id="06f74-297">You replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="06f74-297">You replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>

1. <span data-ttu-id="06f74-298">Select **Deploy** on the command bar to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-298">Select **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="06f74-299">Because the **start** and **end** times are set in the past and **isPaused** is set to **false**, the pipeline (activity in the pipeline) runs immediately after you deploy it.</span><span class="sxs-lookup"><span data-stu-id="06f74-299">Because the **start** and **end** times are set in the past and **isPaused** is set to **false**, the pipeline (activity in the pipeline) runs immediately after you deploy it.</span></span>

1. <span data-ttu-id="06f74-300">Confirm that you see the pipeline in the tree view.</span><span class="sxs-lookup"><span data-stu-id="06f74-300">Confirm that you see the pipeline in the tree view.</span></span>

    ![Tree view with pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)



## <a name="monitor-a-pipeline"></a><span data-ttu-id="06f74-302">Monitor a pipeline</span><span class="sxs-lookup"><span data-stu-id="06f74-302">Monitor a pipeline</span></span>
### <a name="monitor-a-pipeline-by-using-the-diagram-view"></a><span data-ttu-id="06f74-303">Monitor a pipeline by using the Diagram view</span><span class="sxs-lookup"><span data-stu-id="06f74-303">Monitor a pipeline by using the Diagram view</span></span>
1. <span data-ttu-id="06f74-304">On the **Data factory** blade, select **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="06f74-304">On the **Data factory** blade, select **Diagram**.</span></span>

    ![Diagram tile](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)

1. <span data-ttu-id="06f74-306">In the **Diagram** view, you see an overview of the pipelines and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="06f74-306">In the **Diagram** view, you see an overview of the pipelines and datasets used in this tutorial.</span></span>

    ![Diagram view](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)

1. <span data-ttu-id="06f74-308">To view all activities in the pipeline, right-click the pipeline in the diagram, and select **Open pipeline**.</span><span class="sxs-lookup"><span data-stu-id="06f74-308">To view all activities in the pipeline, right-click the pipeline in the diagram, and select **Open pipeline**.</span></span>

    ![Open pipeline menu](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)

1. <span data-ttu-id="06f74-310">Confirm that you see **Hive Activity** in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-310">Confirm that you see **Hive Activity** in the pipeline.</span></span>

    ![Open pipeline view](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="06f74-312">To go back to the previous view, select **Data factory** in the menu at the top.</span><span class="sxs-lookup"><span data-stu-id="06f74-312">To go back to the previous view, select **Data factory** in the menu at the top.</span></span>

1. <span data-ttu-id="06f74-313">In the **Diagram** view, double-click the dataset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="06f74-313">In the **Diagram** view, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="06f74-314">Confirm that the slice is in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="06f74-314">Confirm that the slice is in the **Ready** state.</span></span> <span data-ttu-id="06f74-315">It might take a couple of minutes for the slice to show up as **Ready**.</span><span class="sxs-lookup"><span data-stu-id="06f74-315">It might take a couple of minutes for the slice to show up as **Ready**.</span></span> <span data-ttu-id="06f74-316">If it doesn't appear after you wait for some time, see if you have the input file (**input.log**) placed in the right container (**adfgetstarted**) and folder (**inputdata**).</span><span class="sxs-lookup"><span data-stu-id="06f74-316">If it doesn't appear after you wait for some time, see if you have the input file (**input.log**) placed in the right container (**adfgetstarted**) and folder (**inputdata**).</span></span>

   ![Input slice in Ready state](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)

1. <span data-ttu-id="06f74-318">Close the **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="06f74-318">Close the **AzureBlobInput** blade.</span></span>

1. <span data-ttu-id="06f74-319">In the **Diagram** view, double-click the dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="06f74-319">In the **Diagram** view, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="06f74-320">You see the slice that is currently being processed.</span><span class="sxs-lookup"><span data-stu-id="06f74-320">You see the slice that is currently being processed.</span></span>

   ![Dataset processing in progress](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)

1. <span data-ttu-id="06f74-322">After the processing is finished, you see the slice in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="06f74-322">After the processing is finished, you see the slice in the **Ready** state.</span></span>

   ![Dataset in Ready state](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > Creation of an on-demand HDInsight cluster usually takes approximately 20 minutes. Expect the pipeline to take approximately 30 minutes to process the slice.
   >
   >

1. <span data-ttu-id="06f74-326">When the slice is in the **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="06f74-326">When the slice is in the **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![Output data](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)

1. <span data-ttu-id="06f74-328">Select the slice to see more information about it in a **Data slice** blade.</span><span class="sxs-lookup"><span data-stu-id="06f74-328">Select the slice to see more information about it in a **Data slice** blade.</span></span>

    ![Data slice information](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)

1. <span data-ttu-id="06f74-330">In the **Activity runs** list, select an activity run to see more information about it.</span><span class="sxs-lookup"><span data-stu-id="06f74-330">In the **Activity runs** list, select an activity run to see more information about it.</span></span> <span data-ttu-id="06f74-331">(In this scenario, it's a Hive activity.) The information appears in an **Activity run details** blade.</span><span class="sxs-lookup"><span data-stu-id="06f74-331">(In this scenario, it's a Hive activity.) The information appears in an **Activity run details** blade.</span></span>   

    ![Activity run details window](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="06f74-333">From the log files, you can see the Hive query that was executed and the status information.</span><span class="sxs-lookup"><span data-stu-id="06f74-333">From the log files, you can see the Hive query that was executed and the status information.</span></span> <span data-ttu-id="06f74-334">These logs are useful for troubleshooting any issues.</span><span class="sxs-lookup"><span data-stu-id="06f74-334">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="06f74-335">For more information, see [Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="06f74-335">For more information, see [Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span></span>

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (**input.log**) to the **inputdata** folder of the **adfgetstarted** container.
>
>

### <a name="monitor-a-pipeline-by-using-the-monitor--manage-app"></a><span data-ttu-id="06f74-338">Monitor a pipeline by using the Monitor & Manage app</span><span class="sxs-lookup"><span data-stu-id="06f74-338">Monitor a pipeline by using the Monitor & Manage app</span></span>
<span data-ttu-id="06f74-339">You also can use the Monitor & Manage application to monitor your pipelines.</span><span class="sxs-lookup"><span data-stu-id="06f74-339">You also can use the Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="06f74-340">For more information about how to use this application, see [Monitor and manage Data Factory pipelines by using the Monitor & Manage app](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="06f74-340">For more information about how to use this application, see [Monitor and manage Data Factory pipelines by using the Monitor & Manage app](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="06f74-341">Select the **Monitor & Manage** tile on the home page for your data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-341">Select the **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![Monitor & Manage tile](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)

1. <span data-ttu-id="06f74-343">In the Monitor & Manage application, change the **Start time** and **End time** to match the start and end times of your pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-343">In the Monitor & Manage application, change the **Start time** and **End time** to match the start and end times of your pipeline.</span></span> <span data-ttu-id="06f74-344">Select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="06f74-344">Select **Apply**.</span></span>

    ![Monitor & Manage app](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)

1. <span data-ttu-id="06f74-346">Select an activity window in the **Activity Windows** list to see information about it.</span><span class="sxs-lookup"><span data-stu-id="06f74-346">Select an activity window in the **Activity Windows** list to see information about it.</span></span>

    ![Activity Windows list](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="06f74-348">Summary</span><span class="sxs-lookup"><span data-stu-id="06f74-348">Summary</span></span>
<span data-ttu-id="06f74-349">In this tutorial, you created a data factory to process data by running a Hive script on an HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="06f74-349">In this tutorial, you created a data factory to process data by running a Hive script on an HDInsight Hadoop cluster.</span></span> <span data-ttu-id="06f74-350">You used the Data Factory Editor in the Azure portal to do the following:</span><span class="sxs-lookup"><span data-stu-id="06f74-350">You used the Data Factory Editor in the Azure portal to do the following:</span></span>  

* <span data-ttu-id="06f74-351">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-351">Create a data factory.</span></span>
* <span data-ttu-id="06f74-352">Create two linked services:</span><span class="sxs-lookup"><span data-stu-id="06f74-352">Create two linked services:</span></span>
   * <span data-ttu-id="06f74-353">A Storage linked service to link your blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-353">A Storage linked service to link your blob storage that holds input/output files to the data factory.</span></span>
   * <span data-ttu-id="06f74-354">An HDInsight on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-354">An HDInsight on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="06f74-355">Data Factory creates an HDInsight Hadoop cluster just in time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="06f74-355">Data Factory creates an HDInsight Hadoop cluster just in time to process input data and produce output data.</span></span>
* <span data-ttu-id="06f74-356">Create two datasets, which describe input and output data for an HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="06f74-356">Create two datasets, which describe input and output data for an HDInsight Hive activity in the pipeline.</span></span>
* <span data-ttu-id="06f74-357">Create a pipeline with an HDInsight Hive activity.</span><span class="sxs-lookup"><span data-stu-id="06f74-357">Create a pipeline with an HDInsight Hive activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06f74-358">Next steps</span><span class="sxs-lookup"><span data-stu-id="06f74-358">Next steps</span></span>
<span data-ttu-id="06f74-359">In this article, you created a pipeline with a transformation activity (HDInsight activity) that runs a Hive script on an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="06f74-359">In this article, you created a pipeline with a transformation activity (HDInsight activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="06f74-360">To see how to use a Copy activity to copy data from blob storage to a SQL database, see [Tutorial: Copy data from Blob storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="06f74-360">To see how to use a Copy activity to copy data from blob storage to a SQL database, see [Tutorial: Copy data from Blob storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="06f74-361">See also</span><span class="sxs-lookup"><span data-stu-id="06f74-361">See also</span></span>
| <span data-ttu-id="06f74-362">Topic</span><span class="sxs-lookup"><span data-stu-id="06f74-362">Topic</span></span> | <span data-ttu-id="06f74-363">Description</span><span class="sxs-lookup"><span data-stu-id="06f74-363">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="06f74-364">Pipelines</span><span class="sxs-lookup"><span data-stu-id="06f74-364">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="06f74-365">This article helps you understand pipelines and activities in Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="06f74-365">This article helps you understand pipelines and activities in Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="06f74-366">Datasets</span><span class="sxs-lookup"><span data-stu-id="06f74-366">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="06f74-367">This article helps you understand datasets in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="06f74-367">This article helps you understand datasets in Data Factory.</span></span> |
| [<span data-ttu-id="06f74-368">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="06f74-368">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="06f74-369">This article explains the scheduling and execution aspects of the Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="06f74-369">This article explains the scheduling and execution aspects of the Data Factory application model.</span></span> |
| [<span data-ttu-id="06f74-370">Monitor and manage pipelines by using the Monitor & Manage app</span><span class="sxs-lookup"><span data-stu-id="06f74-370">Monitor and manage pipelines by using the Monitor & Manage app</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="06f74-371">This article describes how to monitor, manage, and debug pipelines by using the Monitor & Manage app.</span><span class="sxs-lookup"><span data-stu-id="06f74-371">This article describes how to monitor, manage, and debug pipelines by using the Monitor & Manage app.</span></span> |
