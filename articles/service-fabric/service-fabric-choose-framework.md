---
title: Service Fabric programming model overview | Microsoft Docs
description: 'Service Fabric offers two frameworks for building services: the actor framework and the services framework. They offer distinct trade-offs in simplicity and control.'
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/28/2017
ms.author: seanmck
ms.openlocfilehash: 25c63326ccf20b3b55ead28c5b9214f34d53d3ee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552594"
---
# <a name="service-fabric-programming-model-overview"></a>Service Fabric programming model overview
Service Fabric offers multiple ways to write and manage your services. Services can choose to use the Service Fabric APIs to take full advantage of the platform's features and application frameworks, or services can simply be any compiled executable program written in any language and simply hosted on a Service Fabric cluster.

## <a name="guest-executable"></a>Guest Executable
A guest executable is an arbitrary executable, written in any language, so you can take your existing applications and host them on a Service Fabric cluster. A guest executable can be packaged in an application and hosted alongside other services. Service Fabric handles orchestration and simple execution management of the executable, ensuring it stays up and running according to the service description. However, because guest executables do not integrate directly with Service Fabric APIs, they do not benefit from the full set of features the platform offers, such as custom health and load reporting, service endpoint registration, and stateful compute.

Get started with guest executables by deploying your first [guest executable application](service-fabric-deploy-existing-app.md).

## <a name="reliable-services"></a>Reliable Services
Reliable Services is a light-weight framework for writing services that integrate with the Service Fabric platform and benefit from the full set of platform features. Reliable Services provide a minimal set of APIs that allow the Service Fabric runtime to manage the lifecycle of your services and that allow your services to interact with the runtime. The application framework is minimal, giving you full control over design and implementation choices, and can be used to host any other application framework, such as ASP.NET MVC or Web API.

Reliable Services can be stateless, similar to most service platforms, such as web servers or Worker Roles in Azure Cloud Services, in which each instance of the service is created equal and state is persisted in an external solution, such as Azure DB or Azure Table Storage.

Reliable Services can also be stateful, exclusive to Service Fabric, where state is persisted directly in the service itself using Reliable Collections. State is made highly-available through replication and distributed through partitioning, all managed automatically by Service Fabric.

[Learn more about Reliable Services](service-fabric-reliable-services-introduction.md) or get started by [writing your first Reliable Service](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Built on top of Reliable Services, the Reliable Actor framework is an application framework that implements the Virtual Actor pattern, based on the actor design pattern. The Reliable Actor framework uses independent units of compute and state with single-threaded execution called actors. The Reliable Actor framework provides built-in communication for actors and pre-set state persistence and scale-out configurations.

As Reliable Actors itself is an application framework built on Reliable Services, it is fully integrated with the Service Fabric platform and benefits from the full set of features offered by the platform.

## <a name="next-steps"></a>Next steps
[Learn more about Reliable Actors](service-fabric-reliable-actors-introduction.md) or get started by [writing your first Reliable Actor service](service-fabric-reliable-actors-get-started.md)
[Learn more about Containerizing your services in Windows or Linux](service-fabric-deploy-container.md)
