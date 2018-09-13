---
title: Manage Azure DC/OS cluster with Marathon REST API | Microsoft Docs
description: Deploy containers to an Azure Container Service DC/OS cluster by using the Marathon REST API.
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.openlocfilehash: 78c8e2560fd4f127582c21990e12e3a76e1a6d57
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556774"
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="0a530-104">DC/OS container management through the Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="0a530-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="0a530-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span><span class="sxs-lookup"><span data-stu-id="0a530-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="0a530-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span><span class="sxs-lookup"><span data-stu-id="0a530-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="0a530-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span><span class="sxs-lookup"><span data-stu-id="0a530-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0a530-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a530-108">Prerequisites</span></span>

<span data-ttu-id="0a530-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="0a530-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="0a530-110">You also need to have remote connectivity to this cluster.</span><span class="sxs-lookup"><span data-stu-id="0a530-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="0a530-111">For more information on these items, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="0a530-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="0a530-112">Deploying an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="0a530-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="0a530-113">Connecting to an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="0a530-113">Connecting to an Azure Container Service cluster</span></span>](container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="0a530-114">Access the DC/OS APIs</span><span class="sxs-lookup"><span data-stu-id="0a530-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="0a530-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span><span class="sxs-lookup"><span data-stu-id="0a530-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="0a530-116">The examples in this document assume that you are tunneling on port 80.</span><span class="sxs-lookup"><span data-stu-id="0a530-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="0a530-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="0a530-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="0a530-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="0a530-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="0a530-119">Gather information from DC/OS and Marathon</span><span class="sxs-lookup"><span data-stu-id="0a530-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="0a530-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span><span class="sxs-lookup"><span data-stu-id="0a530-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="0a530-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span><span class="sxs-lookup"><span data-stu-id="0a530-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="0a530-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span><span class="sxs-lookup"><span data-stu-id="0a530-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="0a530-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="0a530-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="0a530-124">If this is a new cluster, you see an empty array for apps.</span><span class="sxs-lookup"><span data-stu-id="0a530-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="0a530-125">Deploy a Docker-formatted container</span><span class="sxs-lookup"><span data-stu-id="0a530-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="0a530-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span><span class="sxs-lookup"><span data-stu-id="0a530-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="0a530-127">The following sample deploys an Nginx container to a private agent in the cluster.</span><span class="sxs-lookup"><span data-stu-id="0a530-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="0a530-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="0a530-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="0a530-129">Next, to deploy the container, run the following command.</span><span class="sxs-lookup"><span data-stu-id="0a530-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="0a530-130">Specify the name of the JSON file (`marathon.json` in this example).</span><span class="sxs-lookup"><span data-stu-id="0a530-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="0a530-131">The output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="0a530-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="0a530-132">Now, if you query Marathon for applications, this new application appears in the output.</span><span class="sxs-lookup"><span data-stu-id="0a530-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="0a530-133">Reach the container</span><span class="sxs-lookup"><span data-stu-id="0a530-133">Reach the container</span></span>

<span data-ttu-id="0a530-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span><span class="sxs-lookup"><span data-stu-id="0a530-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="0a530-135">To find the host and port where the container is running, query Marathon for the running tasks:</span><span class="sxs-lookup"><span data-stu-id="0a530-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="0a530-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span><span class="sxs-lookup"><span data-stu-id="0a530-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="0a530-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span><span class="sxs-lookup"><span data-stu-id="0a530-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="0a530-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span><span class="sxs-lookup"><span data-stu-id="0a530-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="0a530-139">The Nginx server output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="0a530-139">The Nginx server output is similar to the following:</span></span>

![Nginx from container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="0a530-141">Scale your containers</span><span class="sxs-lookup"><span data-stu-id="0a530-141">Scale your containers</span></span>
<span data-ttu-id="0a530-142">You can use the Marathon API to scale out or scale in application deployments.</span><span class="sxs-lookup"><span data-stu-id="0a530-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="0a530-143">In the previous example, you deployed one instance of an application.</span><span class="sxs-lookup"><span data-stu-id="0a530-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="0a530-144">Let's scale this out to three instances of an application.</span><span class="sxs-lookup"><span data-stu-id="0a530-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="0a530-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="0a530-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="0a530-146">From your tunneled connection, run the following command to scale out the application.</span><span class="sxs-lookup"><span data-stu-id="0a530-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="0a530-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span><span class="sxs-lookup"><span data-stu-id="0a530-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="0a530-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="0a530-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="0a530-149">Finally, query the Marathon endpoint for applications.</span><span class="sxs-lookup"><span data-stu-id="0a530-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="0a530-150">You see that there are now three Nginx containers.</span><span class="sxs-lookup"><span data-stu-id="0a530-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="0a530-151">Equivalent PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="0a530-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="0a530-152">You can perform these same actions by using PowerShell commands on a Windows system.</span><span class="sxs-lookup"><span data-stu-id="0a530-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="0a530-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span><span class="sxs-lookup"><span data-stu-id="0a530-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="0a530-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span><span class="sxs-lookup"><span data-stu-id="0a530-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="0a530-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span><span class="sxs-lookup"><span data-stu-id="0a530-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="0a530-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="0a530-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="0a530-157">Next, to deploy the container, run the following command.</span><span class="sxs-lookup"><span data-stu-id="0a530-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="0a530-158">Specify the path to the JSON file (`marathon.json` in this example).</span><span class="sxs-lookup"><span data-stu-id="0a530-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="0a530-159">You can also use the Marathon API to scale out or scale in application deployments.</span><span class="sxs-lookup"><span data-stu-id="0a530-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="0a530-160">In the previous example, you deployed one instance of an application.</span><span class="sxs-lookup"><span data-stu-id="0a530-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="0a530-161">Let's scale this out to three instances of an application.</span><span class="sxs-lookup"><span data-stu-id="0a530-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="0a530-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="0a530-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="0a530-163">Run the following command to scale out the application:</span><span class="sxs-lookup"><span data-stu-id="0a530-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="0a530-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span><span class="sxs-lookup"><span data-stu-id="0a530-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="0a530-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="0a530-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="0a530-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a530-166">Next steps</span></span>
* [<span data-ttu-id="0a530-167">Read more about the Mesos HTTP endpoints</span><span class="sxs-lookup"><span data-stu-id="0a530-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="0a530-168">Read more about the Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="0a530-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)


