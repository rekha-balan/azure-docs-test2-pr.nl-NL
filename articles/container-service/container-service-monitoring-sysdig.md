---
title: Monitor an Azure Container Service cluster with Sysdig | Microsoft Docs
description: Monitor an Azure Container Service cluster with Sysdig.
services: container-service
documentationcenter: ''
author: sauryadas
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure
ms.assetid: 91d9a28a-3a52-4194-879e-30f2fa3d946b
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.openlocfilehash: 34e9f538c85bc55fc71d83342cae53beda341a3a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553180"
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="7d013-104">Monitor an Azure Container Service cluster with Sysdig</span><span class="sxs-lookup"><span data-stu-id="7d013-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="7d013-105">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="7d013-105">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="7d013-106">You need an account with Sysdig for this configuration.</span><span class="sxs-lookup"><span data-stu-id="7d013-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7d013-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7d013-107">Prerequisites</span></span>
<span data-ttu-id="7d013-108">[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="7d013-108">[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="7d013-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="7d013-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="7d013-110">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span><span class="sxs-lookup"><span data-stu-id="7d013-110">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="7d013-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="7d013-111">Sysdig</span></span>
<span data-ttu-id="7d013-112">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span><span class="sxs-lookup"><span data-stu-id="7d013-112">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span></span> <span data-ttu-id="7d013-113">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span><span class="sxs-lookup"><span data-stu-id="7d013-113">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="7d013-114">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span><span class="sxs-lookup"><span data-stu-id="7d013-114">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span></span> <span data-ttu-id="7d013-115">This view is in the “Overview” section, which is currently in beta.</span><span class="sxs-lookup"><span data-stu-id="7d013-115">This view is in the “Overview” section, which is currently in beta.</span></span> 

![Sysdig UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="7d013-117">Configure a Sysdig deployment with Marathon</span><span class="sxs-lookup"><span data-stu-id="7d013-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="7d013-118">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span><span class="sxs-lookup"><span data-stu-id="7d013-118">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="7d013-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span><span class="sxs-lookup"><span data-stu-id="7d013-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span></span>

![Sysdig in DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="7d013-121">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span><span class="sxs-lookup"><span data-stu-id="7d013-121">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="7d013-122">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span><span class="sxs-lookup"><span data-stu-id="7d013-122">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig API key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="7d013-124">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="7d013-124">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span></span> 

![Sysdig configuration in the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="7d013-126">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span><span class="sxs-lookup"><span data-stu-id="7d013-126">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span></span> <span data-ttu-id="7d013-127">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span><span class="sxs-lookup"><span data-stu-id="7d013-127">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span></span> 

![Sysdig configuration in the DC/OS Universe-instances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="7d013-129">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span><span class="sxs-lookup"><span data-stu-id="7d013-129">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span></span> 

<span data-ttu-id="7d013-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="7d013-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>





