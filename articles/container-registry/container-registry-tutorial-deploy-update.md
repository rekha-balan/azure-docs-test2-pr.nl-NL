---
title: Azure Container Registry tutorial - Push an updated image to regional deployments
description: Push a modified Docker image to your geo-replicated Azure contain registry, then see the changes automatically deployed to web apps running in multiple regions. Part three of a three-part series.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: tutorial
ms.date: 04/30/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 8edb35b91327bde1fa824ec456b8a98962adb7ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868527"
---
# <a name="tutorial-push-an-updated-image-to-regional-deployments"></a><span data-ttu-id="efc9a-104">Tutorial: Push an updated image to regional deployments</span><span class="sxs-lookup"><span data-stu-id="efc9a-104">Tutorial: Push an updated image to regional deployments</span></span>

<span data-ttu-id="efc9a-105">This is part three in a three-part tutorial series.</span><span class="sxs-lookup"><span data-stu-id="efc9a-105">This is part three in a three-part tutorial series.</span></span> <span data-ttu-id="efc9a-106">In the [previous tutorial](container-registry-tutorial-deploy-app.md), geo-replication was configured for two different regional Web App deployments.</span><span class="sxs-lookup"><span data-stu-id="efc9a-106">In the [previous tutorial](container-registry-tutorial-deploy-app.md), geo-replication was configured for two different regional Web App deployments.</span></span> <span data-ttu-id="efc9a-107">In this tutorial, you first modify the application, then build a new container image and push it to your geo-replicated registry.</span><span class="sxs-lookup"><span data-stu-id="efc9a-107">In this tutorial, you first modify the application, then build a new container image and push it to your geo-replicated registry.</span></span> <span data-ttu-id="efc9a-108">Finally, you view the change, deployed automatically by Azure Container Registry webhooks, in both Web App instances.</span><span class="sxs-lookup"><span data-stu-id="efc9a-108">Finally, you view the change, deployed automatically by Azure Container Registry webhooks, in both Web App instances.</span></span>

<span data-ttu-id="efc9a-109">In this tutorial, the final part in the series:</span><span class="sxs-lookup"><span data-stu-id="efc9a-109">In this tutorial, the final part in the series:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="efc9a-110">Modify the web application HTML</span><span class="sxs-lookup"><span data-stu-id="efc9a-110">Modify the web application HTML</span></span>
> * <span data-ttu-id="efc9a-111">Build and tag the Docker image</span><span class="sxs-lookup"><span data-stu-id="efc9a-111">Build and tag the Docker image</span></span>
> * <span data-ttu-id="efc9a-112">Push the change to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="efc9a-112">Push the change to Azure Container Registry</span></span>
> * <span data-ttu-id="efc9a-113">View the updated app in two different regions</span><span class="sxs-lookup"><span data-stu-id="efc9a-113">View the updated app in two different regions</span></span>

<span data-ttu-id="efc9a-114">If you've not yet configured the two *Web App for Containers* regional deployments, return to the previous tutorial in the series, [Deploy web app from Azure Container Registry](container-registry-tutorial-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="efc9a-114">If you've not yet configured the two *Web App for Containers* regional deployments, return to the previous tutorial in the series, [Deploy web app from Azure Container Registry](container-registry-tutorial-deploy-app.md).</span></span>

## <a name="modify-the-web-application"></a><span data-ttu-id="efc9a-115">Modify the web application</span><span class="sxs-lookup"><span data-stu-id="efc9a-115">Modify the web application</span></span>

<span data-ttu-id="efc9a-116">In this step, make a change to the web application that will be highly visible once you push the updated container image to Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="efc9a-116">In this step, make a change to the web application that will be highly visible once you push the updated container image to Azure Container Registry.</span></span>

<span data-ttu-id="efc9a-117">Find the `AcrHelloworld/Views/Home/Index.cshtml` file in the application source you [cloned from GitHub](container-registry-tutorial-prepare-registry.md#get-application-code) in a previous tutorial and open it in your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="efc9a-117">Find the `AcrHelloworld/Views/Home/Index.cshtml` file in the application source you [cloned from GitHub](container-registry-tutorial-prepare-registry.md#get-application-code) in a previous tutorial and open it in your favorite text editor.</span></span> <span data-ttu-id="efc9a-118">Add the following line below the existing `<h1>` line:</span><span class="sxs-lookup"><span data-stu-id="efc9a-118">Add the following line below the existing `<h1>` line:</span></span>

```html
<h1>MODIFIED</h1>
```

<span data-ttu-id="efc9a-119">Your modified `Index.cshtml` should look similar to:</span><span class="sxs-lookup"><span data-stu-id="efc9a-119">Your modified `Index.cshtml` should look similar to:</span></span>

```html
@{
    ViewData["Title"] = "Azure Container Registry :: Geo-replication";
}
<style>
    body {
        background-image: url('images/azure-regions.png');
        background-size: cover;
    }
    .footer {
        position: fixed;
        bottom: 0px;
        width: 100%;
    }
</style>

<h1 style="text-align:center;color:blue">Hello World from:  @ViewData["REGION"]</h1>
<h1>MODIFIED</h1>
<div class="footer">
    <ul>
        <li>Registry URL: @ViewData["REGISTRYURL"]</li>
        <li>Registry IP: @ViewData["REGISTRYIP"]</li>
        <li>Registry Region: @ViewData["REGION"]</li>
    </ul>
</div>
```

## <a name="rebuild-the-image"></a><span data-ttu-id="efc9a-120">Rebuild the image</span><span class="sxs-lookup"><span data-stu-id="efc9a-120">Rebuild the image</span></span>

<span data-ttu-id="efc9a-121">Now that you've updated the web application, rebuild its container image.</span><span class="sxs-lookup"><span data-stu-id="efc9a-121">Now that you've updated the web application, rebuild its container image.</span></span> <span data-ttu-id="efc9a-122">As before, use the fully qualified image name, including the login server's fully qualified domain name (FQDN), for the tag:</span><span class="sxs-lookup"><span data-stu-id="efc9a-122">As before, use the fully qualified image name, including the login server's fully qualified domain name (FQDN), for the tag:</span></span>

```bash
docker build . -f ./AcrHelloworld/Dockerfile -t <acrName>.azurecr.io/acr-helloworld:v1
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="efc9a-123">Push image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="efc9a-123">Push image to Azure Container Registry</span></span>

<span data-ttu-id="efc9a-124">Next, push the updated *acr-helloworld* container image to your geo-replicated registry.</span><span class="sxs-lookup"><span data-stu-id="efc9a-124">Next, push the updated *acr-helloworld* container image to your geo-replicated registry.</span></span> <span data-ttu-id="efc9a-125">Here, you're executing a single `docker push` command to deploy the updated image to the registry replicas in both the *West US* and *East US* regions.</span><span class="sxs-lookup"><span data-stu-id="efc9a-125">Here, you're executing a single `docker push` command to deploy the updated image to the registry replicas in both the *West US* and *East US* regions.</span></span>

```bash
docker push <acrName>.azurecr.io/acr-helloworld:v1
```

<span data-ttu-id="efc9a-126">Your `docker push` output should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="efc9a-126">Your `docker push` output should be similar to the following:</span></span>

```console
$ docker push uniqueregistryname.azurecr.io/acr-helloworld:v1
The push refers to a repository [uniqueregistryname.azurecr.io/acr-helloworld]
5b9454e91555: Pushed
d6803756744a: Layer already exists
b7b1f3a15779: Layer already exists
a89567dff12d: Layer already exists
59c7b561ff56: Layer already exists
9a2f9413d9e4: Layer already exists
a75caa09eb1f: Layer already exists
v1: digest: sha256:4c3f2211569346fbe2d1006c18cbea2a4a9dcc1eb3a078608cef70d3a186ec7a size: 1792
```

## <a name="view-the-webhook-logs"></a><span data-ttu-id="efc9a-127">View the webhook logs</span><span class="sxs-lookup"><span data-stu-id="efc9a-127">View the webhook logs</span></span>

<span data-ttu-id="efc9a-128">While the image is being replicated, you can see the Azure Container Registry webhooks being triggered.</span><span class="sxs-lookup"><span data-stu-id="efc9a-128">While the image is being replicated, you can see the Azure Container Registry webhooks being triggered.</span></span>

<span data-ttu-id="efc9a-129">To see the regional webhooks that were created when you deployed the container to *Web Apps for Containers* in a previous tutorial, navigate to your container registry in the Azure portal, then select **Webhooks** under **SERVICES**.</span><span class="sxs-lookup"><span data-stu-id="efc9a-129">To see the regional webhooks that were created when you deployed the container to *Web Apps for Containers* in a previous tutorial, navigate to your container registry in the Azure portal, then select **Webhooks** under **SERVICES**.</span></span>

![Container registry Webhooks in the Azure portal][tutorial-portal-01]

<span data-ttu-id="efc9a-131">Select each Webhook to see the history of its calls and responses.</span><span class="sxs-lookup"><span data-stu-id="efc9a-131">Select each Webhook to see the history of its calls and responses.</span></span> <span data-ttu-id="efc9a-132">You should see a row for the **push** action in the logs of both Webhooks.</span><span class="sxs-lookup"><span data-stu-id="efc9a-132">You should see a row for the **push** action in the logs of both Webhooks.</span></span> <span data-ttu-id="efc9a-133">Here, the log for the Webhook located in the *West US* region shows the **push** action triggered by the `docker push` in the previous step:</span><span class="sxs-lookup"><span data-stu-id="efc9a-133">Here, the log for the Webhook located in the *West US* region shows the **push** action triggered by the `docker push` in the previous step:</span></span>

![Container registry Webhook log in the Azure portal (West US)][tutorial-portal-02]

## <a name="view-the-updated-web-app"></a><span data-ttu-id="efc9a-135">View the updated web app</span><span class="sxs-lookup"><span data-stu-id="efc9a-135">View the updated web app</span></span>

<span data-ttu-id="efc9a-136">The Webhooks notify Web Apps that a new image has been pushed to the registry, which automatically deploys the updated container to the two regional web apps.</span><span class="sxs-lookup"><span data-stu-id="efc9a-136">The Webhooks notify Web Apps that a new image has been pushed to the registry, which automatically deploys the updated container to the two regional web apps.</span></span>

<span data-ttu-id="efc9a-137">Verify that the application has been updated in both deployments by navigating to both regional Web App deployments in your web browser.</span><span class="sxs-lookup"><span data-stu-id="efc9a-137">Verify that the application has been updated in both deployments by navigating to both regional Web App deployments in your web browser.</span></span> <span data-ttu-id="efc9a-138">As a reminder, you can find the URL for the deployed web app in the top-right of each App Service overview tab.</span><span class="sxs-lookup"><span data-stu-id="efc9a-138">As a reminder, you can find the URL for the deployed web app in the top-right of each App Service overview tab.</span></span>

![App Service overview in the Azure portal][tutorial-portal-03]

<span data-ttu-id="efc9a-140">To see the updated application, select the link in the App Service overview.</span><span class="sxs-lookup"><span data-stu-id="efc9a-140">To see the updated application, select the link in the App Service overview.</span></span> <span data-ttu-id="efc9a-141">Here's an example view of the app running in *West US*:</span><span class="sxs-lookup"><span data-stu-id="efc9a-141">Here's an example view of the app running in *West US*:</span></span>

![Browser view of modified web app running in West US region][deployed-app-westus-modified]

<span data-ttu-id="efc9a-143">Verify that the updated container image was also deployed to the *East US* deployment by viewing it in your browser.</span><span class="sxs-lookup"><span data-stu-id="efc9a-143">Verify that the updated container image was also deployed to the *East US* deployment by viewing it in your browser.</span></span>

![Browser view of modified web app running in East US region][deployed-app-eastus-modified]

<span data-ttu-id="efc9a-145">With a single `docker push`, you've automatically updated the web application running in both regional Web App deployments.</span><span class="sxs-lookup"><span data-stu-id="efc9a-145">With a single `docker push`, you've automatically updated the web application running in both regional Web App deployments.</span></span> <span data-ttu-id="efc9a-146">And, Azure Container Registry served the container images from the repositories located closest to each deployment.</span><span class="sxs-lookup"><span data-stu-id="efc9a-146">And, Azure Container Registry served the container images from the repositories located closest to each deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efc9a-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="efc9a-147">Next steps</span></span>

<span data-ttu-id="efc9a-148">In this tutorial, you updated and pushed a new version of the web application container to your geo-replicated registry.</span><span class="sxs-lookup"><span data-stu-id="efc9a-148">In this tutorial, you updated and pushed a new version of the web application container to your geo-replicated registry.</span></span> <span data-ttu-id="efc9a-149">Webhooks in Azure Container Registry notified Web Apps for Containers of the update, which triggered a local pull from the nearest registry replica.</span><span class="sxs-lookup"><span data-stu-id="efc9a-149">Webhooks in Azure Container Registry notified Web Apps for Containers of the update, which triggered a local pull from the nearest registry replica.</span></span>

### <a name="acr-build-automated-image-build-and-patch"></a><span data-ttu-id="efc9a-150">ACR Build: Automated image build and patch</span><span class="sxs-lookup"><span data-stu-id="efc9a-150">ACR Build: Automated image build and patch</span></span>

<span data-ttu-id="efc9a-151">In addition to geo-replication, ACR Build is another feature of Azure Container Registry that can help optimize your container deployment pipeline.</span><span class="sxs-lookup"><span data-stu-id="efc9a-151">In addition to geo-replication, ACR Build is another feature of Azure Container Registry that can help optimize your container deployment pipeline.</span></span> <span data-ttu-id="efc9a-152">Start with the ACR Build overview to get an idea of its capabilities:</span><span class="sxs-lookup"><span data-stu-id="efc9a-152">Start with the ACR Build overview to get an idea of its capabilities:</span></span>

[<span data-ttu-id="efc9a-153">Automate OS and framework patching with ACR Build</span><span class="sxs-lookup"><span data-stu-id="efc9a-153">Automate OS and framework patching with ACR Build</span></span>](container-registry-build-overview.md)

<!-- IMAGES -->
[deployed-app-eastus-modified]: ./media/container-registry-tutorial-deploy-update/deployed-app-eastus-modified.png
[deployed-app-westus-modified]: ./media/container-registry-tutorial-deploy-update/deployed-app-westus-modified.png
[local-container-01]: ./media/container-registry-tutorial-deploy-update/local-container-01.png
[tutorial-portal-01]: ./media/container-registry-tutorial-deploy-update/tutorial-portal-01.png
[tutorial-portal-02]: ./media/container-registry-tutorial-deploy-update/tutorial-portal-02.png
[tutorial-portal-03]: ./media/container-registry-tutorial-deploy-update/tutorial-portal-03.png