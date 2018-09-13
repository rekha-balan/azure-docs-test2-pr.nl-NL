---
title: Configure your standalone cluster | Microsoft Docs
description: This article describes how to configure your standalone or private Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 2/17/2017
ms.author: ryanwi
ms.openlocfilehash: 8192f9e36ebadd41d93ec3c2fa61b05e342d5bc1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555275"
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="d0cf3-103">Configuration settings for standalone Windows cluster</span><span class="sxs-lookup"><span data-stu-id="d0cf3-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="d0cf3-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="d0cf3-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="d0cf3-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="d0cf3-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="d0cf3-108">Out of these, at least one node must be marked as a primary node.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="d0cf3-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="d0cf3-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span> <span data-ttu-id="d0cf3-111">The number of primary nodes for these cluster will be based on the [reliability level](#reliability).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-111">The number of primary nodes for these cluster will be based on the [reliability level](#reliability).</span></span>

1. <span data-ttu-id="d0cf3-112">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-112">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="d0cf3-113">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-113">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="d0cf3-114">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-114">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="d0cf3-115">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-115">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="d0cf3-116">General cluster configurations</span><span class="sxs-lookup"><span data-stu-id="d0cf3-116">General cluster configurations</span></span>
<span data-ttu-id="d0cf3-117">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-117">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",

<span data-ttu-id="d0cf3-118">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-118">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="d0cf3-119">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-119">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="d0cf3-120">You should however leave the **apiVersion** to the default value.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-120">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="d0cf3-121">Nodes on the cluster</span><span class="sxs-lookup"><span data-stu-id="d0cf3-121">Nodes on the cluster</span></span>
<span data-ttu-id="d0cf3-122">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-122">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="d0cf3-123">A Service Fabric cluster must contain at least 3 nodes.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-123">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="d0cf3-124">You can add more nodes to this section as per your setup.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-124">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="d0cf3-125">The following table explains the configuration settings for each node.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-125">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="d0cf3-126">**Node configuration**</span><span class="sxs-lookup"><span data-stu-id="d0cf3-126">**Node configuration**</span></span> | <span data-ttu-id="d0cf3-127">**Description**</span><span class="sxs-lookup"><span data-stu-id="d0cf3-127">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="d0cf3-128">nodeName</span><span class="sxs-lookup"><span data-stu-id="d0cf3-128">nodeName</span></span> |<span data-ttu-id="d0cf3-129">You can give any friendly name to the node.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-129">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="d0cf3-130">iPAddress</span><span class="sxs-lookup"><span data-stu-id="d0cf3-130">iPAddress</span></span> |<span data-ttu-id="d0cf3-131">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-131">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="d0cf3-132">Note the IPV4 address and assign it to the **iPAddress** variable.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-132">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="d0cf3-133">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="d0cf3-133">nodeTypeRef</span></span> |<span data-ttu-id="d0cf3-134">Each node can be assigned a different node type.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-134">Each node can be assigned a different node type.</span></span> <span data-ttu-id="d0cf3-135">The [node types](#nodetypes) are defined in the section below.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-135">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="d0cf3-136">faultDomain</span><span class="sxs-lookup"><span data-stu-id="d0cf3-136">faultDomain</span></span> |<span data-ttu-id="d0cf3-137">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-137">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="d0cf3-138">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="d0cf3-138">upgradeDomain</span></span> |<span data-ttu-id="d0cf3-139">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-139">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="d0cf3-140">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-140">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="d0cf3-141">Cluster properties</span><span class="sxs-lookup"><span data-stu-id="d0cf3-141">Cluster properties</span></span>
<span data-ttu-id="d0cf3-142">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-142">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="d0cf3-143">Reliability</span><span class="sxs-lookup"><span data-stu-id="d0cf3-143">Reliability</span></span>
<span data-ttu-id="d0cf3-144">The **reliabilityLevel** section defines the number of copies of the system services that can run on the primary nodes of the cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-144">The **reliabilityLevel** section defines the number of copies of the system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="d0cf3-145">This increases the reliability of these services and hence the cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-145">This increases the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="d0cf3-146">You can set this variable to either *Bronze*, *Silver*, *Gold* or *Platinum* for 3, 5, 7 or 9 copies of these services respectively.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-146">You can set this variable to either *Bronze*, *Silver*, *Gold* or *Platinum* for 3, 5, 7 or 9 copies of these services respectively.</span></span> <span data-ttu-id="d0cf3-147">See an example below.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-147">See an example below.</span></span>

    "reliabilityLevel": "Bronze",

<span data-ttu-id="d0cf3-148">Note that since a primary node runs a single copy of the system services, you would need a minimum of 3 primary nodes for *Bronze*, 5 for *Silver*, 7 for *Gold* and 9 for *Platinum* reliability levels.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-148">Note that since a primary node runs a single copy of the system services, you would need a minimum of 3 primary nodes for *Bronze*, 5 for *Silver*, 7 for *Gold* and 9 for *Platinum* reliability levels.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="d0cf3-149">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d0cf3-149">Diagnostics</span></span>
<span data-ttu-id="d0cf3-150">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-150">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="d0cf3-151">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-151">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="d0cf3-152">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-152">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="d0cf3-153">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-153">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="d0cf3-154">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-154">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="d0cf3-155">You can also use *AzureStorage* for storing diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-155">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="d0cf3-156">See below for a sample snippet.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-156">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="d0cf3-157">Security</span><span class="sxs-lookup"><span data-stu-id="d0cf3-157">Security</span></span>
<span data-ttu-id="d0cf3-158">The **security** section is necessary for a secure standalone Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-158">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="d0cf3-159">The following snippet shows a part of this section.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-159">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="d0cf3-160">The **metadata** is a description of your secure cluster and can be set as per your setup.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-160">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="d0cf3-161">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-161">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="d0cf3-162">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-162">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="d0cf3-163">The rest of the **security** section will be based on the type of the security.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-163">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="d0cf3-164">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-164">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="d0cf3-165">Node Types</span><span class="sxs-lookup"><span data-stu-id="d0cf3-165">Node Types</span></span>
<span data-ttu-id="d0cf3-166">The **nodeTypes** section describes the type of the nodes that your cluster has.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-166">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="d0cf3-167">At least one node type must be specified for a cluster, as shown in the snippet below.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-167">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="d0cf3-168">The **name** is the friendly name for this particular node type.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-168">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="d0cf3-169">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-169">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="d0cf3-170">For each node type, define the connection endpoints that will be used.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-170">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="d0cf3-171">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-171">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="d0cf3-172">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-172">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="d0cf3-173">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel** values, and to know what are primary and the non-primary node types.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-173">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel** values, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="d0cf3-174">Endpoints used to configure the node types</span><span class="sxs-lookup"><span data-stu-id="d0cf3-174">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="d0cf3-175">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-175">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="d0cf3-176">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-176">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="d0cf3-177">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-177">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="d0cf3-178">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-178">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="d0cf3-179">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-179">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="d0cf3-180">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-180">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="d0cf3-181">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-181">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="d0cf3-182">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-182">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="d0cf3-183">You need to make sure that the difference between the start and the end ports is at least 255.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-183">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="d0cf3-184">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-184">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="d0cf3-185">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-185">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="d0cf3-186">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-186">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="d0cf3-187">The application port range should be large enough to cover the endpoint requirement of your applications.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-187">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="d0cf3-188">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-188">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="d0cf3-189">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-189">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="d0cf3-190">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-190">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="d0cf3-191">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-191">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="d0cf3-192">Log Settings</span><span class="sxs-lookup"><span data-stu-id="d0cf3-192">Log Settings</span></span>
<span data-ttu-id="d0cf3-193">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-193">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="d0cf3-194">You can customize these only during the initial cluster creation.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-194">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="d0cf3-195">See below for a sample snippet of this section.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-195">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="d0cf3-196">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-196">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="d0cf3-197">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-197">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="d0cf3-198">Stateful Reliable Service Settings</span><span class="sxs-lookup"><span data-stu-id="d0cf3-198">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="d0cf3-199">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-199">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="d0cf3-200">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-200">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="d0cf3-201">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span><span class="sxs-lookup"><span data-stu-id="d0cf3-201">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

## <a name="next-steps"></a><span data-ttu-id="d0cf3-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0cf3-202">Next steps</span></span>
<span data-ttu-id="d0cf3-203">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d0cf3-203">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

