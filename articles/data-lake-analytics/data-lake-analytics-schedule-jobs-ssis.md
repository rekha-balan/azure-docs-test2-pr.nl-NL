---
title: Schedule Azure Data Lake Analytics U-SQL jobs using SSIS
description: Learn how to use SQL Server Integration Services to schedule U-SQL jobs.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.topic: conceptual
ms.workload: big-data
ms.date: 07/17/2018
ms.openlocfilehash: 8b6c8220bd009505f683ce888558e612aebdc0b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866861"
---
# <a name="schedule-u-sql-jobs-using-sql-server-integration-services-ssis"></a><span data-ttu-id="5e863-103">Schedule U-SQL jobs using SQL Server Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="5e863-103">Schedule U-SQL jobs using SQL Server Integration Services (SSIS)</span></span>

<span data-ttu-id="5e863-104">In this document, you learn how to orchestrate and create U-SQL jobs using SQL Server Integration Service (SSIS).</span><span class="sxs-lookup"><span data-stu-id="5e863-104">In this document, you learn how to orchestrate and create U-SQL jobs using SQL Server Integration Service (SSIS).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5e863-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5e863-105">Prerequisites</span></span>

<span data-ttu-id="5e863-106">[Azure Feature Pack for Integration Services](https://docs.microsoft.com/sql/integration-services/azure-feature-pack-for-integration-services-ssis?view=sql-server-2017#scenario-managing-data-in-the-cloud) provides the [Azure Data Lake Analytics task](https://docs.microsoft.com/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017) and the [Azure Data Lake Analytics Connection Manager](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-analytics-connection-manager?view=sql-server-2017) that helps connect to Azure Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="5e863-106">[Azure Feature Pack for Integration Services](https://docs.microsoft.com/sql/integration-services/azure-feature-pack-for-integration-services-ssis?view=sql-server-2017#scenario-managing-data-in-the-cloud) provides the [Azure Data Lake Analytics task](https://docs.microsoft.com/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017) and the [Azure Data Lake Analytics Connection Manager](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-analytics-connection-manager?view=sql-server-2017) that helps connect to Azure Data Lake Analytics service.</span></span> <span data-ttu-id="5e863-107">To use this task, make sure you install:</span><span class="sxs-lookup"><span data-stu-id="5e863-107">To use this task, make sure you install:</span></span>

- [<span data-ttu-id="5e863-108">Download and install SQL Server Data Tools (SSDT) for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5e863-108">Download and install SQL Server Data Tools (SSDT) for Visual Studio</span></span>](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017)
- [<span data-ttu-id="5e863-109">Install Azure Feature Pack for Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="5e863-109">Install Azure Feature Pack for Integration Services (SSIS)</span></span>](https://docs.microsoft.com/sql/integration-services/azure-feature-pack-for-integration-services-ssis?view=sql-server-2017)

## <a name="azure-data-lake-analytics-task"></a><span data-ttu-id="5e863-110">Azure Data Lake Analytics task</span><span class="sxs-lookup"><span data-stu-id="5e863-110">Azure Data Lake Analytics task</span></span>

<span data-ttu-id="5e863-111">The Azure Data Lake Analytics task let users submit U-SQL jobs to the Azure Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="5e863-111">The Azure Data Lake Analytics task let users submit U-SQL jobs to the Azure Data Lake Analytics account.</span></span> 

<span data-ttu-id="5e863-112">[Learn how to configure Azure Data Lake Analytics task](https://docs.microsoft.com/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5e863-112">[Learn how to configure Azure Data Lake Analytics task](https://docs.microsoft.com/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017).</span></span>

![Azure Data Lake Analytics Task in SSIS](./media/data-lake-analytics-schedule-jobs-ssis/data-lake-analytics-azure-data-lake-analytics-task-in-ssis.png)

<span data-ttu-id="5e863-114">You can get the U-SQL script from different places by using SSIS built-in functions and tasks, below scenarios show how can you configure the U-SQL scripts for different user cases.</span><span class="sxs-lookup"><span data-stu-id="5e863-114">You can get the U-SQL script from different places by using SSIS built-in functions and tasks, below scenarios show how can you configure the U-SQL scripts for different user cases.</span></span>

## <a name="scenario-1-use-inline-script-call-tvfs-and-stored-procs"></a><span data-ttu-id="5e863-115">Scenario 1-Use inline script call tvfs and stored procs</span><span class="sxs-lookup"><span data-stu-id="5e863-115">Scenario 1-Use inline script call tvfs and stored procs</span></span>

<span data-ttu-id="5e863-116">In Azure Data Lake Analytics Task Editor, configure **SourceType** as **DiretInput**, and put the U-SQL statements into **USQLStatemnt**.</span><span class="sxs-lookup"><span data-stu-id="5e863-116">In Azure Data Lake Analytics Task Editor, configure **SourceType** as **DiretInput**, and put the U-SQL statements into **USQLStatemnt**.</span></span>

<span data-ttu-id="5e863-117">For easy maintainence and code management, only put short U-SQL script as inline scripts, for example, you can call existing table valued functions and stored procedures in your U-SQL databases.</span><span class="sxs-lookup"><span data-stu-id="5e863-117">For easy maintainence and code management, only put short U-SQL script as inline scripts, for example, you can call existing table valued functions and stored procedures in your U-SQL databases.</span></span> 

![Edit inline U-SQL script in SSIS task](./media/data-lake-analytics-schedule-jobs-ssis/edit-inline-usql-script-in-ssis.png)

<span data-ttu-id="5e863-119">Related article: [How to pass parameter to stored procedures](#scenario-6-pass-parameters-to-u-sql-script)</span><span class="sxs-lookup"><span data-stu-id="5e863-119">Related article: [How to pass parameter to stored procedures](#scenario-6-pass-parameters-to-u-sql-script)</span></span>

## <a name="scenario-2-use-u-sql-files-in-azure-data-lake-store"></a><span data-ttu-id="5e863-120">Scenario 2-Use U-SQL files in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5e863-120">Scenario 2-Use U-SQL files in Azure Data Lake Store</span></span>

<span data-ttu-id="5e863-121">You can also use U-SQL files in the Azure Data Lake Store by using **Azure Data Lake Store File System Task** in Azure Feature Pack.</span><span class="sxs-lookup"><span data-stu-id="5e863-121">You can also use U-SQL files in the Azure Data Lake Store by using **Azure Data Lake Store File System Task** in Azure Feature Pack.</span></span> <span data-ttu-id="5e863-122">This approach enables you to use the scripts stored on cloud.</span><span class="sxs-lookup"><span data-stu-id="5e863-122">This approach enables you to use the scripts stored on cloud.</span></span>

<span data-ttu-id="5e863-123">Follow below steps to set up the connection between Azure Data Lake Store File System Task and Azure Data Lake Analytics Task.</span><span class="sxs-lookup"><span data-stu-id="5e863-123">Follow below steps to set up the connection between Azure Data Lake Store File System Task and Azure Data Lake Analytics Task.</span></span>

### <a name="set-task-control-flow"></a><span data-ttu-id="5e863-124">Set task control flow</span><span class="sxs-lookup"><span data-stu-id="5e863-124">Set task control flow</span></span>

<span data-ttu-id="5e863-125">In SSIS package design view, add an **Azure Data Lake Store File System Task**, a **Foreach Loop Container** and an **Azure Data Lake Analytics Task** in the Foreach Loop Container.</span><span class="sxs-lookup"><span data-stu-id="5e863-125">In SSIS package design view, add an **Azure Data Lake Store File System Task**, a **Foreach Loop Container** and an **Azure Data Lake Analytics Task** in the Foreach Loop Container.</span></span> <span data-ttu-id="5e863-126">The Azure Data Lake Store File System Task helps to download U-SQL files in your ADLS account to a temporary folder.</span><span class="sxs-lookup"><span data-stu-id="5e863-126">The Azure Data Lake Store File System Task helps to download U-SQL files in your ADLS account to a temporary folder.</span></span> <span data-ttu-id="5e863-127">The Foreach Loop Container and the Azure Data Lake Analytics Task help to submit every U-SQL file under the temporary folder to the Azure Data Lake Analytics account as a U-SQL job.</span><span class="sxs-lookup"><span data-stu-id="5e863-127">The Foreach Loop Container and the Azure Data Lake Analytics Task help to submit every U-SQL file under the temporary folder to the Azure Data Lake Analytics account as a U-SQL job.</span></span>

![Use U-SQL files in Azure Data Lake Store](./media/data-lake-analytics-schedule-jobs-ssis/use-u-sql-files-in-azure-data-lake-store.png)

### <a name="configure-azure-data-lake-store-file-system-task"></a><span data-ttu-id="5e863-129">Configure Azure Data Lake Store File System Task</span><span class="sxs-lookup"><span data-stu-id="5e863-129">Configure Azure Data Lake Store File System Task</span></span>

1. <span data-ttu-id="5e863-130">Set **Operation** to **CopyFromADLS**.</span><span class="sxs-lookup"><span data-stu-id="5e863-130">Set **Operation** to **CopyFromADLS**.</span></span>
2. <span data-ttu-id="5e863-131">Set up **AzureDataLakeConnection**, learn more about [Azure Data Lake Store Connection Manager](https://docs.microsoft.com/en-us/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5e863-131">Set up **AzureDataLakeConnection**, learn more about [Azure Data Lake Store Connection Manager](https://docs.microsoft.com/en-us/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager?view=sql-server-2017).</span></span>
3. <span data-ttu-id="5e863-132">Set **AzureDataLakeDirectory**.</span><span class="sxs-lookup"><span data-stu-id="5e863-132">Set **AzureDataLakeDirectory**.</span></span> <span data-ttu-id="5e863-133">Point to the folder storing your U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="5e863-133">Point to the folder storing your U-SQL scripts.</span></span> <span data-ttu-id="5e863-134">Use relative path that is relative to the Azure Data Lake Store account root folder.</span><span class="sxs-lookup"><span data-stu-id="5e863-134">Use relative path that is relative to the Azure Data Lake Store account root folder.</span></span>
4. <span data-ttu-id="5e863-135">Set **Destination** to a folder that caches the downloaded U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="5e863-135">Set **Destination** to a folder that caches the downloaded U-SQL scripts.</span></span> <span data-ttu-id="5e863-136">This folder path will be used in Foreach Loop Container for U-SQL job submission.</span><span class="sxs-lookup"><span data-stu-id="5e863-136">This folder path will be used in Foreach Loop Container for U-SQL job submission.</span></span> 

![Configure Azure Data Lake Store File System Task](./media/data-lake-analytics-schedule-jobs-ssis/configure-azure-data-lake-store-file-system-task.png)

<span data-ttu-id="5e863-138">[Learn more about Azure Data Lake Store File System Task](https://docs.microsoft.com/sql/integration-services/control-flow/azure-data-lake-store-file-system-task?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5e863-138">[Learn more about Azure Data Lake Store File System Task](https://docs.microsoft.com/sql/integration-services/control-flow/azure-data-lake-store-file-system-task?view=sql-server-2017).</span></span>

### <a name="configure-foreach-loop-container"></a><span data-ttu-id="5e863-139">Configure Foreach Loop Container</span><span class="sxs-lookup"><span data-stu-id="5e863-139">Configure Foreach Loop Container</span></span>

1. <span data-ttu-id="5e863-140">In **Collection** page, set **Enumerator** to **Foreach File Enumerator**.</span><span class="sxs-lookup"><span data-stu-id="5e863-140">In **Collection** page, set **Enumerator** to **Foreach File Enumerator**.</span></span>

2. <span data-ttu-id="5e863-141">Set **Folder** under **Enumerator configuration** group to the temporary folder that includes the downloaded U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="5e863-141">Set **Folder** under **Enumerator configuration** group to the temporary folder that includes the downloaded U-SQL scripts.</span></span>

3. <span data-ttu-id="5e863-142">Set **Files** under **Enumerator configuration** to `*.usql` so that the loop container only catches the files ending with `.usql`.</span><span class="sxs-lookup"><span data-stu-id="5e863-142">Set **Files** under **Enumerator configuration** to `*.usql` so that the loop container only catches the files ending with `.usql`.</span></span>

    ![Configure Foreach Loop Container](./media/data-lake-analytics-schedule-jobs-ssis/configure-foreach-loop-container-collection.png)

4. <span data-ttu-id="5e863-144">In **Variable Mappings** page, add a user defined variable to get the file name for each U-SQL file.</span><span class="sxs-lookup"><span data-stu-id="5e863-144">In **Variable Mappings** page, add a user defined variable to get the file name for each U-SQL file.</span></span> <span data-ttu-id="5e863-145">Set the **Index** to 0 to get the file name.</span><span class="sxs-lookup"><span data-stu-id="5e863-145">Set the **Index** to 0 to get the file name.</span></span> <span data-ttu-id="5e863-146">In this example, define a variable called `User::FileName`.</span><span class="sxs-lookup"><span data-stu-id="5e863-146">In this example, define a variable called `User::FileName`.</span></span> <span data-ttu-id="5e863-147">This variable will be used to dynamically get U-SQL script file connection and set U-SQL job name in Azure Data Lake Analytics Task.</span><span class="sxs-lookup"><span data-stu-id="5e863-147">This variable will be used to dynamically get U-SQL script file connection and set U-SQL job name in Azure Data Lake Analytics Task.</span></span>

    ![Configure Foreach Loop Container to get file name](./media/data-lake-analytics-schedule-jobs-ssis/configure-foreach-loop-container-variable-mapping.png)

### <a name="configure-azure-data-lake-analytics-task"></a><span data-ttu-id="5e863-149">Configure Azure Data Lake Analytics Task</span><span class="sxs-lookup"><span data-stu-id="5e863-149">Configure Azure Data Lake Analytics Task</span></span> 

1. <span data-ttu-id="5e863-150">Set **SourceType** to **FileConnection**.</span><span class="sxs-lookup"><span data-stu-id="5e863-150">Set **SourceType** to **FileConnection**.</span></span>

2. <span data-ttu-id="5e863-151">Set **FileConnection** to the file connection that points to the file objects returned from Foreach Loop Container.</span><span class="sxs-lookup"><span data-stu-id="5e863-151">Set **FileConnection** to the file connection that points to the file objects returned from Foreach Loop Container.</span></span>
    
    <span data-ttu-id="5e863-152">To create this file connection:</span><span class="sxs-lookup"><span data-stu-id="5e863-152">To create this file connection:</span></span>

    1. <span data-ttu-id="5e863-153">Choose **<New Connection...>** in FileConnection setting.</span><span class="sxs-lookup"><span data-stu-id="5e863-153">Choose **<New Connection...>** in FileConnection setting.</span></span>
    2. <span data-ttu-id="5e863-154">Set **Usage type** to **Existing file**, and set the **File** to any existing file's file path.</span><span class="sxs-lookup"><span data-stu-id="5e863-154">Set **Usage type** to **Existing file**, and set the **File** to any existing file's file path.</span></span>

        ![Configure Foreach Loop Container](./media/data-lake-analytics-schedule-jobs-ssis/configure-file-connection-for-foreach-loop-container.png)

    3. <span data-ttu-id="5e863-156">In **Connection Managers** view, right-click the file connection created just now, and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5e863-156">In **Connection Managers** view, right-click the file connection created just now, and choose **Properties**.</span></span>

    4. <span data-ttu-id="5e863-157">In the **Properties** window, expand **Expressions**, and set **ConnectionString** to the variable defined in Foreach Loop Container, for example, `@[User::FileName]`.</span><span class="sxs-lookup"><span data-stu-id="5e863-157">In the **Properties** window, expand **Expressions**, and set **ConnectionString** to the variable defined in Foreach Loop Container, for example, `@[User::FileName]`.</span></span>

        ![Configure Foreach Loop Container](./media/data-lake-analytics-schedule-jobs-ssis/configure-file-connection-property-for-foreach-loop-container.png)

3. <span data-ttu-id="5e863-159">Set **AzureDataLakeAnalyticsConnection** to the Azure Data Lake Analytics account that you want to submit jobs to.</span><span class="sxs-lookup"><span data-stu-id="5e863-159">Set **AzureDataLakeAnalyticsConnection** to the Azure Data Lake Analytics account that you want to submit jobs to.</span></span> <span data-ttu-id="5e863-160">Learn more about [Azure Data Lake Analytics Connection Manager](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-analytics-connection-manager?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5e863-160">Learn more about [Azure Data Lake Analytics Connection Manager](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-analytics-connection-manager?view=sql-server-2017).</span></span>

4. <span data-ttu-id="5e863-161">Set other job configurations.</span><span class="sxs-lookup"><span data-stu-id="5e863-161">Set other job configurations.</span></span> <span data-ttu-id="5e863-162">[Learn More](https://docs.microsoft.com/en-us/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5e863-162">[Learn More](https://docs.microsoft.com/en-us/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017).</span></span>

5. <span data-ttu-id="5e863-163">Use **Expressions** to dynamically set U-SQL job name:</span><span class="sxs-lookup"><span data-stu-id="5e863-163">Use **Expressions** to dynamically set U-SQL job name:</span></span>

    1. <span data-ttu-id="5e863-164">In **Expressions** page, add a new expression key-value pair for **JobName**.</span><span class="sxs-lookup"><span data-stu-id="5e863-164">In **Expressions** page, add a new expression key-value pair for **JobName**.</span></span>
    2. <span data-ttu-id="5e863-165">Set the value for JobName to the variable defined in Foreach Loop Container, for example, `@[User::FileName]`.</span><span class="sxs-lookup"><span data-stu-id="5e863-165">Set the value for JobName to the variable defined in Foreach Loop Container, for example, `@[User::FileName]`.</span></span>
    
        ![Configure SSIS Expression for U-SQL job name](./media/data-lake-analytics-schedule-jobs-ssis/configure-expression-for-u-sql-job-name.png)

## <a name="scenario-3-use-u-sql-files-in-azure-blob-storage"></a><span data-ttu-id="5e863-167">Scenario 3-Use U-SQL files in Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="5e863-167">Scenario 3-Use U-SQL files in Azure Blob Storage</span></span>

<span data-ttu-id="5e863-168">You can use U-SQL files in Azure Blob Storage by using **Azure Blob Download Task** in Azure Feature Pack.</span><span class="sxs-lookup"><span data-stu-id="5e863-168">You can use U-SQL files in Azure Blob Storage by using **Azure Blob Download Task** in Azure Feature Pack.</span></span> <span data-ttu-id="5e863-169">This approach enables you using the scripts on cloud.</span><span class="sxs-lookup"><span data-stu-id="5e863-169">This approach enables you using the scripts on cloud.</span></span>

<span data-ttu-id="5e863-170">The steps are similar with [Scnario 2: Use U-SQL files in Azure Data Lake Store](#scenario-2-use-u-sql-files-in-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="5e863-170">The steps are similar with [Scnario 2: Use U-SQL files in Azure Data Lake Store](#scenario-2-use-u-sql-files-in-azure-data-lake-store).</span></span> <span data-ttu-id="5e863-171">Change the Azure Data Lake Store File System Task to Azure Blob Download Task.</span><span class="sxs-lookup"><span data-stu-id="5e863-171">Change the Azure Data Lake Store File System Task to Azure Blob Download Task.</span></span> <span data-ttu-id="5e863-172">[Learn more about Azure Blob Download Task](https://docs.microsoft.com/en-us/sql/integration-services/control-flow/azure-blob-download-task?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5e863-172">[Learn more about Azure Blob Download Task](https://docs.microsoft.com/en-us/sql/integration-services/control-flow/azure-blob-download-task?view=sql-server-2017).</span></span>

<span data-ttu-id="5e863-173">The control flow is like below.</span><span class="sxs-lookup"><span data-stu-id="5e863-173">The control flow is like below.</span></span>

![Use U-SQL files in Azure Data Lake Store](./media/data-lake-analytics-schedule-jobs-ssis/use-u-sql-files-in-azure-blob-storage.png)

## <a name="scenario-4-use-u-sql-files-on-the-local-machine"></a><span data-ttu-id="5e863-175">Scenario 4-Use U-SQL files on the local machine</span><span class="sxs-lookup"><span data-stu-id="5e863-175">Scenario 4-Use U-SQL files on the local machine</span></span>

<span data-ttu-id="5e863-176">Besides of using U-SQL files stored on cloud, you can also use files on your local machine or files deployed with your SSIS packages.</span><span class="sxs-lookup"><span data-stu-id="5e863-176">Besides of using U-SQL files stored on cloud, you can also use files on your local machine or files deployed with your SSIS packages.</span></span>

1. <span data-ttu-id="5e863-177">Right-click **Connection Managers** in SSIS project and choose **New Connection Manager**.</span><span class="sxs-lookup"><span data-stu-id="5e863-177">Right-click **Connection Managers** in SSIS project and choose **New Connection Manager**.</span></span>

2. <span data-ttu-id="5e863-178">Select **File** type and click **Add...**.</span><span class="sxs-lookup"><span data-stu-id="5e863-178">Select **File** type and click **Add...**.</span></span>

3. <span data-ttu-id="5e863-179">Set **Usage type** to **Existing file**, and set the **File** to the file on the local machine.</span><span class="sxs-lookup"><span data-stu-id="5e863-179">Set **Usage type** to **Existing file**, and set the **File** to the file on the local machine.</span></span>

    ![Add file connection to the local file](./media/data-lake-analytics-schedule-jobs-ssis/configure-file-connection-for-foreach-loop-container.png)

4. <span data-ttu-id="5e863-181">Add **Azure Data Lake Analytics** Task and:</span><span class="sxs-lookup"><span data-stu-id="5e863-181">Add **Azure Data Lake Analytics** Task and:</span></span>
    1. <span data-ttu-id="5e863-182">Set **SourceType** to **FileConnection**.</span><span class="sxs-lookup"><span data-stu-id="5e863-182">Set **SourceType** to **FileConnection**.</span></span>
    2. <span data-ttu-id="5e863-183">Set **FileConnection** to the File Connection created just now.</span><span class="sxs-lookup"><span data-stu-id="5e863-183">Set **FileConnection** to the File Connection created just now.</span></span>

5. <span data-ttu-id="5e863-184">Finish other configurations for Azure Data Lake Analytics Task.</span><span class="sxs-lookup"><span data-stu-id="5e863-184">Finish other configurations for Azure Data Lake Analytics Task.</span></span>

## <a name="scenario-5-use-u-sql-statement-in-ssis-variable"></a><span data-ttu-id="5e863-185">Scenario 5-Use U-SQL statement in SSIS variable</span><span class="sxs-lookup"><span data-stu-id="5e863-185">Scenario 5-Use U-SQL statement in SSIS variable</span></span>

<span data-ttu-id="5e863-186">In some cases, you may need to dynamically generate the U-SQL statements.</span><span class="sxs-lookup"><span data-stu-id="5e863-186">In some cases, you may need to dynamically generate the U-SQL statements.</span></span> <span data-ttu-id="5e863-187">You can use **SSIS Variable** with **SSIS Expression** and other SSIS tasks, like Script Task, to help you generate the U-SQL statement dynamically.</span><span class="sxs-lookup"><span data-stu-id="5e863-187">You can use **SSIS Variable** with **SSIS Expression** and other SSIS tasks, like Script Task, to help you generate the U-SQL statement dynamically.</span></span>

1. <span data-ttu-id="5e863-188">Open Variables tool window through **SSIS > Variables** top-level menu.</span><span class="sxs-lookup"><span data-stu-id="5e863-188">Open Variables tool window through **SSIS > Variables** top-level menu.</span></span>

2. <span data-ttu-id="5e863-189">Add an SSIS Variable and set the value directly or use **Expression** to generate the value.</span><span class="sxs-lookup"><span data-stu-id="5e863-189">Add an SSIS Variable and set the value directly or use **Expression** to generate the value.</span></span>

3. <span data-ttu-id="5e863-190">Add **Azure Data Lake Analytics Task** and:</span><span class="sxs-lookup"><span data-stu-id="5e863-190">Add **Azure Data Lake Analytics Task** and:</span></span>
    1. <span data-ttu-id="5e863-191">Set **SourceType** to **Variable**.</span><span class="sxs-lookup"><span data-stu-id="5e863-191">Set **SourceType** to **Variable**.</span></span>
    2. <span data-ttu-id="5e863-192">Set **SourceVariable** to the SSIS Variable created just now.</span><span class="sxs-lookup"><span data-stu-id="5e863-192">Set **SourceVariable** to the SSIS Variable created just now.</span></span>

4. <span data-ttu-id="5e863-193">Finish other configurations for Azure Data Lake Analytics Task.</span><span class="sxs-lookup"><span data-stu-id="5e863-193">Finish other configurations for Azure Data Lake Analytics Task.</span></span>

## <a name="scenario-6-pass-parameters-to-u-sql-script"></a><span data-ttu-id="5e863-194">Scenario 6-Pass parameters to U-SQL script</span><span class="sxs-lookup"><span data-stu-id="5e863-194">Scenario 6-Pass parameters to U-SQL script</span></span>

<span data-ttu-id="5e863-195">In some cases, you may want to dynamically set the U-SQL variable value in the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="5e863-195">In some cases, you may want to dynamically set the U-SQL variable value in the U-SQL script.</span></span> <span data-ttu-id="5e863-196">**Parameter Mapping** feature in Azure Data Lake Analytics Task help with this scenario.</span><span class="sxs-lookup"><span data-stu-id="5e863-196">**Parameter Mapping** feature in Azure Data Lake Analytics Task help with this scenario.</span></span> <span data-ttu-id="5e863-197">There are usually two typical user cases:</span><span class="sxs-lookup"><span data-stu-id="5e863-197">There are usually two typical user cases:</span></span>

- <span data-ttu-id="5e863-198">Set the input and output file path variables dynamically based on current date and time.</span><span class="sxs-lookup"><span data-stu-id="5e863-198">Set the input and output file path variables dynamically based on current date and time.</span></span>
- <span data-ttu-id="5e863-199">Set the parameter for stored procedures.</span><span class="sxs-lookup"><span data-stu-id="5e863-199">Set the parameter for stored procedures.</span></span>

<span data-ttu-id="5e863-200">[Learn more about how to set parameters for the U-SQL script](https://docs.microsoft.com/en-us/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017#parameter-mapping-page-configuration).</span><span class="sxs-lookup"><span data-stu-id="5e863-200">[Learn more about how to set parameters for the U-SQL script](https://docs.microsoft.com/en-us/sql/integration-services/control-flow/azure-data-lake-analytics-task?view=sql-server-2017#parameter-mapping-page-configuration).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e863-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e863-201">Next steps</span></span>

- [<span data-ttu-id="5e863-202">Run SSIS packages in Azure</span><span class="sxs-lookup"><span data-stu-id="5e863-202">Run SSIS packages in Azure</span></span>](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)
- [<span data-ttu-id="5e863-203">Azure Feature Pack for Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="5e863-203">Azure Feature Pack for Integration Services (SSIS)</span></span>](https://docs.microsoft.com/sql/integration-services/azure-feature-pack-for-integration-services-ssis?view=sql-server-2017#scenario-managing-data-in-the-cloud)
- [<span data-ttu-id="5e863-204">Schedule U-SQL jobs using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5e863-204">Schedule U-SQL jobs using Azure Data Factory</span></span>](https://docs.microsoft.com/en-us/azure/data-factory/transform-data-using-data-lake-analytics)

