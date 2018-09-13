---
title: Configure your Azure Service Fabric standalone cluster | Microsoft Docs
description: Learn how to configure your standalone or on-premises Azure Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: ''
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/06/2017
ms.author: dekapur
ms.openlocfilehash: 37859a117c88238089a681e3814c2a52f62bfce4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784282"
---
# <a name="configuration-settings-for-a-standalone-windows-cluster"></a><span data-ttu-id="181b2-103">Configuration settings for a standalone Windows cluster</span><span class="sxs-lookup"><span data-stu-id="181b2-103">Configuration settings for a standalone Windows cluster</span></span>
<span data-ttu-id="181b2-104">This article describes how to configure a standalone Azure Service Fabric cluster by using the ClusterConfig.json file.</span><span class="sxs-lookup"><span data-stu-id="181b2-104">This article describes how to configure a standalone Azure Service Fabric cluster by using the ClusterConfig.json file.</span></span> <span data-ttu-id="181b2-105">You will use this file to specify information about the cluster's nodes, security configurations, as well as the network topology in terms of fault and upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="181b2-105">You will use this file to specify information about the cluster's nodes, security configurations, as well as the network topology in terms of fault and upgrade domains.</span></span>

<span data-ttu-id="181b2-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), ClusterConfig.json samples are also included.</span><span class="sxs-lookup"><span data-stu-id="181b2-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), ClusterConfig.json samples are also included.</span></span> <span data-ttu-id="181b2-107">The samples that have "DevCluster" in their names create a cluster with all three nodes on the same machine, using logical nodes.</span><span class="sxs-lookup"><span data-stu-id="181b2-107">The samples that have "DevCluster" in their names create a cluster with all three nodes on the same machine, using logical nodes.</span></span> <span data-ttu-id="181b2-108">Out of these nodes, at least one must be marked as a primary node.</span><span class="sxs-lookup"><span data-stu-id="181b2-108">Out of these nodes, at least one must be marked as a primary node.</span></span> <span data-ttu-id="181b2-109">This type of cluster is useful for development or test environments.</span><span class="sxs-lookup"><span data-stu-id="181b2-109">This type of cluster is useful for development or test environments.</span></span> <span data-ttu-id="181b2-110">It is not supported as a production cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-110">It is not supported as a production cluster.</span></span> <span data-ttu-id="181b2-111">The samples that have "MultiMachine" in their names help create production grade clusters, with each node on a separate machine.</span><span class="sxs-lookup"><span data-stu-id="181b2-111">The samples that have "MultiMachine" in their names help create production grade clusters, with each node on a separate machine.</span></span> <span data-ttu-id="181b2-112">The number of primary nodes for these clusters is based on the cluster's [reliability level](#reliability).</span><span class="sxs-lookup"><span data-stu-id="181b2-112">The number of primary nodes for these clusters is based on the cluster's [reliability level](#reliability).</span></span> <span data-ttu-id="181b2-113">In release 5.7, API Version 05-2017, we removed the reliability-level property.</span><span class="sxs-lookup"><span data-stu-id="181b2-113">In release 5.7, API Version 05-2017, we removed the reliability-level property.</span></span> <span data-ttu-id="181b2-114">Instead, our code calculates the most optimized reliability level for your cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-114">Instead, our code calculates the most optimized reliability level for your cluster.</span></span> <span data-ttu-id="181b2-115">Do not try to set a value for this property in versions 5.7 onwards.</span><span class="sxs-lookup"><span data-stu-id="181b2-115">Do not try to set a value for this property in versions 5.7 onwards.</span></span>


* <span data-ttu-id="181b2-116">ClusterConfig.Unsecure.DevCluster.json and ClusterConfig.Unsecure.MultiMachine.json show how to create an unsecured test or production cluster, respectively.</span><span class="sxs-lookup"><span data-stu-id="181b2-116">ClusterConfig.Unsecure.DevCluster.json and ClusterConfig.Unsecure.MultiMachine.json show how to create an unsecured test or production cluster, respectively.</span></span>

* <span data-ttu-id="181b2-117">ClusterConfig.Windows.DevCluster.json and ClusterConfig.Windows.MultiMachine.json show how to create test or production clusters that are secured by using [Windows security](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="181b2-117">ClusterConfig.Windows.DevCluster.json and ClusterConfig.Windows.MultiMachine.json show how to create test or production clusters that are secured by using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>

* <span data-ttu-id="181b2-118">ClusterConfig.X509.DevCluster.json and ClusterConfig.X509.MultiMachine.json show how to create test or production clusters that are secured by using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="181b2-118">ClusterConfig.X509.DevCluster.json and ClusterConfig.X509.MultiMachine.json show how to create test or production clusters that are secured by using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span>

<span data-ttu-id="181b2-119">Now let's examine the various sections of a ClusterConfig.json file.</span><span class="sxs-lookup"><span data-stu-id="181b2-119">Now let's examine the various sections of a ClusterConfig.json file.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="181b2-120">General cluster configurations</span><span class="sxs-lookup"><span data-stu-id="181b2-120">General cluster configurations</span></span>
<span data-ttu-id="181b2-121">General cluster configurations cover the broad cluster-specific configurations, as shown in the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="181b2-121">General cluster configurations cover the broad cluster-specific configurations, as shown in the following JSON snippet:</span></span>

```json
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",
```

<span data-ttu-id="181b2-122">You can give any friendly name to your Service Fabric cluster by assigning it to the name variable.</span><span class="sxs-lookup"><span data-stu-id="181b2-122">You can give any friendly name to your Service Fabric cluster by assigning it to the name variable.</span></span> <span data-ttu-id="181b2-123">The clusterConfigurationVersion is the version number of your cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-123">The clusterConfigurationVersion is the version number of your cluster.</span></span> <span data-ttu-id="181b2-124">Increase it every time you upgrade your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-124">Increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="181b2-125">Leave apiVersion set to the default value.</span><span class="sxs-lookup"><span data-stu-id="181b2-125">Leave apiVersion set to the default value.</span></span>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="181b2-126">Nodes on the cluster</span><span class="sxs-lookup"><span data-stu-id="181b2-126">Nodes on the cluster</span></span>
<span data-ttu-id="181b2-127">You can configure the nodes on your Service Fabric cluster by using the nodes section, as the following snippet shows:</span><span class="sxs-lookup"><span data-stu-id="181b2-127">You can configure the nodes on your Service Fabric cluster by using the nodes section, as the following snippet shows:</span></span>

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

<span data-ttu-id="181b2-128">A Service Fabric cluster must contain at least three nodes.</span><span class="sxs-lookup"><span data-stu-id="181b2-128">A Service Fabric cluster must contain at least three nodes.</span></span> <span data-ttu-id="181b2-129">You can add more nodes to this section according to your setup.</span><span class="sxs-lookup"><span data-stu-id="181b2-129">You can add more nodes to this section according to your setup.</span></span> <span data-ttu-id="181b2-130">The following table explains configuration settings for each node:</span><span class="sxs-lookup"><span data-stu-id="181b2-130">The following table explains configuration settings for each node:</span></span>

| <span data-ttu-id="181b2-131">**Node configuration**</span><span class="sxs-lookup"><span data-stu-id="181b2-131">**Node configuration**</span></span> | <span data-ttu-id="181b2-132">**Description**</span><span class="sxs-lookup"><span data-stu-id="181b2-132">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="181b2-133">nodeName</span><span class="sxs-lookup"><span data-stu-id="181b2-133">nodeName</span></span> |<span data-ttu-id="181b2-134">You can give any friendly name to the node.</span><span class="sxs-lookup"><span data-stu-id="181b2-134">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="181b2-135">iPAddress</span><span class="sxs-lookup"><span data-stu-id="181b2-135">iPAddress</span></span> |<span data-ttu-id="181b2-136">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="181b2-136">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="181b2-137">Note the IPV4 address, and assign it to the iPAddress variable.</span><span class="sxs-lookup"><span data-stu-id="181b2-137">Note the IPV4 address, and assign it to the iPAddress variable.</span></span> |
| <span data-ttu-id="181b2-138">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="181b2-138">nodeTypeRef</span></span> |<span data-ttu-id="181b2-139">Each node can be assigned a different node type.</span><span class="sxs-lookup"><span data-stu-id="181b2-139">Each node can be assigned a different node type.</span></span> <span data-ttu-id="181b2-140">The [node types](#node-types) are defined in the following section.</span><span class="sxs-lookup"><span data-stu-id="181b2-140">The [node types](#node-types) are defined in the following section.</span></span> |
| <span data-ttu-id="181b2-141">faultDomain</span><span class="sxs-lookup"><span data-stu-id="181b2-141">faultDomain</span></span> |<span data-ttu-id="181b2-142">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span><span class="sxs-lookup"><span data-stu-id="181b2-142">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="181b2-143">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="181b2-143">upgradeDomain</span></span> |<span data-ttu-id="181b2-144">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span><span class="sxs-lookup"><span data-stu-id="181b2-144">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="181b2-145">You can choose which nodes to assign to which upgrade domains, because they aren't limited by any physical requirements.</span><span class="sxs-lookup"><span data-stu-id="181b2-145">You can choose which nodes to assign to which upgrade domains, because they aren't limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="181b2-146">Cluster properties</span><span class="sxs-lookup"><span data-stu-id="181b2-146">Cluster properties</span></span>
<span data-ttu-id="181b2-147">The properties section in the ClusterConfig.json is used to configure the cluster as shown:</span><span class="sxs-lookup"><span data-stu-id="181b2-147">The properties section in the ClusterConfig.json is used to configure the cluster as shown:</span></span>

### <a name="reliability"></a><span data-ttu-id="181b2-148">Reliability</span><span class="sxs-lookup"><span data-stu-id="181b2-148">Reliability</span></span>
<span data-ttu-id="181b2-149">The concept of reliabilityLevel defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-149">The concept of reliabilityLevel defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="181b2-150">It determines the reliability of these services and hence the cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-150">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="181b2-151">The value is calculated by the system at cluster creation and upgrade time.</span><span class="sxs-lookup"><span data-stu-id="181b2-151">The value is calculated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="181b2-152">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="181b2-152">Diagnostics</span></span>
<span data-ttu-id="181b2-153">In the diagnosticsStore section, you can configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="181b2-153">In the diagnosticsStore section, you can configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet:</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="181b2-154">The metadata is a description of your cluster diagnostics and can be set according to your setup.</span><span class="sxs-lookup"><span data-stu-id="181b2-154">The metadata is a description of your cluster diagnostics and can be set according to your setup.</span></span> <span data-ttu-id="181b2-155">These variables help in collecting ETW trace logs and crash dumps as well as performance counters.</span><span class="sxs-lookup"><span data-stu-id="181b2-155">These variables help in collecting ETW trace logs and crash dumps as well as performance counters.</span></span> <span data-ttu-id="181b2-156">For more information on ETW trace logs, see [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW tracing](https://msdn.microsoft.com/library/ms751538.aspx).</span><span class="sxs-lookup"><span data-stu-id="181b2-156">For more information on ETW trace logs, see [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW tracing](https://msdn.microsoft.com/library/ms751538.aspx).</span></span> <span data-ttu-id="181b2-157">All logs, including [crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx), can be directed to the connectionString folder on your machine.</span><span class="sxs-lookup"><span data-stu-id="181b2-157">All logs, including [crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx), can be directed to the connectionString folder on your machine.</span></span> <span data-ttu-id="181b2-158">You also can use AzureStorage to store diagnostics.</span><span class="sxs-lookup"><span data-stu-id="181b2-158">You also can use AzureStorage to store diagnostics.</span></span> <span data-ttu-id="181b2-159">See the following sample snippet:</span><span class="sxs-lookup"><span data-stu-id="181b2-159">See the following sample snippet:</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="181b2-160">Security</span><span class="sxs-lookup"><span data-stu-id="181b2-160">Security</span></span>
<span data-ttu-id="181b2-161">The security section is necessary for a secure standalone Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-161">The security section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="181b2-162">The following snippet shows a part of this section:</span><span class="sxs-lookup"><span data-stu-id="181b2-162">The following snippet shows a part of this section:</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="181b2-163">The metadata is a description of your secure cluster and can be set according to your setup.</span><span class="sxs-lookup"><span data-stu-id="181b2-163">The metadata is a description of your secure cluster and can be set according to your setup.</span></span> <span data-ttu-id="181b2-164">The ClusterCredentialType and ServerCredentialType determine the type of security that the cluster and the nodes implement.</span><span class="sxs-lookup"><span data-stu-id="181b2-164">The ClusterCredentialType and ServerCredentialType determine the type of security that the cluster and the nodes implement.</span></span> <span data-ttu-id="181b2-165">They can be set to either *X509* for a certificate-based security or *Windows* for Azure Active Directory-based security.</span><span class="sxs-lookup"><span data-stu-id="181b2-165">They can be set to either *X509* for a certificate-based security or *Windows* for Azure Active Directory-based security.</span></span> <span data-ttu-id="181b2-166">The rest of the security section is based on the type of security.</span><span class="sxs-lookup"><span data-stu-id="181b2-166">The rest of the security section is based on the type of security.</span></span> <span data-ttu-id="181b2-167">For information on how to fill out the rest of the security section, see [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="181b2-167">For information on how to fill out the rest of the security section, see [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md).</span></span>

### <a name="node-types"></a><span data-ttu-id="181b2-168">Node types</span><span class="sxs-lookup"><span data-stu-id="181b2-168">Node types</span></span>
<span data-ttu-id="181b2-169">The nodeTypes section describes the type of nodes that your cluster has.</span><span class="sxs-lookup"><span data-stu-id="181b2-169">The nodeTypes section describes the type of nodes that your cluster has.</span></span> <span data-ttu-id="181b2-170">At least one node type must be specified for a cluster, as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="181b2-170">At least one node type must be specified for a cluster, as shown in the following snippet:</span></span> 

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

<span data-ttu-id="181b2-171">The name is the friendly name for this particular node type.</span><span class="sxs-lookup"><span data-stu-id="181b2-171">The name is the friendly name for this particular node type.</span></span> <span data-ttu-id="181b2-172">To create a node of this node type, assign its friendly name to the nodeTypeRef variable for that node, as [previously mentioned](#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="181b2-172">To create a node of this node type, assign its friendly name to the nodeTypeRef variable for that node, as [previously mentioned](#nodes-on-the-cluster).</span></span> <span data-ttu-id="181b2-173">For each node type, define the connection endpoints that are used.</span><span class="sxs-lookup"><span data-stu-id="181b2-173">For each node type, define the connection endpoints that are used.</span></span> <span data-ttu-id="181b2-174">You can choose any port number for these connection endpoints, as long as they don't conflict with any other endpoints in this cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-174">You can choose any port number for these connection endpoints, as long as they don't conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="181b2-175">In a multinode cluster, there are one or more primary nodes (that is, isPrimary is set to *true*), depending on the [reliabilityLevel](#reliability).</span><span class="sxs-lookup"><span data-stu-id="181b2-175">In a multinode cluster, there are one or more primary nodes (that is, isPrimary is set to *true*), depending on the [reliabilityLevel](#reliability).</span></span> <span data-ttu-id="181b2-176">To learn more about primary and nonprimary node types, see [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on nodeTypes and reliabilityLevel.</span><span class="sxs-lookup"><span data-stu-id="181b2-176">To learn more about primary and nonprimary node types, see [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on nodeTypes and reliabilityLevel.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="181b2-177">Endpoints used to configure the node types</span><span class="sxs-lookup"><span data-stu-id="181b2-177">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="181b2-178">clientConnectionEndpointPort is the port used by the client to connect to the cluster when client APIs are used.</span><span class="sxs-lookup"><span data-stu-id="181b2-178">clientConnectionEndpointPort is the port used by the client to connect to the cluster when client APIs are used.</span></span> 
* <span data-ttu-id="181b2-179">clusterConnectionEndpointPort is the port where the nodes communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="181b2-179">clusterConnectionEndpointPort is the port where the nodes communicate with each other.</span></span>
* <span data-ttu-id="181b2-180">leaseDriverEndpointPort is the port used by the cluster lease driver to find out if the nodes are still active.</span><span class="sxs-lookup"><span data-stu-id="181b2-180">leaseDriverEndpointPort is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="181b2-181">serviceConnectionEndpointPort is the port used by the applications and services deployed on a node to communicate with the Service Fabric client on that particular node.</span><span class="sxs-lookup"><span data-stu-id="181b2-181">serviceConnectionEndpointPort is the port used by the applications and services deployed on a node to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="181b2-182">httpGatewayEndpointPort is the port used by Service Fabric Explorer to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-182">httpGatewayEndpointPort is the port used by Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="181b2-183">ephemeralPorts override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="181b2-183">ephemeralPorts override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="181b2-184">Service Fabric uses a part of these ports as application ports, and the remaining are available for the OS.</span><span class="sxs-lookup"><span data-stu-id="181b2-184">Service Fabric uses a part of these ports as application ports, and the remaining are available for the OS.</span></span> <span data-ttu-id="181b2-185">It also maps this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span><span class="sxs-lookup"><span data-stu-id="181b2-185">It also maps this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="181b2-186">Make sure that the difference between the start and the end ports is at least 255.</span><span class="sxs-lookup"><span data-stu-id="181b2-186">Make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="181b2-187">You might run into conflicts if this difference is too low, because this range is shared with the OS.</span><span class="sxs-lookup"><span data-stu-id="181b2-187">You might run into conflicts if this difference is too low, because this range is shared with the OS.</span></span> <span data-ttu-id="181b2-188">To see the configured dynamic port range, run `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="181b2-188">To see the configured dynamic port range, run `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="181b2-189">applicationPorts are the ports that are used by the Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="181b2-189">applicationPorts are the ports that are used by the Service Fabric applications.</span></span> <span data-ttu-id="181b2-190">The application port range should be large enough to cover the endpoint requirement of your applications.</span><span class="sxs-lookup"><span data-stu-id="181b2-190">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="181b2-191">This range should be exclusive from the dynamic port range on the machine, that is, the ephemeralPorts range as set in the configuration.</span><span class="sxs-lookup"><span data-stu-id="181b2-191">This range should be exclusive from the dynamic port range on the machine, that is, the ephemeralPorts range as set in the configuration.</span></span> <span data-ttu-id="181b2-192">Service Fabric uses these ports whenever new ports are required and takes care of opening the firewall for these ports.</span><span class="sxs-lookup"><span data-stu-id="181b2-192">Service Fabric uses these ports whenever new ports are required and takes care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="181b2-193">reverseProxyEndpointPort is an optional reverse proxy endpoint.</span><span class="sxs-lookup"><span data-stu-id="181b2-193">reverseProxyEndpointPort is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="181b2-194">For more information, see [Service Fabric reverse proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="181b2-194">For more information, see [Service Fabric reverse proxy](service-fabric-reverseproxy.md).</span></span> 

### <a name="log-settings"></a><span data-ttu-id="181b2-195">Log settings</span><span class="sxs-lookup"><span data-stu-id="181b2-195">Log settings</span></span>
<span data-ttu-id="181b2-196">In the fabricSettings section, you can set the root directories for the Service Fabric data and logs.</span><span class="sxs-lookup"><span data-stu-id="181b2-196">In the fabricSettings section, you can set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="181b2-197">You can customize these directories only during the initial cluster creation.</span><span class="sxs-lookup"><span data-stu-id="181b2-197">You can customize these directories only during the initial cluster creation.</span></span> <span data-ttu-id="181b2-198">See the following sample snippet of this section:</span><span class="sxs-lookup"><span data-stu-id="181b2-198">See the following sample snippet of this section:</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="181b2-199">We recommend that you use a non-OS drive as the FabricDataRoot and FabricLogRoot.</span><span class="sxs-lookup"><span data-stu-id="181b2-199">We recommend that you use a non-OS drive as the FabricDataRoot and FabricLogRoot.</span></span> <span data-ttu-id="181b2-200">It provides more reliability in avoiding situations when the OS stops responding.</span><span class="sxs-lookup"><span data-stu-id="181b2-200">It provides more reliability in avoiding situations when the OS stops responding.</span></span> <span data-ttu-id="181b2-201">If you customize only the data root, the log root is placed one level below the data root.</span><span class="sxs-lookup"><span data-stu-id="181b2-201">If you customize only the data root, the log root is placed one level below the data root.</span></span>

### <a name="stateful-reliable-services-settings"></a><span data-ttu-id="181b2-202">Stateful Reliable Services settings</span><span class="sxs-lookup"><span data-stu-id="181b2-202">Stateful Reliable Services settings</span></span>
<span data-ttu-id="181b2-203">In the KtlLogger section, you can set the global configuration settings for Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="181b2-203">In the KtlLogger section, you can set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="181b2-204">For more information on these settings, see [Configure Stateful Reliable Services](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="181b2-204">For more information on these settings, see [Configure Stateful Reliable Services](service-fabric-reliable-services-configuration.md).</span></span> <span data-ttu-id="181b2-205">The following example shows how to change the shared transaction log that gets created to back any reliable collections for stateful services:</span><span class="sxs-lookup"><span data-stu-id="181b2-205">The following example shows how to change the shared transaction log that gets created to back any reliable collections for stateful services:</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="181b2-206">Add-on features</span><span class="sxs-lookup"><span data-stu-id="181b2-206">Add-on features</span></span>
<span data-ttu-id="181b2-207">To configure add-on features, configure the apiVersion as 04-2017 or higher, and configure the addonFeatures as shown here:</span><span class="sxs-lookup"><span data-stu-id="181b2-207">To configure add-on features, configure the apiVersion as 04-2017 or higher, and configure the addonFeatures as shown here:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="181b2-208">Container support</span><span class="sxs-lookup"><span data-stu-id="181b2-208">Container support</span></span>
<span data-ttu-id="181b2-209">To enable container support for both Windows Server containers and Hyper-V containers for standalone clusters, the DnsService add-on feature must be enabled.</span><span class="sxs-lookup"><span data-stu-id="181b2-209">To enable container support for both Windows Server containers and Hyper-V containers for standalone clusters, the DnsService add-on feature must be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="181b2-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="181b2-210">Next steps</span></span>
<span data-ttu-id="181b2-211">After you have a complete ClusterConfig.json file configured according to your standalone cluster setup, you can deploy your cluster.</span><span class="sxs-lookup"><span data-stu-id="181b2-211">After you have a complete ClusterConfig.json file configured according to your standalone cluster setup, you can deploy your cluster.</span></span> <span data-ttu-id="181b2-212">Follow the steps in [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="181b2-212">Follow the steps in [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="181b2-213">Then proceed to [Visualize your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) and follow the steps.</span><span class="sxs-lookup"><span data-stu-id="181b2-213">Then proceed to [Visualize your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) and follow the steps.</span></span>

