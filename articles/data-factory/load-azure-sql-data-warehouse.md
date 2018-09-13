---
title: Load data into Azure SQL Data Warehouse by using Azure Data Factory | Microsoft Docs
description: Use Azure Data Factory to copy data into Azure SQL Data Warehouse
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: jingwang
ms.openlocfilehash: 8525dd443e80bb7d67bc48cc007ab1632ee3e611
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856835"
---
# <a name="load-data-into-azure-sql-data-warehouse-by-using-azure-data-factory"></a><span data-ttu-id="8cafe-103">Load data into Azure SQL Data Warehouse by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8cafe-103">Load data into Azure SQL Data Warehouse by using Azure Data Factory</span></span>

<span data-ttu-id="8cafe-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database that's capable of processing massive volumes of data, both relational and non-relational.</span><span class="sxs-lookup"><span data-stu-id="8cafe-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database that's capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="8cafe-105">SQL Data Warehouse is built on the massively parallel processing (MPP) architecture that's optimized for enterprise data warehouse workloads.</span><span class="sxs-lookup"><span data-stu-id="8cafe-105">SQL Data Warehouse is built on the massively parallel processing (MPP) architecture that's optimized for enterprise data warehouse workloads.</span></span> <span data-ttu-id="8cafe-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span><span class="sxs-lookup"><span data-stu-id="8cafe-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="8cafe-107">Getting started with Azure SQL Data Warehouse is now easier than ever when you use Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8cafe-107">Getting started with Azure SQL Data Warehouse is now easier than ever when you use Azure Data Factory.</span></span> <span data-ttu-id="8cafe-108">Azure Data Factory is a fully managed cloud-based data integration service.</span><span class="sxs-lookup"><span data-stu-id="8cafe-108">Azure Data Factory is a fully managed cloud-based data integration service.</span></span> <span data-ttu-id="8cafe-109">You can use the service to populate a SQL Data Warehouse with data from your existing system and save time when building your analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="8cafe-109">You can use the service to populate a SQL Data Warehouse with data from your existing system and save time when building your analytics solutions.</span></span>

<span data-ttu-id="8cafe-110">Azure Data Factory offers the following benefits for loading data into Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="8cafe-110">Azure Data Factory offers the following benefits for loading data into Azure SQL Data Warehouse:</span></span>

* <span data-ttu-id="8cafe-111">**Easy to set up**: An intuitive 5-step wizard with no scripting required.</span><span class="sxs-lookup"><span data-stu-id="8cafe-111">**Easy to set up**: An intuitive 5-step wizard with no scripting required.</span></span>
* <span data-ttu-id="8cafe-112">**Rich data store support**: Built-in support for a rich set of on-premises and cloud-based data stores.</span><span class="sxs-lookup"><span data-stu-id="8cafe-112">**Rich data store support**: Built-in support for a rich set of on-premises and cloud-based data stores.</span></span> <span data-ttu-id="8cafe-113">For a detailed list, see the table of [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8cafe-113">For a detailed list, see the table of [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
* <span data-ttu-id="8cafe-114">**Secure and compliant**: Data is transferred over HTTPS or ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cafe-114">**Secure and compliant**: Data is transferred over HTTPS or ExpressRoute.</span></span> <span data-ttu-id="8cafe-115">The global service presence ensures that your data never leaves the geographical boundary.</span><span class="sxs-lookup"><span data-stu-id="8cafe-115">The global service presence ensures that your data never leaves the geographical boundary.</span></span>
* <span data-ttu-id="8cafe-116">**Unparalleled performance by using PolyBase**: Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8cafe-116">**Unparalleled performance by using PolyBase**: Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8cafe-117">Use the staging blob feature to achieve high load speeds from all types of data stores, including Azure Blob storage and Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8cafe-117">Use the staging blob feature to achieve high load speeds from all types of data stores, including Azure Blob storage and Data Lake Store.</span></span> <span data-ttu-id="8cafe-118">(Polybase supports Azure Blob storage and Azure Data Lake Store by default.) For details, see [Copy activity performance](copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-118">(Polybase supports Azure Blob storage and Azure Data Lake Store by default.) For details, see [Copy activity performance](copy-activity-performance.md).</span></span>

<span data-ttu-id="8cafe-119">This article shows you how to use the Data Factory Copy Data tool to _load data from Azure SQL Database into Azure SQL Data Warehouse_.</span><span class="sxs-lookup"><span data-stu-id="8cafe-119">This article shows you how to use the Data Factory Copy Data tool to _load data from Azure SQL Database into Azure SQL Data Warehouse_.</span></span> <span data-ttu-id="8cafe-120">You can follow similar steps to copy data from other types of data stores.</span><span class="sxs-lookup"><span data-stu-id="8cafe-120">You can follow similar steps to copy data from other types of data stores.</span></span>

> [!NOTE]
> <span data-ttu-id="8cafe-121">For more information, see [Copy data to or from Azure SQL Data Warehouse by using Azure Data Factory](connector-azure-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-121">For more information, see [Copy data to or from Azure SQL Data Warehouse by using Azure Data Factory](connector-azure-sql-data-warehouse.md).</span></span>
## <a name="prerequisites"></a><span data-ttu-id="8cafe-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8cafe-122">Prerequisites</span></span>

* <span data-ttu-id="8cafe-123">Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="8cafe-123">Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>
* <span data-ttu-id="8cafe-124">Azure SQL Data Warehouse: The data warehouse holds the data that's copied over from the SQL database.</span><span class="sxs-lookup"><span data-stu-id="8cafe-124">Azure SQL Data Warehouse: The data warehouse holds the data that's copied over from the SQL database.</span></span> <span data-ttu-id="8cafe-125">If you don't have an Azure SQL Data Warehouse, see the instructions in [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-125">If you don't have an Azure SQL Data Warehouse, see the instructions in [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md).</span></span>
* <span data-ttu-id="8cafe-126">Azure SQL Database: This tutorial copies data from an Azure SQL database with Adventure Works LT sample data.</span><span class="sxs-lookup"><span data-stu-id="8cafe-126">Azure SQL Database: This tutorial copies data from an Azure SQL database with Adventure Works LT sample data.</span></span> <span data-ttu-id="8cafe-127">You can create a SQL database by following the instructions in [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-127">You can create a SQL database by following the instructions in [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md).</span></span> 
* <span data-ttu-id="8cafe-128">Azure storage account: Azure Storage is used as the _staging_ blob in the bulk copy operation.</span><span class="sxs-lookup"><span data-stu-id="8cafe-128">Azure storage account: Azure Storage is used as the _staging_ blob in the bulk copy operation.</span></span> <span data-ttu-id="8cafe-129">If you don't have an Azure storage account, see the instructions in [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-129">If you don't have an Azure storage account, see the instructions in [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="8cafe-130">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="8cafe-130">Create a data factory</span></span>

1. <span data-ttu-id="8cafe-131">On the left menu, select **New** > **Data + Analytics** > **Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="8cafe-131">On the left menu, select **New** > **Data + Analytics** > **Data Factory**:</span></span> 
   
   ![Create a new data factory](./media/load-azure-sql-data-warehouse/new-azure-data-factory-menu.png)
1. <span data-ttu-id="8cafe-133">In the **New data factory** page, provide values for the fields that are shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="8cafe-133">In the **New data factory** page, provide values for the fields that are shown in the following image:</span></span>
      
   ![New data factory page](./media/load-azure-sql-data-warehouse/new-azure-data-factory.png)
 
    * <span data-ttu-id="8cafe-135">**Name**: Enter a globally unique name for your Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="8cafe-135">**Name**: Enter a globally unique name for your Azure data factory.</span></span> <span data-ttu-id="8cafe-136">If you receive the error "Data factory name \"LoadSQLDWDemo\" is not available," enter a different name for the data factory.</span><span class="sxs-lookup"><span data-stu-id="8cafe-136">If you receive the error "Data factory name \"LoadSQLDWDemo\" is not available," enter a different name for the data factory.</span></span> <span data-ttu-id="8cafe-137">For example, you could use the name _**yourname**_**ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-137">For example, you could use the name _**yourname**_**ADFTutorialDataFactory**.</span></span> <span data-ttu-id="8cafe-138">Try creating the data factory again.</span><span class="sxs-lookup"><span data-stu-id="8cafe-138">Try creating the data factory again.</span></span> <span data-ttu-id="8cafe-139">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-139">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>
    * <span data-ttu-id="8cafe-140">**Subscription**: Select your Azure subscription in which to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="8cafe-140">**Subscription**: Select your Azure subscription in which to create the data factory.</span></span> 
    * <span data-ttu-id="8cafe-141">**Resource Group**: Select an existing resource group from the drop-down list, or select the **Create new** option and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="8cafe-141">**Resource Group**: Select an existing resource group from the drop-down list, or select the **Create new** option and enter the name of a resource group.</span></span> <span data-ttu-id="8cafe-142">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8cafe-142">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
    * <span data-ttu-id="8cafe-143">**Version**: Select **V2**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-143">**Version**: Select **V2**.</span></span>
    * <span data-ttu-id="8cafe-144">**Location**: Select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="8cafe-144">**Location**: Select the location for the data factory.</span></span> <span data-ttu-id="8cafe-145">Only supported locations are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="8cafe-145">Only supported locations are displayed in the drop-down list.</span></span> <span data-ttu-id="8cafe-146">The data stores that are used by data factory can be in other locations and regions.</span><span class="sxs-lookup"><span data-stu-id="8cafe-146">The data stores that are used by data factory can be in other locations and regions.</span></span> <span data-ttu-id="8cafe-147">These data stores include Azure Data Lake Store, Azure Storage, Azure SQL Database, and so on.</span><span class="sxs-lookup"><span data-stu-id="8cafe-147">These data stores include Azure Data Lake Store, Azure Storage, Azure SQL Database, and so on.</span></span>

1. <span data-ttu-id="8cafe-148">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-148">Select **Create**.</span></span>
1. <span data-ttu-id="8cafe-149">After creation is complete, go to your data factory.</span><span class="sxs-lookup"><span data-stu-id="8cafe-149">After creation is complete, go to your data factory.</span></span> <span data-ttu-id="8cafe-150">You see the **Data Factory** home page as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="8cafe-150">You see the **Data Factory** home page as shown in the following image:</span></span>
   
   ![Data factory home page](./media/load-azure-sql-data-warehouse/data-factory-home-page.png)

   <span data-ttu-id="8cafe-152">Select the **Author & Monitor** tile to launch the Data Integration Application in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="8cafe-152">Select the **Author & Monitor** tile to launch the Data Integration Application in a separate tab.</span></span>

## <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="8cafe-153">Load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8cafe-153">Load data into Azure SQL Data Warehouse</span></span>

1. <span data-ttu-id="8cafe-154">In the **Get started** page, select the **Copy Data** tile to launch the Copy Data tool:</span><span class="sxs-lookup"><span data-stu-id="8cafe-154">In the **Get started** page, select the **Copy Data** tile to launch the Copy Data tool:</span></span>

   ![Copy Data tool tile](./media/load-azure-sql-data-warehouse/copy-data-tool-tile.png)
1. <span data-ttu-id="8cafe-156">In the **Properties** page, specify **CopyFromSQLToSQLDW** for the **Task name** field, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="8cafe-156">In the **Properties** page, specify **CopyFromSQLToSQLDW** for the **Task name** field, and select **Next**:</span></span>

    ![Properties page](./media/load-azure-sql-data-warehouse/copy-data-tool-properties-page.png)

1. <span data-ttu-id="8cafe-158">In the **Source data store** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8cafe-158">In the **Source data store** page, complete the following steps:</span></span>

    <span data-ttu-id="8cafe-159">a.</span><span class="sxs-lookup"><span data-stu-id="8cafe-159">a.</span></span> <span data-ttu-id="8cafe-160">click **+ Create new connection**:</span><span class="sxs-lookup"><span data-stu-id="8cafe-160">click **+ Create new connection**:</span></span>

    ![Source data store page](./media/load-azure-sql-data-warehouse/new-source-linked-service.png)

    <span data-ttu-id="8cafe-162">b.</span><span class="sxs-lookup"><span data-stu-id="8cafe-162">b.</span></span> <span data-ttu-id="8cafe-163">Select **Azure SQL Database** from the gallery, and select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-163">Select **Azure SQL Database** from the gallery, and select **Continue**.</span></span> <span data-ttu-id="8cafe-164">You can type "SQL" in the search box to filter the connectors.</span><span class="sxs-lookup"><span data-stu-id="8cafe-164">You can type "SQL" in the search box to filter the connectors.</span></span>

    ![Select Azure SQL DB](./media/load-azure-sql-data-warehouse/select-azure-sql-db-source.png)

    <span data-ttu-id="8cafe-166">c.</span><span class="sxs-lookup"><span data-stu-id="8cafe-166">c.</span></span> <span data-ttu-id="8cafe-167">In the **New Linked Service** page, select your server name and DB name from the dropdown list, and specify the username and passworkd.</span><span class="sxs-lookup"><span data-stu-id="8cafe-167">In the **New Linked Service** page, select your server name and DB name from the dropdown list, and specify the username and passworkd.</span></span> <span data-ttu-id="8cafe-168">Click **Test connection** to validate the settings, then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-168">Click **Test connection** to validate the settings, then select **Finish**.</span></span>
   
    ![Configure Azure SQL DB](./media/load-azure-sql-data-warehouse/configure-azure-sql-db.png)

    <span data-ttu-id="8cafe-170">d.</span><span class="sxs-lookup"><span data-stu-id="8cafe-170">d.</span></span> <span data-ttu-id="8cafe-171">Select the newly created linked service as source, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-171">Select the newly created linked service as source, then click **Next**.</span></span>

    ![Select source linked service](./media/load-azure-sql-data-warehouse/select-source-linked-service.png)

1. <span data-ttu-id="8cafe-173">In the **Select tables from which to copy the data or use a custom query** page, enter **SalesLT** to filter the tables.</span><span class="sxs-lookup"><span data-stu-id="8cafe-173">In the **Select tables from which to copy the data or use a custom query** page, enter **SalesLT** to filter the tables.</span></span> <span data-ttu-id="8cafe-174">Choose the **(Select all)** box to use all of the tables for the copy, and then select **Next**:</span><span class="sxs-lookup"><span data-stu-id="8cafe-174">Choose the **(Select all)** box to use all of the tables for the copy, and then select **Next**:</span></span> 

    ![Select source tables](./media/load-azure-sql-data-warehouse/select-source-tables.png)

1. <span data-ttu-id="8cafe-176">In the **Destination data store** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8cafe-176">In the **Destination data store** page, complete the following steps:</span></span>

    <span data-ttu-id="8cafe-177">a.</span><span class="sxs-lookup"><span data-stu-id="8cafe-177">a.</span></span> <span data-ttu-id="8cafe-178">Click **+ Create new connection** to add a connection</span><span class="sxs-lookup"><span data-stu-id="8cafe-178">Click **+ Create new connection** to add a connection</span></span>

    ![Sink data store page](./media/load-azure-sql-data-warehouse/new-sink-linked-service.png)

    <span data-ttu-id="8cafe-180">b.</span><span class="sxs-lookup"><span data-stu-id="8cafe-180">b.</span></span> <span data-ttu-id="8cafe-181">Select **Azure SQL Data Warehouse** from the gallery, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-181">Select **Azure SQL Data Warehouse** from the gallery, and select **Next**.</span></span>

    ![Select Azure SQL DW](./media/load-azure-sql-data-warehouse/select-azure-sql-dw-sink.png)

    <span data-ttu-id="8cafe-183">c.</span><span class="sxs-lookup"><span data-stu-id="8cafe-183">c.</span></span> <span data-ttu-id="8cafe-184">In the **New Linked Service** page, select your server name and DB name from the dropdown list, and specify the username and passworkd.</span><span class="sxs-lookup"><span data-stu-id="8cafe-184">In the **New Linked Service** page, select your server name and DB name from the dropdown list, and specify the username and passworkd.</span></span> <span data-ttu-id="8cafe-185">Click **Test connection** to validate the settings, then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-185">Click **Test connection** to validate the settings, then select **Finish**.</span></span>
   
    ![Configure Azure SQL DW](./media/load-azure-sql-data-warehouse/configure-azure-sql-dw.png)

    <span data-ttu-id="8cafe-187">d.</span><span class="sxs-lookup"><span data-stu-id="8cafe-187">d.</span></span> <span data-ttu-id="8cafe-188">Select the newly created linked service as sink, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-188">Select the newly created linked service as sink, then click **Next**.</span></span>

    ![Select sink linked service](./media/load-azure-sql-data-warehouse/select-sink-linked-service.png)

1. <span data-ttu-id="8cafe-190">In the **Table mapping** page, review the content, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-190">In the **Table mapping** page, review the content, and select **Next**.</span></span> <span data-ttu-id="8cafe-191">An intelligent table mapping displays.</span><span class="sxs-lookup"><span data-stu-id="8cafe-191">An intelligent table mapping displays.</span></span> <span data-ttu-id="8cafe-192">The source tables are mapped to the destination tables based on the table names.</span><span class="sxs-lookup"><span data-stu-id="8cafe-192">The source tables are mapped to the destination tables based on the table names.</span></span> <span data-ttu-id="8cafe-193">If a source table doesn't exist in the destination, Azure Data Factory creates a destination table with the same name by default.</span><span class="sxs-lookup"><span data-stu-id="8cafe-193">If a source table doesn't exist in the destination, Azure Data Factory creates a destination table with the same name by default.</span></span> <span data-ttu-id="8cafe-194">You can also map a source table to an existing destination table.</span><span class="sxs-lookup"><span data-stu-id="8cafe-194">You can also map a source table to an existing destination table.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="8cafe-195">Automatic table creation for the SQL Data Warehouse sink applies when SQL Server or Azure SQL Database is the source.</span><span class="sxs-lookup"><span data-stu-id="8cafe-195">Automatic table creation for the SQL Data Warehouse sink applies when SQL Server or Azure SQL Database is the source.</span></span> <span data-ttu-id="8cafe-196">If you copy data from another source data store, you need to pre-create the schema in the sink Azure SQL Data Warehouse before executing the data copy.</span><span class="sxs-lookup"><span data-stu-id="8cafe-196">If you copy data from another source data store, you need to pre-create the schema in the sink Azure SQL Data Warehouse before executing the data copy.</span></span>

   ![Table mapping page](./media/load-azure-sql-data-warehouse/table-mapping.png)

1. <span data-ttu-id="8cafe-198">In the **Schema mapping** page, review the content, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-198">In the **Schema mapping** page, review the content, and select **Next**.</span></span> <span data-ttu-id="8cafe-199">The intelligent table mapping is based on the column name.</span><span class="sxs-lookup"><span data-stu-id="8cafe-199">The intelligent table mapping is based on the column name.</span></span> <span data-ttu-id="8cafe-200">If you let Data Factory automatically create the tables, data type conversion can occur when there are incompatibilities between the source and destination stores.</span><span class="sxs-lookup"><span data-stu-id="8cafe-200">If you let Data Factory automatically create the tables, data type conversion can occur when there are incompatibilities between the source and destination stores.</span></span> <span data-ttu-id="8cafe-201">If there's an unsupported data type conversion between the source and destination column, you see an error message next to the corresponding table.</span><span class="sxs-lookup"><span data-stu-id="8cafe-201">If there's an unsupported data type conversion between the source and destination column, you see an error message next to the corresponding table.</span></span>

    ![Schema mapping page](./media/load-azure-sql-data-warehouse/schema-mapping.png)

1. <span data-ttu-id="8cafe-203">In the **Settings** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8cafe-203">In the **Settings** page, complete the following steps:</span></span>

    <span data-ttu-id="8cafe-204">a.</span><span class="sxs-lookup"><span data-stu-id="8cafe-204">a.</span></span> <span data-ttu-id="8cafe-205">In **Staging settings** section, click **+ New** to new a staging storage.</span><span class="sxs-lookup"><span data-stu-id="8cafe-205">In **Staging settings** section, click **+ New** to new a staging storage.</span></span> <span data-ttu-id="8cafe-206">The storage is used for staging the data before it loads into SQL Data Warehouse by using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="8cafe-206">The storage is used for staging the data before it loads into SQL Data Warehouse by using PolyBase.</span></span> <span data-ttu-id="8cafe-207">After the copy is complete, the interim data in Azure Storage is automatically cleaned up.</span><span class="sxs-lookup"><span data-stu-id="8cafe-207">After the copy is complete, the interim data in Azure Storage is automatically cleaned up.</span></span> 

    ![Configure staging](./media/load-azure-sql-data-warehouse/configure-staging.png)

    <span data-ttu-id="8cafe-209">b.</span><span class="sxs-lookup"><span data-stu-id="8cafe-209">b.</span></span> <span data-ttu-id="8cafe-210">In the **New Linked Service** page, select your storage account, and select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-210">In the **New Linked Service** page, select your storage account, and select **Finish**.</span></span>
   
    ![Configure Azure Storage](./media/load-azure-sql-data-warehouse/configure-blob-storage.png)

    <span data-ttu-id="8cafe-212">c.</span><span class="sxs-lookup"><span data-stu-id="8cafe-212">c.</span></span> <span data-ttu-id="8cafe-213">In the **Advanced settings** section, deselect the **Use type default** option, then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="8cafe-213">In the **Advanced settings** section, deselect the **Use type default** option, then select **Next**.</span></span>

    ![Configure PolyBase](./media/load-azure-sql-data-warehouse/configure-polybase.png)

1. <span data-ttu-id="8cafe-215">In the **Summary** page, review the settings, and select **Next**:</span><span class="sxs-lookup"><span data-stu-id="8cafe-215">In the **Summary** page, review the settings, and select **Next**:</span></span>

    ![Summary page](./media/load-azure-sql-data-warehouse/summary-page.png)
1. <span data-ttu-id="8cafe-217">In the **Deployment page**, select **Monitor** to monitor the pipeline (task):</span><span class="sxs-lookup"><span data-stu-id="8cafe-217">In the **Deployment page**, select **Monitor** to monitor the pipeline (task):</span></span>

    ![Deployment page](./media/load-azure-sql-data-warehouse/deployment-page.png)
1. <span data-ttu-id="8cafe-219">Notice that the **Monitor** tab on the left is automatically selected.</span><span class="sxs-lookup"><span data-stu-id="8cafe-219">Notice that the **Monitor** tab on the left is automatically selected.</span></span> <span data-ttu-id="8cafe-220">The **Actions** column includes links to view activity run details and to rerun the pipeline:</span><span class="sxs-lookup"><span data-stu-id="8cafe-220">The **Actions** column includes links to view activity run details and to rerun the pipeline:</span></span> 

    ![Monitor pipeline runs](./media/load-azure-sql-data-warehouse/pipeline-monitoring.png)
1. <span data-ttu-id="8cafe-222">To view activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="8cafe-222">To view activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="8cafe-223">To switch back to the pipeline runs view, select the **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="8cafe-223">To switch back to the pipeline runs view, select the **Pipelines** link at the top.</span></span> <span data-ttu-id="8cafe-224">Select **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="8cafe-224">Select **Refresh** to refresh the list.</span></span> 

    ![Monitor activity runs](./media/load-azure-sql-data-warehouse/activity-monitoring.png)

1. <span data-ttu-id="8cafe-226">To monitor the execution details for each copy activity, select the **Details** link under **Actions** in the activity monitoring view.</span><span class="sxs-lookup"><span data-stu-id="8cafe-226">To monitor the execution details for each copy activity, select the **Details** link under **Actions** in the activity monitoring view.</span></span> <span data-ttu-id="8cafe-227">You can monitor details like the volume of data copied from the source to the sink, data throughput, execution steps with corresponding duration, and used configurations:</span><span class="sxs-lookup"><span data-stu-id="8cafe-227">You can monitor details like the volume of data copied from the source to the sink, data throughput, execution steps with corresponding duration, and used configurations:</span></span>

    ![Monitor activity run details](./media/load-azure-sql-data-warehouse/monitor-activity-run-details.png)

## <a name="next-steps"></a><span data-ttu-id="8cafe-229">Next steps</span><span class="sxs-lookup"><span data-stu-id="8cafe-229">Next steps</span></span>

<span data-ttu-id="8cafe-230">Advance to the following article to learn about Azure SQL Data Warehouse support:</span><span class="sxs-lookup"><span data-stu-id="8cafe-230">Advance to the following article to learn about Azure SQL Data Warehouse support:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="8cafe-231">Azure SQL Data Warehouse connector</span><span class="sxs-lookup"><span data-stu-id="8cafe-231">Azure SQL Data Warehouse connector</span></span>](connector-azure-sql-data-warehouse.md)
