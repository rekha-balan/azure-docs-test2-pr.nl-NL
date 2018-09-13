---
title: Service Fabric project creation next steps | Microsoft Docs
description: This article contains links to a set of core development tasks for Service Fabric
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/28/2017
ms.author: seanmck
ms.openlocfilehash: 8208a1a41388a8cc36f3702bd0cad2bb82e16403
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563113"
---
# <a name="your-service-fabric-application-and-next-steps"></a>Your Service Fabric application and next steps
Your Azure Service Fabric application has been created. This article describes the makeup of your project and some potential next steps.

## <a name="your-application"></a>Your application
Every new application includes an application project. There may be one or two additional projects, depending on the type of service chosen.

### <a name="the-application-project"></a>The application project
The application project consists of:

* A set of references to the services that make up your application.
* Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.
* Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.
* A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.
* The application manifest, which describes the application. You can find the manifest under the ApplicationPackageRoot folder.

### <a name="stateless-service"></a>Stateless service
When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`. The service increments a local variable in a counter.

### <a name="stateful-service"></a>Stateful service
When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`. The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.

### <a name="actor-service"></a>Actor service
When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.

The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state. The interface project provides an interface that other services can use to invoke the actor.

### <a name="stateless-web-api"></a>Stateless Web API
The stateless Web API project provides a basic web service that you can use to open your application to external clients. For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET core
The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Guest executables and guest containers

A Service Fabric 'guest' is a service that is not built with the platform's programming models. You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md). In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project. Visual Studio will not create a new service project because the code already exists elsewhere. If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.

## <a name="next-steps"></a>Next steps
### <a name="create-an-azure-cluster"></a>Create an Azure cluster
The Service Fabric SDK provides a local cluster for development and testing. To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].

### <a name="publish-your-application-to-azure"></a>Publish your application to Azure
You can publish your application directly from Visual Studio to an Azure cluster. To learn how, see [Publishing your application to Azure][publish-app-to-azure].

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a>Use Service Fabric Explorer to visualize your cluster
Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout. To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Version and upgrade your services
Service Fabric enables independent versioning and upgrading of independent services in an application. To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Configure continuous integration with Visual Studio Team Services
To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
