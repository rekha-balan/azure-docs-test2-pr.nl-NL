---
title: Using ACR with an Azure DC/OS cluster | Microsoft Docs
description: Use an Azure Container Registry with a DC/OS cluster in Azure Container Service
services: container-service
documentationcenter: ''
author: julienstroheker
manager: dcaro
editor: ''
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, Containers, Micro-services, Mesos, Azure, FileShare, cifs
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.openlocfilehash: a8a3716f8d03b596285026426c7514b7b642cb25
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563746"
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="a04c5-104">Use ACR with a DC/OS cluster to deploy your application</span><span class="sxs-lookup"><span data-stu-id="a04c5-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="a04c5-105">In this article, we'll explore how to use a private container register such as ACR (Azure Container Registry) with a DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="a04c5-105">In this article, we'll explore how to use a private container register such as ACR (Azure Container Registry) with a DC/OS cluster.</span></span> <span data-ttu-id="a04c5-106">Using ACR allows you to store images privately and keep the control on it such as the versions and/or the updates for example.</span><span class="sxs-lookup"><span data-stu-id="a04c5-106">Using ACR allows you to store images privately and keep the control on it such as the versions and/or the updates for example.</span></span>

<span data-ttu-id="a04c5-107">Before working through this example, you need:</span><span class="sxs-lookup"><span data-stu-id="a04c5-107">Before working through this example, you need:</span></span> 
* <span data-ttu-id="a04c5-108">A DC/OS cluster that is configured in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="a04c5-108">A DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="a04c5-109">See [Deploy an Azure Container Service cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a04c5-109">See [Deploy an Azure Container Service cluster](container-service-deployment.md).</span></span>
* <span data-ttu-id="a04c5-110">A Azure Container Service deployed.</span><span class="sxs-lookup"><span data-stu-id="a04c5-110">A Azure Container Service deployed.</span></span> <span data-ttu-id="a04c5-111">See [Create a private Docker container registry using the Azure portal](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-portal) or [Create a private Docker container registry using the Azure CLI 2.0](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="a04c5-111">See [Create a private Docker container registry using the Azure portal](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-portal) or [Create a private Docker container registry using the Azure CLI 2.0](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-azure-cli)</span></span>
* <span data-ttu-id="a04c5-112">A File share that is configured inside your DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="a04c5-112">A File share that is configured inside your DC/OS cluster.</span></span> <span data-ttu-id="a04c5-113">See [Create and mount a file share to a DC/OS cluster](container-service-dcos-fileshare.md)</span><span class="sxs-lookup"><span data-stu-id="a04c5-113">See [Create and mount a file share to a DC/OS cluster](container-service-dcos-fileshare.md)</span></span>
* <span data-ttu-id="a04c5-114">To understand how to deploy a Docker image in a DC/OS cluster by using the [Web UI](container-service-mesos-marathon-ui.md) or the [REST API](container-service-mesos-marathon-rest.md)</span><span class="sxs-lookup"><span data-stu-id="a04c5-114">To understand how to deploy a Docker image in a DC/OS cluster by using the [Web UI](container-service-mesos-marathon-ui.md) or the [REST API](container-service-mesos-marathon-rest.md)</span></span>

## <a name="manage-the-authentication-inside-your-cluster"></a><span data-ttu-id="a04c5-115">Manage the authentication inside your cluster</span><span class="sxs-lookup"><span data-stu-id="a04c5-115">Manage the authentication inside your cluster</span></span>

<span data-ttu-id="a04c5-116">The conventional way to push and pull image from a private registry is to be, first, authenticated on it.</span><span class="sxs-lookup"><span data-stu-id="a04c5-116">The conventional way to push and pull image from a private registry is to be, first, authenticated on it.</span></span> <span data-ttu-id="a04c5-117">To do it, you have to use the `docker login` command line on any docker client process who will need to use your private registry.</span><span class="sxs-lookup"><span data-stu-id="a04c5-117">To do it, you have to use the `docker login` command line on any docker client process who will need to use your private registry.</span></span>
<span data-ttu-id="a04c5-118">When it comes to the production world, using DC/OS in our case, you want to make sure that you are able to pull images from any node.</span><span class="sxs-lookup"><span data-stu-id="a04c5-118">When it comes to the production world, using DC/OS in our case, you want to make sure that you are able to pull images from any node.</span></span> <span data-ttu-id="a04c5-119">It means that you want to automate the authentication process, and don't run the command line on each machines, because as you can imagine, depending on the size of your cluster, it could be a problematic and heavy operation.</span><span class="sxs-lookup"><span data-stu-id="a04c5-119">It means that you want to automate the authentication process, and don't run the command line on each machines, because as you can imagine, depending on the size of your cluster, it could be a problematic and heavy operation.</span></span> 

<span data-ttu-id="a04c5-120">Assuming that you already [setup a file share inside your DC/OS](container-service-dcos-fileshare.md), we will leverage it by doing:</span><span class="sxs-lookup"><span data-stu-id="a04c5-120">Assuming that you already [setup a file share inside your DC/OS](container-service-dcos-fileshare.md), we will leverage it by doing:</span></span>

### <a name="from-any-client-machine-recommended-method"></a><span data-ttu-id="a04c5-121">From any client machine [Recommended Method]</span><span class="sxs-lookup"><span data-stu-id="a04c5-121">From any client machine [Recommended Method]</span></span>

<span data-ttu-id="a04c5-122">The following commands are runnable on any environments (Windows/Mac/Linux)  :</span><span class="sxs-lookup"><span data-stu-id="a04c5-122">The following commands are runnable on any environments (Windows/Mac/Linux)  :</span></span>

1. <span data-ttu-id="a04c5-123">Make sure that you are meeting the following prerequisites :</span><span class="sxs-lookup"><span data-stu-id="a04c5-123">Make sure that you are meeting the following prerequisites :</span></span>
  * <span data-ttu-id="a04c5-124">TAR tool</span><span class="sxs-lookup"><span data-stu-id="a04c5-124">TAR tool</span></span>
    * [<span data-ttu-id="a04c5-125">Windows</span><span class="sxs-lookup"><span data-stu-id="a04c5-125">Windows</span></span>](http://gnuwin32.sourceforge.net/packages/gtar.htm)
  * <span data-ttu-id="a04c5-126">Docker</span><span class="sxs-lookup"><span data-stu-id="a04c5-126">Docker</span></span> 
    * [<span data-ttu-id="a04c5-127">Windows</span><span class="sxs-lookup"><span data-stu-id="a04c5-127">Windows</span></span>](https://www.docker.com/docker-windows)
    * [<span data-ttu-id="a04c5-128">MAC</span><span class="sxs-lookup"><span data-stu-id="a04c5-128">MAC</span></span>](https://www.docker.com/docker-mac)
    * [<span data-ttu-id="a04c5-129">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a04c5-129">Ubuntu</span></span>](https://www.docker.com/docker-ubuntu)
    * [<span data-ttu-id="a04c5-130">Others</span><span class="sxs-lookup"><span data-stu-id="a04c5-130">Others</span></span>](https://www.docker.com/get-docker)
  * <span data-ttu-id="a04c5-131">File share mounted inside your cluster, [with the following method](container-service-dcos-fileshare.md)</span><span class="sxs-lookup"><span data-stu-id="a04c5-131">File share mounted inside your cluster, [with the following method](container-service-dcos-fileshare.md)</span></span>

2. <span data-ttu-id="a04c5-132">Initiate the authentication to your ACR service by using the following command with your favorite terminal: `sudo docker login --username=<USERNAME> --password=<PASSWORD> <ACR-REGISTRY-NAME>.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="a04c5-132">Initiate the authentication to your ACR service by using the following command with your favorite terminal: `sudo docker login --username=<USERNAME> --password=<PASSWORD> <ACR-REGISTRY-NAME>.azurecr.io`.</span></span> <span data-ttu-id="a04c5-133">You have to replace the `USERNAME`, `PASSWORD`and `ACR-REGISTRY-NAME` variables with the values provided on your Azure portal</span><span class="sxs-lookup"><span data-stu-id="a04c5-133">You have to replace the `USERNAME`, `PASSWORD`and `ACR-REGISTRY-NAME` variables with the values provided on your Azure portal</span></span>

3. <span data-ttu-id="a04c5-134">It is interesting to know that when you are doing a `docker login` operation, the values are stored locally on the machine under your home folder (`cd ~/.docker` on Mac and Linux or `cd %HOMEPATH%` on Windows).</span><span class="sxs-lookup"><span data-stu-id="a04c5-134">It is interesting to know that when you are doing a `docker login` operation, the values are stored locally on the machine under your home folder (`cd ~/.docker` on Mac and Linux or `cd %HOMEPATH%` on Windows).</span></span> <span data-ttu-id="a04c5-135">We will compress the contain of this folder by using the `tar czf` command.</span><span class="sxs-lookup"><span data-stu-id="a04c5-135">We will compress the contain of this folder by using the `tar czf` command.</span></span>

4. <span data-ttu-id="a04c5-136">The final step is to copy the tar file that we just created, inside the file share [that you should have created as prerequisite](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="a04c5-136">The final step is to copy the tar file that we just created, inside the file share [that you should have created as prerequisite](container-service-dcos-fileshare.md).</span></span> <span data-ttu-id="a04c5-137">You can do it by using the Azure-CLI with the following command `az storage file upload -s <shareName> --account-name <storageAccountName> --account-key <storageAccountKey> -source <pathToTheTarFile>`</span><span class="sxs-lookup"><span data-stu-id="a04c5-137">You can do it by using the Azure-CLI with the following command `az storage file upload -s <shareName> --account-name <storageAccountName> --account-key <storageAccountKey> -source <pathToTheTarFile>`</span></span>

<span data-ttu-id="a04c5-138">To wrap up, here is an example using the following setup (Using a windows environment):</span><span class="sxs-lookup"><span data-stu-id="a04c5-138">To wrap up, here is an example using the following setup (Using a windows environment):</span></span>
* <span data-ttu-id="a04c5-139">ACR name: **`demodcos`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-139">ACR name: **`demodcos`**</span></span>
* <span data-ttu-id="a04c5-140">Username: **`demodcos`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-140">Username: **`demodcos`**</span></span>
* <span data-ttu-id="a04c5-141">Password: **`+js+/=I1=L+D=+eRpU+/=wI/AjvDo=J0`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-141">Password: **`+js+/=I1=L+D=+eRpU+/=wI/AjvDo=J0`**</span></span>
* <span data-ttu-id="a04c5-142">Storage Account Name: **`anystorageaccountname`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-142">Storage Account Name: **`anystorageaccountname`**</span></span>
* <span data-ttu-id="a04c5-143">Storage Account Key: **`aYGl6Nys4De5J3VPldT1rXxz2+VjgO7dgWytnoWClurZ/l8iO5c5N8xXNS6mpJhSc9xh+7zkT7Mr+xIT4OIVMg==`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-143">Storage Account Key: **`aYGl6Nys4De5J3VPldT1rXxz2+VjgO7dgWytnoWClurZ/l8iO5c5N8xXNS6mpJhSc9xh+7zkT7Mr+xIT4OIVMg==`**</span></span>
* <span data-ttu-id="a04c5-144">Share name created inside the storage account: **`share`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-144">Share name created inside the storage account: **`share`**</span></span>
* <span data-ttu-id="a04c5-145">Path of the tar archive to upload: **`%HOMEPATH%/.docker/docker.tar.gz`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-145">Path of the tar archive to upload: **`%HOMEPATH%/.docker/docker.tar.gz`**</span></span>

```bash
# Changing directory to the home folder of the default user
cd %HOMEPATH%

# Authentication into my ACR
docker login --username=demodcos --password=+js+/=I1=L+D=+eRpU+/=wI/AjvDo=J0 demodcos.azurecr.io

# Tar the contains of the .docker folder
tar czf docker.tar.gz .docker

# Upload the tar archive in the fileshare
az storage file upload -s share --account-name anystorageaccountname --account-key aYGl6Nys4De5J3VPldT1rXxz2+VjgO7dgWytnoWClurZ/l8iO5c5N8xXNS6mpJhSc9xh+7zkT7Mr+xIT4OIVMg== --source %HOMEPATH%/docker.tar.gz
```

### <a name="from-the-master-not-recommended-method"></a><span data-ttu-id="a04c5-146">From the master [Not recommended Method]</span><span class="sxs-lookup"><span data-stu-id="a04c5-146">From the master [Not recommended Method]</span></span>

<span data-ttu-id="a04c5-147">Executing operation from the master are not recommended to avoid mistakes and impact on the whole environments.</span><span class="sxs-lookup"><span data-stu-id="a04c5-147">Executing operation from the master are not recommended to avoid mistakes and impact on the whole environments.</span></span>

1. <span data-ttu-id="a04c5-148">First, SSH to the master (or the first master) of your DC/OS-based cluster.</span><span class="sxs-lookup"><span data-stu-id="a04c5-148">First, SSH to the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="a04c5-149">For example, `ssh userName@masterFQDN –A –p 22`, where the masterFQDN is the fully qualified domain name of the master VM.</span><span class="sxs-lookup"><span data-stu-id="a04c5-149">For example, `ssh userName@masterFQDN –A –p 22`, where the masterFQDN is the fully qualified domain name of the master VM.</span></span> [<span data-ttu-id="a04c5-150">More infos by clicking here</span><span class="sxs-lookup"><span data-stu-id="a04c5-150">More infos by clicking here</span></span>](https://docs.microsoft.com/azure/container-service/container-service-connect#connect-to-a-dcos-or-swarm-cluster)

2. <span data-ttu-id="a04c5-151">Initiate the authentication to your ACR service by using the following command: `sudo docker login --username=<USERNAME> --password=<PASSWORD> <ACR-REGISTRY-NAME>.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="a04c5-151">Initiate the authentication to your ACR service by using the following command: `sudo docker login --username=<USERNAME> --password=<PASSWORD> <ACR-REGISTRY-NAME>.azurecr.io`.</span></span> <span data-ttu-id="a04c5-152">You have to replace the `USERNAME`, `PASSWORD`and `ACR-REGISTRY-NAME` variables with the values provided on your Azure portal</span><span class="sxs-lookup"><span data-stu-id="a04c5-152">You have to replace the `USERNAME`, `PASSWORD`and `ACR-REGISTRY-NAME` variables with the values provided on your Azure portal</span></span>

3. <span data-ttu-id="a04c5-153">It is interesting to know that when you are doing a `docker login` operation, the values are stored locally on the machine under your home folder `~/.docker`.</span><span class="sxs-lookup"><span data-stu-id="a04c5-153">It is interesting to know that when you are doing a `docker login` operation, the values are stored locally on the machine under your home folder `~/.docker`.</span></span> <span data-ttu-id="a04c5-154">We will compress the contain of this folder by using the `tar czf` command.</span><span class="sxs-lookup"><span data-stu-id="a04c5-154">We will compress the contain of this folder by using the `tar czf` command.</span></span>

4. <span data-ttu-id="a04c5-155">The final step is to copy the tar file that we just created, inside the file share.</span><span class="sxs-lookup"><span data-stu-id="a04c5-155">The final step is to copy the tar file that we just created, inside the file share.</span></span> <span data-ttu-id="a04c5-156">This operation will allow, at all the virtual machines inside our cluster, to use this credential and be authenticated on your Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a04c5-156">This operation will allow, at all the virtual machines inside our cluster, to use this credential and be authenticated on your Azure Container Registry.</span></span>

<span data-ttu-id="a04c5-157">To wrap up, here is an example using the following setup:</span><span class="sxs-lookup"><span data-stu-id="a04c5-157">To wrap up, here is an example using the following setup:</span></span>
* <span data-ttu-id="a04c5-158">ACR name: **`demodcos`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-158">ACR name: **`demodcos`**</span></span>
* <span data-ttu-id="a04c5-159">Username: **`demodcos`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-159">Username: **`demodcos`**</span></span>
* <span data-ttu-id="a04c5-160">Password: **`+js+/=I1=L+D=+eRpU+/=wI/AjvDo=J0`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-160">Password: **`+js+/=I1=L+D=+eRpU+/=wI/AjvDo=J0`**</span></span>
* <span data-ttu-id="a04c5-161">Mount point inside the cluster: **`/mnt/share`**</span><span class="sxs-lookup"><span data-stu-id="a04c5-161">Mount point inside the cluster: **`/mnt/share`**</span></span>

```bash
# Changing directory to the home folder of the default user
cd ~

# Authentication into my ACR
sudo docker login --username=demodcos --password=+js+/=I1=L+D=+eRpU+/=wI/AjvDo=J0 demodcos.azurecr.io

# Tar the contains of the .docker folder
sudo tar czf docker.tar.gz .docker

# Copy of the tar file in the file share of my cluster
sudo cp docker.tar.gz /mnt/share
```


## <a name="deploy-an-image-from-acr-with-marathon"></a><span data-ttu-id="a04c5-162">Deploy an image from ACR with Marathon</span><span class="sxs-lookup"><span data-stu-id="a04c5-162">Deploy an image from ACR with Marathon</span></span>

<span data-ttu-id="a04c5-163">Supposedly you already pushed the images that you want to deploy inside your container registry.</span><span class="sxs-lookup"><span data-stu-id="a04c5-163">Supposedly you already pushed the images that you want to deploy inside your container registry.</span></span> <span data-ttu-id="a04c5-164">See [Push your first image to a private Docker container registry using the Docker CLI](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-docker-cli)</span><span class="sxs-lookup"><span data-stu-id="a04c5-164">See [Push your first image to a private Docker container registry using the Docker CLI](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-docker-cli)</span></span>

<span data-ttu-id="a04c5-165">Let's say we want to deploy the **simple-web** image, with the **2.1** tag, from our private registry hosted on Azure (ACR), we will use the following configuration:</span><span class="sxs-lookup"><span data-stu-id="a04c5-165">Let's say we want to deploy the **simple-web** image, with the **2.1** tag, from our private registry hosted on Azure (ACR), we will use the following configuration:</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "demodcos.azurecr.io/simple-web:2.1",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  },
  "uris":  [
       "file:///mnt/share/docker.tar.gz"
   ]
}
```

> [!NOTE] 
> <span data-ttu-id="a04c5-166">As you can see, we are using the **uris** option to specify where are stored our credentials.</span><span class="sxs-lookup"><span data-stu-id="a04c5-166">As you can see, we are using the **uris** option to specify where are stored our credentials.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="a04c5-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="a04c5-167">Next steps</span></span>
* <span data-ttu-id="a04c5-168">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a04c5-168">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>
* <span data-ttu-id="a04c5-169">DC/OS container management through the [Marathon REST API](container-service-mesos-marathon-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a04c5-169">DC/OS container management through the [Marathon REST API](container-service-mesos-marathon-rest.md).</span></span>