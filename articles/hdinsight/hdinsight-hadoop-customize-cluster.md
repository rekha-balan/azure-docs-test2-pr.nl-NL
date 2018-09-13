---
title: Customize HDInsight Clusters using script actions | Microsoft Docs
description: Learn how to customize HDInsight clusters using Script Action.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 35126019f3146d1a968ff2550cb22daded0fcdc5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555844"
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="d1167-103">Customize Windows-based HDInsight clusters using Script Action</span><span class="sxs-lookup"><span data-stu-id="d1167-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="d1167-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="d1167-105">The information in this article is specific to Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="d1167-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d1167-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d1167-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1167-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="d1167-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d1167-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="d1167-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

<span data-ttu-id="d1167-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="d1167-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d1167-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure Portal.</span></span> <span data-ttu-id="d1167-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="d1167-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="d1167-112">Script Action in the cluster creation process</span><span class="sxs-lookup"><span data-stu-id="d1167-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="d1167-113">Script Action is only used while a clusters is in the process of being created.</span><span class="sxs-lookup"><span data-stu-id="d1167-113">Script Action is only used while a clusters is in the process of being created.</span></span> <span data-ttu-id="d1167-114">The following diagram illustrates when Script Action is executed during the creation process:</span><span class="sxs-lookup"><span data-stu-id="d1167-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="d1167-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="d1167-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="d1167-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span><span class="sxs-lookup"><span data-stu-id="d1167-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="d1167-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span><span class="sxs-lookup"><span data-stu-id="d1167-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="d1167-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span><span class="sxs-lookup"><span data-stu-id="d1167-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="d1167-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span><span class="sxs-lookup"><span data-stu-id="d1167-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="d1167-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span><span class="sxs-lookup"><span data-stu-id="d1167-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="d1167-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span><span class="sxs-lookup"><span data-stu-id="d1167-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="d1167-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="d1167-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="d1167-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="d1167-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span><span class="sxs-lookup"><span data-stu-id="d1167-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="d1167-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="d1167-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span><span class="sxs-lookup"><span data-stu-id="d1167-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="d1167-127">A script can be ran on the head node, the worker nodes, or both.</span><span class="sxs-lookup"><span data-stu-id="d1167-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="d1167-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="d1167-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="d1167-129">Name</span><span class="sxs-lookup"><span data-stu-id="d1167-129">Name</span></span> | <span data-ttu-id="d1167-130">Script</span><span class="sxs-lookup"><span data-stu-id="d1167-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="d1167-131">**Install Spark**</span><span class="sxs-lookup"><span data-stu-id="d1167-131">**Install Spark**</span></span> |<span data-ttu-id="d1167-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="d1167-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="d1167-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="d1167-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="d1167-134">**Install R**</span><span class="sxs-lookup"><span data-stu-id="d1167-134">**Install R**</span></span> |<span data-ttu-id="d1167-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="d1167-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="d1167-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="d1167-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="d1167-137">**Install Solr**</span><span class="sxs-lookup"><span data-stu-id="d1167-137">**Install Solr**</span></span> |<span data-ttu-id="d1167-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="d1167-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="d1167-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="d1167-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="d1167-140">- **Install Giraph**</span><span class="sxs-lookup"><span data-stu-id="d1167-140">- **Install Giraph**</span></span> |<span data-ttu-id="d1167-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="d1167-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="d1167-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="d1167-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="d1167-143">**Pre-load Hive libraries**</span><span class="sxs-lookup"><span data-stu-id="d1167-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="d1167-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="d1167-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="d1167-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d1167-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="d1167-146">Call scripts using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1167-146">Call scripts using the Azure Portal</span></span>
<span data-ttu-id="d1167-147">**From the Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="d1167-147">**From the Azure Portal**</span></span>

1. <span data-ttu-id="d1167-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d1167-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="d1167-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span><span class="sxs-lookup"><span data-stu-id="d1167-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="d1167-150">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span><span class="sxs-lookup"><span data-stu-id="d1167-150">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d1167-151">Property</span><span class="sxs-lookup"><span data-stu-id="d1167-151">Property</span></span></th><th><span data-ttu-id="d1167-152">Value</span><span class="sxs-lookup"><span data-stu-id="d1167-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d1167-153">Name</span><span class="sxs-lookup"><span data-stu-id="d1167-153">Name</span></span></td>
            <td><span data-ttu-id="d1167-154">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="d1167-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="d1167-155">Script URI</span><span class="sxs-lookup"><span data-stu-id="d1167-155">Script URI</span></span></td>
            <td><span data-ttu-id="d1167-156">Specify the URI to the script that is invoked to customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="d1167-157">s</span><span class="sxs-lookup"><span data-stu-id="d1167-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="d1167-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="d1167-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="d1167-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span><span class="sxs-lookup"><span data-stu-id="d1167-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="d1167-160">Parameters</span><span class="sxs-lookup"><span data-stu-id="d1167-160">Parameters</span></span></td>
            <td><span data-ttu-id="d1167-161">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="d1167-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="d1167-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="d1167-163">Click **Select** to save the script action configuration and continue with cluster creation.</span><span class="sxs-lookup"><span data-stu-id="d1167-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="d1167-164">Call scripts using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1167-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="d1167-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="d1167-166">To install other software, you will need to replace the script file in the script:</span><span class="sxs-lookup"><span data-stu-id="d1167-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="d1167-167">When prompted, enter the credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="d1167-168">It can take several minutes before the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="d1167-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="d1167-169">Call scripts using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d1167-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="d1167-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="d1167-171">To install other software, you will need to replace the script file in the code.</span><span class="sxs-lookup"><span data-stu-id="d1167-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="d1167-172">**To create an HDInsight cluster with Spark**</span><span class="sxs-lookup"><span data-stu-id="d1167-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="d1167-173">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1167-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d1167-174">From the Nuget Package Manager Console, run the following command.</span><span class="sxs-lookup"><span data-stu-id="d1167-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="d1167-175">Use the following using statements in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="d1167-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="d1167-176">Place the code in the class with the following:</span><span class="sxs-lookup"><span data-stu-id="d1167-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,

                DefaultStorageAccountName = ExistingStorageName,
                DefaultStorageAccountKey = ExistingStorageKey,
                DefaultStorageContainer = ExistingContainer,

                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="d1167-177">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="d1167-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="d1167-178">Support for open-source software used on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="d1167-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="d1167-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1167-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="d1167-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span><span class="sxs-lookup"><span data-stu-id="d1167-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="d1167-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span><span class="sxs-lookup"><span data-stu-id="d1167-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="d1167-182">There are two types of open-source components that are available in the HDInsight service:</span><span class="sxs-lookup"><span data-stu-id="d1167-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="d1167-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="d1167-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span><span class="sxs-lookup"><span data-stu-id="d1167-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="d1167-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span><span class="sxs-lookup"><span data-stu-id="d1167-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="d1167-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span><span class="sxs-lookup"><span data-stu-id="d1167-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="d1167-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="d1167-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="d1167-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="d1167-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="d1167-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="d1167-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="d1167-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span><span class="sxs-lookup"><span data-stu-id="d1167-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="d1167-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="d1167-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="d1167-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d1167-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="d1167-193">The HDInsight service provides several ways to use custom components.</span><span class="sxs-lookup"><span data-stu-id="d1167-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="d1167-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span><span class="sxs-lookup"><span data-stu-id="d1167-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="d1167-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="d1167-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="d1167-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1167-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="d1167-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="d1167-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="d1167-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="d1167-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="d1167-199">These samples are provided without support.</span><span class="sxs-lookup"><span data-stu-id="d1167-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="d1167-200">Develop Script Action scripts</span><span class="sxs-lookup"><span data-stu-id="d1167-200">Develop Script Action scripts</span></span>
<span data-ttu-id="d1167-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="d1167-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="d1167-202">See also</span><span class="sxs-lookup"><span data-stu-id="d1167-202">See also</span></span>
* <span data-ttu-id="d1167-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span><span class="sxs-lookup"><span data-stu-id="d1167-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="d1167-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="d1167-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="d1167-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="d1167-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="d1167-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="d1167-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="d1167-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="d1167-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="d1167-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="d1167-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-provision-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"


