---
title: Azure Service Fabric differences between Linux and Windows | Microsoft Docs
description: Differences between the Azure Service Fabric Preview on Linux and Azure Service Fabric on Windows.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/23/2017
ms.author: subramar
ms.openlocfilehash: 5faf7dc0b544f6fe2f83565cc368e218c6df35af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549827"
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="55ff7-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span><span class="sxs-lookup"><span data-stu-id="55ff7-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="55ff7-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not on Linux.</span></span> <span data-ttu-id="55ff7-105">Eventually, the feature sets will be at parity when Service Fabric on Linux becomes generally available.</span><span class="sxs-lookup"><span data-stu-id="55ff7-105">Eventually, the feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span>

* <span data-ttu-id="55ff7-106">Reliable Collections (and Reliable Stateful Services) are not supported on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-106">Reliable Collections (and Reliable Stateful Services) are not supported on Linux.</span></span>
* <span data-ttu-id="55ff7-107">ReverseProxy isn't available on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-107">ReverseProxy isn't available on Linux.</span></span>
* <span data-ttu-id="55ff7-108">Standalone installer isn't available on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-108">Standalone installer isn't available on Linux.</span></span>
* <span data-ttu-id="55ff7-109">XML schema validation for manifest files is not performed on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-109">XML schema validation for manifest files is not performed on Linux.</span></span> 
* <span data-ttu-id="55ff7-110">Console redirection isn't supported on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-110">Console redirection isn't supported on Linux.</span></span> 
* <span data-ttu-id="55ff7-111">The Fault Analysis Service (FAS) isn't available on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-111">The Fault Analysis Service (FAS) isn't available on Linux.</span></span>
* <span data-ttu-id="55ff7-112">Azure Active Directory support isn't available on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-112">Azure Active Directory support isn't available on Linux.</span></span>
* <span data-ttu-id="55ff7-113">Some CLI command equivalents of Powershell commands aren't available.</span><span class="sxs-lookup"><span data-stu-id="55ff7-113">Some CLI command equivalents of Powershell commands aren't available.</span></span>
* <span data-ttu-id="55ff7-114">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in the next section).</span><span class="sxs-lookup"><span data-stu-id="55ff7-114">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in the next section).</span></span>

>[!NOTE]
><span data-ttu-id="55ff7-115">Console redirection isn't supported in production clusters, even on Windows.</span><span class="sxs-lookup"><span data-stu-id="55ff7-115">Console redirection isn't supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="55ff7-116">The development tooling is different with VisualStudio, Powershell, VSTS, and ETW being used on Windows and Yeoman, Eclipse, Jenkins, and LTTng used on Linux.</span><span class="sxs-lookup"><span data-stu-id="55ff7-116">The development tooling is different with VisualStudio, Powershell, VSTS, and ETW being used on Windows and Yeoman, Eclipse, Jenkins, and LTTng used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="55ff7-117">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="55ff7-117">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="55ff7-118">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="55ff7-118">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="55ff7-119">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="55ff7-119">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="55ff7-120">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="55ff7-120">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="55ff7-121">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="55ff7-121">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="55ff7-122">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="55ff7-122">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="55ff7-123">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="55ff7-123">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="55ff7-124">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="55ff7-124">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="55ff7-125">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="55ff7-125">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="55ff7-126">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="55ff7-126">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="55ff7-127">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="55ff7-127">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="55ff7-128">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="55ff7-128">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="55ff7-129">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="55ff7-129">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="55ff7-130">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="55ff7-130">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="55ff7-131">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="55ff7-131">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="55ff7-132">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="55ff7-132">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="55ff7-133">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="55ff7-133">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="55ff7-134">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="55ff7-134">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="55ff7-135">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="55ff7-135">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="55ff7-136">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="55ff7-136">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="55ff7-137">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="55ff7-137">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="55ff7-138">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="55ff7-138">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="55ff7-139">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="55ff7-139">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="55ff7-140">Cmd</span><span class="sxs-lookup"><span data-stu-id="55ff7-140">Cmd</span></span>
* <span data-ttu-id="55ff7-141">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="55ff7-141">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="55ff7-142">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="55ff7-142">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="55ff7-143">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="55ff7-143">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="55ff7-144">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="55ff7-144">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="55ff7-145">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="55ff7-145">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="55ff7-146">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="55ff7-146">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="55ff7-147">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="55ff7-147">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="55ff7-148">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="55ff7-148">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="55ff7-149">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="55ff7-149">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="55ff7-150">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="55ff7-150">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="55ff7-151">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="55ff7-151">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="55ff7-152">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="55ff7-152">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="55ff7-153">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="55ff7-153">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="55ff7-154">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="55ff7-154">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="55ff7-155">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="55ff7-155">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="55ff7-156">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="55ff7-156">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="55ff7-157">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="55ff7-157">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="55ff7-158">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="55ff7-158">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="55ff7-159">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="55ff7-159">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="55ff7-160">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="55ff7-160">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="55ff7-161">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="55ff7-161">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="55ff7-162">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="55ff7-162">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="55ff7-163">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="55ff7-163">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="55ff7-164">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="55ff7-164">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="55ff7-165">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="55ff7-165">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="55ff7-166">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="55ff7-166">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="55ff7-167">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="55ff7-167">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="55ff7-168">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="55ff7-168">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="55ff7-169">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="55ff7-169">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="55ff7-170">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="55ff7-170">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="55ff7-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="55ff7-171">Next steps</span></span>
* [<span data-ttu-id="55ff7-172">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="55ff7-172">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="55ff7-173">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="55ff7-173">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="55ff7-174">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span><span class="sxs-lookup"><span data-stu-id="55ff7-174">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="55ff7-175">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span><span class="sxs-lookup"><span data-stu-id="55ff7-175">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="55ff7-176">Create your first CSharp application on Linux</span><span class="sxs-lookup"><span data-stu-id="55ff7-176">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="55ff7-177">Use the Azure CLI to manage your Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="55ff7-177">Use the Azure CLI to manage your Service Fabric applications</span></span>](service-fabric-azure-cli.md)
