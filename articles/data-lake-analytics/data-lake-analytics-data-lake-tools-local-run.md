---
title: Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK | Microsoft Docs
description: Learn how to use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to test and debug U-SQL jobs on your local workstation.
services: data-lake-analytics
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: 821673718a9ab564d99d747ad66af3ee176da7f5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563611"
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="d5da6-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="d5da6-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="d5da6-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span><span class="sxs-lookup"><span data-stu-id="d5da6-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="d5da6-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="d5da6-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

<span data-ttu-id="d5da6-106">Prerequisites:</span><span class="sxs-lookup"><span data-stu-id="d5da6-106">Prerequisites:</span></span>

- <span data-ttu-id="d5da6-107">An Azure Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="d5da6-107">An Azure Data Lake Analytics account.</span></span> <span data-ttu-id="d5da6-108">See [Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-108">See [Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="d5da6-109">Azure Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5da6-109">Azure Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="d5da6-110">See [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-110">See [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="d5da6-111">The U-SQL script development experience.</span><span class="sxs-lookup"><span data-stu-id="d5da6-111">The U-SQL script development experience.</span></span> <span data-ttu-id="d5da6-112">See [Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-112">See [Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>


## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="d5da6-113">Understand the data-root folder and the file path</span><span class="sxs-lookup"><span data-stu-id="d5da6-113">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="d5da6-114">Both local run and the U-SQL SDK require a data-root folder.</span><span class="sxs-lookup"><span data-stu-id="d5da6-114">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="d5da6-115">The data-root folder is a "local store" for the local compute account.</span><span class="sxs-lookup"><span data-stu-id="d5da6-115">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="d5da6-116">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="d5da6-116">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="d5da6-117">Switching to a different data-root folder is just like switching to a different store account.</span><span class="sxs-lookup"><span data-stu-id="d5da6-117">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="d5da6-118">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span><span class="sxs-lookup"><span data-stu-id="d5da6-118">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="d5da6-119">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span><span class="sxs-lookup"><span data-stu-id="d5da6-119">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="d5da6-120">The data-root folder is used to:</span><span class="sxs-lookup"><span data-stu-id="d5da6-120">The data-root folder is used to:</span></span>

- <span data-ttu-id="d5da6-121">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span><span class="sxs-lookup"><span data-stu-id="d5da6-121">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="d5da6-122">Look up the input and output paths that are defined as relative paths in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5da6-122">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="d5da6-123">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span><span class="sxs-lookup"><span data-stu-id="d5da6-123">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="d5da6-124">You can use both a relative path and a local absolute path in U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="d5da6-124">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="d5da6-125">The relative path is relative to the specified data-root folder path.</span><span class="sxs-lookup"><span data-stu-id="d5da6-125">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="d5da6-126">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span><span class="sxs-lookup"><span data-stu-id="d5da6-126">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="d5da6-127">Here are some examples of relative paths and their equivalent absolute paths.</span><span class="sxs-lookup"><span data-stu-id="d5da6-127">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="d5da6-128">In these examples, C:\LocalRunDataRoot is the data-root folder.</span><span class="sxs-lookup"><span data-stu-id="d5da6-128">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="d5da6-129">Relative path</span><span class="sxs-lookup"><span data-stu-id="d5da6-129">Relative path</span></span>|<span data-ttu-id="d5da6-130">Absolute path</span><span class="sxs-lookup"><span data-stu-id="d5da6-130">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="d5da6-131">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="d5da6-131">/abc/def/input.csv</span></span> |<span data-ttu-id="d5da6-132">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="d5da6-132">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="d5da6-133">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="d5da6-133">abc/def/input.csv</span></span>  |<span data-ttu-id="d5da6-134">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="d5da6-134">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="d5da6-135">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="d5da6-135">D:/abc/def/input.csv</span></span> |<span data-ttu-id="d5da6-136">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="d5da6-136">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="d5da6-137">Use local run from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5da6-137">Use local run from Visual Studio</span></span>

<span data-ttu-id="d5da6-138">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5da6-138">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="d5da6-139">By using this feature, you can:</span><span class="sxs-lookup"><span data-stu-id="d5da6-139">By using this feature, you can:</span></span>

- <span data-ttu-id="d5da6-140">Run a U-SQL script locally, along with C# assemblies.</span><span class="sxs-lookup"><span data-stu-id="d5da6-140">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="d5da6-141">Debug a C# assembly locally.</span><span class="sxs-lookup"><span data-stu-id="d5da6-141">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="d5da6-142">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="d5da6-142">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="d5da6-143">You can also find the local catalog also from Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="d5da6-143">You can also find the local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools for Visual Studio local-run local catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="d5da6-145">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span><span class="sxs-lookup"><span data-stu-id="d5da6-145">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="d5da6-146">The default local-run parallelism is 1.</span><span class="sxs-lookup"><span data-stu-id="d5da6-146">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="d5da6-147">To configure local run in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5da6-147">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="d5da6-148">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5da6-148">Open Visual Studio.</span></span>
2. <span data-ttu-id="d5da6-149">Open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d5da6-149">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="d5da6-150">Expand **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5da6-150">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="d5da6-151">Click the **Data Lake** menu, and then click **Options and Settings**.</span><span class="sxs-lookup"><span data-stu-id="d5da6-151">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="d5da6-152">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span><span class="sxs-lookup"><span data-stu-id="d5da6-152">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools for Visual Studio local-run configure settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="d5da6-154">A Visual Studio U-SQL project is required for performing local run.</span><span class="sxs-lookup"><span data-stu-id="d5da6-154">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="d5da6-155">This part is different from running U-SQL scripts from Azure.</span><span class="sxs-lookup"><span data-stu-id="d5da6-155">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="d5da6-156">To run a U-SQL script locally</span><span class="sxs-lookup"><span data-stu-id="d5da6-156">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="d5da6-157">From Visual Studio, open your U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="d5da6-157">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="d5da6-158">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="d5da6-158">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="d5da6-159">Select **(Local)** as the Analytics account to run your script locally.</span><span class="sxs-lookup"><span data-stu-id="d5da6-159">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="d5da6-160">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span><span class="sxs-lookup"><span data-stu-id="d5da6-160">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools for Visual Studio local-run submit jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="d5da6-162">Debug scripts and C# assemblies locally</span><span class="sxs-lookup"><span data-stu-id="d5da6-162">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="d5da6-163">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span><span class="sxs-lookup"><span data-stu-id="d5da6-163">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="d5da6-164">You can set breakpoints in both the code behind file and in a referenced C# project.</span><span class="sxs-lookup"><span data-stu-id="d5da6-164">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="d5da6-165">To debug local code in code behind file</span><span class="sxs-lookup"><span data-stu-id="d5da6-165">To debug local code in code behind file</span></span>

1. <span data-ttu-id="d5da6-166">Set breakpoints in the code behind file.</span><span class="sxs-lookup"><span data-stu-id="d5da6-166">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="d5da6-167">Press F5 to debug the script locally.</span><span class="sxs-lookup"><span data-stu-id="d5da6-167">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="d5da6-168">The following procedure only works in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d5da6-168">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="d5da6-169">In older Visual Studio you may need to manually add the pdb files.</span><span class="sxs-lookup"><span data-stu-id="d5da6-169">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="d5da6-170">To debug local code in a referenced C# project</span><span class="sxs-lookup"><span data-stu-id="d5da6-170">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="d5da6-171">Create a C# Assembly project, and build it to generate the output dll.</span><span class="sxs-lookup"><span data-stu-id="d5da6-171">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="d5da6-172">Register the dll using a U-SQL statement:</span><span class="sxs-lookup"><span data-stu-id="d5da6-172">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="d5da6-173">Set breakpoints in the C# code.</span><span class="sxs-lookup"><span data-stu-id="d5da6-173">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="d5da6-174">Press F5 to debug the script with referencing the C# dll locally.</span><span class="sxs-lookup"><span data-stu-id="d5da6-174">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="d5da6-175">Use local run from the Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="d5da6-175">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="d5da6-176">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span><span class="sxs-lookup"><span data-stu-id="d5da6-176">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="d5da6-177">Through these, you can scale your U-SQL local test.</span><span class="sxs-lookup"><span data-stu-id="d5da6-177">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="d5da6-178">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-178">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d5da6-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5da6-179">Next steps</span></span>

* <span data-ttu-id="d5da6-180">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-180">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="d5da6-181">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-181">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="d5da6-182">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-182">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="d5da6-183">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-183">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="d5da6-184">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-184">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="d5da6-185">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-185">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="d5da6-186">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-186">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="d5da6-187">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="d5da6-187">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>



