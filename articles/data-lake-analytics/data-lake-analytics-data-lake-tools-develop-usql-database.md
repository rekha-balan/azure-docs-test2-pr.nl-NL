---
title: Use a U-SQL database project to develop a U-SQL database for Azure Data Lake
description: Learn how to develop a U-SQL database using Azure Data Lake Tools for Visual Studio.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.topic: conceptual
ms.workload: big-data
ms.date: 07/03/2018
ms.openlocfilehash: c731fd78ed7052697b3a5bd7c4da3a743e5a208d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867157"
---
# <a name="use-a-u-sql-database-project-to-develop-a-u-sql-database-for-azure-data-lake"></a><span data-ttu-id="31c7c-103">Use a U-SQL database project to develop a U-SQL database for Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="31c7c-103">Use a U-SQL database project to develop a U-SQL database for Azure Data Lake</span></span>

<span data-ttu-id="31c7c-104">U-SQL database provides structured views over unstructured data and managed structured data in tables.</span><span class="sxs-lookup"><span data-stu-id="31c7c-104">U-SQL database provides structured views over unstructured data and managed structured data in tables.</span></span> <span data-ttu-id="31c7c-105">It also provides a general metadata catalog system for organizing your structured data and custom code.</span><span class="sxs-lookup"><span data-stu-id="31c7c-105">It also provides a general metadata catalog system for organizing your structured data and custom code.</span></span> <span data-ttu-id="31c7c-106">The database is the concept that groups these related objects together.</span><span class="sxs-lookup"><span data-stu-id="31c7c-106">The database is the concept that groups these related objects together.</span></span>

<span data-ttu-id="31c7c-107">Learn more about [U-SQL database and Data Definition Language (DDL)](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/data-definition-language-ddl-statements-u-sql).</span><span class="sxs-lookup"><span data-stu-id="31c7c-107">Learn more about [U-SQL database and Data Definition Language (DDL)](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/data-definition-language-ddl-statements-u-sql).</span></span> 

<span data-ttu-id="31c7c-108">The U-SQL database project is a project type in Visual Studio that helps developers develop, manage, and deploy their U-SQL databases quickly and easily.</span><span class="sxs-lookup"><span data-stu-id="31c7c-108">The U-SQL database project is a project type in Visual Studio that helps developers develop, manage, and deploy their U-SQL databases quickly and easily.</span></span>

## <a name="create-a-u-sql-database-project"></a><span data-ttu-id="31c7c-109">Create a U-SQL database project</span><span class="sxs-lookup"><span data-stu-id="31c7c-109">Create a U-SQL database project</span></span>

<span data-ttu-id="31c7c-110">Azure Data Lake Tools for Visual Studio added a new project template called U-SQL database project after version 2.3.3000.0.</span><span class="sxs-lookup"><span data-stu-id="31c7c-110">Azure Data Lake Tools for Visual Studio added a new project template called U-SQL database project after version 2.3.3000.0.</span></span> <span data-ttu-id="31c7c-111">To create a U-SQL project, select **File > New > Project**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-111">To create a U-SQL project, select **File > New > Project**.</span></span> <span data-ttu-id="31c7c-112">The U-SQL Database Project can be found under **Azure Data Lake > U-SQL node**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-112">The U-SQL Database Project can be found under **Azure Data Lake > U-SQL node**.</span></span>

![Data Lake Tools for Visual Studio--create U-SQL database project](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-create-usql-database-project-creation.png) 

## <a name="develop-u-sql-database-objects-by-using-a-database-project"></a><span data-ttu-id="31c7c-114">Develop U-SQL database objects by using a database project</span><span class="sxs-lookup"><span data-stu-id="31c7c-114">Develop U-SQL database objects by using a database project</span></span>

<span data-ttu-id="31c7c-115">Right-click the U-SQL database project.</span><span class="sxs-lookup"><span data-stu-id="31c7c-115">Right-click the U-SQL database project.</span></span> <span data-ttu-id="31c7c-116">The select **Add > New item**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-116">The select **Add > New item**.</span></span> <span data-ttu-id="31c7c-117">You can find all new supported object types in the **Add New Item** Wizard.</span><span class="sxs-lookup"><span data-stu-id="31c7c-117">You can find all new supported object types in the **Add New Item** Wizard.</span></span> 

<span data-ttu-id="31c7c-118">For a non-assembly object (for example, a table-valued function), a new U-SQL script is created after you add a new item.</span><span class="sxs-lookup"><span data-stu-id="31c7c-118">For a non-assembly object (for example, a table-valued function), a new U-SQL script is created after you add a new item.</span></span> <span data-ttu-id="31c7c-119">You can start to develop the DDL statement for that object in the editor.</span><span class="sxs-lookup"><span data-stu-id="31c7c-119">You can start to develop the DDL statement for that object in the editor.</span></span>

<span data-ttu-id="31c7c-120">For an assembly object, the tool provides a user-friendly UI editor that helps you register the assembly and deploy DLL files and other additional files.</span><span class="sxs-lookup"><span data-stu-id="31c7c-120">For an assembly object, the tool provides a user-friendly UI editor that helps you register the assembly and deploy DLL files and other additional files.</span></span> <span data-ttu-id="31c7c-121">The following steps show you how to add an assembly object definition to the U-SQL database project:</span><span class="sxs-lookup"><span data-stu-id="31c7c-121">The following steps show you how to add an assembly object definition to the U-SQL database project:</span></span>

1.  <span data-ttu-id="31c7c-122">Add references to the C# project that include the UDO/UDAG/UDF for the U-SQL database project.</span><span class="sxs-lookup"><span data-stu-id="31c7c-122">Add references to the C# project that include the UDO/UDAG/UDF for the U-SQL database project.</span></span>

    ![Data Lake Tools for Visual Studio--Add U-SQL database project reference](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-add-project-reference.png) 

    ![Data Lake Tools for Visual Studio--Add U-SQL database project reference](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-add-project-reference-wizard.png)

2.  <span data-ttu-id="31c7c-125">In the assembly design view, choose the referenced assembly from **Create assembly from reference** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="31c7c-125">In the assembly design view, choose the referenced assembly from **Create assembly from reference** drop-down menu.</span></span>

    ![Data Lake Tools for Visual Studio--create assembly from reference](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-create-assembly-from-reference.png)

3.  <span data-ttu-id="31c7c-127">Add **Managed Dependencies** and **Additional Files** if there are any.</span><span class="sxs-lookup"><span data-stu-id="31c7c-127">Add **Managed Dependencies** and **Additional Files** if there are any.</span></span> <span data-ttu-id="31c7c-128">When you add additional files, the tool uses the relative path to make sure it can find the assemblies both on your local machine and on the build machine later.</span><span class="sxs-lookup"><span data-stu-id="31c7c-128">When you add additional files, the tool uses the relative path to make sure it can find the assemblies both on your local machine and on the build machine later.</span></span> 

<span data-ttu-id="31c7c-129">@_DeployTempDirectory is a predefined variable that points the tool to the build output folder.</span><span class="sxs-lookup"><span data-stu-id="31c7c-129">@_DeployTempDirectory is a predefined variable that points the tool to the build output folder.</span></span> <span data-ttu-id="31c7c-130">Under the build output folder, every assembly has a subfolder named with the assembly name.</span><span class="sxs-lookup"><span data-stu-id="31c7c-130">Under the build output folder, every assembly has a subfolder named with the assembly name.</span></span> <span data-ttu-id="31c7c-131">All DLLs and additional files are in that subfolder.</span><span class="sxs-lookup"><span data-stu-id="31c7c-131">All DLLs and additional files are in that subfolder.</span></span> 
 
## <a name="build-a-u-sql-database-project"></a><span data-ttu-id="31c7c-132">Build a U-SQL database project</span><span class="sxs-lookup"><span data-stu-id="31c7c-132">Build a U-SQL database project</span></span>

<span data-ttu-id="31c7c-133">The build output for a U-SQL database project is a U-SQL database deployment package, named with the suffix `.usqldbpack`.</span><span class="sxs-lookup"><span data-stu-id="31c7c-133">The build output for a U-SQL database project is a U-SQL database deployment package, named with the suffix `.usqldbpack`.</span></span> <span data-ttu-id="31c7c-134">The `.usqldbpack` package is a .zip file that includes all DDL statements in a single U-SQL script in the **DDL** folder, and all DLLs and additional files for assemblies in the **Temp** folder.</span><span class="sxs-lookup"><span data-stu-id="31c7c-134">The `.usqldbpack` package is a .zip file that includes all DDL statements in a single U-SQL script in the **DDL** folder, and all DLLs and additional files for assemblies in the **Temp** folder.</span></span>

<span data-ttu-id="31c7c-135">Learn more about [how to build a U-SQL database project with the MSBuild command line and a Azure DevOps Services build task](data-lake-analytics-cicd-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31c7c-135">Learn more about [how to build a U-SQL database project with the MSBuild command line and a Azure DevOps Services build task](data-lake-analytics-cicd-overview.md).</span></span>

## <a name="deploy-a-u-sql-database"></a><span data-ttu-id="31c7c-136">Deploy a U-SQL database</span><span class="sxs-lookup"><span data-stu-id="31c7c-136">Deploy a U-SQL database</span></span>

<span data-ttu-id="31c7c-137">The .usqldbpack package can be deployed to either a local account or an Azure Data Lake Analytics account by using Visual Studio or the deployment SDK.</span><span class="sxs-lookup"><span data-stu-id="31c7c-137">The .usqldbpack package can be deployed to either a local account or an Azure Data Lake Analytics account by using Visual Studio or the deployment SDK.</span></span> 

### <a name="deploy-a-u-sql-database-in-visual-studio"></a><span data-ttu-id="31c7c-138">Deploy a U-SQL database in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31c7c-138">Deploy a U-SQL database in Visual Studio</span></span>

<span data-ttu-id="31c7c-139">You can deploy a U-SQL database through a U-SQL database project or a .usqldbpack package in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31c7c-139">You can deploy a U-SQL database through a U-SQL database project or a .usqldbpack package in Visual Studio.</span></span>

#### <a name="deploy-through-a-u-sql-database-project"></a><span data-ttu-id="31c7c-140">Deploy through a U-SQL database project</span><span class="sxs-lookup"><span data-stu-id="31c7c-140">Deploy through a U-SQL database project</span></span>

1.  <span data-ttu-id="31c7c-141">Right-click the U-SQL database project, and then select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-141">Right-click the U-SQL database project, and then select **Deploy**.</span></span>
2.  <span data-ttu-id="31c7c-142">In the **Deploy U-SQL Database Wizard**, select the **ADLA account** to which you want to deploy the database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-142">In the **Deploy U-SQL Database Wizard**, select the **ADLA account** to which you want to deploy the database.</span></span> <span data-ttu-id="31c7c-143">Both local accounts and ADLA accounts are supported.</span><span class="sxs-lookup"><span data-stu-id="31c7c-143">Both local accounts and ADLA accounts are supported.</span></span>
3.  <span data-ttu-id="31c7c-144">**Database Source** is filled in automatically, and points to the .usqldbpack package in the project's build output folder.</span><span class="sxs-lookup"><span data-stu-id="31c7c-144">**Database Source** is filled in automatically, and points to the .usqldbpack package in the project's build output folder.</span></span>
4.  <span data-ttu-id="31c7c-145">Enter a name in **Database Name** to create a database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-145">Enter a name in **Database Name** to create a database.</span></span> <span data-ttu-id="31c7c-146">If a database with that same name already exists in the target Azure Data Lake Analytics account, all objects that are defined in the database project are created without recreating the database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-146">If a database with that same name already exists in the target Azure Data Lake Analytics account, all objects that are defined in the database project are created without recreating the database.</span></span>
5.  <span data-ttu-id="31c7c-147">To deploy the U-SQL database, select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-147">To deploy the U-SQL database, select **Submit**.</span></span> <span data-ttu-id="31c7c-148">All resources (assemblies and additional files) are uploaded, and a U-SQL job that includes all DDL statements is submitted.</span><span class="sxs-lookup"><span data-stu-id="31c7c-148">All resources (assemblies and additional files) are uploaded, and a U-SQL job that includes all DDL statements is submitted.</span></span>

    ![Data Lake Tools for Visual Studio--Deploy U-SQL database project](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-deploy-usql-database-project.png)

    ![Data Lake Tools for Visual Studio--Deploy U-SQL database project wizard](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-deploy-usql-database-project-wizard.png)

#### <a name="deploy-through-a-u-sql-database-deployment-package"></a><span data-ttu-id="31c7c-151">Deploy through a U-SQL database deployment package</span><span class="sxs-lookup"><span data-stu-id="31c7c-151">Deploy through a U-SQL database deployment package</span></span>

1.  <span data-ttu-id="31c7c-152">Open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-152">Open **Server Explorer**.</span></span> <span data-ttu-id="31c7c-153">Then expand the **Azure Data Lake Analytics account** to which you want to deploy the database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-153">Then expand the **Azure Data Lake Analytics account** to which you want to deploy the database.</span></span>
2.  <span data-ttu-id="31c7c-154">Right click **U-SQL Databases**, and then choose **Deploy Database**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-154">Right click **U-SQL Databases**, and then choose **Deploy Database**.</span></span>
3.  <span data-ttu-id="31c7c-155">Set **Database Source** to the U-SQL database deployment package (.usqldbpack file) path.</span><span class="sxs-lookup"><span data-stu-id="31c7c-155">Set **Database Source** to the U-SQL database deployment package (.usqldbpack file) path.</span></span>
4.  <span data-ttu-id="31c7c-156">Enter the **Database Name** to create a database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-156">Enter the **Database Name** to create a database.</span></span> <span data-ttu-id="31c7c-157">If there is a database with the same name that already exists in the target Azure Data Lake Analytics account, all objects that are defined in the database project are created without recreating the database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-157">If there is a database with the same name that already exists in the target Azure Data Lake Analytics account, all objects that are defined in the database project are created without recreating the database.</span></span>

    ![Data Lake Tools for Visual Studio--Deploy U-SQL database package](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-deploy-usql-database-package.png)

    ![Data Lake Tools for Visual Studio--Deploy U-SQL database package wizard](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-deploy-usql-database-package-wizard.png)
  
### <a name="deploy-u-sql-database-by-using-the-sdk"></a><span data-ttu-id="31c7c-160">Deploy U-SQL database by using the SDK</span><span class="sxs-lookup"><span data-stu-id="31c7c-160">Deploy U-SQL database by using the SDK</span></span>

<span data-ttu-id="31c7c-161">`PackageDeploymentTool.exe` provides the programming and command-line interfaces that help to deploy U-SQL databases.</span><span class="sxs-lookup"><span data-stu-id="31c7c-161">`PackageDeploymentTool.exe` provides the programming and command-line interfaces that help to deploy U-SQL databases.</span></span> <span data-ttu-id="31c7c-162">The SDK is included in the [U-SQL SDK Nuget package](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/), located at `build/runtime/PackageDeploymentTool.exe`.</span><span class="sxs-lookup"><span data-stu-id="31c7c-162">The SDK is included in the [U-SQL SDK Nuget package](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/), located at `build/runtime/PackageDeploymentTool.exe`.</span></span>

<span data-ttu-id="31c7c-163">[Learn more about the SDK and how to set up CI/CD pipeline for U-SQL database deployment](data-lake-analytics-cicd-overview.md#deploy-u-sql-database-through-azure-devops).</span><span class="sxs-lookup"><span data-stu-id="31c7c-163">[Learn more about the SDK and how to set up CI/CD pipeline for U-SQL database deployment](data-lake-analytics-cicd-overview.md#deploy-u-sql-database-through-azure-devops).</span></span>

## <a name="reference-a-u-sql-database-project"></a><span data-ttu-id="31c7c-164">Reference a U-SQL database project</span><span class="sxs-lookup"><span data-stu-id="31c7c-164">Reference a U-SQL database project</span></span>

<span data-ttu-id="31c7c-165">A U-SQL project can reference a U-SQL database project.</span><span class="sxs-lookup"><span data-stu-id="31c7c-165">A U-SQL project can reference a U-SQL database project.</span></span> <span data-ttu-id="31c7c-166">The reference affects two workloads:</span><span class="sxs-lookup"><span data-stu-id="31c7c-166">The reference affects two workloads:</span></span>

- <span data-ttu-id="31c7c-167">*Project build*: Set up the referenced database environments before building the U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="31c7c-167">*Project build*: Set up the referenced database environments before building the U-SQL scripts.</span></span> 
- <span data-ttu-id="31c7c-168">*Local run against (a local-project) account*: The referenced database environments are deployed to (a local-project) account before U-SQL script execution.</span><span class="sxs-lookup"><span data-stu-id="31c7c-168">*Local run against (a local-project) account*: The referenced database environments are deployed to (a local-project) account before U-SQL script execution.</span></span> <span data-ttu-id="31c7c-169">[Learn more about local runs and the difference between (the local-machine) and (a local-project) account here](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="31c7c-169">[Learn more about local runs and the difference between (the local-machine) and (a local-project) account here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

### <a name="how-to-add-a-u-sql-database-reference"></a><span data-ttu-id="31c7c-170">How to add a U-SQL database reference</span><span class="sxs-lookup"><span data-stu-id="31c7c-170">How to add a U-SQL database reference</span></span>

1. <span data-ttu-id="31c7c-171">Right-click the U-SQL project in **Solution Explorer**, and then choose **Add U-SQL Database Reference...**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-171">Right-click the U-SQL project in **Solution Explorer**, and then choose **Add U-SQL Database Reference...**.</span></span>

    ![Data Lake Tools for Visual Studio -- add database project reference](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-add-database-project-reference.png)

2. <span data-ttu-id="31c7c-173">Configure a database reference from a U-SQL database project in the current solution or in a U-SQL database package file.</span><span class="sxs-lookup"><span data-stu-id="31c7c-173">Configure a database reference from a U-SQL database project in the current solution or in a U-SQL database package file.</span></span>
3. <span data-ttu-id="31c7c-174">Provide the name for the database.</span><span class="sxs-lookup"><span data-stu-id="31c7c-174">Provide the name for the database.</span></span>

    ![Data Lake Tools for Visual Studio add database project reference wizard](./media/data-lake-analytics-data-lake-tools-develop-usql-database/data-lake-tools-add-database-project-reference-wizard.png)

## <a name="next-steps"></a><span data-ttu-id="31c7c-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="31c7c-176">Next steps</span></span>

- [<span data-ttu-id="31c7c-177">How to set up a CI/CD pipeline for Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="31c7c-177">How to set up a CI/CD pipeline for Azure Data Lake Analytics</span></span>](data-lake-analytics-cicd-overview.md)
- [<span data-ttu-id="31c7c-178">How to test your Azure Data Lake Analytics code</span><span class="sxs-lookup"><span data-stu-id="31c7c-178">How to test your Azure Data Lake Analytics code</span></span>](data-lake-analytics-cicd-test.md)
- [<span data-ttu-id="31c7c-179">Run U-SQL script on your local machine</span><span class="sxs-lookup"><span data-stu-id="31c7c-179">Run U-SQL script on your local machine</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
