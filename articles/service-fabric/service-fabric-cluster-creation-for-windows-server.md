---
title: Create a standalone Azure Service Fabric cluster | Microsoft Docs
description: Create an Azure Service Fabric cluster on any machine (physical or virtual) running Windows Server, whether it's on-premises or in any cloud.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: ''
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/24/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: c9d273b22df2001d81d9912e6443e60b5c53ca60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552373"
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="6e90d-103">Create a standalone cluster running on Windows Server</span><span class="sxs-lookup"><span data-stu-id="6e90d-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="6e90d-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6e90d-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="6e90d-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span><span class="sxs-lookup"><span data-stu-id="6e90d-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="6e90d-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span><span class="sxs-lookup"><span data-stu-id="6e90d-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="6e90d-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span><span class="sxs-lookup"><span data-stu-id="6e90d-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6e90d-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span><span class="sxs-lookup"><span data-stu-id="6e90d-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="6e90d-109">This package may contain new Service Fabric features that are in "Preview".</span><span class="sxs-lookup"><span data-stu-id="6e90d-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="6e90d-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="6e90d-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="6e90d-111">section for the list of the preview features.</span><span class="sxs-lookup"><span data-stu-id="6e90d-111">section for the list of the preview features.</span></span> <span data-ttu-id="6e90d-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span><span class="sxs-lookup"><span data-stu-id="6e90d-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-standalone-package"></a><span data-ttu-id="6e90d-113">Get support for the Service Fabric standalone package</span><span class="sxs-lookup"><span data-stu-id="6e90d-113">Get support for the Service Fabric standalone package</span></span>
* <span data-ttu-id="6e90d-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="6e90d-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="6e90d-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="6e90d-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="6e90d-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="6e90d-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="6e90d-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="6e90d-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="6e90d-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="6e90d-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="6e90d-119">To collect logs for support purpose, run [Service Fabric Standalone Log collector](https://go.microsoft.com/fwlink/?linkid=842487).</span><span class="sxs-lookup"><span data-stu-id="6e90d-119">To collect logs for support purpose, run [Service Fabric Standalone Log collector](https://go.microsoft.com/fwlink/?linkid=842487).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-standalone-package"></a><span data-ttu-id="6e90d-120">Download the Service Fabric standalone package</span><span class="sxs-lookup"><span data-stu-id="6e90d-120">Download the Service Fabric standalone package</span></span>
<span data-ttu-id="6e90d-121">To create the cluster, use the Service Fabric Standalone Package for Windows Server (2012 R2 and newer) found here:</span><span class="sxs-lookup"><span data-stu-id="6e90d-121">To create the cluster, use the Service Fabric Standalone Package for Windows Server (2012 R2 and newer) found here:</span></span> <br>
[<span data-ttu-id="6e90d-122">Download Link - Service Fabric Standalone Package - Windows Server</span><span class="sxs-lookup"><span data-stu-id="6e90d-122">Download Link - Service Fabric Standalone Package - Windows Server</span></span>](http://go.microsoft.com/fwlink/?LinkId=730690)

<span data-ttu-id="6e90d-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="6e90d-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="6e90d-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span><span class="sxs-lookup"><span data-stu-id="6e90d-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="6e90d-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span><span class="sxs-lookup"><span data-stu-id="6e90d-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br>
[<span data-ttu-id="6e90d-126">Download Link - Service Fabric Runtime - Windows Server</span><span class="sxs-lookup"><span data-stu-id="6e90d-126">Download Link - Service Fabric Runtime - Windows Server</span></span>](https://go.microsoft.com/fwlink/?linkid=839354)

<span data-ttu-id="6e90d-127">Find Standalone Cluster Configuration samples at:</span><span class="sxs-lookup"><span data-stu-id="6e90d-127">Find Standalone Cluster Configuration samples at:</span></span> <br>
[<span data-ttu-id="6e90d-128">Standalone Cluster Configuration Samples</span><span class="sxs-lookup"><span data-stu-id="6e90d-128">Standalone Cluster Configuration Samples</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="6e90d-129">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-129">Create the cluster</span></span>
<span data-ttu-id="6e90d-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="6e90d-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="6e90d-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span><span class="sxs-lookup"><span data-stu-id="6e90d-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="6e90d-132">Step 1A: Create an unsecured local development cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="6e90d-133">See Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span><span class="sxs-lookup"><span data-stu-id="6e90d-133">See Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="6e90d-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section below "[Remove a cluster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="6e90d-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section below "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="6e90d-135">Step 1B: Create a multi-machine cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="6e90d-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span><span class="sxs-lookup"><span data-stu-id="6e90d-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br>
[<span data-ttu-id="6e90d-137">Plan and prepare your cluster deployment</span><span class="sxs-lookup"><span data-stu-id="6e90d-137">Plan and prepare your cluster deployment</span></span>](service-fabric-cluster-standalone-deployment-preparation.md)

1. <span data-ttu-id="6e90d-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span><span class="sxs-lookup"><span data-stu-id="6e90d-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
```

<span data-ttu-id="6e90d-139">You should see output like below.</span><span class="sxs-lookup"><span data-stu-id="6e90d-139">You should see output like below.</span></span> <span data-ttu-id="6e90d-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span><span class="sxs-lookup"><span data-stu-id="6e90d-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

```
Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

2. <span data-ttu-id="6e90d-141">Create the cluster: Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span><span class="sxs-lookup"><span data-stu-id="6e90d-141">Create the cluster: Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
```

> [!NOTE]
> <span data-ttu-id="6e90d-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="6e90d-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="6e90d-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span><span class="sxs-lookup"><span data-stu-id="6e90d-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="6e90d-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="6e90d-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="6e90d-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span><span class="sxs-lookup"><span data-stu-id="6e90d-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="6e90d-146">Step 2: Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-146">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="6e90d-147">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6e90d-147">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="6e90d-148">To connect to an unsecure cluster, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="6e90d-148">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>

Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="6e90d-149">Step 3: Bring up Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="6e90d-149">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="6e90d-150">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="6e90d-150">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="6e90d-151">Add and remove nodes</span><span class="sxs-lookup"><span data-stu-id="6e90d-151">Add and remove nodes</span></span>
<span data-ttu-id="6e90d-152">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span><span class="sxs-lookup"><span data-stu-id="6e90d-152">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="6e90d-153">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="6e90d-153">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="6e90d-154">Remove a cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-154">Remove a cluster</span></span>
<span data-ttu-id="6e90d-155">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="6e90d-155">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="6e90d-156">You can optionally specify a location for the log of the deletion.</span><span class="sxs-lookup"><span data-stu-id="6e90d-156">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="6e90d-157">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span><span class="sxs-lookup"><span data-stu-id="6e90d-157">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="6e90d-158">The machine that this script is run on does not have to be part of the cluster.</span><span class="sxs-lookup"><span data-stu-id="6e90d-158">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="6e90d-159">Telemetry data collected and how to opt out of it</span><span class="sxs-lookup"><span data-stu-id="6e90d-159">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="6e90d-160">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span><span class="sxs-lookup"><span data-stu-id="6e90d-160">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="6e90d-161">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="6e90d-161">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="6e90d-162">If it is not reachable, the setup fails unless you opt out of telemetry.</span><span class="sxs-lookup"><span data-stu-id="6e90d-162">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="6e90d-163">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span><span class="sxs-lookup"><span data-stu-id="6e90d-163">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="6e90d-164">It is a best-effort upload and has no impact on the cluster functionality.</span><span class="sxs-lookup"><span data-stu-id="6e90d-164">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="6e90d-165">The telemetry is only sent from the node that runs the failover manager primary.</span><span class="sxs-lookup"><span data-stu-id="6e90d-165">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="6e90d-166">No other nodes send out telemetry.</span><span class="sxs-lookup"><span data-stu-id="6e90d-166">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="6e90d-167">The telemetry consists of the following:</span><span class="sxs-lookup"><span data-stu-id="6e90d-167">The telemetry consists of the following:</span></span>

* <span data-ttu-id="6e90d-168">Number of services</span><span class="sxs-lookup"><span data-stu-id="6e90d-168">Number of services</span></span>
* <span data-ttu-id="6e90d-169">Number of ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="6e90d-169">Number of ServiceTypes</span></span>
* <span data-ttu-id="6e90d-170">Number of Applications</span><span class="sxs-lookup"><span data-stu-id="6e90d-170">Number of Applications</span></span>
* <span data-ttu-id="6e90d-171">Number of ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="6e90d-171">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="6e90d-172">Number of FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="6e90d-172">Number of FailoverUnits</span></span>
* <span data-ttu-id="6e90d-173">Number of InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="6e90d-173">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="6e90d-174">Number of UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="6e90d-174">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="6e90d-175">Number of Replicas</span><span class="sxs-lookup"><span data-stu-id="6e90d-175">Number of Replicas</span></span>
* <span data-ttu-id="6e90d-176">Number of InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="6e90d-176">Number of InBuildReplicas</span></span>
* <span data-ttu-id="6e90d-177">Number of StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="6e90d-177">Number of StandByReplicas</span></span>
* <span data-ttu-id="6e90d-178">Number of OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="6e90d-178">Number of OfflineReplicas</span></span>
* <span data-ttu-id="6e90d-179">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="6e90d-179">CommonQueueLength</span></span>
* <span data-ttu-id="6e90d-180">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="6e90d-180">QueryQueueLength</span></span>
* <span data-ttu-id="6e90d-181">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="6e90d-181">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="6e90d-182">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="6e90d-182">CommitQueueLength</span></span>
* <span data-ttu-id="6e90d-183">Number of Nodes</span><span class="sxs-lookup"><span data-stu-id="6e90d-183">Number of Nodes</span></span>
* <span data-ttu-id="6e90d-184">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="6e90d-184">IsContextComplete: True/False</span></span>
* <span data-ttu-id="6e90d-185">ClusterId: This is a GUID randomly generated for each cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-185">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="6e90d-186">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="6e90d-186">ServiceFabricVersion</span></span>
* <span data-ttu-id="6e90d-187">IP address of the virtual machine or machine from which the telemetry is uploaded</span><span class="sxs-lookup"><span data-stu-id="6e90d-187">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="6e90d-188">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="6e90d-188">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="6e90d-189">Preview features included in this package</span><span class="sxs-lookup"><span data-stu-id="6e90d-189">Preview features included in this package</span></span>
<span data-ttu-id="6e90d-190">None.</span><span class="sxs-lookup"><span data-stu-id="6e90d-190">None.</span></span>


> [!NOTE]
> <span data-ttu-id="6e90d-191">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span><span class="sxs-lookup"><span data-stu-id="6e90d-191">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="6e90d-192">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span><span class="sxs-lookup"><span data-stu-id="6e90d-192">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6e90d-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e90d-193">Next steps</span></span>
* [<span data-ttu-id="6e90d-194">Deploy and remove applications using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e90d-194">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="6e90d-195">Configuration settings for standalone Windows cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-195">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="6e90d-196">Add or remove nodes to a standalone Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="6e90d-196">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="6e90d-197">Upgrade a standalone Service Fabric cluster version</span><span class="sxs-lookup"><span data-stu-id="6e90d-197">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="6e90d-198">Create a standalone Service Fabric cluster with Azure VMs running Windows</span><span class="sxs-lookup"><span data-stu-id="6e90d-198">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="6e90d-199">Secure a standalone cluster on Windows using Windows security</span><span class="sxs-lookup"><span data-stu-id="6e90d-199">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="6e90d-200">Secure a standalone cluster on Windows using X509 certificates</span><span class="sxs-lookup"><span data-stu-id="6e90d-200">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png

