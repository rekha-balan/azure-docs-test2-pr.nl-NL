---
title: Manage Azure Data Lake Analytics using the Azure portal | Microsoft Docs
description: Learn how to manage Data Lake Analytics acounts, data sources, users, and jobs.
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 9f3d12bfacd58be4cc5e3f7019cfe973d1dcc549
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563188"
---
# <a name="manage-azure-data-lake-analytics-using-azure-portal"></a>Manage Azure Data Lake Analytics using Azure portal
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs using the Azure portal. To see management topics using other tools, click the tab selector on the top of the page.

**Prerequisites**

Before you begin this tutorial, you must have the following items:

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Manage accounts
Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account. Unlike Azure HDInsight, you only pay for a Data Lake Analytics account when you run a job.  You only pay for the time when it is running a job.  For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).  

**To create a Data Lake Analytics account**

1. Sign on to the [Azure portal](https://portal.azure.com).
2. Click **New**, click **Intelligence + analytics**, and then click **Data Lake Analytics**.
3. Type or select the following values:
   
    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-portal-create-adla.png)
   
   * **Name**: Name the Data Lake Analytics account.
   * **Subscription**: Choose the Azure subscription used for the Analytics account.
   * **Resource Group**. Select an existing Azure Resource Group or create a new one. Azure Resource Manager enables you to work with the resources in your application as a group. For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md). 
   * **Location**. Select an Azure data center for the Data Lake Analytics account. 
   * **Data Lake Store**: Each Data Lake Analytics account has a dependent Data Lake Store account. The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center. Follow the instruction to create a new Data Lake Store account, or select an existing one.
4. Click **Create**. It takes you to the portal home screen. A new tile is added to the StartBoard with the label showing "Deploying Azure Data Lake Analytics". It takes a few moments to create a Data Lake Analytics account. When the account is created, the portal opens the account on a new blade.

After a Data Lake Analytics account is created, you can add additional Data Lake Store accounts and Azure Storage accounts. For instructions, see [Manage Data lake Analytics account data sources](data-lake-analytics-manage-use-portal.md#manage-account-data-sources).

<a name="access-adla-account"></a> **To access/open a Data Lake Analytics account**

1. Sign on to the [Azure portal](https://portal.azure.com/).
2. Click **Data Lake Analytics** on the left menu.  If you don't see it, click **More services**, and then click **Data Lake Analytics** under **Intelligence + Analytics**.
3. Click the Data Lake Analytics account that you want to access. It opens the account in a new blade.

**To delete a Data Lake Analytics account**

1. Open the Data Lake Analytics account that you want to delete. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).
2. Click **Delete** from the button menu on the top of the blade.
3. Type the account name, and then click **Delete**.

Deleting a Data Lake Analytics account does not delete the dependent Data Lake Store accounts. For instructions of deleting Data Lake Storage accounts, see [Delete Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#delete-azure-data-lake-store-account).

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Manage account data sources
Data Lake Analytics currently supports the following data sources:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/storage-introduction.md)

When you create a Data Lake Analytics account, you must designate an Azure Data Lake Store account to be the default storage account. The default Data Lake Store account is used to store job metadata and job audit logs. After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Azure Storage account. 

<a name="default-adl-account"></a>**To find the default Data Lake storage account**

* Open the Data Lake Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account). The default Data Lake store is shown in **Essential**:
  
    ![Azure Data Lake Analytics adds data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-default-adl-storage-account.png)

**To add additional data sources**

1. Open the Data Lake Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).
2. Click **Settings** and then click **Data Sources**. You shall see the default Data Lake Store account listed there. 
3. Click **Add Data Source**.
   
    ![Azure Data Lake Analytics add data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-add-data-source.png)
   
    To add an Azure Data Lake Store account, you need the account name, and access to the account to be able query it.
    To add an Azure Blob storage, you need the storage account and the account key, which can be found by navigating to the storage account in the portal.

<a name="explore-data-sources"></a>**To explore data sources**    

1. Open the Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).
2. Click **Settings** and then click **Data Explorer**. 
   
    ![Azure Data Lake Analytics data explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-data-explorer.png)
3. Click a Data Lake Store account to open the account.
   
    ![Azure Data Lake Analytics data explorer storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-explore-adls.png)
   
    For each Data Lake Store account, you can
   
   * **New Folder**: Add new folder.
   * **Upload**: Upload files to the Storage account from your workstation.
   * **Access**: Configure access permissions.
   * **Rename Folder**: Rename a folder.
   * **Folder properties**: Show file or folder properties, such as WASB path, WEBHDFS path, last modified time and so on.
   * **Delete Folder**: Delete a folder.

<a name="upload-data-to-adls"></a> **To upload files to Data Lake Store account**

1. From the Portal, click **Browse** from the left menu, and then click **Data Lake Store**.
2. Click the Data Lake Store account that you want to upload data to. To find the default Data Lake Storage account, see [here](#default-adl-account).
3. Click **Data Explorer** from the top menu.
4. Click **New Directory** to create a new folder, or click a folder name to change folder.
5. Click **Upload** from the top menu to upload file.

<a name="upload-data-to-wasb"></a> **To upload files to Azure Blob storage account**

See [Upload data for Hadoop jobs in HDInsight](../hdinsight/hdinsight-upload-data.md).  The information applies to Data Lake Analytics.

## <a name="manage-users"></a>Manage users
Data Lake Analytics uses role-based access control with Azure Active Directory. When you create a Data Lake Analytics account, a "Subscription Admins" role is added to the account. You can add additional users and security groups with the following roles:

| Role | Description |
| --- | --- |
| Owner |Let you manage everything, including access to resources. |
| Contributor |Access the portal; submit and monitor jobs. To be able to submit jobs, a contributor needs the read or write permission to the Data Lake Store accounts. |
| DataLakeAnalyticsDeveloper |Submit, monitor and cancel jobs.  These users can only cancel their own jobs. They cannot manage their own account, for instance, add users, change permissions, or delete the account. To be able to run jobs, they need read or write access to the Data Lake Store accounts |
| Reader |Lets you view everything, but not make any changes. |
| DevTest Labs User |Lets you view everything, and connect, start, restart, and shutdown virtual machines. |
| User Access Administrator |Lets you manage user access to Azure resources. |

For information on creating Azure Active Directory users and security groups, See [What is Azure Active Directory](../active-directory/active-directory-whatis.md).

**To add users or security groups to a Data Lake Analytics account**

1. Open the Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).
2. Click **Settings**, and then click **Users**. You can also click **Access** on the **Essentials** title bar as shown in the following screenshot:
   
    ![Azure Data Lake Analytics account add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-access-button.png)
3. From the **User** blade, click **Add**.
4. Select a role and add a user, and then click **OK**.

>[!NOTE]
>If this user or security group needs to submit jobs, they need to be given permission on the Data Lake Store as well. For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md)
>

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-jobs"></a>Manage jobs
You must have a Data Lake Analytics account before you can run any U-SQL jobs.  For more information, see [Manage Data Lake Analytics accounts](#manage-data-lake-analytics-accounts).

<a name="create-job"></a>**To create a job**

1. Open the Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).
2. Click **New Job**.
   
    ![create Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-create-job-button.png)
   
    You shall see a new blade similar to:
   
    ![create Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-new-job.png)
   
    For each job, you can configure

    |Name|Description|
    |----|-----------|
    |Job Name|Enter the name of the job.|
    |Priority|Lower number has higher priority. If two jobs are both queued, the one with lower priority runs first|
    |Parallelism |Max number of compute processes that can happen at the same time. Increasing this number can improve performance but can also increase cost.|
    |Script|Enter the U-SQL script for the job.|

    Using the same interface, you can also explore the link data sources, and add additional files to the linked data sources. 
1. Click **Submit Job** if you want to submit the job.

**To submit a job**

See [Create Data Lake Analytics jobs](#create-job).

<a name="monitor-jobs"></a>**To monitor jobs**

1. Open the Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account). The Job Management panel shows the basic job information:
   
    ![manage Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-manage-jobs.png)
2. Click **Job Management** as shown in the previous screenshot.
   
    ![manage Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-manage-jobs-details.png)
3. Click a job from the lists. Or click **Filter** to help you to find the jobs:
   
    ![filter Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-filter-jobs.png)
   
    You can filter jobs by **Time Range**, **Job Name**, and **Author**.
4. Click **Resubmit** if you want to resubmit the job.

**To resubmit a job**

See [Monitor Data Lake Analytics jobs](#monitor-jobs).

## <a name="monitor-account-usage"></a>Monitor account usage
**To monitor account usage**

1. Open the Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account). The Usage panel shows the usage:
   
    ![monitor Azure Data Lake Analytics usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-monitor-usage.png)
2. Double-click the pane to see more details.

## <a name="view-u-sql-catalog"></a>View U-SQL catalog
The [U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md) is used to structure data and code so they can be shared by U-SQL scripts. The catalog enables the highest performance possible with data in Azure Data Lake. From the Azure portal, you are able to view U-SQL catalog.

**To browse U-SQL catalog**

1. Open the Analytics account that you want to manage. For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).
2. Click **Data Explorer** from the top menu.
3. Expand **Catalog**, expand **master**, expand **Tables, or **Table Valued Functions**, or **Assemblies**. The following screenshot shows one table valued function.
   
    ![Azure Data Lake Analytics data explorer storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-explore-catalog.png)

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-azure-resource-manager-groups"></a>Use Azure Resource Manager groups
Applications are typically made up of many components, for example a web app, database, database server, storage, and third-party services. Azure Resource Manager enables you to work with the resources in your application as a group, referred to as an Azure Resource Group. You can deploy, update, monitor, or delete all the resources for your application in a single, coordinated operation. You use a template for deployment and that template can work for different environments such as testing, staging, and production. You can clarify billing for your organization by viewing the rolled-up costs for the entire group. For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md). 

A Data Lake Analytics service can include the following components:

* Azure Data Lake Analytics account
* Required default Azure Data Lake Store account
* Additional Azure Data Lake Store accounts
* Additional Azure Storage accounts

You can create all these components under one Resource Management group to make them easier to manage.

![Azure Data Lake Analytics account and storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.
The Resource Management group however can be located in a different data center.  

## <a name="see-also"></a>See also
* [Overview of Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Get started with Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md)
* [Manage Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)















