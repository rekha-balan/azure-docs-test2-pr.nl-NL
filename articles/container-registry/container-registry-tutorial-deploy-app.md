---
title: Azure Container Registry tutorial - Deploy web app from Azure Container Registry
description: Deploy a Linux-based web app using a container image from a geo-replicated Azure container registry. Part two of a three-part series.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: tutorial
ms.date: 08/20/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 25e3fdfe72fc2a6ffec1bcee23cd9f1edc783838
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871486"
---
# <a name="tutorial-deploy-web-app-from-azure-container-registry"></a><span data-ttu-id="ec418-104">Tutorial: Deploy web app from Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ec418-104">Tutorial: Deploy web app from Azure Container Registry</span></span>

<span data-ttu-id="ec418-105">This is part two in a three-part tutorial series.</span><span class="sxs-lookup"><span data-stu-id="ec418-105">This is part two in a three-part tutorial series.</span></span> <span data-ttu-id="ec418-106">In [part one](container-registry-tutorial-prepare-registry.md), a private, geo-replicated container registry was created, and a container image was built from source and pushed to the registry.</span><span class="sxs-lookup"><span data-stu-id="ec418-106">In [part one](container-registry-tutorial-prepare-registry.md), a private, geo-replicated container registry was created, and a container image was built from source and pushed to the registry.</span></span> <span data-ttu-id="ec418-107">In this article, you take advantage of the network-close aspect of the geo-replicated registry by deploying the container to Web App instances in two different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="ec418-107">In this article, you take advantage of the network-close aspect of the geo-replicated registry by deploying the container to Web App instances in two different Azure regions.</span></span> <span data-ttu-id="ec418-108">Each instance then pulls the container image from the closest registry.</span><span class="sxs-lookup"><span data-stu-id="ec418-108">Each instance then pulls the container image from the closest registry.</span></span>

<span data-ttu-id="ec418-109">In this tutorial, part two in the series:</span><span class="sxs-lookup"><span data-stu-id="ec418-109">In this tutorial, part two in the series:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec418-110">Deploy a container image to two *Web Apps for Containers* instances</span><span class="sxs-lookup"><span data-stu-id="ec418-110">Deploy a container image to two *Web Apps for Containers* instances</span></span>
> * <span data-ttu-id="ec418-111">Verify the deployed application</span><span class="sxs-lookup"><span data-stu-id="ec418-111">Verify the deployed application</span></span>

<span data-ttu-id="ec418-112">If you haven't yet created a geo-replicated registry and pushed the image of the containerized sample application to the registry, return to the previous tutorial in the series, [Prepare a geo-replicated Azure container registry](container-registry-tutorial-prepare-registry.md).</span><span class="sxs-lookup"><span data-stu-id="ec418-112">If you haven't yet created a geo-replicated registry and pushed the image of the containerized sample application to the registry, return to the previous tutorial in the series, [Prepare a geo-replicated Azure container registry](container-registry-tutorial-prepare-registry.md).</span></span>

<span data-ttu-id="ec418-113">In the next article in the series, you update the application, then push the updated container image to the registry.</span><span class="sxs-lookup"><span data-stu-id="ec418-113">In the next article in the series, you update the application, then push the updated container image to the registry.</span></span> <span data-ttu-id="ec418-114">Finally, you browse to each running Web App instance to see the change automatically reflected in both, showing Azure Container Registry geo-replication and webhooks in action.</span><span class="sxs-lookup"><span data-stu-id="ec418-114">Finally, you browse to each running Web App instance to see the change automatically reflected in both, showing Azure Container Registry geo-replication and webhooks in action.</span></span>

## <a name="automatic-deployment-to-web-apps-for-containers"></a><span data-ttu-id="ec418-115">Automatic deployment to Web Apps for Containers</span><span class="sxs-lookup"><span data-stu-id="ec418-115">Automatic deployment to Web Apps for Containers</span></span>

<span data-ttu-id="ec418-116">Azure Container Registry provides support for deploying containerized applications directly to [Web Apps for Containers](../app-service/containers/index.yml).</span><span class="sxs-lookup"><span data-stu-id="ec418-116">Azure Container Registry provides support for deploying containerized applications directly to [Web Apps for Containers](../app-service/containers/index.yml).</span></span> <span data-ttu-id="ec418-117">In this tutorial, you use the Azure portal to deploy the container image created in the previous tutorial to two web app plans located in different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="ec418-117">In this tutorial, you use the Azure portal to deploy the container image created in the previous tutorial to two web app plans located in different Azure regions.</span></span>

<span data-ttu-id="ec418-118">When you deploy a web app from a container image in your registry, and you have a geo-replicated registry in the same region, Azure Container Registry creates an image deployment [webhook](container-registry-webhook.md) for you.</span><span class="sxs-lookup"><span data-stu-id="ec418-118">When you deploy a web app from a container image in your registry, and you have a geo-replicated registry in the same region, Azure Container Registry creates an image deployment [webhook](container-registry-webhook.md) for you.</span></span> <span data-ttu-id="ec418-119">When you push a new image to your container repository, the webhook picks up the change and automatically deploys the new container image to your web app.</span><span class="sxs-lookup"><span data-stu-id="ec418-119">When you push a new image to your container repository, the webhook picks up the change and automatically deploys the new container image to your web app.</span></span>

## <a name="deploy-a-web-app-for-containers-instance"></a><span data-ttu-id="ec418-120">Deploy a Web App for Containers instance</span><span class="sxs-lookup"><span data-stu-id="ec418-120">Deploy a Web App for Containers instance</span></span>

<span data-ttu-id="ec418-121">In this step, you create a Web App for Containers instance in the *West US* region.</span><span class="sxs-lookup"><span data-stu-id="ec418-121">In this step, you create a Web App for Containers instance in the *West US* region.</span></span>

<span data-ttu-id="ec418-122">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the registry you created in the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec418-122">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the registry you created in the previous tutorial.</span></span>

<span data-ttu-id="ec418-123">Select **Repositories** > **acr-helloworld**, then right-click on the **v1** tag under **Tags** and select **Deploy to web app**:</span><span class="sxs-lookup"><span data-stu-id="ec418-123">Select **Repositories** > **acr-helloworld**, then right-click on the **v1** tag under **Tags** and select **Deploy to web app**:</span></span>

![Deploy to app service in the Azure portal][deploy-app-portal-01]

<span data-ttu-id="ec418-125">If "Deploy to web app" is disabled, you might not have enabled the registry admin user as directed in [Create a container registry](container-registry-tutorial-prepare-registry.md#create-a-container-registry) in the first tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec418-125">If "Deploy to web app" is disabled, you might not have enabled the registry admin user as directed in [Create a container registry](container-registry-tutorial-prepare-registry.md#create-a-container-registry) in the first tutorial.</span></span> <span data-ttu-id="ec418-126">You can enable the admin user in **Settings** > **Access keys** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ec418-126">You can enable the admin user in **Settings** > **Access keys** in the Azure portal.</span></span>

<span data-ttu-id="ec418-127">Under **Web App for Containers** that's displayed after you select "Deploy to web app," specify the following values for each setting:</span><span class="sxs-lookup"><span data-stu-id="ec418-127">Under **Web App for Containers** that's displayed after you select "Deploy to web app," specify the following values for each setting:</span></span>

| <span data-ttu-id="ec418-128">Setting</span><span class="sxs-lookup"><span data-stu-id="ec418-128">Setting</span></span> | <span data-ttu-id="ec418-129">Value</span><span class="sxs-lookup"><span data-stu-id="ec418-129">Value</span></span> |
|---|---|
| <span data-ttu-id="ec418-130">**Site Name**</span><span class="sxs-lookup"><span data-stu-id="ec418-130">**Site Name**</span></span> | <span data-ttu-id="ec418-131">A globally unique name for the web app.</span><span class="sxs-lookup"><span data-stu-id="ec418-131">A globally unique name for the web app.</span></span> <span data-ttu-id="ec418-132">In this example, we use the format `<acrName>-westus` to easily identify the registry and region the web app is deployed from.</span><span class="sxs-lookup"><span data-stu-id="ec418-132">In this example, we use the format `<acrName>-westus` to easily identify the registry and region the web app is deployed from.</span></span> |
| <span data-ttu-id="ec418-133">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="ec418-133">**Resource Group**</span></span> | <span data-ttu-id="ec418-134">**Use existing** > `myResourceGroup`</span><span class="sxs-lookup"><span data-stu-id="ec418-134">**Use existing** > `myResourceGroup`</span></span> |
| <span data-ttu-id="ec418-135">**App service plan/Location**</span><span class="sxs-lookup"><span data-stu-id="ec418-135">**App service plan/Location**</span></span> | <span data-ttu-id="ec418-136">Create a new plan named `plan-westus` in the **West US** region.</span><span class="sxs-lookup"><span data-stu-id="ec418-136">Create a new plan named `plan-westus` in the **West US** region.</span></span> |
| <span data-ttu-id="ec418-137">**Image**</span><span class="sxs-lookup"><span data-stu-id="ec418-137">**Image**</span></span> | `acr-helloworld:v1`

<span data-ttu-id="ec418-138">Select **Create** to provision the web app to the *West US* region.</span><span class="sxs-lookup"><span data-stu-id="ec418-138">Select **Create** to provision the web app to the *West US* region.</span></span>

![Web app on Linux configuration in the Azure portal][deploy-app-portal-02]

## <a name="view-the-deployed-web-app"></a><span data-ttu-id="ec418-140">View the deployed web app</span><span class="sxs-lookup"><span data-stu-id="ec418-140">View the deployed web app</span></span>

<span data-ttu-id="ec418-141">When deployment is complete, you can view the running application by navigating to its URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="ec418-141">When deployment is complete, you can view the running application by navigating to its URL in your browser.</span></span>

<span data-ttu-id="ec418-142">In the portal, select **App Services**, then the web app you provisioned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ec418-142">In the portal, select **App Services**, then the web app you provisioned in the previous step.</span></span> <span data-ttu-id="ec418-143">In this example, the web app is named *uniqueregistryname-westus*.</span><span class="sxs-lookup"><span data-stu-id="ec418-143">In this example, the web app is named *uniqueregistryname-westus*.</span></span>

<span data-ttu-id="ec418-144">Select the hyperlinked URL of the web app in the top-right of the **App Service** overview to view the running application in your browser.</span><span class="sxs-lookup"><span data-stu-id="ec418-144">Select the hyperlinked URL of the web app in the top-right of the **App Service** overview to view the running application in your browser.</span></span>

![Web app on Linux configuration in the Azure portal][deploy-app-portal-04]

<span data-ttu-id="ec418-146">Once the Docker image is deployed from your geo-replicated container registry, the site displays an image representing the Azure region hosting the container registry.</span><span class="sxs-lookup"><span data-stu-id="ec418-146">Once the Docker image is deployed from your geo-replicated container registry, the site displays an image representing the Azure region hosting the container registry.</span></span>

![Deployed web application viewed in a browser][deployed-app-westus]

## <a name="deploy-second-web-app-for-containers-instance"></a><span data-ttu-id="ec418-148">Deploy second Web App for Containers instance</span><span class="sxs-lookup"><span data-stu-id="ec418-148">Deploy second Web App for Containers instance</span></span>

<span data-ttu-id="ec418-149">Use the procedure outlined in the previous section to deploy a second web app to the *East US* region.</span><span class="sxs-lookup"><span data-stu-id="ec418-149">Use the procedure outlined in the previous section to deploy a second web app to the *East US* region.</span></span> <span data-ttu-id="ec418-150">Under **Web App for Containers**, specify the following values:</span><span class="sxs-lookup"><span data-stu-id="ec418-150">Under **Web App for Containers**, specify the following values:</span></span>

| <span data-ttu-id="ec418-151">Setting</span><span class="sxs-lookup"><span data-stu-id="ec418-151">Setting</span></span> | <span data-ttu-id="ec418-152">Value</span><span class="sxs-lookup"><span data-stu-id="ec418-152">Value</span></span> |
|---|---|
| <span data-ttu-id="ec418-153">**Site Name**</span><span class="sxs-lookup"><span data-stu-id="ec418-153">**Site Name**</span></span> | <span data-ttu-id="ec418-154">A globally unique name for the web app.</span><span class="sxs-lookup"><span data-stu-id="ec418-154">A globally unique name for the web app.</span></span> <span data-ttu-id="ec418-155">In this example, we use the format `<acrName>-eastus` to easily identify the registry and region the web app is deployed from.</span><span class="sxs-lookup"><span data-stu-id="ec418-155">In this example, we use the format `<acrName>-eastus` to easily identify the registry and region the web app is deployed from.</span></span> |
| <span data-ttu-id="ec418-156">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="ec418-156">**Resource Group**</span></span> | <span data-ttu-id="ec418-157">**Use existing** > `myResourceGroup`</span><span class="sxs-lookup"><span data-stu-id="ec418-157">**Use existing** > `myResourceGroup`</span></span> |
| <span data-ttu-id="ec418-158">**App service plan/Location**</span><span class="sxs-lookup"><span data-stu-id="ec418-158">**App service plan/Location**</span></span> | <span data-ttu-id="ec418-159">Create a new plan named `plan-eastus` in the **East US** region.</span><span class="sxs-lookup"><span data-stu-id="ec418-159">Create a new plan named `plan-eastus` in the **East US** region.</span></span> |
| <span data-ttu-id="ec418-160">**Image**</span><span class="sxs-lookup"><span data-stu-id="ec418-160">**Image**</span></span> | `acr-helloworld:v1`

<span data-ttu-id="ec418-161">Select **Create** to provision the web app to the *East US* region.</span><span class="sxs-lookup"><span data-stu-id="ec418-161">Select **Create** to provision the web app to the *East US* region.</span></span>

![Web app on Linux configuration in the Azure portal][deploy-app-portal-06]

## <a name="view-the-deployed-web-app"></a><span data-ttu-id="ec418-163">View the deployed web app</span><span class="sxs-lookup"><span data-stu-id="ec418-163">View the deployed web app</span></span>

<span data-ttu-id="ec418-164">As before, you can view the running application by navigating to its URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="ec418-164">As before, you can view the running application by navigating to its URL in your browser.</span></span>

<span data-ttu-id="ec418-165">In the portal, select **App Services**, then the web app you provisioned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ec418-165">In the portal, select **App Services**, then the web app you provisioned in the previous step.</span></span> <span data-ttu-id="ec418-166">In this example, the web app is named *uniqueregistryname-eastus*.</span><span class="sxs-lookup"><span data-stu-id="ec418-166">In this example, the web app is named *uniqueregistryname-eastus*.</span></span>

<span data-ttu-id="ec418-167">Select the hyperlinked URL of the web app in the top-right of the **App Service overview** to view the running application in your browser.</span><span class="sxs-lookup"><span data-stu-id="ec418-167">Select the hyperlinked URL of the web app in the top-right of the **App Service overview** to view the running application in your browser.</span></span>

![Web app on Linux configuration in the Azure portal][deploy-app-portal-07]

<span data-ttu-id="ec418-169">Once the Docker image is deployed from your geo-replicated container registry, the site displays an image representing the Azure region hosting the container registry.</span><span class="sxs-lookup"><span data-stu-id="ec418-169">Once the Docker image is deployed from your geo-replicated container registry, the site displays an image representing the Azure region hosting the container registry.</span></span>

![Deployed web application viewed in a browser][deployed-app-eastus]

## <a name="next-steps"></a><span data-ttu-id="ec418-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec418-171">Next steps</span></span>

<span data-ttu-id="ec418-172">In this tutorial, you deployed two Web App for Containers instances from a geo-replicated Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="ec418-172">In this tutorial, you deployed two Web App for Containers instances from a geo-replicated Azure container registry.</span></span>

<span data-ttu-id="ec418-173">Advance to the next tutorial to update and then deploy a new container image to the container registry, then verify that the web apps running in both regions were updated automatically.</span><span class="sxs-lookup"><span data-stu-id="ec418-173">Advance to the next tutorial to update and then deploy a new container image to the container registry, then verify that the web apps running in both regions were updated automatically.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec418-174">Deploy an update to geo-replicated container image</span><span class="sxs-lookup"><span data-stu-id="ec418-174">Deploy an update to geo-replicated container image</span></span>](./container-registry-tutorial-deploy-update.md)

<!-- IMAGES -->
[deploy-app-portal-01]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-01.png
[deploy-app-portal-02]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-02.png
[deploy-app-portal-03]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-03.png
[deploy-app-portal-04]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-04.png
[deploy-app-portal-05]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-05.png
[deploy-app-portal-06]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-06.png
[deploy-app-portal-07]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-07.png
[deployed-app-westus]: ./media/container-registry-tutorial-deploy-app/deployed-app-westus.png
[deployed-app-eastus]: ./media/container-registry-tutorial-deploy-app/deployed-app-eastus.png