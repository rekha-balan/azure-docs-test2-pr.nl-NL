---
title: Start with Apache Kafka - Azure HDInsight Quickstart
description: In this quickstart, you learn how to create an Apache Kafka cluster on Azure HDInsight using Azure PowerShell. You also learn about Kafka topics, subscribers, and consumers.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: mvc,hdinsightactive
ms.topic: quickstart
ms.date: 04/16/2018
ms.openlocfilehash: 756733ec98912685af438861d54db0d18e15a947
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856565"
---
# <a name="quickstart-create-a-kafka-on-hdinsight-cluster"></a><span data-ttu-id="4593d-104">Quickstart: Create a Kafka on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="4593d-104">Quickstart: Create a Kafka on HDInsight cluster</span></span>

<span data-ttu-id="4593d-105">Kafka is an open-source, distributed streaming platform.</span><span class="sxs-lookup"><span data-stu-id="4593d-105">Kafka is an open-source, distributed streaming platform.</span></span> <span data-ttu-id="4593d-106">It's often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span><span class="sxs-lookup"><span data-stu-id="4593d-106">It's often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span> 

<span data-ttu-id="4593d-107">In this quickstart, you learn how to create an [Apache Kafka](https://kafka.apache.org) cluster using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4593d-107">In this quickstart, you learn how to create an [Apache Kafka](https://kafka.apache.org) cluster using Azure PowerShell.</span></span> <span data-ttu-id="4593d-108">You also learn how to use included utilities to send and receive messages using Kafka.</span><span class="sxs-lookup"><span data-stu-id="4593d-108">You also learn how to use included utilities to send and receive messages using Kafka.</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

> [!IMPORTANT]
> <span data-ttu-id="4593d-109">The Kafka API can only be accessed by resources inside the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="4593d-109">The Kafka API can only be accessed by resources inside the same virtual network.</span></span> <span data-ttu-id="4593d-110">In this quickstart, you access the cluster directly using SSH.</span><span class="sxs-lookup"><span data-stu-id="4593d-110">In this quickstart, you access the cluster directly using SSH.</span></span> <span data-ttu-id="4593d-111">To connect other services, networks, or virtual machines to Kafka, you must first create a virtual network and then create the resources within the network.</span><span class="sxs-lookup"><span data-stu-id="4593d-111">To connect other services, networks, or virtual machines to Kafka, you must first create a virtual network and then create the resources within the network.</span></span>
>
> <span data-ttu-id="4593d-112">For more information, see the [Connect to Kafka using a virtual network](apache-kafka-connect-vpn-gateway.md) document.</span><span class="sxs-lookup"><span data-stu-id="4593d-112">For more information, see the [Connect to Kafka using a virtual network](apache-kafka-connect-vpn-gateway.md) document.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4593d-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4593d-113">Prerequisites</span></span>

* <span data-ttu-id="4593d-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4593d-114">An Azure subscription.</span></span> <span data-ttu-id="4593d-115">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="4593d-115">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

* <span data-ttu-id="4593d-116">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4593d-116">Azure PowerShell.</span></span> <span data-ttu-id="4593d-117">For more information, see the [Install and Configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) document.</span><span class="sxs-lookup"><span data-stu-id="4593d-117">For more information, see the [Install and Configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) document.</span></span>

* <span data-ttu-id="4593d-118">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="4593d-118">An SSH client.</span></span> <span data-ttu-id="4593d-119">The steps in this document use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-119">The steps in this document use SSH to connect to the cluster.</span></span>

    <span data-ttu-id="4593d-120">The `ssh` command is provided by default on Linux, Unix, and macOS systems.</span><span class="sxs-lookup"><span data-stu-id="4593d-120">The `ssh` command is provided by default on Linux, Unix, and macOS systems.</span></span> <span data-ttu-id="4593d-121">On Windows 10, use one of the following methods to install the `ssh` command:</span><span class="sxs-lookup"><span data-stu-id="4593d-121">On Windows 10, use one of the following methods to install the `ssh` command:</span></span>

    * <span data-ttu-id="4593d-122">Use the [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart).</span><span class="sxs-lookup"><span data-stu-id="4593d-122">Use the [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart).</span></span> <span data-ttu-id="4593d-123">The cloud shell provides the `ssh` command, and can be configured to use either Bash or PowerShell as the shell environment.</span><span class="sxs-lookup"><span data-stu-id="4593d-123">The cloud shell provides the `ssh` command, and can be configured to use either Bash or PowerShell as the shell environment.</span></span>

    * <span data-ttu-id="4593d-124">[Install the Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10).</span><span class="sxs-lookup"><span data-stu-id="4593d-124">[Install the Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10).</span></span> <span data-ttu-id="4593d-125">The Linux distributions available through the Microsoft Store provide the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="4593d-125">The Linux distributions available through the Microsoft Store provide the `ssh` command.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4593d-126">The steps in this document assume that you are using one of the SSH clients mentioned above.</span><span class="sxs-lookup"><span data-stu-id="4593d-126">The steps in this document assume that you are using one of the SSH clients mentioned above.</span></span> <span data-ttu-id="4593d-127">If you are using a different SSH client and encounter problems, please consult the documentation for your SSH client.</span><span class="sxs-lookup"><span data-stu-id="4593d-127">If you are using a different SSH client and encounter problems, please consult the documentation for your SSH client.</span></span>
    >
    > <span data-ttu-id="4593d-128">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="4593d-128">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="4593d-129">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="4593d-129">Log in to Azure</span></span>

<span data-ttu-id="4593d-130">Log in to your Azure subscription with the `Login-AzureRmAccount` cmdlet and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="4593d-130">Log in to your Azure subscription with the `Login-AzureRmAccount` cmdlet and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="4593d-131">Create resource group</span><span class="sxs-lookup"><span data-stu-id="4593d-131">Create resource group</span></span>

<span data-ttu-id="4593d-132">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="4593d-132">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="4593d-133">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="4593d-133">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="4593d-134">The following example prompts you for the name and location, and then creates a new resource group:</span><span class="sxs-lookup"><span data-stu-id="4593d-134">The following example prompts you for the name and location, and then creates a new resource group:</span></span>

```powershell
$resourceGroup = Read-Input -Prompt "Enter the resource group name"
$location = Read-Input -Prompt "Enter the Azure region to use"

New-AzureRmResourceGroup -Name $resourceGroup -Location $location
```

## <a name="create-a-storage-account"></a><span data-ttu-id="4593d-135">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="4593d-135">Create a storage account</span></span>

<span data-ttu-id="4593d-136">While Kafka on HDInsight uses Azure Managed disks to store Kafka data, the cluster also uses Azure Storage to store information such as logs.</span><span class="sxs-lookup"><span data-stu-id="4593d-136">While Kafka on HDInsight uses Azure Managed disks to store Kafka data, the cluster also uses Azure Storage to store information such as logs.</span></span> <span data-ttu-id="4593d-137">Use [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) to create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="4593d-137">Use [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) to create a new storage account.</span></span>

```powershell
$storageName = Read-Host -Prompt "Enter the storage account name"

New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroup `
        -Name $storageName `
        -Type Standard_LRS `
        -Location $location
```

<span data-ttu-id="4593d-138">HDInsight stores data in the storage account in a blob container.</span><span class="sxs-lookup"><span data-stu-id="4593d-138">HDInsight stores data in the storage account in a blob container.</span></span> <span data-ttu-id="4593d-139">Use [New-AzureStorageContainer](/powershell/module/Azure.Storage/New-AzureStorageContainer) to create a new container.</span><span class="sxs-lookup"><span data-stu-id="4593d-139">Use [New-AzureStorageContainer](/powershell/module/Azure.Storage/New-AzureStorageContainer) to create a new container.</span></span>

```powershell
$containerName = Read-Host -Prompt "Enter the container name"

$storageKey = (Get-AzureRmStorageAccountKey `
                -ResourceGroupName $resourceGroup `
                -Name $storageName)[0].Value
$storageContext = New-AzureStorageContext `
                    -StorageAccountName $storageName `
                    -StorageAccountKey $storageKey
New-AzureStorageContainer -Name $containerName -Context $storageContext 
```

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="4593d-140">Create a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="4593d-140">Create a Kafka cluster</span></span>

<span data-ttu-id="4593d-141">Create a Kafka on HDInsight cluster with [New-AzureRmHDInsightCluster](/powershell/module/AzureRM.HDInsight/New-AzureRmHDInsightCluster).</span><span class="sxs-lookup"><span data-stu-id="4593d-141">Create a Kafka on HDInsight cluster with [New-AzureRmHDInsightCluster](/powershell/module/AzureRM.HDInsight/New-AzureRmHDInsightCluster).</span></span>

```powershell
# Create a Kafka 1.0 cluster
$clusterName = Read-Host -Prompt "Enter the name of the Kafka cluster"
$httpCredential = Get-Credential -Message "Enter the cluster login credentials" `
    -UserName "admin"
$sshCredentials = Get-Credential -Message "Enter the SSH user credentials"

$numberOfWorkerNodes = "4"
$clusterVersion = "3.6"
$clusterType="Kafka"
$clusterOS="Linux"
$disksPerNode=2

$kafkaConfig = New-Object "System.Collections.Generic.Dictionary``2[System.String,System.String]"
$kafkaConfig.Add("kafka", "1.0")

New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroup `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $numberOfWorkerNodes `
        -ClusterType $clusterType `
        -OSType $clusterOS `
        -Version $clusterVersion `
        -ComponentVersion $kafkaConfig `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageKey `
        -DefaultStorageContainer $clusterName `
        -SshCredential $sshCredentials `
        -DisksPerWorkerNode $disksPerNode
```

> [!WARNING]
> <span data-ttu-id="4593d-142">It can take up to 20 minutes to create the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-142">It can take up to 20 minutes to create the HDInsight cluster.</span></span>

> [!TIP]
> <span data-ttu-id="4593d-143">The `-DisksPerWorkerNode` parameter configures the scalability of Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4593d-143">The `-DisksPerWorkerNode` parameter configures the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="4593d-144">Kafka on HDInsight uses the local disk of the virtual machines in the cluster to store data.</span><span class="sxs-lookup"><span data-stu-id="4593d-144">Kafka on HDInsight uses the local disk of the virtual machines in the cluster to store data.</span></span> <span data-ttu-id="4593d-145">Kafka is I/O heavy, so [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) are used to provide high throughput and more storage per node.</span><span class="sxs-lookup"><span data-stu-id="4593d-145">Kafka is I/O heavy, so [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) are used to provide high throughput and more storage per node.</span></span> 
>
> <span data-ttu-id="4593d-146">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="4593d-146">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="4593d-147">The type of disk depends on the VM size used by the worker nodes (Kafka brokers).</span><span class="sxs-lookup"><span data-stu-id="4593d-147">The type of disk depends on the VM size used by the worker nodes (Kafka brokers).</span></span> <span data-ttu-id="4593d-148">Premium disks are used automatically with DS and GS series VMs.</span><span class="sxs-lookup"><span data-stu-id="4593d-148">Premium disks are used automatically with DS and GS series VMs.</span></span> <span data-ttu-id="4593d-149">All other VM types use standard.</span><span class="sxs-lookup"><span data-stu-id="4593d-149">All other VM types use standard.</span></span> <span data-ttu-id="4593d-150">You can set the VM type by using the `-WorkerNodeSize` parameter.</span><span class="sxs-lookup"><span data-stu-id="4593d-150">You can set the VM type by using the `-WorkerNodeSize` parameter.</span></span> <span data-ttu-id="4593d-151">For more information on parameters, see the [New-AzureRmHDInsightCluster](/powershell/module/AzureRM.HDInsight/New-AzureRmHDInsightCluster) documentation.</span><span class="sxs-lookup"><span data-stu-id="4593d-151">For more information on parameters, see the [New-AzureRmHDInsightCluster](/powershell/module/AzureRM.HDInsight/New-AzureRmHDInsightCluster) documentation.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="4593d-152">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must use the `-HeadNodeSize` parameter to specify a VM size with at least 8 cores and 14 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="4593d-152">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must use the `-HeadNodeSize` parameter to specify a VM size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="4593d-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4593d-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="4593d-154">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="4593d-154">Connect to the cluster</span></span>

1. <span data-ttu-id="4593d-155">To connect to the primary head node of the Kafka cluster, use the following command.</span><span class="sxs-lookup"><span data-stu-id="4593d-155">To connect to the primary head node of the Kafka cluster, use the following command.</span></span> <span data-ttu-id="4593d-156">Replace `sshuser` with the SSH user name.</span><span class="sxs-lookup"><span data-stu-id="4593d-156">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="4593d-157">Replace `mykafka` with the name of your Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="4593d-157">Replace `mykafka` with the name of your Kafka cluster</span></span>

    ```bash
    ssh sshuser@mykafka-ssh.azurehdinsight.net
    ```

2. <span data-ttu-id="4593d-158">When you first connect to the cluster, your SSH client may display a warning that the authenticity of the host can't be established.</span><span class="sxs-lookup"><span data-stu-id="4593d-158">When you first connect to the cluster, your SSH client may display a warning that the authenticity of the host can't be established.</span></span> <span data-ttu-id="4593d-159">When prompted type __yes__, and then press __Enter__ to add the host to your SSH client's trusted server list.</span><span class="sxs-lookup"><span data-stu-id="4593d-159">When prompted type __yes__, and then press __Enter__ to add the host to your SSH client's trusted server list.</span></span>

3. <span data-ttu-id="4593d-160">When prompted, enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="4593d-160">When prompted, enter the password for the SSH user.</span></span>

<span data-ttu-id="4593d-161">Once connected, you see information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="4593d-161">Once connected, you see information similar to the following text:</span></span>

```text
Authorized uses only. All activity may be monitored and reported.
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.13.0-1011-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

83 packages can be updated.
37 updates are security updates.



Welcome to Kafka on HDInsight.

Last login: Thu Mar 29 13:25:27 2018 from 108.252.109.241
ssuhuser@hn0-mykafk:~$
```

## <a id="getkafkainfo"></a><span data-ttu-id="4593d-162">Get the Zookeeper and Broker host information</span><span class="sxs-lookup"><span data-stu-id="4593d-162">Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="4593d-163">When working with Kafka, you must know the *Zookeeper* and *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="4593d-163">When working with Kafka, you must know the *Zookeeper* and *Broker* hosts.</span></span> <span data-ttu-id="4593d-164">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span><span class="sxs-lookup"><span data-stu-id="4593d-164">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="4593d-165">In this section, you get the host information from the Ambari REST API on the cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-165">In this section, you get the host information from the Ambari REST API on the cluster.</span></span>

1. <span data-ttu-id="4593d-166">From the SSH connection to the cluster, use the following command to install the `jq` utility.</span><span class="sxs-lookup"><span data-stu-id="4593d-166">From the SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="4593d-167">This utility is used to parse JSON documents, and is useful in retrieving the host information:</span><span class="sxs-lookup"><span data-stu-id="4593d-167">This utility is used to parse JSON documents, and is useful in retrieving the host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="4593d-168">To set an environment variable to the cluster name, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-168">To set an environment variable to the cluster name, use the following command:</span></span>

    ```bash
    read -p "Enter the Kafka on HDInsight cluster name: " CLUSTERNAME
    ```

    <span data-ttu-id="4593d-169">When prompted, enter the name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-169">When prompted, enter the name of the Kafka cluster.</span></span>

3. <span data-ttu-id="4593d-170">To set an environment variable with Zookeeper host information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-170">To set an environment variable with Zookeeper host information, use the following command:</span></span>

    ```bash
    export KAFKAZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="4593d-171">When prompted, enter the password for the cluster login account (not the SSH account).</span><span class="sxs-lookup"><span data-stu-id="4593d-171">When prompted, enter the password for the cluster login account (not the SSH account).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4593d-172">This command retrieves all Zookeeper hosts, then returns only the first two entries.</span><span class="sxs-lookup"><span data-stu-id="4593d-172">This command retrieves all Zookeeper hosts, then returns only the first two entries.</span></span> <span data-ttu-id="4593d-173">This is because you want some redundancy in case one host is unreachable.</span><span class="sxs-lookup"><span data-stu-id="4593d-173">This is because you want some redundancy in case one host is unreachable.</span></span>

4. <span data-ttu-id="4593d-174">To verify that the environment variable is set correctly, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-174">To verify that the environment variable is set correctly, use the following command:</span></span>

    ```bash
     echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    ```

    <span data-ttu-id="4593d-175">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="4593d-175">This command returns information similar to the following text:</span></span>

    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`

5. <span data-ttu-id="4593d-176">To set an environment variable with Kafka broker host information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-176">To set an environment variable with Kafka broker host information, use the following command:</span></span>

    ```bash
    export KAFKABROKERS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="4593d-177">When prompted, enter the password for the cluster login account (not the SSH account).</span><span class="sxs-lookup"><span data-stu-id="4593d-177">When prompted, enter the password for the cluster login account (not the SSH account).</span></span>

6. <span data-ttu-id="4593d-178">To verify that the environment variable is set correctly, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-178">To verify that the environment variable is set correctly, use the following command:</span></span>

    ```bash   
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    <span data-ttu-id="4593d-179">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="4593d-179">This command returns information similar to the following text:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

## <a name="manage-kafka-topics"></a><span data-ttu-id="4593d-180">Manage Kafka topics</span><span class="sxs-lookup"><span data-stu-id="4593d-180">Manage Kafka topics</span></span>

<span data-ttu-id="4593d-181">Kafka stores streams of data in *topics*.</span><span class="sxs-lookup"><span data-stu-id="4593d-181">Kafka stores streams of data in *topics*.</span></span> <span data-ttu-id="4593d-182">You can use the `kafka-topics.sh` utility to manage topics.</span><span class="sxs-lookup"><span data-stu-id="4593d-182">You can use the `kafka-topics.sh` utility to manage topics.</span></span>

* <span data-ttu-id="4593d-183">**To create a topic**, use the following command in the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="4593d-183">**To create a topic**, use the following command in the SSH connection:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="4593d-184">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`.</span><span class="sxs-lookup"><span data-stu-id="4593d-184">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`.</span></span> <span data-ttu-id="4593d-185">It then creates a Kafka topic named **test**.</span><span class="sxs-lookup"><span data-stu-id="4593d-185">It then creates a Kafka topic named **test**.</span></span> 

    * <span data-ttu-id="4593d-186">Data stored in this topic is partitioned across eight partitions.</span><span class="sxs-lookup"><span data-stu-id="4593d-186">Data stored in this topic is partitioned across eight partitions.</span></span>

    * <span data-ttu-id="4593d-187">Each partition is replicated across three worker nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-187">Each partition is replicated across three worker nodes in the cluster.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="4593d-188">If you created the cluster in an Azure region that provides three fault domains, use a replication factor of 3.</span><span class="sxs-lookup"><span data-stu-id="4593d-188">If you created the cluster in an Azure region that provides three fault domains, use a replication factor of 3.</span></span> <span data-ttu-id="4593d-189">Otherwise, use a replication factor of 4.</span><span class="sxs-lookup"><span data-stu-id="4593d-189">Otherwise, use a replication factor of 4.</span></span>
        
        <span data-ttu-id="4593d-190">In regions with three fault domains, a replication factor of 3 allows replicas to be spread across the fault domains.</span><span class="sxs-lookup"><span data-stu-id="4593d-190">In regions with three fault domains, a replication factor of 3 allows replicas to be spread across the fault domains.</span></span> <span data-ttu-id="4593d-191">In regions with two fault domains, a replication factor of four spreads the replicas evenly across the domains.</span><span class="sxs-lookup"><span data-stu-id="4593d-191">In regions with two fault domains, a replication factor of four spreads the replicas evenly across the domains.</span></span>
        
        <span data-ttu-id="4593d-192">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span><span class="sxs-lookup"><span data-stu-id="4593d-192">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span></span>

        > [!IMPORTANT] 
        > <span data-ttu-id="4593d-193">Kafka is not aware of Azure fault domains.</span><span class="sxs-lookup"><span data-stu-id="4593d-193">Kafka is not aware of Azure fault domains.</span></span> <span data-ttu-id="4593d-194">When creating partition replicas for topics, it may not distribute replicas properly for high availability.</span><span class="sxs-lookup"><span data-stu-id="4593d-194">When creating partition replicas for topics, it may not distribute replicas properly for high availability.</span></span>

        <span data-ttu-id="4593d-195">To ensure high availability, use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="4593d-195">To ensure high availability, use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span> <span data-ttu-id="4593d-196">This tool must be ran from an SSH connection to the head node of your Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-196">This tool must be ran from an SSH connection to the head node of your Kafka cluster.</span></span>

        <span data-ttu-id="4593d-197">For the highest availability of your Kafka data, you should rebalance the partition replicas for your topic when:</span><span class="sxs-lookup"><span data-stu-id="4593d-197">For the highest availability of your Kafka data, you should rebalance the partition replicas for your topic when:</span></span>

        * <span data-ttu-id="4593d-198">You create a new topic or partition</span><span class="sxs-lookup"><span data-stu-id="4593d-198">You create a new topic or partition</span></span>

        * <span data-ttu-id="4593d-199">You scale up a cluster</span><span class="sxs-lookup"><span data-stu-id="4593d-199">You scale up a cluster</span></span>

* <span data-ttu-id="4593d-200">**To list topics**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-200">**To list topics**, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="4593d-201">This command lists the topics available on the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="4593d-201">This command lists the topics available on the Kafka cluster.</span></span>

* <span data-ttu-id="4593d-202">**To delete a topic**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-202">**To delete a topic**, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --delete --topic topicname --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="4593d-203">This command deletes the topic named `topicname`.</span><span class="sxs-lookup"><span data-stu-id="4593d-203">This command deletes the topic named `topicname`.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4593d-204">If you delete the `test` topic created earlier, then you must recreate it.</span><span class="sxs-lookup"><span data-stu-id="4593d-204">If you delete the `test` topic created earlier, then you must recreate it.</span></span> <span data-ttu-id="4593d-205">It is used by steps later in this document.</span><span class="sxs-lookup"><span data-stu-id="4593d-205">It is used by steps later in this document.</span></span>

<span data-ttu-id="4593d-206">For more information on the commands available with the `kafka-topics.sh` utility, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4593d-206">For more information on the commands available with the `kafka-topics.sh` utility, use the following command:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh
```

## <a name="produce-and-consume-records"></a><span data-ttu-id="4593d-207">Produce and consume records</span><span class="sxs-lookup"><span data-stu-id="4593d-207">Produce and consume records</span></span>

<span data-ttu-id="4593d-208">Kafka stores *records* in topics.</span><span class="sxs-lookup"><span data-stu-id="4593d-208">Kafka stores *records* in topics.</span></span> <span data-ttu-id="4593d-209">Records are produced by *producers*, and consumed by *consumers*.</span><span class="sxs-lookup"><span data-stu-id="4593d-209">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="4593d-210">Producers and consumers communicate with the *Kafka broker* service.</span><span class="sxs-lookup"><span data-stu-id="4593d-210">Producers and consumers communicate with the *Kafka broker* service.</span></span> <span data-ttu-id="4593d-211">Each worker node in your HDInsight cluster is a Kafka broker host.</span><span class="sxs-lookup"><span data-stu-id="4593d-211">Each worker node in your HDInsight cluster is a Kafka broker host.</span></span>

<span data-ttu-id="4593d-212">To store records into the test topic you created earlier, and then read them using a consumer, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="4593d-212">To store records into the test topic you created earlier, and then read them using a consumer, use the following steps:</span></span>

1. <span data-ttu-id="4593d-213">To write records to the topic, use the `kafka-console-producer.sh` utility from the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="4593d-213">To write records to the topic, use the `kafka-console-producer.sh` utility from the SSH connection:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="4593d-214">After this command, you arrive at an empty line.</span><span class="sxs-lookup"><span data-stu-id="4593d-214">After this command, you arrive at an empty line.</span></span>

2. <span data-ttu-id="4593d-215">Type a text message on the empty line and hit enter.</span><span class="sxs-lookup"><span data-stu-id="4593d-215">Type a text message on the empty line and hit enter.</span></span> <span data-ttu-id="4593d-216">Enter a few messages this way, and then use **Ctrl + C** to return to the normal prompt.</span><span class="sxs-lookup"><span data-stu-id="4593d-216">Enter a few messages this way, and then use **Ctrl + C** to return to the normal prompt.</span></span> <span data-ttu-id="4593d-217">Each line is sent as a separate record to the Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="4593d-217">Each line is sent as a separate record to the Kafka topic.</span></span>

3. <span data-ttu-id="4593d-218">To read records from the topic, use the `kafka-console-consumer.sh` utility from the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="4593d-218">To read records from the topic, use the `kafka-console-consumer.sh` utility from the SSH connection:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="4593d-219">This command retrieves the records from the topic and displays them.</span><span class="sxs-lookup"><span data-stu-id="4593d-219">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="4593d-220">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span><span class="sxs-lookup"><span data-stu-id="4593d-220">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4593d-221">If you are using an older version of Kafka, replace `--bootstrap-server $KAFKABROKERS` with `--zookeeper $KAFKAZKHOSTS`.</span><span class="sxs-lookup"><span data-stu-id="4593d-221">If you are using an older version of Kafka, replace `--bootstrap-server $KAFKABROKERS` with `--zookeeper $KAFKAZKHOSTS`.</span></span>

4. <span data-ttu-id="4593d-222">Use __Ctrl + C__ to stop the consumer.</span><span class="sxs-lookup"><span data-stu-id="4593d-222">Use __Ctrl + C__ to stop the consumer.</span></span>

<span data-ttu-id="4593d-223">You can also programmatically create producers and consumers.</span><span class="sxs-lookup"><span data-stu-id="4593d-223">You can also programmatically create producers and consumers.</span></span> <span data-ttu-id="4593d-224">For an example of using this API, see the [Kafka Producer and Consumer API with HDInsight](apache-kafka-producer-consumer-api.md) document.</span><span class="sxs-lookup"><span data-stu-id="4593d-224">For an example of using this API, see the [Kafka Producer and Consumer API with HDInsight](apache-kafka-producer-consumer-api.md) document.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="4593d-225">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4593d-225">Clean up resources</span></span>

<span data-ttu-id="4593d-226">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, HDInsight, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="4593d-226">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, HDInsight, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

> [!WARNING]
> <span data-ttu-id="4593d-227">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="4593d-227">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="4593d-228">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="4593d-228">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span>
> 
> <span data-ttu-id="4593d-229">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="4593d-229">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4593d-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="4593d-230">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4593d-231">Use Apache Spark with Kafka</span><span class="sxs-lookup"><span data-stu-id="4593d-231">Use Apache Spark with Kafka</span></span>](../hdinsight-apache-kafka-spark-structured-streaming.md)
