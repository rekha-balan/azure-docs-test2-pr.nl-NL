---
title: Set up a standalone Azure Service Fabric cluster | Microsoft Docs
description: Create a development standalone cluster with three nodes running on the same computer. After completing this setup, you will be ready to create a multi-machine cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/11/2017
ms.author: ryanwi
ms.openlocfilehash: 14fa3453c57f094720a39c9e744ebedc1ead2b1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564490"
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="5b5c8-104">Create your first Service Fabric standalone cluster</span><span class="sxs-lookup"><span data-stu-id="5b5c8-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="5b5c8-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="5b5c8-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="5b5c8-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b5c8-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5b5c8-108">Before you begin</span></span>
<span data-ttu-id="5b5c8-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="5b5c8-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="5b5c8-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="5b5c8-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="5b5c8-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="5b5c8-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="5b5c8-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="5b5c8-114">You cannot install Service Fabric on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="5b5c8-115">Validate the environment</span><span class="sxs-lookup"><span data-stu-id="5b5c8-115">Validate the environment</span></span>
<span data-ttu-id="5b5c8-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="5b5c8-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="5b5c8-118">Run the script to verify if you can create the development cluster:</span><span class="sxs-lookup"><span data-stu-id="5b5c8-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="5b5c8-119">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="5b5c8-119">Create the cluster</span></span>
<span data-ttu-id="5b5c8-120">Several sample cluster configuration files are installed with the setup package.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="5b5c8-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="5b5c8-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="5b5c8-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="5b5c8-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="5b5c8-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="5b5c8-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="5b5c8-126">This cluster is unsecure.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-126">This cluster is unsecure.</span></span>  <span data-ttu-id="5b5c8-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="5b5c8-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="5b5c8-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="5b5c8-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="5b5c8-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="5b5c8-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="5b5c8-132">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="5b5c8-132">Connect to the cluster</span></span>
<span data-ttu-id="5b5c8-133">Your three-node development cluster is now running.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="5b5c8-134">The ServiceFabric PowerShell module is installed with the runtime.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="5b5c8-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="5b5c8-136">The [Connect-ServiceFabricCluster](/powershell/module/ServiceFabric/Connect-ServiceFabricCluster) cmdlet establishes a connection to the cluster.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-136">The [Connect-ServiceFabricCluster](/powershell/module/ServiceFabric/Connect-ServiceFabricCluster) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="5b5c8-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="5b5c8-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode) cmdlet to display a list of nodes in the cluster and status information for each node.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="5b5c8-139">**HealthState** should be *OK* for each node.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  ----------- ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.5.216.0   0                     Up 03:00:07   00:00:00              Ok
                     vm1      localhost       NodeType1 5.5.216.0   0                     Up 03:00:02   00:00:00              Ok
                     vm0      localhost       NodeType0 5.5.216.0   0                     Up 03:00:01   00:00:00              Ok
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="5b5c8-140">Visualize the cluster using Service Fabric explorer</span><span class="sxs-lookup"><span data-stu-id="5b5c8-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="5b5c8-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="5b5c8-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="5b5c8-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="5b5c8-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="5b5c8-144">The node view shows the physical layout of the cluster.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="5b5c8-145">For a given node, you can inspect which applications have code deployed on that node.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="5b5c8-147">Remove the cluster</span><span class="sxs-lookup"><span data-stu-id="5b5c8-147">Remove the cluster</span></span>
<span data-ttu-id="5b5c8-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="5b5c8-149">You can optionally specify a location for the log of the deletion.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="5b5c8-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="5b5c8-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b5c8-151">Next steps</span></span>
<span data-ttu-id="5b5c8-152">Now that you have set up a development standalone cluster, try the following articles:</span><span class="sxs-lookup"><span data-stu-id="5b5c8-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="5b5c8-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span><span class="sxs-lookup"><span data-stu-id="5b5c8-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="5b5c8-154">Deploy apps using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b5c8-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-standalone-cluster/sfx.png
