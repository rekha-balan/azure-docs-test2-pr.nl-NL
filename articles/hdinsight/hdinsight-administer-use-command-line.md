---
title: Manage Hadoop clusters using Azure CLI | Microsoft Docs
description: How to use the Azure CLI to manage Hadoop clusters in HDIsight
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: ''
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jgao
ms.openlocfilehash: bdac762a6e8d19e0219f54dd83c4dd6e09a4f93e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550294"
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a>Manage Hadoop clusters in HDInsight using the Azure CLI
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight. The Azure CLI is implemented in Node.js. It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.

This article covers only using the Azure CLI with HDInsight. For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Prerequisites
Before you begin this article, you must have the following:

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.
* **Connect to Azure**, using the following command:
  
        azure login
  
    For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).
* **Switch to the Azure Resource Manager mode**, using the following command:
  
        azure config mode arm

To get help, use the **-h** switch.  For example:

    azure hdinsight cluster create -h

## <a name="create-clusters"></a>Create clusters
See [Create Linux-based clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>List and show cluster details
Use the following commands to list and show cluster details:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![HDI.CLIListCluster][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Delete clusters
Use the following command to delete a cluster:

    azure hdinsight cluster delete <Cluster Name>

You can also delete a cluster by deleting the resource group that contains the cluster. Please note, this will delete all the resources in the group including the default storage account.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Scale clusters
To change the Hadoop cluster size:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Enable/disable HTTP access for a cluster
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Enable/disable RDP access for a cluster
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Next steps
In this article, you have learned how to perform different HDInsight cluster administrative tasks. To learn more, see the following articles:

* [Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]
* [Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]
* [Get started with Azure HDInsight][hdinsight-get-started]
* [How to use the Azure CLI][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]: ../storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-command-line/HDI.CLIListClusters.png "List and show clusters"



