---
title: Monitor Azure DC/OS cluster - Datadog | Microsoft Docs
description: Monitor an Azure Container Service cluster with Datadog. Use the DC/OS web UI to deploy the Datadog agents to your cluster.
services: container-service
documentationcenter: ''
author: sauryadas
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, DC/OS, Docker Swarm, Azure
ms.assetid: ed00635d-4569-4f87-ab63-e307b2690b42
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.openlocfilehash: 123e91aac99697271620133c40f3bcdcd4507a19
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563604"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="393e7-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span><span class="sxs-lookup"><span data-stu-id="393e7-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="393e7-106">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="393e7-106">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="393e7-107">You will need an account with Datadog for this configuration.</span><span class="sxs-lookup"><span data-stu-id="393e7-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="393e7-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="393e7-108">Prerequisites</span></span>
<span data-ttu-id="393e7-109">[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="393e7-109">[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="393e7-110">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="393e7-110">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="393e7-111">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span><span class="sxs-lookup"><span data-stu-id="393e7-111">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="393e7-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="393e7-112">Datadog</span></span>
<span data-ttu-id="393e7-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="393e7-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="393e7-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span><span class="sxs-lookup"><span data-stu-id="393e7-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="393e7-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span><span class="sxs-lookup"><span data-stu-id="393e7-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="393e7-116">Datadog splits metrics into containers and images.</span><span class="sxs-lookup"><span data-stu-id="393e7-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="393e7-117">An example of what the UI looks like for CPU usage is below.</span><span class="sxs-lookup"><span data-stu-id="393e7-117">An example of what the UI looks like for CPU usage is below.</span></span>

![Datadog UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="393e7-119">Configure a Datadog deployment with Marathon</span><span class="sxs-lookup"><span data-stu-id="393e7-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="393e7-120">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span><span class="sxs-lookup"><span data-stu-id="393e7-120">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="393e7-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="393e7-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="393e7-122">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span><span class="sxs-lookup"><span data-stu-id="393e7-122">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog package within the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog1.png)

<span data-ttu-id="393e7-124">Now to complete the configuration you will need a Datadog account or a free trial account.</span><span class="sxs-lookup"><span data-stu-id="393e7-124">Now to complete the configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="393e7-125">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="393e7-125">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog2.png)

<span data-ttu-id="393e7-127">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="393e7-127">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span></span> 

![Datadog configuration in the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="393e7-129">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span><span class="sxs-lookup"><span data-stu-id="393e7-129">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span></span> <span data-ttu-id="393e7-130">This is an interim solution.</span><span class="sxs-lookup"><span data-stu-id="393e7-130">This is an interim solution.</span></span> <span data-ttu-id="393e7-131">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="393e7-131">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="393e7-132">From there you will see Custom and Integration Dashboards.</span><span class="sxs-lookup"><span data-stu-id="393e7-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="393e7-133">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span><span class="sxs-lookup"><span data-stu-id="393e7-133">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span></span> 





