---
title: How to delete an HDInsight cluster - Azure
description: Information on the various ways that you can delete an HDInsight cluster.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 03/22/2018
ms.author: jasonh
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 737cc120877a9d0f06a1f6d209bcf9a233aa7d19
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804185"
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a>Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI

HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted. Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use. In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.

> [!IMPORTANT]
> Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster. You can reuse data stored in those services in the future.

## <a name="azure-portal"></a>Azure portal

1. Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster. If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.
   
    ![portal search](./media/hdinsight-delete-cluster/navbar.png)

2. From the cluster settings, select the **Delete** icon. When prompted, select **Yes** to delete the cluster.
   
    ![delete icon](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

From a PowerShell prompt, use the following command to delete the cluster:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Replace **CLUSTERNAME** with the name of your HDInsight cluster.

## <a name="azure-cli-10"></a>Azure CLI 1.0

From a prompt, use the following to delete the cluster:

    azure hdinsight cluster delete CLUSTERNAME

Replace **CLUSTERNAME** with the name of your HDInsight cluster.

> [!NOTE]
> Azure CLI 2.0 does not support deleting HDInsight clusters at this time (October 23, 2017).
