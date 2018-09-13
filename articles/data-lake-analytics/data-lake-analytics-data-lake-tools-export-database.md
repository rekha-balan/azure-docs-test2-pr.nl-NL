---
title: Export a U-SQL database using Azure Data Lake Tools for Visual Studio
description: Learn how to use Azure Data Lake Tools for Visual Studio to export a U-SQL database and automatically import it to a local account.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.topic: conceptual
ms.date: 11/27/2017
ms.openlocfilehash: e4eea3cb4b16460c7e17bb6575c4e6cf8dda5a0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871102"
---
# <a name="export-a-u-sql-database"></a><span data-ttu-id="4813c-103">Export a U-SQL database</span><span class="sxs-lookup"><span data-stu-id="4813c-103">Export a U-SQL database</span></span>

<span data-ttu-id="4813c-104">In this article, learn how to use [Azure Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs) to export a U-SQL database as a single U-SQL script and downloaded resources.</span><span class="sxs-lookup"><span data-stu-id="4813c-104">In this article, learn how to use [Azure Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs) to export a U-SQL database as a single U-SQL script and downloaded resources.</span></span> <span data-ttu-id="4813c-105">You can import the exported database to a local account in the same process.</span><span class="sxs-lookup"><span data-stu-id="4813c-105">You can import the exported database to a local account in the same process.</span></span>

<span data-ttu-id="4813c-106">Customers usually maintain multiple environments for development, test, and production.</span><span class="sxs-lookup"><span data-stu-id="4813c-106">Customers usually maintain multiple environments for development, test, and production.</span></span> <span data-ttu-id="4813c-107">These environments are hosted on both a local account, on a developer's local computer, and in an Azure Data Lake Analytics account in Azure.</span><span class="sxs-lookup"><span data-stu-id="4813c-107">These environments are hosted on both a local account, on a developer's local computer, and in an Azure Data Lake Analytics account in Azure.</span></span> 

<span data-ttu-id="4813c-108">When you develop and tune U-SQL queries in development and test environments, developers often need to re-create their work in a production database.</span><span class="sxs-lookup"><span data-stu-id="4813c-108">When you develop and tune U-SQL queries in development and test environments, developers often need to re-create their work in a production database.</span></span> <span data-ttu-id="4813c-109">The Database Export Wizard helps accelerate this process.</span><span class="sxs-lookup"><span data-stu-id="4813c-109">The Database Export Wizard helps accelerate this process.</span></span> <span data-ttu-id="4813c-110">By using the wizard, developers can clone the existing database environment and sample data to other Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="4813c-110">By using the wizard, developers can clone the existing database environment and sample data to other Data Lake Analytics accounts.</span></span>

## <a name="export-steps"></a><span data-ttu-id="4813c-111">Export steps</span><span class="sxs-lookup"><span data-stu-id="4813c-111">Export steps</span></span>

### <a name="step-1-export-the-database-in-server-explorer"></a><span data-ttu-id="4813c-112">Step 1: Export the database in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="4813c-112">Step 1: Export the database in Server Explorer</span></span>

<span data-ttu-id="4813c-113">All Data Lake Analytics accounts that you have permissions for are listed in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="4813c-113">All Data Lake Analytics accounts that you have permissions for are listed in Server Explorer.</span></span> <span data-ttu-id="4813c-114">To export the database:</span><span class="sxs-lookup"><span data-stu-id="4813c-114">To export the database:</span></span>

1. <span data-ttu-id="4813c-115">In Server Explorer, expand the account that contains the database that you want to export.</span><span class="sxs-lookup"><span data-stu-id="4813c-115">In Server Explorer, expand the account that contains the database that you want to export.</span></span>
2. <span data-ttu-id="4813c-116">Right-click the database, and then select **Export**.</span><span class="sxs-lookup"><span data-stu-id="4813c-116">Right-click the database, and then select **Export**.</span></span> 
   
    ![Server Explorer - Export a database](./media/data-lake-analytics-data-lake-tools-export-database/export-database.png)

     <span data-ttu-id="4813c-118">If the **Export** menu option isn't available, you need to [update the tool to the lasted release](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="4813c-118">If the **Export** menu option isn't available, you need to [update the tool to the lasted release](http://aka.ms/adltoolsvs).</span></span>

### <a name="step-2-configure-the-objects-that-you-want-to-export"></a><span data-ttu-id="4813c-119">Step 2: Configure the objects that you want to export</span><span class="sxs-lookup"><span data-stu-id="4813c-119">Step 2: Configure the objects that you want to export</span></span>

<span data-ttu-id="4813c-120">If you need only a small part of a large database, you can configure a subset of objects that you want to export in the export wizard.</span><span class="sxs-lookup"><span data-stu-id="4813c-120">If you need only a small part of a large database, you can configure a subset of objects that you want to export in the export wizard.</span></span> 

<span data-ttu-id="4813c-121">The export action is completed by running a U-SQL job.</span><span class="sxs-lookup"><span data-stu-id="4813c-121">The export action is completed by running a U-SQL job.</span></span> <span data-ttu-id="4813c-122">Therefore, exporting from an Azure account incurs some cost.</span><span class="sxs-lookup"><span data-stu-id="4813c-122">Therefore, exporting from an Azure account incurs some cost.</span></span>

![Database Export Wizard - Select export objects](./media/data-lake-analytics-data-lake-tools-export-database/export-database-wizard.png)

### <a name="step-3-check-the-objects-list-and-other-configurations"></a><span data-ttu-id="4813c-124">Step 3: Check the objects list and other configurations</span><span class="sxs-lookup"><span data-stu-id="4813c-124">Step 3: Check the objects list and other configurations</span></span>

<span data-ttu-id="4813c-125">In this step, you can verify the selected objects in the **Export object list** box.</span><span class="sxs-lookup"><span data-stu-id="4813c-125">In this step, you can verify the selected objects in the **Export object list** box.</span></span> <span data-ttu-id="4813c-126">If there are any errors, select **Previous** to go back and correctly configure the objects that you want to export.</span><span class="sxs-lookup"><span data-stu-id="4813c-126">If there are any errors, select **Previous** to go back and correctly configure the objects that you want to export.</span></span>

<span data-ttu-id="4813c-127">You can also configure other settings for the export target.</span><span class="sxs-lookup"><span data-stu-id="4813c-127">You can also configure other settings for the export target.</span></span> <span data-ttu-id="4813c-128">Configuration descriptions are listed in the following table:</span><span class="sxs-lookup"><span data-stu-id="4813c-128">Configuration descriptions are listed in the following table:</span></span>

|<span data-ttu-id="4813c-129">Configuration</span><span class="sxs-lookup"><span data-stu-id="4813c-129">Configuration</span></span>|<span data-ttu-id="4813c-130">Description</span><span class="sxs-lookup"><span data-stu-id="4813c-130">Description</span></span>|
|-------------|-----------|
|<span data-ttu-id="4813c-131">Destination Name</span><span class="sxs-lookup"><span data-stu-id="4813c-131">Destination Name</span></span>|<span data-ttu-id="4813c-132">This name indicates where you want to save the exported database resources.</span><span class="sxs-lookup"><span data-stu-id="4813c-132">This name indicates where you want to save the exported database resources.</span></span> <span data-ttu-id="4813c-133">Examples are assemblies, additional files, and sample data.</span><span class="sxs-lookup"><span data-stu-id="4813c-133">Examples are assemblies, additional files, and sample data.</span></span> <span data-ttu-id="4813c-134">A folder with this name is created under your local data root folder.</span><span class="sxs-lookup"><span data-stu-id="4813c-134">A folder with this name is created under your local data root folder.</span></span>|
|<span data-ttu-id="4813c-135">Project Directory</span><span class="sxs-lookup"><span data-stu-id="4813c-135">Project Directory</span></span>|<span data-ttu-id="4813c-136">This path defines where you want to save the exported U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="4813c-136">This path defines where you want to save the exported U-SQL script.</span></span> <span data-ttu-id="4813c-137">All database object definitions are saved at this location.</span><span class="sxs-lookup"><span data-stu-id="4813c-137">All database object definitions are saved at this location.</span></span>|
|<span data-ttu-id="4813c-138">Schema Only</span><span class="sxs-lookup"><span data-stu-id="4813c-138">Schema Only</span></span>|<span data-ttu-id="4813c-139">If you select this option, only database definitions and resources (like assemblies and additional files) are exported.</span><span class="sxs-lookup"><span data-stu-id="4813c-139">If you select this option, only database definitions and resources (like assemblies and additional files) are exported.</span></span>|
|<span data-ttu-id="4813c-140">Schema and Data</span><span class="sxs-lookup"><span data-stu-id="4813c-140">Schema and Data</span></span>|<span data-ttu-id="4813c-141">If you select this option, database definitions, resources, and data are exported.</span><span class="sxs-lookup"><span data-stu-id="4813c-141">If you select this option, database definitions, resources, and data are exported.</span></span> <span data-ttu-id="4813c-142">The top N rows of tables are exported.</span><span class="sxs-lookup"><span data-stu-id="4813c-142">The top N rows of tables are exported.</span></span>|
|<span data-ttu-id="4813c-143">Import to Local Database Automatically</span><span class="sxs-lookup"><span data-stu-id="4813c-143">Import to Local Database Automatically</span></span>|<span data-ttu-id="4813c-144">If you select this option, the exported database is automatically imported to your local database when exporting is finished.</span><span class="sxs-lookup"><span data-stu-id="4813c-144">If you select this option, the exported database is automatically imported to your local database when exporting is finished.</span></span>|

![Database Export Wizard - Export objects list and other configurations](./media/data-lake-analytics-data-lake-tools-export-database/export-database-wizard-configuration.png)

### <a name="step-4-check-the-export-results"></a><span data-ttu-id="4813c-146">Step 4: Check the export results</span><span class="sxs-lookup"><span data-stu-id="4813c-146">Step 4: Check the export results</span></span>

<span data-ttu-id="4813c-147">When exporting is finished, you can view the exported results in the log window in the wizard.</span><span class="sxs-lookup"><span data-stu-id="4813c-147">When exporting is finished, you can view the exported results in the log window in the wizard.</span></span> <span data-ttu-id="4813c-148">The following example shows how to find exported U-SQL script and database resources, including assemblies, additional files, and sample data:</span><span class="sxs-lookup"><span data-stu-id="4813c-148">The following example shows how to find exported U-SQL script and database resources, including assemblies, additional files, and sample data:</span></span>

![Database Export Wizard - Export results](./media/data-lake-analytics-data-lake-tools-export-database/export-database-wizard-completed.png)

## <a name="import-the-exported-database-to-a-local-account"></a><span data-ttu-id="4813c-150">Import the exported database to a local account</span><span class="sxs-lookup"><span data-stu-id="4813c-150">Import the exported database to a local account</span></span>

<span data-ttu-id="4813c-151">The most convenient way to import the exported database is to select the **Import to Local Database Automatically** check box during the exporting process in Step 3.</span><span class="sxs-lookup"><span data-stu-id="4813c-151">The most convenient way to import the exported database is to select the **Import to Local Database Automatically** check box during the exporting process in Step 3.</span></span> <span data-ttu-id="4813c-152">If you didn't check this box, first, find the exported U-SQL script in the export log.</span><span class="sxs-lookup"><span data-stu-id="4813c-152">If you didn't check this box, first, find the exported U-SQL script in the export log.</span></span> <span data-ttu-id="4813c-153">Then, run the U-SQL script locally to import the database to your local account.</span><span class="sxs-lookup"><span data-stu-id="4813c-153">Then, run the U-SQL script locally to import the database to your local account.</span></span>

## <a name="import-the-exported-database-to-a-data-lake-analytics-account"></a><span data-ttu-id="4813c-154">Import the exported database to a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="4813c-154">Import the exported database to a Data Lake Analytics account</span></span>

<span data-ttu-id="4813c-155">To import the database to different Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="4813c-155">To import the database to different Data Lake Analytics account:</span></span>

1. <span data-ttu-id="4813c-156">Upload the exported resources, including assemblies, additional files, and sample data, to the default Azure Data Lake Store account of the Data Lake Analytics account that you want to import to.</span><span class="sxs-lookup"><span data-stu-id="4813c-156">Upload the exported resources, including assemblies, additional files, and sample data, to the default Azure Data Lake Store account of the Data Lake Analytics account that you want to import to.</span></span> <span data-ttu-id="4813c-157">You can find the exported resource folder under the local data root folder.</span><span class="sxs-lookup"><span data-stu-id="4813c-157">You can find the exported resource folder under the local data root folder.</span></span> <span data-ttu-id="4813c-158">Upload the entire folder to the root of the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4813c-158">Upload the entire folder to the root of the default Data Lake Store account.</span></span>
2. <span data-ttu-id="4813c-159">When uploading is finished, submit the exported U-SQL script to the Data Lake Analytics account that you want to import the database to.</span><span class="sxs-lookup"><span data-stu-id="4813c-159">When uploading is finished, submit the exported U-SQL script to the Data Lake Analytics account that you want to import the database to.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="4813c-160">Known limitations</span><span class="sxs-lookup"><span data-stu-id="4813c-160">Known limitations</span></span>

<span data-ttu-id="4813c-161">Currently, if you select the **Schema and Data** option in Step 3, the tool runs a U-SQL job to export the data stored in tables.</span><span class="sxs-lookup"><span data-stu-id="4813c-161">Currently, if you select the **Schema and Data** option in Step 3, the tool runs a U-SQL job to export the data stored in tables.</span></span> <span data-ttu-id="4813c-162">Because of this, the data exporting process might be slow and you might incur costs.</span><span class="sxs-lookup"><span data-stu-id="4813c-162">Because of this, the data exporting process might be slow and you might incur costs.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4813c-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="4813c-163">Next steps</span></span>

* [<span data-ttu-id="4813c-164">Learn about U-SQL databases</span><span class="sxs-lookup"><span data-stu-id="4813c-164">Learn about U-SQL databases</span></span>](https://msdn.microsoft.com/library/azure/mt621299.aspx) 
* [<span data-ttu-id="4813c-165">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="4813c-165">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>](data-lake-analytics-data-lake-tools-local-run.md)


