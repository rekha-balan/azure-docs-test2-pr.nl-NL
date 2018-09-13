---
title: Debug U-SQL jobs | Microsoft Docs
description: 'Learn how to debug U-SQL failed vertex using Visual Studio. '
services: data-lake-analytics
documentationcenter: ''
author: yanancai
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: yanacai
ms.openlocfilehash: 4f1dddeeef28d5d191bb1d84534f14813941a2bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563177"
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="66144-103">Debug user defined C# code for failed U-SQL jobs</span><span class="sxs-lookup"><span data-stu-id="66144-103">Debug user defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="66144-104">Learn how to debug U-SQL jobs failed with user defined code bugs using Azure Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66144-104">Learn how to debug U-SQL jobs failed with user defined code bugs using Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="background"></a><span data-ttu-id="66144-105">Background</span><span class="sxs-lookup"><span data-stu-id="66144-105">Background</span></span>

<span data-ttu-id="66144-106">U-SQL provides extensibility model through C#, users can write user defined C# code, like user defined extractor, reducer, etc., to achieve more extensibility (learn more about [U-SQL User Defined Code](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#user-defined-functions---udf)).</span><span class="sxs-lookup"><span data-stu-id="66144-106">U-SQL provides extensibility model through C#, users can write user defined C# code, like user defined extractor, reducer, etc., to achieve more extensibility (learn more about [U-SQL User Defined Code](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#user-defined-functions---udf)).</span></span> <span data-ttu-id="66144-107">However, no developers can code without making mistakes, and debugging in big data systems is hard since many systems only provide limited runtime debugging information like logs, etc.</span><span class="sxs-lookup"><span data-stu-id="66144-107">However, no developers can code without making mistakes, and debugging in big data systems is hard since many systems only provide limited runtime debugging information like logs, etc.</span></span> 

<span data-ttu-id="66144-108">ADL Tools for Visual Studio offers a feature called **Failed Vertex Debug**, using which you can easily clone failed environment (including intermediate input data and user code, etc.) from cloud to your local machine to trace and debug failed jobs with the same runtime and exact input data in cloud.</span><span class="sxs-lookup"><span data-stu-id="66144-108">ADL Tools for Visual Studio offers a feature called **Failed Vertex Debug**, using which you can easily clone failed environment (including intermediate input data and user code, etc.) from cloud to your local machine to trace and debug failed jobs with the same runtime and exact input data in cloud.</span></span>

<span data-ttu-id="66144-109">The following video demonstrates **Failed Vertex Debug** in ADL Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66144-109">The following video demonstrates **Failed Vertex Debug** in ADL Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>
>

> [!NOTE]
> <span data-ttu-id="66144-110">Visual Studio may hang or crash if you don’t have the following two windows upgrades: [Microsoft Visual C++ 2015 Redistributable Update 2](https://www.microsoft.com/download/details.aspx?id=51682), [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410&wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="66144-110">Visual Studio may hang or crash if you don’t have the following two windows upgrades: [Microsoft Visual C++ 2015 Redistributable Update 2](https://www.microsoft.com/download/details.aspx?id=51682), [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410&wa=wsignin1.0).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="66144-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="66144-111">Prerequisites</span></span>
* <span data-ttu-id="66144-112">Have gone through the [Get started](data-lake-analytics-data-lake-tools-get-started.md) article.</span><span class="sxs-lookup"><span data-stu-id="66144-112">Have gone through the [Get started](data-lake-analytics-data-lake-tools-get-started.md) article.</span></span>

## <a name="download-failed-vertex-to-local"></a><span data-ttu-id="66144-113">Download failed vertex to local</span><span class="sxs-lookup"><span data-stu-id="66144-113">Download failed vertex to local</span></span>

<span data-ttu-id="66144-114">When opening a failed job in ADL Tools for Visual Studio, you will get an alert.</span><span class="sxs-lookup"><span data-stu-id="66144-114">When opening a failed job in ADL Tools for Visual Studio, you will get an alert.</span></span> <span data-ttu-id="66144-115">The detailed error messages will be shown in error tab and the yellow alert bar on the top of the window.</span><span class="sxs-lookup"><span data-stu-id="66144-115">The detailed error messages will be shown in error tab and the yellow alert bar on the top of the window.</span></span>

1. <span data-ttu-id="66144-116">Click **Download** to download all the required resources and input streams.</span><span class="sxs-lookup"><span data-stu-id="66144-116">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="66144-117">Click **Retry** if the download failed.</span><span class="sxs-lookup"><span data-stu-id="66144-117">Click **Retry** if the download failed.</span></span> 

2. <span data-ttu-id="66144-118">Click **Open** after the download completed to generate local debugging environment.</span><span class="sxs-lookup"><span data-stu-id="66144-118">Click **Open** after the download completed to generate local debugging environment.</span></span> <span data-ttu-id="66144-119">A new Visual Studio instance with a debugging solution will be created and opened automatically.</span><span class="sxs-lookup"><span data-stu-id="66144-119">A new Visual Studio instance with a debugging solution will be created and opened automatically.</span></span> 

3. <span data-ttu-id="66144-120">Debugging steps are little different between failed jobs with code behind and assemblies.</span><span class="sxs-lookup"><span data-stu-id="66144-120">Debugging steps are little different between failed jobs with code behind and assemblies.</span></span>

    - [<span data-ttu-id="66144-121">Debug job failed with code behind</span><span class="sxs-lookup"><span data-stu-id="66144-121">Debug job failed with code behind</span></span>](#debug-job-failed-with-code-behind)
    - [<span data-ttu-id="66144-122">Debug job failed with assemblies</span><span class="sxs-lookup"><span data-stu-id="66144-122">Debug job failed with assemblies</span></span>](#debug-job-failed-with-assemblies)

![Azure Data Lake Analytics U-SQL debug visual studio download vertex](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="66144-124">Debug job failed with code behind</span><span class="sxs-lookup"><span data-stu-id="66144-124">Debug job failed with code behind</span></span>

<span data-ttu-id="66144-125">If you wrote user defined code in code behind file (usually named as "Script.usql.cs" in U-SQL project) and then the U-SQL job failed, the source code will be imported automatically to the generated debugging solution, you can just use Visual Studio based debugging experience (watch, variables, etc.) to troubleshoot the problem.</span><span class="sxs-lookup"><span data-stu-id="66144-125">If you wrote user defined code in code behind file (usually named as "Script.usql.cs" in U-SQL project) and then the U-SQL job failed, the source code will be imported automatically to the generated debugging solution, you can just use Visual Studio based debugging experience (watch, variables, etc.) to troubleshoot the problem.</span></span> 

<span data-ttu-id="66144-126">Before debugging, make sure you checked **Common Language Runtime Exceptions** in Exception Settings window (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="66144-126">Before debugging, make sure you checked **Common Language Runtime Exceptions** in Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL debug visual studio setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="66144-128">Press **F5**, the code behind code will run automatically untill it is stopped by an exception.</span><span class="sxs-lookup"><span data-stu-id="66144-128">Press **F5**, the code behind code will run automatically untill it is stopped by an exception.</span></span>

2. <span data-ttu-id="66144-129">Open **ADLTool_Codebehind.usql.cs** in project, set breakpoints then press F5 to debug code step by step.</span><span class="sxs-lookup"><span data-stu-id="66144-129">Open **ADLTool_Codebehind.usql.cs** in project, set breakpoints then press F5 to debug code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL debug exception](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="66144-131">Debug job failed with assemblies</span><span class="sxs-lookup"><span data-stu-id="66144-131">Debug job failed with assemblies</span></span>

<span data-ttu-id="66144-132">If you use registered assemblies in U-SQL script, the system can't get the source code automatically, you need to do some configurations before debugging user defined code, that is, you must add the source code of assemblies to the automatically generated solution.</span><span class="sxs-lookup"><span data-stu-id="66144-132">If you use registered assemblies in U-SQL script, the system can't get the source code automatically, you need to do some configurations before debugging user defined code, that is, you must add the source code of assemblies to the automatically generated solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="66144-133">Configure the solution</span><span class="sxs-lookup"><span data-stu-id="66144-133">Configure the solution</span></span>

1. <span data-ttu-id="66144-134">Right click **Solution 'VertexDebug'** > **Add** > **Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span><span class="sxs-lookup"><span data-stu-id="66144-134">Right click **Solution 'VertexDebug'** > **Add** > **Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL debug add project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="66144-136">Right click **LocalVertexHost** > **Properties** in solution, copy **Working Directory** path.</span><span class="sxs-lookup"><span data-stu-id="66144-136">Right click **LocalVertexHost** > **Properties** in solution, copy **Working Directory** path.</span></span>

3. <span data-ttu-id="66144-137">Right Click **assembly source code project** > **Properties**, select **Build** tab at left, paste the path copied in 2 to **Output** > **Output path**.</span><span class="sxs-lookup"><span data-stu-id="66144-137">Right Click **assembly source code project** > **Properties**, select **Build** tab at left, paste the path copied in 2 to **Output** > **Output path**.</span></span>  

    ![Azure Data Lake Analytics U-SQL debug set pdb path](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="66144-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span><span class="sxs-lookup"><span data-stu-id="66144-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="66144-140">Start debug</span><span class="sxs-lookup"><span data-stu-id="66144-140">Start debug</span></span>

1. <span data-ttu-id="66144-141">Right click **assembly source code project** > **Rebuild** to output pdb files to LocalVertexHost working directory.</span><span class="sxs-lookup"><span data-stu-id="66144-141">Right click **assembly source code project** > **Rebuild** to output pdb files to LocalVertexHost working directory.</span></span>

2. <span data-ttu-id="66144-142">Press **F5**, the project will run automatically untill it is stopped by an exception.</span><span class="sxs-lookup"><span data-stu-id="66144-142">Press **F5**, the project will run automatically untill it is stopped by an exception.</span></span> <span data-ttu-id="66144-143">You may see the following message for the first time which you can ignore.</span><span class="sxs-lookup"><span data-stu-id="66144-143">You may see the following message for the first time which you can ignore.</span></span> <span data-ttu-id="66144-144">It can take up to one minute to get to the debug screen.</span><span class="sxs-lookup"><span data-stu-id="66144-144">It can take up to one minute to get to the debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL debug visual studio warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="66144-146">Open you source code and set breakpoints, then press **F5** to debug code step by step.</span><span class="sxs-lookup"><span data-stu-id="66144-146">Open you source code and set breakpoints, then press **F5** to debug code step by step.</span></span>

<span data-ttu-id="66144-147">You can also use other Visual Studio based debugging experiences (watch, variables, etc.) to debug the problem.</span><span class="sxs-lookup"><span data-stu-id="66144-147">You can also use other Visual Studio based debugging experiences (watch, variables, etc.) to debug the problem.</span></span> 

<span data-ttu-id="66144-148">**Note that** you need to rebuild the assembly source code project every time you modify the code to bring the new pdb files into effect.</span><span class="sxs-lookup"><span data-stu-id="66144-148">**Note that** you need to rebuild the assembly source code project every time you modify the code to bring the new pdb files into effect.</span></span>

<span data-ttu-id="66144-149">After the debug has been completed successfully, the output window shows the following massage:</span><span class="sxs-lookup"><span data-stu-id="66144-149">After the debug has been completed successfully, the output window shows the following massage:</span></span>

    The Program ‘LocalVertexHost.exe’ has exited with code 0 (0x0).

![Azure Data Lake Analytics U-SQL debug succeed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="66144-151">Resubmit the job</span><span class="sxs-lookup"><span data-stu-id="66144-151">Resubmit the job</span></span>
<span data-ttu-id="66144-152">After you have completed debugging, you can resubmit the failed job.</span><span class="sxs-lookup"><span data-stu-id="66144-152">After you have completed debugging, you can resubmit the failed job.</span></span>

1. <span data-ttu-id="66144-153">Register new .dll assemblies to your ADLA database.</span><span class="sxs-lookup"><span data-stu-id="66144-153">Register new .dll assemblies to your ADLA database.</span></span>

    1. <span data-ttu-id="66144-154">From Server Explorer/Cloud Explorer, expand **ADLA account** > **Databases** node.</span><span class="sxs-lookup"><span data-stu-id="66144-154">From Server Explorer/Cloud Explorer, expand **ADLA account** > **Databases** node.</span></span>
    2. <span data-ttu-id="66144-155">Right-click **Assemblies** to Register assemblies.</span><span class="sxs-lookup"><span data-stu-id="66144-155">Right-click **Assemblies** to Register assemblies.</span></span> 
    3. <span data-ttu-id="66144-156">Register your new .dll assemblies to the ADLA database.</span><span class="sxs-lookup"><span data-stu-id="66144-156">Register your new .dll assemblies to the ADLA database.</span></span>
    <span data-ttu-id="66144-157">![Azure Data Lake Analytics U-SQL debug register assembly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="66144-157">![Azure Data Lake Analytics U-SQL debug register assembly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
2. <span data-ttu-id="66144-158">Or copy your C# code back to script.usql.cs--C# code behind file.</span><span class="sxs-lookup"><span data-stu-id="66144-158">Or copy your C# code back to script.usql.cs--C# code behind file.</span></span>
3. <span data-ttu-id="66144-159">Resubmit your job.</span><span class="sxs-lookup"><span data-stu-id="66144-159">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66144-160">Next Steps</span><span class="sxs-lookup"><span data-stu-id="66144-160">Next Steps</span></span>

* [<span data-ttu-id="66144-161">U-SQL programmability guide</span><span class="sxs-lookup"><span data-stu-id="66144-161">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
* [<span data-ttu-id="66144-162">Develop U-SQL User defined operators for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="66144-162">Develop U-SQL User defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
* [<span data-ttu-id="66144-163">Tutorial: Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="66144-163">Tutorial: Get started with Azure Data Lake Analytics U-SQL language</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="66144-164">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66144-164">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)










