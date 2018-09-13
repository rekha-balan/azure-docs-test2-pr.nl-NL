---
title: Application scenarios and design | Microsoft Docs
description: Overview of categories of cloud applications in Service Fabric. Discusses application design that uses stateful and stateless services.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/17/2017
ms.author: mfussell
ms.openlocfilehash: 3eb35fa17698d88e676d66d9a9101580467af731
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554362"
---
# <a name="service-fabric-application-scenarios"></a>Service Fabric application scenarios
Azure Service Fabric offers a reliable and flexible platform that enables you to write and run many types of business applications and services. These applications and microservices can be stateless or stateful, and they are resource-balanced across virtual machines to maximize efficiency. The unique architecture of Service Fabric enables you to perform near real-time data analysis, in-memory computation, parallel transactions, and event processing in your applications. You can easily scale your applications up or down (really in or out), depending on your changing resource requirements.

The Service Fabric platform in Azure is ideal for the following categories of applications:

* **Highly available services**: Service Fabric services provide fast failover by creating multiple secondary service replicas. If a node, process, or individual service goes down due to hardware or other failure, one of the secondary replicas is promoted to a primary replica with minimal loss of service.
* **Scalable services**: Individual services can be partitioned, allowing for state to be scaled out across the cluster. In addition, individual services can be created and removed on the fly. Services can be quickly and easily scaled out from a few instances on a few nodes to thousands of instances on many nodes, and then scaled in again, depending on your resource needs. You can use Service Fabric to build these services and manage their complete lifecycles.
* **Computation on nonstatic data**: Service Fabric enables you to build data, input/output, and compute intensive stateful applications. Service Fabric allows the collocation of processing (computation) and data in applications. Normally, when your application requires access to data, there is network latency associated with an external data cache or storage tier. With stateful Service Fabric services, that latency is eliminated, enabling more performant reads and writes. Say for example that you have an application that performs near real-time recommendation selections for customers, with a round-trip time requirement of less than 100 milliseconds. The latency and performance characteristics of Service Fabric services (where the computation of recommendation selection is collocated with the data and rules) provides a responsive experience to the user compared with the standard implementation model of having to fetch the necessary data from remote storage.  
* **Session-based interactive applications**: Service Fabric is useful if your applications, such as online gaming or instant messaging, require low latency reads and writes. Service Fabric enables you to build these interactive, stateful applications without having to create a separate store or cache, as required for stateless apps. (This increases latency and potentially introduces consistency issues.)
* **Distributed graph processing**: The growth of social networks has greatly increased the need to analyze large-scale graphs in parallel. Fast scaling and parallel load processing make Service Fabric a natural platform for processing large-scale graphs. Service Fabric enables you to build highly scalable services for groups such as social networking, business intelligence, and scientific research.
* **Data analytics and workflows**: The fast reads and writes of Service Fabric enable applications that must reliably process events or streams of data. Service Fabric also enables applications that describe processing pipelines, where results must be reliable and passed on to the next processing stage without loss. These include transactional and financial systems, where data consistency and computation guarantees are essential.
* **Data gathering, processing and IoT**: Since Service Fabric handles large scale and has low latency through its stateful services, it is ideal for data processing on millions of devices where the data for the device and the computation are co-located.
We have seen several customers who have built IoT systems using Service Fabric including [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) and [Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Application design case studies
A number of case studies showing how Service Fabric is used to design applications are published on the [Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) and the [microservices solutions site](https://azure.microsoft.com/solutions/microservice-applications/)

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Design applications composed of stateless and stateful microservices
Building applications with Azure cloud service worker roles is an example of a stateless service. In contrast, stateful microservices maintain their authoritative state beyond the request and its response. This provides high availability and consistency of the state through simple APIs that provide transactional guarantees backed by replication. Service Fabric's stateful services democratize high availability, bringing it to all types of applications, not just databases and other data stores. This is a natural progression. Applications have already moved from using purely relational databases for high availability to NoSQL databases. Now the applications themselves can have their "hot" state and data managed within them for additional performance gains without sacrificing reliability, consistency, or availability.

When building applications consisting of microservices, you typically have a combination of stateless web apps (ASP.NET, Node.js, etc.) calling onto stateless and stateful business middle-tier services, all deployed into the same Service Fabric cluster using the Service Fabric deployment commands. Each of these services is independent with regard to scale, reliability, and resource usage, greatly improving agility in development and lifecycle management.

Stateful microservices simplify application designs because they remove the need for the additional queues and caches that have traditionally been required to address the availability and latency requirements of purely stateless applications. Since stateful services are naturally highly available and low latency, this means that there are fewer moving parts to manage in your application as a whole. The diagrams below illustrate the differences between designing an application that is stateless and one that is stateful. By taking advantage of the [reliable services](service-fabric-reliable-services-introduction.md) and [reliable actors](service-fabric-reliable-actors-introduction.md) programming models, stateful services reduce application complexity while achieving high throughput and low latency.

## <a name="an-application-built-using-stateless-services"></a>An application built using stateless services
![Application using stateless service][Image1]

## <a name="an-application-built-using-stateful-services"></a>An application built using stateful services
![Application using stateless service][Image2]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Next steps
* Get started building stateless and stateful services with the Service Fabric [reliable services](service-fabric-reliable-services-quick-start.md) and [reliable actors](service-fabric-reliable-actors-get-started.md) programming models.
* Learn more about [Patterns and scenarios](service-fabric-patterns-and-scenarios.md).
* Learn about [customer case studies](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
).
* Also see the following topics:
  * [Tell me about microservices](service-fabric-overview-microservices.md)
  * [Define and manage service state](service-fabric-concepts-state.md)
  * [Availability of Service Fabric services](service-fabric-availability-services.md)
  * [Scale Service Fabric services](service-fabric-concepts-scalability.md)
  * [Partition Service Fabric services](service-fabric-concepts-partitioning.md)

[Image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-scenarios/AppwithStatefulServices.jpg


