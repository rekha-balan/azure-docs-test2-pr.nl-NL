---
title: Load data into Azure Data Lake Storage Gen2 (Preview) with Azure Data Factory
description: Use Azure Data Factory to copy data into Azure Data Lake Storage Gen2 (Preview)
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 07/06/2018
ms.author: jingwang
ms.openlocfilehash: 558b426ea85decb0309390e36910eb18719e6e99
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868269"
---
# <a name="load-data-into-azure-data-lake-storage-gen2-preview-with-azure-data-factory"></a><span data-ttu-id="f12d4-103">Load data into Azure Data Lake Storage Gen2 (Preview) with Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f12d4-103">Load data into Azure Data Lake Storage Gen2 (Preview) with Azure Data Factory</span></span>

<span data-ttu-id="f12d4-104">[Azure Data Lake Storage Gen2 (Preview)](../storage/data-lake-storage/introduction.md) adds a protocol with hierarchical file system namespace and security features to Azure Blob Storage making it easy to connect analytics frameworks to a durable storage layer.</span><span class="sxs-lookup"><span data-stu-id="f12d4-104">[Azure Data Lake Storage Gen2 (Preview)](../storage/data-lake-storage/introduction.md) adds a protocol with hierarchical file system namespace and security features to Azure Blob Storage making it easy to connect analytics frameworks to a durable storage layer.</span></span> <span data-ttu-id="f12d4-105">In Data Lake Storage Gen2 (Preview), all the qualities of object storage remain while adding the advantages of a file system interface.</span><span class="sxs-lookup"><span data-stu-id="f12d4-105">In Data Lake Storage Gen2 (Preview), all the qualities of object storage remain while adding the advantages of a file system interface.</span></span>

<span data-ttu-id="f12d4-106">Azure Data Factory is a fully managed cloud-based data integration service.</span><span class="sxs-lookup"><span data-stu-id="f12d4-106">Azure Data Factory is a fully managed cloud-based data integration service.</span></span> <span data-ttu-id="f12d4-107">You can use the service to populate the lake with data from a rich set of on-premises and cloud-based data stores and save time when building your analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="f12d4-107">You can use the service to populate the lake with data from a rich set of on-premises and cloud-based data stores and save time when building your analytics solutions.</span></span> <span data-ttu-id="f12d4-108">For a detailed list of supported connectors, see the table of [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f12d4-108">For a detailed list of supported connectors, see the table of [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>

<span data-ttu-id="f12d4-109">Azure Data Factory offers a scale-out, managed data movement solution.</span><span class="sxs-lookup"><span data-stu-id="f12d4-109">Azure Data Factory offers a scale-out, managed data movement solution.</span></span> <span data-ttu-id="f12d4-110">Due to the scale-out architecture of ADF, it can ingest data at a high throughput.</span><span class="sxs-lookup"><span data-stu-id="f12d4-110">Due to the scale-out architecture of ADF, it can ingest data at a high throughput.</span></span> <span data-ttu-id="f12d4-111">For details, see [Copy activity performance](copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f12d4-111">For details, see [Copy activity performance](copy-activity-performance.md).</span></span>

<span data-ttu-id="f12d4-112">This article shows you how to use the Data Factory Copy Data tool to load data from _Amazon Web Services S3 service_ into _Azure Data Lake Storage Gen2_.</span><span class="sxs-lookup"><span data-stu-id="f12d4-112">This article shows you how to use the Data Factory Copy Data tool to load data from _Amazon Web Services S3 service_ into _Azure Data Lake Storage Gen2_.</span></span> <span data-ttu-id="f12d4-113">You can follow similar steps to copy data from other types of data stores.</span><span class="sxs-lookup"><span data-stu-id="f12d4-113">You can follow similar steps to copy data from other types of data stores.</span></span>

>[!TIP]
><span data-ttu-id="f12d4-114">For copying data from Azure Data Lake Storage Gen1 into Gen2, refer to [this specific walkthrough](load-azure-data-lake-storage-gen2-from-gen1.md).</span><span class="sxs-lookup"><span data-stu-id="f12d4-114">For copying data from Azure Data Lake Storage Gen1 into Gen2, refer to [this specific walkthrough](load-azure-data-lake-storage-gen2-from-gen1.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f12d4-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f12d4-115">Prerequisites</span></span>

* <span data-ttu-id="f12d4-116">Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f12d4-116">Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>
* <span data-ttu-id="f12d4-117">Azure Storage account with Data Lake Storage Gen2 enabled: If you don't have a Storage account, click [here](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) to create one.</span><span class="sxs-lookup"><span data-stu-id="f12d4-117">Azure Storage account with Data Lake Storage Gen2 enabled: If you don't have a Storage account, click [here](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) to create one.</span></span>
* <span data-ttu-id="f12d4-118">AWS account with an S3 bucket that contains data: This article shows how to copy data from Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="f12d4-118">AWS account with an S3 bucket that contains data: This article shows how to copy data from Amazon S3.</span></span> <span data-ttu-id="f12d4-119">You can use other data stores by following similar steps.</span><span class="sxs-lookup"><span data-stu-id="f12d4-119">You can use other data stores by following similar steps.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="f12d4-120">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="f12d4-120">Create a data factory</span></span>

1. <span data-ttu-id="f12d4-121">On the left menu, select **New** > **Data + Analytics** > **Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-121">On the left menu, select **New** > **Data + Analytics** > **Data Factory**:</span></span>
   
   ![Create a new data factory](./media/load-azure-data-lake-storage-gen2/new-azure-data-factory-menu.png)
2. <span data-ttu-id="f12d4-123">In the **New data factory** page, provide values for the fields that are shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="f12d4-123">In the **New data factory** page, provide values for the fields that are shown in the following image:</span></span> 
      
   ![New data factory page](./media/load-azure-data-lake-storage-gen2//new-azure-data-factory.png)
 
    * <span data-ttu-id="f12d4-125">**Name**: Enter a globally unique name for your Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="f12d4-125">**Name**: Enter a globally unique name for your Azure data factory.</span></span> <span data-ttu-id="f12d4-126">If you receive the error "Data factory name \"LoadADLSDemo\" is not available," enter a different name for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f12d4-126">If you receive the error "Data factory name \"LoadADLSDemo\" is not available," enter a different name for the data factory.</span></span> <span data-ttu-id="f12d4-127">For example, you could use the name _**yourname**_**ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="f12d4-127">For example, you could use the name _**yourname**_**ADFTutorialDataFactory**.</span></span> <span data-ttu-id="f12d4-128">Try creating the data factory again.</span><span class="sxs-lookup"><span data-stu-id="f12d4-128">Try creating the data factory again.</span></span> <span data-ttu-id="f12d4-129">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="f12d4-129">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>
    * <span data-ttu-id="f12d4-130">**Subscription**: Select your Azure subscription in which to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="f12d4-130">**Subscription**: Select your Azure subscription in which to create the data factory.</span></span> 
    * <span data-ttu-id="f12d4-131">**Resource Group**: Select an existing resource group from the drop-down list, or select the **Create new** option and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="f12d4-131">**Resource Group**: Select an existing resource group from the drop-down list, or select the **Create new** option and enter the name of a resource group.</span></span> <span data-ttu-id="f12d4-132">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f12d4-132">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
    * <span data-ttu-id="f12d4-133">**Version**: Select **V2**.</span><span class="sxs-lookup"><span data-stu-id="f12d4-133">**Version**: Select **V2**.</span></span>
    * <span data-ttu-id="f12d4-134">**Location**: Select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f12d4-134">**Location**: Select the location for the data factory.</span></span> <span data-ttu-id="f12d4-135">Only supported locations are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f12d4-135">Only supported locations are displayed in the drop-down list.</span></span> <span data-ttu-id="f12d4-136">The data stores that are used by data factory can be in other locations and regions.</span><span class="sxs-lookup"><span data-stu-id="f12d4-136">The data stores that are used by data factory can be in other locations and regions.</span></span> 

3. <span data-ttu-id="f12d4-137">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f12d4-137">Select **Create**.</span></span>
4. <span data-ttu-id="f12d4-138">After creation is complete, go to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f12d4-138">After creation is complete, go to your data factory.</span></span> <span data-ttu-id="f12d4-139">You see the **Data Factory** home page as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="f12d4-139">You see the **Data Factory** home page as shown in the following image:</span></span> 
   
   ![Data factory home page](./media/load-azure-data-lake-storage-gen2/data-factory-home-page.png)

   <span data-ttu-id="f12d4-141">Select the **Author & Monitor** tile to launch the Data Integration Application in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="f12d4-141">Select the **Author & Monitor** tile to launch the Data Integration Application in a separate tab.</span></span>

## <a name="load-data-into-azure-data-lake-storage-gen2"></a><span data-ttu-id="f12d4-142">Load data into Azure Data Lake Storage Gen2</span><span class="sxs-lookup"><span data-stu-id="f12d4-142">Load data into Azure Data Lake Storage Gen2</span></span>

1. <span data-ttu-id="f12d4-143">In the **Get started** page, select the **Copy Data** tile to launch the Copy Data tool:</span><span class="sxs-lookup"><span data-stu-id="f12d4-143">In the **Get started** page, select the **Copy Data** tile to launch the Copy Data tool:</span></span> 

   ![Copy Data tool tile](./media/load-azure-data-lake-storage-gen2/copy-data-tool-tile.png)
2. <span data-ttu-id="f12d4-145">In the **Properties** page, specify **CopyFromAmazonS3ToADLS** for the **Task name** field, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-145">In the **Properties** page, specify **CopyFromAmazonS3ToADLS** for the **Task name** field, and select **Next**:</span></span>

    ![Properties page](./media/load-azure-data-lake-storage-gen2/copy-data-tool-properties-page.png)
3. <span data-ttu-id="f12d4-147">In the **Source data store** page, click **+ Create new connection**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-147">In the **Source data store** page, click **+ Create new connection**:</span></span>

    ![Source data store page](./media/load-azure-data-lake-storage-gen2/source-data-store-page.png)
    
    <span data-ttu-id="f12d4-149">Select **Amazon S3** from the connector gallery, and select **Continue**</span><span class="sxs-lookup"><span data-stu-id="f12d4-149">Select **Amazon S3** from the connector gallery, and select **Continue**</span></span>
    
    ![Source data store s3 page](./media/load-azure-data-lake-storage-gen2/source-data-store-page-s3.png)
    
4. <span data-ttu-id="f12d4-151">In the **Specify Amazon S3 connection** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="f12d4-151">In the **Specify Amazon S3 connection** page, do the following steps:</span></span>
   1. <span data-ttu-id="f12d4-152">Specify the **Access Key ID** value.</span><span class="sxs-lookup"><span data-stu-id="f12d4-152">Specify the **Access Key ID** value.</span></span>
   2. <span data-ttu-id="f12d4-153">Specify the **Secret Access Key** value.</span><span class="sxs-lookup"><span data-stu-id="f12d4-153">Specify the **Secret Access Key** value.</span></span>
   3. <span data-ttu-id="f12d4-154">Click **Test connection** to validate the settings, then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f12d4-154">Click **Test connection** to validate the settings, then select **Finish**.</span></span>
   
   ![Specify Amazon S3 account](./media/load-azure-data-lake-storage-gen2/specify-amazon-s3-account.png)
   
   4. <span data-ttu-id="f12d4-156">You will see a new connection gets created.</span><span class="sxs-lookup"><span data-stu-id="f12d4-156">You will see a new connection gets created.</span></span> <span data-ttu-id="f12d4-157">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f12d4-157">Select **Next**.</span></span>
   
5. <span data-ttu-id="f12d4-158">In the **Choose the input file or folder** page, browse to the folder and file that you want to copy over.</span><span class="sxs-lookup"><span data-stu-id="f12d4-158">In the **Choose the input file or folder** page, browse to the folder and file that you want to copy over.</span></span> <span data-ttu-id="f12d4-159">Select the folder/file, select **Choose**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-159">Select the folder/file, select **Choose**:</span></span>

    ![Choose input file or folder](./media/load-azure-data-lake-storage-gen2/choose-input-folder.png)

6. <span data-ttu-id="f12d4-161">Specify the copy behavior by checking the **Copy files recursively** and **Binary copy** options.</span><span class="sxs-lookup"><span data-stu-id="f12d4-161">Specify the copy behavior by checking the **Copy files recursively** and **Binary copy** options.</span></span> <span data-ttu-id="f12d4-162">Select **Next**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-162">Select **Next**:</span></span>

    ![Specify output folder](./media/load-azure-data-lake-storage-gen2/specify-binary-copy.png)
    
7. <span data-ttu-id="f12d4-164">In the **Destination data store** page, click **+ Create new connection**, and then select **Azure Data Lake Storage Gen2 (Preview)**, and select **Continue**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-164">In the **Destination data store** page, click **+ Create new connection**, and then select **Azure Data Lake Storage Gen2 (Preview)**, and select **Continue**:</span></span>

    ![Destination data store page](./media/load-azure-data-lake-storage-gen2/destination-data-storage-page.png)

8. <span data-ttu-id="f12d4-166">In the **Specify Azure Data Lake Storage connection** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="f12d4-166">In the **Specify Azure Data Lake Storage connection** page, do the following steps:</span></span>

   1. <span data-ttu-id="f12d4-167">Select your Data Lake Storage Gen2 capable account from the "Storage account name" drop down list.</span><span class="sxs-lookup"><span data-stu-id="f12d4-167">Select your Data Lake Storage Gen2 capable account from the "Storage account name" drop down list.</span></span>
   2. <span data-ttu-id="f12d4-168">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f12d4-168">Select **Next**.</span></span>
   
   ![Specify Azure Data Lake Storage Gen2 account](./media/load-azure-data-lake-storage-gen2/specify-adls.png)

9. <span data-ttu-id="f12d4-170">In the **Choose the output file or folder** page, enter **copyfroms3** as the output folder name, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-170">In the **Choose the output file or folder** page, enter **copyfroms3** as the output folder name, and select **Next**:</span></span> 

    ![Specify output folder](./media/load-azure-data-lake-storage-gen2/specify-adls-path.png)

10. <span data-ttu-id="f12d4-172">In the **Settings** page, select **Next** to use the default settings:</span><span class="sxs-lookup"><span data-stu-id="f12d4-172">In the **Settings** page, select **Next** to use the default settings:</span></span>

    ![Settings page](./media/load-azure-data-lake-storage-gen2/copy-settings.png)
11. <span data-ttu-id="f12d4-174">In the **Summary** page, review the settings, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="f12d4-174">In the **Summary** page, review the settings, and select **Next**:</span></span>

    ![Summary page](./media/load-azure-data-lake-storage-gen2/copy-summary.png)
12. <span data-ttu-id="f12d4-176">In the **Deployment page**, select **Monitor** to monitor the pipeline:</span><span class="sxs-lookup"><span data-stu-id="f12d4-176">In the **Deployment page**, select **Monitor** to monitor the pipeline:</span></span>

    ![Deployment page](./media/load-azure-data-lake-storage-gen2/deployment-page.png)
13. <span data-ttu-id="f12d4-178">Notice that the **Monitor** tab on the left is automatically selected.</span><span class="sxs-lookup"><span data-stu-id="f12d4-178">Notice that the **Monitor** tab on the left is automatically selected.</span></span> <span data-ttu-id="f12d4-179">The **Actions** column includes links to view activity run details and to rerun the pipeline:</span><span class="sxs-lookup"><span data-stu-id="f12d4-179">The **Actions** column includes links to view activity run details and to rerun the pipeline:</span></span>

    ![Monitor pipeline runs](./media/load-azure-data-lake-storage-gen2/monitor-pipeline-runs.png)

14. <span data-ttu-id="f12d4-181">To view activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="f12d4-181">To view activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="f12d4-182">There's only one activity (copy activity) in the pipeline, so you see only one entry.</span><span class="sxs-lookup"><span data-stu-id="f12d4-182">There's only one activity (copy activity) in the pipeline, so you see only one entry.</span></span> <span data-ttu-id="f12d4-183">To switch back to the pipeline runs view, select the **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="f12d4-183">To switch back to the pipeline runs view, select the **Pipelines** link at the top.</span></span> <span data-ttu-id="f12d4-184">Select **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="f12d4-184">Select **Refresh** to refresh the list.</span></span> 

    ![Monitor activity runs](./media/load-azure-data-lake-storage-gen2/monitor-activity-runs.png)

15. <span data-ttu-id="f12d4-186">To monitor the execution details for each copy activity, select the **Details** link (eyeglasses image) under **Actions** in the activity monitoring view.</span><span class="sxs-lookup"><span data-stu-id="f12d4-186">To monitor the execution details for each copy activity, select the **Details** link (eyeglasses image) under **Actions** in the activity monitoring view.</span></span> <span data-ttu-id="f12d4-187">You can monitor details like the volume of data copied from the source to the sink, data throughput, execution steps with corresponding duration, and used configurations:</span><span class="sxs-lookup"><span data-stu-id="f12d4-187">You can monitor details like the volume of data copied from the source to the sink, data throughput, execution steps with corresponding duration, and used configurations:</span></span>

    ![Monitor activity run details](./media/load-azure-data-lake-storage-gen2/monitor-activity-run-details.png)

16. <span data-ttu-id="f12d4-189">Verify that the data is copied into your Data Lake Storage Gen2 account.</span><span class="sxs-lookup"><span data-stu-id="f12d4-189">Verify that the data is copied into your Data Lake Storage Gen2 account.</span></span>

## <a name="best-practices"></a><span data-ttu-id="f12d4-190">Best practices</span><span class="sxs-lookup"><span data-stu-id="f12d4-190">Best practices</span></span>

<span data-ttu-id="f12d4-191">When copy large volume of data from file-based data store, you are suggested to:</span><span class="sxs-lookup"><span data-stu-id="f12d4-191">When copy large volume of data from file-based data store, you are suggested to:</span></span>

- <span data-ttu-id="f12d4-192">Partition the files into 10TB to 30TB fileset each.</span><span class="sxs-lookup"><span data-stu-id="f12d4-192">Partition the files into 10TB to 30TB fileset each.</span></span>
- <span data-ttu-id="f12d4-193">Do not trigger too many concurrent copy runs to avoid throttling from source or sink data stores.</span><span class="sxs-lookup"><span data-stu-id="f12d4-193">Do not trigger too many concurrent copy runs to avoid throttling from source or sink data stores.</span></span> <span data-ttu-id="f12d4-194">You can start with one copy run and monitor the throughput, then gradually add more as needed.</span><span class="sxs-lookup"><span data-stu-id="f12d4-194">You can start with one copy run and monitor the throughput, then gradually add more as needed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f12d4-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="f12d4-195">Next steps</span></span>

* [<span data-ttu-id="f12d4-196">Copy activity overview</span><span class="sxs-lookup"><span data-stu-id="f12d4-196">Copy activity overview</span></span>](copy-activity-overview.md)
* [<span data-ttu-id="f12d4-197">Azure Data Lake Storage Gen2 connector</span><span class="sxs-lookup"><span data-stu-id="f12d4-197">Azure Data Lake Storage Gen2 connector</span></span>](connector-azure-data-lake-storage.md)