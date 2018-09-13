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
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Troubleshoot your local development cluster setup
If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.

## <a name="cluster-setup-failures"></a>Cluster setup failures
### <a name="cannot-clean-up-service-fabric-logs"></a>Cannot clean up Service Fabric logs
#### <a name="problem"></a>Problem
While running the DevClusterSetup script, you see the following error:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Solution
Close the current PowerShell window and open a new PowerShell window as an administrator. You can now successfully run the script.

## <a name="cluster-connection-failures"></a>Cluster connection failures

### <a name="type-initialization-exception"></a>Type Initialization exception
#### <a name="problem"></a>Problem
When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Solution
Your path variable was not correctly set during installation. Sign out of Windows and sign back in. This refreshes your path.

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
Close the current PowerShell window and open a new PowerShell window as an administrator.

### <a name="fabric-connection-denied-exception"></a>Fabric Connection Denied exception
#### <a name="problem"></a>Problem
When debugging from Visual Studio, you get a FabricConnectionDeniedException error.

#### <a name="solution"></a>Solution
This error usually occurs when you try to start a service host process manually.

Ensure that you do not have any service projects set as startup projects in your solution. Only Service Fabric application projects should be set as startup projects.

> [!TIP]
> If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application. This removes the existing cluster and set up a new one. Note that all deployed applications and associated data is removed.
> 
> 

## <a name="next-steps"></a>Next steps
* [Understand and troubleshoot your cluster with system health reports](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualize your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

