---
title: Azure Service Fabric differences between Linux and Windows | Microsoft Docs
description: Differences between the Azure Service Fabric on Linux and Azure Service Fabric on Windows.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/23/2018
ms.author: subramar
ms.openlocfilehash: 386bb07aeebb99fe224d03cac2e646f665c70d7c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830570"
---
# <a name="differences-between-service-fabric-on-linux-and-windows"></a><span data-ttu-id="83803-103">Differences between Service Fabric on Linux and Windows</span><span class="sxs-lookup"><span data-stu-id="83803-103">Differences between Service Fabric on Linux and Windows</span></span>

<span data-ttu-id="83803-104">There are some features that are supported on Windows, but not yet on Linux.</span><span class="sxs-lookup"><span data-stu-id="83803-104">There are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="83803-105">Eventually, the feature sets will be at parity and with each release this feature gap will shrink.</span><span class="sxs-lookup"><span data-stu-id="83803-105">Eventually, the feature sets will be at parity and with each release this feature gap will shrink.</span></span> <span data-ttu-id="83803-106">The following differences exist between the latest available releases.</span><span class="sxs-lookup"><span data-stu-id="83803-106">The following differences exist between the latest available releases.</span></span>

* <span data-ttu-id="83803-107">Envoy (Reverse Proxy) is in preview on Linux</span><span class="sxs-lookup"><span data-stu-id="83803-107">Envoy (Reverse Proxy) is in preview on Linux</span></span>
* <span data-ttu-id="83803-108">Standalone installer for Linux is not yet available on Linux</span><span class="sxs-lookup"><span data-stu-id="83803-108">Standalone installer for Linux is not yet available on Linux</span></span>
* <span data-ttu-id="83803-109">Console redirection (not supported in Linux or Windows production clusters)</span><span class="sxs-lookup"><span data-stu-id="83803-109">Console redirection (not supported in Linux or Windows production clusters)</span></span>
* <span data-ttu-id="83803-110">The Fault Analysis Service (FAS) on Linux</span><span class="sxs-lookup"><span data-stu-id="83803-110">The Fault Analysis Service (FAS) on Linux</span></span>
* <span data-ttu-id="83803-111">DNS service for Service Fabric services (DNS service is supported for containers on Linux)</span><span class="sxs-lookup"><span data-stu-id="83803-111">DNS service for Service Fabric services (DNS service is supported for containers on Linux)</span></span>
* <span data-ttu-id="83803-112">CLI command equivalents of certain Powershell commands (list below, most of which apply only to standalone clusters)</span><span class="sxs-lookup"><span data-stu-id="83803-112">CLI command equivalents of certain Powershell commands (list below, most of which apply only to standalone clusters)</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="83803-113">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="83803-113">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="83803-114">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="83803-114">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="83803-115">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="83803-115">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="83803-116">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="83803-116">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="83803-117">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="83803-117">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="83803-118">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="83803-118">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="83803-119">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="83803-119">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="83803-120">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="83803-120">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="83803-121">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="83803-121">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="83803-122">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="83803-122">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="83803-123">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="83803-123">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="83803-124">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="83803-124">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="83803-125">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="83803-125">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="83803-126">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="83803-126">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="83803-127">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="83803-127">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="83803-128">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="83803-128">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="83803-129">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="83803-129">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="83803-130">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="83803-130">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="83803-131">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="83803-131">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="83803-132">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="83803-132">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="83803-133">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="83803-133">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="83803-134">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="83803-134">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="83803-135">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="83803-135">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="83803-136">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="83803-136">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="83803-137">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="83803-137">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="83803-138">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="83803-138">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="83803-139">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="83803-139">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="83803-140">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="83803-140">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="83803-141">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="83803-141">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="83803-142">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="83803-142">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="83803-143">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="83803-143">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="83803-144">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="83803-144">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="83803-145">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="83803-145">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="83803-146">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="83803-146">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="83803-147">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="83803-147">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="83803-148">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="83803-148">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="83803-149">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="83803-149">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="83803-150">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="83803-150">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="83803-151">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="83803-151">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="83803-152">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="83803-152">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="83803-153">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="83803-153">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="83803-154">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="83803-154">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="83803-155">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="83803-155">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="83803-156">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="83803-156">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="83803-157">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="83803-157">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="83803-158">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="83803-158">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="83803-159">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="83803-159">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="83803-160">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="83803-160">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="83803-161">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="83803-161">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="83803-162">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="83803-162">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="83803-163">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="83803-163">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="83803-164">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="83803-164">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="83803-165">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="83803-165">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="83803-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="83803-166">Next steps</span></span>
* [<span data-ttu-id="83803-167">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="83803-167">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="83803-168">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="83803-168">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="83803-169">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span><span class="sxs-lookup"><span data-stu-id="83803-169">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="83803-170">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span><span class="sxs-lookup"><span data-stu-id="83803-170">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="83803-171">Create your first CSharp application on Linux</span><span class="sxs-lookup"><span data-stu-id="83803-171">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="83803-172">Use the Service Fabric CLI to manage your applications</span><span class="sxs-lookup"><span data-stu-id="83803-172">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
