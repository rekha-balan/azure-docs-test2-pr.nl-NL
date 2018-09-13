---
title: Quickstart - Create your first Azure Container Instances container with the Azure portal
description: In this quickstart, you use the Azure portal to deploy a container in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: quickstart
ms.date: 05/11/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 6aa6fb27b2aa7c8b9614e5812fadc629b1e185f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968787"
---
# <a name="quickstart-create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="1cc24-103">Quickstart: Create your first container in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="1cc24-103">Quickstart: Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="1cc24-104">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span><span class="sxs-lookup"><span data-stu-id="1cc24-104">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span></span> <span data-ttu-id="1cc24-105">In this quickstart, you use the Azure portal to create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="1cc24-105">In this quickstart, you use the Azure portal to create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="1cc24-106">After configuring a few settings, you'll see this in your browser:</span><span class="sxs-lookup"><span data-stu-id="1cc24-106">After configuring a few settings, you'll see this in your browser:</span></span>

![App deployed using Azure Container Instances viewed in browser][aci-portal-07]

## <a name="sign-in-to-azure"></a><span data-ttu-id="1cc24-108">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="1cc24-108">Sign in to Azure</span></span>

<span data-ttu-id="1cc24-109">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="1cc24-109">Sign in to the Azure portal at https://portal.azure.com.</span></span>

<span data-ttu-id="1cc24-110">If you don't have an Azure subscription, create a [free account][azure-free-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="1cc24-110">If you don't have an Azure subscription, create a [free account][azure-free-account] before you begin.</span></span>

## <a name="create-a-container-instance"></a><span data-ttu-id="1cc24-111">Create a container instance</span><span class="sxs-lookup"><span data-stu-id="1cc24-111">Create a container instance</span></span>

<span data-ttu-id="1cc24-112">Select the **Create a resource** > **Containers** > **Container Instances**.</span><span class="sxs-lookup"><span data-stu-id="1cc24-112">Select the **Create a resource** > **Containers** > **Container Instances**.</span></span>

![Begin creating a new container instance in the Azure portal][aci-portal-01]

<span data-ttu-id="1cc24-114">Enter the following values in the **Container name**, **Container image**, and **Resource group** text boxes.</span><span class="sxs-lookup"><span data-stu-id="1cc24-114">Enter the following values in the **Container name**, **Container image**, and **Resource group** text boxes.</span></span> <span data-ttu-id="1cc24-115">Leave the other values at their defaults, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cc24-115">Leave the other values at their defaults, then select **OK**.</span></span>

* <span data-ttu-id="1cc24-116">Container name: `mycontainer`</span><span class="sxs-lookup"><span data-stu-id="1cc24-116">Container name: `mycontainer`</span></span>
* <span data-ttu-id="1cc24-117">Container image: `microsoft/aci-helloworld`</span><span class="sxs-lookup"><span data-stu-id="1cc24-117">Container image: `microsoft/aci-helloworld`</span></span>
* <span data-ttu-id="1cc24-118">Resource group: `myResourceGroup`</span><span class="sxs-lookup"><span data-stu-id="1cc24-118">Resource group: `myResourceGroup`</span></span>

![Configuring basic settings for a new container instance in the Azure portal][aci-portal-03]

<span data-ttu-id="1cc24-120">You can create both Windows and Linux containers in Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="1cc24-120">You can create both Windows and Linux containers in Azure Container Instances.</span></span> <span data-ttu-id="1cc24-121">For this quickstart, leave the default setting of **Linux** to deploy the Linux-based `microsoft/aci-helloworld` image.</span><span class="sxs-lookup"><span data-stu-id="1cc24-121">For this quickstart, leave the default setting of **Linux** to deploy the Linux-based `microsoft/aci-helloworld` image.</span></span>

<span data-ttu-id="1cc24-122">Under **Configuration**, specify a **DNS name label** for your container.</span><span class="sxs-lookup"><span data-stu-id="1cc24-122">Under **Configuration**, specify a **DNS name label** for your container.</span></span> <span data-ttu-id="1cc24-123">The name must be unique within the Azure region you create the container instance.</span><span class="sxs-lookup"><span data-stu-id="1cc24-123">The name must be unique within the Azure region you create the container instance.</span></span> <span data-ttu-id="1cc24-124">Your container will be publicly reachable at `<dns-name-label>.<region>.azurecontainer.io`.</span><span class="sxs-lookup"><span data-stu-id="1cc24-124">Your container will be publicly reachable at `<dns-name-label>.<region>.azurecontainer.io`.</span></span>

<span data-ttu-id="1cc24-125">Leave the other settings in **Configuration** at their defaults, then select **OK** to validate the configuration.</span><span class="sxs-lookup"><span data-stu-id="1cc24-125">Leave the other settings in **Configuration** at their defaults, then select **OK** to validate the configuration.</span></span>

![Configuring a new container instance in the Azure portal][aci-portal-04]

<span data-ttu-id="1cc24-127">When the validation completes, you're shown a summary of the container's settings.</span><span class="sxs-lookup"><span data-stu-id="1cc24-127">When the validation completes, you're shown a summary of the container's settings.</span></span> <span data-ttu-id="1cc24-128">Select **OK** to submit your container deployment request.</span><span class="sxs-lookup"><span data-stu-id="1cc24-128">Select **OK** to submit your container deployment request.</span></span>

![Settings summary for a new container instance in the Azure portal][aci-portal-05]

<span data-ttu-id="1cc24-130">When deployment starts, a tile appears on your portal dashboard indicating the deployment is in progress.</span><span class="sxs-lookup"><span data-stu-id="1cc24-130">When deployment starts, a tile appears on your portal dashboard indicating the deployment is in progress.</span></span> <span data-ttu-id="1cc24-131">Once deployed, the tile displays your new container instance.</span><span class="sxs-lookup"><span data-stu-id="1cc24-131">Once deployed, the tile displays your new container instance.</span></span>

![Creation progress of a new container instance in the Azure portal][aci-portal-08]

<span data-ttu-id="1cc24-133">Select the **mycontainer** container instance to display its properties.</span><span class="sxs-lookup"><span data-stu-id="1cc24-133">Select the **mycontainer** container instance to display its properties.</span></span> <span data-ttu-id="1cc24-134">Take note of the **FQDN** (the fully qualified domain name) of the container instance, as well its **Status**.</span><span class="sxs-lookup"><span data-stu-id="1cc24-134">Take note of the **FQDN** (the fully qualified domain name) of the container instance, as well its **Status**.</span></span>

![Container group overview in the Azure portal][aci-portal-06]

<span data-ttu-id="1cc24-136">Once its **Status** is *Running*, navigate to the container's FQDN in your browser.</span><span class="sxs-lookup"><span data-stu-id="1cc24-136">Once its **Status** is *Running*, navigate to the container's FQDN in your browser.</span></span>

![App deployed using Azure Container Instances viewed in browser][aci-portal-07]

<span data-ttu-id="1cc24-138">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="1cc24-138">Congratulations!</span></span> <span data-ttu-id="1cc24-139">By configuring just a few settings, you've deployed a publicly accessible application in Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="1cc24-139">By configuring just a few settings, you've deployed a publicly accessible application in Azure Container Instances.</span></span>

## <a name="view-container-logs"></a><span data-ttu-id="1cc24-140">View container logs</span><span class="sxs-lookup"><span data-stu-id="1cc24-140">View container logs</span></span>

<span data-ttu-id="1cc24-141">Viewing the logs for a container instance is helpful when troubleshooting issues with your container or the application it runs.</span><span class="sxs-lookup"><span data-stu-id="1cc24-141">Viewing the logs for a container instance is helpful when troubleshooting issues with your container or the application it runs.</span></span>

<span data-ttu-id="1cc24-142">To view the container's logs, under **SETTINGS**, select **Containers**, then **Logs**.</span><span class="sxs-lookup"><span data-stu-id="1cc24-142">To view the container's logs, under **SETTINGS**, select **Containers**, then **Logs**.</span></span> <span data-ttu-id="1cc24-143">You should see the HTTP GET request generated when you viewed the application in your browser.</span><span class="sxs-lookup"><span data-stu-id="1cc24-143">You should see the HTTP GET request generated when you viewed the application in your browser.</span></span>

![Container logs in the Azure portal][aci-portal-11]

## <a name="clean-up-resources"></a><span data-ttu-id="1cc24-145">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1cc24-145">Clean up resources</span></span>

<span data-ttu-id="1cc24-146">When you're done with the container, select **Overview** for the *mycontainer* container instance, then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1cc24-146">When you're done with the container, select **Overview** for the *mycontainer* container instance, then select **Delete**.</span></span>

![Deleting the container instance in the Azure portal][aci-portal-09]

<span data-ttu-id="1cc24-148">Select **Yes** when the confirmation dialog appears.</span><span class="sxs-lookup"><span data-stu-id="1cc24-148">Select **Yes** when the confirmation dialog appears.</span></span>

![Delete confirmation of a container instance in the Azure portal][aci-portal-10]

## <a name="next-steps"></a><span data-ttu-id="1cc24-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="1cc24-150">Next steps</span></span>

<span data-ttu-id="1cc24-151">In this quickstart, you created an Azure container instance from an image in the public Docker Hub registry.</span><span class="sxs-lookup"><span data-stu-id="1cc24-151">In this quickstart, you created an Azure container instance from an image in the public Docker Hub registry.</span></span> <span data-ttu-id="1cc24-152">If you'd like to build a container image yourself and deploy it to Azure Container Instances from a private Azure container registry, continue to the Azure Container Instances tutorial.</span><span class="sxs-lookup"><span data-stu-id="1cc24-152">If you'd like to build a container image yourself and deploy it to Azure Container Instances from a private Azure container registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1cc24-153">Azure Container Instances tutorial</span><span class="sxs-lookup"><span data-stu-id="1cc24-153">Azure Container Instances tutorial</span></span>](./container-instances-tutorial-prepare-app.md)

<!-- IMAGES -->
[aci-portal-01]: ./media/container-instances-quickstart-portal/qs-portal-01.png
[aci-portal-03]: ./media/container-instances-quickstart-portal/qs-portal-03.png
[aci-portal-04]: ./media/container-instances-quickstart-portal/qs-portal-04.png
[aci-portal-05]: ./media/container-instances-quickstart-portal/qs-portal-05.png
[aci-portal-06]: ./media/container-instances-quickstart-portal/qs-portal-06.png
[aci-portal-07]: ./media/container-instances-quickstart-portal/qs-portal-07.png
[aci-portal-08]: ./media/container-instances-quickstart-portal/qs-portal-08.png
[aci-portal-09]: ./media/container-instances-quickstart-portal/qs-portal-09.png
[aci-portal-10]: ./media/container-instances-quickstart-portal/qs-portal-10.png
[aci-portal-11]: ./media/container-instances-quickstart-portal/qs-portal-11.png

<!-- LINKS - External -->
[azure-free-account]: https://azure.microsoft.com/free/