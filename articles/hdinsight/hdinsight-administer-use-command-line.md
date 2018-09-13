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
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="23eed-103">Manage Hadoop clusters in HDInsight using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="23eed-103">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="23eed-104">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23eed-104">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="23eed-105">The Azure CLI is implemented in Node.js.</span><span class="sxs-lookup"><span data-stu-id="23eed-105">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="23eed-106">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="23eed-106">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="23eed-107">This article covers only using the Azure CLI with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23eed-107">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="23eed-108">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="23eed-108">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="23eed-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="23eed-109">Prerequisites</span></span>
<span data-ttu-id="23eed-110">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="23eed-110">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="23eed-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="23eed-111">**An Azure subscription**.</span></span> <span data-ttu-id="23eed-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="23eed-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="23eed-113">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span><span class="sxs-lookup"><span data-stu-id="23eed-113">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="23eed-114">**Connect to Azure**, using the following command:</span><span class="sxs-lookup"><span data-stu-id="23eed-114">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="23eed-115">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="23eed-115">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="23eed-116">**Switch to the Azure Resource Manager mode**, using the following command:</span><span class="sxs-lookup"><span data-stu-id="23eed-116">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="23eed-117">To get help, use the **-h** switch.</span><span class="sxs-lookup"><span data-stu-id="23eed-117">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="23eed-118">For example:</span><span class="sxs-lookup"><span data-stu-id="23eed-118">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters"></a><span data-ttu-id="23eed-119">Create clusters</span><span class="sxs-lookup"><span data-stu-id="23eed-119">Create clusters</span></span>
<span data-ttu-id="23eed-120">See [Create Linux-based clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="23eed-120">See [Create Linux-based clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="23eed-121">List and show cluster details</span><span class="sxs-lookup"><span data-stu-id="23eed-121">List and show cluster details</span></span>
<span data-ttu-id="23eed-122">Use the following commands to list and show cluster details:</span><span class="sxs-lookup"><span data-stu-id="23eed-122">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="23eed-123">![HDI.CLIListCluster][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="23eed-123">![HDI.CLIListCluster][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="23eed-124">Delete clusters</span><span class="sxs-lookup"><span data-stu-id="23eed-124">Delete clusters</span></span>
<span data-ttu-id="23eed-125">Use the following command to delete a cluster:</span><span class="sxs-lookup"><span data-stu-id="23eed-125">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="23eed-126">You can also delete a cluster by deleting the resource group that contains the cluster.</span><span class="sxs-lookup"><span data-stu-id="23eed-126">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="23eed-127">Please note, this will delete all the resources in the group including the default storage account.</span><span class="sxs-lookup"><span data-stu-id="23eed-127">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="23eed-128">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="23eed-128">Scale clusters</span></span>
<span data-ttu-id="23eed-129">To change the Hadoop cluster size:</span><span class="sxs-lookup"><span data-stu-id="23eed-129">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="23eed-130">Enable/disable HTTP access for a cluster</span><span class="sxs-lookup"><span data-stu-id="23eed-130">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="23eed-131">Enable/disable RDP access for a cluster</span><span class="sxs-lookup"><span data-stu-id="23eed-131">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="23eed-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="23eed-132">Next steps</span></span>
<span data-ttu-id="23eed-133">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span><span class="sxs-lookup"><span data-stu-id="23eed-133">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="23eed-134">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="23eed-134">To learn more, see the following articles:</span></span>

* <span data-ttu-id="23eed-135">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="23eed-135">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="23eed-136">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="23eed-136">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="23eed-137">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="23eed-137">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="23eed-138">[How to use the Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="23eed-138">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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



