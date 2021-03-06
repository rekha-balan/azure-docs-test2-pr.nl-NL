---
title: Azure Data Lake Store cross-region migration | Microsoft Docs
description: Learn about cross-region migration for Azure Data Lake Store.
services: data-lake-store
documentationcenter: ''
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 34b449b251672619aec6e86b9343343a9404126a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564111"
---
# <a name="migrate-data-lake-store-across-regions"></a>Migrate Data Lake Store across regions

As Azure Data Lake Store becomes available in new regions, you might choose to do a one-time migration, to take advantage of the new region. Learn what to consider as you plan and complete the migration.

## <a name="prerequisites"></a>Prerequisites

* **An Azure subscription**. For more information, see [Create your free Azure account today](https://azure.microsoft.com/pricing/free-trial/).
* **A Data Lake Store account in two different regions**. For more information, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. For more information, see [Introduction to Azure Data Factory](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Migration considerations

First, identify the migration strategy that works best for your application that writes, reads, or processes data in Data Lake Store. When you choose a strategy, consider your application’s availability requirements, and the downtime that occurs during a migration. For example, your simplest approach might be to use the “lift-and-shift” cloud migration model. In this approach, you pause the application in your existing region while all your data is copied to the new region. When the copy process is finished, you resume your application in the new region, and then delete the old Data Lake Store account. Downtime during the migration is required.

To reduce downtime, you might immediately start ingesting new data in the new region. When you have the minimum data needed, run your application in the new region. In the background, continue to copy older data from the existing Data Lake Store account to the new Data Lake Store account in the new region. By using this approach, you can make the switch to the new region with little downtime. When all the older data has been copied, delete the old Data Lake Store account.

Other important details to consider when planning your migration are:

* **Data volume**. The volume of data (in gigabytes, the number of files and folders, and so on) affects the time and resources you need for the migration.

* **Data Lake Store account name**. The new account name in the new region must be globally unique. For example, the name of your old Data Lake Store account in East US 2 might be contosoeastus2.azuredatalakestore.net. You might name your new Data Lake Store account in North EU contosonortheu.azuredatalakestore.net.

* **Tools**. We recommend that you use the [Azure Data Factory Copy Activity](../data-factory/data-factory-azure-datalake-connector.md) to copy Data Lake Store files. Data Factory supports data movement with high performance and reliability. Keep in mind that Data Factory copies only the folder hierarchy and content of the files. You need to manually apply any access control lists (ACLs) that you use in the old account to the new account. For more information, including performance targets for best-case scenarios, see the [Copy Activity performance and tuning guide](../data-factory/data-factory-copy-activity-performance.md). If you want data copied more quickly, you might need to use additional Cloud Data Movement Units. Some other tools, like AdlCopy, don't support copying data between regions.  

* **Bandwidth charges**. [Bandwidth charges](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) apply because data is transferred out of an Azure region.

* **ACLs on your data**. Secure your data in the new region by applying ACLs to files and folders. For more information, see [Securing data stored in Azure Data Lake Store](data-lake-store-secure-data.md). We recommend that you use the migration to update and adjust your ACLs. You might want to use settings similar to your current settings. You can view the ACLs that are applied to any file by using the Azure portal, [PowerShell cmdlets](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.datalakestore/v3.1.0/get-azurermdatalakestoreitempermission), or SDKs.  

* **Location of analytics services**. For best performance, your analytics services, like Azure Data Lake Analytics or Azure HDInsight, should be in the same region as your data.  

## <a name="next-steps"></a>Next steps
* [Overview of Azure Data Lake Store](data-lake-store-overview.md)
