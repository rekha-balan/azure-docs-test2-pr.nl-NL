---
title: Learn about Azure Service Fabric | Microsoft Docs
description: An overview and getting started guide for Azure Service Fabric. Learn about Service Fabric and get started developing scalable, reliable, and easily managed applications composed of microservices.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/18/2017
ms.author: ryanwi
ms.openlocfilehash: 073f45ae32e0dfb2375149c4a17f9e832ed04618
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663075"
---
# <a name="so-you-want-to-learn-about-service-fabric"></a>So you want to learn about Service Fabric?
This primer provides a brief overview to Service Fabric, an introduction to the core concepts and terminology, a getting started guide, and an overview of each area of Service Fabric.  This primer does not contain a comprehensive content list, but does link to overview and getting started articles for every area of Service Fabric. 

## <a name="the-five-minute-overview"></a>The five-minute overview
Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices.  Service Fabric addresses the significant challenges in developing and managing cloud applications. By using Service Fabric, developers and administrators can avoid solving complex infrastructure problems.  Instead, you can focus on implementing mission-critical, demanding workloads knowing that they are scalable, reliable, and manageable. Service Fabric represents the next-generation middleware platform for building and managing these enterprise-class, Tier-1 cloud-scale applications.  

This short Channel9 video introduces Service Fabric and microservices: <center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="the-detailed-overview"></a>The detailed overview
Service Fabric enables you to build and manage scalable and reliable applications composed of microservices.  These microservices run at very high density on a shared pool of machines, which is referred to as a cluster. It provides a sophisticated runtime to build distributed, scalable, stateless and stateful microservices. It also provides comprehensive application management capabilities to provision, deploy, monitor, upgrade/patch, and delete deployed applications.  Read [Overview of Service Fabric](service-fabric-overview.md) to learn more.

Why a microservices design approach? All applications evolve over time. Successful applications evolve by being useful to people. How much do you know about your requirements today, and what will they be in the future? Sometimes, getting a simple app out the door as proof of concept is the driving factor (knowing that the application can be redesigned at a later time). On the other hand, when companies talk about building for the cloud there is the expectation of growth and usage. The issue is that growth and scale are unpredictable. Developers want to prototype quickly while knowing that the app can scale to react to unpredictable growth and usage.  [What are microservices?](service-fabric-overview-microservices.md) describes how the microservice design approach meets these challenges and how you can create microservices, which you can scale up or down, test, deploy, and manage independently.

Service Fabric offers a reliable and flexible platform that enables you to write and run many types of business applications and services.  You can also run any of your existing applications (written in any language).  These applications and microservices can be stateless or stateful, and they are resource-balanced across virtual machines to maximize efficiency. The unique architecture of Service Fabric enables you to perform near real-time data analysis, in-memory computation, parallel transactions, and event processing in your applications. You can easily [scale your applications](service-fabric-concepts-scalability.md) up or down (really in or out), depending on your changing resource requirements. Read [Application scenarios](service-fabric-application-scenarios.md) and [patterns and scenarios](service-fabric-patterns-and-scenarios.md) to learn about the categories of applications and services you can create as well as customer case studies.

This longer Microsoft Virtual Academy video describes the Service Fabric core concepts: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="get-started-and-create-your-first-app"></a>Get started and create your first app 
Using the Service Fabric SDKs and tools, you can develop apps in Windows, Linux, or MacOS environments and deploy those apps to clusters running on Windows or Linux.  The following guides will have you deploying an app within minutes.  After you've run your first application, download and run some of our [sample apps](http://aka.ms/servicefabricsamples). In particular start with the [Getting Started Samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)

### <a name="on-windows"></a>On Windows
The Service Fabric SDK includes an add-in for Visual Studio that provides templates and tools for creating, deploying, and debugging Service Fabric applications. These topics walk you through the process of creating your first application in Visual Studio and running it on your development computer.

[Set up your dev environment](service-fabric-get-started.md)
[Create your first app (C#)](service-fabric-create-your-first-application-in-visual-studio.md)

#### <a name="practical-hands-on-labs"></a>Practical hands on labs
Try this extensive [hands-on-lab Part 1](https://msdnshared.blob.core.windows.net/media/2016/07/SF-Lab-Part-I.docx) to get familiar with the end-to-end development flow for Service Fabric.  Learn to create a stateless service, configure monitoring and health reports, and perform an application upgrade. After Part 1, go through [hands-on-lab Part 2](http://aka.ms/sflab2), which takes you through stateful services.

The following Channel9 video walks you through the process of creating a C# app in Visual Studio:  
<center><a target="_blank" href="https://channel9.msdn.com/Blogs/Azure/Creating-your-first-Service-Fabric-application-in-Visual-Studio">  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/first-app-vid.png" WIDTH="360" HEIGHT="244">  
</a></center>

### <a name="on-linux"></a>On Linux
Service Fabric provides SDKs for building services on Linux in both .NET Core and Java. These topics walk you through the process of creating your first Java or C# application on Linux and running it on your development computer: [Set up your dev environment](service-fabric-get-started-linux.md), [Create your first app (Java)](service-fabric-create-your-first-linux-application-with-java.md), and [Create your first app (C#)](service-fabric-create-your-first-linux-application-with-csharp.md).

The following Microsoft Virtual Academy video walks you through the process of creating a Java app on Linux:  
<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/LinuxVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

### <a name="on-macos"></a>On MacOS
You can build Service Fabric applications on MacOS X to run on Linux clusters. These articles describe how to set up your Mac for development and walk you through creating a Java application on MacOS and running it on an Ubuntu virtual machine: [Set up your dev environment](service-fabric-get-started-mac.md) and [Create your first app (Java)](service-fabric-create-your-first-linux-application-with-java.md).

## <a name="core-concepts"></a>Core concepts
[Service Fabric terminology](service-fabric-technical-overview.md), [Application model](service-fabric-application-model.md), and [Supported programming models](service-fabric-choose-framework.md) provide more concepts and descriptions, but here are the basics.

<table><tr><th>Core concepts</th><th>Design time</th><th>Run time</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-app-type-service-type-app-package-and-manifest-service-package-and-manifest"></a>Design time: app type, service type, app package and manifest, service package and manifest
An application type is the name/version assigned to a collection of service types. Defined in an ApplicationManifest.xml file, embedded in an application package directory, which is then copied to the Service Fabric cluster's image store. You can then create a named application from this application type, which then runs within the cluster. 

A service type is the name/version assigned to a service's code packages, data packages, and configuration packages. Defined in a ServiceManifest.xml file, embedded in a service package directory and the service package directory is then referenced by an application package's ApplicationManifest.xml file. Within the cluster, after creating a named application, you can create a named service from one of the application type's service types. A service type is described by it's ServiceManifest.xml file.  It's composed of executable code service configuration settings, which are loaded at run time, and static data that is consumed by the service.

![Service Fabric application types and service types][cluster-imagestore-apptypes]

The application package is a disk directory containing the application type's ApplicationManifest.xml file, which references the service packages for each service type that makes up the application type. For example, an application package for an email application type could contain references to a queue service package, a frontend service package, and a database service package. The files in the application package directory are copied to the Service Fabric cluster's image store. 

A service package is a disk directory containing the service type's ServiceManifest.xml file, which references the code, static data, and configuration packages for the service type. The files in the service package directory are referenced by the application type's ApplicationManifest.xml file. For example, a service package could refer to the code, static data, and configuration packages that make up a database service.

### <a name="run-time-clusters-and-nodes-named-apps-named-services-partitions-and-replicas"></a>Run time: clusters and nodes, named apps, named services, partitions, and replicas
A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed. Clusters can scale to thousands of machines.

A machine or VM that is part of a cluster is called a node. Each node is assigned a node name (a string). Nodes have characteristics such as placement properties. Each machine or VM has an auto-start Windows service, FabricHost.exe, which starts running upon boot and then starts two executables: Fabric.exe and FabricGateway.exe. These two executables make up the node. For development or testing scenarios, you can host multiple nodes on a single machine or VM by running multiple instances of Fabric.exe and FabricGateway.exe.

A named application is a collection of named services that performs a certain function or functions. A service performs a complete and standalone function (it can start and run independently of other services) and is composed of code, configuration, and data. After an application package is copied to the image store, you create an instance of the application within the cluster by specifying the application package's application type (using its name/version). Each application type instance is assigned a URI name that looks like *fabric:/MyNamedApp*. Within a cluster, you can create multiple named applications from a single application type. You can also create named applications from different application types. Each named application is managed and versioned independently.

After creating a named application, you can create an instance of one of its service types (a named service) within the cluster by specifying the service type (using its name/version). Each service type instance is assigned a URI name scoped under its named application's URI. For example, if you create a "MyDatabase" named service within a "MyNamedApp" named application, the URI looks like: *fabric:/MyNamedApp/MyDatabase*. Within a named application, you can create one or more named services. Each named service can have its own partition scheme and instance/replica counts. 

There are two types of services: stateless and stateful.  Stateless services store persistent state in an external storage service such as Azure Storage, Azure SQL Database, or Azure DocumentDB. Use a stateless service when the service has no persistent storage at all. A stateful service uses Service Fabric to manage your service's state via its Reliable Collections or Reliable Actors programming models.  

When creating a named service, you specify a partition scheme. Services with large amounts of state split the data across partitions.  Each partition is responsible for a portion of the complete state of the service, which is spread across the cluster's nodes.  Within a partition, stateless named services have instances while stateful named services have replicas. Usually, stateless named services only ever have one partition since they have no internal state. Stateful named services maintain their state within replicas and each partition has its own replica set.  Read and write operations are performed at one replica (called the Primary). Changes to state from write operations are replicated to multiple other replicas (called Active Secondaries).  

The following diagram shows the relationship between applications and service instances, partitions, and replicas.

![Partitions and replicas within a service][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Partitioning, scaling, and availability
[Partitioning](service-fabric-concepts-partitioning.md) is not unique to Service Fabric. A well known form of partitioning is data partitioning, or sharding. Stateful services with large amounts of state split the data across partitions.  Each partition is responsible for a portion of the complete state of the service. 

The replicas of each partition are spread across the cluster's nodes, which allows your named service's state to [scale](service-fabric-concepts-scalability.md). As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes to make efficient use of hardware resources. If you add new nodes to the cluster, Service Fabric will rebalance the partition replicas across the increased number of nodes.  Overall application performance improves and contention for access to memory decreases.  If the nodes in the cluster are not being used efficiently, you can decrease the number of nodes in the cluster.  Service Fabric again rebalances the partition replicas across the decreased number of nodes to make better use of the hardware on each node.

Within a partition, stateless named services have instances while stateful named services have replicas. Usually, stateless named services only ever have one partition since they have no internal state. The partition instances provide for [availability](service-fabric-availability-services.md).  If one instance fails, other instances continue to operate normally and then Service Fabric creates a new instance. Stateful named services maintain their state within replicas and each partition has its own replica set.  Read and write operations are performed at one replica (called the Primary). Changes to state from write operations are replicated to multiple other replicas (called Active Secondaries).  Should a replica fail, Service Fabric builds a new replica from the existing replicas.

## <a name="supported-programming-models"></a>Supported programming models
Service Fabric offers multiple ways to write and manage your services. Services can choose to use the Service Fabric APIs to take full advantage of the platform's features and application frameworks.  Or, services can be any compiled executable program written in any language and hosted on a Service Fabric cluster. For more information, see [Supported programming models](service-fabric-choose-framework.md).

### <a name="guest-executables"></a>Guest executables
A [guest executable](service-fabric-deploy-existing-app.md) is an existing, arbitrary executable (written in any language) hosted on a Service Fabric cluster alongside other services. Guest executables do not integrate directly with Service Fabric APIs, however.  Guest executables do not benefit from the full set of features the platform offers, such as custom health and load reporting, service endpoint registration, and stateful compute.

### <a name="containers"></a>Containers
By default, Service Fabric deploys and activates services as processes. Service Fabric can also deploy services in [container images](service-fabric-containers-overview.md). Importantly, you can mix services in processes and services in containers in the same application.  Service Fabric currently supports deployment of Docker containers on Linux and Windows Server containers on Windows Server 2016. In the Service Fabric application model, a container represents an application host in which multiple service replicas are placed.  You can deploy existing applications, stateless services, or stateful services in a container using Service Fabric.  

### <a name="reliable-services"></a>Reliable Services
[Reliable Services](service-fabric-reliable-services-introduction.md) is a light-weight framework for writing services that integrate with the Service Fabric platform and benefit from the full set of platform features. Reliable Services can be stateless (similar to most service platforms, such as web servers or Worker Roles in Azure Cloud Services). State is persisted in an external solution, such as Azure DB or Azure Table Storage. Reliable Services can also be stateful, where state is persisted directly in the service itself using Reliable Collections. State is made [highly available](service-fabric-availability-services.md) through replication and distributed through [partitioning](service-fabric-concepts-partitioning.md), all managed automatically by Service Fabric.

### <a name="reliable-actors"></a>Reliable Actors
Built on top of Reliable Services, the [Reliable Actor](service-fabric-reliable-actors-introduction.md) framework is an application framework that implements the Virtual Actor pattern, based on the actor design pattern. The Reliable Actor framework uses independent units of compute and state with single-threaded execution called actors. The Reliable Actor framework provides built in communication for actors and pre-set state persistence and scale-out configurations.

## <a name="app-lifecycle"></a>App lifecycle
As with other platforms, an application on Service Fabric usually goes through the following phases: design, development, testing, deployment, upgrade, maintenance, and removal. Service Fabric provides first-class support for the full application lifecycle of cloud applications, from development through deployment, daily management, and maintenance to eventual decommissioning. The service model enables several different roles to participate independently in the application lifecycle. [Service Fabric application lifecycle](service-fabric-application-lifecycle.md) provides an overview of the APIs and how they are used by the different roles throughout the phases of the Service Fabric application lifecycle.  

The entire app lifecycle can be managed using [PowerShell cmdlets](/powershell/module/ServiceFabric/), [C# APIs](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [Java APIs](/java/api/system.fabric._application_management_client), and [REST APIs](/rest/api/servicefabric/). You can also set up continuous integration/continuous deployment pipelines using tools such as [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) or [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md)

The following Microsoft Virtual Academy video describes how to manage your application lifecycle: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-apps-and-services"></a>Test apps and services
To create truly cloud-scale services, it is critical to verify that your apps aps and services can withstand real-world failures.  The Fault Analysis Service is designed for testing services that are built on Service Fabric. With the [Fault Analysis Service](service-fabric-testability-overview.md) you can induce meaningful faults and run complete test scenarios against your applications. These faults and scenarios exercise and validate the numerous states and transitions that a service will experience throughout its lifetime, all in a controlled, safe, and consistent manner.

[Actions](service-fabric-testability-actions.md) target a service for testing using individual faults. A service developer can use these as building blocks to write complicated scenarios. Examples of simulated faults are:

* Restart a node to simulate any number of situations where a machine or VM is rebooted.
* Move a replica of your stateful service to simulate load balancing, failover, or application upgrade.
* Invoke quorum loss on a stateful service to create a situation where write operations can't proceed because there aren't enough "back-up" or "secondary" replicas to accept new data.
* Invoke data loss on a stateful service to create a situation where all in-memory state is completely wiped out.

[Scenarios](service-fabric-testability-scenarios.md) are complex operations composed of one or more actions. The Fault Analysis Service provides two built-in complete scenarios:

* [Chaos scenario](service-fabric-controlled-chaos.md)- simulates continuous, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.
* [Failover scenario](service-fabric-testability-scenarios.md#failover-test)- a version of the chaos test scenario that targets a specific service partition while leaving other services unaffected.

## <a name="clusters"></a>Clusters
A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed. Clusters can scale to thousands of machines. A machine or VM that is part of a cluster is called a cluster node. Each node is assigned a node name (a string). Nodes have characteristics such as placement properties. Each machine or VM has an auto-start service, FabricHost.exe, which starts running upon boot and then starts two executables: Fabric.exe and FabricGateway.exe. These two executables make up the node. For testing scenarios, you can host multiple nodes on a single machine or VM by running multiple instances of Fabric.exe and FabricGateway.exe.

Service Fabric clusters can be created on any virtual machines or computers running Windows Server or Linux. You are able to deploy and run Service Fabric applications in any environment where you have a set of Windows Server or Linux computers that are interconnected: on-premises, on Microsoft Azure, or on any cloud provider.

The following Microsoft Virtual Academy video describes Service Fabric clusters: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Clusters on Azure
Running Service Fabric clusters on Azure provide integration with other Azure features and services, which makes operations and management of the cluster easier and more reliable.  A cluster is an Azure Resource Manager resource, so you can model clusters like any other resources in Azure. Resource Manager also provides easy management of all resources used by the cluster as a single unit.  Clusters on Azure are integrated with Azure diagnostics and Log Analytics.  Cluster nodetypes are [virtual machine scale sets](/azure/virtual-machine-scale-sets/index), so autoscaling functionality is built-in.

You can create a cluster on Azure through the [Azure portal](service-fabric-cluster-creation-via-portal.md), from a [template](service-fabric-cluster-creation-via-arm.md), or from [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows. The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).  You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework. In addition, the preview also supports orchestrating Docker containers. Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks. For more information, read [Service Fabric on Linux](service-fabric-linux-overview.md).

Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not on Linux. To learn more, read [Differences between Service Fabric on Linux and Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Standalone clusters
Service Fabric provides an install package for you to create standalone Service Fabric clusters on-premises or on any cloud provider.  Standalone clusters give you the freedom to host a cluster wherever you want.  If your data is subject to compliance or regulatory constraints, or you want to keep your data local, you can host your own cluster and apps.  Service Fabric apps can run in multiple hosting environments with no changes, so your knowledge of building apps carries over from one hosting environment to another. 

[Create your first Service Fabric standalone cluster](service-fabric-get-started-standalone-cluster.md)

Linux standalone clusters are not yet supported.

### <a name="cluster-security"></a>Cluster security
Clusters must be secured to prevent unauthorized users from connecting to your cluster, especially when it has production workloads running on it. Although it is possible to create an unsecured cluster, doing so allows anonymous users to connect to it if management endpoints are exposed to the public internet.  It is not possible to later enable security on an unsecured cluster: cluster security is enabled at cluster creation time.

The cluster security scenarios are:
* Node-to-node security
* Client-to-node security
* Role-based access control (RBAC)

For more information, read [Secure a cluster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Scaling
If you add new nodes to the cluster, Service Fabric rebalances the partition replicas and instances across the increased number of nodes.  Overall application performance improves and contention for access to memory decreases.  If the nodes in the cluster are not being used efficiently, you can decrease the number of nodes in the cluster.  Service Fabric again rebalances the partition replicas and instances across the decreased number of nodes to make better use of the hardware on each node.  You can scale clusters on Azure either [manually](service-fabric-cluster-scale-up-down.md) or [programmatically](service-fabric-cluster-programmatic-scaling.md).  Standalone clusters can be scaled [manually](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Cluster upgrades
Periodically, new versions of the Service Fabric runtime are released.  Perform runtime, or fabric, upgrades on your cluster so that you are always running a [supported version](service-fabric-support.md).  In addition to fabric upgrades, you can also update cluster configuration such as certificates or application ports.

A Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.  Microsoft is responsible for patching the underlying OS and performing fabric upgrades on your cluster.  You can set your cluster to receive automatic fabric upgrades, when Microsoft releases a new version, or choose to select a supported fabric version that you want.  Fabric and configuration upgrades can be set through the Azure portal or through Resource Manager.  For more information, read [Upgrade a Service Fabric cluster](service-fabric-cluster-upgrade.md).  

A standalone cluster is a resource that you entirely own.  You are responsible for patching the underlying OS and initiating fabric upgrades.  If your cluster can connect to [https://www.microsoft.com/download](https://www.microsoft.com/download), you can set your cluster to automatically download and provision the new Service Fabric runtime package.  You would then initiate the upgrade.  If your cluster can't access [https://www.microsoft.com/download](https://www.microsoft.com/download), you can manually download the new runtime package from an internet connected machine and then initiate the upgrade.  For more information, read [Upgrade a standalone Service Fabric cluster](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Health monitoring
Service Fabric introduces a [health model](service-fabric-health-introduction.md) designed to flag unhealthy cluster and application conditions on specific entities (such as cluster nodes and service replicas). The health model uses health reporters (system components and watchdogs). The goal is easy and fast diagnosis and repair. Service writers need to think upfront about health and how to [design health reporting](service-fabric-report-health.md#design-health-reporting). Any condition that can impact health should be reported on, especially if it can help flag problems close to the root. The health information can save time and effort on debugging and investigation once the service is up and running at scale in production.

The Service Fabric reporters monitor identified conditions of interest. They report on those conditions based on their local view. The [health store](service-fabric-health-introduction.md#health-store) aggregates health data sent by all reporters to determine whether entities are globally healthy. The model is intended to be rich, flexible, and easy to use. The quality of the health reports determines the accuracy of the health view of the cluster. False positives that wrongly show unhealthy issues can negatively impact upgrades or other services that use health data. Examples of such services are repair services and alerting mechanisms. Therefore, some thought is needed to provide reports that capture conditions of interest in the best possible way.

Reporting can be done from:
* The monitored Service Fabric service replica or instance.
* Internal watchdogs deployed as a Service Fabric service (for example, a Service Fabric stateless service that monitors conditions and issues reports). The watchdogs can be deployed an all nodes or can be affinitized to the monitored service.
* Internal watchdogs that run on the Service Fabric nodes but are not implemented as Service Fabric services.
* External watchdogs that probe the resource from outside the Service Fabric cluster (for example, monitoring service like Gomez).

Out of the box, Service Fabric components report health on all entities in the cluster.  [System health reports](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) provide visibility into cluster and application functionality and flag issues through health. For applications and services, system health reports verify that entities are implemented and are behaving correctly from the perspective of the Service Fabric runtime. The reports do not provide any health monitoring of the business logic of the service or detect hung processes. To add health information specific to your service's logic, [implement custom health reporting](service-fabric-report-health.md) in your services.

Service Fabric provides multiple ways to [view health reports](service-fabric-view-entities-aggregated-health.md) aggregated in the health store:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools/
* Health queries (through [PowerShell](/powershell/module/ServiceFabric/), the [C# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) and [Java FabricClient APIs](/java/api/system.fabric._health_client), or [REST APIs](/rest/api/servicefabric)).
* General queries that return a list of entities that have health as one of the properties (through PowerShell, the API, or REST).

The following Microsoft Virtual Academy video describes the Service Fabric health model and how it's used: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Next steps
* Learn how to create a [cluster in Azure](service-fabric-cluster-creation-via-portal.md) or a [standalone cluster on Windows](service-fabric-cluster-creation-for-windows-server.md).
* Try creating a service using the [Reliable Services](service-fabric-reliable-services-quick-start.md) or [Reliable Actors](service-fabric-reliable-actors-get-started.md) programming models.
* Learn how to [migrate from Cloud Services](service-fabric-cloud-services-migration-differences.md).
* Learn to [monitor and diagnose services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Learn to [test your apps and services](service-fabric-testability-overview.md).
* Learn to [manage and orchestrate cluster resources](service-fabric-cluster-resource-manager-introduction.md).
* Look through the [Service Fabric samples](http://aka.ms/servicefabricsamples).
* Learn about [Service Fabric support options](service-fabric-support.md).
* Read the [team blog](https://blogs.msdn.microsoft.com/azureservicefabric/) for articles and announcements.


[cluster-application-instances]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png












