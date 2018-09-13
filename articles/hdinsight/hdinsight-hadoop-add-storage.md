---
title: Add additional Azure storage accounts to HDInsight | Microsoft Docs
description: Learn how to add additional Azure storage accounts to an existing HDInsight cluster.
services: hdinsight
documentationCenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: ''
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/23/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0bd6fce848c6d174eb519f8ef8a14f9ead5fa5ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562832"
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="1a332-103">Add additional storage accounts to HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a332-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="1a332-104">Learn how to use script actions to add additional Azure storage accounts to an existing HDInsight cluster that uses Linux as the operating system.</span><span class="sxs-lookup"><span data-stu-id="1a332-104">Learn how to use script actions to add additional Azure storage accounts to an existing HDInsight cluster that uses Linux as the operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a332-105">The information in this document is about adding additional storage to a cluster after it has been created.</span><span class="sxs-lookup"><span data-stu-id="1a332-105">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="1a332-106">For information on adding additional storage accounts during cluster creation, see the __Use additional storage__ section of the [Create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md#use-additional-storage) document.</span><span class="sxs-lookup"><span data-stu-id="1a332-106">For information on adding additional storage accounts during cluster creation, see the __Use additional storage__ section of the [Create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md#use-additional-storage) document.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1a332-107">How it works</span><span class="sxs-lookup"><span data-stu-id="1a332-107">How it works</span></span>

<span data-ttu-id="1a332-108">This script takes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a332-108">This script takes the following parameters:</span></span>

* <span data-ttu-id="1a332-109">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-109">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="1a332-110">After running the script, HDInsight can read and write data stored in this storage account.</span><span class="sxs-lookup"><span data-stu-id="1a332-110">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="1a332-111">__Azure storage account key__: A key that grants access to the storage account.</span><span class="sxs-lookup"><span data-stu-id="1a332-111">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="1a332-112">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span><span class="sxs-lookup"><span data-stu-id="1a332-112">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="1a332-113">During processing, the script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="1a332-113">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="1a332-114">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span><span class="sxs-lookup"><span data-stu-id="1a332-114">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="1a332-115">Verifies that the storage account exists and can be accessed using the key.</span><span class="sxs-lookup"><span data-stu-id="1a332-115">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="1a332-116">Encrypts the key using the cluster credential.</span><span class="sxs-lookup"><span data-stu-id="1a332-116">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="1a332-117">Adds the storage account to the core-site.xml file.</span><span class="sxs-lookup"><span data-stu-id="1a332-117">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="1a332-118">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services so that they pick up the new storage account information.</span><span class="sxs-lookup"><span data-stu-id="1a332-118">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services so that they pick up the new storage account information.</span></span>

> [!WARNING]
> <span data-ttu-id="1a332-119">Using a storage account in a different location than the HDInsight cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="1a332-119">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="1a332-120">The script</span><span class="sxs-lookup"><span data-stu-id="1a332-120">The script</span></span>

<span data-ttu-id="1a332-121">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="1a332-121">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="1a332-122">__Requirements__:</span><span class="sxs-lookup"><span data-stu-id="1a332-122">__Requirements__:</span></span>

* <span data-ttu-id="1a332-123">The script must be applied on the __Head nodes__.</span><span class="sxs-lookup"><span data-stu-id="1a332-123">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="1a332-124">To use the script</span><span class="sxs-lookup"><span data-stu-id="1a332-124">To use the script</span></span>

<span data-ttu-id="1a332-125">See the Apply a script action to a running cluster section of the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document for information on using script actions through the Azure portal, Azure PowerShell, and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1a332-125">See the Apply a script action to a running cluster section of the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document for information on using script actions through the Azure portal, Azure PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="1a332-126">When using the information provided in the customization document, replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="1a332-126">When using the information provided in the customization document, replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span> <span data-ttu-id="1a332-127">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-127">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1a332-128">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-128">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="1a332-129">Known issues</span><span class="sxs-lookup"><span data-stu-id="1a332-129">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="1a332-130">Storage accounts not displayed in Azure portal or tools</span><span class="sxs-lookup"><span data-stu-id="1a332-130">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="1a332-131">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span><span class="sxs-lookup"><span data-stu-id="1a332-131">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="1a332-132">Azure PowerShell and Azure CLI do not display the additional storage account either.</span><span class="sxs-lookup"><span data-stu-id="1a332-132">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="1a332-133">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-133">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="1a332-134">This information is not used when retrieving the cluster information using Azure management APIs.</span><span class="sxs-lookup"><span data-stu-id="1a332-134">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="1a332-135">To view storage account information added to the cluster using this script, use the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="1a332-135">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="1a332-136">The following command demonstrates how to use [cURL (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data from Ambari:</span><span class="sxs-lookup"><span data-stu-id="1a332-136">The following command demonstrates how to use [cURL (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data from Ambari:</span></span>

> [!div class="tabbedCodeSnippets" data-resources="OutlookServices.Calendar"]
> ```PowerShell
> curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["""fs.azure.account.key.STORAGEACCOUNT.blob.core.windows.net"""] | select(. != null)'
> ```
> ```Bash
> curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.STORAGEACCOUNT.blob.core.windows.net"] | select(. != null)'
> ```

<span data-ttu-id="1a332-137">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-137">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="1a332-138">Replace __PASSWORD__ with the HTTP login password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-138">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="1a332-139">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span><span class="sxs-lookup"><span data-stu-id="1a332-139">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="1a332-140">Information returned from this command appears similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="1a332-140">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="1a332-141">This text is an example of an encrypted key, which is used to access the storage account.</span><span class="sxs-lookup"><span data-stu-id="1a332-141">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="1a332-142">Unable to access storage after changing key</span><span class="sxs-lookup"><span data-stu-id="1a332-142">Unable to access storage after changing key</span></span>

<span data-ttu-id="1a332-143">If you change the key for a storage account, HDInsight can no longer access the storage account.</span><span class="sxs-lookup"><span data-stu-id="1a332-143">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="1a332-144">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-144">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="1a332-145">This cached copy must be updated to match the new key.</span><span class="sxs-lookup"><span data-stu-id="1a332-145">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="1a332-146">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span><span class="sxs-lookup"><span data-stu-id="1a332-146">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="1a332-147">If an entry already exists, it does not make any changes.</span><span class="sxs-lookup"><span data-stu-id="1a332-147">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="1a332-148">To work around this problem, you must remove the existing entry for the storage account.</span><span class="sxs-lookup"><span data-stu-id="1a332-148">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="1a332-149">Use the following steps to remove the existing entry:</span><span class="sxs-lookup"><span data-stu-id="1a332-149">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="1a332-150">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-150">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="1a332-151">The URI is https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1a332-151">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1a332-152">Replace __CLUSTERNAME__ with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-152">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="1a332-153">When prompted, enter the HTTP login user and password for your cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-153">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="1a332-154">From the list of services on the left of the page, select __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="1a332-154">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="1a332-155">Then select the __Configs__ tab in the center of the page.</span><span class="sxs-lookup"><span data-stu-id="1a332-155">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="1a332-156">In the __Filter...__ field, enter a value of __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="1a332-156">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="1a332-157">This returns entries for any additional storage accounts that have been added to the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-157">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="1a332-158">There are two types of entries; __keyprovider__ and __key__.</span><span class="sxs-lookup"><span data-stu-id="1a332-158">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="1a332-159">Both contain the name of the storage account as part of the key name.</span><span class="sxs-lookup"><span data-stu-id="1a332-159">Both contain the name of the storage account as part of the key name.</span></span> 

    <span data-ttu-id="1a332-160">The following are example entries for a storage account named __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="1a332-160">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="1a332-161">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span><span class="sxs-lookup"><span data-stu-id="1a332-161">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="1a332-162">Then use the __Save__ button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="1a332-162">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="1a332-163">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-163">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="1a332-164">Poor performance</span><span class="sxs-lookup"><span data-stu-id="1a332-164">Poor performance</span></span>

<span data-ttu-id="1a332-165">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span><span class="sxs-lookup"><span data-stu-id="1a332-165">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="1a332-166">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span><span class="sxs-lookup"><span data-stu-id="1a332-166">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="1a332-167">Additional charges</span><span class="sxs-lookup"><span data-stu-id="1a332-167">Additional charges</span></span>

<span data-ttu-id="1a332-168">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span><span class="sxs-lookup"><span data-stu-id="1a332-168">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="1a332-169">An egress charge is applied when data leaves a regional data center, even if the traffic is destined for another Azure data center in a different region.</span><span class="sxs-lookup"><span data-stu-id="1a332-169">An egress charge is applied when data leaves a regional data center, even if the traffic is destined for another Azure data center in a different region.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a332-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a332-170">Next steps</span></span>

<span data-ttu-id="1a332-171">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1a332-171">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="1a332-172">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1a332-172">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>