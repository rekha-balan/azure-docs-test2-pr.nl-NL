---
title: Canary release with Vamp on Azure DC/OS cluster
description: How to use Vamp to canary release services and apply smart traffic filtering on an Azure Container Service DC/OS cluster
services: container-service
author: gggina
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: 0f6c0e9206d9e056ee0496b6cc515625b08b1e4a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870069"
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="9d608-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="9d608-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="9d608-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="9d608-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="9d608-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span><span class="sxs-lookup"><span data-stu-id="9d608-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="9d608-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span><span class="sxs-lookup"><span data-stu-id="9d608-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="9d608-107">About canary releases and Vamp</span><span class="sxs-lookup"><span data-stu-id="9d608-107">About canary releases and Vamp</span></span>


<span data-ttu-id="9d608-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span><span class="sxs-lookup"><span data-stu-id="9d608-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="9d608-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span><span class="sxs-lookup"><span data-stu-id="9d608-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="9d608-110">So why aren’t all companies using it?</span><span class="sxs-lookup"><span data-stu-id="9d608-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="9d608-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span><span class="sxs-lookup"><span data-stu-id="9d608-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="9d608-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span><span class="sxs-lookup"><span data-stu-id="9d608-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="9d608-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span><span class="sxs-lookup"><span data-stu-id="9d608-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span></span> <span data-ttu-id="9d608-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span><span class="sxs-lookup"><span data-stu-id="9d608-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="9d608-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span><span class="sxs-lookup"><span data-stu-id="9d608-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="9d608-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span><span class="sxs-lookup"><span data-stu-id="9d608-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="9d608-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span><span class="sxs-lookup"><span data-stu-id="9d608-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="9d608-118">Set up Azure Container Service with DC/OS</span><span class="sxs-lookup"><span data-stu-id="9d608-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="9d608-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span><span class="sxs-lookup"><span data-stu-id="9d608-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="9d608-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="9d608-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span></span> <span data-ttu-id="9d608-121">This article assumes that you tunnel to the cluster on local port 80.</span><span class="sxs-lookup"><span data-stu-id="9d608-121">This article assumes that you tunnel to the cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="9d608-122">Set up Vamp</span><span class="sxs-lookup"><span data-stu-id="9d608-122">Set up Vamp</span></span>

<span data-ttu-id="9d608-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="9d608-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span></span> 

![DC/OS UI](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="9d608-125">Installation is done in two stages:</span><span class="sxs-lookup"><span data-stu-id="9d608-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="9d608-126">**Deploy Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="9d608-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="9d608-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span><span class="sxs-lookup"><span data-stu-id="9d608-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="9d608-128">Deploy Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="9d608-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="9d608-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span><span class="sxs-lookup"><span data-stu-id="9d608-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="9d608-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span><span class="sxs-lookup"><span data-stu-id="9d608-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="9d608-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span><span class="sxs-lookup"><span data-stu-id="9d608-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="9d608-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span><span class="sxs-lookup"><span data-stu-id="9d608-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span></span>

  ![Select JSON mode](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="9d608-134">Paste in the following JSON.</span><span class="sxs-lookup"><span data-stu-id="9d608-134">Paste in the following JSON.</span></span> <span data-ttu-id="9d608-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span><span class="sxs-lookup"><span data-stu-id="9d608-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="9d608-136">Click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="9d608-136">Click **Deploy**.</span></span>

  <span data-ttu-id="9d608-137">DC/OS deploys the Elasticsearch container.</span><span class="sxs-lookup"><span data-stu-id="9d608-137">DC/OS deploys the Elasticsearch container.</span></span> <span data-ttu-id="9d608-138">You can track progress on the **Services** page.</span><span class="sxs-lookup"><span data-stu-id="9d608-138">You can track progress on the **Services** page.</span></span>  

  ![deploy e?Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="9d608-140">Deploy Vamp</span><span class="sxs-lookup"><span data-stu-id="9d608-140">Deploy Vamp</span></span>

<span data-ttu-id="9d608-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span><span class="sxs-lookup"><span data-stu-id="9d608-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="9d608-142">Go to **Universe** and search for **vamp**.</span><span class="sxs-lookup"><span data-stu-id="9d608-142">Go to **Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="9d608-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="9d608-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="9d608-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span><span class="sxs-lookup"><span data-stu-id="9d608-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="9d608-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="9d608-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Enter Elasticsearch URL](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="9d608-147">Click **Review and Install**, then click **Install** to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="9d608-147">Click **Review and Install**, then click **Install** to start the deployment.</span></span>  

  <span data-ttu-id="9d608-148">DC/OS deploys all required Vamp components.</span><span class="sxs-lookup"><span data-stu-id="9d608-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="9d608-149">You can track progress on the **Services** page.</span><span class="sxs-lookup"><span data-stu-id="9d608-149">You can track progress on the **Services** page.</span></span>
  
  ![Deploy Vamp as universe package](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="9d608-151">Once deployment has completed, you can access the Vamp UI:</span><span class="sxs-lookup"><span data-stu-id="9d608-151">Once deployment has completed, you can access the Vamp UI:</span></span>

  ![Vamp service on DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp UI](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="9d608-154">Deploy your first service</span><span class="sxs-lookup"><span data-stu-id="9d608-154">Deploy your first service</span></span>

<span data-ttu-id="9d608-155">Now that Vamp is up and running, deploy a service from a blueprint.</span><span class="sxs-lookup"><span data-stu-id="9d608-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="9d608-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span><span class="sxs-lookup"><span data-stu-id="9d608-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span></span> <span data-ttu-id="9d608-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span><span class="sxs-lookup"><span data-stu-id="9d608-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="9d608-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="9d608-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="9d608-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span><span class="sxs-lookup"><span data-stu-id="9d608-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span></span> <span data-ttu-id="9d608-161">Deploy the app through Vamp using a simple blueprint.</span><span class="sxs-lookup"><span data-stu-id="9d608-161">Deploy the app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="9d608-162">Go to **Deployments**.</span><span class="sxs-lookup"><span data-stu-id="9d608-162">Go to **Deployments**.</span></span>

2. <span data-ttu-id="9d608-163">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="9d608-163">Click **Add**.</span></span>

3. <span data-ttu-id="9d608-164">Paste in the following blueprint YAML.</span><span class="sxs-lookup"><span data-stu-id="9d608-164">Paste in the following blueprint YAML.</span></span> <span data-ttu-id="9d608-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span><span class="sxs-lookup"><span data-stu-id="9d608-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster to create
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="9d608-166">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d608-166">Click **Save**.</span></span> <span data-ttu-id="9d608-167">Vamp initiates the deployment.</span><span class="sxs-lookup"><span data-stu-id="9d608-167">Vamp initiates the deployment.</span></span>

<span data-ttu-id="9d608-168">The deployment is listed on the **Deployments** page.</span><span class="sxs-lookup"><span data-stu-id="9d608-168">The deployment is listed on the **Deployments** page.</span></span> <span data-ttu-id="9d608-169">Click the deployment to monitor its status.</span><span class="sxs-lookup"><span data-stu-id="9d608-169">Click the deployment to monitor its status.</span></span>

![Vamp UI - deploying sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![sava service in Vamp UI](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="9d608-172">Two gateways are created, which are listed on the **Gateways** page:</span><span class="sxs-lookup"><span data-stu-id="9d608-172">Two gateways are created, which are listed on the **Gateways** page:</span></span>

* <span data-ttu-id="9d608-173">a stable endpoint to access the running service (port 9050)</span><span class="sxs-lookup"><span data-stu-id="9d608-173">a stable endpoint to access the running service (port 9050)</span></span> 
* <span data-ttu-id="9d608-174">a Vamp-managed internal gateway (more on this gateway later).</span><span class="sxs-lookup"><span data-stu-id="9d608-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Vamp UI - sava gateways](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="9d608-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span><span class="sxs-lookup"><span data-stu-id="9d608-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span></span> <span data-ttu-id="9d608-177">To access the service, update the Azure networking configuration.</span><span class="sxs-lookup"><span data-stu-id="9d608-177">To access the service, update the Azure networking configuration.</span></span>


## <a name="update-the-azure-network-configuration"></a><span data-ttu-id="9d608-178">Update the Azure network configuration</span><span class="sxs-lookup"><span data-stu-id="9d608-178">Update the Azure network configuration</span></span>

<span data-ttu-id="9d608-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span><span class="sxs-lookup"><span data-stu-id="9d608-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="9d608-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span><span class="sxs-lookup"><span data-stu-id="9d608-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="9d608-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span><span class="sxs-lookup"><span data-stu-id="9d608-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span></span> 

2. <span data-ttu-id="9d608-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span><span class="sxs-lookup"><span data-stu-id="9d608-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span></span>

<span data-ttu-id="9d608-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="9d608-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="9d608-184">Specify port 9050 for all port settings.</span><span class="sxs-lookup"><span data-stu-id="9d608-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="9d608-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="9d608-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="9d608-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span><span class="sxs-lookup"><span data-stu-id="9d608-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span></span>

![Azure portal - get public IP address](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="9d608-189">Run a canary release</span><span class="sxs-lookup"><span data-stu-id="9d608-189">Run a canary release</span></span>

<span data-ttu-id="9d608-190">Suppose you have a new version of this application that you want to canary release into production.</span><span class="sxs-lookup"><span data-stu-id="9d608-190">Suppose you have a new version of this application that you want to canary release into production.</span></span> <span data-ttu-id="9d608-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span><span class="sxs-lookup"><span data-stu-id="9d608-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span></span> <span data-ttu-id="9d608-192">Vamp lets you easily add new services to the running deployment.</span><span class="sxs-lookup"><span data-stu-id="9d608-192">Vamp lets you easily add new services to the running deployment.</span></span> <span data-ttu-id="9d608-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span><span class="sxs-lookup"><span data-stu-id="9d608-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="9d608-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span><span class="sxs-lookup"><span data-stu-id="9d608-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span></span> <span data-ttu-id="9d608-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span><span class="sxs-lookup"><span data-stu-id="9d608-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="9d608-196">Merge a new service variant</span><span class="sxs-lookup"><span data-stu-id="9d608-196">Merge a new service variant</span></span>

<span data-ttu-id="9d608-197">To merge the new sava 1.1 service with the running deployment:</span><span class="sxs-lookup"><span data-stu-id="9d608-197">To merge the new sava 1.1 service with the running deployment:</span></span>

1. <span data-ttu-id="9d608-198">In the Vamp UI, click **Blueprints**.</span><span class="sxs-lookup"><span data-stu-id="9d608-198">In the Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="9d608-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="9d608-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster to update
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint to update
  ```
  
3. <span data-ttu-id="9d608-200">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d608-200">Click **Save**.</span></span> <span data-ttu-id="9d608-201">The blueprint is stored and listed on the **Blueprints** page.</span><span class="sxs-lookup"><span data-stu-id="9d608-201">The blueprint is stored and listed on the **Blueprints** page.</span></span>

4. <span data-ttu-id="9d608-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span><span class="sxs-lookup"><span data-stu-id="9d608-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Vamp UI - blueprints](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="9d608-204">Select the **sava** deployment and click **Merge**.</span><span class="sxs-lookup"><span data-stu-id="9d608-204">Select the **sava** deployment and click **Merge**.</span></span>

  ![Vamp UI - merge blueprint to deployment](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="9d608-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span><span class="sxs-lookup"><span data-stu-id="9d608-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span></span> 

![Vamp UI - updated sava deployment](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="9d608-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span></span> <span data-ttu-id="9d608-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span><span class="sxs-lookup"><span data-stu-id="9d608-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span></span>

![Vamp UI - cluster gateway](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="9d608-211">Canary release</span><span class="sxs-lookup"><span data-stu-id="9d608-211">Canary release</span></span>

<span data-ttu-id="9d608-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span><span class="sxs-lookup"><span data-stu-id="9d608-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span></span>

1. <span data-ttu-id="9d608-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span><span class="sxs-lookup"><span data-stu-id="9d608-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span></span>

2. <span data-ttu-id="9d608-214">Set the weight distribution to 50%/50% and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d608-214">Set the weight distribution to 50%/50% and click **Save**.</span></span>

  ![Vamp UI - gateway weight slider](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="9d608-216">Go back to your browser and refresh the sava page a few more times.</span><span class="sxs-lookup"><span data-stu-id="9d608-216">Go back to your browser and refresh the sava page a few more times.</span></span> <span data-ttu-id="9d608-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span><span class="sxs-lookup"><span data-stu-id="9d608-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![alternating sava1.0 and sava1.1 services](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="9d608-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span><span class="sxs-lookup"><span data-stu-id="9d608-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="9d608-220">Filter traffic</span><span class="sxs-lookup"><span data-stu-id="9d608-220">Filter traffic</span></span>

<span data-ttu-id="9d608-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span><span class="sxs-lookup"><span data-stu-id="9d608-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="9d608-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span></span> <span data-ttu-id="9d608-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span></span>

<span data-ttu-id="9d608-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span><span class="sxs-lookup"><span data-stu-id="9d608-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span></span> <span data-ttu-id="9d608-225">Traffic is first filtered and directed according to the conditions applied to each route.</span><span class="sxs-lookup"><span data-stu-id="9d608-225">Traffic is first filtered and directed according to the conditions applied to each route.</span></span> <span data-ttu-id="9d608-226">All remaining traffic is distributed according to the gateway weight setting.</span><span class="sxs-lookup"><span data-stu-id="9d608-226">All remaining traffic is distributed according to the gateway weight setting.</span></span>

<span data-ttu-id="9d608-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span><span class="sxs-lookup"><span data-stu-id="9d608-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span></span>

1. <span data-ttu-id="9d608-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="9d608-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="9d608-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="9d608-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="9d608-230">Vamp adds the condition with a default strength of 0%.</span><span class="sxs-lookup"><span data-stu-id="9d608-230">Vamp adds the condition with a default strength of 0%.</span></span> <span data-ttu-id="9d608-231">To start filtering traffic, you need to adjust the condition strength.</span><span class="sxs-lookup"><span data-stu-id="9d608-231">To start filtering traffic, you need to adjust the condition strength.</span></span>

3. <span data-ttu-id="9d608-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span><span class="sxs-lookup"><span data-stu-id="9d608-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span></span>
 
4. <span data-ttu-id="9d608-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span><span class="sxs-lookup"><span data-stu-id="9d608-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span></span>

  <span data-ttu-id="9d608-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span></span>

  ![Vamp UI - apply condition to gateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="9d608-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span></span> <span data-ttu-id="9d608-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="9d608-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="9d608-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span></span>

6. <span data-ttu-id="9d608-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span><span class="sxs-lookup"><span data-stu-id="9d608-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span></span> <span data-ttu-id="9d608-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="9d608-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span></span>

  ![Vamp UI - filter traffic](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="9d608-242">Summing up</span><span class="sxs-lookup"><span data-stu-id="9d608-242">Summing up</span></span>

<span data-ttu-id="9d608-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="9d608-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span></span> <span data-ttu-id="9d608-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span><span class="sxs-lookup"><span data-stu-id="9d608-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span></span>

<span data-ttu-id="9d608-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span><span class="sxs-lookup"><span data-stu-id="9d608-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d608-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d608-246">Next steps</span></span>

* <span data-ttu-id="9d608-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="9d608-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="9d608-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="9d608-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="9d608-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/).</span><span class="sxs-lookup"><span data-stu-id="9d608-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/).</span></span>

