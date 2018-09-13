---
title: Scale U-SQL local run and test with Azure Data Lake U-SQL SDK | Microsoft Docs
description: Learn how to use Azure Data Lake U-SQL SDK to scale U-SQL jobs local run and test with command line and programming interfaces on your local workstation.
services: data-lake-analytics
documentationcenter: ''
author: ''
manager: ''
editor: ''
ms.assetid: ''
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 8d7663343922d4f422146b2132985d7df9615e77
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563567"
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="3b4eb-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="3b4eb-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="3b4eb-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="3b4eb-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="3b4eb-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="3b4eb-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="3b4eb-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="3b4eb-109">Install Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="3b4eb-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="3b4eb-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need to make sure you have dependencies as follows.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="3b4eb-111">Dependencies</span><span class="sxs-lookup"><span data-stu-id="3b4eb-111">Dependencies</span></span>

<span data-ttu-id="3b4eb-112">The Data Lake U-SQL SDK requires the following dependencies:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-112">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="3b4eb-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="3b4eb-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="3b4eb-115">There are two ways to get CppSDK:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-115">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="3b4eb-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="3b4eb-117">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-117">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="3b4eb-118">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-118">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="3b4eb-119">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-119">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="3b4eb-120">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-120">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools for Visual Studio local-run Windows 10 SDK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="3b4eb-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="3b4eb-123">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-123">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="3b4eb-124">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-124">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="3b4eb-125">You need to specify the CppSDK path for it.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-125">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="3b4eb-126">You can either copy the files to another location or use it as is.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-126">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="3b4eb-127">Understand basic concepts</span><span class="sxs-lookup"><span data-stu-id="3b4eb-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="3b4eb-128">Data root</span><span class="sxs-lookup"><span data-stu-id="3b4eb-128">Data root</span></span>

<span data-ttu-id="3b4eb-129">The data-root folder is a "local store" for the local compute account.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-129">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="3b4eb-130">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-130">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="3b4eb-131">Switching to a different data-root folder is just like switching to a different store account.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-131">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="3b4eb-132">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-132">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="3b4eb-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="3b4eb-134">The data-root folder is used to:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-134">The data-root folder is used to:</span></span>

- <span data-ttu-id="3b4eb-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="3b4eb-136">Look up the input and output paths that are defined as relative paths in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-136">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="3b4eb-137">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-137">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="3b4eb-138">File path in U-SQL</span><span class="sxs-lookup"><span data-stu-id="3b4eb-138">File path in U-SQL</span></span>

<span data-ttu-id="3b4eb-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="3b4eb-140">The relative path is relative to the specified data-root folder path.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-140">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="3b4eb-141">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-141">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="3b4eb-142">Here are some examples of relative paths and their equivalent absolute paths.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="3b4eb-143">In these examples, C:\LocalRunDataRoot is the data-root folder.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-143">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="3b4eb-144">Relative path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-144">Relative path</span></span>|<span data-ttu-id="3b4eb-145">Absolute path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="3b4eb-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="3b4eb-146">/abc/def/input.csv</span></span> |<span data-ttu-id="3b4eb-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="3b4eb-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="3b4eb-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="3b4eb-148">abc/def/input.csv</span></span>  |<span data-ttu-id="3b4eb-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="3b4eb-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="3b4eb-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="3b4eb-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="3b4eb-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="3b4eb-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="3b4eb-152">Working directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-152">Working directory</span></span>

<span data-ttu-id="3b4eb-153">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-153">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="3b4eb-154">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-154">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="3b4eb-155">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-155">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="3b4eb-156">Directory/file</span><span class="sxs-lookup"><span data-stu-id="3b4eb-156">Directory/file</span></span>|<span data-ttu-id="3b4eb-157">Directory/file</span><span class="sxs-lookup"><span data-stu-id="3b4eb-157">Directory/file</span></span>|<span data-ttu-id="3b4eb-158">Directory/file</span><span class="sxs-lookup"><span data-stu-id="3b4eb-158">Directory/file</span></span>|<span data-ttu-id="3b4eb-159">Definition</span><span class="sxs-lookup"><span data-stu-id="3b4eb-159">Definition</span></span>|<span data-ttu-id="3b4eb-160">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="3b4eb-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="3b4eb-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="3b4eb-162">Hash string of runtime version</span><span class="sxs-lookup"><span data-stu-id="3b4eb-162">Hash string of runtime version</span></span>|<span data-ttu-id="3b4eb-163">Shadow copy of runtime files needed for local execution</span><span class="sxs-lookup"><span data-stu-id="3b4eb-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="3b4eb-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="3b4eb-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="3b4eb-165">Script name + hash string of script path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-165">Script name + hash string of script path</span></span>|<span data-ttu-id="3b4eb-166">Compilation outputs and execution step logging</span><span class="sxs-lookup"><span data-stu-id="3b4eb-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="3b4eb-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="3b4eb-167">\_script\_.abr</span></span>|<span data-ttu-id="3b4eb-168">Compiler output</span><span class="sxs-lookup"><span data-stu-id="3b4eb-168">Compiler output</span></span>|<span data-ttu-id="3b4eb-169">Algebra file</span><span class="sxs-lookup"><span data-stu-id="3b4eb-169">Algebra file</span></span>|
| | |<span data-ttu-id="3b4eb-170">\_ScopeCodeGen\_.\*</span><span class="sxs-lookup"><span data-stu-id="3b4eb-170">\_ScopeCodeGen\_.\*</span></span>|<span data-ttu-id="3b4eb-171">Compiler output</span><span class="sxs-lookup"><span data-stu-id="3b4eb-171">Compiler output</span></span>|<span data-ttu-id="3b4eb-172">Generated managed code</span><span class="sxs-lookup"><span data-stu-id="3b4eb-172">Generated managed code</span></span>|
| | |<span data-ttu-id="3b4eb-173">\_ScopeCodeGenEngine\_.\*</span><span class="sxs-lookup"><span data-stu-id="3b4eb-173">\_ScopeCodeGenEngine\_.\*</span></span>|<span data-ttu-id="3b4eb-174">Compiler output</span><span class="sxs-lookup"><span data-stu-id="3b4eb-174">Compiler output</span></span>|<span data-ttu-id="3b4eb-175">Generated native code</span><span class="sxs-lookup"><span data-stu-id="3b4eb-175">Generated native code</span></span>|
| | |<span data-ttu-id="3b4eb-176">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="3b4eb-176">referenced assemblies</span></span>|<span data-ttu-id="3b4eb-177">Assembly reference</span><span class="sxs-lookup"><span data-stu-id="3b4eb-177">Assembly reference</span></span>|<span data-ttu-id="3b4eb-178">Referenced assembly files</span><span class="sxs-lookup"><span data-stu-id="3b4eb-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="3b4eb-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="3b4eb-179">deployed_resources</span></span>|<span data-ttu-id="3b4eb-180">Resource deployment</span><span class="sxs-lookup"><span data-stu-id="3b4eb-180">Resource deployment</span></span>|<span data-ttu-id="3b4eb-181">Resource deployment files</span><span class="sxs-lookup"><span data-stu-id="3b4eb-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="3b4eb-182">xxxxxxxx.xxx[1..n]\_\*.\*</span><span class="sxs-lookup"><span data-stu-id="3b4eb-182">xxxxxxxx.xxx[1..n]\_\*.\*</span></span>|<span data-ttu-id="3b4eb-183">Execution log</span><span class="sxs-lookup"><span data-stu-id="3b4eb-183">Execution log</span></span>|<span data-ttu-id="3b4eb-184">Log of execution steps</span><span class="sxs-lookup"><span data-stu-id="3b4eb-184">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="3b4eb-185">Use the SDK from the command line</span><span class="sxs-lookup"><span data-stu-id="3b4eb-185">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="3b4eb-186">Command-line interface of the helper application</span><span class="sxs-lookup"><span data-stu-id="3b4eb-186">Command-line interface of the helper application</span></span>

<span data-ttu-id="3b4eb-187">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-187">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="3b4eb-188">Note that both the command and the argument switches are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-188">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="3b4eb-189">To invoke it:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-189">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="3b4eb-190">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-190">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="3b4eb-191">In the help information:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-191">In the help information:</span></span>

-  <span data-ttu-id="3b4eb-192">**Command** gives the command’s name.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-192">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="3b4eb-193">**Required Argument** lists arguments that must be supplied.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="3b4eb-194">**Optional Argument** lists arguments that are optional, with default values.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="3b4eb-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="3b4eb-196">Return value and logging</span><span class="sxs-lookup"><span data-stu-id="3b4eb-196">Return value and logging</span></span>

<span data-ttu-id="3b4eb-197">The helper application returns **0** for success and **-1** for failure.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-197">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="3b4eb-198">By default, the helper sends all messages to the current console.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-198">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="3b4eb-199">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-199">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="3b4eb-200">Environment variable configuring</span><span class="sxs-lookup"><span data-stu-id="3b4eb-200">Environment variable configuring</span></span>

<span data-ttu-id="3b4eb-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="3b4eb-202">You can both set the argument in command-line or set environment variable for them.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-202">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="3b4eb-203">Set the **SCOPE_CPP_SDK** environment variable.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-203">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="3b4eb-204">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-204">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="3b4eb-205">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-205">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="3b4eb-206">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-206">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="3b4eb-207">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-207">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="3b4eb-208">This argument overwrites your default CppSDK environment variable.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="3b4eb-209">Set the **LOCALRUN_DATAROOT** environment variable.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-209">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="3b4eb-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="3b4eb-211">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-211">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="3b4eb-212">This argument overwrites your default data-root environment variable.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="3b4eb-213">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-213">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="3b4eb-214">SDK command line usage samples</span><span class="sxs-lookup"><span data-stu-id="3b4eb-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="3b4eb-215">Compile and run</span><span class="sxs-lookup"><span data-stu-id="3b4eb-215">Compile and run</span></span>

<span data-ttu-id="3b4eb-216">The **run** command is used to compile the script and then execute compiled results.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-216">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="3b4eb-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="3b4eb-218">The following are optional arguments for **run**:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-218">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="3b4eb-219">Argument</span><span class="sxs-lookup"><span data-stu-id="3b4eb-219">Argument</span></span>|<span data-ttu-id="3b4eb-220">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-220">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="3b4eb-221">-CodeBehind [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-221">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="3b4eb-222">The script has .cs code behind</span><span class="sxs-lookup"><span data-stu-id="3b4eb-222">The script has .cs code behind</span></span>|
|<span data-ttu-id="3b4eb-223">-CppSDK [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-223">-CppSDK [default value '']</span></span>|<span data-ttu-id="3b4eb-224">CppSDK Directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-224">CppSDK Directory</span></span>|
|<span data-ttu-id="3b4eb-225">-DataRoot [default value 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-225">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="3b4eb-226">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span><span class="sxs-lookup"><span data-stu-id="3b4eb-226">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="3b4eb-227">-MessageOut [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-227">-MessageOut [default value '']</span></span>|<span data-ttu-id="3b4eb-228">Dump messages on console to a file</span><span class="sxs-lookup"><span data-stu-id="3b4eb-228">Dump messages on console to a file</span></span>|
|<span data-ttu-id="3b4eb-229">-Parallel [default value '1']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-229">-Parallel [default value '1']</span></span>|<span data-ttu-id="3b4eb-230">Run the plan with the specified parallelism</span><span class="sxs-lookup"><span data-stu-id="3b4eb-230">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="3b4eb-231">-References [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-231">-References [default value '']</span></span>|<span data-ttu-id="3b4eb-232">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span><span class="sxs-lookup"><span data-stu-id="3b4eb-232">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="3b4eb-233">-UdoRedirect [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-233">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="3b4eb-234">Generate Udo assembly redirect config</span><span class="sxs-lookup"><span data-stu-id="3b4eb-234">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="3b4eb-235">-UseDatabase [default value 'master']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-235">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="3b4eb-236">Database to use for code behind temporary assembly registration</span><span class="sxs-lookup"><span data-stu-id="3b4eb-236">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="3b4eb-237">-Verbose [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-237">-Verbose [default value 'False']</span></span>|<span data-ttu-id="3b4eb-238">Show detailed outputs from runtime</span><span class="sxs-lookup"><span data-stu-id="3b4eb-238">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="3b4eb-239">-WorkDir [default value 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-239">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="3b4eb-240">Directory for compiler usage and outputs</span><span class="sxs-lookup"><span data-stu-id="3b4eb-240">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="3b4eb-241">-RunScopeCEP [default value '0']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-241">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="3b4eb-242">ScopeCEP mode to use</span><span class="sxs-lookup"><span data-stu-id="3b4eb-242">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="3b4eb-243">-ScopeCEPTempPath [default value 'temp']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-243">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="3b4eb-244">Temp path to use for streaming data</span><span class="sxs-lookup"><span data-stu-id="3b4eb-244">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="3b4eb-245">-OptFlags [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-245">-OptFlags [default value '']</span></span>|<span data-ttu-id="3b4eb-246">Comma-separated list of optimizer flags</span><span class="sxs-lookup"><span data-stu-id="3b4eb-246">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="3b4eb-247">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-247">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="3b4eb-248">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-248">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="3b4eb-249">Compile a U-SQL script</span><span class="sxs-lookup"><span data-stu-id="3b4eb-249">Compile a U-SQL script</span></span>

<span data-ttu-id="3b4eb-250">The **compile** command is used to compile a U-SQL script to executables.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-250">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="3b4eb-251">The following are optional arguments for **compile**:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-251">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="3b4eb-252">Argument</span><span class="sxs-lookup"><span data-stu-id="3b4eb-252">Argument</span></span>|<span data-ttu-id="3b4eb-253">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-253">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="3b4eb-254">-CodeBehind [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-254">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="3b4eb-255">The script has .cs code behind</span><span class="sxs-lookup"><span data-stu-id="3b4eb-255">The script has .cs code behind</span></span>|
| <span data-ttu-id="3b4eb-256">-CppSDK [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-256">-CppSDK [default value '']</span></span>|<span data-ttu-id="3b4eb-257">CppSDK Directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-257">CppSDK Directory</span></span>|
| <span data-ttu-id="3b4eb-258">-DataRoot [default value 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-258">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="3b4eb-259">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span><span class="sxs-lookup"><span data-stu-id="3b4eb-259">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="3b4eb-260">-MessageOut [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-260">-MessageOut [default value '']</span></span>|<span data-ttu-id="3b4eb-261">Dump messages on console to a file</span><span class="sxs-lookup"><span data-stu-id="3b4eb-261">Dump messages on console to a file</span></span>|
| <span data-ttu-id="3b4eb-262">-References [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-262">-References [default value '']</span></span>|<span data-ttu-id="3b4eb-263">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span><span class="sxs-lookup"><span data-stu-id="3b4eb-263">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="3b4eb-264">-Shallow [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-264">-Shallow [default value 'False']</span></span>|<span data-ttu-id="3b4eb-265">Shallow compile</span><span class="sxs-lookup"><span data-stu-id="3b4eb-265">Shallow compile</span></span>|
| <span data-ttu-id="3b4eb-266">-UdoRedirect [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-266">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="3b4eb-267">Generate Udo assembly redirect config</span><span class="sxs-lookup"><span data-stu-id="3b4eb-267">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="3b4eb-268">-UseDatabase [default value 'master']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-268">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="3b4eb-269">Database to use for code behind temporary assembly registration</span><span class="sxs-lookup"><span data-stu-id="3b4eb-269">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="3b4eb-270">-WorkDir [default value 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-270">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="3b4eb-271">Directory for compiler usage and outputs</span><span class="sxs-lookup"><span data-stu-id="3b4eb-271">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="3b4eb-272">-RunScopeCEP [default value '0']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-272">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="3b4eb-273">ScopeCEP mode to use</span><span class="sxs-lookup"><span data-stu-id="3b4eb-273">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="3b4eb-274">-ScopeCEPTempPath [default value 'temp']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-274">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="3b4eb-275">Temp path to use for streaming data</span><span class="sxs-lookup"><span data-stu-id="3b4eb-275">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="3b4eb-276">-OptFlags [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-276">-OptFlags [default value '']</span></span>|<span data-ttu-id="3b4eb-277">Comma-separated list of optimizer flags</span><span class="sxs-lookup"><span data-stu-id="3b4eb-277">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="3b4eb-278">Here are some usage examples.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-278">Here are some usage examples.</span></span>

<span data-ttu-id="3b4eb-279">Compile a U-SQL script:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-279">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="3b4eb-280">Compile a U-SQL script and set the data-root folder.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-280">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="3b4eb-281">Note that this will overwrite the set environment variable.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-281">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="3b4eb-282">Compile a U-SQL script and set a working directory, reference assembly, and database:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-282">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="3b4eb-283">Execute compiled results</span><span class="sxs-lookup"><span data-stu-id="3b4eb-283">Execute compiled results</span></span>

<span data-ttu-id="3b4eb-284">The **execute** command is used to execute compiled results.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-284">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="3b4eb-285">The following are optional arguments for **execute**:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-285">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="3b4eb-286">Argument</span><span class="sxs-lookup"><span data-stu-id="3b4eb-286">Argument</span></span>|<span data-ttu-id="3b4eb-287">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-287">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="3b4eb-288">-DataRoot [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-288">-DataRoot [default value '']</span></span>|<span data-ttu-id="3b4eb-289">Data root for metadata execution.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-289">Data root for metadata execution.</span></span> <span data-ttu-id="3b4eb-290">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-290">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="3b4eb-291">-MessageOut [default value '']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-291">-MessageOut [default value '']</span></span>|<span data-ttu-id="3b4eb-292">Dump messages on the console to a file.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-292">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="3b4eb-293">-Parallel [default value '1']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-293">-Parallel [default value '1']</span></span>|<span data-ttu-id="3b4eb-294">Indicator to run the generated local-run steps with the specified parallelism level.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-294">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="3b4eb-295">-Verbose [default value 'False']</span><span class="sxs-lookup"><span data-stu-id="3b4eb-295">-Verbose [default value 'False']</span></span>|<span data-ttu-id="3b4eb-296">Indicator to show detailed outputs from runtime.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-296">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="3b4eb-297">Here's a usage example:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-297">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="3b4eb-298">Use the SDK with programming interfaces</span><span class="sxs-lookup"><span data-stu-id="3b4eb-298">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="3b4eb-299">The programming interfaces are all located in the LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-299">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="3b4eb-300">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-300">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="3b4eb-301">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-301">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="3b4eb-302">Step 1: Create C# unit test project and configuration</span><span class="sxs-lookup"><span data-stu-id="3b4eb-302">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="3b4eb-303">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-303">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="3b4eb-304">Add LocalRunHelper.exe as a reference for the project.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-304">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="3b4eb-305">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-305">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL SDK Add Reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="3b4eb-307">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-307">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="3b4eb-308">You can set that through Project Property > Build > Platform target.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-308">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL SDK Configure x64 Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="3b4eb-310">Make sure to set your test environment as x64.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-310">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="3b4eb-311">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-311">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL SDK Configure x64 Test Environment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="3b4eb-313">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-313">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="3b4eb-314">Step 2: Create U-SQL script test case</span><span class="sxs-lookup"><span data-stu-id="3b4eb-314">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="3b4eb-315">Below is the sample code for U-SQL script test.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-315">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="3b4eb-316">For testing, you need to prepare scripts, input files and expected output files.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-316">For testing, you need to prepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget to close MessageOutput to get logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="3b4eb-317">Programming interfaces in LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="3b4eb-317">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="3b4eb-318">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-318">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="3b4eb-319">**Constructor**</span><span class="sxs-lookup"><span data-stu-id="3b4eb-319">**Constructor**</span></span>

<span data-ttu-id="3b4eb-320">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="3b4eb-320">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="3b4eb-321">Parameter</span><span class="sxs-lookup"><span data-stu-id="3b4eb-321">Parameter</span></span>|<span data-ttu-id="3b4eb-322">Type</span><span class="sxs-lookup"><span data-stu-id="3b4eb-322">Type</span></span>|<span data-ttu-id="3b4eb-323">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-323">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="3b4eb-324">messageOutput</span><span class="sxs-lookup"><span data-stu-id="3b4eb-324">messageOutput</span></span>|<span data-ttu-id="3b4eb-325">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="3b4eb-325">System.IO.TextWriter</span></span>|<span data-ttu-id="3b4eb-326">for output messages, set to null to use Console</span><span class="sxs-lookup"><span data-stu-id="3b4eb-326">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="3b4eb-327">**Properties**</span><span class="sxs-lookup"><span data-stu-id="3b4eb-327">**Properties**</span></span>

|<span data-ttu-id="3b4eb-328">Property</span><span class="sxs-lookup"><span data-stu-id="3b4eb-328">Property</span></span>|<span data-ttu-id="3b4eb-329">Type</span><span class="sxs-lookup"><span data-stu-id="3b4eb-329">Type</span></span>|<span data-ttu-id="3b4eb-330">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-330">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="3b4eb-331">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="3b4eb-331">AlgebraPath</span></span>|<span data-ttu-id="3b4eb-332">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-332">string</span></span>|<span data-ttu-id="3b4eb-333">The path to algebra file (algebra file is one of the compilation results)</span><span class="sxs-lookup"><span data-stu-id="3b4eb-333">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="3b4eb-334">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="3b4eb-334">CodeBehindReferences</span></span>|<span data-ttu-id="3b4eb-335">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-335">string</span></span>|<span data-ttu-id="3b4eb-336">If the script has additional code behind references, specify the paths separated with ';'</span><span class="sxs-lookup"><span data-stu-id="3b4eb-336">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="3b4eb-337">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-337">CppSdkDir</span></span>|<span data-ttu-id="3b4eb-338">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-338">string</span></span>|<span data-ttu-id="3b4eb-339">CppSDK directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-339">CppSDK directory</span></span>|
|<span data-ttu-id="3b4eb-340">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-340">CurrentDir</span></span>|<span data-ttu-id="3b4eb-341">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-341">string</span></span>|<span data-ttu-id="3b4eb-342">Current directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-342">Current directory</span></span>|
|<span data-ttu-id="3b4eb-343">DataRoot</span><span class="sxs-lookup"><span data-stu-id="3b4eb-343">DataRoot</span></span>|<span data-ttu-id="3b4eb-344">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-344">string</span></span>|<span data-ttu-id="3b4eb-345">Data root path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-345">Data root path</span></span>|
|<span data-ttu-id="3b4eb-346">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="3b4eb-346">DebuggerMailPath</span></span>|<span data-ttu-id="3b4eb-347">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-347">string</span></span>|<span data-ttu-id="3b4eb-348">The path to debugger mailslot</span><span class="sxs-lookup"><span data-stu-id="3b4eb-348">The path to debugger mailslot</span></span>|
|<span data-ttu-id="3b4eb-349">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="3b4eb-349">GenerateUdoRedirect</span></span>|<span data-ttu-id="3b4eb-350">bool</span><span class="sxs-lookup"><span data-stu-id="3b4eb-350">bool</span></span>|<span data-ttu-id="3b4eb-351">If we want to generate assembly loading redirection override config</span><span class="sxs-lookup"><span data-stu-id="3b4eb-351">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="3b4eb-352">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="3b4eb-352">HasCodeBehind</span></span>|<span data-ttu-id="3b4eb-353">bool</span><span class="sxs-lookup"><span data-stu-id="3b4eb-353">bool</span></span>|<span data-ttu-id="3b4eb-354">If the script has code behind</span><span class="sxs-lookup"><span data-stu-id="3b4eb-354">If the script has code behind</span></span>|
|<span data-ttu-id="3b4eb-355">InputDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-355">InputDir</span></span>|<span data-ttu-id="3b4eb-356">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-356">string</span></span>|<span data-ttu-id="3b4eb-357">Directory for input data</span><span class="sxs-lookup"><span data-stu-id="3b4eb-357">Directory for input data</span></span>|
|<span data-ttu-id="3b4eb-358">MessagePath</span><span class="sxs-lookup"><span data-stu-id="3b4eb-358">MessagePath</span></span>|<span data-ttu-id="3b4eb-359">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-359">string</span></span>|<span data-ttu-id="3b4eb-360">Message dump file path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-360">Message dump file path</span></span>|
|<span data-ttu-id="3b4eb-361">OutputDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-361">OutputDir</span></span>|<span data-ttu-id="3b4eb-362">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-362">string</span></span>|<span data-ttu-id="3b4eb-363">Directory for output data</span><span class="sxs-lookup"><span data-stu-id="3b4eb-363">Directory for output data</span></span>|
|<span data-ttu-id="3b4eb-364">Parallelism</span><span class="sxs-lookup"><span data-stu-id="3b4eb-364">Parallelism</span></span>|<span data-ttu-id="3b4eb-365">int</span><span class="sxs-lookup"><span data-stu-id="3b4eb-365">int</span></span>|<span data-ttu-id="3b4eb-366">Parallelism to run the algebra</span><span class="sxs-lookup"><span data-stu-id="3b4eb-366">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="3b4eb-367">ParentPid</span><span class="sxs-lookup"><span data-stu-id="3b4eb-367">ParentPid</span></span>|<span data-ttu-id="3b4eb-368">int</span><span class="sxs-lookup"><span data-stu-id="3b4eb-368">int</span></span>|<span data-ttu-id="3b4eb-369">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span><span class="sxs-lookup"><span data-stu-id="3b4eb-369">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="3b4eb-370">ResultPath</span><span class="sxs-lookup"><span data-stu-id="3b4eb-370">ResultPath</span></span>|<span data-ttu-id="3b4eb-371">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-371">string</span></span>|<span data-ttu-id="3b4eb-372">Result dump file path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-372">Result dump file path</span></span>|
|<span data-ttu-id="3b4eb-373">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-373">RuntimeDir</span></span>|<span data-ttu-id="3b4eb-374">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-374">string</span></span>|<span data-ttu-id="3b4eb-375">Runtime directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-375">Runtime directory</span></span>|
|<span data-ttu-id="3b4eb-376">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="3b4eb-376">ScriptPath</span></span>|<span data-ttu-id="3b4eb-377">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-377">string</span></span>|<span data-ttu-id="3b4eb-378">Where to find the script</span><span class="sxs-lookup"><span data-stu-id="3b4eb-378">Where to find the script</span></span>|
|<span data-ttu-id="3b4eb-379">Shallow</span><span class="sxs-lookup"><span data-stu-id="3b4eb-379">Shallow</span></span>|<span data-ttu-id="3b4eb-380">bool</span><span class="sxs-lookup"><span data-stu-id="3b4eb-380">bool</span></span>|<span data-ttu-id="3b4eb-381">Shallow compile or not</span><span class="sxs-lookup"><span data-stu-id="3b4eb-381">Shallow compile or not</span></span>|
|<span data-ttu-id="3b4eb-382">TempDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-382">TempDir</span></span>|<span data-ttu-id="3b4eb-383">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-383">string</span></span>|<span data-ttu-id="3b4eb-384">Temp directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-384">Temp directory</span></span>|
|<span data-ttu-id="3b4eb-385">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="3b4eb-385">UseDataBase</span></span>|<span data-ttu-id="3b4eb-386">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-386">string</span></span>|<span data-ttu-id="3b4eb-387">Specify the database to use for code behind temporary assembly registration, master by default</span><span class="sxs-lookup"><span data-stu-id="3b4eb-387">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="3b4eb-388">WorkDir</span><span class="sxs-lookup"><span data-stu-id="3b4eb-388">WorkDir</span></span>|<span data-ttu-id="3b4eb-389">string</span><span class="sxs-lookup"><span data-stu-id="3b4eb-389">string</span></span>|<span data-ttu-id="3b4eb-390">Preferred working directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-390">Preferred working directory</span></span>|


<span data-ttu-id="3b4eb-391">**Method**</span><span class="sxs-lookup"><span data-stu-id="3b4eb-391">**Method**</span></span>

|<span data-ttu-id="3b4eb-392">Method</span><span class="sxs-lookup"><span data-stu-id="3b4eb-392">Method</span></span>|<span data-ttu-id="3b4eb-393">Description</span><span class="sxs-lookup"><span data-stu-id="3b4eb-393">Description</span></span>|<span data-ttu-id="3b4eb-394">Return</span><span class="sxs-lookup"><span data-stu-id="3b4eb-394">Return</span></span>|<span data-ttu-id="3b4eb-395">Parameter</span><span class="sxs-lookup"><span data-stu-id="3b4eb-395">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="3b4eb-396">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="3b4eb-396">public bool DoCompile()</span></span>|<span data-ttu-id="3b4eb-397">Compile the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="3b4eb-397">Compile the U-SQL script</span></span>|<span data-ttu-id="3b4eb-398">True on success</span><span class="sxs-lookup"><span data-stu-id="3b4eb-398">True on success</span></span>| |
|<span data-ttu-id="3b4eb-399">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="3b4eb-399">public bool DoExec()</span></span>|<span data-ttu-id="3b4eb-400">Execute the compiled result</span><span class="sxs-lookup"><span data-stu-id="3b4eb-400">Execute the compiled result</span></span>|<span data-ttu-id="3b4eb-401">True on success</span><span class="sxs-lookup"><span data-stu-id="3b4eb-401">True on success</span></span>| |
|<span data-ttu-id="3b4eb-402">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="3b4eb-402">public bool DoRun()</span></span>|<span data-ttu-id="3b4eb-403">Run the U-SQL script (Compile + Execute)</span><span class="sxs-lookup"><span data-stu-id="3b4eb-403">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="3b4eb-404">True on success</span><span class="sxs-lookup"><span data-stu-id="3b4eb-404">True on success</span></span>| |
|<span data-ttu-id="3b4eb-405">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="3b4eb-405">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="3b4eb-406">Check if the given path is valid runtime path</span><span class="sxs-lookup"><span data-stu-id="3b4eb-406">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="3b4eb-407">True for valid</span><span class="sxs-lookup"><span data-stu-id="3b4eb-407">True for valid</span></span>|<span data-ttu-id="3b4eb-408">The path of runtime directory</span><span class="sxs-lookup"><span data-stu-id="3b4eb-408">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="3b4eb-409">FAQ about common issue</span><span class="sxs-lookup"><span data-stu-id="3b4eb-409">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="3b4eb-410">Error 1:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-410">Error 1:</span></span>
<span data-ttu-id="3b4eb-411">E_CSC_SYSTEM_INTERNAL: Internal error!</span><span class="sxs-lookup"><span data-stu-id="3b4eb-411">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="3b4eb-412">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-412">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="3b4eb-413">The specified module could not be found.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-413">The specified module could not be found.</span></span>

<span data-ttu-id="3b4eb-414">Please check the following:</span><span class="sxs-lookup"><span data-stu-id="3b4eb-414">Please check the following:</span></span>

- <span data-ttu-id="3b4eb-415">Make sure you have x64 environment.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-415">Make sure you have x64 environment.</span></span> <span data-ttu-id="3b4eb-416">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-416">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="3b4eb-417">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span><span class="sxs-lookup"><span data-stu-id="3b4eb-417">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b4eb-418">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b4eb-418">Next steps</span></span>

* <span data-ttu-id="3b4eb-419">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-419">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="3b4eb-420">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-420">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="3b4eb-421">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-421">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="3b4eb-422">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-422">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="3b4eb-423">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-423">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="3b4eb-424">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-424">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="3b4eb-425">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-425">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="3b4eb-426">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="3b4eb-426">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>




