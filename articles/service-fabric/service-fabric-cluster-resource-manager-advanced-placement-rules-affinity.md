---
title: Service Fabric Cluster Resource Manager - Affinity | Microsoft Docs
description: Overview of configuring affinity for Service Fabric Services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: bd7444947924be0b66e4838cfc4917822ab770e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564694"
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Configuring and using service affinity in Service Fabric
Affinity is a control that is provided mainly to help ease the transition of larger monolithic applications into the cloud and microservices world. That said it can also be used in certain cases as a legitimate optimization for improving the performance of services, although doing so can have side effects.

Let’s say you’re bringing a larger app, or one that just wasn’t designed with microservices in mind, to Service Fabric. This type of transition is common. You start by lifting the entire app into the environment, packaging it, and making sure it is running smoothly. Then you start breaking it down into different smaller services that all talk to each other.

Then there’s an “Oops...”. The “Oops” usually falls into one of these categories:

1. Some component X in the monolithic app had an undocumented dependency on component Y, and you just turned those components into separate services. Since these services are now running on different nodes in the cluster, they're broken.
2. These things communicate via (local named pipes | shared memory | files on disk) but they really need to be able to write to a shared resource for performance reasons right now. That hard dependency gets removed later.
3. Everything is fine, but it turns out that these two components are actually chatty/performance sensitive. When they moved them into separate services overall application performance tanked or latency increased. As a result, the overall application is not meeting expectations.

In these cases we don’t want to lose our refactoring work, and don’t want to go back to the monolith. However, until we can redesign the components to work naturally as services (or until we can solve the performance expectations some other way) we're going to need some sense of locality.

What to do? Well, you could try turning on affinity.

## <a name="how-to-configure-affinity"></a>How to configure affinity
To set up affinity, you define an affinity relationship between two different services. You can think of affinity as “pointing” one service at another and saying “This service can only run where that service is running.” Sometimes we refer to affinity as a parent/child relationship (where you point the child at the parent). Affinity ensures that the replicas or instances of one service are placed on the same nodes as the replicas or instances of another.

``` csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

## <a name="different-affinity-options"></a>Different affinity options
Affinity is represented via one of several correlation schemes, and has two different modes. The most common mode of affinity is what we call NonAlignedAffinity. In NonAlignedAffinity, the replicas or instances of the different services are placed on the same nodes. The other mode is AlignedAffinity. Aligned Affinity is useful only with stateful services. Configuring two stateful services to have aligned affinity ensures that the primaries of those services are placed on the same nodes as each other. It also causes each pair of secondaries for those services to be placed on the same nodes. It is also possible (though less common) to configure NonAlignedAffinity for stateful services. For NonAlignedAffinity, the different replicas of the two stateful services would be collocated on the same nodes, but no attempt would be made to align their primaries or secondaries.

<center>
![Affinity Modes and Their Effects][Image1]
</center>

### <a name="best-effort-desired-state"></a>Best effort desired state
There are a few differences between affinity and monolithic architectures. Many of them are because an affinity relationship is best effort. The services in an affinity relationship are fundamentally different entities that can fail and be moved independently. There are also causes for why an affinity relationship could break. For example, capacity limitations where only some of the service objects in the affinity relationship can fit on a given node. In these cases even though there's an affinity relationship in place, it can't be enforced due to the other constraints. if it is possible to do so, the violation is automatically corrected later.

### <a name="chains-vs-stars"></a>Chains vs. stars
Today the Cluster Resource Manager isn't able to model chains of affinity relationships. What this means is that a service that is a child in one affinity relationship can’t be a parent in another affinity relationship. If you want to model this type of relationship, you effectively have to model it as a star, rather than a chain. To move from a chain to a star, the bottommost child would be parented to the first child’s parent instead. Depending on the arrangement of your services, you may have to do this multiple times. If there's no natural parent service, you may have to create one that serves as a placeholder. Depending on your requirements, you may also want to look into [Application Groups](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Chains vs. Stars in the Context of Affinity Relationships][Image2]
</center>

Another thing to note about affinity relationships today is that they are directional. This means that the “affinity” rule only enforces that the child is where the parent is, not that the parent is located with the child. For example, let's say the parent suddenly fails over to another node. When this happens the Cluster Resource Manager thinks everything is fine until it notices that the child is not located with a parent. The affinity relationship can't be perfect or instantly enforced since these are different services with different lifecycles.

### <a name="partitioning-support"></a>Partitioning support
The final thing to notice about affinity is that affinity relationships aren’t supported where the parent is partitioned. This is something that we may support eventually, but today it is not allowed.

## <a name="next-steps"></a>Next steps
* For more information about the other options available for configuring services, check out the topic on the other Cluster Resource Manager configurations available [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)
* For uses such as limiting services to a small set of machines and trying to aggregate the load of a collection of services, use [Application Groups](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png


