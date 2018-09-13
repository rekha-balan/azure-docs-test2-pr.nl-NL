---
title: Load terabytes of data into SQL Data Warehouse | Microsoft Docs
description: Demonstrates how 1 TB of data can be loaded into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jingwang
ms.openlocfilehash: 66017bbabecac64b83aa72234f42b6d98c99f99c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550762"
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-azure-data-factory-copy-wizard"></a><span data-ttu-id="174d0-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory [Copy Wizard]</span><span class="sxs-lookup"><span data-stu-id="174d0-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory [Copy Wizard]</span></span>
<span data-ttu-id="174d0-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span><span class="sxs-lookup"><span data-stu-id="174d0-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="174d0-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span><span class="sxs-lookup"><span data-stu-id="174d0-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="174d0-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span><span class="sxs-lookup"><span data-stu-id="174d0-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="174d0-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="174d0-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="174d0-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions on top of it.</span><span class="sxs-lookup"><span data-stu-id="174d0-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions on top of it.</span></span>  <span data-ttu-id="174d0-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="174d0-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="174d0-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span><span class="sxs-lookup"><span data-stu-id="174d0-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="174d0-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span><span class="sxs-lookup"><span data-stu-id="174d0-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="174d0-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span><span class="sxs-lookup"><span data-stu-id="174d0-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="174d0-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="174d0-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="174d0-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span><span class="sxs-lookup"><span data-stu-id="174d0-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="174d0-115">This article shows you how to use Data Factory Copy Wizard to load 1 TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span><span class="sxs-lookup"><span data-stu-id="174d0-115">This article shows you how to use Data Factory Copy Wizard to load 1 TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="174d0-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="174d0-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
> <span data-ttu-id="174d0-117">See [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article for general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="174d0-117">See [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article for general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse.</span></span>
>
> <span data-ttu-id="174d0-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="174d0-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="174d0-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="174d0-119">Prerequisites</span></span>
* <span data-ttu-id="174d0-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span><span class="sxs-lookup"><span data-stu-id="174d0-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="174d0-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="174d0-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="174d0-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span><span class="sxs-lookup"><span data-stu-id="174d0-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="174d0-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span><span class="sxs-lookup"><span data-stu-id="174d0-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="174d0-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="174d0-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="174d0-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span><span class="sxs-lookup"><span data-stu-id="174d0-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="174d0-126">…</span><span class="sxs-lookup"><span data-stu-id="174d0-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="174d0-127">Now copy the generated files to Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="174d0-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="174d0-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span><span class="sxs-lookup"><span data-stu-id="174d0-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="174d0-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span><span class="sxs-lookup"><span data-stu-id="174d0-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="174d0-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="174d0-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="174d0-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span><span class="sxs-lookup"><span data-stu-id="174d0-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="174d0-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="174d0-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="174d0-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87min (~200MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46min (~380MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14min (~1.2GBps throughput)</span><span class="sxs-lookup"><span data-stu-id="174d0-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87min (~200MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46min (~380MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14min (~1.2GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="174d0-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span><span class="sxs-lookup"><span data-stu-id="174d0-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Performance slider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="174d0-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span><span class="sxs-lookup"><span data-stu-id="174d0-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="174d0-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="174d0-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Scale button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="174d0-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="174d0-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Scale dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="174d0-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span><span class="sxs-lookup"><span data-stu-id="174d0-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="174d0-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span><span class="sxs-lookup"><span data-stu-id="174d0-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="174d0-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="174d0-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).</span></span>  
* <span data-ttu-id="174d0-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span><span class="sxs-lookup"><span data-stu-id="174d0-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="174d0-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="174d0-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="174d0-146">Launch Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="174d0-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="174d0-147">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="174d0-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="174d0-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="174d0-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="174d0-149">In the **New data factory** blade:</span><span class="sxs-lookup"><span data-stu-id="174d0-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="174d0-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="174d0-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="174d0-151">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="174d0-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="174d0-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="174d0-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="174d0-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="174d0-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="174d0-154">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="174d0-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="174d0-155">For Resource Group, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="174d0-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="174d0-156">Select **Use existing** to select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="174d0-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="174d0-157">Select **Create new** to enter a name for a resource group.</span><span class="sxs-lookup"><span data-stu-id="174d0-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="174d0-158">Select a **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="174d0-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="174d0-159">Select **Pin to dashboard** check box at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="174d0-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="174d0-160">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="174d0-160">Click **Create**.</span></span>
4. <span data-ttu-id="174d0-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="174d0-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Data factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="174d0-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="174d0-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="174d0-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span><span class="sxs-lookup"><span data-stu-id="174d0-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="174d0-165">Step 1: Configure data loading schedule</span><span class="sxs-lookup"><span data-stu-id="174d0-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="174d0-166">The first step is to configure the data loading schedule.</span><span class="sxs-lookup"><span data-stu-id="174d0-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="174d0-167">In the **Properties** page:</span><span class="sxs-lookup"><span data-stu-id="174d0-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="174d0-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span><span class="sxs-lookup"><span data-stu-id="174d0-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="174d0-169">Select **Run once now** option.</span><span class="sxs-lookup"><span data-stu-id="174d0-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="174d0-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-170">Click **Next**.</span></span>  

    ![Copy Wizard - Properties page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="174d0-172">Step 2: Configure source</span><span class="sxs-lookup"><span data-stu-id="174d0-172">Step 2: Configure source</span></span>
<span data-ttu-id="174d0-173">This section shows you the steps to configure the source: Azure Blob containing the 1 TB TPC-H line item files.</span><span class="sxs-lookup"><span data-stu-id="174d0-173">This section shows you the steps to configure the source: Azure Blob containing the 1 TB TPC-H line item files.</span></span>

1. <span data-ttu-id="174d0-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Copy Wizard - Select source page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="174d0-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Copy Wizard - Source connection information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="174d0-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Copy Wizard - select input folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="174d0-180">Upon clicking **Next**, the file format settings are detected automatically.</span><span class="sxs-lookup"><span data-stu-id="174d0-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="174d0-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span><span class="sxs-lookup"><span data-stu-id="174d0-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="174d0-182">Click **Next** after you have previewed the data.</span><span class="sxs-lookup"><span data-stu-id="174d0-182">Click **Next** after you have previewed the data.</span></span>

    ![Copy Wizard - file format settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="174d0-184">Step 3: Configure destination</span><span class="sxs-lookup"><span data-stu-id="174d0-184">Step 3: Configure destination</span></span>
<span data-ttu-id="174d0-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="174d0-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="174d0-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Copy Wizard - select destination data store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="174d0-188">Fill in the connection information for Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="174d0-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="174d0-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Copy Wizard - destination connection info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="174d0-191">Choose the destination table and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-191">Choose the destination table and click **Next**.</span></span>

    ![Copy Wizard - table mapping page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="174d0-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="174d0-194">Step 4: Performance settings</span><span class="sxs-lookup"><span data-stu-id="174d0-194">Step 4: Performance settings</span></span>

<span data-ttu-id="174d0-195">**Allow polybase** is checked by default.</span><span class="sxs-lookup"><span data-stu-id="174d0-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="174d0-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="174d0-196">Click **Next**.</span></span>

![Copy Wizard - schema mapping page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="174d0-198">Step 5: Deploy and monitor load results</span><span class="sxs-lookup"><span data-stu-id="174d0-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="174d0-199">Click **Finish** button to deploy.</span><span class="sxs-lookup"><span data-stu-id="174d0-199">Click **Finish** button to deploy.</span></span>

    ![Copy Wizard - summary page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="174d0-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span><span class="sxs-lookup"><span data-stu-id="174d0-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="174d0-202">Select the copy pipeline you created in the **Activity Windows** list.</span><span class="sxs-lookup"><span data-stu-id="174d0-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Copy Wizard - summary page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="174d0-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span><span class="sxs-lookup"><span data-stu-id="174d0-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="174d0-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span><span class="sxs-lookup"><span data-stu-id="174d0-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Copy Wizard - succeeded dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="174d0-207">Best practices</span><span class="sxs-lookup"><span data-stu-id="174d0-207">Best practices</span></span>
<span data-ttu-id="174d0-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span><span class="sxs-lookup"><span data-stu-id="174d0-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="174d0-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span><span class="sxs-lookup"><span data-stu-id="174d0-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="174d0-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span><span class="sxs-lookup"><span data-stu-id="174d0-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="174d0-211">For faster load speeds, consider using heap for transient data.</span><span class="sxs-lookup"><span data-stu-id="174d0-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="174d0-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="174d0-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="174d0-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span><span class="sxs-lookup"><span data-stu-id="174d0-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="174d0-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="174d0-214">Next steps</span></span>
* <span data-ttu-id="174d0-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="174d0-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="174d0-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span><span class="sxs-lookup"><span data-stu-id="174d0-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
















