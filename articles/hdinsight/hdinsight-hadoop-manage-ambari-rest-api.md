---
title: Monitor and manage Azure HDInsight using Ambari REST API | Microsoft Docs
description: Learn how to use Ambari to monitor and manage Linux-based HDInsight clusters. In this document, you will learn how to use the Ambari REST API included with HDInsight clusters.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/23/2017
ms.author: larryfr
ms.openlocfilehash: 36e2c7b08a22946129bf91b478da9b2e191d353a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552119"
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="e0f5c-104">Manage HDInsight clusters by using the Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="e0f5c-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="e0f5c-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="e0f5c-106">Ambari is included on HDInsight clusters that use the Linux operating system, and is used to monitor the cluster and make configuration changes.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-106">Ambari is included on HDInsight clusters that use the Linux operating system, and is used to monitor the cluster and make configuration changes.</span></span> <span data-ttu-id="e0f5c-107">In this document, you learn the basics of working with the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-107">In this document, you learn the basics of working with the Ambari REST API.</span></span>

## <a id="whatis"></a><span data-ttu-id="e0f5c-108">What is Ambari</span><span class="sxs-lookup"><span data-stu-id="e0f5c-108">What is Ambari</span></span>

<span data-ttu-id="e0f5c-109">[Apache Ambari](http://ambari.apache.org) makes Hadoop management simpler by providing an easy-to-use web UI that can be used to provision, manage, and monitor Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-109">[Apache Ambari](http://ambari.apache.org) makes Hadoop management simpler by providing an easy-to-use web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="e0f5c-110">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-110">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="e0f5c-111">Ambari is provided by default with Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-111">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="e0f5c-112">How to use the Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="e0f5c-112">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0f5c-113">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-113">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="e0f5c-114">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-114">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="e0f5c-115">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-115">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="e0f5c-116">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-116">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="e0f5c-117">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-117">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="e0f5c-118">If using the __Bourne shell__ (Bash), you must have the following installed:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-118">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="e0f5c-119">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-119">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="e0f5c-120">In this document, it is used to communicate with the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-120">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="e0f5c-121">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-121">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="e0f5c-122">Jq is a utility for working with JSON documents.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-122">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="e0f5c-123">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-123">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="e0f5c-124">Base URI for Ambari Rest API</span><span class="sxs-lookup"><span data-stu-id="e0f5c-124">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="e0f5c-125">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-125">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0f5c-126">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-126">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="e0f5c-127">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-127">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="e0f5c-128">The following URIs return an error because the second occurrence of the name is not the correct case.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-128">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="e0f5c-129">Authentication</span><span class="sxs-lookup"><span data-stu-id="e0f5c-129">Authentication</span></span>

<span data-ttu-id="e0f5c-130">Connecting to Ambari on HDInsight requires HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-130">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="e0f5c-131">When authenticating the connection, you must use the admin account name (the default is **admin**) and password you provided when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-131">When authenticating the connection, you must use the admin account name (the default is **admin**) and password you provided when the cluster was created.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="e0f5c-132">Examples: Authentication and parsing JSON</span><span class="sxs-lookup"><span data-stu-id="e0f5c-132">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="e0f5c-133">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-133">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="e0f5c-134">The Bash examples in this document make the following assumptions:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-134">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="e0f5c-135">The login name for the cluster is the default value of `admin`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-135">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="e0f5c-136">`$PASSWORD` contains the password for the HDInsight login command.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-136">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="e0f5c-137">You can set this value by using `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-137">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="e0f5c-138">`$CLUSTERNAME` contains the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-138">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="e0f5c-139">You can set this value by using `set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="e0f5c-139">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="e0f5c-140">The PowerShell examples in this document make the following assumptions:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-140">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="e0f5c-141">`$creds` is a credential object that contains the admin login and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-141">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="e0f5c-142">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-142">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="e0f5c-143">`$clusterName` is a string that contains the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-143">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="e0f5c-144">You can set this value by using `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-144">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="e0f5c-145">Both examples return a JSON document that begins with information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-145">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="e0f5c-146">Parsing JSON data</span><span class="sxs-lookup"><span data-stu-id="e0f5c-146">Parsing JSON data</span></span>

<span data-ttu-id="e0f5c-147">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-147">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="e0f5c-148">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-148">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="e0f5c-149">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-149">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="e0f5c-150">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-150">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="e0f5c-151">Jq is used in this example to construct a new template from the JSON response document.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-151">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="e0f5c-152">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-152">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="e0f5c-153">Example: Get the FQDN of cluster nodes</span><span class="sxs-lookup"><span data-stu-id="e0f5c-153">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="e0f5c-154">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-154">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="e0f5c-155">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-155">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="e0f5c-156">**All nodes**</span><span class="sxs-lookup"><span data-stu-id="e0f5c-156">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="e0f5c-157">**Head nodes**</span><span class="sxs-lookup"><span data-stu-id="e0f5c-157">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="e0f5c-158">**Worker nodes**</span><span class="sxs-lookup"><span data-stu-id="e0f5c-158">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="e0f5c-159">**Zookeeper nodes**</span><span class="sxs-lookup"><span data-stu-id="e0f5c-159">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="e0f5c-160">Example: Get the internal IP address of cluster nodes</span><span class="sxs-lookup"><span data-stu-id="e0f5c-160">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0f5c-161">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-161">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="e0f5c-162">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-162">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="e0f5c-163">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-163">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="e0f5c-164">You must know the FQDN for the host before you can obtain the IP address.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-164">You must know the FQDN for the host before you can obtain the IP address.</span></span> <span data-ttu-id="e0f5c-165">Once you have the FQDN, you can then get the IP address of the host.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-165">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="e0f5c-166">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-166">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="e0f5c-167">Example: Get the default storage</span><span class="sxs-lookup"><span data-stu-id="e0f5c-167">Example: Get the default storage</span></span>

<span data-ttu-id="e0f5c-168">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-168">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="e0f5c-169">You can use Ambari to retrieve this information after the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-169">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="e0f5c-170">For example, if you want to read/write data to the container outside HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-170">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="e0f5c-171">The following examples retrieve the default storage configuration from the cluster:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-171">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="e0f5c-172">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-172">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="e0f5c-173">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-173">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="e0f5c-174">The return value is similar to one of the following examples:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-174">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="e0f5c-175">`wasbs://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-175">`wasbs://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="e0f5c-176">The `ACCOUNTNAME` value is the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-176">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="e0f5c-177">The `CONTAINER` portion is the name of the blob container in the storage account.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-177">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="e0f5c-178">The container is the root of the HDFS compatible storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-178">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="e0f5c-179">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-179">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="e0f5c-180">To find the Data Lake Store account name, use the following examples:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-180">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="e0f5c-181">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-181">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="e0f5c-182">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-182">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="e0f5c-183">The return value is similar to `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-183">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="e0f5c-184">This value is a path within the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-184">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="e0f5c-185">This path is the root of the HDFS compatible file system for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-185">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0f5c-186">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](https://docs.microsoft.com/powershell/) also returns the storage information for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-186">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](https://docs.microsoft.com/powershell/) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="e0f5c-187">Example: Get configuration</span><span class="sxs-lookup"><span data-stu-id="e0f5c-187">Example: Get configuration</span></span>

1. <span data-ttu-id="e0f5c-188">Get the configurations that are available for your cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-188">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="e0f5c-189">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-189">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="e0f5c-190">The following example is an excerpt from the data returned from a Spark cluster type.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-190">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="e0f5c-191">Get the configuration for the component that you are interested in.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-191">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="e0f5c-192">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-192">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="e0f5c-193">This example returns a JSON document containing the current configuration for the `core-site` component.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-193">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="e0f5c-194">Example: Update configuration</span><span class="sxs-lookup"><span data-stu-id="e0f5c-194">Example: Update configuration</span></span>

1. <span data-ttu-id="e0f5c-195">Get the current configuration, which Ambari stores as the "desired configuration":</span><span class="sxs-lookup"><span data-stu-id="e0f5c-195">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="e0f5c-196">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-196">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="e0f5c-197">The following example is an excerpt from the data returned from a Spark cluster type.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-197">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="e0f5c-198">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-198">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="e0f5c-199">Retrieve the configuration for the component and tag by using the following commands.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-199">Retrieve the configuration for the component and tag by using the following commands.</span></span> <span data-ttu-id="e0f5c-200">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-200">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```
   
    <span data-ttu-id="e0f5c-201">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-201">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="e0f5c-202">Specifically, these examples perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-202">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="e0f5c-203">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-203">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="e0f5c-204">Creates a root document for the new desired configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-204">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="e0f5c-205">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-205">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="e0f5c-206">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-206">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="e0f5c-207">Adds a `tag` element with a value of `version#################`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-207">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="e0f5c-208">The numeric portion is based on the current date.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-208">The numeric portion is based on the current date.</span></span> <span data-ttu-id="e0f5c-209">Each configuration must have a unique tag.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-209">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="e0f5c-210">Finally, the data is saved to the `newconfig.json` document.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-210">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="e0f5c-211">The document structure should appear similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-211">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="e0f5c-212">Open the `newconfig.json` document and modify/add values in the `properties` object.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-212">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="e0f5c-213">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-213">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="e0f5c-214">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-214">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="e0f5c-215">Save the file once you are done making modifications.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-215">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="e0f5c-216">Use the following commands to submit the updated configuration to Ambari.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-216">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="e0f5c-217">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-217">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="e0f5c-218">The request returns a JSON document.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-218">The request returns a JSON document.</span></span> <span data-ttu-id="e0f5c-219">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-219">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="e0f5c-220">Example: Restart a service component</span><span class="sxs-lookup"><span data-stu-id="e0f5c-220">Example: Restart a service component</span></span>

<span data-ttu-id="e0f5c-221">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-221">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="e0f5c-222">Use the following steps to restart the service.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-222">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="e0f5c-223">Use the following to enable maintenance mode for the Spark service:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-223">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="e0f5c-224">These commands send a JSON document to the server that turns on maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-224">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="e0f5c-225">You can verify that the service is now in maintenance mode using the following request:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-225">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="e0f5c-226">The return value is `ON`.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-226">The return value is `ON`.</span></span>

2. <span data-ttu-id="e0f5c-227">Next, use the following to turn off the service:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-227">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="e0f5c-228">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-228">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="e0f5c-229">The `href` value returned by this URI is using the internal IP address of the cluster node.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-229">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="e0f5c-230">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-230">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="e0f5c-231">The following commands retrieve the status of the request:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-231">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="e0f5c-232">A response of `COMPLETED` indicates that the request has finished.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-232">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="e0f5c-233">Once the previous request completes, use the following to start the service.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-233">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="e0f5c-234">The service is now using the new configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-234">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="e0f5c-235">Finally, use the following to turn off maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-235">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="e0f5c-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0f5c-236">Next steps</span></span>

<span data-ttu-id="e0f5c-237">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-237">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

