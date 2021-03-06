---
title: Register data from Data Lake Store in Azure Data Catalog | Microsoft Docs
description: Register data from Data Lake Store in Azure Data Catalog
services: data-lake-store,data-catalog
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: e5174ba0e67fd99bde3fd10bfcd6248d2148828d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564123"
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Register data from Data Lake Store in Azure Data Catalog
In this article you will learn how to integrate Azure Data Lake Store with Azure Data Catalog to make your data discoverable within an organization by integrating it with Data Catalog. For more information on cataloging data, see [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md). To understand scenarios in which you can use Data Catalog, see [Azure Data Catalog common scenarios](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Prerequisites
Before you begin this tutorial, you must have the following:

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **Enable your Azure subscription** for Data Lake Store Public Preview. See [instructions](data-lake-store-get-started-portal.md).
* **Azure Data Lake Store account**. Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md). For this tutorial, let us create a Data Lake Store account called **datacatalogstore**.

    Once you have created the account, upload a sample data set to it. For this tutorial, let us upload all the .csv files under the **AmbulanceData** folder in the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.
* **Azure Data Catalog**. Your organization must already have an Azure Data Catalog created for your organization. Only one catalog is allowed for each organization.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Register Data Lake Store as a source for Data Catalog

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Go to `https://azure.microsoft.com/services/data-catalog`, and click **Get started**.
2. Log into the Azure Data Catalog portal, and click **Publish data**.

    ![Register a data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/register-data-source.png "Register a data source")
3. On the next page, click **Launch Application**. This will download the application manifest file on your computer. Double-click the manifest file to start the application.
4. On the Welcome page, click **Sign in**, and enter your credentials.

    ![Welcome screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/welcome.screen.png "Welcome screen")
5. On the Select a Data Source page, select **Azure Data Lake**, and then click **Next**.

    ![Select data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/select-source.png "Select data source")
6. On the next page, provide the Data Lake Store account name that you want to register in Data Catalog. Leave the other options as default and then click **Connect**.

    ![Connect to data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/connect-to-source.png "Connect to data source")
7. The next page can be divided into the following segments.

    a. The **Server Hierarchy** box represents the Data Lake Store account folder structure. **$Root** represents the Data Lake Store account root, and **AmbulanceData** represents the folder created in the root of the Data Lake Store account.

    b. The **Available objects** box lists the files and folders under the **AmbulanceData** folder.

    c. **Objects to be registered box** lists the files and folders that you want to register in Azure Data Catalog.

    ![View data structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/view-data-structure.png "View data structure")
8. For this tutorial, you should register all the files in the directory. For that, click the (![move objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/move-objects.png "Move objects")) button to move all the files to **Objects to be registered** box.

    Because the data will be registered in an organization-wide data catalog, it is a recommened approach to add some metadata which you can later use to quickly locate the data. For example, you can add an e-mail address for the data owner (for example, one who is uploading the data) or add a tag to identify the data. The screen capture below shows a tag that we add to the data.

    ![View data structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/view-selected-data-structure.png "View data structure")

    Click **Register**.
9. The following screen capture denotes that the data is successfully registered in the Data Catalog.

    ![Registration complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/registration-complete.png "View data structure")
10. Click **View Portal** to go back to the Data Catalog portal and verify that you can now access the registered data from the portal. To search the data, you can use the tag you used while registering the data.

     ![Search data in catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Search data in catalog")
11. You can now perform operations like adding annotations and documentation to the data. For more information, see the following links.

    * [Annotate data sources in Data Catalog](../data-catalog/data-catalog-how-to-annotate.md)
    * [Document data sources in Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>See also
* [Annotate data sources in Data Catalog](../data-catalog/data-catalog-how-to-annotate.md)
* [Document data sources in Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)
* [Integrate Data Lake Store with other Azure services](data-lake-store-integrate-with-other-services.md)









