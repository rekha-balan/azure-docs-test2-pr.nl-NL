---
title: Manage Hadoop clusters in HDInsight with .NET SDK | Microsoft Docs
description: Learn how to perform administrative tasks for the Hadoop clusters in HDInsight using HDInsight .NET SDK.
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: ''
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jgao
ms.openlocfilehash: 3507a926b14c39f74794028c2e39f96f840fc4c4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662122"
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="60f7d-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="60f7d-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="60f7d-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="60f7d-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="60f7d-105">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="60f7d-105">**Prerequisites**</span></span>

<span data-ttu-id="60f7d-106">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="60f7d-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="60f7d-107">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="60f7d-107">**An Azure subscription**.</span></span> <span data-ttu-id="60f7d-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="60f7d-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="60f7d-109">Connect to Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="60f7d-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="60f7d-110">You need the following Nuget packages:</span><span class="sxs-lookup"><span data-stu-id="60f7d-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="60f7d-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="60f7d-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
            /// </summary>
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
        }
    }

<span data-ttu-id="60f7d-112">You shall see a prompt when you run this program.</span><span class="sxs-lookup"><span data-stu-id="60f7d-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="60f7d-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="60f7d-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="60f7d-114">Create clusters</span><span class="sxs-lookup"><span data-stu-id="60f7d-114">Create clusters</span></span>
<span data-ttu-id="60f7d-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="60f7d-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="60f7d-116">List clusters</span><span class="sxs-lookup"><span data-stu-id="60f7d-116">List clusters</span></span>
<span data-ttu-id="60f7d-117">The following code snippet lists clusters and some properties:</span><span class="sxs-lookup"><span data-stu-id="60f7d-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="60f7d-118">Delete clusters</span><span class="sxs-lookup"><span data-stu-id="60f7d-118">Delete clusters</span></span>
<span data-ttu-id="60f7d-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span><span class="sxs-lookup"><span data-stu-id="60f7d-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="60f7d-120">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="60f7d-120">Scale clusters</span></span>
<span data-ttu-id="60f7d-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="60f7d-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="60f7d-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span><span class="sxs-lookup"><span data-stu-id="60f7d-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="60f7d-123">If you are unsure of the version of your cluster, you can check the Properties page.</span><span class="sxs-lookup"><span data-stu-id="60f7d-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="60f7d-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="60f7d-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="60f7d-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span><span class="sxs-lookup"><span data-stu-id="60f7d-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="60f7d-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="60f7d-126">Hadoop</span></span>
  
    <span data-ttu-id="60f7d-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span><span class="sxs-lookup"><span data-stu-id="60f7d-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="60f7d-128">New jobs can also be submitted while the operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="60f7d-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="60f7d-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span><span class="sxs-lookup"><span data-stu-id="60f7d-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="60f7d-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span><span class="sxs-lookup"><span data-stu-id="60f7d-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="60f7d-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="60f7d-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="60f7d-132">You can, however, resubmit the jobs once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="60f7d-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="60f7d-133">HBase</span><span class="sxs-lookup"><span data-stu-id="60f7d-133">HBase</span></span>
  
    <span data-ttu-id="60f7d-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="60f7d-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="60f7d-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="60f7d-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="60f7d-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span><span class="sxs-lookup"><span data-stu-id="60f7d-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="60f7d-137">Storm</span><span class="sxs-lookup"><span data-stu-id="60f7d-137">Storm</span></span>
  
    <span data-ttu-id="60f7d-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="60f7d-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="60f7d-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span><span class="sxs-lookup"><span data-stu-id="60f7d-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="60f7d-140">Rebalancing can be accomplished in two ways:</span><span class="sxs-lookup"><span data-stu-id="60f7d-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="60f7d-141">Storm web UI</span><span class="sxs-lookup"><span data-stu-id="60f7d-141">Storm web UI</span></span>
  * <span data-ttu-id="60f7d-142">Command-line interface (CLI) tool</span><span class="sxs-lookup"><span data-stu-id="60f7d-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="60f7d-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span><span class="sxs-lookup"><span data-stu-id="60f7d-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="60f7d-144">The Storm web UI is available on the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="60f7d-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![HDInsight Storm scale rebalance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.storm.rebalance.png)
    
    <span data-ttu-id="60f7d-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span><span class="sxs-lookup"><span data-stu-id="60f7d-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="60f7d-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span><span class="sxs-lookup"><span data-stu-id="60f7d-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="60f7d-148">Grant/revoke access</span><span class="sxs-lookup"><span data-stu-id="60f7d-148">Grant/revoke access</span></span>
<span data-ttu-id="60f7d-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span><span class="sxs-lookup"><span data-stu-id="60f7d-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="60f7d-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="60f7d-150">ODBC</span></span>
* <span data-ttu-id="60f7d-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="60f7d-151">JDBC</span></span>
* <span data-ttu-id="60f7d-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="60f7d-152">Ambari</span></span>
* <span data-ttu-id="60f7d-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="60f7d-153">Oozie</span></span>
* <span data-ttu-id="60f7d-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="60f7d-154">Templeton</span></span>

<span data-ttu-id="60f7d-155">By default, these services are granted for access.</span><span class="sxs-lookup"><span data-stu-id="60f7d-155">By default, these services are granted for access.</span></span> <span data-ttu-id="60f7d-156">You can revoke/grant the access.</span><span class="sxs-lookup"><span data-stu-id="60f7d-156">You can revoke/grant the access.</span></span> <span data-ttu-id="60f7d-157">To revoke:</span><span class="sxs-lookup"><span data-stu-id="60f7d-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="60f7d-158">To grant:</span><span class="sxs-lookup"><span data-stu-id="60f7d-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="60f7d-159">By granting/revoking the access, you will reset the cluster user name and password.</span><span class="sxs-lookup"><span data-stu-id="60f7d-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="60f7d-160">This can also be done via the Portal.</span><span class="sxs-lookup"><span data-stu-id="60f7d-160">This can also be done via the Portal.</span></span> <span data-ttu-id="60f7d-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="60f7d-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="60f7d-162">Update HTTP user credentials</span><span class="sxs-lookup"><span data-stu-id="60f7d-162">Update HTTP user credentials</span></span>
<span data-ttu-id="60f7d-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span><span class="sxs-lookup"><span data-stu-id="60f7d-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="60f7d-164">And then grant the access with new HTTP user credentials.</span><span class="sxs-lookup"><span data-stu-id="60f7d-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="60f7d-165">Find the default storage account</span><span class="sxs-lookup"><span data-stu-id="60f7d-165">Find the default storage account</span></span>
<span data-ttu-id="60f7d-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span><span class="sxs-lookup"><span data-stu-id="60f7d-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="60f7d-167">Submit jobs</span><span class="sxs-lookup"><span data-stu-id="60f7d-167">Submit jobs</span></span>
<span data-ttu-id="60f7d-168">**To submit MapReduce jobs**</span><span class="sxs-lookup"><span data-stu-id="60f7d-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="60f7d-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="60f7d-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="60f7d-170">**To submit Hive jobs**</span><span class="sxs-lookup"><span data-stu-id="60f7d-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="60f7d-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="60f7d-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="60f7d-172">**To submit Pig jobs**</span><span class="sxs-lookup"><span data-stu-id="60f7d-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="60f7d-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="60f7d-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="60f7d-174">**To submit Sqoop jobs**</span><span class="sxs-lookup"><span data-stu-id="60f7d-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="60f7d-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="60f7d-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="60f7d-176">**To submit Oozie jobs**</span><span class="sxs-lookup"><span data-stu-id="60f7d-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="60f7d-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="60f7d-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="60f7d-178">Upload data to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="60f7d-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="60f7d-179">See [Upload data to HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="60f7d-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="60f7d-180">See Also</span><span class="sxs-lookup"><span data-stu-id="60f7d-180">See Also</span></span>
* [<span data-ttu-id="60f7d-181">HDInsight .NET SDK reference documentation</span><span class="sxs-lookup"><span data-stu-id="60f7d-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="60f7d-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="60f7d-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="60f7d-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="60f7d-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="60f7d-184">[Create HDInsight clusters][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="60f7d-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="60f7d-185">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="60f7d-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="60f7d-186">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="60f7d-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-provision-custom-options]: hdinsight-provision-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md



