---
title: Upgrade a standalone Azure Service Fabric cluster on Windows Server | Microsoft Docs
description: Upgrade the Azure Service Fabric code and/or configuration that runs a standalone Service Fabric cluster, including setting the cluster update mode.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: ''
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: chackdan
ms.openlocfilehash: ebfc80147ab8fef647e5d329a439b8137dea2371
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662360"
---
# <a name="upgrade-your-standalone-azure-service-fabric-cluster-on-windows-server"></a>Upgrade your standalone Azure Service Fabric cluster on Windows Server
> [!div class="op_single_selector"]
> * [Azure Cluster](service-fabric-cluster-upgrade.md)
> * [Standalone Cluster](service-fabric-cluster-upgrade-windows-server.md)
>
>

For any modern system, the ability to upgrade is a key to the long-term success of your product. An Azure Service Fabric cluster is a resource that you own. This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a>Control the Service Fabric version that runs on your cluster
To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the **fabricClusterAutoupgradeEnabled** cluster configuration to true. To select a supported version of Service Fabric that you want your cluster to be on, set the **fabricClusterAutoupgradeEnabled** cluster configuration to false.

> [!NOTE]
> Make sure that your cluster always runs a supported Service Fabric version. When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement. New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/). The new release is available to choose at that point.
>
>

You can upgrade your cluster to the new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine. If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.

Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version. One workflow is for clusters that have connectivity to download the latest version automatically. The other workflow is for clusters that do not have connectivity to download the latest Service Fabric version.

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a>Upgrade clusters that have connectivity to download the latest code and configuration
Use these steps to upgrade your cluster to a supported version if your cluster nodes have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).

For clusters that have connectivity to [http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.

When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade. Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:

“The current cluster version [version#] support ends [Date]."

After the cluster is running the latest version, the warning goes away.

#### <a name="cluster-upgrade-workflow"></a>Cluster upgrade workflow
After you see the cluster health warning, do the following:

1. Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster. The machine that this script is run on does not have to be part of the cluster.

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

2. Get the list of Service Fabric versions that you can upgrade to.

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    You should get an output similar to this:

    ![get fabric versions][getfabversions]
3. Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following Windows PowerShell command.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    If the cluster health policies are not met, the upgrade is rolled back. To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.

### <a name="upgrade-clusters-that-have-uno-connectivityu-to-download-the-latest-code-and-configuration"></a>Upgrade clusters that have <U>no connectivity</u> to download the latest code and configuration
Use these steps to upgrade your cluster to a supported version if your cluster nodes do not have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> If you are running a cluster that is not connected to the Internet, you will have to monitor the Service Fabric team blog to learn about a new release. The system does not show a cluster health warning to alert you of a new release.  
>
>

Modify your cluster configuration to set the following property to false before you start a configuration upgrade.

        "fabricClusterAutoupgradeEnabled": false,

Refer to [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details. Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a>Cluster upgrade workflow

1. Run Get-ServiceFabricClusterUpgrade from one of the nodes in the cluster and note the TargetCodeVersion.
2. Run the following from an internet connected machine to list all upgrade compatible versions with the current version and download the corresponding package from the associated download links.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster. The machine that this script is run on does not have to be part of the cluster

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Copy the downloaded package into the cluster image store.

5. Register the copied package.

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Start a cluster upgrade to an available version.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    If the cluster health policies are not met, the upgrade is rolled back. To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.


## <a name="upgrade-the-cluster-configuration"></a>Upgrade the cluster configuration
To upgrade the cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**. The configuration upgrade is processed upgrade domain by upgrade domain.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Cluster certificate config upgrade  
Cluster certificate is used for authentication between cluster nodes, so the certificate roll over should be performed with extra caution because failure will block the communication among cluster nodes.  
Technically, two options are supported:  

1. Single certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.   
2. Double certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.


## <a name="next-steps"></a>Next steps
* Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).
* Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).
* Learn about [application upgrades](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG

