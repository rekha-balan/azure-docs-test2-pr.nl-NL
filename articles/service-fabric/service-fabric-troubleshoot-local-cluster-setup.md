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
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Troubleshoot your local development cluster setup
If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.

## <a name="cluster-setup-failures"></a>Cluster setup failures
### <a name="cannot-clean-up-service-fabric-logs"></a>Cannot clean up Service Fabric logs
#### <a name="problem"></a>Problem
While running the DevClusterSetup script, you see an error like this:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Solution
Close the current PowerShell window and open a new PowerShell window as an administrator. You should now be able to successfully run the script.

## <a name="cluster-connection-failures"></a>Cluster connection failures
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell
#### <a name="problem"></a>Problem
If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized. The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.

#### <a name="solution"></a>Solution
Always run Service Fabric cmdlets directly from Windows PowerShell.

> [!NOTE]
> The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.
> 
> 

### <a name="type-initialization-exception"></a>Type Initialization exception
#### <a name="problem"></a>Problem
When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Solution
Your path variable was not correctly set during installation. Please sign out of Windows and sign back in. This will fully refresh your path.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Cluster connection fails with "Object is closed"
#### <a name="problem"></a>Problem
A call to Connect-ServiceFabricCluster fails with an error like this:

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Solution
Close the current PowerShell window and open a new PowerShell window as an administrator. You should now be able to successfully connect.

### <a name="fabric-connection-denied-exception"></a>Fabric Connection Denied exception
#### <a name="problem"></a>Problem
When debugging from Visual Studio, you get a FabricConnectionDeniedException error.

#### <a name="solution"></a>Solution
This error usually occurs when you try to try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.

Ensure that you do not have any service projects set as startup projects in your solution. Only Service Fabric application projects should be set as startup projects.

> [!TIP]
> If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application. This will remove the existing cluster and set up a new one. Please note that all deployed applications and associated data will be removed.
> 
> 

## <a name="next-steps"></a>Next steps
* [Understand and troubleshoot your cluster with system health reports](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualize your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
