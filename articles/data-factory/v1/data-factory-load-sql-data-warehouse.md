---
title: Load terabytes of data into SQL Data Warehouse | Microsoft Docs
description: Demonstrates how 1 TB of data can be loaded into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 5fb4034d49982d600fe5b0de17d0b198e3ee653e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865769"
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="6a7c3-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span><span class="sxs-lookup"><span data-stu-id="6a7c3-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
> [!NOTE]
> <span data-ttu-id="6a7c3-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="6a7c3-105">If you are using the current version of the Data Factory service, see [Copy data to or from Azure SQL Data Warehouse by using Data Factory](../connector-azure-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="6a7c3-105">If you are using the current version of the Data Factory service, see [Copy data to or from Azure SQL Data Warehouse by using Data Factory](../connector-azure-sql-data-warehouse.md).</span></span>


<span data-ttu-id="6a7c3-106">[Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-106">[Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="6a7c3-107">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-107">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="6a7c3-108">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-108">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="6a7c3-109">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-109">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="6a7c3-110">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-110">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="6a7c3-111">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-111">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="6a7c3-112">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-112">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="6a7c3-113">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-113">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="6a7c3-114">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span><span class="sxs-lookup"><span data-stu-id="6a7c3-114">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="6a7c3-115">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-115">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="6a7c3-116">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-116">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="6a7c3-117">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-117">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="6a7c3-118">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-118">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="6a7c3-119">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-119">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="6a7c3-120">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-120">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="6a7c3-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a7c3-121">Prerequisites</span></span>
* <span data-ttu-id="6a7c3-122">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-122">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="6a7c3-123">If you do not have an Azure storage account, learn [how to create a storage account](../../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6a7c3-123">If you do not have an Azure storage account, learn [how to create a storage account](../../storage/common/storage-quickstart-create-account.md).</span></span>
* <span data-ttu-id="6a7c3-124">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-124">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="6a7c3-125">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-125">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="6a7c3-126">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="6a7c3-126">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="6a7c3-127">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-127">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="6a7c3-128">…</span><span class="sxs-lookup"><span data-stu-id="6a7c3-128">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="6a7c3-129">Now copy the generated files to Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-129">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="6a7c3-130">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-130">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="6a7c3-131">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span><span class="sxs-lookup"><span data-stu-id="6a7c3-131">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="6a7c3-132">Refer to [Create an Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-132">Refer to [Create an Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="6a7c3-133">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-133">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6a7c3-134">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-134">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="6a7c3-135">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span><span class="sxs-lookup"><span data-stu-id="6a7c3-135">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="6a7c3-136">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-136">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Performance slider](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="6a7c3-138">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-138">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="6a7c3-139">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-139">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Scale button](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="6a7c3-141">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-141">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Scale dialog](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="6a7c3-143">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-143">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="6a7c3-144">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-144">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="6a7c3-145">Learn how to do that by following [Change a user resource class example](../../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="6a7c3-145">Learn how to do that by following [Change a user resource class example](../../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md).</span></span>  
* <span data-ttu-id="6a7c3-146">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-146">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="6a7c3-147">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-147">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="6a7c3-148">Launch Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="6a7c3-148">Launch Copy Wizard</span></span>
1. <span data-ttu-id="6a7c3-149">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a7c3-149">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6a7c3-150">Click **Create a resource** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-150">Click **Create a resource** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="6a7c3-151">In the **New data factory** pane:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-151">In the **New data factory** pane:</span></span>

   1. <span data-ttu-id="6a7c3-152">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-152">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="6a7c3-153">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-153">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="6a7c3-154">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-154">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="6a7c3-155">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-155">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="6a7c3-156">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-156">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="6a7c3-157">For Resource Group, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-157">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="6a7c3-158">Select **Use existing** to select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-158">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="6a7c3-159">Select **Create new** to enter a name for a resource group.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-159">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="6a7c3-160">Select a **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-160">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="6a7c3-161">Select **Pin to dashboard** check box at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-161">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="6a7c3-162">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-162">Click **Create**.</span></span>
4. <span data-ttu-id="6a7c3-163">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-163">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Data factory home page](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="6a7c3-165">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-165">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6a7c3-166">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-166">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="6a7c3-167">Step 1: Configure data loading schedule</span><span class="sxs-lookup"><span data-stu-id="6a7c3-167">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="6a7c3-168">The first step is to configure the data loading schedule.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-168">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="6a7c3-169">In the **Properties** page:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-169">In the **Properties** page:</span></span>

1. <span data-ttu-id="6a7c3-170">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span><span class="sxs-lookup"><span data-stu-id="6a7c3-170">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="6a7c3-171">Select **Run once now** option.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-171">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="6a7c3-172">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-172">Click **Next**.</span></span>  

    ![Copy Wizard - Properties page](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="6a7c3-174">Step 2: Configure source</span><span class="sxs-lookup"><span data-stu-id="6a7c3-174">Step 2: Configure source</span></span>
<span data-ttu-id="6a7c3-175">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-175">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="6a7c3-176">Select the **Azure Blob Storage** as the data store and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-176">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Copy Wizard - Select source page](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="6a7c3-178">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-178">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Copy Wizard - Source connection information](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="6a7c3-180">Choose the **folder** containing the TPC-H line item files and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-180">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Copy Wizard - select input folder](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="6a7c3-182">Upon clicking **Next**, the file format settings are detected automatically.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-182">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="6a7c3-183">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-183">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="6a7c3-184">Click **Next** after you have previewed the data.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-184">Click **Next** after you have previewed the data.</span></span>

    ![Copy Wizard - file format settings](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="6a7c3-186">Step 3: Configure destination</span><span class="sxs-lookup"><span data-stu-id="6a7c3-186">Step 3: Configure destination</span></span>
<span data-ttu-id="6a7c3-187">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-187">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="6a7c3-188">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-188">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Copy Wizard - select destination data store](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="6a7c3-190">Fill in the connection information for Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-190">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="6a7c3-191">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-191">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Copy Wizard - destination connection info](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="6a7c3-193">Choose the destination table and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-193">Choose the destination table and click **Next**.</span></span>

    ![Copy Wizard - table mapping page](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="6a7c3-195">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-195">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="6a7c3-196">Step 4: Performance settings</span><span class="sxs-lookup"><span data-stu-id="6a7c3-196">Step 4: Performance settings</span></span>

<span data-ttu-id="6a7c3-197">**Allow polybase** is checked by default.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-197">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="6a7c3-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-198">Click **Next**.</span></span>

![Copy Wizard - schema mapping page](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="6a7c3-200">Step 5: Deploy and monitor load results</span><span class="sxs-lookup"><span data-stu-id="6a7c3-200">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="6a7c3-201">Click **Finish** button to deploy.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-201">Click **Finish** button to deploy.</span></span>

    ![Copy Wizard - summary page](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="6a7c3-203">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-203">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="6a7c3-204">Select the copy pipeline you created in the **Activity Windows** list.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-204">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Copy Wizard - summary page](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="6a7c3-206">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-206">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="6a7c3-207">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span><span class="sxs-lookup"><span data-stu-id="6a7c3-207">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Copy Wizard - succeeded dialog](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="6a7c3-209">Best practices</span><span class="sxs-lookup"><span data-stu-id="6a7c3-209">Best practices</span></span>
<span data-ttu-id="6a7c3-210">Here are a few best practices for running your Azure SQL Data Warehouse database:</span><span class="sxs-lookup"><span data-stu-id="6a7c3-210">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="6a7c3-211">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-211">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="6a7c3-212">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-212">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="6a7c3-213">For faster load speeds, consider using heap for transient data.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-213">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="6a7c3-214">Create statistics after you finish loading Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-214">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="6a7c3-215">See [Best practices for Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-215">See [Best practices for Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a7c3-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a7c3-216">Next steps</span></span>
* <span data-ttu-id="6a7c3-217">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-217">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="6a7c3-218">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span><span class="sxs-lookup"><span data-stu-id="6a7c3-218">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
