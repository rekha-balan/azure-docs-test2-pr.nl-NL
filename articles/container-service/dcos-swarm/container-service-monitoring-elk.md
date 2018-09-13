---
title: Monitor an Azure DC/OS cluster - ELK stack
description: Monitor a DC/OS cluster in Azure Container Service cluster with ELK (Elasticsearch, Logstash, and Kibana).
services: container-service
author: sauryadas
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: dc863894d8846e066c90bdf7b309f141d32a1186
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866747"
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="3247c-103">Monitor an Azure Container Service cluster with ELK</span><span class="sxs-lookup"><span data-stu-id="3247c-103">Monitor an Azure Container Service cluster with ELK</span></span>

<span data-ttu-id="3247c-104">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3247c-104">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3247c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3247c-105">Prerequisites</span></span>
<span data-ttu-id="3247c-106">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3247c-106">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="3247c-107">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="3247c-107">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="3247c-108">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="3247c-108">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="3247c-109">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="3247c-109">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="3247c-110">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span><span class="sxs-lookup"><span data-stu-id="3247c-110">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="3247c-111">Configure the ELK stack on a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="3247c-111">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="3247c-112">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span><span class="sxs-lookup"><span data-stu-id="3247c-112">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="3247c-113">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span><span class="sxs-lookup"><span data-stu-id="3247c-113">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="3247c-114">You can learn more about configuration if you go to the **Advanced Installation** link.</span><span class="sxs-lookup"><span data-stu-id="3247c-114">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="3247c-118">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="3247c-118">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="3247c-119">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span><span class="sxs-lookup"><span data-stu-id="3247c-119">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="3247c-121">Toggle to **JSON mode** and scroll down to the labels section.</span><span class="sxs-lookup"><span data-stu-id="3247c-121">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="3247c-122">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span><span class="sxs-lookup"><span data-stu-id="3247c-122">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="3247c-123">Once you click **Deploy changes**, your container restarts.</span><span class="sxs-lookup"><span data-stu-id="3247c-123">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="3247c-125">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span><span class="sxs-lookup"><span data-stu-id="3247c-125">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="3247c-126">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span><span class="sxs-lookup"><span data-stu-id="3247c-126">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="3247c-127">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="3247c-127">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="3247c-128">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="3247c-128">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="3247c-129">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span><span class="sxs-lookup"><span data-stu-id="3247c-129">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="3247c-131">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span><span class="sxs-lookup"><span data-stu-id="3247c-131">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="3247c-132">Follow instructions [here](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="3247c-132">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="3247c-133">Then open the Kibana dashboard at: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="3247c-133">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3247c-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="3247c-134">Next steps</span></span>

* <span data-ttu-id="3247c-135">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="3247c-135">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="3247c-136">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="3247c-136">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

