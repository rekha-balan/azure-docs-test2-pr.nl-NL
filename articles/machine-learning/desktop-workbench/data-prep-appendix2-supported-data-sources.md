---
title: Supported data sources available with Azure Machine Learning data preparation  | Microsoft Docs
description: This document provides a complete list of supported data sources available for Azure Machine Learning data preparation.
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 88ed4fa43e5724cfe1d6f1555db947d77045cd2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865724"
---
# <a name="supported-data-sources-for-azure-machine-learning-data-preparation"></a>Supported data sources for Azure Machine Learning data preparation 
This article outlines the currently supported data sources for Azure Machine Learning data preparation.

The supported data sources for this release are as follows.

## <a name="types"></a>Types 

### <a name="sql-server"></a>SQL Server
Read from on-prem SQL server or Azure SQL database.

#### <a name="options"></a>Options
- Server Address
- Trust Server (Even when the certificate on the server is not valid. Use with caution)
- Authentication Type (Windows, Server)
- User Name
- Password
- Database to connect to
- SQL Query

#### <a name="notes"></a>Notes
- Sql-variant columns are not supported
- Time column is converted to datetime by appending time from database to date 1970/1/1
- When executed on Spark cluster, all data related columns (date, datetime, datetime2, datetimeoffset) will evaluate incorrect values for dates before 1583
- Values in decimal columns may lose precision due to conversion to decimal

### <a name="directory-vs-file"></a>Directory vs. file
Choose a single file and read it into data preparation. The file type is parsed to determine the default parameters for the file connection shown on the next screen.

Choose a directory or a set of files within a directory (the file picker is multiselect). With either approach, the files are read in as a single data flow and are appended to each other, with headers stripped out if needed.

The supported file types are:
- Delimited (.csv, .tsv, .txt, etc.)
- Fixed width
- Plain text
- JSON file

### <a name="csv-file"></a>CSV file
Read a comma-separated-value file from storage.

#### <a name="options"></a>Options
- Separator
- Comment
- Headers
- Decimal symbol
- File encoding
- Lines to skip

### <a name="tsv-file"></a>TSV file
Read a tab-separated-value file from storage.

#### <a name="options"></a>Options
- Comment
- Headers
- File encoding
- Lines to skip

### <a name="excel-xlsxlsx"></a>Excel (.xls/.xlsx)
Read an Excel file one sheet at a time by specifying sheet name or number.

#### <a name="options"></a>Options
- Sheet name or number
- Headers
- Lines to skip

### <a name="json-file"></a>JSON file
Read a JSON file from storage. The file is "flattened" on read.

#### <a name="options"></a>Options
- None

### <a name="parquet"></a>Parquet
Read a Parquet data set, either a single file or a folder.

Parquet as a format can take various forms in storage. For smaller data sets, a single .parquet file is sometimes used. Various Python libraries support reading or writing to single .parquet files. For the moment, Azure Machine Learning data preparation relies on the PyArrow Python library for reading Parquet during local interactive use. It supports single .parquet files (as long as they were written as such, and not as part of a larger data set), as well as Parquet data sets.

A Parquet data set is a collection of more than one .parquet file, each of which represents a smaller partition of a larger data set. Data sets are usually contained in a folder and are the default parquet output format for platforms such as Spark and Hive.

>[!NOTE]
>When you're reading Parquet data that's in a folder with multiple .parquet files, it's safest to select the directory for reading, and the **Parquet data set** option. This makes PyArrow read the whole folder instead of the individual files. This ensures support for reading more complicated ways of storing Parquet on disk, such as folder partitioning.

Scale-out execution relies on Spark's Parquet reading capabilities and supports single files as well as folders, similar to local interactive use.

#### <a name="options"></a>Options
- Parquet data set. This option determines whether Azure Machine Learning data preparation expands a given directory and attempts to read each file individually (the unselected mode), or whether it treats the directory as the whole data set (the selected mode). With the selected mode, PyArrow chooses the best way to interpret the files.


## <a name="locations"></a>Locations
### <a name="local"></a>Local
A local hard drive or a mapped network storage location.

### <a name="sql-server"></a>SQL Server
On-prem SQL sever, or Azure SQL database.

### <a name="azure-blob-storage"></a>Azure Blob storage
Azure Blob storage, which requires an Azure subscription.

