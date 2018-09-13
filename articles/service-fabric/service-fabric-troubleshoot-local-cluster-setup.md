---
title: Troubleshoot your local Azure Service Fabric cluster setup | Microsoft Docs
description: This article covers a set of suggestions for troubleshooting your local development cluster
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: ''
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/23/2018
ms.author: mikhegn
ms.openlocfilehash: a759798fe0e452295df1abf1b8632af06dfe73c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774325"
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="81494-103">Troubleshoot your local development cluster setup</span><span class="sxs-lookup"><span data-stu-id="81494-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="81494-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span><span class="sxs-lookup"><span data-stu-id="81494-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="81494-105">Cluster setup failures</span><span class="sxs-lookup"><span data-stu-id="81494-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="81494-106">Cannot clean up Service Fabric logs</span><span class="sxs-lookup"><span data-stu-id="81494-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="81494-107">Problem</span><span class="sxs-lookup"><span data-stu-id="81494-107">Problem</span></span>
<span data-ttu-id="81494-108">While running the DevClusterSetup script, you see the following error:</span><span class="sxs-lookup"><span data-stu-id="81494-108">While running the DevClusterSetup script, you see the following error:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="81494-109">Solution</span><span class="sxs-lookup"><span data-stu-id="81494-109">Solution</span></span>
<span data-ttu-id="81494-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="81494-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="81494-111">You can now successfully run the script.</span><span class="sxs-lookup"><span data-stu-id="81494-111">You can now successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="81494-112">Cluster connection failures</span><span class="sxs-lookup"><span data-stu-id="81494-112">Cluster connection failures</span></span>

### <a name="type-initialization-exception"></a><span data-ttu-id="81494-113">Type Initialization exception</span><span class="sxs-lookup"><span data-stu-id="81494-113">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="81494-114">Problem</span><span class="sxs-lookup"><span data-stu-id="81494-114">Problem</span></span>
<span data-ttu-id="81494-115">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="81494-115">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="81494-116">Solution</span><span class="sxs-lookup"><span data-stu-id="81494-116">Solution</span></span>
<span data-ttu-id="81494-117">Your path variable was not correctly set during installation.</span><span class="sxs-lookup"><span data-stu-id="81494-117">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="81494-118">Sign out of Windows and sign back in.</span><span class="sxs-lookup"><span data-stu-id="81494-118">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="81494-119">This refreshes your path.</span><span class="sxs-lookup"><span data-stu-id="81494-119">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="81494-120">Cluster connection fails with "Object is closed"</span><span class="sxs-lookup"><span data-stu-id="81494-120">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="81494-121">Problem</span><span class="sxs-lookup"><span data-stu-id="81494-121">Problem</span></span>
<span data-ttu-id="81494-122">A call to Connect-ServiceFabricCluster fails with an error like this:</span><span class="sxs-lookup"><span data-stu-id="81494-122">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="81494-123">Solution</span><span class="sxs-lookup"><span data-stu-id="81494-123">Solution</span></span>
<span data-ttu-id="81494-124">Close the current PowerShell window and open a new PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="81494-124">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="81494-125">Fabric Connection Denied exception</span><span class="sxs-lookup"><span data-stu-id="81494-125">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="81494-126">Problem</span><span class="sxs-lookup"><span data-stu-id="81494-126">Problem</span></span>
<span data-ttu-id="81494-127">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span><span class="sxs-lookup"><span data-stu-id="81494-127">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="81494-128">Solution</span><span class="sxs-lookup"><span data-stu-id="81494-128">Solution</span></span>
<span data-ttu-id="81494-129">This error usually occurs when you try to start a service host process manually.</span><span class="sxs-lookup"><span data-stu-id="81494-129">This error usually occurs when you try to start a service host process manually.</span></span>

<span data-ttu-id="81494-130">Ensure that you do not have any service projects set as startup projects in your solution.</span><span class="sxs-lookup"><span data-stu-id="81494-130">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="81494-131">Only Service Fabric application projects should be set as startup projects.</span><span class="sxs-lookup"><span data-stu-id="81494-131">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="81494-132">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span><span class="sxs-lookup"><span data-stu-id="81494-132">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="81494-133">This removes the existing cluster and set up a new one.</span><span class="sxs-lookup"><span data-stu-id="81494-133">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="81494-134">Note that all deployed applications and associated data is removed.</span><span class="sxs-lookup"><span data-stu-id="81494-134">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="81494-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="81494-135">Next steps</span></span>
* [<span data-ttu-id="81494-136">Understand and troubleshoot your cluster with system health reports</span><span class="sxs-lookup"><span data-stu-id="81494-136">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="81494-137">Visualize your cluster with Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="81494-137">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

