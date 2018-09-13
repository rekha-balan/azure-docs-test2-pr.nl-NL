---
title: Monitor Azure DC/OS cluster - Dynatrace | Microsoft Docs
description: Monitor an Azure Container Service DC/OS cluster with Dynatrace. Deploy the Dynatrace OneAgent by using the DC/OS dashboard.
services: container-service
documentationcenter: ''
author: MartinGoodwell
manager: ''
editor: ''
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.openlocfilehash: 7a082f9973587d1b5418585831a4170434a9941e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554040"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="d2a59-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="d2a59-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="d2a59-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="d2a59-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="d2a59-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span><span class="sxs-lookup"><span data-stu-id="d2a59-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="d2a59-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="d2a59-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="d2a59-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span><span class="sxs-lookup"><span data-stu-id="d2a59-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="d2a59-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span><span class="sxs-lookup"><span data-stu-id="d2a59-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="d2a59-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span><span class="sxs-lookup"><span data-stu-id="d2a59-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="d2a59-112">The following figure shows the Dynatrace UI:</span><span class="sxs-lookup"><span data-stu-id="d2a59-112">The following figure shows the Dynatrace UI:</span></span>

![Dynatrace UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="d2a59-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d2a59-114">Prerequisites</span></span> 
<span data-ttu-id="d2a59-115">[Deploy](./container-service-deployment.md) and [connect](./container-service-connect.md) to a cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="d2a59-115">[Deploy](./container-service-deployment.md) and [connect](./container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="d2a59-116">Explore the [Marathon UI](./container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="d2a59-116">Explore the [Marathon UI](./container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="d2a59-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span><span class="sxs-lookup"><span data-stu-id="d2a59-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="d2a59-118">Configure a Dynatrace deployment with Marathon</span><span class="sxs-lookup"><span data-stu-id="d2a59-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="d2a59-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span><span class="sxs-lookup"><span data-stu-id="d2a59-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="d2a59-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="d2a59-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="d2a59-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="d2a59-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace in DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="d2a59-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span><span class="sxs-lookup"><span data-stu-id="d2a59-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="d2a59-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="d2a59-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace Set up PaaS integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="d2a59-126">On the page, select **Set up PaaS integration**.</span><span class="sxs-lookup"><span data-stu-id="d2a59-126">On the page, select **Set up PaaS integration**.</span></span> 

    ![Dynatrace API token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="d2a59-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="d2a59-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![Dynatrace OneAgent configuration in the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="d2a59-130">Set the instances to the number of nodes you intend to run.</span><span class="sxs-lookup"><span data-stu-id="d2a59-130">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="d2a59-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span><span class="sxs-lookup"><span data-stu-id="d2a59-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="d2a59-132">If you prefer, you can also set this to a value like 1000000.</span><span class="sxs-lookup"><span data-stu-id="d2a59-132">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="d2a59-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span><span class="sxs-lookup"><span data-stu-id="d2a59-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![Dynatrace configuration in the DC/OS Universe-instances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="d2a59-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2a59-135">Next steps</span></span>

<span data-ttu-id="d2a59-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span><span class="sxs-lookup"><span data-stu-id="d2a59-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="d2a59-137">You can explore the different usage metrics for the containers within your cluster.</span><span class="sxs-lookup"><span data-stu-id="d2a59-137">You can explore the different usage metrics for the containers within your cluster.</span></span> 





