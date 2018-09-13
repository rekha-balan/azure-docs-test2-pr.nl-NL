---
title: Monitor Hadoop clusters in HDInsight using the Ambari API | Microsoft Docs
description: Use the Apache Ambari APIs for creating, managing, and monitoring Hadoop clusters. Intuitive operator tools and APIs hide the complexity of Hadoop.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 1baeca35b82dbd97e1ac20cec9af3d1fef27bf1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555295"
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="97090-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span><span class="sxs-lookup"><span data-stu-id="97090-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="97090-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span><span class="sxs-lookup"><span data-stu-id="97090-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="97090-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="97090-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="97090-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="97090-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="97090-108">What is Ambari?</span><span class="sxs-lookup"><span data-stu-id="97090-108">What is Ambari?</span></span>
<span data-ttu-id="97090-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="97090-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="97090-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span><span class="sxs-lookup"><span data-stu-id="97090-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="97090-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="97090-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="97090-112">HDInsight currently supports only the Ambari monitoring feature.</span><span class="sxs-lookup"><span data-stu-id="97090-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="97090-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span><span class="sxs-lookup"><span data-stu-id="97090-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="97090-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span><span class="sxs-lookup"><span data-stu-id="97090-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="97090-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span><span class="sxs-lookup"><span data-stu-id="97090-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="97090-116">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="97090-116">**Prerequisites**</span></span>

<span data-ttu-id="97090-117">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="97090-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="97090-118">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="97090-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="97090-119">(Optional) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="97090-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="97090-120">To install it, see [cURL Releases and Downloads][curl-download].</span><span class="sxs-lookup"><span data-stu-id="97090-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="97090-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span><span class="sxs-lookup"><span data-stu-id="97090-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="97090-122">**An Azure HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="97090-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="97090-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="97090-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="97090-124">You need the following data to go through the tutorial:</span><span class="sxs-lookup"><span data-stu-id="97090-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="97090-125">Cluster property</span><span class="sxs-lookup"><span data-stu-id="97090-125">Cluster property</span></span> | <span data-ttu-id="97090-126">Azure PowerShell variable name</span><span class="sxs-lookup"><span data-stu-id="97090-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="97090-127">Value</span><span class="sxs-lookup"><span data-stu-id="97090-127">Value</span></span> | <span data-ttu-id="97090-128">Description</span><span class="sxs-lookup"><span data-stu-id="97090-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="97090-129">HDInsight cluster name</span><span class="sxs-lookup"><span data-stu-id="97090-129">HDInsight cluster name</span></span> |<span data-ttu-id="97090-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="97090-130">$clusterName</span></span> | |<span data-ttu-id="97090-131">The name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="97090-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="97090-132">Cluster username</span><span class="sxs-lookup"><span data-stu-id="97090-132">Cluster username</span></span> |<span data-ttu-id="97090-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="97090-133">$clusterUsername</span></span> | |<span data-ttu-id="97090-134">Cluster user name specified when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="97090-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="97090-135">Cluster password</span><span class="sxs-lookup"><span data-stu-id="97090-135">Cluster password</span></span> |<span data-ttu-id="97090-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="97090-136">$clusterPassword</span></span> | |<span data-ttu-id="97090-137">Cluster user password.</span><span class="sxs-lookup"><span data-stu-id="97090-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="97090-138">Jump-start</span><span class="sxs-lookup"><span data-stu-id="97090-138">Jump-start</span></span>
<span data-ttu-id="97090-139">There are several ways to use Ambari to monitor HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="97090-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="97090-140">**Use Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="97090-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="97090-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span><span class="sxs-lookup"><span data-stu-id="97090-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="97090-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span><span class="sxs-lookup"><span data-stu-id="97090-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="97090-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span><span class="sxs-lookup"><span data-stu-id="97090-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="97090-144">The output is:</span><span class="sxs-lookup"><span data-stu-id="97090-144">The output is:</span></span>

![Jobtracker Output][img-jobtracker-output]

<span data-ttu-id="97090-146">**Use cURL**</span><span class="sxs-lookup"><span data-stu-id="97090-146">**Use cURL**</span></span>

<span data-ttu-id="97090-147">The following example gets cluster information by using cURL:</span><span class="sxs-lookup"><span data-stu-id="97090-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="97090-148">The output is:</span><span class="sxs-lookup"><span data-stu-id="97090-148">The output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="97090-149">**For the 10/8/2014 release**:</span><span class="sxs-lookup"><span data-stu-id="97090-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="97090-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span><span class="sxs-lookup"><span data-stu-id="97090-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="97090-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="97090-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="97090-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span><span class="sxs-lookup"><span data-stu-id="97090-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="97090-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span><span class="sxs-lookup"><span data-stu-id="97090-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="97090-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span><span class="sxs-lookup"><span data-stu-id="97090-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="97090-155">Ambari monitoring APIs</span><span class="sxs-lookup"><span data-stu-id="97090-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="97090-156">The following table lists some of the most common Ambari monitoring API calls.</span><span class="sxs-lookup"><span data-stu-id="97090-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="97090-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="97090-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="97090-158">Monitor API call</span><span class="sxs-lookup"><span data-stu-id="97090-158">Monitor API call</span></span> | <span data-ttu-id="97090-159">URI</span><span class="sxs-lookup"><span data-stu-id="97090-159">URI</span></span> | <span data-ttu-id="97090-160">Description</span><span class="sxs-lookup"><span data-stu-id="97090-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97090-161">Get clusters</span><span class="sxs-lookup"><span data-stu-id="97090-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="97090-162">Get cluster info.</span><span class="sxs-lookup"><span data-stu-id="97090-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="97090-163">clusters, services, hosts</span><span class="sxs-lookup"><span data-stu-id="97090-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="97090-164">Get services</span><span class="sxs-lookup"><span data-stu-id="97090-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="97090-165">Services include: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="97090-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="97090-166">Get services info.</span><span class="sxs-lookup"><span data-stu-id="97090-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="97090-167">Get service components</span><span class="sxs-lookup"><span data-stu-id="97090-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="97090-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="97090-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="97090-169">Get component info.</span><span class="sxs-lookup"><span data-stu-id="97090-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="97090-170">ServiceComponentInfo, host-components, metrics</span><span class="sxs-lookup"><span data-stu-id="97090-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="97090-171">Get hosts</span><span class="sxs-lookup"><span data-stu-id="97090-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="97090-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="97090-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="97090-173">Get host info.</span><span class="sxs-lookup"><span data-stu-id="97090-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="97090-174">Get host components</span><span class="sxs-lookup"><span data-stu-id="97090-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="97090-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="97090-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="97090-176">Get host component info.</span><span class="sxs-lookup"><span data-stu-id="97090-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="97090-177">HostRoles, component, host, metrics</span><span class="sxs-lookup"><span data-stu-id="97090-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="97090-178">Get configurations</span><span class="sxs-lookup"><span data-stu-id="97090-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="97090-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="97090-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="97090-180">Get configuration info.</span><span class="sxs-lookup"><span data-stu-id="97090-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="97090-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="97090-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="97090-182">Next Steps</span><span class="sxs-lookup"><span data-stu-id="97090-182">Next Steps</span></span>
<span data-ttu-id="97090-183">Now you have learned how to use Ambari monitoring API calls.</span><span class="sxs-lookup"><span data-stu-id="97090-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="97090-184">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="97090-184">To learn more, see:</span></span>

* <span data-ttu-id="97090-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="97090-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="97090-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="97090-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="97090-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="97090-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="97090-188">[HDInsight documentation][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="97090-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="97090-189">[Get started with HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="97090-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-provision-clusters.md

[img-jobtracker-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png

