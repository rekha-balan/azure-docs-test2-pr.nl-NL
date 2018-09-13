---
title: Azure Service Fabric on Linux | Microsoft Docs
description: Service Fabric clusters support Linux and Java, which means you'll be able to deploy and host Service Fabric applications written in Java and C# on Linux.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: SubramaR
ms.openlocfilehash: 62d7e0088c66a538dff7f3b99882ebef4949211b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554620"
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="3aa2c-103">Service Fabric on Linux</span><span class="sxs-lookup"><span data-stu-id="3aa2c-103">Service Fabric on Linux</span></span>
<span data-ttu-id="3aa2c-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="3aa2c-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="3aa2c-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="3aa2c-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="3aa2c-107">In addition, the preview also supports orchestrating Docker containers.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="3aa2c-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="3aa2c-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span><span class="sxs-lookup"><span data-stu-id="3aa2c-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="3aa2c-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="3aa2c-111">Supported operating systems and programming languages</span><span class="sxs-lookup"><span data-stu-id="3aa2c-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="3aa2c-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="3aa2c-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="3aa2c-114">Reliable Collections are not supported in Linux yet.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="3aa2c-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="3aa2c-116">Supported tooling</span><span class="sxs-lookup"><span data-stu-id="3aa2c-116">Supported tooling</span></span>
<span data-ttu-id="3aa2c-117">The preview supports interaction with the cluster through Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-117">The preview supports interaction with the cluster through Azure CLI.</span></span> <span data-ttu-id="3aa2c-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="3aa2c-119">The OSX integration uses a Linux VM under the hood via vagrant.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="3aa2c-120">For C# developers, integration with Yeoman is provided to generate application templates.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aa2c-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="3aa2c-121">Next steps</span></span>
1. <span data-ttu-id="3aa2c-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks.</span><span class="sxs-lookup"><span data-stu-id="3aa2c-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks.</span></span>
2. [<span data-ttu-id="3aa2c-123">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="3aa2c-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
3. [<span data-ttu-id="3aa2c-124">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="3aa2c-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
4. [<span data-ttu-id="3aa2c-125">Create your first Service Fabric Java application on Linux</span><span class="sxs-lookup"><span data-stu-id="3aa2c-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
5. [<span data-ttu-id="3aa2c-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span><span class="sxs-lookup"><span data-stu-id="3aa2c-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
6. [<span data-ttu-id="3aa2c-127">Service Fabric Windows/Linux differences</span><span class="sxs-lookup"><span data-stu-id="3aa2c-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
