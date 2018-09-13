---
title: How to scale an Azure Container Service cluster for Machine Learning | Microsoft Docs
description: Scaling an ACS cluster - autoscale and static scaling; scaling the number of nodes in the cluster
services: machine-learning
author: aashishb
ms.author: aashishb
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 10/04/2017
ms.openlocfilehash: e547d778ebf34b55c0c18921cf28e2a78fd269cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966360"
---
# <a name="scaling-the-cluster-to-manage-web-service-throughput"></a><span data-ttu-id="531e5-103">Scaling the cluster to manage web service throughput</span><span class="sxs-lookup"><span data-stu-id="531e5-103">Scaling the cluster to manage web service throughput</span></span>

## <a name="why-scale-the-cluster"></a><span data-ttu-id="531e5-104">Why scale the cluster?</span><span class="sxs-lookup"><span data-stu-id="531e5-104">Why scale the cluster?</span></span>

<span data-ttu-id="531e5-105">Scaling the Azure Container Service (ACS) cluster is an effective way to optimize the service throughput while keeping the cluster size to a minimum to reduce cost.</span><span class="sxs-lookup"><span data-stu-id="531e5-105">Scaling the Azure Container Service (ACS) cluster is an effective way to optimize the service throughput while keeping the cluster size to a minimum to reduce cost.</span></span> 

<span data-ttu-id="531e5-106">To better understand autoscaling, consider the following example of a cluster running three web services:</span><span class="sxs-lookup"><span data-stu-id="531e5-106">To better understand autoscaling, consider the following example of a cluster running three web services:</span></span>

![Example: Three services on a cluster](media/how-to-scale-clusters/three-services.png)

<span data-ttu-id="531e5-108">The services have various peak demands: Service 1 (blue line) requires 40 pods at peak demand, Service 2 (orange line) requires 38 at peak, and Service 3 (gray line) requires 50 at peak.</span><span class="sxs-lookup"><span data-stu-id="531e5-108">The services have various peak demands: Service 1 (blue line) requires 40 pods at peak demand, Service 2 (orange line) requires 38 at peak, and Service 3 (gray line) requires 50 at peak.</span></span> <span data-ttu-id="531e5-109">If you reserve the needed peak capacity for each service individually, this cluster would need at least 40 + 38 + 50 = 128 total pods.</span><span class="sxs-lookup"><span data-stu-id="531e5-109">If you reserve the needed peak capacity for each service individually, this cluster would need at least 40 + 38 + 50 = 128 total pods.</span></span>

<span data-ttu-id="531e5-110">But consider the actual pod usage at any point in time, represented by the black dashed line in the graph.</span><span class="sxs-lookup"><span data-stu-id="531e5-110">But consider the actual pod usage at any point in time, represented by the black dashed line in the graph.</span></span> <span data-ttu-id="531e5-111">In this case, the *highest number of pods used at any one time* is 64, which occurs at 20:00 when Service 3 is at peak.</span><span class="sxs-lookup"><span data-stu-id="531e5-111">In this case, the *highest number of pods used at any one time* is 64, which occurs at 20:00 when Service 3 is at peak.</span></span> <span data-ttu-id="531e5-112">At this time, Service 3 uses 50 pods, but Service 2 uses just 9 pods, and Service 1 uses only 5.</span><span class="sxs-lookup"><span data-stu-id="531e5-112">At this time, Service 3 uses 50 pods, but Service 2 uses just 9 pods, and Service 1 uses only 5.</span></span> <span data-ttu-id="531e5-113">Remember, this is *peak usage* for this cluster.</span><span class="sxs-lookup"><span data-stu-id="531e5-113">Remember, this is *peak usage* for this cluster.</span></span> <span data-ttu-id="531e5-114">This means that at no time does the cluster use more than 64 pods -- half the calculated requirement of 128 pods for the three services scaled independently for peak usage.</span><span class="sxs-lookup"><span data-stu-id="531e5-114">This means that at no time does the cluster use more than 64 pods -- half the calculated requirement of 128 pods for the three services scaled independently for peak usage.</span></span>

<span data-ttu-id="531e5-115">By reassigning pods in the cluster -- that is, by rescaling -- to meet the current demand of each service rather than simply require sufficient resources for the peak demand of all services, you can decrease your cluster size.</span><span class="sxs-lookup"><span data-stu-id="531e5-115">By reassigning pods in the cluster -- that is, by rescaling -- to meet the current demand of each service rather than simply require sufficient resources for the peak demand of all services, you can decrease your cluster size.</span></span> <span data-ttu-id="531e5-116">In this simple example, autoscaling decreases the required number of pods from 128 to 64, cutting the required cluster size in half.</span><span class="sxs-lookup"><span data-stu-id="531e5-116">In this simple example, autoscaling decreases the required number of pods from 128 to 64, cutting the required cluster size in half.</span></span>

<span data-ttu-id="531e5-117">Scaling the number of pods is a relatively fast operation, requiring less than a minute, so the service's responsiveness is not seriously impacted.</span><span class="sxs-lookup"><span data-stu-id="531e5-117">Scaling the number of pods is a relatively fast operation, requiring less than a minute, so the service's responsiveness is not seriously impacted.</span></span>

> [!NOTE]
> <span data-ttu-id="531e5-118">Scaling a cluster will not help with request latency issues.</span><span class="sxs-lookup"><span data-stu-id="531e5-118">Scaling a cluster will not help with request latency issues.</span></span> <span data-ttu-id="531e5-119">For operationalization purposes, scaling up should increase the number of successes and decrease Service Unavailable errors.</span><span class="sxs-lookup"><span data-stu-id="531e5-119">For operationalization purposes, scaling up should increase the number of successes and decrease Service Unavailable errors.</span></span> 

## <a name="how-to-scale-web-services-on-your-acs-cluster"></a><span data-ttu-id="531e5-120">How to scale web services on your ACS cluster</span><span class="sxs-lookup"><span data-stu-id="531e5-120">How to scale web services on your ACS cluster</span></span>

<span data-ttu-id="531e5-121">The cluster setup option of the model management CLI by default configures two agents and one pod in your environment.</span><span class="sxs-lookup"><span data-stu-id="531e5-121">The cluster setup option of the model management CLI by default configures two agents and one pod in your environment.</span></span> <span data-ttu-id="531e5-122">It also installs the Kubernetes CLI.</span><span class="sxs-lookup"><span data-stu-id="531e5-122">It also installs the Kubernetes CLI.</span></span>

<span data-ttu-id="531e5-123">You can scale the web services you have deployed to ACS by adjusting:</span><span class="sxs-lookup"><span data-stu-id="531e5-123">You can scale the web services you have deployed to ACS by adjusting:</span></span>

* <span data-ttu-id="531e5-124">The number of agent nodes in the cluster</span><span class="sxs-lookup"><span data-stu-id="531e5-124">The number of agent nodes in the cluster</span></span>
* <span data-ttu-id="531e5-125">The number of Kubernetes pod replicas running on agent nodes</span><span class="sxs-lookup"><span data-stu-id="531e5-125">The number of Kubernetes pod replicas running on agent nodes</span></span>

### <a name="scaling-the-number-of-nodes-in-the-cluster"></a><span data-ttu-id="531e5-126">Scaling the number of nodes in the cluster</span><span class="sxs-lookup"><span data-stu-id="531e5-126">Scaling the number of nodes in the cluster</span></span>

<span data-ttu-id="531e5-127">The following command sets the count of agent nodes in the cluster:</span><span class="sxs-lookup"><span data-stu-id="531e5-127">The following command sets the count of agent nodes in the cluster:</span></span>

```
az acs scale -g <resource group> -n <cluster name> --new-agent-count <new scale>
```

<span data-ttu-id="531e5-128">This will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="531e5-128">This will take a few minutes to complete.</span></span> <span data-ttu-id="531e5-129">For more information on scaling the number of nodes in the cluster, see [Scale agent nodes in a Container Service cluster](https://docs.microsoft.com/azure/container-service/container-service-scale).</span><span class="sxs-lookup"><span data-stu-id="531e5-129">For more information on scaling the number of nodes in the cluster, see [Scale agent nodes in a Container Service cluster](https://docs.microsoft.com/azure/container-service/container-service-scale).</span></span>

### <a name="scaling-the-number-of-kubernetes-pod-replicas-in-a-cluster"></a><span data-ttu-id="531e5-130">Scaling the number of Kubernetes pod replicas in a cluster</span><span class="sxs-lookup"><span data-stu-id="531e5-130">Scaling the number of Kubernetes pod replicas in a cluster</span></span>
 
<span data-ttu-id="531e5-131">You can scale the number of pod replicas assigned to the cluster using the Azure Machine Learning CLI or the [Kubernetes dashboard] (https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="531e5-131">You can scale the number of pod replicas assigned to the cluster using the Azure Machine Learning CLI or the [Kubernetes dashboard] (https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).</span></span>

<span data-ttu-id="531e5-132">For more information on Kubernetes replica pods, see the [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) documentation.</span><span class="sxs-lookup"><span data-stu-id="531e5-132">For more information on Kubernetes replica pods, see the [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) documentation.</span></span>

#### <a name="scaling-a-cluster-with-the-azure-machine-learning-cli"></a><span data-ttu-id="531e5-133">Scaling a cluster with the Azure Machine Learning CLI</span><span class="sxs-lookup"><span data-stu-id="531e5-133">Scaling a cluster with the Azure Machine Learning CLI</span></span>

<span data-ttu-id="531e5-134">There are two ways to scale a cluster using the CLI:</span><span class="sxs-lookup"><span data-stu-id="531e5-134">There are two ways to scale a cluster using the CLI:</span></span>

- <span data-ttu-id="531e5-135">Autoscale</span><span class="sxs-lookup"><span data-stu-id="531e5-135">Autoscale</span></span>
- <span data-ttu-id="531e5-136">Static scale</span><span class="sxs-lookup"><span data-stu-id="531e5-136">Static scale</span></span>

<span data-ttu-id="531e5-137">Autoscale is active by default when the service is created, and in most situations is the preferred scaling method.</span><span class="sxs-lookup"><span data-stu-id="531e5-137">Autoscale is active by default when the service is created, and in most situations is the preferred scaling method.</span></span>

##### <a name="autoscale"></a><span data-ttu-id="531e5-138">Autoscale</span><span class="sxs-lookup"><span data-stu-id="531e5-138">Autoscale</span></span>

<span data-ttu-id="531e5-139">The following command enables auto-scale, and sets the minimum and maximum number of replicas for the service.</span><span class="sxs-lookup"><span data-stu-id="531e5-139">The following command enables auto-scale, and sets the minimum and maximum number of replicas for the service.</span></span>

```
az ml service update realtime -i <service id> --autoscale-enabled true --autoscale-min-replicas <positive number> --autoscale-max-replicas <positive number>
```

<span data-ttu-id="531e5-140">For example, setting `autoscale-min-replicas` to 5 will create five replicas.</span><span class="sxs-lookup"><span data-stu-id="531e5-140">For example, setting `autoscale-min-replicas` to 5 will create five replicas.</span></span> <span data-ttu-id="531e5-141">To arrive at an optimum number for the web service, set the number to values such as 10 and monitor the number of 503 error messages.</span><span class="sxs-lookup"><span data-stu-id="531e5-141">To arrive at an optimum number for the web service, set the number to values such as 10 and monitor the number of 503 error messages.</span></span> <span data-ttu-id="531e5-142">Then adjust the number accordingly.</span><span class="sxs-lookup"><span data-stu-id="531e5-142">Then adjust the number accordingly.</span></span>


| <span data-ttu-id="531e5-143">Parameter name</span><span class="sxs-lookup"><span data-stu-id="531e5-143">Parameter name</span></span> | <span data-ttu-id="531e5-144">Type</span><span class="sxs-lookup"><span data-stu-id="531e5-144">Type</span></span> | <span data-ttu-id="531e5-145">Description</span><span class="sxs-lookup"><span data-stu-id="531e5-145">Description</span></span> |
|--------------------|--------------------|--------------------|
| `autoscale-enabled` | <span data-ttu-id="531e5-146">boolean</span><span class="sxs-lookup"><span data-stu-id="531e5-146">boolean</span></span> | <span data-ttu-id="531e5-147">Specifies whether Autoscale is enabled.</span><span class="sxs-lookup"><span data-stu-id="531e5-147">Specifies whether Autoscale is enabled.</span></span> <span data-ttu-id="531e5-148">Default: true</span><span class="sxs-lookup"><span data-stu-id="531e5-148">Default: true</span></span> |
| `autoscale-min-replicas` | <span data-ttu-id="531e5-149">integer</span><span class="sxs-lookup"><span data-stu-id="531e5-149">integer</span></span> | <span data-ttu-id="531e5-150">Specifies the minimum number of pods.</span><span class="sxs-lookup"><span data-stu-id="531e5-150">Specifies the minimum number of pods.</span></span> <span data-ttu-id="531e5-151">Must be 0 or greater.</span><span class="sxs-lookup"><span data-stu-id="531e5-151">Must be 0 or greater.</span></span> <span data-ttu-id="531e5-152">Default: 1</span><span class="sxs-lookup"><span data-stu-id="531e5-152">Default: 1</span></span> |
| `autoscale-max-replicas` | <span data-ttu-id="531e5-153">integer</span><span class="sxs-lookup"><span data-stu-id="531e5-153">integer</span></span> | <span data-ttu-id="531e5-154">Specifies the maximum number of pods.</span><span class="sxs-lookup"><span data-stu-id="531e5-154">Specifies the maximum number of pods.</span></span> <span data-ttu-id="531e5-155">Must be 1 or greater.</span><span class="sxs-lookup"><span data-stu-id="531e5-155">Must be 1 or greater.</span></span> <span data-ttu-id="531e5-156">If autoscale-max-replicas is smaller than autoscale-min-replicas, autoscale-max-replicas will be ignored.</span><span class="sxs-lookup"><span data-stu-id="531e5-156">If autoscale-max-replicas is smaller than autoscale-min-replicas, autoscale-max-replicas will be ignored.</span></span> <span data-ttu-id="531e5-157">Default: 10</span><span class="sxs-lookup"><span data-stu-id="531e5-157">Default: 10</span></span> |
| `autoscale-refresh-period-seconds` | <span data-ttu-id="531e5-158">integer</span><span class="sxs-lookup"><span data-stu-id="531e5-158">integer</span></span> | <span data-ttu-id="531e5-159">Specifies the duration in seconds between autoscale refreshes.</span><span class="sxs-lookup"><span data-stu-id="531e5-159">Specifies the duration in seconds between autoscale refreshes.</span></span> <span data-ttu-id="531e5-160">Default: 1</span><span class="sxs-lookup"><span data-stu-id="531e5-160">Default: 1</span></span> |
| `autoscale-target-utilization` | <span data-ttu-id="531e5-161">integer</span><span class="sxs-lookup"><span data-stu-id="531e5-161">integer</span></span> | <span data-ttu-id="531e5-162">Specifies the percent utilization that autoscale targets, between 1 and 100.</span><span class="sxs-lookup"><span data-stu-id="531e5-162">Specifies the percent utilization that autoscale targets, between 1 and 100.</span></span> <span data-ttu-id="531e5-163">Default: 70</span><span class="sxs-lookup"><span data-stu-id="531e5-163">Default: 70</span></span> |

<span data-ttu-id="531e5-164">Autoscale works to ensure the following two conditions:</span><span class="sxs-lookup"><span data-stu-id="531e5-164">Autoscale works to ensure the following two conditions:</span></span>

1. <span data-ttu-id="531e5-165">The target utilization is met</span><span class="sxs-lookup"><span data-stu-id="531e5-165">The target utilization is met</span></span>
2. <span data-ttu-id="531e5-166">Scaling never exceeds the minimum and maximum settings</span><span class="sxs-lookup"><span data-stu-id="531e5-166">Scaling never exceeds the minimum and maximum settings</span></span>

<span data-ttu-id="531e5-167">Services in a cluster compete for cluster resources.</span><span class="sxs-lookup"><span data-stu-id="531e5-167">Services in a cluster compete for cluster resources.</span></span> <span data-ttu-id="531e5-168">An autoscaled service will increase its cluster resource usage as its requests per second (RPS) increases, and will slowly release resources as the RPS decreases.</span><span class="sxs-lookup"><span data-stu-id="531e5-168">An autoscaled service will increase its cluster resource usage as its requests per second (RPS) increases, and will slowly release resources as the RPS decreases.</span></span> <span data-ttu-id="531e5-169">Cluster resources will be acquired on demand as long as such resources exist for the service to acquire.</span><span class="sxs-lookup"><span data-stu-id="531e5-169">Cluster resources will be acquired on demand as long as such resources exist for the service to acquire.</span></span>

<span data-ttu-id="531e5-170">For more information on using the autoscale parameters, see the [Model Management Command Line Interface Reference](model-management-cli-reference.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="531e5-170">For more information on using the autoscale parameters, see the [Model Management Command Line Interface Reference](model-management-cli-reference.md) documentation.</span></span>

##### <a name="static-scale"></a><span data-ttu-id="531e5-171">Static scale</span><span class="sxs-lookup"><span data-stu-id="531e5-171">Static scale</span></span>

<span data-ttu-id="531e5-172">In general, static scaling should be avoided, since it does not allow the cluster size reduction of autoscaling.</span><span class="sxs-lookup"><span data-stu-id="531e5-172">In general, static scaling should be avoided, since it does not allow the cluster size reduction of autoscaling.</span></span> <span data-ttu-id="531e5-173">Even so, in some situations static scaling might be advised.</span><span class="sxs-lookup"><span data-stu-id="531e5-173">Even so, in some situations static scaling might be advised.</span></span> <span data-ttu-id="531e5-174">For example, when a cluster is dedicated to a single service, autoscaling provides no benefit; all cluster resources should be assigned to that service.</span><span class="sxs-lookup"><span data-stu-id="531e5-174">For example, when a cluster is dedicated to a single service, autoscaling provides no benefit; all cluster resources should be assigned to that service.</span></span>

<span data-ttu-id="531e5-175">In order to statically scale a cluster, autoscaling must be turned off.</span><span class="sxs-lookup"><span data-stu-id="531e5-175">In order to statically scale a cluster, autoscaling must be turned off.</span></span> <span data-ttu-id="531e5-176">Disable autoscale with the following command:</span><span class="sxs-lookup"><span data-stu-id="531e5-176">Disable autoscale with the following command:</span></span>

```
az ml service update realtime -i <service id> --autoscale-enabled false
```

<span data-ttu-id="531e5-177">After turning off autoscale, the following command directly scales the number of replicas for a service.</span><span class="sxs-lookup"><span data-stu-id="531e5-177">After turning off autoscale, the following command directly scales the number of replicas for a service.</span></span>

```
az ml service update realtime -i <service id> -z <replica count>
```
 
<span data-ttu-id="531e5-178">For more information on scaling the number of nodes in the cluster, see Scale agent nodes in a Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="531e5-178">For more information on scaling the number of nodes in the cluster, see Scale agent nodes in a Container Service cluster.</span></span>

#### <a name="scaling-number-of-replicas-using-the-kubernetes-dashboard"></a><span data-ttu-id="531e5-179">Scaling number of replicas using the Kubernetes dashboard</span><span class="sxs-lookup"><span data-stu-id="531e5-179">Scaling number of replicas using the Kubernetes dashboard</span></span>

<span data-ttu-id="531e5-180">At the command line, enter:</span><span class="sxs-lookup"><span data-stu-id="531e5-180">At the command line, enter:</span></span>

```
kubectl proxy
```

<span data-ttu-id="531e5-181">On Windows, the Kubernetes install location is not automatically added to the path.</span><span class="sxs-lookup"><span data-stu-id="531e5-181">On Windows, the Kubernetes install location is not automatically added to the path.</span></span> <span data-ttu-id="531e5-182">First navigate to the install folder:</span><span class="sxs-lookup"><span data-stu-id="531e5-182">First navigate to the install folder:</span></span>

```
c:\users\<user name>\bin
```

<span data-ttu-id="531e5-183">Once you run the command, you should see the following informational message:</span><span class="sxs-lookup"><span data-stu-id="531e5-183">Once you run the command, you should see the following informational message:</span></span>

```
Starting to serve on 127.0.0.1:8001
```

<span data-ttu-id="531e5-184">If the port is already in use, you see a message similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="531e5-184">If the port is already in use, you see a message similar to the following example:</span></span>

```
F0612 21:49:22.459111   59621 proxy.go:137] listen tcp 127.0.0.1:8001: bind: address already in use
```

<span data-ttu-id="531e5-185">You can specify an alternate port number using the *--port* parameter.</span><span class="sxs-lookup"><span data-stu-id="531e5-185">You can specify an alternate port number using the *--port* parameter.</span></span>

```
kubectl proxy --port=8010
Starting to serve on 127.0.0.1:8010
```

<span data-ttu-id="531e5-186">Once you have started the dashboard server, open a browser and enter the following URL:</span><span class="sxs-lookup"><span data-stu-id="531e5-186">Once you have started the dashboard server, open a browser and enter the following URL:</span></span>

```
127.0.0.1:<port number>/ui
```

<span data-ttu-id="531e5-187">From the dashboard main screen, click **Deployments** on the left navigation bar.</span><span class="sxs-lookup"><span data-stu-id="531e5-187">From the dashboard main screen, click **Deployments** on the left navigation bar.</span></span> <span data-ttu-id="531e5-188">If the navigation pane does not display, select this icon ![Menu consisting of three short horizontal lines](media/how-to-scale-clusters/icon-hamburger.png) on the upper left.</span><span class="sxs-lookup"><span data-stu-id="531e5-188">If the navigation pane does not display, select this icon ![Menu consisting of three short horizontal lines](media/how-to-scale-clusters/icon-hamburger.png) on the upper left.</span></span>

<span data-ttu-id="531e5-189">Locate the deployment to modify and click this icon ![Menu icon consisting of three vertical dots](media/how-to-scale-clusters/icon-kebab.png) on the right and then click **View/Edit YAML**.</span><span class="sxs-lookup"><span data-stu-id="531e5-189">Locate the deployment to modify and click this icon ![Menu icon consisting of three vertical dots](media/how-to-scale-clusters/icon-kebab.png) on the right and then click **View/Edit YAML**.</span></span>

<span data-ttu-id="531e5-190">On the Edit deployment screen, locate the *spec* node, modify the *replicas* value, and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="531e5-190">On the Edit deployment screen, locate the *spec* node, modify the *replicas* value, and click **Update**.</span></span>
