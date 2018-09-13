---
title: How to delete an HDInsight cluster | Microsoft Docs
description: Information on the various ways that you can delete an HDInsight cluster.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/08/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 530402c5d2bdabae67327716d4551f3df741bbcd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554955"
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="0fc4d-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0fc4d-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="0fc4d-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="0fc4d-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="0fc4d-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fc4d-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts associated with the cluster.</span></span> <span data-ttu-id="0fc4d-108">Since the storage account is not deleted, your data is retained and can be reused in the future.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-108">Since the storage account is not deleted, your data is retained and can be reused in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="0fc4d-109">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0fc4d-109">Azure portal</span></span>

1. <span data-ttu-id="0fc4d-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="0fc4d-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![portal search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="0fc4d-113">Once the blade opens for the cluster, select the **Delete** icon.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="0fc4d-114">When prompted, select **Yes** to delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![delete icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="0fc4d-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc4d-116">Azure PowerShell</span></span>

<span data-ttu-id="0fc4d-117">From a PowerShell prompt, use the following command to delete the cluster:</span><span class="sxs-lookup"><span data-stu-id="0fc4d-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="0fc4d-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="0fc4d-119">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0fc4d-119">Azure CLI</span></span>

<span data-ttu-id="0fc4d-120">From a prompt, use the following to delete the cluster:</span><span class="sxs-lookup"><span data-stu-id="0fc4d-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="0fc4d-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0fc4d-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>



