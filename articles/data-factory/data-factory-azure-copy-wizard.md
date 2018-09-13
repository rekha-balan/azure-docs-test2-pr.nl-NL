---
title: Data Factory Azure Copy Wizard | Microsoft Docs
description: Learn about how to use the Data Factory Azure Copy Wizard to copy data from supported data sources to sinks.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: spelluru
ms.openlocfilehash: 318fa0bbeb8fa7ea99b959379bf0b56cf7b6af12
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540649"
---
# <a name="azure-data-factory-copy-wizard"></a><span data-ttu-id="120f6-103">Azure Data Factory Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="120f6-103">Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="120f6-104">The Azure Data Factory Copy Wizard eases the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span><span class="sxs-lookup"><span data-stu-id="120f6-104">The Azure Data Factory Copy Wizard eases the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="120f6-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, data sets, and pipelines.</span><span class="sxs-lookup"><span data-stu-id="120f6-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, data sets, and pipelines.</span></span> <span data-ttu-id="120f6-106">The wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span><span class="sxs-lookup"><span data-stu-id="120f6-106">The wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="120f6-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring.</span><span class="sxs-lookup"><span data-stu-id="120f6-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring.</span></span> <span data-ttu-id="120f6-108">This saves time, especially when you are ingesting data for the first time from the data source.</span><span class="sxs-lookup"><span data-stu-id="120f6-108">This saves time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="120f6-109">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="120f6-109">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![Copy Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a><span data-ttu-id="120f6-111">Designed for big data</span><span class="sxs-lookup"><span data-stu-id="120f6-111">Designed for big data</span></span>
<span data-ttu-id="120f6-112">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span><span class="sxs-lookup"><span data-stu-id="120f6-112">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="120f6-113">After you go through the wizard, a pipeline with a copy activity is automatically created for you, along with dependent Data Factory entities (linked services and data sets).</span><span class="sxs-lookup"><span data-stu-id="120f6-113">After you go through the wizard, a pipeline with a copy activity is automatically created for you, along with dependent Data Factory entities (linked services and data sets).</span></span> <span data-ttu-id="120f6-114">No additional steps are required to create the pipeline.</span><span class="sxs-lookup"><span data-stu-id="120f6-114">No additional steps are required to create the pipeline.</span></span>   

![Select data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="120f6-116">For step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table, see the [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="120f6-116">For step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table, see the [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md).</span></span>
>
>

<span data-ttu-id="120f6-117">The wizard is designed with big data in mind from the start, with support for diverse data and object types.</span><span class="sxs-lookup"><span data-stu-id="120f6-117">The wizard is designed with big data in mind from the start, with support for diverse data and object types.</span></span> <span data-ttu-id="120f6-118">You can author Data Factory pipelines that move hundreds of folders, files, or tables.</span><span class="sxs-lookup"><span data-stu-id="120f6-118">You can author Data Factory pipelines that move hundreds of folders, files, or tables.</span></span> <span data-ttu-id="120f6-119">The wizard supports automatic data preview, schema capture and mapping, and data filtering.</span><span class="sxs-lookup"><span data-stu-id="120f6-119">The wizard supports automatic data preview, schema capture and mapping, and data filtering.</span></span>

## <a name="automatic-data-preview"></a><span data-ttu-id="120f6-120">Automatic data preview</span><span class="sxs-lookup"><span data-stu-id="120f6-120">Automatic data preview</span></span>
<span data-ttu-id="120f6-121">You can preview part of the data from the selected data source in order to validate whether the data is what you want to copy.</span><span class="sxs-lookup"><span data-stu-id="120f6-121">You can preview part of the data from the selected data source in order to validate whether the data is what you want to copy.</span></span> <span data-ttu-id="120f6-122">In addition, if the source data is in a text file, the Copy Wizard parses the text file to learn the row and column delimiters and schema automatically.</span><span class="sxs-lookup"><span data-stu-id="120f6-122">In addition, if the source data is in a text file, the Copy Wizard parses the text file to learn the row and column delimiters and schema automatically.</span></span>

![File format settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="120f6-124">Schema capture and mapping</span><span class="sxs-lookup"><span data-stu-id="120f6-124">Schema capture and mapping</span></span>
<span data-ttu-id="120f6-125">The schema of input data may not match the schema of output data in some cases.</span><span class="sxs-lookup"><span data-stu-id="120f6-125">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="120f6-126">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span><span class="sxs-lookup"><span data-stu-id="120f6-126">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span>

> [!TIP]
> <span data-ttu-id="120f6-127">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory support auto table creation using source's schema.</span><span class="sxs-lookup"><span data-stu-id="120f6-127">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory support auto table creation using source's schema.</span></span> <span data-ttu-id="120f6-128">Learn more from [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).</span><span class="sxs-lookup"><span data-stu-id="120f6-128">Learn more from [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).</span></span>
>

<span data-ttu-id="120f6-129">Use a drop-down list to select a column from the source schema to map to a column in the destination schema.</span><span class="sxs-lookup"><span data-stu-id="120f6-129">Use a drop-down list to select a column from the source schema to map to a column in the destination schema.</span></span> <span data-ttu-id="120f6-130">The Copy Wizard tries to understand your pattern for column mapping.</span><span class="sxs-lookup"><span data-stu-id="120f6-130">The Copy Wizard tries to understand your pattern for column mapping.</span></span> <span data-ttu-id="120f6-131">It applies the same pattern to the rest of the columns, so that you do not need to select each of the columns individually to complete the schema mapping.</span><span class="sxs-lookup"><span data-stu-id="120f6-131">It applies the same pattern to the rest of the columns, so that you do not need to select each of the columns individually to complete the schema mapping.</span></span> <span data-ttu-id="120f6-132">If you prefer, you can override these mappings by using the drop-down lists to map the columns one by one.</span><span class="sxs-lookup"><span data-stu-id="120f6-132">If you prefer, you can override these mappings by using the drop-down lists to map the columns one by one.</span></span> <span data-ttu-id="120f6-133">The pattern becomes more accurate as you map more columns.</span><span class="sxs-lookup"><span data-stu-id="120f6-133">The pattern becomes more accurate as you map more columns.</span></span> <span data-ttu-id="120f6-134">The Copy Wizard constantly updates the pattern, and ultimately reaches the right pattern for the column mapping you want to achieve.</span><span class="sxs-lookup"><span data-stu-id="120f6-134">The Copy Wizard constantly updates the pattern, and ultimately reaches the right pattern for the column mapping you want to achieve.</span></span>     

![Schema mapping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="120f6-136">Filtering data</span><span class="sxs-lookup"><span data-stu-id="120f6-136">Filtering data</span></span>
<span data-ttu-id="120f6-137">You can filter source data to select only the data that needs to be copied to the sink data store.</span><span class="sxs-lookup"><span data-stu-id="120f6-137">You can filter source data to select only the data that needs to be copied to the sink data store.</span></span> <span data-ttu-id="120f6-138">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span><span class="sxs-lookup"><span data-stu-id="120f6-138">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="120f6-139">It provides a flexible way to filter data in a relational database by using the SQL query language, or files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="120f6-139">It provides a flexible way to filter data in a relational database by using the SQL query language, or files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="120f6-140">Filtering of data in a database</span><span class="sxs-lookup"><span data-stu-id="120f6-140">Filtering of data in a database</span></span>
<span data-ttu-id="120f6-141">The following screenshot shows a SQL query using the `Text.Format` function and `WindowStart` variable.</span><span class="sxs-lookup"><span data-stu-id="120f6-141">The following screenshot shows a SQL query using the `Text.Format` function and `WindowStart` variable.</span></span>

![Validate expressions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="120f6-143">Filtering of data in an Azure blob folder</span><span class="sxs-lookup"><span data-stu-id="120f6-143">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="120f6-144">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="120f6-144">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="120f6-145">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span><span class="sxs-lookup"><span data-stu-id="120f6-145">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="120f6-146">For example: inputfolder/{year}/{month}/{day}.</span><span class="sxs-lookup"><span data-stu-id="120f6-146">For example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="120f6-147">Suppose that you have input folders in the following format:</span><span class="sxs-lookup"><span data-stu-id="120f6-147">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="120f6-148">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span><span class="sxs-lookup"><span data-stu-id="120f6-148">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="120f6-149">You should see `2016/03/01/02` in the text box.</span><span class="sxs-lookup"><span data-stu-id="120f6-149">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="120f6-150">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press the **Tab** key.</span><span class="sxs-lookup"><span data-stu-id="120f6-150">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press the **Tab** key.</span></span> <span data-ttu-id="120f6-151">You should see drop-down lists to select the format for these four variables:</span><span class="sxs-lookup"><span data-stu-id="120f6-151">You should see drop-down lists to select the format for these four variables:</span></span>

![Using system variables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="120f6-153">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span><span class="sxs-lookup"><span data-stu-id="120f6-153">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="120f6-154">To select a folder with that structure, use the **Browse** button first.</span><span class="sxs-lookup"><span data-stu-id="120f6-154">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="120f6-155">Then replace a value with **{custom}**, and press the **Tab** key to see the text box where you can type the format string.</span><span class="sxs-lookup"><span data-stu-id="120f6-155">Then replace a value with **{custom}**, and press the **Tab** key to see the text box where you can type the format string.</span></span>     

![Using custom variable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a><span data-ttu-id="120f6-157">Scheduling options</span><span class="sxs-lookup"><span data-stu-id="120f6-157">Scheduling options</span></span>
<span data-ttu-id="120f6-158">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span><span class="sxs-lookup"><span data-stu-id="120f6-158">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="120f6-159">Both of these options can be used for the breadth of the connectors across environments, including on-premises, cloud, and local desktop copy.</span><span class="sxs-lookup"><span data-stu-id="120f6-159">Both of these options can be used for the breadth of the connectors across environments, including on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="120f6-160">A one-time copy operation enables data movement from a source to a destination only once.</span><span class="sxs-lookup"><span data-stu-id="120f6-160">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="120f6-161">It applies to data of any size and any supported format.</span><span class="sxs-lookup"><span data-stu-id="120f6-161">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="120f6-162">The scheduled copy allows you to copy data on a prescribed recurrence.</span><span class="sxs-lookup"><span data-stu-id="120f6-162">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="120f6-163">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span><span class="sxs-lookup"><span data-stu-id="120f6-163">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![Scheduling properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="120f6-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="120f6-165">Next steps</span></span>
<span data-ttu-id="120f6-166">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="120f6-166">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>








