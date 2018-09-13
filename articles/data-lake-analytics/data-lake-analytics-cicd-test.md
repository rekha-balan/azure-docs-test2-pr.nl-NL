---
title: How to test your Azure Data Lake Analytics code
description: Learn how to add test cases for U-SQL and extended C# code for Azure Data Lake Analytics.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.topic: conceptual
ms.workload: big-data
ms.date: 07/03/2018
ms.openlocfilehash: 82ffcc6f891a64650375121b9418daad33dc2628
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864803"
---
# <a name="test-your-azure-data-lake-analytics-code"></a><span data-ttu-id="24a29-103">Test your Azure Data Lake Analytics code</span><span class="sxs-lookup"><span data-stu-id="24a29-103">Test your Azure Data Lake Analytics code</span></span>

<span data-ttu-id="24a29-104">Azure Data Lake provides the U-SQL language, which combines declarative SQL with imperative C# to process data at any scale.</span><span class="sxs-lookup"><span data-stu-id="24a29-104">Azure Data Lake provides the U-SQL language, which combines declarative SQL with imperative C# to process data at any scale.</span></span> <span data-ttu-id="24a29-105">In this document, you learn how to create test cases for U-SQL and extended C# UDO (user-defined operator) code.</span><span class="sxs-lookup"><span data-stu-id="24a29-105">In this document, you learn how to create test cases for U-SQL and extended C# UDO (user-defined operator) code.</span></span>

## <a name="test-u-sql-scripts"></a><span data-ttu-id="24a29-106">Test U-SQL scripts</span><span class="sxs-lookup"><span data-stu-id="24a29-106">Test U-SQL scripts</span></span>

<span data-ttu-id="24a29-107">The U-SQL script is compiled and optimized for executable code to run across machines on the cloud or on your local machine.</span><span class="sxs-lookup"><span data-stu-id="24a29-107">The U-SQL script is compiled and optimized for executable code to run across machines on the cloud or on your local machine.</span></span> <span data-ttu-id="24a29-108">The compilation and optimization process treats the entire U-SQL script as a whole.</span><span class="sxs-lookup"><span data-stu-id="24a29-108">The compilation and optimization process treats the entire U-SQL script as a whole.</span></span> <span data-ttu-id="24a29-109">You can't do a traditional "unit test" for every statement.</span><span class="sxs-lookup"><span data-stu-id="24a29-109">You can't do a traditional "unit test" for every statement.</span></span> <span data-ttu-id="24a29-110">However, by using the U-SQL test SDK and the local run SDK, you can do script-level tests.</span><span class="sxs-lookup"><span data-stu-id="24a29-110">However, by using the U-SQL test SDK and the local run SDK, you can do script-level tests.</span></span>

### <a name="create-test-cases-for-u-sql-script"></a><span data-ttu-id="24a29-111">Create test cases for U-SQL script</span><span class="sxs-lookup"><span data-stu-id="24a29-111">Create test cases for U-SQL script</span></span>

<span data-ttu-id="24a29-112">Azure Data Lake Tools for Visual Studio enables you to create U-SQL script test cases.</span><span class="sxs-lookup"><span data-stu-id="24a29-112">Azure Data Lake Tools for Visual Studio enables you to create U-SQL script test cases.</span></span>

1.  <span data-ttu-id="24a29-113">Right-click a U-SQL script in Solution Explorer, and then select **Create Unit Test**.</span><span class="sxs-lookup"><span data-stu-id="24a29-113">Right-click a U-SQL script in Solution Explorer, and then select **Create Unit Test**.</span></span>
2.  <span data-ttu-id="24a29-114">Create a new test project or insert the test case into an existing test project.</span><span class="sxs-lookup"><span data-stu-id="24a29-114">Create a new test project or insert the test case into an existing test project.</span></span>

    ![Data Lake Tools for Visual Studio -- create a U-SQL test project](./media/data-lake-analytics-cicd-test/data-lake-tools-create-usql-test-project.png) 

    ![Data Lake Tools for Visual Studio -- create a U-SQL test project configuration](./media/data-lake-analytics-cicd-test/data-lake-tools-create-usql-test-project-configure.png) 

### <a name="manage-the-test-data-source"></a><span data-ttu-id="24a29-117">Manage the test data source</span><span class="sxs-lookup"><span data-stu-id="24a29-117">Manage the test data source</span></span>

<span data-ttu-id="24a29-118">When you test U-SQL scripts, you need test input files.</span><span class="sxs-lookup"><span data-stu-id="24a29-118">When you test U-SQL scripts, you need test input files.</span></span> <span data-ttu-id="24a29-119">You can manage the test data by configuring **Test Data Source** in the U-SQL project properties.</span><span class="sxs-lookup"><span data-stu-id="24a29-119">You can manage the test data by configuring **Test Data Source** in the U-SQL project properties.</span></span> 

<span data-ttu-id="24a29-120">When you call the `Initialize()` interface in the U-SQL test SDK, a temporary local data root folder is created under the working directory of the test project, and all files and subfolders (and files under subfolders) in the test data source folder are copied to the temporary local data root folder before you run the U-SQL script test cases.</span><span class="sxs-lookup"><span data-stu-id="24a29-120">When you call the `Initialize()` interface in the U-SQL test SDK, a temporary local data root folder is created under the working directory of the test project, and all files and subfolders (and files under subfolders) in the test data source folder are copied to the temporary local data root folder before you run the U-SQL script test cases.</span></span> <span data-ttu-id="24a29-121">You can add more test data source folders by splitting the test data folder path with a semicolon.</span><span class="sxs-lookup"><span data-stu-id="24a29-121">You can add more test data source folders by splitting the test data folder path with a semicolon.</span></span>

![Data Lake Tools for Visual Studio -- configure project test data source](./media/data-lake-analytics-cicd-test/data-lake-tools-configure-project-test-data-source.png)

### <a name="manage-the-database-environment-for-testing"></a><span data-ttu-id="24a29-123">Manage the database environment for testing</span><span class="sxs-lookup"><span data-stu-id="24a29-123">Manage the database environment for testing</span></span>

<span data-ttu-id="24a29-124">If your U-SQL scripts use or query with U-SQL database objects (for example, when calling stored procedures) then you need to initialize the database environment before running U-SQL test cases.</span><span class="sxs-lookup"><span data-stu-id="24a29-124">If your U-SQL scripts use or query with U-SQL database objects (for example, when calling stored procedures) then you need to initialize the database environment before running U-SQL test cases.</span></span> <span data-ttu-id="24a29-125">The `Initialize()` interface in the U-SQL test SDK helps you deploy all databases that are referenced by the U-SQL project to the temporary local data root folder in the working directory of the test project.</span><span class="sxs-lookup"><span data-stu-id="24a29-125">The `Initialize()` interface in the U-SQL test SDK helps you deploy all databases that are referenced by the U-SQL project to the temporary local data root folder in the working directory of the test project.</span></span> 

<span data-ttu-id="24a29-126">Learn more about [how to manage U-SQL database project references for a U-SQL project](data-lake-analytics-data-lake-tools-develop-usql-database.md#reference-a-u-sql-database-project).</span><span class="sxs-lookup"><span data-stu-id="24a29-126">Learn more about [how to manage U-SQL database project references for a U-SQL project](data-lake-analytics-data-lake-tools-develop-usql-database.md#reference-a-u-sql-database-project).</span></span>

### <a name="verify-test-results"></a><span data-ttu-id="24a29-127">Verify test results</span><span class="sxs-lookup"><span data-stu-id="24a29-127">Verify test results</span></span>

<span data-ttu-id="24a29-128">The `Run()` interface returns a job execution result.</span><span class="sxs-lookup"><span data-stu-id="24a29-128">The `Run()` interface returns a job execution result.</span></span> <span data-ttu-id="24a29-129">0 means success, and 1 means failure.</span><span class="sxs-lookup"><span data-stu-id="24a29-129">0 means success, and 1 means failure.</span></span> <span data-ttu-id="24a29-130">You can also use C# assert functions to verify the outputs.</span><span class="sxs-lookup"><span data-stu-id="24a29-130">You can also use C# assert functions to verify the outputs.</span></span> 

### <a name="run-test-cases-in-visual-studio"></a><span data-ttu-id="24a29-131">Run test cases in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24a29-131">Run test cases in Visual Studio</span></span>

<span data-ttu-id="24a29-132">A U-SQL script test project is built on top of a C# unit test framework.</span><span class="sxs-lookup"><span data-stu-id="24a29-132">A U-SQL script test project is built on top of a C# unit test framework.</span></span> <span data-ttu-id="24a29-133">After you build the project, you can run all test cases through **Test Explorer > Playlist**.</span><span class="sxs-lookup"><span data-stu-id="24a29-133">After you build the project, you can run all test cases through **Test Explorer > Playlist**.</span></span> <span data-ttu-id="24a29-134">Alternatively, right-click the .cs file, and then select **Run Tests**.</span><span class="sxs-lookup"><span data-stu-id="24a29-134">Alternatively, right-click the .cs file, and then select **Run Tests**.</span></span>

## <a name="test-c-udos"></a><span data-ttu-id="24a29-135">Test C# UDOs</span><span class="sxs-lookup"><span data-stu-id="24a29-135">Test C# UDOs</span></span>

### <a name="create-test-cases-for-c-udos"></a><span data-ttu-id="24a29-136">Create test cases for C# UDOs</span><span class="sxs-lookup"><span data-stu-id="24a29-136">Create test cases for C# UDOs</span></span>

<span data-ttu-id="24a29-137">You can use a C# unit test framework to test your C# UDOs (user-defined operators).</span><span class="sxs-lookup"><span data-stu-id="24a29-137">You can use a C# unit test framework to test your C# UDOs (user-defined operators).</span></span> <span data-ttu-id="24a29-138">When testing UDOs, you need to prepare corresponding **IRowset** objects as inputs.</span><span class="sxs-lookup"><span data-stu-id="24a29-138">When testing UDOs, you need to prepare corresponding **IRowset** objects as inputs.</span></span>

<span data-ttu-id="24a29-139">There are two ways to create an IRowset object:</span><span class="sxs-lookup"><span data-stu-id="24a29-139">There are two ways to create an IRowset object:</span></span>

- <span data-ttu-id="24a29-140">Load data from a file to create IRowset:</span><span class="sxs-lookup"><span data-stu-id="24a29-140">Load data from a file to create IRowset:</span></span>

    ```csharp
    //Schema: "a:int, b:int"
    USqlColumn<int> col1 = new USqlColumn<int>("a");
    USqlColumn<int> col2 = new USqlColumn<int>("b");
    List<IColumn> columns = new List<IColumn> { col1, col2 };
    USqlSchema schema = new USqlSchema(columns);

    //Generate one row with default values
    IUpdatableRow output = new USqlRow(schema, null).AsUpdatable();

    //Get data from file
    IRowset rowset = UnitTestHelper.GetRowsetFromFile(@"processor.txt", schema, output.AsReadOnly(), discardAdditionalColumns: true, rowDelimiter: null, columnSeparator: '\t');
    ```

- <span data-ttu-id="24a29-141">Use data from a data collection to create IRowset:</span><span class="sxs-lookup"><span data-stu-id="24a29-141">Use data from a data collection to create IRowset:</span></span>

    ```csharp
    //Schema: "a:int, b:int"
    USqlSchema schema = new USqlSchema(
        new USqlColumn<int>("a"),
        new USqlColumn<int>("b")
    );

    IUpdatableRow output = new USqlRow(schema, null).AsUpdatable();

    //Generate Rowset with specified values
    List<object[]> values = new List<object[]>{
        new object[2] { 2, 3 },
        new object[2] { 10, 20 }
    };

    IEnumerable<IRow> rows = UnitTestHelper.CreateRowsFromValues(schema, values);
    IRowset rowset = UnitTestHelper.GetRowsetFromCollection(rows, output.AsReadOnly());
    ```

### <a name="verify-test-results"></a><span data-ttu-id="24a29-142">Verify test results</span><span class="sxs-lookup"><span data-stu-id="24a29-142">Verify test results</span></span>

<span data-ttu-id="24a29-143">After you call UDO functions, you can verify the results through the schema and Rowset value verification by using C# assert functions.</span><span class="sxs-lookup"><span data-stu-id="24a29-143">After you call UDO functions, you can verify the results through the schema and Rowset value verification by using C# assert functions.</span></span> <span data-ttu-id="24a29-144">You can use sample code in a U-SQL C# UDO unit test sample project through **File > New > Project** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24a29-144">You can use sample code in a U-SQL C# UDO unit test sample project through **File > New > Project** in Visual Studio.</span></span>

### <a name="run-test-cases-in-visual-studio"></a><span data-ttu-id="24a29-145">Run test cases in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24a29-145">Run test cases in Visual Studio</span></span>

<span data-ttu-id="24a29-146">After you build the test project, you can run all test cases though **Test Explorer > Playlist**, or right-click the .cs file and choose **Run Tests**.</span><span class="sxs-lookup"><span data-stu-id="24a29-146">After you build the test project, you can run all test cases though **Test Explorer > Playlist**, or right-click the .cs file and choose **Run Tests**.</span></span>

## <a name="run-test-cases-in-azure-devops"></a><span data-ttu-id="24a29-147">Run test cases in Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="24a29-147">Run test cases in Azure DevOps</span></span>

<span data-ttu-id="24a29-148">Both **U-SQL script test projects** and **C# UDO test projects** inherit C# unit test projects.</span><span class="sxs-lookup"><span data-stu-id="24a29-148">Both **U-SQL script test projects** and **C# UDO test projects** inherit C# unit test projects.</span></span> <span data-ttu-id="24a29-149">The [Visual Studio test task](https://docs.microsoft.com/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts) in Azure DevOps can run these test cases.</span><span class="sxs-lookup"><span data-stu-id="24a29-149">The [Visual Studio test task](https://docs.microsoft.com/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts) in Azure DevOps can run these test cases.</span></span> 

### <a name="run-u-sql-test-cases-in-azure-devops"></a><span data-ttu-id="24a29-150">Run U-SQL test cases in Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="24a29-150">Run U-SQL test cases in Azure DevOps</span></span>

<span data-ttu-id="24a29-151">For a U-SQL test, make sure you load `CPPSDK` on your build machine, and then pass the `CPPSDK` path to USqlScriptTestRunner(cppSdkFolderFullPath: @"").</span><span class="sxs-lookup"><span data-stu-id="24a29-151">For a U-SQL test, make sure you load `CPPSDK` on your build machine, and then pass the `CPPSDK` path to USqlScriptTestRunner(cppSdkFolderFullPath: @"").</span></span>

<span data-ttu-id="24a29-152">**What is CPPSDK?**</span><span class="sxs-lookup"><span data-stu-id="24a29-152">**What is CPPSDK?**</span></span>

<span data-ttu-id="24a29-153">CPPSDK is a package that includes Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0.</span><span class="sxs-lookup"><span data-stu-id="24a29-153">CPPSDK is a package that includes Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0.</span></span> <span data-ttu-id="24a29-154">This is the environment that's needed by the U-SQL runtime.</span><span class="sxs-lookup"><span data-stu-id="24a29-154">This is the environment that's needed by the U-SQL runtime.</span></span> <span data-ttu-id="24a29-155">You can get this package under the Azure Data Lake Tools for Visual Studio installation folder:</span><span class="sxs-lookup"><span data-stu-id="24a29-155">You can get this package under the Azure Data Lake Tools for Visual Studio installation folder:</span></span>

- <span data-ttu-id="24a29-156">For Visual Studio 2015, it is under `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK`</span><span class="sxs-lookup"><span data-stu-id="24a29-156">For Visual Studio 2015, it is under `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK`</span></span>
- <span data-ttu-id="24a29-157">For Visual Studio 2017, it is under `C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\SDK\ScopeCppSDK`</span><span class="sxs-lookup"><span data-stu-id="24a29-157">For Visual Studio 2017, it is under `C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\SDK\ScopeCppSDK`</span></span>

<span data-ttu-id="24a29-158">**Prepare CPPSDK in the Azure DevOps build agent**</span><span class="sxs-lookup"><span data-stu-id="24a29-158">**Prepare CPPSDK in the Azure DevOps build agent**</span></span>

<span data-ttu-id="24a29-159">The most common way to prepare the CPPSDK dependency in Azure DevOps is as follows:</span><span class="sxs-lookup"><span data-stu-id="24a29-159">The most common way to prepare the CPPSDK dependency in Azure DevOps is as follows:</span></span>

1.  <span data-ttu-id="24a29-160">Zip the folder  that includes the CPPSDK libraries.</span><span class="sxs-lookup"><span data-stu-id="24a29-160">Zip the folder  that includes the CPPSDK libraries.</span></span>
2.  <span data-ttu-id="24a29-161">Check in the .zip file to your source control system.</span><span class="sxs-lookup"><span data-stu-id="24a29-161">Check in the .zip file to your source control system.</span></span> <span data-ttu-id="24a29-162">(The .zip file ensures that you check in all libraries under the CPPSDK folder so that some files aren't ignored by ".gitignore".)</span><span class="sxs-lookup"><span data-stu-id="24a29-162">(The .zip file ensures that you check in all libraries under the CPPSDK folder so that some files aren't ignored by ".gitignore".)</span></span>   
3.  <span data-ttu-id="24a29-163">Unzip the .zip file in the build pipeline.</span><span class="sxs-lookup"><span data-stu-id="24a29-163">Unzip the .zip file in the build pipeline.</span></span>
4.  <span data-ttu-id="24a29-164">Point `USqlScriptTestRunner` to this unzipped folder on the build machine.</span><span class="sxs-lookup"><span data-stu-id="24a29-164">Point `USqlScriptTestRunner` to this unzipped folder on the build machine.</span></span>

### <a name="run-c-udo-test-cases-in-azure-devops"></a><span data-ttu-id="24a29-165">Run C# UDO test cases in Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="24a29-165">Run C# UDO test cases in Azure DevOps</span></span>

<span data-ttu-id="24a29-166">For a C# UDO test, make sure to reference the following assemblies, which  are needed for UDOs.</span><span class="sxs-lookup"><span data-stu-id="24a29-166">For a C# UDO test, make sure to reference the following assemblies, which  are needed for UDOs.</span></span> <span data-ttu-id="24a29-167">If you reference them through [the Nuget package Microsoft.Azure.DataLake.USQL.Interfaces](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.Interfaces/), make sure you add a NuGet Restore task in your build pipeline.</span><span class="sxs-lookup"><span data-stu-id="24a29-167">If you reference them through [the Nuget package Microsoft.Azure.DataLake.USQL.Interfaces](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.Interfaces/), make sure you add a NuGet Restore task in your build pipeline.</span></span>

* <span data-ttu-id="24a29-168">Microsoft.Analytics.Interfaces</span><span class="sxs-lookup"><span data-stu-id="24a29-168">Microsoft.Analytics.Interfaces</span></span>
* <span data-ttu-id="24a29-169">Microsoft.Analytics.Types</span><span class="sxs-lookup"><span data-stu-id="24a29-169">Microsoft.Analytics.Types</span></span>
* <span data-ttu-id="24a29-170">Microsoft.Analytics.UnitTest</span><span class="sxs-lookup"><span data-stu-id="24a29-170">Microsoft.Analytics.UnitTest</span></span>

## <a name="next-steps"></a><span data-ttu-id="24a29-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="24a29-171">Next steps</span></span>

- [<span data-ttu-id="24a29-172">How to set up CI/CD pipeline for Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="24a29-172">How to set up CI/CD pipeline for Azure Data Lake Analytics</span></span>](data-lake-analytics-cicd-overview.md)
- [<span data-ttu-id="24a29-173">Run U-SQL script on your local machine</span><span class="sxs-lookup"><span data-stu-id="24a29-173">Run U-SQL script on your local machine</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
- [<span data-ttu-id="24a29-174">Use U-SQL database project to develop U-SQL database</span><span class="sxs-lookup"><span data-stu-id="24a29-174">Use U-SQL database project to develop U-SQL database</span></span>](data-lake-analytics-data-lake-tools-develop-usql-database.md)

