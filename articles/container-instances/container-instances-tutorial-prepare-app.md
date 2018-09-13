---
title: Azure Container Instances tutorial - Prepare your app
description: Azure Container Instances tutorial part 1 of 3 - Prepare an app for deployment to Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: tutorial
ms.date: 03/21/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 79041123196559c5759789638228ea0dd21f2762
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871644"
---
# <a name="tutorial-create-container-for-deployment-to-azure-container-instances"></a><span data-ttu-id="eb6b7-103">Tutorial: Create container for deployment to Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="eb6b7-103">Tutorial: Create container for deployment to Azure Container Instances</span></span>

<span data-ttu-id="eb6b7-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting a higher-level service.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting a higher-level service.</span></span> <span data-ttu-id="eb6b7-105">In this tutorial, you package a small Node.js web application into a container image that can be run using Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-105">In this tutorial, you package a small Node.js web application into a container image that can be run using Azure Container Instances.</span></span>

<span data-ttu-id="eb6b7-106">In this article, part one of the series, you:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-106">In this article, part one of the series, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb6b7-107">Clone application source code from GitHub</span><span class="sxs-lookup"><span data-stu-id="eb6b7-107">Clone application source code from GitHub</span></span>
> * <span data-ttu-id="eb6b7-108">Create a container image from application source</span><span class="sxs-lookup"><span data-stu-id="eb6b7-108">Create a container image from application source</span></span>
> * <span data-ttu-id="eb6b7-109">Test the image in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="eb6b7-109">Test the image in a local Docker environment</span></span>

<span data-ttu-id="eb6b7-110">In tutorial parts two and three, you upload your image to Azure Container Registry, and then deploy it to Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-110">In tutorial parts two and three, you upload your image to Azure Container Registry, and then deploy it to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eb6b7-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="eb6b7-111">Before you begin</span></span>

[!INCLUDE [container-instances-tutorial-prerequisites](../../includes/container-instances-tutorial-prerequisites.md)]

## <a name="get-application-code"></a><span data-ttu-id="eb6b7-112">Get application code</span><span class="sxs-lookup"><span data-stu-id="eb6b7-112">Get application code</span></span>

<span data-ttu-id="eb6b7-113">The sample application in this tutorial is a simple web app built in [Node.js][nodejs].</span><span class="sxs-lookup"><span data-stu-id="eb6b7-113">The sample application in this tutorial is a simple web app built in [Node.js][nodejs].</span></span> <span data-ttu-id="eb6b7-114">The application serves a static HTML page, and looks similar to the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-114">The application serves a static HTML page, and looks similar to the following screenshot:</span></span>

![Tutorial app shown in browser][aci-tutorial-app]

<span data-ttu-id="eb6b7-116">Use Git to clone the sample application's repository:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-116">Use Git to clone the sample application's repository:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

<span data-ttu-id="eb6b7-117">You can also [download the ZIP archive][aci-helloworld-zip] from GitHub directly.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-117">You can also [download the ZIP archive][aci-helloworld-zip] from GitHub directly.</span></span>

## <a name="build-the-container-image"></a><span data-ttu-id="eb6b7-118">Build the container image</span><span class="sxs-lookup"><span data-stu-id="eb6b7-118">Build the container image</span></span>

<span data-ttu-id="eb6b7-119">The Dockerfile in the sample application shows how the container is built.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-119">The Dockerfile in the sample application shows how the container is built.</span></span> <span data-ttu-id="eb6b7-120">It starts from an [official Node.js image][docker-hub-nodeimage] based on [Alpine Linux][alpine-linux], a small distribution that is well suited for use with containers.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-120">It starts from an [official Node.js image][docker-hub-nodeimage] based on [Alpine Linux][alpine-linux], a small distribution that is well suited for use with containers.</span></span> <span data-ttu-id="eb6b7-121">It then copies the application files into the container, installs dependencies using the Node Package Manager, and finally, starts the application.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-121">It then copies the application files into the container, installs dependencies using the Node Package Manager, and finally, starts the application.</span></span>

```Dockerfile
FROM node:8.9.3-alpine
RUN mkdir -p /usr/src/app
COPY ./app/ /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="eb6b7-122">Use the [docker build][docker-build] command to create the container image and tag it as *aci-tutorial-app*:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-122">Use the [docker build][docker-build] command to create the container image and tag it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="eb6b7-123">Output from the [docker build][docker-build] command is similar to the following (truncated for readability):</span><span class="sxs-lookup"><span data-stu-id="eb6b7-123">Output from the [docker build][docker-build] command is similar to the following (truncated for readability):</span></span>

```console
$ docker build ./aci-helloworld -t aci-tutorial-app
Sending build context to Docker daemon  119.3kB
Step 1/6 : FROM node:8.9.3-alpine
8.9.3-alpine: Pulling from library/node
88286f41530e: Pull complete
84f3a4bf8410: Pull complete
d0d9b2214720: Pull complete
Digest: sha256:c73277ccc763752b42bb2400d1aaecb4e3d32e3a9dbedd0e49885c71bea07354
Status: Downloaded newer image for node:8.9.3-alpine
 ---> 90f5ee24bee2
...
Step 6/6 : CMD node /usr/src/app/index.js
 ---> Running in f4a1ea099eec
 ---> 6edad76d09e9
Removing intermediate container f4a1ea099eec
Successfully built 6edad76d09e9
Successfully tagged aci-tutorial-app:latest
```

<span data-ttu-id="eb6b7-124">Use the [docker images][docker-images] command to see the built image:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-124">Use the [docker images][docker-images] command to see the built image:</span></span>

```bash
docker images
```

<span data-ttu-id="eb6b7-125">Your newly built image should appear in the list:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-125">Your newly built image should appear in the list:</span></span>

```console
$ docker images
REPOSITORY          TAG       IMAGE ID        CREATED           SIZE
aci-tutorial-app    latest    5c745774dfa9    39 seconds ago    68.1 MB
```

## <a name="run-the-container-locally"></a><span data-ttu-id="eb6b7-126">Run the container locally</span><span class="sxs-lookup"><span data-stu-id="eb6b7-126">Run the container locally</span></span>

<span data-ttu-id="eb6b7-127">Before you deploy the container to Azure Container Instances, use [docker run][docker-run] to run it locally and confirm that it works.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-127">Before you deploy the container to Azure Container Instances, use [docker run][docker-run] to run it locally and confirm that it works.</span></span> <span data-ttu-id="eb6b7-128">The `-d` switch lets the container run in the background, while `-p` allows you to map an arbitrary port on your computer to port 80 in the container.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-128">The `-d` switch lets the container run in the background, while `-p` allows you to map an arbitrary port on your computer to port 80 in the container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="eb6b7-129">Output from the `docker run` command displays the running container's ID if the command was successful:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-129">Output from the `docker run` command displays the running container's ID if the command was successful:</span></span>

```console
$ docker run -d -p 8080:80 aci-tutorial-app
a2e3e4435db58ab0c664ce521854c2e1a1bda88c9cf2fcff46aedf48df86cccf
```

<span data-ttu-id="eb6b7-130">Now, navigate to http://localhost:8080 in your browser to confirm that the container is running.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-130">Now, navigate to http://localhost:8080 in your browser to confirm that the container is running.</span></span> <span data-ttu-id="eb6b7-131">You should see a web page similar to the following:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-131">You should see a web page similar to the following:</span></span>

![Running the app locally in the browser][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="eb6b7-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb6b7-133">Next steps</span></span>

<span data-ttu-id="eb6b7-134">In this tutorial, you created a container image that can be deployed in Azure Container Instances, and verified that it runs locally.</span><span class="sxs-lookup"><span data-stu-id="eb6b7-134">In this tutorial, you created a container image that can be deployed in Azure Container Instances, and verified that it runs locally.</span></span> <span data-ttu-id="eb6b7-135">So far, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-135">So far, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb6b7-136">Cloned the application source from GitHub</span><span class="sxs-lookup"><span data-stu-id="eb6b7-136">Cloned the application source from GitHub</span></span>
> * <span data-ttu-id="eb6b7-137">Created a container image from the application source</span><span class="sxs-lookup"><span data-stu-id="eb6b7-137">Created a container image from the application source</span></span>
> * <span data-ttu-id="eb6b7-138">Tested the container locally</span><span class="sxs-lookup"><span data-stu-id="eb6b7-138">Tested the container locally</span></span>

<span data-ttu-id="eb6b7-139">Advance to the next tutorial in the series to learn about storing your container image in Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="eb6b7-139">Advance to the next tutorial in the series to learn about storing your container image in Azure Container Registry:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb6b7-140">Push image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="eb6b7-140">Push image to Azure Container Registry</span></span>](container-instances-tutorial-prepare-acr.md)

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png

<!-- LINKS - External -->
[aci-helloworld-zip]: https://github.com/Azure-Samples/aci-helloworld/archive/master.zip
[alpine-linux]: https://alpinelinux.org/
[docker-build]: https://docs.docker.com/engine/reference/commandline/build/
[docker-get-started]: https://docs.docker.com/get-started/
[docker-hub-nodeimage]: https://store.docker.com/images/node
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-run]: https://docs.docker.com/engine/reference/commandline/run/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/
[nodejs]: http://nodejs.org

<!-- LINKS - Internal -->
[azure-cli-install]: /cli/azure/install-azure-cli
