---
title: Create your first Azure microservices app on Linux using C#| Microsoft Docs
description: Create and deploy a Service Fabric application using C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
ms.openlocfilehash: 2c60b874e2e7bc476ec7f16b05e354fac34c739b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555530"
---
# <a name="create-your-first-azure-service-fabric-application"></a>Create your first Azure Service Fabric application
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
> 
> 

Service Fabric provides SDKs for building services on Linux in both .NET Core and Java. In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).

## <a name="prerequisites"></a>Prerequisites
Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md). If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).

## <a name="create-the-application"></a>Create the application
A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality. The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your first service and to add more later. Let's use Yeoman to create an application with a single service.

1. In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`
2. Name your application.
3. Choose the type of your first service and name it. For the purposes of this tutorial, we choose a Reliable Actor Service.
   
   ![Service Fabric Yeoman generator for C#][sf-yeoman]

> [!NOTE]
> For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).
> 
> 

## <a name="build-the-application"></a>Build the application
The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).

  ```sh
 cd myapp 
 ./build.sh 
  ```

## <a name="deploy-the-application"></a>Deploy the application
Once the application is built, you can deploy it to the local cluster using the Azure CLI.

1. Connect to the local Service Fabric cluster.
   
    ```sh
    azure servicefabric cluster connect
    ```
2. Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.
   
    ```bash
    ./install.sh
    ```
3. Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).
4. Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.

## <a name="start-the-test-client-and-perform-a-failover"></a>Start the test client and perform a failover
Actor projects do not do anything on their own. They require another service or client to send them messages. The actor template includes a simple test script that you can use to interact with the actor service.

1. Run the script using the watch utility to see the output of the actor service.
   
    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. In Service Fabric Explorer, locate node hosting the primary replica for the actor service. In the screenshot below, it is node 3.
   
    ![Finding the primary replica in Service Fabric Explorer][sfx-primary]
3. Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu. This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node. As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.

## <a name="adding-more-services-to-an-existing-application"></a>Adding more services to an existing application

To add another service to an application already created using `yo`, perform the following steps: 
1. Change directory to the root of the existing application.  For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.
2. Run `yo azuresfcsharp:AddService`

## <a name="next-steps"></a>Next steps
* [Learn more about Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interacting with Service Fabric clusters using the Azure CLI](service-fabric-azure-cli.md)
* Learn about [Service Fabric support options](service-fabric-support.md)

<!-- Images -->
[sf-yeoman]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png


