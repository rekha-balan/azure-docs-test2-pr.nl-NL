---
title: Upgrade a standalone Azure Service Fabric cluster on Windows Server | Microsoft Docs
description: Upgrade the Azure Service Fabric code and/or configuration that runs a standalone Service Fabric cluster, including setting the cluster update mode.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: ''
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/15/2017
ms.author: dekapur
ms.openlocfilehash: 93b79b7adacdec18912d28bb9725e2dc77737d59
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793837"
---
# <a name="upgrade-your-standalone-azure-service-fabric-cluster-on-windows-server"></a><span data-ttu-id="31f63-103">Upgrade your standalone Azure Service Fabric cluster on Windows Server</span><span class="sxs-lookup"><span data-stu-id="31f63-103">Upgrade your standalone Azure Service Fabric cluster on Windows Server</span></span> 
> [!div class="op_single_selector"]
> * [Azure cluster](service-fabric-cluster-upgrade.md)
> * [Standalone cluster](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="31f63-106">For any modern system, the ability to upgrade is key to the long-term success of your product.</span><span class="sxs-lookup"><span data-stu-id="31f63-106">For any modern system, the ability to upgrade is key to the long-term success of your product.</span></span> <span data-ttu-id="31f63-107">An Azure Service Fabric cluster is a resource that you own.</span><span class="sxs-lookup"><span data-stu-id="31f63-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="31f63-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span><span class="sxs-lookup"><span data-stu-id="31f63-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="31f63-109">Control the Service Fabric version that runs on your cluster</span><span class="sxs-lookup"><span data-stu-id="31f63-109">Control the Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="31f63-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the fabricClusterAutoupgradeEnabled cluster configuration to *true*.</span><span class="sxs-lookup"><span data-stu-id="31f63-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the fabricClusterAutoupgradeEnabled cluster configuration to *true*.</span></span> <span data-ttu-id="31f63-111">To select a supported version of Service Fabric that you want your cluster to be on, set the fabricClusterAutoupgradeEnabled cluster configuration to *false*.</span><span class="sxs-lookup"><span data-stu-id="31f63-111">To select a supported version of Service Fabric that you want your cluster to be on, set the fabricClusterAutoupgradeEnabled cluster configuration to *false*.</span></span>

> [!NOTE]
> Make sure that your cluster always runs a supported Service Fabric version. When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement. New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/). The new release is available to choose at that point.
>
>

<span data-ttu-id="31f63-116">You can upgrade your cluster to the new version only if you're using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="31f63-116">You can upgrade your cluster to the new version only if you're using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="31f63-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span><span class="sxs-lookup"><span data-stu-id="31f63-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span></span>

<span data-ttu-id="31f63-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span><span class="sxs-lookup"><span data-stu-id="31f63-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="31f63-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span><span class="sxs-lookup"><span data-stu-id="31f63-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span></span> <span data-ttu-id="31f63-120">The other workflow is for clusters that don't have connectivity to download the latest Service Fabric version.</span><span class="sxs-lookup"><span data-stu-id="31f63-120">The other workflow is for clusters that don't have connectivity to download the latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="31f63-121">Upgrade clusters that have connectivity to download the latest code and configuration</span><span class="sxs-lookup"><span data-stu-id="31f63-121">Upgrade clusters that have connectivity to download the latest code and configuration</span></span>
<span data-ttu-id="31f63-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have internet connectivity to the [Microsoft Download Center](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="31f63-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have internet connectivity to the [Microsoft Download Center](http://download.microsoft.com).</span></span>

<span data-ttu-id="31f63-123">For clusters that have connectivity to the [Microsoft Download Center](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span><span class="sxs-lookup"><span data-stu-id="31f63-123">For clusters that have connectivity to the [Microsoft Download Center](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span></span>

<span data-ttu-id="31f63-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span><span class="sxs-lookup"><span data-stu-id="31f63-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span></span> <span data-ttu-id="31f63-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span><span class="sxs-lookup"><span data-stu-id="31f63-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span></span>

<span data-ttu-id="31f63-126">"The current cluster version [version #] support ends [date]."</span><span class="sxs-lookup"><span data-stu-id="31f63-126">"The current cluster version [version #] support ends [date]."</span></span>

<span data-ttu-id="31f63-127">After the cluster is running the latest version, the warning goes away.</span><span class="sxs-lookup"><span data-stu-id="31f63-127">After the cluster is running the latest version, the warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="31f63-128">Cluster upgrade workflow</span><span class="sxs-lookup"><span data-stu-id="31f63-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="31f63-129">When you see the cluster health warning, do the following:</span><span class="sxs-lookup"><span data-stu-id="31f63-129">When you see the cluster health warning, do the following:</span></span>

1. <span data-ttu-id="31f63-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="31f63-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="31f63-131">The machine that this script is run on doesn't have to be part of the cluster.</span><span class="sxs-lookup"><span data-stu-id="31f63-131">The machine that this script is run on doesn't have to be part of the cluster.</span></span>

    ```powershell

    ###### connect to the secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="31f63-132">Get the list of Service Fabric versions that you can upgrade to.</span><span class="sxs-lookup"><span data-stu-id="31f63-132">Get the list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="31f63-133">You should get an output similar to this:</span><span class="sxs-lookup"><span data-stu-id="31f63-133">You should get an output similar to this:</span></span>

    ![Get Service Fabric versions][getfabversions]
3. <span data-ttu-id="31f63-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterupgrade) Windows PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="31f63-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterupgrade) Windows PowerShell command.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="31f63-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="31f63-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following PowerShell command:</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="31f63-137">If the cluster health policies aren't met, the upgrade is rolled back.</span><span class="sxs-lookup"><span data-stu-id="31f63-137">If the cluster health policies aren't met, the upgrade is rolled back.</span></span> <span data-ttu-id="31f63-138">To specify custom health policies for the Start-ServiceFabricClusterUpgrade command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterupgrade).</span><span class="sxs-lookup"><span data-stu-id="31f63-138">To specify custom health policies for the Start-ServiceFabricClusterUpgrade command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterupgrade).</span></span>

    <span data-ttu-id="31f63-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span><span class="sxs-lookup"><span data-stu-id="31f63-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-no-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="31f63-140">Upgrade clusters that have *no connectivity* to download the latest code and configuration</span><span class="sxs-lookup"><span data-stu-id="31f63-140">Upgrade clusters that have *no connectivity* to download the latest code and configuration</span></span>
<span data-ttu-id="31f63-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes don't have internet connectivity to the [Microsoft Download Center](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="31f63-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes don't have internet connectivity to the [Microsoft Download Center](http://download.microsoft.com).</span></span>

> [!NOTE]
> If you're running a cluster that isn't connected to the internet, you have to monitor the Service Fabric team blog to learn about new releases. The system doesn't show a cluster health warning to alert you of new releases.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="31f63-144">Auto provisioning vs. manual provisioning</span><span class="sxs-lookup"><span data-stu-id="31f63-144">Auto provisioning vs. manual provisioning</span></span>
<span data-ttu-id="31f63-145">To enable automatic downloading and registration for the latest code version, set up the Service Fabric Update Service.</span><span class="sxs-lookup"><span data-stu-id="31f63-145">To enable automatic downloading and registration for the latest code version, set up the Service Fabric Update Service.</span></span> <span data-ttu-id="31f63-146">For instructions, see Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [standalone package](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="31f63-146">For instructions, see Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [standalone package](service-fabric-cluster-standalone-package-contents.md).</span></span>
<span data-ttu-id="31f63-147">For the manual process, follow these instructions.</span><span class="sxs-lookup"><span data-stu-id="31f63-147">For the manual process, follow these instructions.</span></span>

<span data-ttu-id="31f63-148">Modify your cluster configuration to set the following property to *false* before you start a configuration upgrade:</span><span class="sxs-lookup"><span data-stu-id="31f63-148">Modify your cluster configuration to set the following property to *false* before you start a configuration upgrade:</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="31f63-149">For usage details, see the [Start-ServiceFabricClusterConfigurationUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade) PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="31f63-149">For usage details, see the [Start-ServiceFabricClusterConfigurationUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade) PowerShell command.</span></span> <span data-ttu-id="31f63-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span><span class="sxs-lookup"><span data-stu-id="31f63-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="31f63-151">Cluster upgrade workflow</span><span class="sxs-lookup"><span data-stu-id="31f63-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="31f63-152">Run [Get-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterupgrade) from one of the nodes in the cluster and note the *TargetCodeVersion*.</span><span class="sxs-lookup"><span data-stu-id="31f63-152">Run [Get-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterupgrade) from one of the nodes in the cluster and note the *TargetCodeVersion*.</span></span>

2. <span data-ttu-id="31f63-153">Run the following from an internet-connected machine to list all upgrade-compatible versions with the current version and download the corresponding package from the associated download links:</span><span class="sxs-lookup"><span data-stu-id="31f63-153">Run the following from an internet-connected machine to list all upgrade-compatible versions with the current version and download the corresponding package from the associated download links:</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="31f63-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="31f63-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="31f63-155">The machine that this script is run on doesn't have to be part of the cluster.</span><span class="sxs-lookup"><span data-stu-id="31f63-155">The machine that this script is run on doesn't have to be part of the cluster.</span></span>

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="31f63-156">Copy the downloaded package into the cluster image store.</span><span class="sxs-lookup"><span data-stu-id="31f63-156">Copy the downloaded package into the cluster image store.</span></span>

5. <span data-ttu-id="31f63-157">Register the copied package.</span><span class="sxs-lookup"><span data-stu-id="31f63-157">Register the copied package.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="31f63-158">Start a cluster upgrade to an available version.</span><span class="sxs-lookup"><span data-stu-id="31f63-158">Start a cluster upgrade to an available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="31f63-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="31f63-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command:</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="31f63-160">If the cluster health policies aren't met, the upgrade is rolled back.</span><span class="sxs-lookup"><span data-stu-id="31f63-160">If the cluster health policies aren't met, the upgrade is rolled back.</span></span> <span data-ttu-id="31f63-161">To specify custom health policies for the Start-ServiceFabricClusterUpgrade command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterupgrade).</span><span class="sxs-lookup"><span data-stu-id="31f63-161">To specify custom health policies for the Start-ServiceFabricClusterUpgrade command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterupgrade).</span></span>

    <span data-ttu-id="31f63-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span><span class="sxs-lookup"><span data-stu-id="31f63-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>


## <a name="upgrade-the-cluster-configuration"></a><span data-ttu-id="31f63-163">Upgrade the cluster configuration</span><span class="sxs-lookup"><span data-stu-id="31f63-163">Upgrade the cluster configuration</span></span>
<span data-ttu-id="31f63-164">Before you initiate the configuration upgrade, you can test your new cluster configuration JSON by running the following PowerShell script in the standalone package:</span><span class="sxs-lookup"><span data-stu-id="31f63-164">Before you initiate the configuration upgrade, you can test your new cluster configuration JSON by running the following PowerShell script in the standalone package:</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
<span data-ttu-id="31f63-165">Or use this script:</span><span class="sxs-lookup"><span data-stu-id="31f63-165">Or use this script:</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

<span data-ttu-id="31f63-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. The new cluster configuration JSON is tested against the old one and throws errors in the PowerShell window if there's an issue.</span><span class="sxs-lookup"><span data-stu-id="31f63-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. The new cluster configuration JSON is tested against the old one and throws errors in the PowerShell window if there's an issue.</span></span>

<span data-ttu-id="31f63-167">To upgrade the cluster configuration upgrade, run [Start-ServiceFabricClusterConfigurationUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade).</span><span class="sxs-lookup"><span data-stu-id="31f63-167">To upgrade the cluster configuration upgrade, run [Start-ServiceFabricClusterConfigurationUpgrade](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade).</span></span> <span data-ttu-id="31f63-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span><span class="sxs-lookup"><span data-stu-id="31f63-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="31f63-169">Cluster certificate config upgrade</span><span class="sxs-lookup"><span data-stu-id="31f63-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="31f63-170">A cluster certificate is used for authentication between cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="31f63-170">A cluster certificate is used for authentication between cluster nodes.</span></span> <span data-ttu-id="31f63-171">The certificate rollover should be performed with extra caution because failure blocks the communication among cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="31f63-171">The certificate rollover should be performed with extra caution because failure blocks the communication among cluster nodes.</span></span>

<span data-ttu-id="31f63-172">Technically, four options are supported:</span><span class="sxs-lookup"><span data-stu-id="31f63-172">Technically, four options are supported:</span></span>  

* <span data-ttu-id="31f63-173">Single certificate upgrade: The upgrade path is Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) ->....</span><span class="sxs-lookup"><span data-stu-id="31f63-173">Single certificate upgrade: The upgrade path is Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) ->....</span></span>

* <span data-ttu-id="31f63-174">Double certificate upgrade: The upgrade path is Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) ->....</span><span class="sxs-lookup"><span data-stu-id="31f63-174">Double certificate upgrade: The upgrade path is Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) ->....</span></span>

* <span data-ttu-id="31f63-175">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span><span class="sxs-lookup"><span data-stu-id="31f63-175">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="31f63-176">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span><span class="sxs-lookup"><span data-stu-id="31f63-176">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>

* <span data-ttu-id="31f63-177">Certificate issuer thumbprint upgrade: The upgrade path is Certificate CN=A,IssuerThumbprint=IT1 (Primary) -> Certificate CN=A,IssuerThumbprint=IT1,IT2 (Primary) -> Certificate CN=A,IssuerThumbprint=IT2 (Primary).</span><span class="sxs-lookup"><span data-stu-id="31f63-177">Certificate issuer thumbprint upgrade: The upgrade path is Certificate CN=A,IssuerThumbprint=IT1 (Primary) -> Certificate CN=A,IssuerThumbprint=IT1,IT2 (Primary) -> Certificate CN=A,IssuerThumbprint=IT2 (Primary).</span></span>


## <a name="next-steps"></a><span data-ttu-id="31f63-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="31f63-178">Next steps</span></span>
* <span data-ttu-id="31f63-179">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="31f63-179">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="31f63-180">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="31f63-180">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="31f63-181">Learn about [application upgrades](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="31f63-181">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
