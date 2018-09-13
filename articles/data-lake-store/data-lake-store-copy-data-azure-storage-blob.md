---
title: Copy data from Azure Storage Blobs into Data Lake Store| Microsoft Docs
description: Use AdlCopy tool to copy data from Azure Storage Blobs to Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: nitinme
ms.openlocfilehash: ffbfbd2d5e3389a5898ad60a15b5c34070d4a1dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552501"
---
# <a name="copy-data-from-azure-storage-blobs-to-data-lake-store"></a>Copy data from Azure Storage Blobs to Data Lake Store
> [!div class="op_single_selector"]
> * [Using DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Using AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
> 
> 

Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), to copy data from the following sources:

* From Azure Storage Blobs into Data Lake Store. You cannot use AdlCopy to copy data from Data Lake Store to Azure Storage blobs.
* Between two Azure Data Lake Store accounts. 

Also, you can use the AdlCopy tool in two different modes:

* **Standalone**, where the tool uses Data Lake Store resources to perform the task.
* **Using a Data Lake Analytics account**, where the units assigned to your Data Lake Analytics account are used to perform the copy operation. You might want to use this option when you are looking to perform the copy tasks in a predictable manner.

## <a name="prerequisites"></a>Prerequisites
Before you begin this article, you must have the following:

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Storage Blobs** container with some data.
* **An Azure Data Lake Store account**. For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how to create a Data Lake Store account.
* **AdlCopy tool**. Install the AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-the-adlcopy-tool"></a>Syntax of the AdlCopy tool
Use the following syntax to work with the AdlCopy tool

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern 

The parameters in the syntax are described below:

| Option | Description |
| --- | --- |
| Source |Specifies the location of the source data in the Azure storage blob. The source can be a blob container, a blob, or another Data Lake Store account. |
| Dest |Specifies the Data Lake Store destination to copy to. |
| SourceKey |Specifies the storage access key for the Azure storage blob source. This is required only if the source is a blob container or a blob. |
| Account |**Optional**. Use this if you want to use Azure Data Lake Analytics account to run the copy job. If you use the /Account option in the syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account to run the job. Also, if you use this option, you must add the source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account. |
| Units |Specifies the number of Data Lake Analytics units that will be used for the copy job. This option is mandatory if you use the **/Account** option to specify the Data Lake Analytics account. |
| Pattern |Specifies a regex pattern that indicates which blobs or files to copy. AdlCopy uses case-sensitive matching. The default pattern used when no pattern is specified is to copy all items. Specifying multiple file patterns is not supported. |

## <a name="use-adlcopy-as-standalone-to-copy-data-from-an-azure-storage-blob"></a>Use AdlCopy (as standalone) to copy data from an Azure Storage blob
1. Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.
2. Run the following command to copy a specific blob from the source container to a Data Lake Store:
   
        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>
   
    For example:
   
        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] The syntax above specifies the file to be copied to a folder in the Data Lake Store account. AdlCopy tool creates a folder if the specified folder name does not exist.

    You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account. You will see an output similar to the following:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. You can also copy all the blobs from one container to the Data Lake Store account using the following command:
   
        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        
   
    For example:
   
        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Performance considerations

If you are copying from an Azure Blob Storage account, you may be throttled during copy on the blob storage side. This will degrade the performance of your copy job. To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-to-copy-data-from-another-data-lake-store-account"></a>Use AdlCopy (as standalone) to copy data from another Data Lake Store account
You can also use AdlCopy to copy data between two Data Lake Store accounts.

1. Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.
2. Run the following command to copy a specific file from one Data Lake Store account to another.
   
        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/
   
    For example:
   
        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/
   
   > [!NOTE]
   > The syntax above specifies the file to be copied to a folder in the destination Data Lake Store account. AdlCopy tool creates a folder if the specified folder name does not exist.
   > 
   > 
   
    You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account. You will see an output similar to the following:
   
        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. The following command copies all files from a specific folder in the source Data Lake Store account to a folder in the destination Data Lake Store account.
   
        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Performance considerations

When using AdlCopy as a standalone tool, the copy is run on shared, Azure managed resources. The performance you may get in this environment depends on system load and available resources. This mode is best used for small transfers on an ad hoc basis. No parameters need to be tuned when using AdlCopy as a standalone tool.

## <a name="use-adlcopy-with-data-lake-analytics-account-to-copy-data"></a>Use AdlCopy (with Data Lake Analytics account) to copy data
You can also use your Data Lake Analytics account to run the AdlCopy job to copy data from Azure storage blobs to Data Lake Store. You would typically use this option when the data to be moved is in the range of gigabytes and terabytes, and you want better and predictable performance throughput.

To use your Data Lake Analytics account with AdlCopy to copy from an Azure Storage Blob, the source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account. For instructions on adding additional data sources to your Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-account-data-sources).

> [!NOTE]
> If you are copying from an Azure Data Lake Store account as the source using a Data Lake Analytics account, you do not need to associate the Data Lake Store account with the Data Lake Analytics account. The requirement to associate the source store with the Data Lake Analytics account is only when the source is an Azure Storage account.
> 
> 

Run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

For example:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Similarly, run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Performance considerations

When copying data in the range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance. The parameter that should be tuned is the number of Azure Data Lake Analytics Units to use for the copy job. Increasing the number of units will increase the performance of your copy job. Each file to be copied can use maximum one unit. Specifying more units than the number of files being copied will not increase performance.

## <a name="use-adlcopy-to-copy-data-using-pattern-matching"></a>Use AdlCopy to copy data using pattern matching
In this section, you learn how to use AdlCopy to copy data from a source (in our example below we use Azure Storage Blob) to a destination Data Lake Store account using pattern matching. For example, you can use the steps below to copy all files with .csv extension from the source blob to the destination.

1. Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.
2. Run the following command to copy all files with *.csv extension from a specific blob from the source container to a Data Lake Store:
   
        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv
   
    For example:
   
        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Billing
* If you use the AdlCopy tool as standalone you will be billed for egress costs for moving data, if the source Azure Storage account is not in the same region as the Data Lake Store.
* If you use the AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.

## <a name="considerations-for-using-adlcopy"></a>Considerations for using AdlCopy
* AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders. However, if you encounter issues copying a large dataset, you can distribute the files/folders into different sub-folders and use the path to those sub-folders as the source instead.

## <a name="performance-considerations-for-using-adlcopy"></a>Performance considerations for using AdlCopy

AdlCopy supports copying data containing thousands of files and folders. However, if you encounter issues copying a large dataset, you can distribute the files/folders into smaller sub-folders. AdlCopy was built for ad hoc copies. If you are trying to copy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around the copy operations.

## <a name="next-steps"></a>Next steps
* [Secure data in Data Lake Store](data-lake-store-secure-data.md)
* [Use Azure Data Lake Analytics with Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Use Azure HDInsight with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
