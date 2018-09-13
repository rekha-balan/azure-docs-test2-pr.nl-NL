---
title: Start with Apache Kafka - Azure HDInsight Quickstart
description: In this quickstart, you learn how to create an Apache Kafka cluster on Azure HDInsight using the Azure portal. You also learn about Kafka topics, subscribers, and consumers.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.custom: mvc,hdinsightactive
ms.topic: quickstart
ms.date: 05/23/2018
ms.openlocfilehash: c8ec39c6962c4044810d0ae65d2736043bdd4d72
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968033"
---
# <a name="quickstart-create-a-kafka-on-hdinsight-cluster"></a><span data-ttu-id="3a2f3-104">Quickstart: Create a Kafka on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="3a2f3-104">Quickstart: Create a Kafka on HDInsight cluster</span></span>

<span data-ttu-id="3a2f3-105">Kafka is an open-source, distributed streaming platform.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-105">Kafka is an open-source, distributed streaming platform.</span></span> <span data-ttu-id="3a2f3-106">It's often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-106">It's often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span> 

<span data-ttu-id="3a2f3-107">In this quickstart, you learn how to create an [Apache Kafka](https://kafka.apache.org) cluster using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-107">In this quickstart, you learn how to create an [Apache Kafka](https://kafka.apache.org) cluster using the Azure portal.</span></span> <span data-ttu-id="3a2f3-108">You also learn how to use included utilities to send and receive messages using Kafka.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-108">You also learn how to use included utilities to send and receive messages using Kafka.</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

> [!IMPORTANT]
> <span data-ttu-id="3a2f3-109">The Kafka API can only be accessed by resources inside the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-109">The Kafka API can only be accessed by resources inside the same virtual network.</span></span> <span data-ttu-id="3a2f3-110">In this quickstart, you access the cluster directly using SSH.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-110">In this quickstart, you access the cluster directly using SSH.</span></span> <span data-ttu-id="3a2f3-111">To connect other services, networks, or virtual machines to Kafka, you must first create a virtual network and then create the resources within the network.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-111">To connect other services, networks, or virtual machines to Kafka, you must first create a virtual network and then create the resources within the network.</span></span>
>
> <span data-ttu-id="3a2f3-112">For more information, see the [Connect to Kafka using a virtual network](apache-kafka-connect-vpn-gateway.md) document.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-112">For more information, see the [Connect to Kafka using a virtual network](apache-kafka-connect-vpn-gateway.md) document.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a2f3-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3a2f3-113">Prerequisites</span></span>

* <span data-ttu-id="3a2f3-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-114">An Azure subscription.</span></span> <span data-ttu-id="3a2f3-115">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-115">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

* <span data-ttu-id="3a2f3-116">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-116">An SSH client.</span></span> <span data-ttu-id="3a2f3-117">The steps in this document use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-117">The steps in this document use SSH to connect to the cluster.</span></span>

    <span data-ttu-id="3a2f3-118">The `ssh` command is provided by default on Linux, Unix, and macOS systems.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-118">The `ssh` command is provided by default on Linux, Unix, and macOS systems.</span></span> <span data-ttu-id="3a2f3-119">On Windows 10, use one of the following methods to install the `ssh` command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-119">On Windows 10, use one of the following methods to install the `ssh` command:</span></span>

    * <span data-ttu-id="3a2f3-120">Use the [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-120">Use the [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart).</span></span> <span data-ttu-id="3a2f3-121">The cloud shell provides the `ssh` command, and can be configured to use either Bash or PowerShell as the shell environment.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-121">The cloud shell provides the `ssh` command, and can be configured to use either Bash or PowerShell as the shell environment.</span></span>

    * <span data-ttu-id="3a2f3-122">[Install the Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-122">[Install the Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10).</span></span> <span data-ttu-id="3a2f3-123">The Linux distributions available through the Microsoft Store provide the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-123">The Linux distributions available through the Microsoft Store provide the `ssh` command.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3a2f3-124">The steps in this document assume that you are using one of the SSH clients mentioned above.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-124">The steps in this document assume that you are using one of the SSH clients mentioned above.</span></span> <span data-ttu-id="3a2f3-125">If you are using a different SSH client and encounter problems, please consult the documentation for your SSH client.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-125">If you are using a different SSH client and encounter problems, please consult the documentation for your SSH client.</span></span>
    >
    > <span data-ttu-id="3a2f3-126">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-126">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="3a2f3-127">Create a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="3a2f3-127">Create a Kafka cluster</span></span>

<span data-ttu-id="3a2f3-128">To create a Kafka on HDInsight cluster, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-128">To create a Kafka on HDInsight cluster, use the following steps:</span></span>

1. <span data-ttu-id="3a2f3-129">From the [Azure portal](https://portal.azure.com), select **+ Create a resource**, **Data + Analytics**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-129">From the [Azure portal](https://portal.azure.com), select **+ Create a resource**, **Data + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Create a HDInsight cluster](./media/apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="3a2f3-131">From **Basics**, enter or select the following information:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-131">From **Basics**, enter or select the following information:</span></span>

    | <span data-ttu-id="3a2f3-132">Setting</span><span class="sxs-lookup"><span data-stu-id="3a2f3-132">Setting</span></span> | <span data-ttu-id="3a2f3-133">Value</span><span class="sxs-lookup"><span data-stu-id="3a2f3-133">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3a2f3-134">Cluster Name</span><span class="sxs-lookup"><span data-stu-id="3a2f3-134">Cluster Name</span></span> | <span data-ttu-id="3a2f3-135">A unique name for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-135">A unique name for the HDInsight cluster.</span></span> |
    | <span data-ttu-id="3a2f3-136">Subscription</span><span class="sxs-lookup"><span data-stu-id="3a2f3-136">Subscription</span></span> | <span data-ttu-id="3a2f3-137">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-137">Select your subscription.</span></span> |
    
    <span data-ttu-id="3a2f3-138">Select __Cluster Type__ to display the **Cluster configuration**.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-138">Select __Cluster Type__ to display the **Cluster configuration**.</span></span>

    ![Select subscription](./media/apache-kafka-get-started/hdinsight-basic-configuration-1.png)

3. <span data-ttu-id="3a2f3-140">From the __Cluster configuration__, select the following values:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-140">From the __Cluster configuration__, select the following values:</span></span>

    | <span data-ttu-id="3a2f3-141">Setting</span><span class="sxs-lookup"><span data-stu-id="3a2f3-141">Setting</span></span> | <span data-ttu-id="3a2f3-142">Value</span><span class="sxs-lookup"><span data-stu-id="3a2f3-142">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3a2f3-143">Cluster Type</span><span class="sxs-lookup"><span data-stu-id="3a2f3-143">Cluster Type</span></span> | <span data-ttu-id="3a2f3-144">Kafka</span><span class="sxs-lookup"><span data-stu-id="3a2f3-144">Kafka</span></span> |
    | <span data-ttu-id="3a2f3-145">Version</span><span class="sxs-lookup"><span data-stu-id="3a2f3-145">Version</span></span> | <span data-ttu-id="3a2f3-146">Kafka 1.0.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="3a2f3-146">Kafka 1.0.0 (HDI 3.6)</span></span> |

    <span data-ttu-id="3a2f3-147">Use the **Select** button to save the cluster type settings and return to __Basics__.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-147">Use the **Select** button to save the cluster type settings and return to __Basics__.</span></span>

    ![Select cluster type](./media/apache-kafka-get-started/kafka-cluster-type.png)

4. <span data-ttu-id="3a2f3-149">From __Basics__, enter or select the following information:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-149">From __Basics__, enter or select the following information:</span></span>

    | <span data-ttu-id="3a2f3-150">Setting</span><span class="sxs-lookup"><span data-stu-id="3a2f3-150">Setting</span></span> | <span data-ttu-id="3a2f3-151">Value</span><span class="sxs-lookup"><span data-stu-id="3a2f3-151">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3a2f3-152">Cluster login username</span><span class="sxs-lookup"><span data-stu-id="3a2f3-152">Cluster login username</span></span> | <span data-ttu-id="3a2f3-153">The login name when accessing web services or REST APIs hosted on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-153">The login name when accessing web services or REST APIs hosted on the cluster.</span></span> <span data-ttu-id="3a2f3-154">Keep the default value (admin).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-154">Keep the default value (admin).</span></span> |
    | <span data-ttu-id="3a2f3-155">Cluster login password</span><span class="sxs-lookup"><span data-stu-id="3a2f3-155">Cluster login password</span></span> | <span data-ttu-id="3a2f3-156">The login password when accessing web services or REST APIs hosted on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-156">The login password when accessing web services or REST APIs hosted on the cluster.</span></span> |
    | <span data-ttu-id="3a2f3-157">Secure Shell (SSH) username</span><span class="sxs-lookup"><span data-stu-id="3a2f3-157">Secure Shell (SSH) username</span></span> | <span data-ttu-id="3a2f3-158">The login used when accessing the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-158">The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="3a2f3-159">By default the password is the same as the cluster login password.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-159">By default the password is the same as the cluster login password.</span></span> |
    | <span data-ttu-id="3a2f3-160">Resource Group</span><span class="sxs-lookup"><span data-stu-id="3a2f3-160">Resource Group</span></span> | <span data-ttu-id="3a2f3-161">The resource group to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-161">The resource group to create the cluster in.</span></span> |
    | <span data-ttu-id="3a2f3-162">Location</span><span class="sxs-lookup"><span data-stu-id="3a2f3-162">Location</span></span> | <span data-ttu-id="3a2f3-163">The Azure region to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-163">The Azure region to create the cluster in.</span></span> |

    > [!TIP]
    > <span data-ttu-id="3a2f3-164">Each Azure region (location) provides _fault domains_.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-164">Each Azure region (location) provides _fault domains_.</span></span> <span data-ttu-id="3a2f3-165">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-165">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="3a2f3-166">Each fault domain shares a common power source and network switch.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-166">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="3a2f3-167">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-167">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="3a2f3-168">This architecture limits the potential impact of physical hardware failures.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-168">This architecture limits the potential impact of physical hardware failures.</span></span>
    >
    > <span data-ttu-id="3a2f3-169">For high availability of data, select a region (location) that contains __three fault domains__.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-169">For high availability of data, select a region (location) that contains __three fault domains__.</span></span> <span data-ttu-id="3a2f3-170">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-170">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span></span>

    ![Select subscription](./media/apache-kafka-get-started/hdinsight-basic-configuration-2.png)

    <span data-ttu-id="3a2f3-172">Use the __Next__ button to finish basic configuration.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-172">Use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="3a2f3-173">From **Storage**, select or create a Storage account.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-173">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="3a2f3-174">For the steps in this document, leave the other fields at the default values.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-174">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="3a2f3-175">Use the __Next__ button to save storage configuration.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-175">Use the __Next__ button to save storage configuration.</span></span> <span data-ttu-id="3a2f3-176">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-176">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

    ![Set the storage account settings for HDInsight](./media/apache-kafka-get-started/storage-configuration.png)

6. <span data-ttu-id="3a2f3-178">From __Applications (optional)__, select __Next__ to continue with the default settings.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-178">From __Applications (optional)__, select __Next__ to continue with the default settings.</span></span>

7. <span data-ttu-id="3a2f3-179">From __Cluster size__, select __Next__ to continue with the default settings.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-179">From __Cluster size__, select __Next__ to continue with the default settings.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3a2f3-180">To guarantee availability of Kafka on HDInsight, the __number of worker nodes__ entry must be set to 3 or greater.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-180">To guarantee availability of Kafka on HDInsight, the __number of worker nodes__ entry must be set to 3 or greater.</span></span> <span data-ttu-id="3a2f3-181">The default value is 4.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-181">The default value is 4.</span></span>
    
    > [!TIP]
    > <span data-ttu-id="3a2f3-182">The **disks per worker node** entry configures the scalability of Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-182">The **disks per worker node** entry configures the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="3a2f3-183">Kafka on HDInsight uses the local disk of the virtual machines in the cluster to store data.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-183">Kafka on HDInsight uses the local disk of the virtual machines in the cluster to store data.</span></span> <span data-ttu-id="3a2f3-184">Kafka is I/O heavy, so [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) are used to provide high throughput and more storage per node.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-184">Kafka is I/O heavy, so [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) are used to provide high throughput and more storage per node.</span></span> <span data-ttu-id="3a2f3-185">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-185">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="3a2f3-186">The type of disk depends on the VM size used by the worker nodes (Kafka brokers).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-186">The type of disk depends on the VM size used by the worker nodes (Kafka brokers).</span></span> <span data-ttu-id="3a2f3-187">Premium disks are used automatically with DS and GS series VMs.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-187">Premium disks are used automatically with DS and GS series VMs.</span></span> <span data-ttu-id="3a2f3-188">All other VM types use standard.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-188">All other VM types use standard.</span></span>

    ![Set the Kafka cluster size](./media/apache-kafka-get-started/kafka-cluster-size.png)

8. <span data-ttu-id="3a2f3-190">From __Advanced settings__, select __Next__ to continue with the default settings.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-190">From __Advanced settings__, select __Next__ to continue with the default settings.</span></span>

9. <span data-ttu-id="3a2f3-191">From the **Summary**, review the configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-191">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="3a2f3-192">Use the __Edit__ links to change any settings that are incorrect.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-192">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="3a2f3-193">Finally, use the__Create__ button to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-193">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Cluster configuration summary](./media/apache-kafka-get-started/kafka-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="3a2f3-195">It can take up to 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-195">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="3a2f3-196">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="3a2f3-196">Connect to the cluster</span></span>

1. <span data-ttu-id="3a2f3-197">To connect to the primary head node of the Kafka cluster, use the following command.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-197">To connect to the primary head node of the Kafka cluster, use the following command.</span></span> <span data-ttu-id="3a2f3-198">Replace `sshuser` with the SSH user name.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-198">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="3a2f3-199">Replace `mykafka` with the name of your Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="3a2f3-199">Replace `mykafka` with the name of your Kafka cluster</span></span>

    ```bash
    ssh sshuser@mykafka-ssh.azurehdinsight.net
    ```

2. <span data-ttu-id="3a2f3-200">When you first connect to the cluster, your SSH client may display a warning that the authenticity of the host can't be established.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-200">When you first connect to the cluster, your SSH client may display a warning that the authenticity of the host can't be established.</span></span> <span data-ttu-id="3a2f3-201">When prompted type __yes__, and then press __Enter__ to add the host to your SSH client's trusted server list.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-201">When prompted type __yes__, and then press __Enter__ to add the host to your SSH client's trusted server list.</span></span>

3. <span data-ttu-id="3a2f3-202">When prompted, enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-202">When prompted, enter the password for the SSH user.</span></span>

<span data-ttu-id="3a2f3-203">Once connected, you see information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-203">Once connected, you see information similar to the following text:</span></span>

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

## <a id="getkafkainfo"></a><span data-ttu-id="3a2f3-204">Get the Zookeeper and Broker host information</span><span class="sxs-lookup"><span data-stu-id="3a2f3-204">Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="3a2f3-205">When working with Kafka, you must know the *Zookeeper* and *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-205">When working with Kafka, you must know the *Zookeeper* and *Broker* hosts.</span></span> <span data-ttu-id="3a2f3-206">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-206">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="3a2f3-207">In this section, you get the host information from the Ambari REST API on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-207">In this section, you get the host information from the Ambari REST API on the cluster.</span></span>

1. <span data-ttu-id="3a2f3-208">From the SSH connection to the cluster, use the following command to install the `jq` utility.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-208">From the SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="3a2f3-209">This utility is used to parse JSON documents, and is useful in retrieving the host information:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-209">This utility is used to parse JSON documents, and is useful in retrieving the host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="3a2f3-210">To set an environment variable to the cluster name, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-210">To set an environment variable to the cluster name, use the following command:</span></span>

    ```bash
    read -p "Enter the Kafka on HDInsight cluster name: " CLUSTERNAME
    ```

    <span data-ttu-id="3a2f3-211">When prompted, enter the name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-211">When prompted, enter the name of the Kafka cluster.</span></span>

3. <span data-ttu-id="3a2f3-212">To set an environment variable with Zookeeper host information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-212">To set an environment variable with Zookeeper host information, use the following command:</span></span>
    
    ```bash
    export KAFKAZKHOSTS=`curl -sS -u admin -G http://headnodehost:8080/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    ```

    > [!TIP]
    > <span data-ttu-id="3a2f3-213">This command directly queries the Ambari service on the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-213">This command directly queries the Ambari service on the cluster head node.</span></span> <span data-ttu-id="3a2f3-214">You can also access ambari using the public address of `https://$CLUSTERNAME.azurehdinsight.net:80/`.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-214">You can also access ambari using the public address of `https://$CLUSTERNAME.azurehdinsight.net:80/`.</span></span> <span data-ttu-id="3a2f3-215">Some network configurations can prevent access to the public address.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-215">Some network configurations can prevent access to the public address.</span></span> <span data-ttu-id="3a2f3-216">For example, using Network Security Groups (NSG) to restrict access to HDInsight in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-216">For example, using Network Security Groups (NSG) to restrict access to HDInsight in a virtual network.</span></span>

    <span data-ttu-id="3a2f3-217">When prompted, enter the password for the cluster login account (not the SSH account).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-217">When prompted, enter the password for the cluster login account (not the SSH account).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a2f3-218">This command retrieves all Zookeeper hosts, then returns only the first two entries.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-218">This command retrieves all Zookeeper hosts, then returns only the first two entries.</span></span> <span data-ttu-id="3a2f3-219">This is because you want some redundancy in case one host is unreachable.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-219">This is because you want some redundancy in case one host is unreachable.</span></span>

4. <span data-ttu-id="3a2f3-220">To verify that the environment variable is set correctly, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-220">To verify that the environment variable is set correctly, use the following command:</span></span>

    ```bash
     echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    ```

    <span data-ttu-id="3a2f3-221">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-221">This command returns information similar to the following text:</span></span>

    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`

5. <span data-ttu-id="3a2f3-222">To set an environment variable with Kafka broker host information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-222">To set an environment variable with Kafka broker host information, use the following command:</span></span>

    ```bash
    export KAFKABROKERS=`curl -sS -u admin -G http://headnodehost:8080/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="3a2f3-223">When prompted, enter the password for the cluster login account (not the SSH account).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-223">When prompted, enter the password for the cluster login account (not the SSH account).</span></span>

6. <span data-ttu-id="3a2f3-224">To verify that the environment variable is set correctly, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-224">To verify that the environment variable is set correctly, use the following command:</span></span>

    ```bash   
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    <span data-ttu-id="3a2f3-225">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-225">This command returns information similar to the following text:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

## <a name="manage-kafka-topics"></a><span data-ttu-id="3a2f3-226">Manage Kafka topics</span><span class="sxs-lookup"><span data-stu-id="3a2f3-226">Manage Kafka topics</span></span>

<span data-ttu-id="3a2f3-227">Kafka stores streams of data in *topics*.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-227">Kafka stores streams of data in *topics*.</span></span> <span data-ttu-id="3a2f3-228">You can use the `kafka-topics.sh` utility to manage topics.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-228">You can use the `kafka-topics.sh` utility to manage topics.</span></span>

* <span data-ttu-id="3a2f3-229">**To create a topic**, use the following command in the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-229">**To create a topic**, use the following command in the SSH connection:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="3a2f3-230">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-230">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`.</span></span> <span data-ttu-id="3a2f3-231">It then creates a Kafka topic named **test**.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-231">It then creates a Kafka topic named **test**.</span></span> 

    * <span data-ttu-id="3a2f3-232">Data stored in this topic is partitioned across eight partitions.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-232">Data stored in this topic is partitioned across eight partitions.</span></span>

    * <span data-ttu-id="3a2f3-233">Each partition is replicated across three worker nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-233">Each partition is replicated across three worker nodes in the cluster.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="3a2f3-234">If you created the cluster in an Azure region that provides three fault domains, use a replication factor of 3.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-234">If you created the cluster in an Azure region that provides three fault domains, use a replication factor of 3.</span></span> <span data-ttu-id="3a2f3-235">Otherwise, use a replication factor of 4.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-235">Otherwise, use a replication factor of 4.</span></span>
        
        <span data-ttu-id="3a2f3-236">In regions with three fault domains, a replication factor of 3 allows replicas to be spread across the fault domains.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-236">In regions with three fault domains, a replication factor of 3 allows replicas to be spread across the fault domains.</span></span> <span data-ttu-id="3a2f3-237">In regions with two fault domains, a replication factor of four spreads the replicas evenly across the domains.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-237">In regions with two fault domains, a replication factor of four spreads the replicas evenly across the domains.</span></span>
        
        <span data-ttu-id="3a2f3-238">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-238">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span></span>

        > [!IMPORTANT] 
        > <span data-ttu-id="3a2f3-239">Kafka is not aware of Azure fault domains.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-239">Kafka is not aware of Azure fault domains.</span></span> <span data-ttu-id="3a2f3-240">When creating partition replicas for topics, it may not distribute replicas properly for high availability.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-240">When creating partition replicas for topics, it may not distribute replicas properly for high availability.</span></span>

        <span data-ttu-id="3a2f3-241">To ensure high availability, use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="3a2f3-241">To ensure high availability, use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span> <span data-ttu-id="3a2f3-242">This tool must be ran from an SSH connection to the head node of your Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-242">This tool must be ran from an SSH connection to the head node of your Kafka cluster.</span></span>

        <span data-ttu-id="3a2f3-243">For the highest availability of your Kafka data, you should rebalance the partition replicas for your topic when:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-243">For the highest availability of your Kafka data, you should rebalance the partition replicas for your topic when:</span></span>

        * <span data-ttu-id="3a2f3-244">You create a new topic or partition</span><span class="sxs-lookup"><span data-stu-id="3a2f3-244">You create a new topic or partition</span></span>

        * <span data-ttu-id="3a2f3-245">You scale up a cluster</span><span class="sxs-lookup"><span data-stu-id="3a2f3-245">You scale up a cluster</span></span>

* <span data-ttu-id="3a2f3-246">**To list topics**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-246">**To list topics**, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="3a2f3-247">This command lists the topics available on the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-247">This command lists the topics available on the Kafka cluster.</span></span>

* <span data-ttu-id="3a2f3-248">**To delete a topic**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-248">**To delete a topic**, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --delete --topic topicname --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="3a2f3-249">This command deletes the topic named `topicname`.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-249">This command deletes the topic named `topicname`.</span></span>

    > [!WARNING]
    > <span data-ttu-id="3a2f3-250">If you delete the `test` topic created earlier, then you must recreate it.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-250">If you delete the `test` topic created earlier, then you must recreate it.</span></span> <span data-ttu-id="3a2f3-251">It is used by steps later in this document.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-251">It is used by steps later in this document.</span></span>

<span data-ttu-id="3a2f3-252">For more information on the commands available with the `kafka-topics.sh` utility, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-252">For more information on the commands available with the `kafka-topics.sh` utility, use the following command:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh
```

## <a name="produce-and-consume-records"></a><span data-ttu-id="3a2f3-253">Produce and consume records</span><span class="sxs-lookup"><span data-stu-id="3a2f3-253">Produce and consume records</span></span>

<span data-ttu-id="3a2f3-254">Kafka stores *records* in topics.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-254">Kafka stores *records* in topics.</span></span> <span data-ttu-id="3a2f3-255">Records are produced by *producers*, and consumed by *consumers*.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-255">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="3a2f3-256">Producers and consumers communicate with the *Kafka broker* service.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-256">Producers and consumers communicate with the *Kafka broker* service.</span></span> <span data-ttu-id="3a2f3-257">Each worker node in your HDInsight cluster is a Kafka broker host.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-257">Each worker node in your HDInsight cluster is a Kafka broker host.</span></span>

<span data-ttu-id="3a2f3-258">To store records into the test topic you created earlier, and then read them using a consumer, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-258">To store records into the test topic you created earlier, and then read them using a consumer, use the following steps:</span></span>

1. <span data-ttu-id="3a2f3-259">To write records to the topic, use the `kafka-console-producer.sh` utility from the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-259">To write records to the topic, use the `kafka-console-producer.sh` utility from the SSH connection:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="3a2f3-260">After this command, you arrive at an empty line.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-260">After this command, you arrive at an empty line.</span></span>

2. <span data-ttu-id="3a2f3-261">Type a text message on the empty line and hit enter.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-261">Type a text message on the empty line and hit enter.</span></span> <span data-ttu-id="3a2f3-262">Enter a few messages this way, and then use **Ctrl + C** to return to the normal prompt.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-262">Enter a few messages this way, and then use **Ctrl + C** to return to the normal prompt.</span></span> <span data-ttu-id="3a2f3-263">Each line is sent as a separate record to the Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-263">Each line is sent as a separate record to the Kafka topic.</span></span>

3. <span data-ttu-id="3a2f3-264">To read records from the topic, use the `kafka-console-consumer.sh` utility from the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-264">To read records from the topic, use the `kafka-console-consumer.sh` utility from the SSH connection:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="3a2f3-265">This command retrieves the records from the topic and displays them.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-265">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="3a2f3-266">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-266">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a2f3-267">If you are using an older version of Kafka, replace `--bootstrap-server $KAFKABROKERS` with `--zookeeper $KAFKAZKHOSTS`.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-267">If you are using an older version of Kafka, replace `--bootstrap-server $KAFKABROKERS` with `--zookeeper $KAFKAZKHOSTS`.</span></span>

4. <span data-ttu-id="3a2f3-268">Use __Ctrl + C__ to stop the consumer.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-268">Use __Ctrl + C__ to stop the consumer.</span></span>

<span data-ttu-id="3a2f3-269">You can also programmatically create producers and consumers.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-269">You can also programmatically create producers and consumers.</span></span> <span data-ttu-id="3a2f3-270">For an example of using this API, see the [Kafka Producer and Consumer API with HDInsight](apache-kafka-producer-consumer-api.md) document.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-270">For an example of using this API, see the [Kafka Producer and Consumer API with HDInsight](apache-kafka-producer-consumer-api.md) document.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="3a2f3-271">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3a2f3-271">Clean up resources</span></span>

<span data-ttu-id="3a2f3-272">To clean up the resources created by this quickstart, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-272">To clean up the resources created by this quickstart, you can delete the resource group.</span></span> <span data-ttu-id="3a2f3-273">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-273">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span></span>

<span data-ttu-id="3a2f3-274">To remove the resource group using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="3a2f3-274">To remove the resource group using the Azure portal:</span></span>

1. <span data-ttu-id="3a2f3-275">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-275">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span></span>
2. <span data-ttu-id="3a2f3-276">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-276">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span></span>
3. <span data-ttu-id="3a2f3-277">Select __Delete resource group__, and then confirm.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-277">Select __Delete resource group__, and then confirm.</span></span>

> [!WARNING]
> <span data-ttu-id="3a2f3-278">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-278">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="3a2f3-279">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-279">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span>
> 
> <span data-ttu-id="3a2f3-280">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="3a2f3-280">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a2f3-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a2f3-281">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a2f3-282">Use Apache Spark with Kafka</span><span class="sxs-lookup"><span data-stu-id="3a2f3-282">Use Apache Spark with Kafka</span></span>](../hdinsight-apache-kafka-spark-structured-streaming.md)

