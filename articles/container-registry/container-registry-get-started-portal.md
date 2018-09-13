---
title: Quickstart - Create a private Docker registry in Azure with the Azure portal
description: Quickly learn to create a private Docker container registry with the Azure portal.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: quickstart
ms.date: 03/03/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 55da52e0d314c353c669c56ad918c4dd6bef44c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790589"
---
# <a name="quickstart-create-a-container-registry-using-the-azure-portal"></a><span data-ttu-id="7df79-103">Quickstart: Create a container registry using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7df79-103">Quickstart: Create a container registry using the Azure portal</span></span>

<span data-ttu-id="7df79-104">An Azure container registry is a private Docker registry in Azure where you can store and manage your private Docker container images.</span><span class="sxs-lookup"><span data-stu-id="7df79-104">An Azure container registry is a private Docker registry in Azure where you can store and manage your private Docker container images.</span></span> <span data-ttu-id="7df79-105">In this quickstart, you create a container registry with the Azure portal, push a container image into the registry and finally deploy the container from your registry into Azure Container Instances (ACI).</span><span class="sxs-lookup"><span data-stu-id="7df79-105">In this quickstart, you create a container registry with the Azure portal, push a container image into the registry and finally deploy the container from your registry into Azure Container Instances (ACI).</span></span>

<span data-ttu-id="7df79-106">To complete this quickstart, you must have Docker installed locally.</span><span class="sxs-lookup"><span data-stu-id="7df79-106">To complete this quickstart, you must have Docker installed locally.</span></span> <span data-ttu-id="7df79-107">Docker provides packages that easily configure Docker on any [Mac][docker-mac], [Windows][docker-windows], or [Linux][docker-linux] system.</span><span class="sxs-lookup"><span data-stu-id="7df79-107">Docker provides packages that easily configure Docker on any [Mac][docker-mac], [Windows][docker-windows], or [Linux][docker-linux] system.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="7df79-108">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="7df79-108">Sign in to Azure</span></span>

<span data-ttu-id="7df79-109">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="7df79-109">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="7df79-110">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="7df79-110">Create a container registry</span></span>

<span data-ttu-id="7df79-111">Select **Create a resource** > **Containers** > **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="7df79-111">Select **Create a resource** > **Containers** > **Azure Container Registry**.</span></span>

![Creating a container registry in the Azure portal][qs-portal-01]

<span data-ttu-id="7df79-113">Enter values for **Registry name** and **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="7df79-113">Enter values for **Registry name** and **Resource group**.</span></span> <span data-ttu-id="7df79-114">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="7df79-114">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="7df79-115">Create a new resource group named `myResourceGroup`, and for **SKU**, select 'Basic'.</span><span class="sxs-lookup"><span data-stu-id="7df79-115">Create a new resource group named `myResourceGroup`, and for **SKU**, select 'Basic'.</span></span> <span data-ttu-id="7df79-116">Select **Create** to deploy the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="7df79-116">Select **Create** to deploy the ACR instance.</span></span>

![Creating a container registry in the Azure portal][qs-portal-03]

<span data-ttu-id="7df79-118">In this quickstart, we create a *Basic* registry.</span><span class="sxs-lookup"><span data-stu-id="7df79-118">In this quickstart, we create a *Basic* registry.</span></span> <span data-ttu-id="7df79-119">Azure Container Registry is available in several different SKUs, described briefly in the following table.</span><span class="sxs-lookup"><span data-stu-id="7df79-119">Azure Container Registry is available in several different SKUs, described briefly in the following table.</span></span> <span data-ttu-id="7df79-120">For extended details on each, see [Container registry SKUs][container-registry-skus].</span><span class="sxs-lookup"><span data-stu-id="7df79-120">For extended details on each, see [Container registry SKUs][container-registry-skus].</span></span>

[!INCLUDE [container-registry-sku-matrix](../../includes/container-registry-sku-matrix.md)]

<span data-ttu-id="7df79-121">When the **Deployment succeeded** message appears, select the container registry in the portal, then select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="7df79-121">When the **Deployment succeeded** message appears, select the container registry in the portal, then select **Access keys**.</span></span>

![Creating a container registry in the Azure portal][qs-portal-05]

<span data-ttu-id="7df79-123">Under **Admin user**, select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="7df79-123">Under **Admin user**, select **Enable**.</span></span> <span data-ttu-id="7df79-124">Take note of the following values:</span><span class="sxs-lookup"><span data-stu-id="7df79-124">Take note of the following values:</span></span>

* <span data-ttu-id="7df79-125">Login server</span><span class="sxs-lookup"><span data-stu-id="7df79-125">Login server</span></span>
* <span data-ttu-id="7df79-126">Username</span><span class="sxs-lookup"><span data-stu-id="7df79-126">Username</span></span>
* <span data-ttu-id="7df79-127">password</span><span class="sxs-lookup"><span data-stu-id="7df79-127">password</span></span>

<span data-ttu-id="7df79-128">You use these values in the following steps while working with your registry with the Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="7df79-128">You use these values in the following steps while working with your registry with the Docker CLI.</span></span>

![Creating a container registry in the Azure portal][qs-portal-06]

## <a name="log-in-to-acr"></a><span data-ttu-id="7df79-130">Log in to ACR</span><span class="sxs-lookup"><span data-stu-id="7df79-130">Log in to ACR</span></span>

<span data-ttu-id="7df79-131">Before pushing and pulling container images, you must log in to the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="7df79-131">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="7df79-132">To do so, use the [docker login][docker-login] command.</span><span class="sxs-lookup"><span data-stu-id="7df79-132">To do so, use the [docker login][docker-login] command.</span></span> <span data-ttu-id="7df79-133">Replace the *username*, *password*, and *login server* values with those you noted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7df79-133">Replace the *username*, *password*, and *login server* values with those you noted in the previous step.</span></span>

```bash
docker login --username <username> --password <password> <login server>
```

<span data-ttu-id="7df79-134">The command returns `Login Succeeded` once completed.</span><span class="sxs-lookup"><span data-stu-id="7df79-134">The command returns `Login Succeeded` once completed.</span></span> <span data-ttu-id="7df79-135">You might also see a security warning recommending the use of the `--password-stdin` parameter.</span><span class="sxs-lookup"><span data-stu-id="7df79-135">You might also see a security warning recommending the use of the `--password-stdin` parameter.</span></span> <span data-ttu-id="7df79-136">While its use is outside the scope of this article, we recommend following this best practice.</span><span class="sxs-lookup"><span data-stu-id="7df79-136">While its use is outside the scope of this article, we recommend following this best practice.</span></span> <span data-ttu-id="7df79-137">See the [docker login][docker-login] command reference for more information.</span><span class="sxs-lookup"><span data-stu-id="7df79-137">See the [docker login][docker-login] command reference for more information.</span></span>

## <a name="push-image-to-acr"></a><span data-ttu-id="7df79-138">Push image to ACR</span><span class="sxs-lookup"><span data-stu-id="7df79-138">Push image to ACR</span></span>

<span data-ttu-id="7df79-139">To push an image to your Azure Container Registry, you must first have an image.</span><span class="sxs-lookup"><span data-stu-id="7df79-139">To push an image to your Azure Container Registry, you must first have an image.</span></span> <span data-ttu-id="7df79-140">If needed, run the following command to pull an existing image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="7df79-140">If needed, run the following command to pull an existing image from Docker Hub.</span></span>

```bash
docker pull microsoft/aci-helloworld
```

<span data-ttu-id="7df79-141">Before you push the image to your registry, you must tag the image with the ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="7df79-141">Before you push the image to your registry, you must tag the image with the ACR login server name.</span></span> <span data-ttu-id="7df79-142">Tag the image using the [docker tag][docker-tag] command.</span><span class="sxs-lookup"><span data-stu-id="7df79-142">Tag the image using the [docker tag][docker-tag] command.</span></span> <span data-ttu-id="7df79-143">Replace *login server* with the login server name you recorded earlier.</span><span class="sxs-lookup"><span data-stu-id="7df79-143">Replace *login server* with the login server name you recorded earlier.</span></span>

```bash
docker tag microsoft/aci-helloworld <login server>/aci-helloworld:v1
```

<span data-ttu-id="7df79-144">Finally, use [docker push][docker-push] to push the image to the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="7df79-144">Finally, use [docker push][docker-push] to push the image to the ACR instance.</span></span> <span data-ttu-id="7df79-145">Replace *login server* with the login server name of your ACR instance.</span><span class="sxs-lookup"><span data-stu-id="7df79-145">Replace *login server* with the login server name of your ACR instance.</span></span>

```bash
docker push <login server>/aci-helloworld:v1
```

<span data-ttu-id="7df79-146">Output from a successful `docker push` command is similar to:</span><span class="sxs-lookup"><span data-stu-id="7df79-146">Output from a successful `docker push` command is similar to:</span></span>

```
The push refers to a repository [uniqueregistryname.azurecr.io/aci-helloworld]
7c701b1aeecd: Pushed
c4332f071aa2: Pushed
0607e25cc175: Pushed
d8fbd47558a8: Pushed
44ab46125c35: Pushed
5bef08742407: Pushed
v1: digest: sha256:f2867748615cc327d31c68b1172cc03c0544432717c4d2ba2c1c2d34b18c62ba size: 1577
```

## <a name="list-container-images"></a><span data-ttu-id="7df79-147">List container images</span><span class="sxs-lookup"><span data-stu-id="7df79-147">List container images</span></span>

<span data-ttu-id="7df79-148">To list the images in your ACR instance, navigate to your registry in the portal and select **Repositories**, then select the repository you created with `docker push`.</span><span class="sxs-lookup"><span data-stu-id="7df79-148">To list the images in your ACR instance, navigate to your registry in the portal and select **Repositories**, then select the repository you created with `docker push`.</span></span>

<span data-ttu-id="7df79-149">In this example, we select the **aci-helloworld** repository, and we can see the `v1`-tagged image under **TAGS**.</span><span class="sxs-lookup"><span data-stu-id="7df79-149">In this example, we select the **aci-helloworld** repository, and we can see the `v1`-tagged image under **TAGS**.</span></span>

![Creating a container registry in the Azure portal][qs-portal-09]

## <a name="deploy-image-to-aci"></a><span data-ttu-id="7df79-151">Deploy image to ACI</span><span class="sxs-lookup"><span data-stu-id="7df79-151">Deploy image to ACI</span></span>

<span data-ttu-id="7df79-152">In order to deploy to an instance from the registry we need to navigate to the repository (aci-helloworld), and then click on the ellipsis next to v1.</span><span class="sxs-lookup"><span data-stu-id="7df79-152">In order to deploy to an instance from the registry we need to navigate to the repository (aci-helloworld), and then click on the ellipsis next to v1.</span></span>

![Launching an Azure Container Instance from the portal][qs-portal-10]

<span data-ttu-id="7df79-154">A context menu will appear, select **Run instance**:</span><span class="sxs-lookup"><span data-stu-id="7df79-154">A context menu will appear, select **Run instance**:</span></span>

![Launch ACI context menu][qs-portal-11]

<span data-ttu-id="7df79-156">Fill in **Container name**, ensure the correct subscription is selected, select the existing **Resource group**: "myResourceGroup" and then click **OK** to launch the Azure Container Instance.</span><span class="sxs-lookup"><span data-stu-id="7df79-156">Fill in **Container name**, ensure the correct subscription is selected, select the existing **Resource group**: "myResourceGroup" and then click **OK** to launch the Azure Container Instance.</span></span>

![Launch ACI deployment options][qs-portal-12]

<span data-ttu-id="7df79-158">When deployment starts a tile is placed on your portal dashboard indicating deployment progress.</span><span class="sxs-lookup"><span data-stu-id="7df79-158">When deployment starts a tile is placed on your portal dashboard indicating deployment progress.</span></span> <span data-ttu-id="7df79-159">Once deployment completes, the tile is updated to show your new **mycontainer** container group.</span><span class="sxs-lookup"><span data-stu-id="7df79-159">Once deployment completes, the tile is updated to show your new **mycontainer** container group.</span></span>

![ACI deployment status][qs-portal-13]

<span data-ttu-id="7df79-161">Select the mycontainer container group to display the container group properties.</span><span class="sxs-lookup"><span data-stu-id="7df79-161">Select the mycontainer container group to display the container group properties.</span></span> <span data-ttu-id="7df79-162">Take note of the **IP address** of the container group, as well as the **STATUS** of the container.</span><span class="sxs-lookup"><span data-stu-id="7df79-162">Take note of the **IP address** of the container group, as well as the **STATUS** of the container.</span></span>

![ACI container details][qs-portal-14]

## <a name="view-the-application"></a><span data-ttu-id="7df79-164">View the application</span><span class="sxs-lookup"><span data-stu-id="7df79-164">View the application</span></span>

<span data-ttu-id="7df79-165">Once the container is in the **Running** state, use your favorite browser to navigate to the IP address you noted in the previous step to display the application.</span><span class="sxs-lookup"><span data-stu-id="7df79-165">Once the container is in the **Running** state, use your favorite browser to navigate to the IP address you noted in the previous step to display the application.</span></span>

![Hello world app in the browser][qs-portal-15]

## <a name="clean-up-resources"></a><span data-ttu-id="7df79-167">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7df79-167">Clean up resources</span></span>

<span data-ttu-id="7df79-168">To clean up your resources navigate to the **myResourceGroup** resource group in the portal.</span><span class="sxs-lookup"><span data-stu-id="7df79-168">To clean up your resources navigate to the **myResourceGroup** resource group in the portal.</span></span> <span data-ttu-id="7df79-169">Once the resource group is loaded click on **Delete resource group** to remove the resource group, the Azure Container Registry, and all Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="7df79-169">Once the resource group is loaded click on **Delete resource group** to remove the resource group, the Azure Container Registry, and all Azure Container Instances.</span></span>

![Creating a container registry in the Azure portal][qs-portal-08]

## <a name="next-steps"></a><span data-ttu-id="7df79-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="7df79-171">Next steps</span></span>

<span data-ttu-id="7df79-172">In this quickstart, you created an Azure Container Registry with the Azure CLI, and launched an instance of it via Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="7df79-172">In this quickstart, you created an Azure Container Registry with the Azure CLI, and launched an instance of it via Azure Container Instances.</span></span> <span data-ttu-id="7df79-173">Continue to the Azure Container Instances tutorial for a deeper look at ACI.</span><span class="sxs-lookup"><span data-stu-id="7df79-173">Continue to the Azure Container Instances tutorial for a deeper look at ACI.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="7df79-174">[Azure Container Instances tutorials][container-instances-tutorial-prepare-app]</span><span class="sxs-lookup"><span data-stu-id="7df79-174">[Azure Container Instances tutorials][container-instances-tutorial-prepare-app]</span></span>

<!-- IMAGES -->
[qs-portal-01]: ./media/container-registry-get-started-portal/qs-portal-01.png
[qs-portal-02]: ./media/container-registry-get-started-portal/qs-portal-02.png
[qs-portal-03]: ./media/container-registry-get-started-portal/qs-portal-03.png
[qs-portal-04]: ./media/container-registry-get-started-portal/qs-portal-04.png
[qs-portal-05]: ./media/container-registry-get-started-portal/qs-portal-05.png
[qs-portal-06]: ./media/container-registry-get-started-portal/qs-portal-06.png
[qs-portal-07]: ./media/container-registry-get-started-portal/qs-portal-07.png
[qs-portal-08]: ./media/container-registry-get-started-portal/qs-portal-08.png
[qs-portal-09]: ./media/container-registry-get-started-portal/qs-portal-09.png
[qs-portal-10]: ./media/container-registry-get-started-portal/qs-portal-10.png
[qs-portal-11]: ./media/container-registry-get-started-portal/qs-portal-11.png
[qs-portal-12]: ./media/container-registry-get-started-portal/qs-portal-12.png
[qs-portal-13]: ./media/container-registry-get-started-portal/qs-portal-13.png
[qs-portal-14]: ./media/container-registry-get-started-portal/qs-portal-14.png
[qs-portal-15]: ./media/container-registry-get-started-portal/qs-portal-15.png

<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- LINKS - internal -->
[container-instances-tutorial-prepare-app]: ../container-instances/container-instances-tutorial-prepare-app.md
[container-registry-skus]: container-registry-skus.md
