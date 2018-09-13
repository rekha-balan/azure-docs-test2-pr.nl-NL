---
title: Copy data easily with Copy Wizard - Azure | Microsoft Docs
description: Learn about how to use the Data Factory Copy Wizard to copy data from supported data sources to sinks.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: ''
editor: ''
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 8b74a431664faa95e8be9c9ff90970fd6e7c0ec7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855882"
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a><span data-ttu-id="ffd76-103">Copy or move data easily with Azure Data Factory Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="ffd76-103">Copy or move data easily with Azure Data Factory Copy Wizard</span></span>
> [!NOTE]
> <span data-ttu-id="ffd76-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ffd76-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="ffd76-105">If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="ffd76-105">If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md).</span></span> 


<span data-ttu-id="ffd76-106">The Azure Data Factory Copy Wizard is to ease the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span><span class="sxs-lookup"><span data-stu-id="ffd76-106">The Azure Data Factory Copy Wizard is to ease the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="ffd76-107">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, datasets, and pipelines.</span><span class="sxs-lookup"><span data-stu-id="ffd76-107">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="ffd76-108">However, after you complete all the steps in the wizard, the wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span><span class="sxs-lookup"><span data-stu-id="ffd76-108">However, after you complete all the steps in the wizard, the wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="ffd76-109">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring, which saves much of your time, especially when you are ingesting data for the first time from the data source.</span><span class="sxs-lookup"><span data-stu-id="ffd76-109">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring, which saves much of your time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="ffd76-110">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="ffd76-110">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![Copy Wizard](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a><span data-ttu-id="ffd76-112">An intuitive wizard for copying data</span><span class="sxs-lookup"><span data-stu-id="ffd76-112">An intuitive wizard for copying data</span></span>
<span data-ttu-id="ffd76-113">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span><span class="sxs-lookup"><span data-stu-id="ffd76-113">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="ffd76-114">After going through the wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets).</span><span class="sxs-lookup"><span data-stu-id="ffd76-114">After going through the wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets).</span></span> <span data-ttu-id="ffd76-115">No additional steps are required to create the pipeline.</span><span class="sxs-lookup"><span data-stu-id="ffd76-115">No additional steps are required to create the pipeline.</span></span>   

![Select data source](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="ffd76-117">See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table.</span><span class="sxs-lookup"><span data-stu-id="ffd76-117">See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table.</span></span> 
> 
> 

<span data-ttu-id="ffd76-118">The wizard is designed with big data in mind from the start.</span><span class="sxs-lookup"><span data-stu-id="ffd76-118">The wizard is designed with big data in mind from the start.</span></span> <span data-ttu-id="ffd76-119">It is simple and efficient to author Data Factory pipelines that move hundreds of folders, files, or tables using the Copy Data wizard.</span><span class="sxs-lookup"><span data-stu-id="ffd76-119">It is simple and efficient to author Data Factory pipelines that move hundreds of folders, files, or tables using the Copy Data wizard.</span></span> <span data-ttu-id="ffd76-120">The wizard supports the following three features: Automatic data preview, schema capture and mapping, and filtering data.</span><span class="sxs-lookup"><span data-stu-id="ffd76-120">The wizard supports the following three features: Automatic data preview, schema capture and mapping, and filtering data.</span></span> 

## <a name="automatic-data-preview"></a><span data-ttu-id="ffd76-121">Automatic data preview</span><span class="sxs-lookup"><span data-stu-id="ffd76-121">Automatic data preview</span></span>
<span data-ttu-id="ffd76-122">The copy wizard allows you to review part of the data from the selected data source for you to validate whether the data it is the right data you want to copy.</span><span class="sxs-lookup"><span data-stu-id="ffd76-122">The copy wizard allows you to review part of the data from the selected data source for you to validate whether the data it is the right data you want to copy.</span></span> <span data-ttu-id="ffd76-123">In addition, if the source data is in a text file, the copy wizard parses the text file to learn row and column delimiters, and schema automatically.</span><span class="sxs-lookup"><span data-stu-id="ffd76-123">In addition, if the source data is in a text file, the copy wizard parses the text file to learn row and column delimiters, and schema automatically.</span></span> 

![File format settings](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="ffd76-125">Schema capture and mapping</span><span class="sxs-lookup"><span data-stu-id="ffd76-125">Schema capture and mapping</span></span>
<span data-ttu-id="ffd76-126">The schema of input data may not match the schema of output data in some cases.</span><span class="sxs-lookup"><span data-stu-id="ffd76-126">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="ffd76-127">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span><span class="sxs-lookup"><span data-stu-id="ffd76-127">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span> 

<span data-ttu-id="ffd76-128">The copy wizard automatically maps columns in the source schema to columns in the destination schema.</span><span class="sxs-lookup"><span data-stu-id="ffd76-128">The copy wizard automatically maps columns in the source schema to columns in the destination schema.</span></span> <span data-ttu-id="ffd76-129">You can override the mappings by using the drop-down lists (or) specify whether a column needs to be skipped while copying the data.</span><span class="sxs-lookup"><span data-stu-id="ffd76-129">You can override the mappings by using the drop-down lists (or) specify whether a column needs to be skipped while copying the data.</span></span>   

![Schema mapping](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="ffd76-131">Filtering data</span><span class="sxs-lookup"><span data-stu-id="ffd76-131">Filtering data</span></span>
<span data-ttu-id="ffd76-132">The wizard allows you to filter source data to select only the data that needs to be copied to the destination/sink data store.</span><span class="sxs-lookup"><span data-stu-id="ffd76-132">The wizard allows you to filter source data to select only the data that needs to be copied to the destination/sink data store.</span></span> <span data-ttu-id="ffd76-133">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span><span class="sxs-lookup"><span data-stu-id="ffd76-133">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="ffd76-134">It provides a flexible way to filter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="ffd76-134">It provides a flexible way to filter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="ffd76-135">Filtering of data in a database</span><span class="sxs-lookup"><span data-stu-id="ffd76-135">Filtering of data in a database</span></span>
<span data-ttu-id="ffd76-136">In the example, the SQL query uses the `Text.Format` function and `WindowStart` variable.</span><span class="sxs-lookup"><span data-stu-id="ffd76-136">In the example, the SQL query uses the `Text.Format` function and `WindowStart` variable.</span></span> 

![Validate expressions](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="ffd76-138">Filtering of data in an Azure blob folder</span><span class="sxs-lookup"><span data-stu-id="ffd76-138">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="ffd76-139">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="ffd76-139">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="ffd76-140">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span><span class="sxs-lookup"><span data-stu-id="ffd76-140">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="ffd76-141">Example: inputfolder/{year}/{month}/{day}.</span><span class="sxs-lookup"><span data-stu-id="ffd76-141">Example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="ffd76-142">Suppose that you have input folders in the following format:</span><span class="sxs-lookup"><span data-stu-id="ffd76-142">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="ffd76-143">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span><span class="sxs-lookup"><span data-stu-id="ffd76-143">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="ffd76-144">You should see `2016/03/01/02` in the text box.</span><span class="sxs-lookup"><span data-stu-id="ffd76-144">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="ffd76-145">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab. You should see drop-down lists to select the format for these four variables:</span><span class="sxs-lookup"><span data-stu-id="ffd76-145">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab. You should see drop-down lists to select the format for these four variables:</span></span>

![Using system variables](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="ffd76-147">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffd76-147">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="ffd76-148">To select a folder with that structure, use the **Browse** button first.</span><span class="sxs-lookup"><span data-stu-id="ffd76-148">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="ffd76-149">Then replace a value with **{custom}**, and press Tab to see the text box where you can type the format string.</span><span class="sxs-lookup"><span data-stu-id="ffd76-149">Then replace a value with **{custom}**, and press Tab to see the text box where you can type the format string.</span></span>     

![Using custom variable](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a><span data-ttu-id="ffd76-151">Support for diverse data and object types</span><span class="sxs-lookup"><span data-stu-id="ffd76-151">Support for diverse data and object types</span></span>
<span data-ttu-id="ffd76-152">By using the Copy Wizard, you can efficiently move hundreds of folders, files, or tables.</span><span class="sxs-lookup"><span data-stu-id="ffd76-152">By using the Copy Wizard, you can efficiently move hundreds of folders, files, or tables.</span></span>

![Select tables from which to copy data](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a><span data-ttu-id="ffd76-154">Scheduling options</span><span class="sxs-lookup"><span data-stu-id="ffd76-154">Scheduling options</span></span>
<span data-ttu-id="ffd76-155">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span><span class="sxs-lookup"><span data-stu-id="ffd76-155">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="ffd76-156">Both of these options can be used for the breadth of the connectors across on-premises, cloud, and local desktop copy.</span><span class="sxs-lookup"><span data-stu-id="ffd76-156">Both of these options can be used for the breadth of the connectors across on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="ffd76-157">A one-time copy operation enables data movement from a source to a destination only once.</span><span class="sxs-lookup"><span data-stu-id="ffd76-157">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="ffd76-158">It applies to data of any size and any supported format.</span><span class="sxs-lookup"><span data-stu-id="ffd76-158">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="ffd76-159">The scheduled copy allows you to copy data on a prescribed recurrence.</span><span class="sxs-lookup"><span data-stu-id="ffd76-159">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="ffd76-160">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span><span class="sxs-lookup"><span data-stu-id="ffd76-160">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![Scheduling properties](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="ffd76-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffd76-162">Next steps</span></span>
<span data-ttu-id="ffd76-163">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ffd76-163">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

