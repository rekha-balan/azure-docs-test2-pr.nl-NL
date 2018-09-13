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
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="df4ab-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="df4ab-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="df4ab-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="df4ab-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="df4ab-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="df4ab-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="df4ab-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="df4ab-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df4ab-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="df4ab-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="df4ab-108">You can reuse data stored in those services in the future.</span><span class="sxs-lookup"><span data-stu-id="df4ab-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="df4ab-109">Azure portal</span><span class="sxs-lookup"><span data-stu-id="df4ab-109">Azure portal</span></span>

1. <span data-ttu-id="df4ab-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="df4ab-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="df4ab-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span><span class="sxs-lookup"><span data-stu-id="df4ab-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![portal search](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="df4ab-113">From the cluster settings, select the **Delete** icon.</span><span class="sxs-lookup"><span data-stu-id="df4ab-113">From the cluster settings, select the **Delete** icon.</span></span> <span data-ttu-id="df4ab-114">When prompted, select **Yes** to delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="df4ab-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![delete icon](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="df4ab-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df4ab-116">Azure PowerShell</span></span>

<span data-ttu-id="df4ab-117">From a PowerShell prompt, use the following command to delete the cluster:</span><span class="sxs-lookup"><span data-stu-id="df4ab-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="df4ab-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="df4ab-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="df4ab-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="df4ab-119">Azure CLI 1.0</span></span>

<span data-ttu-id="df4ab-120">From a prompt, use the following to delete the cluster:</span><span class="sxs-lookup"><span data-stu-id="df4ab-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="df4ab-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="df4ab-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="df4ab-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (October 23, 2017).</span><span class="sxs-lookup"><span data-stu-id="df4ab-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (October 23, 2017).</span></span>
