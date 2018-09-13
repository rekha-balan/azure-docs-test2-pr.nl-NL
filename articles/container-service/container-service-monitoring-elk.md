---
title: Monitor an Azure DC/OS cluster - ELK stack | Microsoft Docs
description: Monitor a DC/OS cluster in Azure Container Service cluster with ELK (Elasticsearch, Logstash, and Kibana).
services: container-service
documentationcenter: ''
author: sauryadas
manager: madhana
editor: ''
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure, monitoring, elk
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.openlocfilehash: efa0531d7ee22b9f1e42c14bb10cc58dce981847
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554663"
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="fec4e-104">Monitor an Azure Container Service cluster with ELK</span><span class="sxs-lookup"><span data-stu-id="fec4e-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="fec4e-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="fec4e-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fec4e-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fec4e-106">Prerequisites</span></span>
<span data-ttu-id="fec4e-107">[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="fec4e-107">[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="fec4e-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="fec4e-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="fec4e-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="fec4e-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="fec4e-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="fec4e-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="fec4e-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span><span class="sxs-lookup"><span data-stu-id="fec4e-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="fec4e-112">Configure the ELK stack on a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="fec4e-112">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="fec4e-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span><span class="sxs-lookup"><span data-stu-id="fec4e-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="fec4e-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span><span class="sxs-lookup"><span data-stu-id="fec4e-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="fec4e-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span><span class="sxs-lookup"><span data-stu-id="fec4e-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-elk/elk1.PNG) ![ELK2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-elk/elk2.PNG) ![ELK3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="fec4e-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="fec4e-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="fec4e-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span><span class="sxs-lookup"><span data-stu-id="fec4e-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="fec4e-122">Toggle to **JSON mode** and scroll down to the labels section.</span><span class="sxs-lookup"><span data-stu-id="fec4e-122">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="fec4e-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span><span class="sxs-lookup"><span data-stu-id="fec4e-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="fec4e-124">Once you click **Deploy changes**, your container restarts.</span><span class="sxs-lookup"><span data-stu-id="fec4e-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="fec4e-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span><span class="sxs-lookup"><span data-stu-id="fec4e-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="fec4e-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span><span class="sxs-lookup"><span data-stu-id="fec4e-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="fec4e-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="fec4e-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="fec4e-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="fec4e-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="fec4e-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span><span class="sxs-lookup"><span data-stu-id="fec4e-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="fec4e-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span><span class="sxs-lookup"><span data-stu-id="fec4e-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="fec4e-133">Follow instructions [here](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="fec4e-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="fec4e-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="fec4e-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fec4e-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="fec4e-135">Next steps</span></span>

* <span data-ttu-id="fec4e-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="fec4e-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="fec4e-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="fec4e-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 







