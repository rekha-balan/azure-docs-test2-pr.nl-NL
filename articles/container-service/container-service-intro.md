---
title: Docker container hosting in Azure cloud | Microsoft Docs
description: Azure Container Service provides a way to simplify the creation, configuration, and management of a cluster of virtual machines that are preconfigured to run containerized applications.
services: container-service
documentationcenter: ''
author: rgardler
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: 52da4163-1182-4b2e-be00-4951e5c1da16
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1e8e1af45b5798d58e53d34a2aaac0b8d3c75466
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554921"
---
# <a name="introduction-to-docker-container-hosting-solutions-with-azure-container-service"></a><span data-ttu-id="86bb6-104">Introduction to Docker container hosting solutions with Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="86bb6-104">Introduction to Docker container hosting solutions with Azure Container Service</span></span> 
<span data-ttu-id="86bb6-105">Azure Container Service makes it simpler for you to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span><span class="sxs-lookup"><span data-stu-id="86bb6-105">Azure Container Service makes it simpler for you to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="86bb6-106">It uses an optimized configuration of popular open-source scheduling and orchestration tools.</span><span class="sxs-lookup"><span data-stu-id="86bb6-106">It uses an optimized configuration of popular open-source scheduling and orchestration tools.</span></span> <span data-ttu-id="86bb6-107">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86bb6-107">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

![Azure Container Service provides a means to manage containerized applications on multiple hosts on Azure.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/acs-intro/acs-cluster-new.png)

<span data-ttu-id="86bb6-109">Azure Container Service leverages the Docker container format to ensure that your application containers are fully portable.</span><span class="sxs-lookup"><span data-stu-id="86bb6-109">Azure Container Service leverages the Docker container format to ensure that your application containers are fully portable.</span></span> <span data-ttu-id="86bb6-110">It also supports your choice of Marathon and DC/OS, Docker Swarm, or Kubernetes so that you can scale these applications to thousands of containers, or even tens of thousands.</span><span class="sxs-lookup"><span data-stu-id="86bb6-110">It also supports your choice of Marathon and DC/OS, Docker Swarm, or Kubernetes so that you can scale these applications to thousands of containers, or even tens of thousands.</span></span>

<span data-ttu-id="86bb6-111">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability--including portability at the orchestration layers.</span><span class="sxs-lookup"><span data-stu-id="86bb6-111">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability--including portability at the orchestration layers.</span></span>

## <a name="using-azure-container-service"></a><span data-ttu-id="86bb6-112">Using Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="86bb6-112">Using Azure Container Service</span></span>
<span data-ttu-id="86bb6-113">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span><span class="sxs-lookup"><span data-stu-id="86bb6-113">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="86bb6-114">To this end, we expose the standard API endpoints for your chosen orchestrator (DC/OS, Docker Swarm, or Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="86bb6-114">To this end, we expose the standard API endpoints for your chosen orchestrator (DC/OS, Docker Swarm, or Kubernetes).</span></span> <span data-ttu-id="86bb6-115">By using these endpoints, you can leverage any software that is capable of talking to those endpoints.</span><span class="sxs-lookup"><span data-stu-id="86bb6-115">By using these endpoints, you can leverage any software that is capable of talking to those endpoints.</span></span> <span data-ttu-id="86bb6-116">For example, in the case of the Docker Swarm endpoint, you might choose to use the Docker command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="86bb6-116">For example, in the case of the Docker Swarm endpoint, you might choose to use the Docker command-line interface (CLI).</span></span> <span data-ttu-id="86bb6-117">For DC/OS, you might choose the DCOS CLI.</span><span class="sxs-lookup"><span data-stu-id="86bb6-117">For DC/OS, you might choose the DCOS CLI.</span></span> <span data-ttu-id="86bb6-118">For Kubernetes, you might choose `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="86bb6-118">For Kubernetes, you might choose `kubectl`.</span></span>

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a><span data-ttu-id="86bb6-119">Creating a Docker cluster by using Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="86bb6-119">Creating a Docker cluster by using Azure Container Service</span></span>
<span data-ttu-id="86bb6-120">To begin using Azure Container Service, you deploy an Azure Container Service cluster via the portal (search the Marketplace for **Azure Container Service**), by using an Azure Resource Manager template ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), or [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), or with the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span><span class="sxs-lookup"><span data-stu-id="86bb6-120">To begin using Azure Container Service, you deploy an Azure Container Service cluster via the portal (search the Marketplace for **Azure Container Service**), by using an Azure Resource Manager template ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), or [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), or with the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span></span> <span data-ttu-id="86bb6-121">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="86bb6-121">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span></span> <span data-ttu-id="86bb6-122">For more information, see [Deploy an Azure Container Service cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="86bb6-122">For more information, see [Deploy an Azure Container Service cluster](container-service-deployment.md).</span></span>

## <a name="deploying-an-application"></a><span data-ttu-id="86bb6-123">Deploying an application</span><span class="sxs-lookup"><span data-stu-id="86bb6-123">Deploying an application</span></span>
<span data-ttu-id="86bb6-124">Azure Container Service provides a choice of Docker Swarm, DC/OS, or Kubernetes for orchestration.</span><span class="sxs-lookup"><span data-stu-id="86bb6-124">Azure Container Service provides a choice of Docker Swarm, DC/OS, or Kubernetes for orchestration.</span></span> <span data-ttu-id="86bb6-125">How you deploy your application depends on your choice of orchestrator.</span><span class="sxs-lookup"><span data-stu-id="86bb6-125">How you deploy your application depends on your choice of orchestrator.</span></span>

### <a name="using-dcos"></a><span data-ttu-id="86bb6-126">Using DC/OS</span><span class="sxs-lookup"><span data-stu-id="86bb6-126">Using DC/OS</span></span>
<span data-ttu-id="86bb6-127">DC/OS is a distributed operating system based on the Apache Mesos distributed systems kernel.</span><span class="sxs-lookup"><span data-stu-id="86bb6-127">DC/OS is a distributed operating system based on the Apache Mesos distributed systems kernel.</span></span> <span data-ttu-id="86bb6-128">Apache Mesos is housed at the Apache Software Foundation and lists some of the [biggest names in IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) as users and contributors.</span><span class="sxs-lookup"><span data-stu-id="86bb6-128">Apache Mesos is housed at the Apache Software Foundation and lists some of the [biggest names in IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) as users and contributors.</span></span>

![Azure Container Service configured for DC/OS showing agents and masters.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/acs-intro/dcos.png)

<span data-ttu-id="86bb6-130">DC/OS and Apache Mesos include an impressive feature set:</span><span class="sxs-lookup"><span data-stu-id="86bb6-130">DC/OS and Apache Mesos include an impressive feature set:</span></span>

* <span data-ttu-id="86bb6-131">Proven scalability</span><span class="sxs-lookup"><span data-stu-id="86bb6-131">Proven scalability</span></span>
* <span data-ttu-id="86bb6-132">Fault-tolerant replicated master and slaves using Apache ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="86bb6-132">Fault-tolerant replicated master and slaves using Apache ZooKeeper</span></span>
* <span data-ttu-id="86bb6-133">Support for Docker-formatted containers</span><span class="sxs-lookup"><span data-stu-id="86bb6-133">Support for Docker-formatted containers</span></span>
* <span data-ttu-id="86bb6-134">Native isolation between tasks with Linux containers</span><span class="sxs-lookup"><span data-stu-id="86bb6-134">Native isolation between tasks with Linux containers</span></span>
* <span data-ttu-id="86bb6-135">Multiresource scheduling (memory, CPU, disk, and ports)</span><span class="sxs-lookup"><span data-stu-id="86bb6-135">Multiresource scheduling (memory, CPU, disk, and ports)</span></span>
* <span data-ttu-id="86bb6-136">Java, Python, and C++ APIs for developing new parallel applications</span><span class="sxs-lookup"><span data-stu-id="86bb6-136">Java, Python, and C++ APIs for developing new parallel applications</span></span>
* <span data-ttu-id="86bb6-137">A web UI for viewing cluster state</span><span class="sxs-lookup"><span data-stu-id="86bb6-137">A web UI for viewing cluster state</span></span>

<span data-ttu-id="86bb6-138">By default, DC/OS running on Azure Container Service includes the Marathon orchestration platform for scheduling workloads.</span><span class="sxs-lookup"><span data-stu-id="86bb6-138">By default, DC/OS running on Azure Container Service includes the Marathon orchestration platform for scheduling workloads.</span></span> <span data-ttu-id="86bb6-139">However, included with the DC/OS deployment of ACS is the Mesosphere Universe of services that can be added to your service.</span><span class="sxs-lookup"><span data-stu-id="86bb6-139">However, included with the DC/OS deployment of ACS is the Mesosphere Universe of services that can be added to your service.</span></span> <span data-ttu-id="86bb6-140">Services in the Universe include Spark, Hadoop, Cassandra, and much more.</span><span class="sxs-lookup"><span data-stu-id="86bb6-140">Services in the Universe include Spark, Hadoop, Cassandra, and much more.</span></span>

![DC/OS Universe in Azure Container Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/dcos/universe.png)

#### <a name="using-marathon"></a><span data-ttu-id="86bb6-142">Using Marathon</span><span class="sxs-lookup"><span data-stu-id="86bb6-142">Using Marathon</span></span>
<span data-ttu-id="86bb6-143">Marathon is a cluster-wide init and control system for services in cgroups--or, in the case of Azure Container Service, Docker-formatted containers.</span><span class="sxs-lookup"><span data-stu-id="86bb6-143">Marathon is a cluster-wide init and control system for services in cgroups--or, in the case of Azure Container Service, Docker-formatted containers.</span></span> <span data-ttu-id="86bb6-144">Marathon provides a web UI from which you can deploy your applications.</span><span class="sxs-lookup"><span data-stu-id="86bb6-144">Marathon provides a web UI from which you can deploy your applications.</span></span> <span data-ttu-id="86bb6-145">You can access this at a URL that looks something like `http://DNS_PREFIX.REGION.cloudapp.azure.com` where DNS\_PREFIX and REGION are both defined at deployment time.</span><span class="sxs-lookup"><span data-stu-id="86bb6-145">You can access this at a URL that looks something like `http://DNS_PREFIX.REGION.cloudapp.azure.com` where DNS\_PREFIX and REGION are both defined at deployment time.</span></span> <span data-ttu-id="86bb6-146">Of course, you can also provide your own DNS name.</span><span class="sxs-lookup"><span data-stu-id="86bb6-146">Of course, you can also provide your own DNS name.</span></span> <span data-ttu-id="86bb6-147">For more information on running a container using the Marathon web UI, see [DC/OS container management through the Marathon web UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="86bb6-147">For more information on running a container using the Marathon web UI, see [DC/OS container management through the Marathon web UI](container-service-mesos-marathon-ui.md).</span></span>

![Marathon Applications List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/dcos/marathon-applications-list.png)

<span data-ttu-id="86bb6-149">You can also use the REST APIs for communicating with Marathon.</span><span class="sxs-lookup"><span data-stu-id="86bb6-149">You can also use the REST APIs for communicating with Marathon.</span></span> <span data-ttu-id="86bb6-150">There are a number of client libraries that are available for each tool.</span><span class="sxs-lookup"><span data-stu-id="86bb6-150">There are a number of client libraries that are available for each tool.</span></span> <span data-ttu-id="86bb6-151">They cover a variety of languages--and, of course, you can use the HTTP protocol in any language.</span><span class="sxs-lookup"><span data-stu-id="86bb6-151">They cover a variety of languages--and, of course, you can use the HTTP protocol in any language.</span></span> <span data-ttu-id="86bb6-152">In addition, many popular DevOps tools provide support for Marathon.</span><span class="sxs-lookup"><span data-stu-id="86bb6-152">In addition, many popular DevOps tools provide support for Marathon.</span></span> <span data-ttu-id="86bb6-153">This provides maximum flexibility for your operations team when you are working with an Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="86bb6-153">This provides maximum flexibility for your operations team when you are working with an Azure Container Service cluster.</span></span> <span data-ttu-id="86bb6-154">For more information on running a container by using the Marathon REST API, see [DC/OS container management through the Marathon REST API](container-service-mesos-marathon-rest.md).</span><span class="sxs-lookup"><span data-stu-id="86bb6-154">For more information on running a container by using the Marathon REST API, see [DC/OS container management through the Marathon REST API](container-service-mesos-marathon-rest.md).</span></span>

### <a name="using-docker-swarm"></a><span data-ttu-id="86bb6-155">Using Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="86bb6-155">Using Docker Swarm</span></span>
<span data-ttu-id="86bb6-156">Docker Swarm provides native clustering for Docker.</span><span class="sxs-lookup"><span data-stu-id="86bb6-156">Docker Swarm provides native clustering for Docker.</span></span> <span data-ttu-id="86bb6-157">Because Docker Swarm serves the standard Docker API, any tool that already communicates with a Docker daemon can use Swarm to transparently scale to multiple hosts on Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="86bb6-157">Because Docker Swarm serves the standard Docker API, any tool that already communicates with a Docker daemon can use Swarm to transparently scale to multiple hosts on Azure Container Service.</span></span>

![Azure Container Service configured to use Swarm.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/acs-intro/acs-swarm2.png)

<span data-ttu-id="86bb6-159">Supported tools for managing containers on a Swarm cluster include, but are not limited to, the following:</span><span class="sxs-lookup"><span data-stu-id="86bb6-159">Supported tools for managing containers on a Swarm cluster include, but are not limited to, the following:</span></span>

* <span data-ttu-id="86bb6-160">Dokku</span><span class="sxs-lookup"><span data-stu-id="86bb6-160">Dokku</span></span>
* <span data-ttu-id="86bb6-161">Docker CLI and Docker Compose</span><span class="sxs-lookup"><span data-stu-id="86bb6-161">Docker CLI and Docker Compose</span></span>
* <span data-ttu-id="86bb6-162">Krane</span><span class="sxs-lookup"><span data-stu-id="86bb6-162">Krane</span></span>
* <span data-ttu-id="86bb6-163">Jenkins</span><span class="sxs-lookup"><span data-stu-id="86bb6-163">Jenkins</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="86bb6-164">Using Kubernetes</span><span class="sxs-lookup"><span data-stu-id="86bb6-164">Using Kubernetes</span></span>
<span data-ttu-id="86bb6-165">Kubernetes is a popular open-source, production-grade container orchestrator tool.</span><span class="sxs-lookup"><span data-stu-id="86bb6-165">Kubernetes is a popular open-source, production-grade container orchestrator tool.</span></span> <span data-ttu-id="86bb6-166">Kubernetes automates deployment, scaling, and management of containerized applications.</span><span class="sxs-lookup"><span data-stu-id="86bb6-166">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="86bb6-167">Because it is an open-source solution and is driven by the open-source community, it runs seamlessly on Azure Container Service and can be used to deploy containers at scale on Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="86bb6-167">Because it is an open-source solution and is driven by the open-source community, it runs seamlessly on Azure Container Service and can be used to deploy containers at scale on Azure Container Service.</span></span>

![Azure Container Service configured to use Kubernetes.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/acs-intro/kubernetes.png)

<span data-ttu-id="86bb6-169">It has a rich set of features including:</span><span class="sxs-lookup"><span data-stu-id="86bb6-169">It has a rich set of features including:</span></span>
* <span data-ttu-id="86bb6-170">Horizontal scaling</span><span class="sxs-lookup"><span data-stu-id="86bb6-170">Horizontal scaling</span></span>
* <span data-ttu-id="86bb6-171">Service discovery and load balancing</span><span class="sxs-lookup"><span data-stu-id="86bb6-171">Service discovery and load balancing</span></span>
* <span data-ttu-id="86bb6-172">Secrets and configuration management</span><span class="sxs-lookup"><span data-stu-id="86bb6-172">Secrets and configuration management</span></span>
* <span data-ttu-id="86bb6-173">API-based automated rollouts and rollbacks</span><span class="sxs-lookup"><span data-stu-id="86bb6-173">API-based automated rollouts and rollbacks</span></span>
* <span data-ttu-id="86bb6-174">Self-healing</span><span class="sxs-lookup"><span data-stu-id="86bb6-174">Self-healing</span></span>




## <a name="videos"></a><span data-ttu-id="86bb6-175">Videos</span><span class="sxs-lookup"><span data-stu-id="86bb6-175">Videos</span></span>
<span data-ttu-id="86bb6-176">Getting started with Azure Container Service (101):</span><span class="sxs-lookup"><span data-stu-id="86bb6-176">Getting started with Azure Container Service (101):</span></span>  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

<span data-ttu-id="86bb6-177">Building Applications Using the Azure Container Service (Build 2016)</span><span class="sxs-lookup"><span data-stu-id="86bb6-177">Building Applications Using the Azure Container Service (Build 2016)</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="86bb6-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="86bb6-178">Next steps</span></span>

<span data-ttu-id="86bb6-179">Deploy a container service cluster using the [portal](container-service-deployment.md) or [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span><span class="sxs-lookup"><span data-stu-id="86bb6-179">Deploy a container service cluster using the [portal](container-service-deployment.md) or [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span></span>





