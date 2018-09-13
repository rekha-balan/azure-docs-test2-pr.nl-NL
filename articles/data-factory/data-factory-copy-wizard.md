---
title: Copy data easily with Copy Wizard - Azure | Microsoft Docs
description: Learn about how to use the Data Factory Copy Wizard to copy data from supported data sources to sinks.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: spelluru
ms.openlocfilehash: 0ee8344a73ad02e926edd10caebc9d71caa0cf67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553440"
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Copy or move data easily with Azure Data Factory Copy Wizard
The Azure Data Factory Copy Wizard is to ease the process of ingesting data, which is usually a first step in an end-to-end data integration scenario. When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, datasets, and pipelines. However, after you complete all the steps in the wizard, the wizard automatically creates a pipeline to copy data from the selected data source to the selected destination. In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring, which saves much of your time, especially when you are ingesting data for the first time from the data source. To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.

![Copy Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>An intuitive wizard for copying data
This wizard allows you to easily move data from a wide variety of sources to destinations in minutes. After going through the wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets). No additional steps are required to create the pipeline.   

![Select data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table. 
> 
> 

The wizard is designed with big data in mind from the start. It is simple and efficient to author Data Factory pipelines that move hundreds of folders, files, or tables using the Copy Data wizard. The wizard supports the following three features: Automatic data preview, schema capture and mapping, and filtering data. 

## <a name="automatic-data-preview"></a>Automatic data preview
The copy wizard allows you to review part of the data from the selected data source for you to validate whether the data it is the right data you want to copy. In addition, if the source data is in a text file, the copy wizard parses the text file to learn row and column delimiters, and schema automatically. 

![File format settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Schema capture and mapping
The schema of input data may not match the schema of output data in some cases. In this scenario, you need to map columns from the source schema to columns from the destination schema. 

The copy wizard automatically maps columns in the source schema to columns in the destination schema. You can override the mappings by using the drop-down lists (or) specify whether a column needs to be skipped while copying the data.   

![Schema mapping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtering data
The wizard allows you to filter source data to select only the data that needs to be copied to the destination/sink data store. Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation. It provides a flexible way to filter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtering of data in a database
In the example, the SQL query uses the `Text.Format` function and `WindowStart` variable. 

![Validate expressions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtering of data in an Azure blob folder
You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables). The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**. Example: inputfolder/{year}/{month}/{day}.

Suppose that you have input folders in the following format:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**. You should see `2016/03/01/02` in the text box. Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab. You should see drop-down lists to select the format for these four variables:

![Using system variables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx). To select a folder with that structure, use the **Browse** button first. Then replace a value with **{custom}**, and press Tab to see the text box where you can type the format string.     

![Using custom variable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Support for diverse data and object types
By using the Copy Wizard, you can efficiently move hundreds of folders, files, or tables.

![Select tables from which to copy data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Scheduling options
You can run the copy operation once or on a schedule (hourly, daily, and so on). Both of these options can be used for the breadth of the connectors across on-premises, cloud, and local desktop copy.

A one-time copy operation enables data movement from a source to a destination only once. It applies to data of any size and any supported format. The scheduled copy allows you to copy data on a prescribed recurrence. You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.

![Scheduling properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Next steps
For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).










