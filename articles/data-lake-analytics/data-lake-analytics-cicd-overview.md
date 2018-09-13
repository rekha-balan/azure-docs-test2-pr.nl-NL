---
title: How to set up a CI/CD pipeline for Azure Data Lake Analytics
description: Learn how to set up continuous integration and continuous deployment for Azure Data Lake Analytics.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.topic: conceptual
ms.workload: big-data
ms.date: 07/03/2018
ms.openlocfilehash: 77675a89fdb203abca25cef02914bd2e30ee9e87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865659"
---
# <a name="how-to-set-up-a-cicd-pipeline-for-azure-data-lake-analytics"></a><span data-ttu-id="9bbbb-103">How to set up a CI/CD pipeline for Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9bbbb-103">How to set up a CI/CD pipeline for Azure Data Lake Analytics</span></span>  

<span data-ttu-id="9bbbb-104">In this article, you learn how to set up a continuous integration and deployment (CI/CD) pipeline for U-SQL jobs and U-SQL databases.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-104">In this article, you learn how to set up a continuous integration and deployment (CI/CD) pipeline for U-SQL jobs and U-SQL databases.</span></span>  

## <a name="use-cicd-for-u-sql-jobs"></a><span data-ttu-id="9bbbb-105">Use CI/CD for U-SQL jobs</span><span class="sxs-lookup"><span data-stu-id="9bbbb-105">Use CI/CD for U-SQL jobs</span></span>

<span data-ttu-id="9bbbb-106">Azure Data Lake Tools for Visual Studio provides the U-SQL project type that helps you organize U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-106">Azure Data Lake Tools for Visual Studio provides the U-SQL project type that helps you organize U-SQL scripts.</span></span> <span data-ttu-id="9bbbb-107">Using the U-SQL project to manage your U-SQL code makes further CI/CD scenarios easy.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-107">Using the U-SQL project to manage your U-SQL code makes further CI/CD scenarios easy.</span></span>

## <a name="build-a-u-sql-project"></a><span data-ttu-id="9bbbb-108">Build a U-SQL project</span><span class="sxs-lookup"><span data-stu-id="9bbbb-108">Build a U-SQL project</span></span>

<span data-ttu-id="9bbbb-109">A U-SQL project can be built with the Microsoft Build Engine (MSBuild) by passing corresponding parameters.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-109">A U-SQL project can be built with the Microsoft Build Engine (MSBuild) by passing corresponding parameters.</span></span> <span data-ttu-id="9bbbb-110">Follow the steps in this article to set up a build process for a U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-110">Follow the steps in this article to set up a build process for a U-SQL project.</span></span>

### <a name="project-migration"></a><span data-ttu-id="9bbbb-111">Project migration</span><span class="sxs-lookup"><span data-stu-id="9bbbb-111">Project migration</span></span>

<span data-ttu-id="9bbbb-112">Before you set up a build task for a U-SQL project, make sure you have the latest version of the U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-112">Before you set up a build task for a U-SQL project, make sure you have the latest version of the U-SQL project.</span></span> <span data-ttu-id="9bbbb-113">Open the U-SQL project file in your editor and verify that you have these import items:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-113">Open the U-SQL project file in your editor and verify that you have these import items:</span></span>

```   
<!-- check for SDK Build target in current path then in USQLSDKPath-->
<Import Project="UsqlSDKBuild.targets" Condition="Exists('UsqlSDKBuild.targets')" />
<Import Project="$(USQLSDKPath)\UsqlSDKBuild.targets" Condition="!Exists('UsqlSDKBuild.targets') And '$(USQLSDKPath)' != '' And Exists('$(USQLSDKPath)\UsqlSDKBuild.targets')" />
``` 

<span data-ttu-id="9bbbb-114">If not, you have two options to migrate the project:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-114">If not, you have two options to migrate the project:</span></span>

- <span data-ttu-id="9bbbb-115">Option 1: Change the old import item to the preceding one.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-115">Option 1: Change the old import item to the preceding one.</span></span>
- <span data-ttu-id="9bbbb-116">Option 2: Open the old project in the Azure Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-116">Option 2: Open the old project in the Azure Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="9bbbb-117">Use a version newer than 2.3.3000.0.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-117">Use a version newer than 2.3.3000.0.</span></span> <span data-ttu-id="9bbbb-118">The old project template will be upgraded automatically to the newest version.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-118">The old project template will be upgraded automatically to the newest version.</span></span> <span data-ttu-id="9bbbb-119">New projects created with versions newer than 2.3.3000.0 use the new template.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-119">New projects created with versions newer than 2.3.3000.0 use the new template.</span></span>

### <a name="get-nuget"></a><span data-ttu-id="9bbbb-120">Get NuGet</span><span class="sxs-lookup"><span data-stu-id="9bbbb-120">Get NuGet</span></span>

<span data-ttu-id="9bbbb-121">MSBuild doesn't provide built-in support for U-SQL projects.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-121">MSBuild doesn't provide built-in support for U-SQL projects.</span></span> <span data-ttu-id="9bbbb-122">To get this support, you need to add a reference for your solution to the [Microsoft.Azure.DataLake.USQL.SDK](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) NuGet package that adds the required language service.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-122">To get this support, you need to add a reference for your solution to the [Microsoft.Azure.DataLake.USQL.SDK](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) NuGet package that adds the required language service.</span></span>

<span data-ttu-id="9bbbb-123">To add the NuGet package reference, right-click the solution in Visual Studio Solution Explorer and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-123">To add the NuGet package reference, right-click the solution in Visual Studio Solution Explorer and choose **Manage NuGet Packages**.</span></span> <span data-ttu-id="9bbbb-124">Or you can add a file called `packages.config` in the solution folder and put the following contents into it:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-124">Or you can add a file called `packages.config` in the solution folder and put the following contents into it:</span></span>

```xml 
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.Azure.DataLake.USQL.SDK" version="1.3.180620" targetFramework="net452" />
</packages>
``` 

### <a name="manage-u-sql-database-references"></a><span data-ttu-id="9bbbb-125">Manage U-SQL database references</span><span class="sxs-lookup"><span data-stu-id="9bbbb-125">Manage U-SQL database references</span></span>

<span data-ttu-id="9bbbb-126">U-SQL scripts in a U-SQL project might have query statements for U-SQL database objects.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-126">U-SQL scripts in a U-SQL project might have query statements for U-SQL database objects.</span></span> <span data-ttu-id="9bbbb-127">In that case, you need to reference the corresponding U-SQL database project that includes the objects' definition before you build the U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-127">In that case, you need to reference the corresponding U-SQL database project that includes the objects' definition before you build the U-SQL project.</span></span> <span data-ttu-id="9bbbb-128">An example is when you query a U-SQL table or reference an assembly.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-128">An example is when you query a U-SQL table or reference an assembly.</span></span> 

<span data-ttu-id="9bbbb-129">Learn more about [U-SQL database project](data-lake-analytics-data-lake-tools-develop-usql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-129">Learn more about [U-SQL database project](data-lake-analytics-data-lake-tools-develop-usql-database.md).</span></span>

>[!NOTE]
><span data-ttu-id="9bbbb-130">U-SQL database project is currently in public preview.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-130">U-SQL database project is currently in public preview.</span></span> <span data-ttu-id="9bbbb-131">If you have DROP statement in the project, the build fails.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-131">If you have DROP statement in the project, the build fails.</span></span> <span data-ttu-id="9bbbb-132">The DROP statement will be allowed soon.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-132">The DROP statement will be allowed soon.</span></span>
>

### <a name="build-a-u-sql-project-with-the-msbuild-command-line"></a><span data-ttu-id="9bbbb-133">Build a U-SQL project with the MSBuild command line</span><span class="sxs-lookup"><span data-stu-id="9bbbb-133">Build a U-SQL project with the MSBuild command line</span></span>

<span data-ttu-id="9bbbb-134">First migrate the project and get the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-134">First migrate the project and get the NuGet package.</span></span> <span data-ttu-id="9bbbb-135">Then call the standard MSBuild command line with the following additional arguments to build your U-SQL project:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-135">Then call the standard MSBuild command line with the following additional arguments to build your U-SQL project:</span></span> 

``` 
msbuild USQLBuild.usqlproj /p:USQLSDKPath=packages\Microsoft.Azure.DataLake.USQL.SDK.1.3.180615\build\runtime;USQLTargetType=SyntaxCheck;DataRoot=datarootfolder;/p:EnableDeployment=true
``` 

<span data-ttu-id="9bbbb-136">The arguments definition and values are as follows:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-136">The arguments definition and values are as follows:</span></span>

* <span data-ttu-id="9bbbb-137">**USQLSDKPath=<U-SQL Nuget package>\build\runtime**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-137">**USQLSDKPath=<U-SQL Nuget package>\build\runtime**.</span></span> <span data-ttu-id="9bbbb-138">This parameter refers to the installation path of the NuGet package for the U-SQL language service.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-138">This parameter refers to the installation path of the NuGet package for the U-SQL language service.</span></span>
* <span data-ttu-id="9bbbb-139">**USQLTargetType=Merge or SyntaxCheck**:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-139">**USQLTargetType=Merge or SyntaxCheck**:</span></span>
    * <span data-ttu-id="9bbbb-140">**Merge**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-140">**Merge**.</span></span> <span data-ttu-id="9bbbb-141">Merge mode compiles code-behind files.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-141">Merge mode compiles code-behind files.</span></span> <span data-ttu-id="9bbbb-142">Examples are **.cs**, **.py**, and **.r** files.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-142">Examples are **.cs**, **.py**, and **.r** files.</span></span> <span data-ttu-id="9bbbb-143">It inlines the resulting user-defined code library into the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-143">It inlines the resulting user-defined code library into the U-SQL script.</span></span> <span data-ttu-id="9bbbb-144">Examples are a dll binary, Python, or R code.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-144">Examples are a dll binary, Python, or R code.</span></span>
    * <span data-ttu-id="9bbbb-145">**SyntaxCheck**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-145">**SyntaxCheck**.</span></span> <span data-ttu-id="9bbbb-146">SyntaxCheck mode first merges code-behind files into the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-146">SyntaxCheck mode first merges code-behind files into the U-SQL script.</span></span> <span data-ttu-id="9bbbb-147">Then it compiles the U-SQL script to validate your code.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-147">Then it compiles the U-SQL script to validate your code.</span></span>
* <span data-ttu-id="9bbbb-148">**DataRoot=<DataRoot path>**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-148">**DataRoot=<DataRoot path>**.</span></span> <span data-ttu-id="9bbbb-149">DataRoot is needed only for SyntaxCheck mode.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-149">DataRoot is needed only for SyntaxCheck mode.</span></span> <span data-ttu-id="9bbbb-150">When it builds the script with SyntaxCheck mode, MSBuild checks the references to database objects in the script.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-150">When it builds the script with SyntaxCheck mode, MSBuild checks the references to database objects in the script.</span></span> <span data-ttu-id="9bbbb-151">Before building, set up a matching local environment that contains the referenced objects from the U-SQL database in the build machine's DataRoot folder.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-151">Before building, set up a matching local environment that contains the referenced objects from the U-SQL database in the build machine's DataRoot folder.</span></span> <span data-ttu-id="9bbbb-152">You can also manage these database dependencies by [referencing a U-SQL database project](data-lake-analytics-data-lake-tools-develop-usql-database.md#reference-a-u-sql-database-project).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-152">You can also manage these database dependencies by [referencing a U-SQL database project](data-lake-analytics-data-lake-tools-develop-usql-database.md#reference-a-u-sql-database-project).</span></span> <span data-ttu-id="9bbbb-153">MSBuild only checks database object references, not files.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-153">MSBuild only checks database object references, not files.</span></span>
* <span data-ttu-id="9bbbb-154">**EnableDeployment=true** or **false**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-154">**EnableDeployment=true** or **false**.</span></span> <span data-ttu-id="9bbbb-155">EnableDeployment indicates if it's allowed to deploy referenced U-SQL databases during the build process.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-155">EnableDeployment indicates if it's allowed to deploy referenced U-SQL databases during the build process.</span></span> <span data-ttu-id="9bbbb-156">If you reference a U-SQL database project and consume the database objects in your U-SQL script, set this parameter to **true**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-156">If you reference a U-SQL database project and consume the database objects in your U-SQL script, set this parameter to **true**.</span></span>

### <a name="continuous-integration-with-azure-devops"></a><span data-ttu-id="9bbbb-157">Continuous integration with Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="9bbbb-157">Continuous integration with Azure DevOps</span></span>

<span data-ttu-id="9bbbb-158">In addition to the command line, you can also use the Visual Studio Build or an MSBuild task to build U-SQL projects in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-158">In addition to the command line, you can also use the Visual Studio Build or an MSBuild task to build U-SQL projects in Azure DevOps.</span></span> <span data-ttu-id="9bbbb-159">To set up a build pipeline, make sure to add two tasks in the build pipeline: a NuGet restore task and an MSBuild task.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-159">To set up a build pipeline, make sure to add two tasks in the build pipeline: a NuGet restore task and an MSBuild task.</span></span>

![MSBuild task for a U-SQL project](./media/data-lake-analytics-cicd-overview/data-lake-analytics-set-vsts-msbuild-task.png) 

1.  <span data-ttu-id="9bbbb-161">Add a NuGet restore task to get the solution-referenced NuGet package that includes `Azure.DataLake.USQL.SDK`, so that MSBuild can find the U-SQL language targets.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-161">Add a NuGet restore task to get the solution-referenced NuGet package that includes `Azure.DataLake.USQL.SDK`, so that MSBuild can find the U-SQL language targets.</span></span> <span data-ttu-id="9bbbb-162">Set **Advanced** > **Destination directory** to `$(Build.SourcesDirectory)/packages` if you want to use the MSBuild arguments sample directly in step 2.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-162">Set **Advanced** > **Destination directory** to `$(Build.SourcesDirectory)/packages` if you want to use the MSBuild arguments sample directly in step 2.</span></span>

    ![NuGet restore task for a U-SQL project](./media/data-lake-analytics-cicd-overview/data-lake-analytics-set-vsts-nuget-task.png)

2.  <span data-ttu-id="9bbbb-164">Set MSBuild arguments in Visual Studio build tools or in an MSBuild task as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-164">Set MSBuild arguments in Visual Studio build tools or in an MSBuild task as shown in the following example.</span></span> <span data-ttu-id="9bbbb-165">Or you can define variables for these arguments in the Azure DevOps build pipeline.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-165">Or you can define variables for these arguments in the Azure DevOps build pipeline.</span></span>

    ![Define CI/CD MSBuild variables for a U-SQL project](./media/data-lake-analytics-cicd-overview/data-lake-analytics-set-vsts-msbuild-variables.png) 

    ```
    /p:USQLSDKPath=/p:USQLSDKPath=$(Build.SourcesDirectory)/packages/Microsoft.Azure.DataLake.USQL.SDK.1.3.180615/build/runtime /p:USQLTargetType=SyntaxCheck /p:DataRoot=$(Build.SourcesDirectory) /p:EnableDeployment=true
    ```

### <a name="u-sql-project-build-output"></a><span data-ttu-id="9bbbb-167">U-SQL project build output</span><span class="sxs-lookup"><span data-stu-id="9bbbb-167">U-SQL project build output</span></span>

<span data-ttu-id="9bbbb-168">After you run a build, all scripts in the U-SQL project are built and output to a zip file called `USQLProjectName.usqlpack`.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-168">After you run a build, all scripts in the U-SQL project are built and output to a zip file called `USQLProjectName.usqlpack`.</span></span> <span data-ttu-id="9bbbb-169">The folder structure in your project is kept in the zipped build output.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-169">The folder structure in your project is kept in the zipped build output.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9bbbb-170">Code-behind files for each U-SQL script will be merged as an inline statement to the script build output.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-170">Code-behind files for each U-SQL script will be merged as an inline statement to the script build output.</span></span>
>

## <a name="test-u-sql-scripts"></a><span data-ttu-id="9bbbb-171">Test U-SQL scripts</span><span class="sxs-lookup"><span data-stu-id="9bbbb-171">Test U-SQL scripts</span></span>

<span data-ttu-id="9bbbb-172">Azure Data Lake provides test projects for U-SQL scripts and C# UDO/UDAG/UDF:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-172">Azure Data Lake provides test projects for U-SQL scripts and C# UDO/UDAG/UDF:</span></span>
* <span data-ttu-id="9bbbb-173">Learn how to [add test cases for U-SQL scripts and extended C# code](data-lake-analytics-cicd-test.md#test-u-sql-scripts).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-173">Learn how to [add test cases for U-SQL scripts and extended C# code](data-lake-analytics-cicd-test.md#test-u-sql-scripts).</span></span>
* <span data-ttu-id="9bbbb-174">Learn how to [run test cases in Azure DevOps](data-lake-analytics-cicd-test.md#run-test-cases-in-azure-devops).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-174">Learn how to [run test cases in Azure DevOps](data-lake-analytics-cicd-test.md#run-test-cases-in-azure-devops).</span></span>

## <a name="deploy-a-u-sql-job"></a><span data-ttu-id="9bbbb-175">Deploy a U-SQL job</span><span class="sxs-lookup"><span data-stu-id="9bbbb-175">Deploy a U-SQL job</span></span>

<span data-ttu-id="9bbbb-176">After you verify code through the build and test process, you can submit U-SQL jobs directly from Azure DevOps through an Azure PowerShell task.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-176">After you verify code through the build and test process, you can submit U-SQL jobs directly from Azure DevOps through an Azure PowerShell task.</span></span> <span data-ttu-id="9bbbb-177">You can also deploy the script to Azure Data Lake Store or Azure Blob storage and [run the scheduled jobs through Azure Data Factory](https://docs.microsoft.com/azure/data-factory/transform-data-using-data-lake-analytics).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-177">You can also deploy the script to Azure Data Lake Store or Azure Blob storage and [run the scheduled jobs through Azure Data Factory](https://docs.microsoft.com/azure/data-factory/transform-data-using-data-lake-analytics).</span></span>

### <a name="submit-u-sql-jobs-through-azure-devops"></a><span data-ttu-id="9bbbb-178">Submit U-SQL jobs through Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="9bbbb-178">Submit U-SQL jobs through Azure DevOps</span></span>

<span data-ttu-id="9bbbb-179">The build output of the U-SQL project is a zip file called **USQLProjectName.usqlpack**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-179">The build output of the U-SQL project is a zip file called **USQLProjectName.usqlpack**.</span></span> <span data-ttu-id="9bbbb-180">The zip file includes all U-SQL scripts in the project.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-180">The zip file includes all U-SQL scripts in the project.</span></span> <span data-ttu-id="9bbbb-181">You can use the [Azure PowerShell task](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-powershell?view=vsts) in Azure DevOps with the following sample PowerShell script to submit U-SQL jobs directly from the Azure Pipelines.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-181">You can use the [Azure PowerShell task](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-powershell?view=vsts) in Azure DevOps with the following sample PowerShell script to submit U-SQL jobs directly from the Azure Pipelines.</span></span>

```powershell
<#
    This script can be used to submit U-SQL Jobs with given U-SQL project build output(.usqlpack file).
    This will unzip the U-SQL project build output, and submit all scripts one-by-one.

    Note: the code behind file for each U-SQL script will be merged into the built U-SQL script in build output.
          
    Example :
        USQLJobSubmission.ps1 -ADLAAccountName "myadlaaccount" -ArtifactsRoot "C:\USQLProject\bin\debug\" -DegreeOfParallelism 2
#>

param(
    [Parameter(Mandatory=$true)][string]$ADLAAccountName, # ADLA account name to submit U-SQL jobs
    [Parameter(Mandatory=$true)][string]$ArtifactsRoot, # Root folder of U-SQL project build output
    [Parameter(Mandatory=$false)][string]$DegreeOfParallelism = 1
)

function Unzip($USQLPackfile, $UnzipOutput)
{
    $USQLPackfileZip = Rename-Item -Path $USQLPackfile -NewName $([System.IO.Path]::ChangeExtension($USQLPackfile, ".zip")) -Force -PassThru
    Expand-Archive -Path $USQLPackfileZip -DestinationPath $UnzipOutput -Force
    Rename-Item -Path $USQLPackfileZip -NewName $([System.IO.Path]::ChangeExtension($USQLPackfileZip, ".usqlpack")) -Force
}

## Get U-SQL scripts in U-SQL project build output(.usqlpack file)
Function GetUsqlFiles()
{

    $USQLPackfiles = Get-ChildItem -Path $ArtifactsRoot -Include *.usqlpack -File -Recurse -ErrorAction SilentlyContinue

    $UnzipOutput = Join-Path $ArtifactsRoot -ChildPath "UnzipUSQLScripts"

    foreach ($USQLPackfile in $USQLPackfiles)
    {
        Unzip $USQLPackfile $UnzipOutput
    }

    $USQLFiles = Get-ChildItem -Path $UnzipOutput -Include *.usql -File -Recurse -ErrorAction SilentlyContinue

    return $USQLFiles
}

## Submit U-SQL scripts to ADLA account one-by-one
Function SubmitAnalyticsJob()
{
    $usqlFiles = GetUsqlFiles

    Write-Output "$($usqlFiles.Count) jobs to be submitted..."

    # Submit each usql script and wait for completion before moving ahead.
    foreach ($usqlFile in $usqlFiles)
    {
        $scriptName = "[Release].[$([System.IO.Path]::GetFileNameWithoutExtension($usqlFile.fullname))]"

        Write-Output "Submitting job for '{$usqlFile}'"

        $jobToSubmit = Submit-AzureRmDataLakeAnalyticsJob -Account $ADLAAccountName -Name $scriptName -ScriptPath $usqlFile -DegreeOfParallelism $DegreeOfParallelism
        
        LogJobInformation $jobToSubmit
        
        Write-Output "Waiting for job to complete. Job ID:'{$($jobToSubmit.JobId)}', Name: '$($jobToSubmit.Name)' "
        $jobResult = Wait-AzureRmDataLakeAnalyticsJob -Account $ADLAAccountName -JobId $jobToSubmit.JobId  
        LogJobInformation $jobResult
    }
}

Function LogJobInformation($jobInfo)
{
    Write-Output "************************************************************************"
    Write-Output ([string]::Format("Job Id: {0}", $(DefaultIfNull $jobInfo.JobId)))
    Write-Output ([string]::Format("Job Name: {0}", $(DefaultIfNull $jobInfo.Name)))
    Write-Output ([string]::Format("Job State: {0}", $(DefaultIfNull $jobInfo.State)))
    Write-Output ([string]::Format("Job Started at: {0}", $(DefaultIfNull  $jobInfo.StartTime)))
    Write-Output ([string]::Format("Job Ended at: {0}", $(DefaultIfNull  $jobInfo.EndTime)))
    Write-Output ([string]::Format("Job Result: {0}", $(DefaultIfNull $jobInfo.Result)))
    Write-Output "************************************************************************"
}

Function DefaultIfNull($item)
{
    if ($item -ne $null)
    {
        return $item
    }
    return ""
}

Function Main()
{
    Write-Output ([string]::Format("ADLA account: {0}", $ADLAAccountName))
    Write-Output ([string]::Format("Root folde for usqlpack: {0}", $ArtifactsRoot))
    Write-Output ([string]::Format("AU count: {0}", $DegreeOfParallelism))

    Write-Output "Starting USQL script deployment..."
    
    SubmitAnalyticsJob

    Write-Output "Finished deployment..."
}

Main
```

### <a name="deploy-u-sql-jobs-through-azure-data-factory"></a><span data-ttu-id="9bbbb-182">Deploy U-SQL jobs through Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9bbbb-182">Deploy U-SQL jobs through Azure Data Factory</span></span>

<span data-ttu-id="9bbbb-183">You can submit U-SQL jobs directly from Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-183">You can submit U-SQL jobs directly from Azure DevOps.</span></span> <span data-ttu-id="9bbbb-184">Or you can upload the built scripts to Azure Data Lake Store or Azure Blob storage and [run the scheduled jobs through Azure Data Factory](https://docs.microsoft.com/azure/data-factory/transform-data-using-data-lake-analytics).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-184">Or you can upload the built scripts to Azure Data Lake Store or Azure Blob storage and [run the scheduled jobs through Azure Data Factory](https://docs.microsoft.com/azure/data-factory/transform-data-using-data-lake-analytics).</span></span>

<span data-ttu-id="9bbbb-185">Use the [Azure PowerShell task](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-powershell?view=vsts) in Azure DevOps with the following sample PowerShell script to upload the U-SQL scripts to an Azure Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-185">Use the [Azure PowerShell task](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-powershell?view=vsts) in Azure DevOps with the following sample PowerShell script to upload the U-SQL scripts to an Azure Data Lake Store account:</span></span>

```powershell
<#
    This script can be used to upload U-SQL files to ADLS with given U-SQL project build output(.usqlpack file).
    This will unzip the U-SQL project build output, and upload all scripts to ADLS one-by-one.
          
    Example :
        FileUpload.ps1 -ADLSName "myadlsaccount" -ArtifactsRoot "C:\USQLProject\bin\debug\"
#>

param(
    [Parameter(Mandatory=$true)][string]$ADLSName, # ADLS account name to upload U-SQL scripts
    [Parameter(Mandatory=$true)][string]$ArtifactsRoot, # Root folder of U-SQL project build output
    [Parameter(Mandatory=$false)][string]$DesitinationFolder = "USQLScriptSource" # Desitination folder in ADLS
)

Function UploadResources()
{
    Write-Host "************************************************************************"
    Write-Host "Uploading files to $ADLSName"
    Write-Host "***********************************************************************"

    $usqlScripts = GetUsqlFiles

    $files = @(get-childitem $usqlScripts -recurse)
    foreach($file in $files)
    {
        Write-Host "Uploading file: $($file.Name)"
        Import-AzureRmDataLakeStoreItem -AccountName $ADLSName -Path $file.FullName -Destination "/$(Join-Path $DesitinationFolder $file)" -Force
    }
}

function Unzip($USQLPackfile, $UnzipOutput)
{
    $USQLPackfileZip = Rename-Item -Path $USQLPackfile -NewName $([System.IO.Path]::ChangeExtension($USQLPackfile, ".zip")) -Force -PassThru
    Expand-Archive -Path $USQLPackfileZip -DestinationPath $UnzipOutput -Force
    Rename-Item -Path $USQLPackfileZip -NewName $([System.IO.Path]::ChangeExtension($USQLPackfileZip, ".usqlpack")) -Force
}

Function GetUsqlFiles()
{

    $USQLPackfiles = Get-ChildItem -Path $ArtifactsRoot -Include *.usqlpack -File -Recurse -ErrorAction SilentlyContinue

    $UnzipOutput = Join-Path $ArtifactsRoot -ChildPath "UnzipUSQLScripts"

    foreach ($USQLPackfile in $USQLPackfiles)
    {
        Unzip $USQLPackfile $UnzipOutput
    }

    return Get-ChildItem -Path $UnzipOutput -Include *.usql -File -Recurse -ErrorAction SilentlyContinue
}

UploadResources
```

## <a name="cicd-for-a-u-sql-database"></a><span data-ttu-id="9bbbb-186">CI/CD for a U-SQL database</span><span class="sxs-lookup"><span data-stu-id="9bbbb-186">CI/CD for a U-SQL database</span></span>

<span data-ttu-id="9bbbb-187">Azure Data Lake Tools for Visual Studio provides U-SQL database project templates that help you develop, manage, and deploy U-SQL databases.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-187">Azure Data Lake Tools for Visual Studio provides U-SQL database project templates that help you develop, manage, and deploy U-SQL databases.</span></span> <span data-ttu-id="9bbbb-188">Learn more about a [U-SQL database project](data-lake-analytics-data-lake-tools-develop-usql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-188">Learn more about a [U-SQL database project](data-lake-analytics-data-lake-tools-develop-usql-database.md).</span></span>

## <a name="build-u-sql-database-project"></a><span data-ttu-id="9bbbb-189">Build U-SQL database project</span><span class="sxs-lookup"><span data-stu-id="9bbbb-189">Build U-SQL database project</span></span>

### <a name="get-the-nuget-package"></a><span data-ttu-id="9bbbb-190">Get the NuGet package</span><span class="sxs-lookup"><span data-stu-id="9bbbb-190">Get the NuGet package</span></span>

<span data-ttu-id="9bbbb-191">MSBuild doesn't provide built-in support for U-SQL database projects.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-191">MSBuild doesn't provide built-in support for U-SQL database projects.</span></span> <span data-ttu-id="9bbbb-192">To get this ability, you need to add a reference for your solution to the [Microsoft.Azure.DataLake.USQL.SDK](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) NuGet package that adds the required language service.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-192">To get this ability, you need to add a reference for your solution to the [Microsoft.Azure.DataLake.USQL.SDK](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) NuGet package that adds the required language service.</span></span>

<span data-ttu-id="9bbbb-193">To add the NuGet package reference, right-click the solution in Visual Studio Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-193">To add the NuGet package reference, right-click the solution in Visual Studio Solution Explorer.</span></span> <span data-ttu-id="9bbbb-194">Choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-194">Choose **Manage NuGet Packages**.</span></span> <span data-ttu-id="9bbbb-195">Then search for and install the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-195">Then search for and install the NuGet package.</span></span> <span data-ttu-id="9bbbb-196">Or you can add a file called **packages.config** in the solution folder and put the following contents into it:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-196">Or you can add a file called **packages.config** in the solution folder and put the following contents into it:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.Azure.DataLake.USQL.SDK" version="1.3.180615" targetFramework="net452" />
</packages>
```

### <a name="build-u-sql-a-database-project-with-the-msbuild-command-line"></a><span data-ttu-id="9bbbb-197">Build U-SQL a database project with the MSBuild command line</span><span class="sxs-lookup"><span data-stu-id="9bbbb-197">Build U-SQL a database project with the MSBuild command line</span></span>

<span data-ttu-id="9bbbb-198">To build your U-SQL database project, call the standard MSBuild command line and pass the U-SQL SDK NuGet package reference as an additional argument.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-198">To build your U-SQL database project, call the standard MSBuild command line and pass the U-SQL SDK NuGet package reference as an additional argument.</span></span> <span data-ttu-id="9bbbb-199">See the following example:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-199">See the following example:</span></span> 

```
msbuild DatabaseProject.usqldbproj /p:USQLSDKPath=packages\Microsoft.Azure.DataLake.USQL.SDK.1.3.180615\build\runtime
```

<span data-ttu-id="9bbbb-200">The argument `USQLSDKPath=<U-SQL Nuget package>\build\runtime` refers to the install path of the NuGet package for the U-SQL language service.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-200">The argument `USQLSDKPath=<U-SQL Nuget package>\build\runtime` refers to the install path of the NuGet package for the U-SQL language service.</span></span>

### <a name="continuous-integration-with-azure-devops"></a><span data-ttu-id="9bbbb-201">Continuous integration with Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="9bbbb-201">Continuous integration with Azure DevOps</span></span>

<span data-ttu-id="9bbbb-202">In addition to the command line, you can use Visual Studio Build or an MSBuild task to build U-SQL database projects in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-202">In addition to the command line, you can use Visual Studio Build or an MSBuild task to build U-SQL database projects in Azure DevOps.</span></span> <span data-ttu-id="9bbbb-203">To set up a build task, make sure to add two tasks in the build pipeline: a NuGet restore task and an MSBuild task.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-203">To set up a build task, make sure to add two tasks in the build pipeline: a NuGet restore task and an MSBuild task.</span></span>

   ![CI/CD MSBuild task for a U-SQL project](./media/data-lake-analytics-cicd-overview/data-lake-analytics-set-vsts-msbuild-task.png) 


1.  <span data-ttu-id="9bbbb-205">Add a NuGet restore task to get the solution-referenced NuGet package, which includes `Azure.DataLake.USQL.SDK`, so that MSBuild can find the U-SQL language targets.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-205">Add a NuGet restore task to get the solution-referenced NuGet package, which includes `Azure.DataLake.USQL.SDK`, so that MSBuild can find the U-SQL language targets.</span></span> <span data-ttu-id="9bbbb-206">Set **Advanced** > **Destination directory** to `$(Build.SourcesDirectory)/packages` if you want to use the MSBuild arguments sample directly in step 2.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-206">Set **Advanced** > **Destination directory** to `$(Build.SourcesDirectory)/packages` if you want to use the MSBuild arguments sample directly in step 2.</span></span>

    ![CI/CD NuGet task for a U-SQL project](./media/data-lake-analytics-cicd-overview/data-lake-analytics-set-vsts-nuget-task.png)

2.  <span data-ttu-id="9bbbb-208">Set MSBuild arguments in Visual Studio build tools or in an MSBuild task as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-208">Set MSBuild arguments in Visual Studio build tools or in an MSBuild task as shown in the following example.</span></span> <span data-ttu-id="9bbbb-209">Or you can define variables for these arguments in the Azure DevOps build pipeline.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-209">Or you can define variables for these arguments in the Azure DevOps build pipeline.</span></span>

   ![Define CI/CD MSBuild variables for a U-SQL database project](./media/data-lake-analytics-cicd-overview/data-lake-analytics-set-vsts-msbuild-variables-database-project.png) 

    ```
    /p:USQLSDKPath=/p:USQLSDKPath=$(Build.SourcesDirectory)/packages/Microsoft.Azure.DataLake.USQL.SDK.1.3.180615/build/runtime
    ```
 
### <a name="u-sql-database-project-build-output"></a><span data-ttu-id="9bbbb-211">U-SQL database project build output</span><span class="sxs-lookup"><span data-stu-id="9bbbb-211">U-SQL database project build output</span></span>

<span data-ttu-id="9bbbb-212">The build output for a U-SQL database project is a U-SQL database deployment package, named with the suffix `.usqldbpack`.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-212">The build output for a U-SQL database project is a U-SQL database deployment package, named with the suffix `.usqldbpack`.</span></span> <span data-ttu-id="9bbbb-213">The `.usqldbpack` package is a zip file that includes all DDL statements in a single U-SQL script in a DDL folder.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-213">The `.usqldbpack` package is a zip file that includes all DDL statements in a single U-SQL script in a DDL folder.</span></span> <span data-ttu-id="9bbbb-214">It includes all **.dlls** and additional files for assembly in a temp folder.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-214">It includes all **.dlls** and additional files for assembly in a temp folder.</span></span>

## <a name="test-table-valued-functions-and-stored-procedures"></a><span data-ttu-id="9bbbb-215">Test table-valued functions and stored procedures</span><span class="sxs-lookup"><span data-stu-id="9bbbb-215">Test table-valued functions and stored procedures</span></span>

<span data-ttu-id="9bbbb-216">Adding test cases for table-valued functions and stored procedures directly isn't currently supported.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-216">Adding test cases for table-valued functions and stored procedures directly isn't currently supported.</span></span> <span data-ttu-id="9bbbb-217">As a workaround, you can create a U-SQL project that has U-SQL scripts that call those functions and write test cases for them.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-217">As a workaround, you can create a U-SQL project that has U-SQL scripts that call those functions and write test cases for them.</span></span> <span data-ttu-id="9bbbb-218">Take the following steps to set up test cases for table-valued functions and stored procedures defined in the U-SQL database project:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-218">Take the following steps to set up test cases for table-valued functions and stored procedures defined in the U-SQL database project:</span></span>

1.  <span data-ttu-id="9bbbb-219">Create a U-SQL project for test purposes and write U-SQL scripts calling the table-valued functions and stored procedures.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-219">Create a U-SQL project for test purposes and write U-SQL scripts calling the table-valued functions and stored procedures.</span></span>
2.  <span data-ttu-id="9bbbb-220">Add a database reference to the U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-220">Add a database reference to the U-SQL project.</span></span> <span data-ttu-id="9bbbb-221">To get the table-valued function and stored procedure definition, you need to reference the database project that contains the DDL statement.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-221">To get the table-valued function and stored procedure definition, you need to reference the database project that contains the DDL statement.</span></span> <span data-ttu-id="9bbbb-222">Learn more about [database references](data-lake-analytics-data-lake-tools-develop-usql-database.md#reference-a-u-sql-database-project).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-222">Learn more about [database references](data-lake-analytics-data-lake-tools-develop-usql-database.md#reference-a-u-sql-database-project).</span></span>
3.  <span data-ttu-id="9bbbb-223">Add test cases for U-SQL scripts that call table-valued functions and stored procedures.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-223">Add test cases for U-SQL scripts that call table-valued functions and stored procedures.</span></span> <span data-ttu-id="9bbbb-224">Learn how to [add test cases for U-SQL scripts](data-lake-analytics-cicd-test.md#test-u-sql-scripts).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-224">Learn how to [add test cases for U-SQL scripts](data-lake-analytics-cicd-test.md#test-u-sql-scripts).</span></span>

## <a name="deploy-u-sql-database-through-azure-devops"></a><span data-ttu-id="9bbbb-225">Deploy U-SQL database through Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="9bbbb-225">Deploy U-SQL database through Azure DevOps</span></span>

<span data-ttu-id="9bbbb-226">`PackageDeploymentTool.exe` provides the programming and command-line interfaces that help deploy U-SQL database deployment packages, **.usqldbpack**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-226">`PackageDeploymentTool.exe` provides the programming and command-line interfaces that help deploy U-SQL database deployment packages, **.usqldbpack**.</span></span> <span data-ttu-id="9bbbb-227">The SDK is included in the [U-SQL SDK NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/), located at **build/runtime/PackageDeploymentTool.exe**.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-227">The SDK is included in the [U-SQL SDK NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/), located at **build/runtime/PackageDeploymentTool.exe**.</span></span> <span data-ttu-id="9bbbb-228">By using `PackageDeploymentTool.exe`, you can deploy U-SQL databases to both Azure Data Lake Analytics and local accounts.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-228">By using `PackageDeploymentTool.exe`, you can deploy U-SQL databases to both Azure Data Lake Analytics and local accounts.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9bbbb-229">PowerShell command-line support and Azure DevOps release task support for U-SQL database deployment is currently pending.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-229">PowerShell command-line support and Azure DevOps release task support for U-SQL database deployment is currently pending.</span></span>
>

<span data-ttu-id="9bbbb-230">Take the following steps to set up a database deployment task in Azure DevOps:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-230">Take the following steps to set up a database deployment task in Azure DevOps:</span></span>

1. <span data-ttu-id="9bbbb-231">Add a PowerShell Script task in a build or release pipeline and execute the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-231">Add a PowerShell Script task in a build or release pipeline and execute the following PowerShell script.</span></span> <span data-ttu-id="9bbbb-232">This task helps to get Azure SDK dependencies for `PackageDeploymentTool.exe` and `PackageDeploymentTool.exe`.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-232">This task helps to get Azure SDK dependencies for `PackageDeploymentTool.exe` and `PackageDeploymentTool.exe`.</span></span> <span data-ttu-id="9bbbb-233">You can set the **-AzureSDK** and **-DBDeploymentTool** parameters to load the dependencies and deployment tool to specific folders.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-233">You can set the **-AzureSDK** and **-DBDeploymentTool** parameters to load the dependencies and deployment tool to specific folders.</span></span> <span data-ttu-id="9bbbb-234">Pass the **-AzureSDK** path to `PackageDeploymentTool.exe` as the **-AzureSDKPath** parameter in step 2.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-234">Pass the **-AzureSDK** path to `PackageDeploymentTool.exe` as the **-AzureSDKPath** parameter in step 2.</span></span> 

    ```powershell
    <#
        This script is used for getting dependencies and SDKs for U-SQL database deployment.
        PowerShell command line support for deploying U-SQL database package(.usqldbpack file) will come soon.
        
        Example :
            GetUSQLDBDeploymentSDK.ps1 -AzureSDK "AzureSDKFolderPath" -DBDeploymentTool "DBDeploymentToolFolderPath"
    #>

    param (
        [string]$AzureSDK = "AzureSDK", # Folder to cache Azure SDK dependencies
        [string]$DBDeploymentTool = "DBDeploymentTool", # Folder to cache U-SQL database deployment tool
        [string]$workingfolder = "" # Folder to execute these command lines
    )

    if ([string]::IsNullOrEmpty($workingfolder))
    {
        $scriptpath = $MyInvocation.MyCommand.Path
        $workingfolder = Split-Path $scriptpath
    }
    cd $workingfolder

    echo "workingfolder=$workingfolder, outputfolder=$outputfolder"
    echo "Downloading required packages..."

    iwr https://www.nuget.org/api/v2/package/Microsoft.Azure.Management.DataLake.Analytics/3.2.3-preview -outf Microsoft.Azure.Management.DataLake.Analytics.3.2.3-preview.zip
    iwr https://www.nuget.org/api/v2/package/Microsoft.Azure.Management.DataLake.Store/2.3.3-preview -outf Microsoft.Azure.Management.DataLake.Store.2.3.3-preview.zip
    iwr https://www.nuget.org/api/v2/package/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.3 -outf Microsoft.IdentityModel.Clients.ActiveDirectory.2.28.3.zip
    iwr https://www.nuget.org/api/v2/package/Microsoft.Rest.ClientRuntime/2.3.11 -outf Microsoft.Rest.ClientRuntime.2.3.11.zip
    iwr https://www.nuget.org/api/v2/package/Microsoft.Rest.ClientRuntime.Azure/3.3.7 -outf Microsoft.Rest.ClientRuntime.Azure.3.3.7.zip
    iwr https://www.nuget.org/api/v2/package/Microsoft.Rest.ClientRuntime.Azure.Authentication/2.3.3 -outf Microsoft.Rest.ClientRuntime.Azure.Authentication.2.3.3.zip
    iwr https://www.nuget.org/api/v2/package/Newtonsoft.Json/6.0.8 -outf Newtonsoft.Json.6.0.8.zip
    iwr https://www.nuget.org/api/v2/package/Microsoft.Azure.DataLake.USQL.SDK/ -outf USQLSDK.zip

    echo "Extracting packages..."

    Expand-Archive Microsoft.Azure.Management.DataLake.Analytics.3.2.3-preview.zip -DestinationPath Microsoft.Azure.Management.DataLake.Analytics.3.2.3-preview -Force
    Expand-Archive Microsoft.Azure.Management.DataLake.Store.2.3.3-preview.zip -DestinationPath Microsoft.Azure.Management.DataLake.Store.2.3.3-preview -Force
    Expand-Archive Microsoft.IdentityModel.Clients.ActiveDirectory.2.28.3.zip -DestinationPath Microsoft.IdentityModel.Clients.ActiveDirectory.2.28.3 -Force
    Expand-Archive Microsoft.Rest.ClientRuntime.2.3.11.zip -DestinationPath Microsoft.Rest.ClientRuntime.2.3.11 -Force
    Expand-Archive Microsoft.Rest.ClientRuntime.Azure.3.3.7.zip -DestinationPath Microsoft.Rest.ClientRuntime.Azure.3.3.7 -Force
    Expand-Archive Microsoft.Rest.ClientRuntime.Azure.Authentication.2.3.3.zip -DestinationPath Microsoft.Rest.ClientRuntime.Azure.Authentication.2.3.3 -Force
    Expand-Archive Newtonsoft.Json.6.0.8.zip -DestinationPath Newtonsoft.Json.6.0.8 -Force
    Expand-Archive USQLSDK.zip -DestinationPath USQLSDK -Force

    echo "Copy required DLLs to output folder..."

    mkdir $AzureSDK -Force
    mkdir $DBDeploymentTool -Force
    copy Microsoft.Azure.Management.DataLake.Analytics.3.2.3-preview\lib\net452\*.dll $AzureSDK
    copy Microsoft.Azure.Management.DataLake.Store.2.3.3-preview\lib\net452\*.dll $AzureSDK
    copy Microsoft.IdentityModel.Clients.ActiveDirectory.2.28.3\lib\net45\*.dll $AzureSDK
    copy Microsoft.Rest.ClientRuntime.2.3.11\lib\net452\*.dll $AzureSDK
    copy Microsoft.Rest.ClientRuntime.Azure.3.3.7\lib\net452\*.dll $AzureSDK
    copy Microsoft.Rest.ClientRuntime.Azure.Authentication.2.3.3\lib\net452\*.dll $AzureSDK
    copy Newtonsoft.Json.6.0.8\lib\net45\*.dll $AzureSDK
    copy USQLSDK\build\runtime\*.* $DBDeploymentTool
    ```

2. <span data-ttu-id="9bbbb-235">Add a **Command-Line task** in a build or release pipeline and fill in the script by calling `PackageDeploymentTool.exe`.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-235">Add a **Command-Line task** in a build or release pipeline and fill in the script by calling `PackageDeploymentTool.exe`.</span></span> <span data-ttu-id="9bbbb-236">`PackageDeploymentTool.exe` is located under the defined **$DBDeploymentTool** folder.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-236">`PackageDeploymentTool.exe` is located under the defined **$DBDeploymentTool** folder.</span></span> <span data-ttu-id="9bbbb-237">The sample script is as follows:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-237">The sample script is as follows:</span></span> 

    * <span data-ttu-id="9bbbb-238">Deploy a U-SQL database locally:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-238">Deploy a U-SQL database locally:</span></span>

        ```
        PackageDeploymentTool.exe deploylocal -Package <package path> -Database <database name> -DataRoot <data root path>
        ```

    * <span data-ttu-id="9bbbb-239">Use interactive authentication mode to deploy a U-SQL database to an Azure Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-239">Use interactive authentication mode to deploy a U-SQL database to an Azure Data Lake Analytics account:</span></span>

        ```
        PackageDeploymentTool.exe deploycluster -Package <package path> -Database <database name> -Account <account name> -ResourceGroup <resource group name> -SubscriptionId <subscript id> -Tenant <tenant name> -AzureSDKPath <azure sdk path> -Interactive
        ```

    * <span data-ttu-id="9bbbb-240">Use **secrete** authentication to deploy a U-SQL database to an Azure Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-240">Use **secrete** authentication to deploy a U-SQL database to an Azure Data Lake Analytics account:</span></span>

        ```
        PackageDeploymentTool.exe deploycluster -Package <package path> -Database <database name> -Account <account name> -ResourceGroup <resource group name> -SubscriptionId <subscript id> -Tenant <tenant name> -ClientId <client id> -Secrete <secrete>
        ```

    * <span data-ttu-id="9bbbb-241">Use **certFile** authentication to deploy a U-SQL database to an Azure Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="9bbbb-241">Use **certFile** authentication to deploy a U-SQL database to an Azure Data Lake Analytics account:</span></span>

        ```
        PackageDeploymentTool.exe deploycluster -Package <package path> -Database <database name> -Account <account name> -ResourceGroup <resource group name> -SubscriptionId <subscript id> -Tenant <tenant name> -ClientId <client id> -Secrete <secrete> -CertFile <certFile>
        ```

### <a name="packagedeploymenttoolexe-parameter-descriptions"></a><span data-ttu-id="9bbbb-242">PackageDeploymentTool.exe parameter descriptions</span><span class="sxs-lookup"><span data-stu-id="9bbbb-242">PackageDeploymentTool.exe parameter descriptions</span></span>

#### <a name="common-parameters"></a><span data-ttu-id="9bbbb-243">Common parameters</span><span class="sxs-lookup"><span data-stu-id="9bbbb-243">Common parameters</span></span>

| <span data-ttu-id="9bbbb-244">Parameter</span><span class="sxs-lookup"><span data-stu-id="9bbbb-244">Parameter</span></span> | <span data-ttu-id="9bbbb-245">Description</span><span class="sxs-lookup"><span data-stu-id="9bbbb-245">Description</span></span> | <span data-ttu-id="9bbbb-246">Default Value</span><span class="sxs-lookup"><span data-stu-id="9bbbb-246">Default Value</span></span> | <span data-ttu-id="9bbbb-247">Required</span><span class="sxs-lookup"><span data-stu-id="9bbbb-247">Required</span></span> |
|---------|-----------|-------------|--------|
|<span data-ttu-id="9bbbb-248">Package</span><span class="sxs-lookup"><span data-stu-id="9bbbb-248">Package</span></span>|<span data-ttu-id="9bbbb-249">The path of the U-SQL database deployment package to be deployed.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-249">The path of the U-SQL database deployment package to be deployed.</span></span>|<span data-ttu-id="9bbbb-250">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-250">null</span></span>|<span data-ttu-id="9bbbb-251">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-251">true</span></span>|
|<span data-ttu-id="9bbbb-252">Database</span><span class="sxs-lookup"><span data-stu-id="9bbbb-252">Database</span></span>|<span data-ttu-id="9bbbb-253">The database name to be deployed to or created.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-253">The database name to be deployed to or created.</span></span>|<span data-ttu-id="9bbbb-254">master</span><span class="sxs-lookup"><span data-stu-id="9bbbb-254">master</span></span>|<span data-ttu-id="9bbbb-255">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-255">false</span></span>|
|<span data-ttu-id="9bbbb-256">LogFile</span><span class="sxs-lookup"><span data-stu-id="9bbbb-256">LogFile</span></span>|<span data-ttu-id="9bbbb-257">The path of the file for logging.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-257">The path of the file for logging.</span></span> <span data-ttu-id="9bbbb-258">Default to standard out (console).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-258">Default to standard out (console).</span></span>|<span data-ttu-id="9bbbb-259">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-259">null</span></span>|<span data-ttu-id="9bbbb-260">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-260">false</span></span>|
|<span data-ttu-id="9bbbb-261">LogLevel</span><span class="sxs-lookup"><span data-stu-id="9bbbb-261">LogLevel</span></span>|<span data-ttu-id="9bbbb-262">Log level: Verbose, Normal, Warning, or Error.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-262">Log level: Verbose, Normal, Warning, or Error.</span></span>|<span data-ttu-id="9bbbb-263">LogLevel.Normal</span><span class="sxs-lookup"><span data-stu-id="9bbbb-263">LogLevel.Normal</span></span>|<span data-ttu-id="9bbbb-264">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-264">false</span></span>|

#### <a name="parameter-for-local-deployment"></a><span data-ttu-id="9bbbb-265">Parameter for local deployment</span><span class="sxs-lookup"><span data-stu-id="9bbbb-265">Parameter for local deployment</span></span>

|<span data-ttu-id="9bbbb-266">Parameter</span><span class="sxs-lookup"><span data-stu-id="9bbbb-266">Parameter</span></span>|<span data-ttu-id="9bbbb-267">Description</span><span class="sxs-lookup"><span data-stu-id="9bbbb-267">Description</span></span>|<span data-ttu-id="9bbbb-268">Default Value</span><span class="sxs-lookup"><span data-stu-id="9bbbb-268">Default Value</span></span>|<span data-ttu-id="9bbbb-269">Required</span><span class="sxs-lookup"><span data-stu-id="9bbbb-269">Required</span></span>|
|---------|-----------|-------------|--------|
|<span data-ttu-id="9bbbb-270">DataRoot</span><span class="sxs-lookup"><span data-stu-id="9bbbb-270">DataRoot</span></span>|<span data-ttu-id="9bbbb-271">The path of the local data root folder.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-271">The path of the local data root folder.</span></span>|<span data-ttu-id="9bbbb-272">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-272">null</span></span>|<span data-ttu-id="9bbbb-273">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-273">true</span></span>|

#### <a name="parameters-for-azure-data-lake-analytics-deployment"></a><span data-ttu-id="9bbbb-274">Parameters for Azure Data Lake Analytics deployment</span><span class="sxs-lookup"><span data-stu-id="9bbbb-274">Parameters for Azure Data Lake Analytics deployment</span></span>

|<span data-ttu-id="9bbbb-275">Parameter</span><span class="sxs-lookup"><span data-stu-id="9bbbb-275">Parameter</span></span>|<span data-ttu-id="9bbbb-276">Description</span><span class="sxs-lookup"><span data-stu-id="9bbbb-276">Description</span></span>|<span data-ttu-id="9bbbb-277">Default Value</span><span class="sxs-lookup"><span data-stu-id="9bbbb-277">Default Value</span></span>|<span data-ttu-id="9bbbb-278">Required</span><span class="sxs-lookup"><span data-stu-id="9bbbb-278">Required</span></span>|
|---------|-----------|-------------|--------|
|<span data-ttu-id="9bbbb-279">Account</span><span class="sxs-lookup"><span data-stu-id="9bbbb-279">Account</span></span>|<span data-ttu-id="9bbbb-280">Specifies which Azure Data Lake Analytics account to deploy to by account name.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-280">Specifies which Azure Data Lake Analytics account to deploy to by account name.</span></span>|<span data-ttu-id="9bbbb-281">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-281">null</span></span>|<span data-ttu-id="9bbbb-282">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-282">true</span></span>|
|<span data-ttu-id="9bbbb-283">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9bbbb-283">ResourceGroup</span></span>|<span data-ttu-id="9bbbb-284">The Azure resource group name for the Azure Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-284">The Azure resource group name for the Azure Data Lake Analytics account.</span></span>|<span data-ttu-id="9bbbb-285">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-285">null</span></span>|<span data-ttu-id="9bbbb-286">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-286">true</span></span>|
|<span data-ttu-id="9bbbb-287">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="9bbbb-287">SubscriptionId</span></span>|<span data-ttu-id="9bbbb-288">The Azure subscription ID for the Azure Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-288">The Azure subscription ID for the Azure Data Lake Analytics account.</span></span>|<span data-ttu-id="9bbbb-289">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-289">null</span></span>|<span data-ttu-id="9bbbb-290">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-290">true</span></span>|
|<span data-ttu-id="9bbbb-291">Tenant</span><span class="sxs-lookup"><span data-stu-id="9bbbb-291">Tenant</span></span>|<span data-ttu-id="9bbbb-292">The tenant name is the Azure Active Directory (Azure AD) domain name.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-292">The tenant name is the Azure Active Directory (Azure AD) domain name.</span></span> <span data-ttu-id="9bbbb-293">Find it in the subscription management page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-293">Find it in the subscription management page in the Azure portal.</span></span>|<span data-ttu-id="9bbbb-294">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-294">null</span></span>|<span data-ttu-id="9bbbb-295">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-295">true</span></span>|
|<span data-ttu-id="9bbbb-296">AzureSDKPath</span><span class="sxs-lookup"><span data-stu-id="9bbbb-296">AzureSDKPath</span></span>|<span data-ttu-id="9bbbb-297">The path to search dependent assemblies in the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-297">The path to search dependent assemblies in the Azure SDK.</span></span>|<span data-ttu-id="9bbbb-298">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-298">null</span></span>|<span data-ttu-id="9bbbb-299">true</span><span class="sxs-lookup"><span data-stu-id="9bbbb-299">true</span></span>|
|<span data-ttu-id="9bbbb-300">Interactive</span><span class="sxs-lookup"><span data-stu-id="9bbbb-300">Interactive</span></span>|<span data-ttu-id="9bbbb-301">Whether or not to use interactive mode for authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-301">Whether or not to use interactive mode for authentication.</span></span>|<span data-ttu-id="9bbbb-302">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-302">false</span></span>|<span data-ttu-id="9bbbb-303">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-303">false</span></span>|
|<span data-ttu-id="9bbbb-304">ClientId</span><span class="sxs-lookup"><span data-stu-id="9bbbb-304">ClientId</span></span>|<span data-ttu-id="9bbbb-305">The Azure AD application ID required for non-interactive authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-305">The Azure AD application ID required for non-interactive authentication.</span></span>|<span data-ttu-id="9bbbb-306">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-306">null</span></span>|<span data-ttu-id="9bbbb-307">Required for non-interactive authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-307">Required for non-interactive authentication.</span></span>|
|<span data-ttu-id="9bbbb-308">Secrete</span><span class="sxs-lookup"><span data-stu-id="9bbbb-308">Secrete</span></span>|<span data-ttu-id="9bbbb-309">The secrete or password for non-interactive authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-309">The secrete or password for non-interactive authentication.</span></span> <span data-ttu-id="9bbbb-310">It should be used only in a trusted and secure environment.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-310">It should be used only in a trusted and secure environment.</span></span>|<span data-ttu-id="9bbbb-311">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-311">null</span></span>|<span data-ttu-id="9bbbb-312">Required for non-interactive authentication, or else use SecreteFile.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-312">Required for non-interactive authentication, or else use SecreteFile.</span></span>|
|<span data-ttu-id="9bbbb-313">SecreteFile</span><span class="sxs-lookup"><span data-stu-id="9bbbb-313">SecreteFile</span></span>|<span data-ttu-id="9bbbb-314">The file saves the secrete or password for non-interactive authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-314">The file saves the secrete or password for non-interactive authentication.</span></span> <span data-ttu-id="9bbbb-315">Make sure to keep it readable only by the current user.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-315">Make sure to keep it readable only by the current user.</span></span>|<span data-ttu-id="9bbbb-316">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-316">null</span></span>|<span data-ttu-id="9bbbb-317">Required for non-interactive authentication, or else use Secrete.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-317">Required for non-interactive authentication, or else use Secrete.</span></span>|
|<span data-ttu-id="9bbbb-318">CertFile</span><span class="sxs-lookup"><span data-stu-id="9bbbb-318">CertFile</span></span>|<span data-ttu-id="9bbbb-319">The file saves X.509 certification for non-interactive authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-319">The file saves X.509 certification for non-interactive authentication.</span></span> <span data-ttu-id="9bbbb-320">The default is to use client secrete authentication.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-320">The default is to use client secrete authentication.</span></span>|<span data-ttu-id="9bbbb-321">null</span><span class="sxs-lookup"><span data-stu-id="9bbbb-321">null</span></span>|<span data-ttu-id="9bbbb-322">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-322">false</span></span>|
| <span data-ttu-id="9bbbb-323">JobPrefix</span><span class="sxs-lookup"><span data-stu-id="9bbbb-323">JobPrefix</span></span> | <span data-ttu-id="9bbbb-324">The prefix for database deployment of a U-SQL DDL job.</span><span class="sxs-lookup"><span data-stu-id="9bbbb-324">The prefix for database deployment of a U-SQL DDL job.</span></span> | <span data-ttu-id="9bbbb-325">Deploy_ + DateTime.Now</span><span class="sxs-lookup"><span data-stu-id="9bbbb-325">Deploy_ + DateTime.Now</span></span> | <span data-ttu-id="9bbbb-326">false</span><span class="sxs-lookup"><span data-stu-id="9bbbb-326">false</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9bbbb-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bbbb-327">Next steps</span></span>

- <span data-ttu-id="9bbbb-328">[How to test your Azure Data Lake Analytics code](data-lake-analytics-cicd-test.md).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-328">[How to test your Azure Data Lake Analytics code](data-lake-analytics-cicd-test.md).</span></span>
- <span data-ttu-id="9bbbb-329">[Run U-SQL script on your local machine](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-329">[Run U-SQL script on your local machine](data-lake-analytics-data-lake-tools-local-run.md).</span></span>
- <span data-ttu-id="9bbbb-330">[Use U-SQL database project to develop U-SQL database](data-lake-analytics-data-lake-tools-develop-usql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9bbbb-330">[Use U-SQL database project to develop U-SQL database](data-lake-analytics-data-lake-tools-develop-usql-database.md).</span></span>
