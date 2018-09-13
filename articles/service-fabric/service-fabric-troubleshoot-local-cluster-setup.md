---
title: Troubleshoot your local Service Fabric cluster setup | Microsoft Docs
description: This article covers a set of suggestions for troubleshooting your local development cluster
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: seanmck
ms.openlocfilehash: 1b1e4ab93b399e9365a273096fb9747407d47581
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660901"
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="9e01c-103">Troubleshoot your local development cluster setup</span><span class="sxs-lookup"><span data-stu-id="9e01c-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="9e01c-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span><span class="sxs-lookup"><span data-stu-id="9e01c-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="9e01c-105">Cluster setup failures</span><span class="sxs-lookup"><span data-stu-id="9e01c-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="9e01c-106">Cannot clean up Service Fabric logs</span><span class="sxs-lookup"><span data-stu-id="9e01c-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="9e01c-107">Problem</span><span class="sxs-lookup"><span data-stu-id="9e01c-107">Problem</span></span>
<span data-ttu-id="9e01c-108">While running the DevClusterSetup script, you see an error like this:</span><span class="sxs-lookup"><span data-stu-id="9e01c-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="9e01c-109">Solution</span><span class="sxs-lookup"><span data-stu-id="9e01c-109">Solution</span></span>
<span data-ttu-id="9e01c-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9e01c-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="9e01c-111">You should now be able to successfully run the script.</span><span class="sxs-lookup"><span data-stu-id="9e01c-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="9e01c-112">Cluster connection failures</span><span class="sxs-lookup"><span data-stu-id="9e01c-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="9e01c-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e01c-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="9e01c-114">Problem</span><span class="sxs-lookup"><span data-stu-id="9e01c-114">Problem</span></span>
<span data-ttu-id="9e01c-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span><span class="sxs-lookup"><span data-stu-id="9e01c-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="9e01c-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span><span class="sxs-lookup"><span data-stu-id="9e01c-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="9e01c-117">Solution</span><span class="sxs-lookup"><span data-stu-id="9e01c-117">Solution</span></span>
<span data-ttu-id="9e01c-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e01c-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="9e01c-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span><span class="sxs-lookup"><span data-stu-id="9e01c-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="9e01c-120">Type Initialization exception</span><span class="sxs-lookup"><span data-stu-id="9e01c-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="9e01c-121">Problem</span><span class="sxs-lookup"><span data-stu-id="9e01c-121">Problem</span></span>
<span data-ttu-id="9e01c-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="9e01c-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="9e01c-123">Solution</span><span class="sxs-lookup"><span data-stu-id="9e01c-123">Solution</span></span>
<span data-ttu-id="9e01c-124">Your path variable was not correctly set during installation.</span><span class="sxs-lookup"><span data-stu-id="9e01c-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="9e01c-125">Please sign out of Windows and sign back in.</span><span class="sxs-lookup"><span data-stu-id="9e01c-125">Please sign out of Windows and sign back in.</span></span> <span data-ttu-id="9e01c-126">This will fully refresh your path.</span><span class="sxs-lookup"><span data-stu-id="9e01c-126">This will fully refresh your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="9e01c-127">Cluster connection fails with "Object is closed"</span><span class="sxs-lookup"><span data-stu-id="9e01c-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="9e01c-128">Problem</span><span class="sxs-lookup"><span data-stu-id="9e01c-128">Problem</span></span>
<span data-ttu-id="9e01c-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span><span class="sxs-lookup"><span data-stu-id="9e01c-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="9e01c-130">Solution</span><span class="sxs-lookup"><span data-stu-id="9e01c-130">Solution</span></span>
<span data-ttu-id="9e01c-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9e01c-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="9e01c-132">You should now be able to successfully connect.</span><span class="sxs-lookup"><span data-stu-id="9e01c-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="9e01c-133">Fabric Connection Denied exception</span><span class="sxs-lookup"><span data-stu-id="9e01c-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="9e01c-134">Problem</span><span class="sxs-lookup"><span data-stu-id="9e01c-134">Problem</span></span>
<span data-ttu-id="9e01c-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span><span class="sxs-lookup"><span data-stu-id="9e01c-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="9e01c-136">Solution</span><span class="sxs-lookup"><span data-stu-id="9e01c-136">Solution</span></span>
<span data-ttu-id="9e01c-137">This error usually occurs when you try to try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span><span class="sxs-lookup"><span data-stu-id="9e01c-137">This error usually occurs when you try to try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="9e01c-138">Ensure that you do not have any service projects set as startup projects in your solution.</span><span class="sxs-lookup"><span data-stu-id="9e01c-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="9e01c-139">Only Service Fabric application projects should be set as startup projects.</span><span class="sxs-lookup"><span data-stu-id="9e01c-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="9e01c-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span><span class="sxs-lookup"><span data-stu-id="9e01c-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="9e01c-141">This will remove the existing cluster and set up a new one.</span><span class="sxs-lookup"><span data-stu-id="9e01c-141">This will remove the existing cluster and set up a new one.</span></span> <span data-ttu-id="9e01c-142">Please note that all deployed applications and associated data will be removed.</span><span class="sxs-lookup"><span data-stu-id="9e01c-142">Please note that all deployed applications and associated data will be removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9e01c-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e01c-143">Next steps</span></span>
* [<span data-ttu-id="9e01c-144">Understand and troubleshoot your cluster with system health reports</span><span class="sxs-lookup"><span data-stu-id="9e01c-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="9e01c-145">Visualize your cluster with Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="9e01c-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

