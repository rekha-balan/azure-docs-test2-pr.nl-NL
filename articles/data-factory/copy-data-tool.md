---
title: Copy Data tool Azure Data Factory | Microsoft Docs
description: Provides information about the Copy Data tool in Azure Data Factory UI
services: data-factory
documentationcenter: ''
author: dearandyxu
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 06/18/2018
ms.author: yexu
ms.openlocfilehash: 8941ec26cef5e3dc2f17faf0d7eb843b76f8926f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856733"
---
# <a name="copy-data-tool-in-azure-data-factory"></a><span data-ttu-id="d6fa1-103">Copy Data tool in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d6fa1-103">Copy Data tool in Azure Data Factory</span></span>
<span data-ttu-id="d6fa1-104">The Azure Data Factory Copy Data tool eases and optimizes the process of ingesting data into a data lake, which is usually a first step in an end-to-end data integration scenario.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-104">The Azure Data Factory Copy Data tool eases and optimizes the process of ingesting data into a data lake, which is usually a first step in an end-to-end data integration scenario.</span></span>  <span data-ttu-id="d6fa1-105">It saves time, especially when you use Azure Data Factory to ingest data from a data source for the first time.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-105">It saves time, especially when you use Azure Data Factory to ingest data from a data source for the first time.</span></span> <span data-ttu-id="d6fa1-106">Some of the benefits of using this tool are:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-106">Some of the benefits of using this tool are:</span></span>

- <span data-ttu-id="d6fa1-107">When using the Azure Data Factory Copy Data tool, you do not need understand Data Factory definitions for linked services, datasets, pipelines, activities, and triggers.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-107">When using the Azure Data Factory Copy Data tool, you do not need understand Data Factory definitions for linked services, datasets, pipelines, activities, and triggers.</span></span> 
- <span data-ttu-id="d6fa1-108">The flow of Copy Data tool is intuitive for loading data into a data lake.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-108">The flow of Copy Data tool is intuitive for loading data into a data lake.</span></span> <span data-ttu-id="d6fa1-109">The tool automatically creates all the necessary Data Factory resources to copy data from the selected source data store to the selected destination/sink data store.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-109">The tool automatically creates all the necessary Data Factory resources to copy data from the selected source data store to the selected destination/sink data store.</span></span> 
- <span data-ttu-id="d6fa1-110">The Copy Data tool helps you validate the data that is being ingested at the time of authoring, which helps you avoid any potential errors at the beginning itself.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-110">The Copy Data tool helps you validate the data that is being ingested at the time of authoring, which helps you avoid any potential errors at the beginning itself.</span></span>
- <span data-ttu-id="d6fa1-111">If you need to implement complex business logic to load data into a data lake, you can still edit the Data Factory resources created by the Copy Data tool by using the per-activity authoring in Data Factory UI.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-111">If you need to implement complex business logic to load data into a data lake, you can still edit the Data Factory resources created by the Copy Data tool by using the per-activity authoring in Data Factory UI.</span></span> 

<span data-ttu-id="d6fa1-112">The following table provides guidance on when to use the Copy Data tool vs. per-activity authoring in Data Factory UI:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-112">The following table provides guidance on when to use the Copy Data tool vs. per-activity authoring in Data Factory UI:</span></span> 

| <span data-ttu-id="d6fa1-113">Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="d6fa1-113">Copy Data tool</span></span> | <span data-ttu-id="d6fa1-114">Per activity (Copy activity) authoring</span><span class="sxs-lookup"><span data-stu-id="d6fa1-114">Per activity (Copy activity) authoring</span></span> |
| -------------- | -------------------------------------- |
| <span data-ttu-id="d6fa1-115">You want to easily build a data loading task without learning about Azure Data Factory entities (linked services, datasets, pipelines, etc.)</span><span class="sxs-lookup"><span data-stu-id="d6fa1-115">You want to easily build a data loading task without learning about Azure Data Factory entities (linked services, datasets, pipelines, etc.)</span></span> | <span data-ttu-id="d6fa1-116">You want to implement complex and flexible logic for loading data into lake.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-116">You want to implement complex and flexible logic for loading data into lake.</span></span> |
| <span data-ttu-id="d6fa1-117">You want to quickly load a large number of data artifacts into a data lake.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-117">You want to quickly load a large number of data artifacts into a data lake.</span></span> | <span data-ttu-id="d6fa1-118">You want to chain Copy activity with subsequent activities for cleansing or processing data.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-118">You want to chain Copy activity with subsequent activities for cleansing or processing data.</span></span> |

<span data-ttu-id="d6fa1-119">To start the Copy Data tool, click the **Copy Data** tile on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-119">To start the Copy Data tool, click the **Copy Data** tile on the home page of your data factory.</span></span>

![Get started page - link to Copy Data tool](./media/copy-data-tool/get-started-page.png)


## <a name="intuitive-flow-for-loading-data-into-a-data-lake"></a><span data-ttu-id="d6fa1-121">Intuitive flow for loading data into a data lake</span><span class="sxs-lookup"><span data-stu-id="d6fa1-121">Intuitive flow for loading data into a data lake</span></span>
<span data-ttu-id="d6fa1-122">This tool allows you to easily move data from a wide variety of sources to destinations in minutes with an intuitive flow:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-122">This tool allows you to easily move data from a wide variety of sources to destinations in minutes with an intuitive flow:</span></span>  

1. <span data-ttu-id="d6fa1-123">Configure settings for the **source**.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-123">Configure settings for the **source**.</span></span>
2. <span data-ttu-id="d6fa1-124">Configure settings for the **destination**.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-124">Configure settings for the **destination**.</span></span> 
3. <span data-ttu-id="d6fa1-125">Configure **advanced settings** for the copy operation such as column mapping, performance settings, and fault tolerance settings.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-125">Configure **advanced settings** for the copy operation such as column mapping, performance settings, and fault tolerance settings.</span></span> 
4. <span data-ttu-id="d6fa1-126">Specify a **schedule** for the data loading task.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-126">Specify a **schedule** for the data loading task.</span></span> 
5. <span data-ttu-id="d6fa1-127">Review **summary** of Data Factory entities to be created.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-127">Review **summary** of Data Factory entities to be created.</span></span> 
6. <span data-ttu-id="d6fa1-128">**Edit** the pipeline to update settings for the copy activity as needed.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-128">**Edit** the pipeline to update settings for the copy activity as needed.</span></span> 

 <span data-ttu-id="d6fa1-129">The tool is designed with big data in mind from the start, with support for diverse data and object types.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-129">The tool is designed with big data in mind from the start, with support for diverse data and object types.</span></span> <span data-ttu-id="d6fa1-130">You can use it to move hundreds of folders, files, or tables.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-130">You can use it to move hundreds of folders, files, or tables.</span></span> <span data-ttu-id="d6fa1-131">The tool supports automatic data preview, schema capture and automatic mapping, and data filtering as well.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-131">The tool supports automatic data preview, schema capture and automatic mapping, and data filtering as well.</span></span>

![Copy Data tool](./media/copy-data-tool/copy-data-tool.png)

## <a name="automatic-data-preview"></a><span data-ttu-id="d6fa1-133">Automatic data preview</span><span class="sxs-lookup"><span data-stu-id="d6fa1-133">Automatic data preview</span></span>
<span data-ttu-id="d6fa1-134">You can preview part of the data from the selected source data store, which allows you to validate the data that is being copied.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-134">You can preview part of the data from the selected source data store, which allows you to validate the data that is being copied.</span></span> <span data-ttu-id="d6fa1-135">In addition, if the source data is in a text file, the Copy Data tool parses the text file to automatically detect the row and column delimiters, and schema.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-135">In addition, if the source data is in a text file, the Copy Data tool parses the text file to automatically detect the row and column delimiters, and schema.</span></span>

![File settings](./media/copy-data-tool/file-format-settings.png)

<span data-ttu-id="d6fa1-137">After the detection:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-137">After the detection:</span></span>

![Detected file settings and preview](./media/copy-data-tool/after-detection.png)

## <a name="schema-capture-and-automatic-mapping"></a><span data-ttu-id="d6fa1-139">Schema capture and automatic mapping</span><span class="sxs-lookup"><span data-stu-id="d6fa1-139">Schema capture and automatic mapping</span></span>
<span data-ttu-id="d6fa1-140">The schema of data source may not be same as the schema of data destination in many cases.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-140">The schema of data source may not be same as the schema of data destination in many cases.</span></span> <span data-ttu-id="d6fa1-141">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-141">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span>

<span data-ttu-id="d6fa1-142">The Copy Data tool monitors and learns your behavior when you are mapping columns between source and destination stores.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-142">The Copy Data tool monitors and learns your behavior when you are mapping columns between source and destination stores.</span></span> <span data-ttu-id="d6fa1-143">After you pick one or a few columns from source data store, and map them to the destination schema, the Copy Data tool starts to analyze the pattern for column pairs you picked from both sides.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-143">After you pick one or a few columns from source data store, and map them to the destination schema, the Copy Data tool starts to analyze the pattern for column pairs you picked from both sides.</span></span> <span data-ttu-id="d6fa1-144">Then, it applies the same pattern to the rest of the columns.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-144">Then, it applies the same pattern to the rest of the columns.</span></span> <span data-ttu-id="d6fa1-145">Therefore, you see all the columns have been mapped to the destination in a way you want just after several clicks.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-145">Therefore, you see all the columns have been mapped to the destination in a way you want just after several clicks.</span></span>  <span data-ttu-id="d6fa1-146">If you are not satisfied with the choice of column mapping provided by Copy Data tool, you can ignore it and continue with manually mapping the columns.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-146">If you are not satisfied with the choice of column mapping provided by Copy Data tool, you can ignore it and continue with manually mapping the columns.</span></span> <span data-ttu-id="d6fa1-147">Meanwhile, the Copy Data tool constantly learns and updates the pattern, and ultimately reaches the right pattern for the column mapping you want to achieve.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-147">Meanwhile, the Copy Data tool constantly learns and updates the pattern, and ultimately reaches the right pattern for the column mapping you want to achieve.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6fa1-148">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if the table does not exist in the destination store, Copy Data tool supports creation of the table automatically by using the source schema.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-148">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if the table does not exist in the destination store, Copy Data tool supports creation of the table automatically by using the source schema.</span></span> 

## <a name="filter-data"></a><span data-ttu-id="d6fa1-149">Filter data</span><span class="sxs-lookup"><span data-stu-id="d6fa1-149">Filter data</span></span>
<span data-ttu-id="d6fa1-150">You can filter source data to select only the data that needs to be copied to the sink data store.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-150">You can filter source data to select only the data that needs to be copied to the sink data store.</span></span> <span data-ttu-id="d6fa1-151">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-151">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="d6fa1-152">Copy Data tool provides a flexible way to filter data in a relational database by using the SQL query language, or files in an Azure blob folder.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-152">Copy Data tool provides a flexible way to filter data in a relational database by using the SQL query language, or files in an Azure blob folder.</span></span> 

### <a name="filter-data-in-a-database"></a><span data-ttu-id="d6fa1-153">Filter data in a database</span><span class="sxs-lookup"><span data-stu-id="d6fa1-153">Filter data in a database</span></span>
<span data-ttu-id="d6fa1-154">The following screenshot shows a SQL query to filter the data.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-154">The following screenshot shows a SQL query to filter the data.</span></span>

![Filter data in a database](./media/copy-data-tool/filter-data-in-database.png)

### <a name="filter-data-in-an-azure-blob-folder"></a><span data-ttu-id="d6fa1-156">Filter data in an Azure blob folder</span><span class="sxs-lookup"><span data-stu-id="d6fa1-156">Filter data in an Azure blob folder</span></span>
<span data-ttu-id="d6fa1-157">You can use variables in the folder path to copy data from a folder.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-157">You can use variables in the folder path to copy data from a folder.</span></span> <span data-ttu-id="d6fa1-158">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, and **{minute}**.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-158">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, and **{minute}**.</span></span> <span data-ttu-id="d6fa1-159">For example: inputfolder/{year}/{month}/{day}.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-159">For example: inputfolder/{year}/{month}/{day}.</span></span> 

<span data-ttu-id="d6fa1-160">Suppose that you have input folders in the following format:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-160">Suppose that you have input folders in the following format:</span></span> 

```
2016/03/01/01
2016/03/01/02
2016/03/01/03
...
```

<span data-ttu-id="d6fa1-161">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-161">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="d6fa1-162">You should see 2016/03/01/02 in the text box.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-162">You should see 2016/03/01/02 in the text box.</span></span> 

<span data-ttu-id="d6fa1-163">Then, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press the **Tab** key.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-163">Then, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press the **Tab** key.</span></span> <span data-ttu-id="d6fa1-164">You should see drop-down lists to select the format for these four variables:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-164">You should see drop-down lists to select the format for these four variables:</span></span>

![Filter file or folder](./media/copy-data-tool/filter-file-or-folder.png)

<span data-ttu-id="d6fa1-166">The Copy Data tool generates parameters with expressions, functions, and system variables that can be used to represent {year}, {month}, {day}, {hour}, and {minute} when creating pipeline.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-166">The Copy Data tool generates parameters with expressions, functions, and system variables that can be used to represent {year}, {month}, {day}, {hour}, and {minute} when creating pipeline.</span></span> <span data-ttu-id="d6fa1-167">For more information, see the [How to read or write partitioned data](how-to-read-write-partitioned-data.md) article.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-167">For more information, see the [How to read or write partitioned data](how-to-read-write-partitioned-data.md) article.</span></span>

## <a name="scheduling-options"></a><span data-ttu-id="d6fa1-168">Scheduling options</span><span class="sxs-lookup"><span data-stu-id="d6fa1-168">Scheduling options</span></span>
<span data-ttu-id="d6fa1-169">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span><span class="sxs-lookup"><span data-stu-id="d6fa1-169">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="d6fa1-170">These options can be used for the connectors across different environments, including on-premises, cloud, and local desktop.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-170">These options can be used for the connectors across different environments, including on-premises, cloud, and local desktop.</span></span> 

<span data-ttu-id="d6fa1-171">A one-time copy operation enables data movement from a source to a destination only once.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-171">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="d6fa1-172">It applies to data of any size and any supported format.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-172">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="d6fa1-173">The scheduled copy allows you to copy data on a recurrence that you specify.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-173">The scheduled copy allows you to copy data on a recurrence that you specify.</span></span> <span data-ttu-id="d6fa1-174">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span><span class="sxs-lookup"><span data-stu-id="d6fa1-174">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![Scheduling options](./media/copy-data-tool/scheduling-options.png)


## <a name="next-steps"></a><span data-ttu-id="d6fa1-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6fa1-176">Next steps</span></span>
<span data-ttu-id="d6fa1-177">Try these tutorials that use the Copy Data tool:</span><span class="sxs-lookup"><span data-stu-id="d6fa1-177">Try these tutorials that use the Copy Data tool:</span></span>

- [<span data-ttu-id="d6fa1-178">Quickstart: create a data factory using the Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="d6fa1-178">Quickstart: create a data factory using the Copy Data tool</span></span>](quickstart-create-data-factory-copy-data-tool.md)
- [<span data-ttu-id="d6fa1-179">Tutorial: copy data in Azure using the Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="d6fa1-179">Tutorial: copy data in Azure using the Copy Data tool</span></span>](tutorial-copy-data-tool.md) 
- [<span data-ttu-id="d6fa1-180">Tutorial: copy on-premises data to Azure using the Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="d6fa1-180">Tutorial: copy on-premises data to Azure using the Copy Data tool</span></span>](tutorial-hybrid-copy-data-tool.md)
