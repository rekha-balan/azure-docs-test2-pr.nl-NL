---
title: Create a standalone Azure Service Fabric cluster | Microsoft Docs
description: Create an Azure Service Fabric cluster on any machine (physical or virtual) running Windows Server, whether it's on-premises or in any cloud.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: ''
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: dekapur
ms.openlocfilehash: 3ce47d631e8a2ec7daf96ef95200001e5d4f8327
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773636"
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="54d10-103">Create a standalone cluster running on Windows Server</span><span class="sxs-lookup"><span data-stu-id="54d10-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="54d10-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="54d10-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="54d10-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span><span class="sxs-lookup"><span data-stu-id="54d10-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="54d10-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span><span class="sxs-lookup"><span data-stu-id="54d10-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="54d10-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span><span class="sxs-lookup"><span data-stu-id="54d10-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="54d10-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span><span class="sxs-lookup"><span data-stu-id="54d10-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="54d10-109">This package may contain new Service Fabric features that are in "Preview".</span><span class="sxs-lookup"><span data-stu-id="54d10-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="54d10-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="54d10-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="54d10-111">section for the list of the preview features.</span><span class="sxs-lookup"><span data-stu-id="54d10-111">section for the list of the preview features.</span></span> <span data-ttu-id="54d10-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span><span class="sxs-lookup"><span data-stu-id="54d10-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="54d10-113">Get support for the Service Fabric for Windows Server package</span><span class="sxs-lookup"><span data-stu-id="54d10-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="54d10-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="54d10-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="54d10-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="54d10-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="54d10-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="54d10-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="54d10-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="54d10-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="54d10-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="54d10-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="54d10-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="54d10-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="54d10-120">Download the Service Fabric for Windows Server package</span><span class="sxs-lookup"><span data-stu-id="54d10-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="54d10-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span><span class="sxs-lookup"><span data-stu-id="54d10-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br>
[<span data-ttu-id="54d10-122">Download Link - Service Fabric Standalone Package - Windows Server</span><span class="sxs-lookup"><span data-stu-id="54d10-122">Download Link - Service Fabric Standalone Package - Windows Server</span></span>](http://go.microsoft.com/fwlink/?LinkId=730690)

<span data-ttu-id="54d10-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="54d10-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="54d10-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span><span class="sxs-lookup"><span data-stu-id="54d10-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="54d10-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span><span class="sxs-lookup"><span data-stu-id="54d10-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br>
[<span data-ttu-id="54d10-126">Download Link - Service Fabric Runtime - Windows Server</span><span class="sxs-lookup"><span data-stu-id="54d10-126">Download Link - Service Fabric Runtime - Windows Server</span></span>](https://go.microsoft.com/fwlink/?linkid=839354)

<span data-ttu-id="54d10-127">Find Standalone Cluster Configuration samples at:</span><span class="sxs-lookup"><span data-stu-id="54d10-127">Find Standalone Cluster Configuration samples at:</span></span> <br>
[<span data-ttu-id="54d10-128">Standalone Cluster Configuration Samples</span><span class="sxs-lookup"><span data-stu-id="54d10-128">Standalone Cluster Configuration Samples</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="54d10-129">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-129">Create the cluster</span></span>
<span data-ttu-id="54d10-130">Several sample cluster configuration files are installed with the setup package.</span><span class="sxs-lookup"><span data-stu-id="54d10-130">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="54d10-131">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span><span class="sxs-lookup"><span data-stu-id="54d10-131">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="54d10-132">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span><span class="sxs-lookup"><span data-stu-id="54d10-132">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="54d10-133">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span><span class="sxs-lookup"><span data-stu-id="54d10-133">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="54d10-134">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="54d10-134">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="54d10-135">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span><span class="sxs-lookup"><span data-stu-id="54d10-135">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="54d10-136">The cluster created in this article is unsecure.</span><span class="sxs-lookup"><span data-stu-id="54d10-136">The cluster created in this article is unsecure.</span></span>  <span data-ttu-id="54d10-137">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span><span class="sxs-lookup"><span data-stu-id="54d10-137">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="54d10-138">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="54d10-138">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span> <span data-ttu-id="54d10-139">Update the config file enable [certificate security](service-fabric-windows-cluster-x509-security.md) or [Windows security](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="54d10-139">Update the config file enable [certificate security](service-fabric-windows-cluster-x509-security.md) or [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="54d10-140">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span><span class="sxs-lookup"><span data-stu-id="54d10-140">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>

### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="54d10-141">Step 1A: Create an unsecured local development cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-141">Step 1A: Create an unsecured local development cluster</span></span>
<span data-ttu-id="54d10-142">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="54d10-142">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="54d10-143">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder.</span><span class="sxs-lookup"><span data-stu-id="54d10-143">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder.</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="54d10-144">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span><span class="sxs-lookup"><span data-stu-id="54d10-144">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="54d10-145">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="54d10-145">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="54d10-146">Step 1B: Create a multi-machine cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-146">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="54d10-147">After you have gone through the planning and preparation steps detailed at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md), you are ready to create your production cluster using your cluster configuration file.</span><span class="sxs-lookup"><span data-stu-id="54d10-147">After you have gone through the planning and preparation steps detailed at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md), you are ready to create your production cluster using your cluster configuration file.</span></span>

<span data-ttu-id="54d10-148">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span><span class="sxs-lookup"><span data-stu-id="54d10-148">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="54d10-149">You cannot install Service Fabric on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="54d10-149">You cannot install Service Fabric on a domain controller.</span></span>

1. <span data-ttu-id="54d10-150">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span><span class="sxs-lookup"><span data-stu-id="54d10-150">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="54d10-151">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span><span class="sxs-lookup"><span data-stu-id="54d10-151">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="54d10-152">Run the script to verify if you can create the development cluster:</span><span class="sxs-lookup"><span data-stu-id="54d10-152">Run the script to verify if you can create the development cluster:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="54d10-153">You should see output similiar to the following.</span><span class="sxs-lookup"><span data-stu-id="54d10-153">You should see output similiar to the following.</span></span> <span data-ttu-id="54d10-154">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span><span class="sxs-lookup"><span data-stu-id="54d10-154">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```powershell
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

2. <span data-ttu-id="54d10-155">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span><span class="sxs-lookup"><span data-stu-id="54d10-155">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="54d10-156">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="54d10-156">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="54d10-157">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span><span class="sxs-lookup"><span data-stu-id="54d10-157">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="54d10-158">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="54d10-158">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="54d10-159">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span><span class="sxs-lookup"><span data-stu-id="54d10-159">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="54d10-160">Step 1C: Create an offline (internet-disconnected) cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-160">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="54d10-161">The Service Fabric runtime package is automatically downloaded at cluster creation.</span><span class="sxs-lookup"><span data-stu-id="54d10-161">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="54d10-162">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span><span class="sxs-lookup"><span data-stu-id="54d10-162">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="54d10-163">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="54d10-163">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="54d10-164">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown in this example:</span><span class="sxs-lookup"><span data-stu-id="54d10-164">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown in this example:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```

<span data-ttu-id="54d10-165">*.\ClusterConfig.json* and *.\MicrosoftAzureServiceFabric.cab* are the paths to the cluster configuration and the runtime .cab file respectively.</span><span class="sxs-lookup"><span data-stu-id="54d10-165">*.\ClusterConfig.json* and *.\MicrosoftAzureServiceFabric.cab* are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>

### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="54d10-166">Step 2: Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-166">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="54d10-167">Connect to the cluster to verify the cluster is running and available.</span><span class="sxs-lookup"><span data-stu-id="54d10-167">Connect to the cluster to verify the cluster is running and available.</span></span> <span data-ttu-id="54d10-168">The ServiceFabric PowerShell module is installed with the runtime.</span><span class="sxs-lookup"><span data-stu-id="54d10-168">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="54d10-169">You can connect to the cluster from one of the cluster nodes or from a remote computer with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="54d10-169">You can connect to the cluster from one of the cluster nodes or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="54d10-170">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span><span class="sxs-lookup"><span data-stu-id="54d10-170">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>

<span data-ttu-id="54d10-171">To connect to an unsecure cluster, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="54d10-171">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```

<span data-ttu-id="54d10-172">For example:</span><span class="sxs-lookup"><span data-stu-id="54d10-172">For example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```

<span data-ttu-id="54d10-173">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span><span class="sxs-lookup"><span data-stu-id="54d10-173">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="54d10-174">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span><span class="sxs-lookup"><span data-stu-id="54d10-174">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="54d10-175">**HealthState** should be *OK* for each node.</span><span class="sxs-lookup"><span data-stu-id="54d10-175">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

### <a name="step-3-visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="54d10-176">Step 3: Visualize the cluster using Service Fabric explorer</span><span class="sxs-lookup"><span data-stu-id="54d10-176">Step 3: Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="54d10-177">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span><span class="sxs-lookup"><span data-stu-id="54d10-177">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="54d10-178">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="54d10-178">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>

<span data-ttu-id="54d10-179">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span><span class="sxs-lookup"><span data-stu-id="54d10-179">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="54d10-180">The node view shows the physical layout of the cluster.</span><span class="sxs-lookup"><span data-stu-id="54d10-180">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="54d10-181">For a given node, you can inspect which applications have code deployed on that node.</span><span class="sxs-lookup"><span data-stu-id="54d10-181">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="add-and-remove-nodes"></a><span data-ttu-id="54d10-183">Add and remove nodes</span><span class="sxs-lookup"><span data-stu-id="54d10-183">Add and remove nodes</span></span>
<span data-ttu-id="54d10-184">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span><span class="sxs-lookup"><span data-stu-id="54d10-184">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="54d10-185">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="54d10-185">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="54d10-186">Remove a cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-186">Remove a cluster</span></span>
<span data-ttu-id="54d10-187">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="54d10-187">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="54d10-188">You can optionally specify a location for the log of the deletion.</span><span class="sxs-lookup"><span data-stu-id="54d10-188">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="54d10-189">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span><span class="sxs-lookup"><span data-stu-id="54d10-189">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="54d10-190">The machine that this script is run on does not have to be part of the cluster.</span><span class="sxs-lookup"><span data-stu-id="54d10-190">The machine that this script is run on does not have to be part of the cluster.</span></span>

```powershell
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```powershell
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="54d10-191">Telemetry data collected and how to opt out of it</span><span class="sxs-lookup"><span data-stu-id="54d10-191">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="54d10-192">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span><span class="sxs-lookup"><span data-stu-id="54d10-192">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="54d10-193">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="54d10-193">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="54d10-194">If it is not reachable, the setup fails unless you opt out of telemetry.</span><span class="sxs-lookup"><span data-stu-id="54d10-194">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="54d10-195">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span><span class="sxs-lookup"><span data-stu-id="54d10-195">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="54d10-196">It is a best-effort upload and has no impact on the cluster functionality.</span><span class="sxs-lookup"><span data-stu-id="54d10-196">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="54d10-197">The telemetry is only sent from the node that runs the failover manager primary.</span><span class="sxs-lookup"><span data-stu-id="54d10-197">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="54d10-198">No other nodes send out telemetry.</span><span class="sxs-lookup"><span data-stu-id="54d10-198">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="54d10-199">The telemetry consists of the following:</span><span class="sxs-lookup"><span data-stu-id="54d10-199">The telemetry consists of the following:</span></span>

* <span data-ttu-id="54d10-200">Number of services</span><span class="sxs-lookup"><span data-stu-id="54d10-200">Number of services</span></span>
* <span data-ttu-id="54d10-201">Number of ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="54d10-201">Number of ServiceTypes</span></span>
* <span data-ttu-id="54d10-202">Number of Applications</span><span class="sxs-lookup"><span data-stu-id="54d10-202">Number of Applications</span></span>
* <span data-ttu-id="54d10-203">Number of ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="54d10-203">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="54d10-204">Number of FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="54d10-204">Number of FailoverUnits</span></span>
* <span data-ttu-id="54d10-205">Number of InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="54d10-205">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="54d10-206">Number of UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="54d10-206">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="54d10-207">Number of Replicas</span><span class="sxs-lookup"><span data-stu-id="54d10-207">Number of Replicas</span></span>
* <span data-ttu-id="54d10-208">Number of InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="54d10-208">Number of InBuildReplicas</span></span>
* <span data-ttu-id="54d10-209">Number of StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="54d10-209">Number of StandByReplicas</span></span>
* <span data-ttu-id="54d10-210">Number of OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="54d10-210">Number of OfflineReplicas</span></span>
* <span data-ttu-id="54d10-211">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="54d10-211">CommonQueueLength</span></span>
* <span data-ttu-id="54d10-212">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="54d10-212">QueryQueueLength</span></span>
* <span data-ttu-id="54d10-213">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="54d10-213">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="54d10-214">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="54d10-214">CommitQueueLength</span></span>
* <span data-ttu-id="54d10-215">Number of Nodes</span><span class="sxs-lookup"><span data-stu-id="54d10-215">Number of Nodes</span></span>
* <span data-ttu-id="54d10-216">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="54d10-216">IsContextComplete: True/False</span></span>
* <span data-ttu-id="54d10-217">ClusterId: This is a GUID randomly generated for each cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-217">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="54d10-218">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="54d10-218">ServiceFabricVersion</span></span>
* <span data-ttu-id="54d10-219">IP address of the virtual machine or machine from which the telemetry is uploaded</span><span class="sxs-lookup"><span data-stu-id="54d10-219">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="54d10-220">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="54d10-220">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="54d10-221">Preview features included in this package</span><span class="sxs-lookup"><span data-stu-id="54d10-221">Preview features included in this package</span></span>
<span data-ttu-id="54d10-222">None.</span><span class="sxs-lookup"><span data-stu-id="54d10-222">None.</span></span>


> [!NOTE]
> <span data-ttu-id="54d10-223">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span><span class="sxs-lookup"><span data-stu-id="54d10-223">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="54d10-224">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span><span class="sxs-lookup"><span data-stu-id="54d10-224">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="54d10-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="54d10-225">Next steps</span></span>
* [<span data-ttu-id="54d10-226">Deploy and remove applications using PowerShell</span><span class="sxs-lookup"><span data-stu-id="54d10-226">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="54d10-227">Configuration settings for standalone Windows cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-227">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="54d10-228">Add or remove nodes to a standalone Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="54d10-228">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="54d10-229">Upgrade a standalone Service Fabric cluster version</span><span class="sxs-lookup"><span data-stu-id="54d10-229">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="54d10-230">Create a standalone Service Fabric cluster with Azure VMs running Windows</span><span class="sxs-lookup"><span data-stu-id="54d10-230">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="54d10-231">Secure a standalone cluster on Windows using Windows security</span><span class="sxs-lookup"><span data-stu-id="54d10-231">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="54d10-232">Secure a standalone cluster on Windows using X509 certificates</span><span class="sxs-lookup"><span data-stu-id="54d10-232">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
[service-fabric-explorer]: ./media/service-fabric-cluster-creation-for-windows-server/sfx.png