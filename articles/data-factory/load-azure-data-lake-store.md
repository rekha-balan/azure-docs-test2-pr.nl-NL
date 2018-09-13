---
title: Load data into Azure Data Lake Storage Gen1 by using Azure Data Factory | Microsoft Docs
description: Use Azure Data Factory to copy data into Azure Data Lake Storage Gen1
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 01/17/2018
ms.author: jingwang
ms.openlocfilehash: e401508fc5ffc1de666f727ffbb7790005384fc1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856009"
---
# <a name="load-data-into-azure-data-lake-storage-gen1-by-using-azure-data-factory"></a><span data-ttu-id="b2328-103">Load data into Azure Data Lake Storage Gen1 by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b2328-103">Load data into Azure Data Lake Storage Gen1 by using Azure Data Factory</span></span>

<span data-ttu-id="b2328-104">[Azure Data Lake Storage Gen1](../data-lake-store/data-lake-store-overview.md) (previously known as Azure Data Lake Store) is an enterprise-wide hyper-scale repository for big data analytic workloads.</span><span class="sxs-lookup"><span data-stu-id="b2328-104">[Azure Data Lake Storage Gen1](../data-lake-store/data-lake-store-overview.md) (previously known as Azure Data Lake Store) is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="b2328-105">Azure Data Lake lets you capture data of any size, type, and ingestion speed.</span><span class="sxs-lookup"><span data-stu-id="b2328-105">Azure Data Lake lets you capture data of any size, type, and ingestion speed.</span></span> <span data-ttu-id="b2328-106">The data is captured in a single place for operational and exploratory analytics.</span><span class="sxs-lookup"><span data-stu-id="b2328-106">The data is captured in a single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="b2328-107">Azure Data Factory is a fully managed cloud-based data integration service.</span><span class="sxs-lookup"><span data-stu-id="b2328-107">Azure Data Factory is a fully managed cloud-based data integration service.</span></span> <span data-ttu-id="b2328-108">You can use the service to populate the lake with data from your existing system and save time when building your analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="b2328-108">You can use the service to populate the lake with data from your existing system and save time when building your analytics solutions.</span></span>

<span data-ttu-id="b2328-109">Azure Data Factory offers the following benefits for loading data into Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="b2328-109">Azure Data Factory offers the following benefits for loading data into Azure Data Lake Store:</span></span>

* <span data-ttu-id="b2328-110">**Easy to set up**: An intuitive 5-step wizard with no scripting required.</span><span class="sxs-lookup"><span data-stu-id="b2328-110">**Easy to set up**: An intuitive 5-step wizard with no scripting required.</span></span>
* <span data-ttu-id="b2328-111">**Rich data store support**: Built-in support for a rich set of on-premises and cloud-based data stores.</span><span class="sxs-lookup"><span data-stu-id="b2328-111">**Rich data store support**: Built-in support for a rich set of on-premises and cloud-based data stores.</span></span> <span data-ttu-id="b2328-112">For a detailed list, see the table of [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b2328-112">For a detailed list, see the table of [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
* <span data-ttu-id="b2328-113">**Secure and compliant**: Data is transferred over HTTPS or ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b2328-113">**Secure and compliant**: Data is transferred over HTTPS or ExpressRoute.</span></span> <span data-ttu-id="b2328-114">The global service presence ensures that your data never leaves the geographical boundary.</span><span class="sxs-lookup"><span data-stu-id="b2328-114">The global service presence ensures that your data never leaves the geographical boundary.</span></span>
* <span data-ttu-id="b2328-115">**High performance**: Up to 1-GB/s data loading speed into Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b2328-115">**High performance**: Up to 1-GB/s data loading speed into Azure Data Lake Store.</span></span> <span data-ttu-id="b2328-116">For details, see [Copy activity performance](copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b2328-116">For details, see [Copy activity performance](copy-activity-performance.md).</span></span>

<span data-ttu-id="b2328-117">This article shows you how to use the Data Factory Copy Data tool to _load data from Amazon S3 into Azure Data Lake Store_.</span><span class="sxs-lookup"><span data-stu-id="b2328-117">This article shows you how to use the Data Factory Copy Data tool to _load data from Amazon S3 into Azure Data Lake Store_.</span></span> <span data-ttu-id="b2328-118">You can follow similar steps to copy data from other types of data stores.</span><span class="sxs-lookup"><span data-stu-id="b2328-118">You can follow similar steps to copy data from other types of data stores.</span></span>

> [!NOTE]
> <span data-ttu-id="b2328-119">For more information, see [Copy data to or from Azure Data Lake Store by using Azure Data Factory](connector-azure-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="b2328-119">For more information, see [Copy data to or from Azure Data Lake Store by using Azure Data Factory](connector-azure-data-lake-store.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2328-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b2328-120">Prerequisites</span></span>

* <span data-ttu-id="b2328-121">Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="b2328-121">Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>
* <span data-ttu-id="b2328-122">Azure Data Lake Store: If you don't have a Data Lake Store account, see the instructions in [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#create-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="b2328-122">Azure Data Lake Store: If you don't have a Data Lake Store account, see the instructions in [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#create-an-azure-data-lake-store-account).</span></span>
* <span data-ttu-id="b2328-123">Amazon S3: This article shows how to copy data from Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="b2328-123">Amazon S3: This article shows how to copy data from Amazon S3.</span></span> <span data-ttu-id="b2328-124">You can use other data stores by following similar steps.</span><span class="sxs-lookup"><span data-stu-id="b2328-124">You can use other data stores by following similar steps.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="b2328-125">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="b2328-125">Create a data factory</span></span>

1. <span data-ttu-id="b2328-126">On the left menu, select **New** > **Data + Analytics** > **Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="b2328-126">On the left menu, select **New** > **Data + Analytics** > **Data Factory**:</span></span>
   
   ![Create a new data factory](./media/load-data-into-azure-data-lake-store/new-azure-data-factory-menu.png)
2. <span data-ttu-id="b2328-128">In the **New data factory** page, provide values for the fields that are shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="b2328-128">In the **New data factory** page, provide values for the fields that are shown in the following image:</span></span> 
      
   ![New data factory page](./media/load-data-into-azure-data-lake-store//new-azure-data-factory.png)
 
    * <span data-ttu-id="b2328-130">**Name**: Enter a globally unique name for your Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="b2328-130">**Name**: Enter a globally unique name for your Azure data factory.</span></span> <span data-ttu-id="b2328-131">If you receive the error "Data factory name \"LoadADLSDemo\" is not available," enter a different name for the data factory.</span><span class="sxs-lookup"><span data-stu-id="b2328-131">If you receive the error "Data factory name \"LoadADLSDemo\" is not available," enter a different name for the data factory.</span></span> <span data-ttu-id="b2328-132">For example, you could use the name _**yourname**_**ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="b2328-132">For example, you could use the name _**yourname**_**ADFTutorialDataFactory**.</span></span> <span data-ttu-id="b2328-133">Try creating the data factory again.</span><span class="sxs-lookup"><span data-stu-id="b2328-133">Try creating the data factory again.</span></span> <span data-ttu-id="b2328-134">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="b2328-134">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>
    * <span data-ttu-id="b2328-135">**Subscription**: Select your Azure subscription in which to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="b2328-135">**Subscription**: Select your Azure subscription in which to create the data factory.</span></span> 
    * <span data-ttu-id="b2328-136">**Resource Group**: Select an existing resource group from the drop-down list, or select the **Create new** option and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="b2328-136">**Resource Group**: Select an existing resource group from the drop-down list, or select the **Create new** option and enter the name of a resource group.</span></span> <span data-ttu-id="b2328-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2328-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
    * <span data-ttu-id="b2328-138">**Version**: Select **V2**.</span><span class="sxs-lookup"><span data-stu-id="b2328-138">**Version**: Select **V2**.</span></span>
    * <span data-ttu-id="b2328-139">**Location**: Select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="b2328-139">**Location**: Select the location for the data factory.</span></span> <span data-ttu-id="b2328-140">Only supported locations are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b2328-140">Only supported locations are displayed in the drop-down list.</span></span> <span data-ttu-id="b2328-141">The data stores that are used by data factory can be in other locations and regions.</span><span class="sxs-lookup"><span data-stu-id="b2328-141">The data stores that are used by data factory can be in other locations and regions.</span></span> <span data-ttu-id="b2328-142">These data stores include Azure Data Lake Store, Azure Storage, Azure SQL Database, and so on.</span><span class="sxs-lookup"><span data-stu-id="b2328-142">These data stores include Azure Data Lake Store, Azure Storage, Azure SQL Database, and so on.</span></span>

3. <span data-ttu-id="b2328-143">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2328-143">Select **Create**.</span></span>
4. <span data-ttu-id="b2328-144">After creation is complete, go to your data factory.</span><span class="sxs-lookup"><span data-stu-id="b2328-144">After creation is complete, go to your data factory.</span></span> <span data-ttu-id="b2328-145">You see the **Data Factory** home page as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="b2328-145">You see the **Data Factory** home page as shown in the following image:</span></span> 
   
   ![Data factory home page](./media/load-data-into-azure-data-lake-store/data-factory-home-page.png)

   <span data-ttu-id="b2328-147">Select the **Author & Monitor** tile to launch the Data Integration Application in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="b2328-147">Select the **Author & Monitor** tile to launch the Data Integration Application in a separate tab.</span></span>

## <a name="load-data-into-azure-data-lake-store"></a><span data-ttu-id="b2328-148">Load data into Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b2328-148">Load data into Azure Data Lake Store</span></span>

1. <span data-ttu-id="b2328-149">In the **Get started** page, select the **Copy Data** tile to launch the Copy Data tool:</span><span class="sxs-lookup"><span data-stu-id="b2328-149">In the **Get started** page, select the **Copy Data** tile to launch the Copy Data tool:</span></span> 

   ![Copy Data tool tile](./media/load-data-into-azure-data-lake-store/copy-data-tool-tile.png)
2. <span data-ttu-id="b2328-151">In the **Properties** page, specify **CopyFromAmazonS3ToADLS** for the **Task name** field, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="b2328-151">In the **Properties** page, specify **CopyFromAmazonS3ToADLS** for the **Task name** field, and select **Next**:</span></span>

    ![Properties page](./media/load-data-into-azure-data-lake-store/copy-data-tool-properties-page.png)
3. <span data-ttu-id="b2328-153">In the **Source data store** page, click **+ Create new connection**:</span><span class="sxs-lookup"><span data-stu-id="b2328-153">In the **Source data store** page, click **+ Create new connection**:</span></span>

    ![Source data store page](./media/load-data-into-azure-data-lake-store/source-data-store-page.png)
    
    <span data-ttu-id="b2328-155">Select **Amazon S3**, and select **Continue**</span><span class="sxs-lookup"><span data-stu-id="b2328-155">Select **Amazon S3**, and select **Continue**</span></span>
    
    ![Source data store s3 page](./media/load-data-into-azure-data-lake-store/source-data-store-page-s3.png)
    
4. <span data-ttu-id="b2328-157">In the **Specify Amazon S3 connection** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b2328-157">In the **Specify Amazon S3 connection** page, do the following steps:</span></span> 
   1. <span data-ttu-id="b2328-158">Specify the **Access Key ID** value.</span><span class="sxs-lookup"><span data-stu-id="b2328-158">Specify the **Access Key ID** value.</span></span>
   2. <span data-ttu-id="b2328-159">Specify the **Secret Access Key** value.</span><span class="sxs-lookup"><span data-stu-id="b2328-159">Specify the **Secret Access Key** value.</span></span>
   3. <span data-ttu-id="b2328-160">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b2328-160">Select **Finish**.</span></span>
   
   ![Specify Amazon S3 account](./media/load-data-into-azure-data-lake-store/specify-amazon-s3-account.png)
   
   4. <span data-ttu-id="b2328-162">You will see a new connection.</span><span class="sxs-lookup"><span data-stu-id="b2328-162">You will see a new connection.</span></span> <span data-ttu-id="b2328-163">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b2328-163">Select **Next**.</span></span>
   
   ![Specify Amazon S3 account](./media/load-data-into-azure-data-lake-store/specify-amazon-s3-account-created.png)
   
5. <span data-ttu-id="b2328-165">In the **Choose the input file or folder** page, browse to the folder and file that you want to copy over.</span><span class="sxs-lookup"><span data-stu-id="b2328-165">In the **Choose the input file or folder** page, browse to the folder and file that you want to copy over.</span></span> <span data-ttu-id="b2328-166">Select the folder/file, select **Choose**, and then select **Next**:</span><span class="sxs-lookup"><span data-stu-id="b2328-166">Select the folder/file, select **Choose**, and then select **Next**:</span></span>

    ![Choose input file or folder](./media/load-data-into-azure-data-lake-store/choose-input-folder.png)

6. <span data-ttu-id="b2328-168">Choose the copy behavior by selecting the **Copy files recursively** and **Binary copy** (copy files as-is) options.</span><span class="sxs-lookup"><span data-stu-id="b2328-168">Choose the copy behavior by selecting the **Copy files recursively** and **Binary copy** (copy files as-is) options.</span></span> <span data-ttu-id="b2328-169">Select **Next**:</span><span class="sxs-lookup"><span data-stu-id="b2328-169">Select **Next**:</span></span>

    ![Specify output folder](./media/load-data-into-azure-data-lake-store/specify-binary-copy.png)
    
7. <span data-ttu-id="b2328-171">In the **Destination data store** page, click **+ Create new connection**, and then select **Azure Data Lake Store**, and select **Continue**:</span><span class="sxs-lookup"><span data-stu-id="b2328-171">In the **Destination data store** page, click **+ Create new connection**, and then select **Azure Data Lake Store**, and select **Continue**:</span></span>

    ![Destination data store page](./media/load-data-into-azure-data-lake-store/destination-data-storage-page.png)

8. <span data-ttu-id="b2328-173">In the **Specify Data Lake Store connection** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b2328-173">In the **Specify Data Lake Store connection** page, do the following steps:</span></span> 

   1. <span data-ttu-id="b2328-174">Select your Data Lake Store for the **Data Lake Store account name**.</span><span class="sxs-lookup"><span data-stu-id="b2328-174">Select your Data Lake Store for the **Data Lake Store account name**.</span></span>
   2. <span data-ttu-id="b2328-175">Specify the **Tenant**, and select Finish.</span><span class="sxs-lookup"><span data-stu-id="b2328-175">Specify the **Tenant**, and select Finish.</span></span>
   3. <span data-ttu-id="b2328-176">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b2328-176">Select **Next**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b2328-177">In this walkthrough, you use a _managed service identity_ to authenticate your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b2328-177">In this walkthrough, you use a _managed service identity_ to authenticate your Data Lake Store.</span></span> <span data-ttu-id="b2328-178">Be sure to grant the MSI the proper permissions in Azure Data Lake Store by following [these instructions](connector-azure-data-lake-store.md#using-managed-service-identity-authentication).</span><span class="sxs-lookup"><span data-stu-id="b2328-178">Be sure to grant the MSI the proper permissions in Azure Data Lake Store by following [these instructions](connector-azure-data-lake-store.md#using-managed-service-identity-authentication).</span></span>
   
   ![Specify Azure Data Lake Store account](./media/load-data-into-azure-data-lake-store/specify-adls.png)
9. <span data-ttu-id="b2328-180">In the **Choose the output file or folder** page, enter **copyfroms3** as the output folder name, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="b2328-180">In the **Choose the output file or folder** page, enter **copyfroms3** as the output folder name, and select **Next**:</span></span> 

    ![Specify output folder](./media/load-data-into-azure-data-lake-store/specify-adls-path.png)

10. <span data-ttu-id="b2328-182">In the **Settings** page, select **Next**:</span><span class="sxs-lookup"><span data-stu-id="b2328-182">In the **Settings** page, select **Next**:</span></span>

    ![Settings page](./media/load-data-into-azure-data-lake-store/copy-settings.png)
11. <span data-ttu-id="b2328-184">In the **Summary** page, review the settings, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="b2328-184">In the **Summary** page, review the settings, and select **Next**:</span></span>

    ![Summary page](./media/load-data-into-azure-data-lake-store/copy-summary.png)
12. <span data-ttu-id="b2328-186">In the **Deployment page**, select **Monitor** to monitor the pipeline (task):</span><span class="sxs-lookup"><span data-stu-id="b2328-186">In the **Deployment page**, select **Monitor** to monitor the pipeline (task):</span></span>

    ![Deployment page](./media/load-data-into-azure-data-lake-store/deployment-page.png)
13. <span data-ttu-id="b2328-188">Notice that the **Monitor** tab on the left is automatically selected.</span><span class="sxs-lookup"><span data-stu-id="b2328-188">Notice that the **Monitor** tab on the left is automatically selected.</span></span> <span data-ttu-id="b2328-189">The **Actions** column includes links to view activity run details and to rerun the pipeline:</span><span class="sxs-lookup"><span data-stu-id="b2328-189">The **Actions** column includes links to view activity run details and to rerun the pipeline:</span></span>

    ![Monitor pipeline runs](./media/load-data-into-azure-data-lake-store/monitor-pipeline-runs.png)
14. <span data-ttu-id="b2328-191">To view activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="b2328-191">To view activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="b2328-192">There's only one activity (copy activity) in the pipeline, so you see only one entry.</span><span class="sxs-lookup"><span data-stu-id="b2328-192">There's only one activity (copy activity) in the pipeline, so you see only one entry.</span></span> <span data-ttu-id="b2328-193">To switch back to the pipeline runs view, select the **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="b2328-193">To switch back to the pipeline runs view, select the **Pipelines** link at the top.</span></span> <span data-ttu-id="b2328-194">Select **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="b2328-194">Select **Refresh** to refresh the list.</span></span> 

    ![Monitor activity runs](./media/load-data-into-azure-data-lake-store/monitor-activity-runs.png)

15. <span data-ttu-id="b2328-196">To monitor the execution details for each copy activity, select the **Details** link under **Actions** in the activity monitoring view.</span><span class="sxs-lookup"><span data-stu-id="b2328-196">To monitor the execution details for each copy activity, select the **Details** link under **Actions** in the activity monitoring view.</span></span> <span data-ttu-id="b2328-197">You can monitor details like the volume of data copied from the source to the sink, data throughput, execution steps with corresponding duration, and used configurations:</span><span class="sxs-lookup"><span data-stu-id="b2328-197">You can monitor details like the volume of data copied from the source to the sink, data throughput, execution steps with corresponding duration, and used configurations:</span></span>

    ![Monitor activity run details](./media/load-data-into-azure-data-lake-store/monitor-activity-run-details.png)

16. <span data-ttu-id="b2328-199">Verify that the data is copied into your Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="b2328-199">Verify that the data is copied into your Azure Data Lake Store:</span></span> 

    ![Verify Data Lake Store output](./media/load-data-into-azure-data-lake-store/adls-copy-result.png)

## <a name="next-steps"></a><span data-ttu-id="b2328-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2328-201">Next steps</span></span>

<span data-ttu-id="b2328-202">Advance to the following article to learn about Azure Data Lake Store support:</span><span class="sxs-lookup"><span data-stu-id="b2328-202">Advance to the following article to learn about Azure Data Lake Store support:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="b2328-203">Azure Data Lake Store connector</span><span class="sxs-lookup"><span data-stu-id="b2328-203">Azure Data Lake Store connector</span></span>](connector-azure-data-lake-store.md)
