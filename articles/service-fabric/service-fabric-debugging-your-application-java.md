---
title: Debug your Azure Service Fabric Application in Eclipse| Microsoft Docs
description: Improve the reliability and performance of your services by developing and debugging them in Eclipse on a local development cluster.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: c31d8019dfa8e483d545543bdcae96f330c7be34
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564644"
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="2f1bb-103">Debug your Java Service Fabric application using Eclipse</span><span class="sxs-lookup"><span data-stu-id="2f1bb-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="2f1bb-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2f1bb-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="2f1bb-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="2f1bb-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="2f1bb-109">Port 8001 is set for debugging in this example.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="2f1bb-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="2f1bb-111">This setting avoids conflicts for the port that is used for debugging.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="2f1bb-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="2f1bb-113">Deploy the application.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-113">Deploy the application.</span></span>

5. <span data-ttu-id="2f1bb-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span><span class="sxs-lookup"><span data-stu-id="2f1bb-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="2f1bb-115">Set breakpoints at desired points and debug the application.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="2f1bb-116">If the application is crashing, you may also want to enable coredumps.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="2f1bb-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="2f1bb-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="2f1bb-119">You can also verify the status using the command ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="2f1bb-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="2f1bb-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="2f1bb-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f1bb-121">Next steps</span></span>

* <span data-ttu-id="2f1bb-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="2f1bb-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="2f1bb-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2f1bb-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
