---
title: Reliable service architecture | Microsoft Docs
description: Overview of the Reliable Service architecture for stateful and stateless services
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: 31b2550f90d61106a75b3e8e3679d1c36dc97fb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669775"
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Architecture for stateful and stateless Reliable Services
An Azure Service Fabric Reliable Service may be stateful or stateless. Each type of service runs within a specific architecture. These architectures are described in this article.
See the [Reliable Service overview](service-fabric-reliable-services-introduction.md) for more information about the differences between stateful and stateless services.

## <a name="stateful-reliable-services"></a>Stateful Reliable Services
### <a name="architecture-of-a-stateful-service"></a>Architecture of a stateful service
![Architecture diagram of a stateful service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Stateful Reliable Service
A stateful Reliable Service can derive from either the StatefulService or StatefulServiceBase class. Both of these base classes are provided by Service Fabric. They offer various levels of support and abstraction for the stateful service to interface with Service Fabric--and to participate as a service within the Service Fabric cluster.

StatefulService derives from StatefulServiceBase. StatefulServiceBase offers services more flexibility, but requires more understanding of the internals of Service Fabric.
See the [Reliable Service overview](service-fabric-reliable-services-introduction.md) and [Reliable Service advanced usage](service-fabric-reliable-services-advanced-usage.md) for more information on the specifics of writing services by using the StatefulService and StatefulServiceBase classes.

Both base classes manage the lifetime and role of the service implementation. The service implementation may override virtual methods of either base class if the service implementation has work to do at those points in the service implementation lifecycle--or if it wants to create a communication listener object. Note that although a service implementation may implement its own communication listener object exposing ICommunicationListener, in the diagram above, the communication listener is implemented by Service Fabric--as the service implementation uses a communication listener that is implemented by Service Fabric.

A stateful Reliable Service uses the reliable state manager to take advantage of reliable collections. Reliable collections are local data structures that are highly available to the service--that is, they are always available, regardless of service failovers. Each type of reliable collection is implemented by a reliable state provider.
For more information on reliable collections, see the [reliable collections overview](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Reliable state manager and state providers
The reliable state manager is the object that manages reliable state providers. It has the functionality to create, delete, enumerate, and ensure that the reliable state providers are persisted and highly available. A reliable state provider instance represents an instance of a persisted and highly available data structure, such as a dictionary or a queue.

Each reliable state provider exposes an interface that is used by a stateful service to interact with the reliable state provider. For example, IReliableDictionary is used to interface with the reliable dictionary, while IReliableQueue is used to interface with the reliable queue. All reliable state providers implement the IReliableState interface.

The reliable state manager has an interface named IReliableStateManager, which allows access to it from a stateful service. Interfaces to reliable state providers are returned through IReliableStateManager.

The reliable state manager uses a plug-in architecture so that new types of reliable collections can be plugged in dynamically.

The reliable dictionary and reliable queue are built upon the implementation of a high-performance, versioned differential store.

### <a name="transactional-replicator"></a>Transactional replicator
The transactional replicator component is responsible for ensuring that the state of a service (that is, the state within the reliable state manager and the reliable collections) is consistent across all replicas running the service. It also ensures that the state is persisted in the log. The reliable state manager interfaces with the transactional replicator via a private mechanism.

The transactional replicator uses a network protocol to communicate state with other replicas of the service instance so that all replicas have up-to-date state information.

The transactional replicator uses a log to persist state information so that the state information survives process or node crashes. The interface to the log is via a private mechanism.

### <a name="log"></a>Log
The log component provides a high-performance persistent store that can be optimized for writing to spinning or solid-state disks.  The design of the log is for the persistent storage (i.e., hard disks) to be local to the nodes that are running the stateful service. This allows for low latencies and high throughput, as compared to remote persistent storage, which is not local to the node.

The log component uses multiple log files. There is a node-wide shared log file that all replicas use as it can provide the lowest latency and highest throughput for storing state data. By default the shared log is placed in the Service Fabric node work directory but it may also be configured to be placed at another location, ideally on a disk reserved for only the shared log. Each replica for the service also has a dedicated log file and the dedicated log is placed within the service's work directory. There is no mechanism to configure the dedicated log to be placed at a different location.

The shared log is a transitional area for the replica's state information, while the dedicated log file is the final destination where it is persisted. In this design, the state information is first written to the shared log file and then lazily moved to the dedicated log file in the background. In this way, the write to the shared log would have the lowest latency and highest throughput which allows the service to make progress faster.

Reads and writes to the shared log are done via direct IO to preallocated space on the disk for the shared log file. To allow optimal use of disk space on the drive with dedicated logs, the dedicated log file is created as a NTFS sparse file. Note that this will allow overprovisioning of disk space and the OS will show the dedicated log files using much more disk space than is actually used.

Aside from a minimal user-mode interface to the log, the log is written as a kernel-mode driver. By running as a kernel-mode driver, the log can provide the highest performance to all services that use it.

For more information about configuring the log, see [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Stateless Reliable Service
### <a name="architecture-of-a-stateless-service"></a>Architecture of a stateless service
![Architecture diagram of a stateless service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Stateless Reliable Service
Stateless service implementations derive from the StatelessService or StatelessServiceBase class. The StatelessServiceBase class allows more flexibility than the StatelessService class.
Both base classes manage the lifetime and role of a service.

The service implementation may override virtual methods of either base class if the service has work to do at those points in the service lifecycle--or if it wants to create a communication listener object. Note that although the service may implement its own communication listener object exposing ICommunicationListener, in the diagram above, the communication listener is implemented by Service Fabric, as that service implementation uses a communication listener that is implemented by Service Fabric.

See the [Reliable Service overview](service-fabric-reliable-services-introduction.md) and [Reliable Service advanced usage](service-fabric-reliable-services-advanced-usage.md) for more information on the specifics of writing services using the StatelessService and StatelessServiceBase classes.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Next steps
For more information about Service Fabric, see:

[Reliable service overview](service-fabric-reliable-services-introduction.md)

[Quick start](service-fabric-reliable-services-quick-start.md)

[Reliable collections overview](service-fabric-reliable-services-reliable-collections.md)

[Reliable service advanced usage](service-fabric-reliable-services-advanced-usage.md)

[Reliable service configuration](service-fabric-reliable-services-configuration.md)  



