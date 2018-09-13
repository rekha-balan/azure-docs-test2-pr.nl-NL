---
title: Use command-line interface to get started with Azure Data Lake Store | Microsoft Docs
description: Use Azure cross-platform command line to create a Data Lake Store account and perform basic operations
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 380788f3-041d-4ae5-b6be-37ca74ca333d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/17/2017
ms.author: nitinme
ms.openlocfilehash: f7748dba30c6e0332c166feda25f4aaa93c06efa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554197"
---
# <a name="get-started-with-azure-data-lake-store-using-azure-command-line"></a>Get started with Azure Data Lake Store using Azure Command Line
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Learn how to use Azure command line interface to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).

The Azure CLI is implemented in Node.js. It can be used on any platform that supports Node.js, including Windows, Mac, and Linux. The Azure CLI is open source. The source code is managed in GitHub at <a href= "https://github.com/azure/azure-xplat-cli">https://github.com/azure/azure-xplat-cli</a>. This article covers only using the Azure CLI with Data Lake Store. For a general guide on how to use Azure CLI, see [How to use the Azure CLI][azure-command-line-tools].


> [!NOTE]
> For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md). These options have better performance as they use multiple threads to parallelize the data movement.
> 
>

## <a name="prerequisites"></a>Prerequisites
Before you begin this article, you must have the following:

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information. Make sure you reboot your computer after you install the CLI.

## <a name="authentication"></a>Authentication

This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user. The access level to Data Lake Store account and file system is then governed by the access level of the logged in user. However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**. For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="login-to-your-azure-subscription"></a>Login to your Azure subscription

1. Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the `azure login` method.

2. List the subscriptions that are associated with your account using the `azure account list` command.
   
        info:    Executing command account list
        data:    Name              Id                                    Current
        data:    ----------------  ------------------------------------  -------
        data:    Azure-sub-1       ####################################  true
        data:    Azure-sub-2       ####################################  false
   
    From the output above, **Azure-sub-1** is currently enabled, and the other subscription is **Azure-sub-2**. 
3. Select the subscription you want to work under. If you want to work under the Azure-sub-2 subscription, use the `azure account set` command.
   
        azure account set Azure-sub-2

## <a name="create-an-azure-data-lake-store-account"></a>Create an Azure Data Lake Store account
Open a command prompt, shell, or a terminal session and run the following commands.

1. Switch to Azure Resource Manager mode using the following command:
   
        azure config mode arm
2. Create a new resource group. In the following command, provide the parameter values you want to use.
   
        azure group create <resourceGroup> <location>
   
    If the location name contains spaces, put it in quotes. For example "East US 2".
3. Create the Data Lake Store account.
   
        azure datalake store account create <dataLakeStoreAccountName> <location> <resourceGroup>

## <a name="create-folders-in-your-data-lake-store"></a>Create folders in your Data Lake Store
You can create folders under your Azure Data Lake Store account to manage and store data. Use the following command to create a folder called "mynewfolder" at the root of the Data Lake Store.

    azure datalake store filesystem create <dataLakeStoreAccountName> <path> --folder

For example:

    azure datalake store filesystem create mynewdatalakestore /mynewfolder --folder

## <a name="upload-data-to-your-data-lake-store"></a>Upload data to your Data Lake Store
You can upload your data to Data Lake Store directly at the root level or to a folder that you created within the account. The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.

If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Download the file and store it in a local directory on your computer, such as  C:\sampledata\.

    azure datalake store filesystem import <dataLakeStoreAccountName> "<source path>" "<destination path>"

For example:

    azure datalake store filesystem import mynewdatalakestore "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" "/mynewfolder/vehicle1_09142014.csv"


## <a name="list-files-in-data-lake-store"></a>List files in Data Lake Store
Use the following command to list the files in a Data Lake Store account.

    azure datalake store filesystem list <dataLakeStoreAccountName> <path>

For example:

    azure datalake store filesystem list mynewdatalakestore /mynewfolder

The output of this should be similar to the following:

    info:    Executing command datalake store filesystem list
    data:    accessTime: 1446245025257
    data:    blockSize: 268435456
    data:    group: NotSupportYet
    data:    length: 1589881
    data:    modificationTime: 1446245105763
    data:    owner: NotSupportYet
    data:    pathSuffix: vehicle1_09142014.csv
    data:    permission: 777
    data:    replication: 0
    data:    type: FILE
    data:    ------------------------------------------------------------------------------------
    info:    datalake store filesystem list command OK

## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Rename, download, and delete data from your Data Lake Store
* **To rename a file**, use the following command:
  
        azure datalake store filesystem move <dataLakeStoreAccountName> <path/old_file_name> <path/new_file_name>
  
    For example:
  
        azure datalake store filesystem move mynewdatalakestore /mynewfolder/vehicle1_09142014.csv /mynewfolder/vehicle1_09142014_copy.csv
* **To download a file**, use the following command. Make sure the destination path you specify already exists.
  
        azure datalake store filesystem export <dataLakeStoreAccountName> <source_path> <destination_path>
  
    For example:
  
        azure datalake store filesystem export mynewdatalakestore /mynewfolder/vehicle1_09142014_copy.csv "C:\mysampledata\vehicle1_09142014_copy.csv"
* **To delete a file**, use the following command:
  
        azure datalake store filesystem delete <dataLakeStoreAccountName> <path>
  
    For example:
  
        azure datalake store filesystem delete mynewdatalakestore /mynewfolder/vehicle1_09142014_copy.csv
  
    When prompted, enter **Y** to delete the item.

## <a name="view-the-access-control-list-for-a-folder-in-data-lake-store"></a>View the access control list for a folder in Data Lake Store
Use the following command to view the ACLs on a Data Lake Store folder. In the current release, ACLs can be set only on the root of the Data Lake Store. So, the path parameter below will always be root (/).

    azure datalake store permissions show <dataLakeStoreName> <path>

For example:

    azure datalake store permissions show mynewdatalakestore /


## <a name="delete-your-data-lake-store-account"></a>Delete your Data Lake Store account
Use the following command to delete a Data Lake Store account.

    azure datalake store account delete <dataLakeStoreAccountName>

For example:

    azure datalake store account delete mynewdatalakestore

When prompted, enter **Y** to delete the account.

## <a name="next-steps"></a>Next steps
* [Secure data in Data Lake Store](data-lake-store-secure-data.md)
* [Use Azure Data Lake Analytics with Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Use Azure HDInsight with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../cli-install-nodejs.md
