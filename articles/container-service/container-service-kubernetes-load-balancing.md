---
title: Load balance Kubernetes containers in Azure | Microsoft Docs
description: Connect externally and load balance across multiple containers in a Kubernetes cluster in Azure Container Service.
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, Micro-services, Kubernetes, Azure
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: danlep
ms.openlocfilehash: 63c4533a63a811c6c711794bc41d3c5eccaa7296
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554666"
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="f8b19-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f8b19-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="f8b19-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="f8b19-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="f8b19-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span><span class="sxs-lookup"><span data-stu-id="f8b19-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="f8b19-107">You can set up a Kubernetes service to use [Azure Load Balancer](../load-balancer/load-balancer-overview.md) to manage external network (TCP or UDP) traffic.</span><span class="sxs-lookup"><span data-stu-id="f8b19-107">You can set up a Kubernetes service to use [Azure Load Balancer](../load-balancer/load-balancer-overview.md) to manage external network (TCP or UDP) traffic.</span></span> <span data-ttu-id="f8b19-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span><span class="sxs-lookup"><span data-stu-id="f8b19-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8b19-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f8b19-109">Prerequisites</span></span>
* <span data-ttu-id="f8b19-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f8b19-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="f8b19-111">[Connect your client](container-service-connect.md) to your cluster</span><span class="sxs-lookup"><span data-stu-id="f8b19-111">[Connect your client](container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="f8b19-112">Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="f8b19-112">Azure load balancer</span></span>

<span data-ttu-id="f8b19-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span><span class="sxs-lookup"><span data-stu-id="f8b19-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="f8b19-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 (TCP, UDP) load balancer.</span><span class="sxs-lookup"><span data-stu-id="f8b19-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 (TCP, UDP) load balancer.</span></span>

<span data-ttu-id="f8b19-115">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span><span class="sxs-lookup"><span data-stu-id="f8b19-115">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="f8b19-116">To configure the load balancer, set the service `type` to `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-116">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="f8b19-117">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span><span class="sxs-lookup"><span data-stu-id="f8b19-117">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="f8b19-118">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-118">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="f8b19-119">(After trying the examples, delete the deployments if you no longer need them.)</span><span class="sxs-lookup"><span data-stu-id="f8b19-119">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="f8b19-120">Example: Use the `kubectl expose` command</span><span class="sxs-lookup"><span data-stu-id="f8b19-120">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="f8b19-121">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span><span class="sxs-lookup"><span data-stu-id="f8b19-121">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="f8b19-122">Here are the steps :</span><span class="sxs-lookup"><span data-stu-id="f8b19-122">Here are the steps :</span></span>

1. <span data-ttu-id="f8b19-123">Start a new container deployment.</span><span class="sxs-lookup"><span data-stu-id="f8b19-123">Start a new container deployment.</span></span> <span data-ttu-id="f8b19-124">For example, the following command starts a new deployment called `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-124">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="f8b19-125">The deployment consists of three containers based on the Docker image for the Nginx web server.</span><span class="sxs-lookup"><span data-stu-id="f8b19-125">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="f8b19-126">Verify that the containers are running.</span><span class="sxs-lookup"><span data-stu-id="f8b19-126">Verify that the containers are running.</span></span> <span data-ttu-id="f8b19-127">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f8b19-127">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![Get Nginx containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="f8b19-129">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-129">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="f8b19-130">The following command exposes the Nginx server on port 80:</span><span class="sxs-lookup"><span data-stu-id="f8b19-130">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="f8b19-131">Type `kubectl get svc` to see the state of the services in the cluster.</span><span class="sxs-lookup"><span data-stu-id="f8b19-131">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="f8b19-132">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-132">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="f8b19-133">After a few minutes, the external IP address is configured:</span><span class="sxs-lookup"><span data-stu-id="f8b19-133">After a few minutes, the external IP address is configured:</span></span> 

    ![Configure Azure load balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="f8b19-135">Verify that you can access the service at the external IP address.</span><span class="sxs-lookup"><span data-stu-id="f8b19-135">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="f8b19-136">For example, open a web browser to the IP address shown.</span><span class="sxs-lookup"><span data-stu-id="f8b19-136">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="f8b19-137">The browser shows the Nginx web server running in one of the containers.</span><span class="sxs-lookup"><span data-stu-id="f8b19-137">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="f8b19-138">Or, run the `curl` or `wget` command.</span><span class="sxs-lookup"><span data-stu-id="f8b19-138">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="f8b19-139">For example:</span><span class="sxs-lookup"><span data-stu-id="f8b19-139">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="f8b19-140">You should see output similar to:</span><span class="sxs-lookup"><span data-stu-id="f8b19-140">You should see output similar to:</span></span>

    ![Access Nginx with curl](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="f8b19-142">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8b19-142">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="f8b19-143">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span><span class="sxs-lookup"><span data-stu-id="f8b19-143">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="f8b19-144">Its name should be the same as the container service.</span><span class="sxs-lookup"><span data-stu-id="f8b19-144">Its name should be the same as the container service.</span></span> <span data-ttu-id="f8b19-145">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span><span class="sxs-lookup"><span data-stu-id="f8b19-145">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![Load balancer in resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="f8b19-147">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span><span class="sxs-lookup"><span data-stu-id="f8b19-147">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![Load balancer rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="f8b19-149">Example: Specify `type: LoadBalancer` in the service configuration file</span><span class="sxs-lookup"><span data-stu-id="f8b19-149">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="f8b19-150">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span><span class="sxs-lookup"><span data-stu-id="f8b19-150">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="f8b19-151">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="f8b19-151">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="f8b19-152">This example is a multi-tier web app based on  Redis and PHP Docker images.</span><span class="sxs-lookup"><span data-stu-id="f8b19-152">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="f8b19-153">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="f8b19-153">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="f8b19-154">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="f8b19-154">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="f8b19-155">Browse for the `spec` for the `frontend` service.</span><span class="sxs-lookup"><span data-stu-id="f8b19-155">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="f8b19-156">Uncomment the line `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-156">Uncomment the line `type: LoadBalancer`.</span></span>

    ![Load balancer in service configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="f8b19-158">Save the file, and deploy the app by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f8b19-158">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="f8b19-159">Type `kubectl get svc` to see the state of the services in the cluster.</span><span class="sxs-lookup"><span data-stu-id="f8b19-159">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="f8b19-160">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-160">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="f8b19-161">After a few minutes, the external IP address is configured:</span><span class="sxs-lookup"><span data-stu-id="f8b19-161">After a few minutes, the external IP address is configured:</span></span> 

    ![Configure Azure load balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="f8b19-163">Verify that you can access the service at the external IP address.</span><span class="sxs-lookup"><span data-stu-id="f8b19-163">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="f8b19-164">For example, you can open a web browser to the external IP address of the service.</span><span class="sxs-lookup"><span data-stu-id="f8b19-164">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![Access guestbook externally](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="f8b19-166">You can add guestbook entries.</span><span class="sxs-lookup"><span data-stu-id="f8b19-166">You can add guestbook entries.</span></span>

7. <span data-ttu-id="f8b19-167">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8b19-167">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f8b19-168">See the steps in the previous example.</span><span class="sxs-lookup"><span data-stu-id="f8b19-168">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="f8b19-169">Considerations</span><span class="sxs-lookup"><span data-stu-id="f8b19-169">Considerations</span></span>

* <span data-ttu-id="f8b19-170">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span><span class="sxs-lookup"><span data-stu-id="f8b19-170">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="f8b19-171">Every service is automatically assigned its own virtual IP address in the load balancer.</span><span class="sxs-lookup"><span data-stu-id="f8b19-171">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="f8b19-172">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span><span class="sxs-lookup"><span data-stu-id="f8b19-172">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="f8b19-173">HTTP or HTTPS traffic</span><span class="sxs-lookup"><span data-stu-id="f8b19-173">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="f8b19-174">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span><span class="sxs-lookup"><span data-stu-id="f8b19-174">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="f8b19-175">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span><span class="sxs-lookup"><span data-stu-id="f8b19-175">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="f8b19-176">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span><span class="sxs-lookup"><span data-stu-id="f8b19-176">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="f8b19-177">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span><span class="sxs-lookup"><span data-stu-id="f8b19-177">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="f8b19-178">Several controller implementations are available.</span><span class="sxs-lookup"><span data-stu-id="f8b19-178">Several controller implementations are available.</span></span> <span data-ttu-id="f8b19-179">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="f8b19-179">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="f8b19-180">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="f8b19-180">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8b19-181">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f8b19-181">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="f8b19-182">This configures the Azure load balancer to route traffic to the controller.</span><span class="sxs-lookup"><span data-stu-id="f8b19-182">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="f8b19-183">For more information, see the previous section.</span><span class="sxs-lookup"><span data-stu-id="f8b19-183">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f8b19-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8b19-184">Next steps</span></span>

* <span data-ttu-id="f8b19-185">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="f8b19-185">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="f8b19-186">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="f8b19-186">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="f8b19-187">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="f8b19-187">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>









