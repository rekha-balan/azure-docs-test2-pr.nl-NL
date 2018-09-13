---
title: Manage Azure DC/OS cluster with Marathon REST API
description: Deploy containers to an Azure Container Service DC/OS cluster by using the Marathon REST API.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 04/04/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 34fc6f946d172f1431367e84f9d4d8a6855003ed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871423"
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="9049c-103">DC/OS container management through the Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="9049c-103">DC/OS container management through the Marathon REST API</span></span>

<span data-ttu-id="9049c-104">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span><span class="sxs-lookup"><span data-stu-id="9049c-104">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="9049c-105">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span><span class="sxs-lookup"><span data-stu-id="9049c-105">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="9049c-106">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span><span class="sxs-lookup"><span data-stu-id="9049c-106">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9049c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9049c-107">Prerequisites</span></span>

<span data-ttu-id="9049c-108">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="9049c-108">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="9049c-109">You also need to have remote connectivity to this cluster.</span><span class="sxs-lookup"><span data-stu-id="9049c-109">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="9049c-110">For more information on these items, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="9049c-110">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="9049c-111">Deploying an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="9049c-111">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="9049c-112">Connecting to an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="9049c-112">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="9049c-113">Access the DC/OS APIs</span><span class="sxs-lookup"><span data-stu-id="9049c-113">Access the DC/OS APIs</span></span>
<span data-ttu-id="9049c-114">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span><span class="sxs-lookup"><span data-stu-id="9049c-114">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="9049c-115">The examples in this document assume that you are tunneling on port 80.</span><span class="sxs-lookup"><span data-stu-id="9049c-115">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="9049c-116">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="9049c-116">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="9049c-117">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="9049c-117">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="9049c-118">Gather information from DC/OS and Marathon</span><span class="sxs-lookup"><span data-stu-id="9049c-118">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="9049c-119">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span><span class="sxs-lookup"><span data-stu-id="9049c-119">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="9049c-120">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span><span class="sxs-lookup"><span data-stu-id="9049c-120">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="9049c-121">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span><span class="sxs-lookup"><span data-stu-id="9049c-121">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="9049c-122">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="9049c-122">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="9049c-123">If this is a new cluster, you see an empty array for apps.</span><span class="sxs-lookup"><span data-stu-id="9049c-123">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="9049c-124">Deploy a Docker-formatted container</span><span class="sxs-lookup"><span data-stu-id="9049c-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="9049c-125">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span><span class="sxs-lookup"><span data-stu-id="9049c-125">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="9049c-126">The following sample deploys an Nginx container to a private agent in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9049c-126">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

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

<span data-ttu-id="9049c-127">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="9049c-127">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="9049c-128">Next, to deploy the container, run the following command.</span><span class="sxs-lookup"><span data-stu-id="9049c-128">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="9049c-129">Specify the name of the JSON file (`marathon.json` in this example).</span><span class="sxs-lookup"><span data-stu-id="9049c-129">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="9049c-130">The output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="9049c-130">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="9049c-131">Now, if you query Marathon for applications, this new application appears in the output.</span><span class="sxs-lookup"><span data-stu-id="9049c-131">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="9049c-132">Reach the container</span><span class="sxs-lookup"><span data-stu-id="9049c-132">Reach the container</span></span>

<span data-ttu-id="9049c-133">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9049c-133">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="9049c-134">To find the host and port where the container is running, query Marathon for the running tasks:</span><span class="sxs-lookup"><span data-stu-id="9049c-134">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="9049c-135">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span><span class="sxs-lookup"><span data-stu-id="9049c-135">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="9049c-136">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span><span class="sxs-lookup"><span data-stu-id="9049c-136">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="9049c-137">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span><span class="sxs-lookup"><span data-stu-id="9049c-137">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="9049c-138">The Nginx server output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="9049c-138">The Nginx server output is similar to the following:</span></span>

![Nginx from container](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="9049c-140">Scale your containers</span><span class="sxs-lookup"><span data-stu-id="9049c-140">Scale your containers</span></span>
<span data-ttu-id="9049c-141">You can use the Marathon API to scale out or scale in application deployments.</span><span class="sxs-lookup"><span data-stu-id="9049c-141">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="9049c-142">In the previous example, you deployed one instance of an application.</span><span class="sxs-lookup"><span data-stu-id="9049c-142">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="9049c-143">Let's scale this out to three instances of an application.</span><span class="sxs-lookup"><span data-stu-id="9049c-143">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="9049c-144">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="9049c-144">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="9049c-145">From your tunneled connection, run the following command to scale out the application.</span><span class="sxs-lookup"><span data-stu-id="9049c-145">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="9049c-146">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span><span class="sxs-lookup"><span data-stu-id="9049c-146">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="9049c-147">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="9049c-147">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="9049c-148">Finally, query the Marathon endpoint for applications.</span><span class="sxs-lookup"><span data-stu-id="9049c-148">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="9049c-149">You see that there are now three Nginx containers.</span><span class="sxs-lookup"><span data-stu-id="9049c-149">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="9049c-150">Equivalent PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="9049c-150">Equivalent PowerShell commands</span></span>
<span data-ttu-id="9049c-151">You can perform these same actions by using PowerShell commands on a Windows system.</span><span class="sxs-lookup"><span data-stu-id="9049c-151">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="9049c-152">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span><span class="sxs-lookup"><span data-stu-id="9049c-152">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="9049c-153">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span><span class="sxs-lookup"><span data-stu-id="9049c-153">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="9049c-154">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span><span class="sxs-lookup"><span data-stu-id="9049c-154">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

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

<span data-ttu-id="9049c-155">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="9049c-155">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="9049c-156">Next, to deploy the container, run the following command.</span><span class="sxs-lookup"><span data-stu-id="9049c-156">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="9049c-157">Specify the path to the JSON file (`marathon.json` in this example).</span><span class="sxs-lookup"><span data-stu-id="9049c-157">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="9049c-158">You can also use the Marathon API to scale out or scale in application deployments.</span><span class="sxs-lookup"><span data-stu-id="9049c-158">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="9049c-159">In the previous example, you deployed one instance of an application.</span><span class="sxs-lookup"><span data-stu-id="9049c-159">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="9049c-160">Let's scale this out to three instances of an application.</span><span class="sxs-lookup"><span data-stu-id="9049c-160">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="9049c-161">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span><span class="sxs-lookup"><span data-stu-id="9049c-161">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="9049c-162">Run the following command to scale out the application:</span><span class="sxs-lookup"><span data-stu-id="9049c-162">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="9049c-163">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span><span class="sxs-lookup"><span data-stu-id="9049c-163">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="9049c-164">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="9049c-164">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="9049c-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="9049c-165">Next steps</span></span>
* [<span data-ttu-id="9049c-166">Read more about the Mesos HTTP endpoints</span><span class="sxs-lookup"><span data-stu-id="9049c-166">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="9049c-167">Read more about the Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="9049c-167">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

