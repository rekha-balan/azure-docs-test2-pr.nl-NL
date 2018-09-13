---
title: Monitor and manage Hadoop with Ambari REST API - Azure HDInsight
description: Learn how to use Ambari to monitor and manage Hadoop clusters in Azure HDInsight. In this document, you will learn how to use the Ambari REST API included with HDInsight clusters.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/23/2018
ms.author: jasonh
ms.openlocfilehash: d6e2bdba7e3536404f087dc468a0895d0be0c2a0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812018"
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="ffab5-104">Manage HDInsight clusters by using the Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="ffab5-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="ffab5-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ffab5-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="ffab5-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span><span class="sxs-lookup"><span data-stu-id="ffab5-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="ffab5-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="ffab5-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="ffab5-108">You can use Ambari to monitor the cluster and make configuration changes.</span><span class="sxs-lookup"><span data-stu-id="ffab5-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <a id="whatis"></a><span data-ttu-id="ffab5-109">What is Ambari</span><span class="sxs-lookup"><span data-stu-id="ffab5-109">What is Ambari</span></span>

<span data-ttu-id="ffab5-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to manage and monitor Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="ffab5-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to manage and monitor Hadoop clusters.</span></span> <span data-ttu-id="ffab5-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="ffab5-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="ffab5-112">Ambari is provided by default with Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="ffab5-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="ffab5-113">How to use the Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="ffab5-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffab5-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="ffab5-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="ffab5-115">For more information, see [Get started with HDInsight](hadoop/apache-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ffab5-115">For more information, see [Get started with HDInsight](hadoop/apache-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="ffab5-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffab5-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="ffab5-117">The bash examples were tested with GNU bash version 4.3.11, but should work with other Unix shells.</span><span class="sxs-lookup"><span data-stu-id="ffab5-117">The bash examples were tested with GNU bash version 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="ffab5-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span><span class="sxs-lookup"><span data-stu-id="ffab5-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="ffab5-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span><span class="sxs-lookup"><span data-stu-id="ffab5-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="ffab5-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span><span class="sxs-lookup"><span data-stu-id="ffab5-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="ffab5-121">In this document, it is used to communicate with the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="ffab5-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="ffab5-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span><span class="sxs-lookup"><span data-stu-id="ffab5-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="ffab5-123">Jq is a utility for working with JSON documents.</span><span class="sxs-lookup"><span data-stu-id="ffab5-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="ffab5-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span><span class="sxs-lookup"><span data-stu-id="ffab5-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="ffab5-125">Base URI for Ambari Rest API</span><span class="sxs-lookup"><span data-stu-id="ffab5-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="ffab5-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffab5-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="ffab5-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="ffab5-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span><span class="sxs-lookup"><span data-stu-id="ffab5-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="ffab5-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span><span class="sxs-lookup"><span data-stu-id="ffab5-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="ffab5-130">Authentication</span><span class="sxs-lookup"><span data-stu-id="ffab5-130">Authentication</span></span>

<span data-ttu-id="ffab5-131">Connecting to Ambari on HDInsight requires HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ffab5-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="ffab5-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="ffab5-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="ffab5-133">Examples: Authentication and parsing JSON</span><span class="sxs-lookup"><span data-stu-id="ffab5-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="ffab5-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span><span class="sxs-lookup"><span data-stu-id="ffab5-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="ffab5-135">The Bash examples in this document make the following assumptions:</span><span class="sxs-lookup"><span data-stu-id="ffab5-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="ffab5-136">The login name for the cluster is the default value of `admin`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="ffab5-137">`$CLUSTERNAME` contains the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-137">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="ffab5-138">You can set this value by using `set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="ffab5-138">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>
> * <span data-ttu-id="ffab5-139">When prompted, enter the password for the cluster login (admin).</span><span class="sxs-lookup"><span data-stu-id="ffab5-139">When prompted, enter the password for the cluster login (admin).</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="ffab5-140">The PowerShell examples in this document make the following assumptions:</span><span class="sxs-lookup"><span data-stu-id="ffab5-140">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="ffab5-141">`$creds` is a credential object that contains the admin login and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-141">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="ffab5-142">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="ffab5-142">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="ffab5-143">`$clusterName` is a string that contains the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-143">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="ffab5-144">You can set this value by using `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-144">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="ffab5-145">Both examples return a JSON document that begins with information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ffab5-145">Both examples return a JSON document that begins with information similar to the following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="ffab5-146">Parsing JSON data</span><span class="sxs-lookup"><span data-stu-id="ffab5-146">Parsing JSON data</span></span>

<span data-ttu-id="ffab5-147">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span><span class="sxs-lookup"><span data-stu-id="ffab5-147">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="ffab5-148">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffab5-148">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="ffab5-149">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span><span class="sxs-lookup"><span data-stu-id="ffab5-149">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="ffab5-150">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span><span class="sxs-lookup"><span data-stu-id="ffab5-150">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="ffab5-151">Jq is used in this example to construct a new template from the JSON response document.</span><span class="sxs-lookup"><span data-stu-id="ffab5-151">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="ffab5-152">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="ffab5-152">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="ffab5-153">Example: Get the FQDN of cluster nodes</span><span class="sxs-lookup"><span data-stu-id="ffab5-153">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="ffab5-154">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span><span class="sxs-lookup"><span data-stu-id="ffab5-154">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="ffab5-155">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span><span class="sxs-lookup"><span data-stu-id="ffab5-155">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="ffab5-156">**All nodes**</span><span class="sxs-lookup"><span data-stu-id="ffab5-156">**All nodes**</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="ffab5-157">**Head nodes**</span><span class="sxs-lookup"><span data-stu-id="ffab5-157">**Head nodes**</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="ffab5-158">**Worker nodes**</span><span class="sxs-lookup"><span data-stu-id="ffab5-158">**Worker nodes**</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="ffab5-159">**Zookeeper nodes**</span><span class="sxs-lookup"><span data-stu-id="ffab5-159">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="ffab5-160">Example: Get the internal IP address of cluster nodes</span><span class="sxs-lookup"><span data-stu-id="ffab5-160">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffab5-161">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="ffab5-161">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="ffab5-162">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-162">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="ffab5-163">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="ffab5-163">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="ffab5-164">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="ffab5-164">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="ffab5-165">Once you have the FQDN, you can then get the IP address of the host.</span><span class="sxs-lookup"><span data-stu-id="ffab5-165">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="ffab5-166">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span><span class="sxs-lookup"><span data-stu-id="ffab5-166">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

> [!TIP]
> <span data-ttu-id="ffab5-167">Previous examples prompt you for the password.</span><span class="sxs-lookup"><span data-stu-id="ffab5-167">Previous examples prompt you for the password.</span></span> <span data-ttu-id="ffab5-168">This example runs the `curl` command multiple times, so the password is provided as `$PASSWORD` to avoid multiple prompts.</span><span class="sxs-lookup"><span data-stu-id="ffab5-168">This example runs the `curl` command multiple times, so the password is provided as `$PASSWORD` to avoid multiple prompts.</span></span>

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

## <a name="example-get-the-default-storage"></a><span data-ttu-id="ffab5-169">Example: Get the default storage</span><span class="sxs-lookup"><span data-stu-id="ffab5-169">Example: Get the default storage</span></span>

<span data-ttu-id="ffab5-170">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-170">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="ffab5-171">You can use Ambari to retrieve this information after the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="ffab5-171">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="ffab5-172">For example, if you want to read/write data to the container outside HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ffab5-172">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="ffab5-173">The following examples retrieve the default storage configuration from the cluster:</span><span class="sxs-lookup"><span data-stu-id="ffab5-173">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="ffab5-174">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span><span class="sxs-lookup"><span data-stu-id="ffab5-174">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="ffab5-175">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span><span class="sxs-lookup"><span data-stu-id="ffab5-175">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="ffab5-176">The return value is similar to one of the following examples:</span><span class="sxs-lookup"><span data-stu-id="ffab5-176">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="ffab5-177">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span><span class="sxs-lookup"><span data-stu-id="ffab5-177">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="ffab5-178">The `ACCOUNTNAME` value is the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="ffab5-178">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="ffab5-179">The `CONTAINER` portion is the name of the blob container in the storage account.</span><span class="sxs-lookup"><span data-stu-id="ffab5-179">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="ffab5-180">The container is the root of the HDFS compatible storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-180">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="ffab5-181">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span><span class="sxs-lookup"><span data-stu-id="ffab5-181">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="ffab5-182">To find the Data Lake Store account name, use the following examples:</span><span class="sxs-lookup"><span data-stu-id="ffab5-182">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="ffab5-183">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="ffab5-183">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="ffab5-184">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span><span class="sxs-lookup"><span data-stu-id="ffab5-184">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="ffab5-185">The return value is similar to `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-185">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="ffab5-186">This value is a path within the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="ffab5-186">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="ffab5-187">This path is the root of the HDFS compatible file system for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-187">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="ffab5-188">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-188">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="ffab5-189">Example: Get configuration</span><span class="sxs-lookup"><span data-stu-id="ffab5-189">Example: Get configuration</span></span>

1. <span data-ttu-id="ffab5-190">Get the configurations that are available for your cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-190">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="ffab5-191">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-191">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="ffab5-192">The following example is an excerpt from the data returned from a Spark cluster type.</span><span class="sxs-lookup"><span data-stu-id="ffab5-192">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="ffab5-193">Get the configuration for the component that you are interested in.</span><span class="sxs-lookup"><span data-stu-id="ffab5-193">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="ffab5-194">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span><span class="sxs-lookup"><span data-stu-id="ffab5-194">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="ffab5-195">This example returns a JSON document containing the current configuration for the `core-site` component.</span><span class="sxs-lookup"><span data-stu-id="ffab5-195">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="ffab5-196">Example: Update configuration</span><span class="sxs-lookup"><span data-stu-id="ffab5-196">Example: Update configuration</span></span>

1. <span data-ttu-id="ffab5-197">Get the current configuration, which Ambari stores as the "desired configuration":</span><span class="sxs-lookup"><span data-stu-id="ffab5-197">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="ffab5-198">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-198">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="ffab5-199">The following example is an excerpt from the data returned from a Spark cluster type.</span><span class="sxs-lookup"><span data-stu-id="ffab5-199">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="ffab5-200">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span><span class="sxs-lookup"><span data-stu-id="ffab5-200">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="ffab5-201">Retrieve the configuration for the component and tag by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="ffab5-201">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
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

    > [!NOTE]
    > <span data-ttu-id="ffab5-202">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span><span class="sxs-lookup"><span data-stu-id="ffab5-202">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="ffab5-203">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span><span class="sxs-lookup"><span data-stu-id="ffab5-203">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="ffab5-204">Specifically, these examples perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="ffab5-204">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="ffab5-205">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-205">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="ffab5-206">Creates a root document for the new desired configuration.</span><span class="sxs-lookup"><span data-stu-id="ffab5-206">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="ffab5-207">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span><span class="sxs-lookup"><span data-stu-id="ffab5-207">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="ffab5-208">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span><span class="sxs-lookup"><span data-stu-id="ffab5-208">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="ffab5-209">Adds a `tag` element with a value of `version#################`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-209">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="ffab5-210">The numeric portion is based on the current date.</span><span class="sxs-lookup"><span data-stu-id="ffab5-210">The numeric portion is based on the current date.</span></span> <span data-ttu-id="ffab5-211">Each configuration must have a unique tag.</span><span class="sxs-lookup"><span data-stu-id="ffab5-211">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="ffab5-212">Finally, the data is saved to the `newconfig.json` document.</span><span class="sxs-lookup"><span data-stu-id="ffab5-212">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="ffab5-213">The document structure should appear similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ffab5-213">The document structure should appear similar to the following example:</span></span>
     
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

3. <span data-ttu-id="ffab5-214">Open the `newconfig.json` document and modify/add values in the `properties` object.</span><span class="sxs-lookup"><span data-stu-id="ffab5-214">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="ffab5-215">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-215">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="ffab5-216">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-216">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="ffab5-217">Save the file once you are done making modifications.</span><span class="sxs-lookup"><span data-stu-id="ffab5-217">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="ffab5-218">Use the following commands to submit the updated configuration to Ambari.</span><span class="sxs-lookup"><span data-stu-id="ffab5-218">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
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
   
    <span data-ttu-id="ffab5-219">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span><span class="sxs-lookup"><span data-stu-id="ffab5-219">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="ffab5-220">The request returns a JSON document.</span><span class="sxs-lookup"><span data-stu-id="ffab5-220">The request returns a JSON document.</span></span> <span data-ttu-id="ffab5-221">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span><span class="sxs-lookup"><span data-stu-id="ffab5-221">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="ffab5-222">Example: Restart a service component</span><span class="sxs-lookup"><span data-stu-id="ffab5-222">Example: Restart a service component</span></span>

<span data-ttu-id="ffab5-223">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span><span class="sxs-lookup"><span data-stu-id="ffab5-223">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="ffab5-224">Use the following steps to restart the service.</span><span class="sxs-lookup"><span data-stu-id="ffab5-224">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="ffab5-225">Use the following to enable maintenance mode for the Spark service:</span><span class="sxs-lookup"><span data-stu-id="ffab5-225">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" \
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
   
    <span data-ttu-id="ffab5-226">These commands send a JSON document to the server that turns on maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="ffab5-226">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="ffab5-227">You can verify that the service is now in maintenance mode using the following request:</span><span class="sxs-lookup"><span data-stu-id="ffab5-227">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="ffab5-228">The return value is `ON`.</span><span class="sxs-lookup"><span data-stu-id="ffab5-228">The return value is `ON`.</span></span>

2. <span data-ttu-id="ffab5-229">Next, use the following to turn off the service:</span><span class="sxs-lookup"><span data-stu-id="ffab5-229">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" \
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
    
    <span data-ttu-id="ffab5-230">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ffab5-230">The response is similar to the following example:</span></span>
   
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
    > <span data-ttu-id="ffab5-231">The `href` value returned by this URI is using the internal IP address of the cluster node.</span><span class="sxs-lookup"><span data-stu-id="ffab5-231">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="ffab5-232">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span><span class="sxs-lookup"><span data-stu-id="ffab5-232">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="ffab5-233">The following commands retrieve the status of the request:</span><span class="sxs-lookup"><span data-stu-id="ffab5-233">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="ffab5-234">A response of `COMPLETED` indicates that the request has finished.</span><span class="sxs-lookup"><span data-stu-id="ffab5-234">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="ffab5-235">Once the previous request completes, use the following to start the service.</span><span class="sxs-lookup"><span data-stu-id="ffab5-235">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" \
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
    <span data-ttu-id="ffab5-236">The service is now using the new configuration.</span><span class="sxs-lookup"><span data-stu-id="ffab5-236">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="ffab5-237">Finally, use the following to turn off maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="ffab5-237">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin -sS -H "X-Requested-By: ambari" \
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

## <a name="next-steps"></a><span data-ttu-id="ffab5-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffab5-238">Next steps</span></span>

<span data-ttu-id="ffab5-239">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="ffab5-239">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

