---
title: Quickstart - Send Azure Container Registry events to Event Grid
description: In this quickstart, you enable Event Grid events for your container registry, then send container image push and delete events to a sample application.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 08/23/2018
ms.author: marsma
ms.openlocfilehash: 6ff83885ba80f0399f7b085970b1191e8e4cd999
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867079"
---
# <a name="quickstart-send-container-registry-events-to-event-grid"></a><span data-ttu-id="86718-103">Quickstart: Send container registry events to Event Grid</span><span class="sxs-lookup"><span data-stu-id="86718-103">Quickstart: Send container registry events to Event Grid</span></span>

<span data-ttu-id="86718-104">Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.</span><span class="sxs-lookup"><span data-stu-id="86718-104">Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.</span></span> <span data-ttu-id="86718-105">In this quickstart, you use the Azure CLI to create a container registry, subscribe to registry events, then deploy a sample web application to receive the events.</span><span class="sxs-lookup"><span data-stu-id="86718-105">In this quickstart, you use the Azure CLI to create a container registry, subscribe to registry events, then deploy a sample web application to receive the events.</span></span> <span data-ttu-id="86718-106">Finally, you trigger container image `push` and `delete` events and view the event payload in the sample application.</span><span class="sxs-lookup"><span data-stu-id="86718-106">Finally, you trigger container image `push` and `delete` events and view the event payload in the sample application.</span></span>

<span data-ttu-id="86718-107">After you complete the steps in this article, events sent from your container registry to Event Grid appear in the sample web app:</span><span class="sxs-lookup"><span data-stu-id="86718-107">After you complete the steps in this article, events sent from your container registry to Event Grid appear in the sample web app:</span></span>

![Web browser rendering the sample web application with three received events][sample-app-01]

<span data-ttu-id="86718-109">If you don't have an Azure subscription, create a [free account][azure-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="86718-109">If you don't have an Azure subscription, create a [free account][azure-account] before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="86718-110">The Azure CLI commands in this article are formatted for the **Bash** shell.</span><span class="sxs-lookup"><span data-stu-id="86718-110">The Azure CLI commands in this article are formatted for the **Bash** shell.</span></span> <span data-ttu-id="86718-111">If you're using a different shell like PowerShell or Command Prompt, you may need to adjust line continuation characters or variable assignment lines accordingly.</span><span class="sxs-lookup"><span data-stu-id="86718-111">If you're using a different shell like PowerShell or Command Prompt, you may need to adjust line continuation characters or variable assignment lines accordingly.</span></span> <span data-ttu-id="86718-112">This article uses variables to minimize the amount of command editing required.</span><span class="sxs-lookup"><span data-stu-id="86718-112">This article uses variables to minimize the amount of command editing required.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="86718-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="86718-113">Create a resource group</span></span>

<span data-ttu-id="86718-114">An Azure resource group is a logical container in which you deploy and manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="86718-114">An Azure resource group is a logical container in which you deploy and manage your Azure resources.</span></span> <span data-ttu-id="86718-115">The following [az group create][az-group-create] command creates a resource group named *myResourceGroup* in the *eastus* region.</span><span class="sxs-lookup"><span data-stu-id="86718-115">The following [az group create][az-group-create] command creates a resource group named *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="86718-116">If you want to use a different name for your resource group, set `RESOURCE_GROUP_NAME` to a different value.</span><span class="sxs-lookup"><span data-stu-id="86718-116">If you want to use a different name for your resource group, set `RESOURCE_GROUP_NAME` to a different value.</span></span>

```azurecli-interactive
RESOURCE_GROUP_NAME=myResourceGroup

az group create --name $RESOURCE_GROUP_NAME --location eastus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="86718-117">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="86718-117">Create a container registry</span></span>

<span data-ttu-id="86718-118">Next, deploy a container registry into the resource group with the following commands.</span><span class="sxs-lookup"><span data-stu-id="86718-118">Next, deploy a container registry into the resource group with the following commands.</span></span> <span data-ttu-id="86718-119">Before you run the [az acr create][az-acr-create] command, set `ACR_NAME` to a name for your registry.</span><span class="sxs-lookup"><span data-stu-id="86718-119">Before you run the [az acr create][az-acr-create] command, set `ACR_NAME` to a name for your registry.</span></span> <span data-ttu-id="86718-120">The name must be unique within Azure, and is restricted to 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="86718-120">The name must be unique within Azure, and is restricted to 5-50 alphanumeric characters.</span></span>

```azurecli-interactive
ACR_NAME=<acrName>

az acr create --resource-group $RESOURCE_GROUP_NAME --name $ACR_NAME --sku Basic
```

<span data-ttu-id="86718-121">Once the registry has been created, the Azure CLI returns output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="86718-121">Once the registry has been created, the Azure CLI returns output similar to the following:</span></span>

```json
{
  "adminUserEnabled": false,
  "creationDate": "2018-08-16T20:02:46.569509+00:00",
  "id": "/subscriptions/<Subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myregistry",
  "location": "eastus",
  "loginServer": "myregistry.azurecr.io",
  "name": "myregistry",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```

## <a name="create-an-event-endpoint"></a><span data-ttu-id="86718-122">Create an event endpoint</span><span class="sxs-lookup"><span data-stu-id="86718-122">Create an event endpoint</span></span>

<span data-ttu-id="86718-123">In this section, you use a Resource Manager template located in a GitHub repository to deploy a pre-built sample web application to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="86718-123">In this section, you use a Resource Manager template located in a GitHub repository to deploy a pre-built sample web application to Azure App Service.</span></span> <span data-ttu-id="86718-124">Later, you subscribe to your registry's Event Grid events and specify this app as the endpoint to which the events are sent.</span><span class="sxs-lookup"><span data-stu-id="86718-124">Later, you subscribe to your registry's Event Grid events and specify this app as the endpoint to which the events are sent.</span></span>

<span data-ttu-id="86718-125">To deploy the sample app, set `SITE_NAME` to a unique name for your web app, and execute the following commands.</span><span class="sxs-lookup"><span data-stu-id="86718-125">To deploy the sample app, set `SITE_NAME` to a unique name for your web app, and execute the following commands.</span></span> <span data-ttu-id="86718-126">The site name must be unique within Azure because it forms part of the fully qualified domain name (FQDN) of the web app.</span><span class="sxs-lookup"><span data-stu-id="86718-126">The site name must be unique within Azure because it forms part of the fully qualified domain name (FQDN) of the web app.</span></span> <span data-ttu-id="86718-127">In a later section, you navigate to the app's FQDN in a web browser to view your registry's events.</span><span class="sxs-lookup"><span data-stu-id="86718-127">In a later section, you navigate to the app's FQDN in a web browser to view your registry's events.</span></span>

```azurecli-interactive
SITE_NAME=<your-site-name>

az group deployment create \
    --resource-group $RESOURCE_GROUP_NAME \
    --template-uri "https://raw.githubusercontent.com/Azure-Samples/azure-event-grid-viewer/master/azuredeploy.json" \
    --parameters siteName=$SITE_NAME hostingPlanName=$SITE_NAME-plan
```

<span data-ttu-id="86718-128">Once the deployment has succeeded (it might take a few minutes), open a browser and navigate to your web app to make sure it's running:</span><span class="sxs-lookup"><span data-stu-id="86718-128">Once the deployment has succeeded (it might take a few minutes), open a browser and navigate to your web app to make sure it's running:</span></span>

`http://<your-site-name>.azurewebsites.net`

<span data-ttu-id="86718-129">You should see the sample app rendered with no event messages displayed:</span><span class="sxs-lookup"><span data-stu-id="86718-129">You should see the sample app rendered with no event messages displayed:</span></span>

![Web browser showing sample web app with no events displayed][sample-app-02]

[!INCLUDE [event-grid-register-provider-cli.md](../../includes/event-grid-register-provider-cli.md)]

## <a name="subscribe-to-registry-events"></a><span data-ttu-id="86718-131">Subscribe to registry events</span><span class="sxs-lookup"><span data-stu-id="86718-131">Subscribe to registry events</span></span>

<span data-ttu-id="86718-132">In Event Grid, you subscribe to a *topic* to tell it which events you want to track, and where to send them.</span><span class="sxs-lookup"><span data-stu-id="86718-132">In Event Grid, you subscribe to a *topic* to tell it which events you want to track, and where to send them.</span></span> <span data-ttu-id="86718-133">The following [az eventgrid event-subscription create][az-eventgrid-event-subscription-create] command subscribes to the container registry you created, and specifies your web app's URL as the endpoint to which it should send events.</span><span class="sxs-lookup"><span data-stu-id="86718-133">The following [az eventgrid event-subscription create][az-eventgrid-event-subscription-create] command subscribes to the container registry you created, and specifies your web app's URL as the endpoint to which it should send events.</span></span> <span data-ttu-id="86718-134">The environment variables you populated in earlier sections are reused here, so no edits are required.</span><span class="sxs-lookup"><span data-stu-id="86718-134">The environment variables you populated in earlier sections are reused here, so no edits are required.</span></span>

```azurecli-interactive
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME --query id --output tsv)
APP_ENDPOINT=https://$SITE_NAME.azurewebsites.net/api/updates

az eventgrid event-subscription create \
    --name event-sub-acr \
    --resource-id $ACR_REGISTRY_ID \
    --endpoint $APP_ENDPOINT
```

<span data-ttu-id="86718-135">When the subscription is completed, you should output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="86718-135">When the subscription is completed, you should output similar to the following:</span></span>

```JSON
{
  "destination": {
    "endpointBaseUrl": "https://eventgridviewer.azurewebsites.net/api/updates",
    "endpointType": "WebHook",
    "endpointUrl": null
  },
  "filter": {
    "includedEventTypes": [
      "All"
    ],
    "isSubjectCaseSensitive": null,
    "subjectBeginsWith": "",
    "subjectEndsWith": ""
  },
  "id": "/subscriptions/<Subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myregistry/providers/Microsoft.EventGrid/eventSubscriptions/event-sub-acr",
  "labels": null,
  "name": "event-sub-acr",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "topic": "/subscriptions/<Subscription ID>/resourceGroups/myresourcegroup/providers/microsoft.containerregistry/registries/myregistry",
  "type": "Microsoft.EventGrid/eventSubscriptions"
}
```

## <a name="trigger-registry-events"></a><span data-ttu-id="86718-136">Trigger registry events</span><span class="sxs-lookup"><span data-stu-id="86718-136">Trigger registry events</span></span>

<span data-ttu-id="86718-137">Now that the sample app is up and running and you've subscribed to your registry with Event Grid, you're ready to generate some events.</span><span class="sxs-lookup"><span data-stu-id="86718-137">Now that the sample app is up and running and you've subscribed to your registry with Event Grid, you're ready to generate some events.</span></span> <span data-ttu-id="86718-138">In this section, you use ACR Build to build and push a container image to your registry.</span><span class="sxs-lookup"><span data-stu-id="86718-138">In this section, you use ACR Build to build and push a container image to your registry.</span></span> <span data-ttu-id="86718-139">ACR Build is a feature of Azure Container Registry that allows you to build container images in the cloud, without needing the Docker Engine installed on your local machine.</span><span class="sxs-lookup"><span data-stu-id="86718-139">ACR Build is a feature of Azure Container Registry that allows you to build container images in the cloud, without needing the Docker Engine installed on your local machine.</span></span>

### <a name="build-and-push-image"></a><span data-ttu-id="86718-140">Build and push image</span><span class="sxs-lookup"><span data-stu-id="86718-140">Build and push image</span></span>

<span data-ttu-id="86718-141">Execute the following Azure CLI command to build a container image from the contents of a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="86718-141">Execute the following Azure CLI command to build a container image from the contents of a GitHub repository.</span></span> <span data-ttu-id="86718-142">By default, ACR Build automatically pushes a successfully built image to your registry, which generates the `ImagePushed` event.</span><span class="sxs-lookup"><span data-stu-id="86718-142">By default, ACR Build automatically pushes a successfully built image to your registry, which generates the `ImagePushed` event.</span></span>

```azurecli-interactive
az acr build --registry $ACR_NAME --image myimage:v1 https://github.com/Azure-Samples/acr-build-helloworld-node.git
```

<span data-ttu-id="86718-143">You should see output similar to the following while ACR Build builds and then pushes your image.</span><span class="sxs-lookup"><span data-stu-id="86718-143">You should see output similar to the following while ACR Build builds and then pushes your image.</span></span> <span data-ttu-id="86718-144">The following sample output has been truncated for brevity.</span><span class="sxs-lookup"><span data-stu-id="86718-144">The following sample output has been truncated for brevity.</span></span>

```console
$ az acr build -r $ACR_NAME --image myimage:v1 https://github.com/Azure-Samples/acr-build-helloworld-node.git
Sending build context to ACR...
Queued a build with build ID: aa2
Waiting for build agent...
2018/08/16 22:19:38 Using acb_vol_27a2afa6-27dc-4ae4-9e52-6d6c8b7455b2 as the home volume
2018/08/16 22:19:38 Setting up Docker configuration...
2018/08/16 22:19:39 Successfully set up Docker configuration
2018/08/16 22:19:39 Logging in to registry: myregistry.azurecr.io
2018/08/16 22:19:55 Successfully logged in
Sending build context to Docker daemon  94.72kB
Step 1/5 : FROM node:9-alpine
...
```

<span data-ttu-id="86718-145">To verify that the built image is in your registry, execute the following command to view the tags in the "myimage" repository:</span><span class="sxs-lookup"><span data-stu-id="86718-145">To verify that the built image is in your registry, execute the following command to view the tags in the "myimage" repository:</span></span>

```azurecli-interactive
az acr repository show-tags --name $ACR_NAME --repository myimage
```

<span data-ttu-id="86718-146">The "v1" tag of the image you built should appear in the output, similar to the following:</span><span class="sxs-lookup"><span data-stu-id="86718-146">The "v1" tag of the image you built should appear in the output, similar to the following:</span></span>

```console
$ az acr repository show-tags --name $ACR_NAME --repository myimage
[
  "v1"
]
```

### <a name="delete-the-image"></a><span data-ttu-id="86718-147">Delete the image</span><span class="sxs-lookup"><span data-stu-id="86718-147">Delete the image</span></span>

<span data-ttu-id="86718-148">Now, generate an `ImageDeleted` event by deleting the image with the [az acr repository delete][az-acr-repository-delete] command:</span><span class="sxs-lookup"><span data-stu-id="86718-148">Now, generate an `ImageDeleted` event by deleting the image with the [az acr repository delete][az-acr-repository-delete] command:</span></span>

```azurecli-interactive
az acr repository delete --name $ACR_NAME --image myimage:v1
```

<span data-ttu-id="86718-149">You should see output similar to the following, asking for confirmation to delete the manifest and associated images:</span><span class="sxs-lookup"><span data-stu-id="86718-149">You should see output similar to the following, asking for confirmation to delete the manifest and associated images:</span></span>

```console
$ az acr repository delete --name $ACR_NAME --image myimage:v1
This operation will delete the manifest 'sha256:f15fa9d0a69081ba93eee308b0e475a54fac9c682196721e294b2bc20ab23a1b' and all the following images: 'myimage:v1'.
Are you sure you want to continue? (y/n): y
```

## <a name="view-registry-events"></a><span data-ttu-id="86718-150">View registry events</span><span class="sxs-lookup"><span data-stu-id="86718-150">View registry events</span></span>

<span data-ttu-id="86718-151">You've now pushed an image to your registry and then deleted it.</span><span class="sxs-lookup"><span data-stu-id="86718-151">You've now pushed an image to your registry and then deleted it.</span></span> <span data-ttu-id="86718-152">Navigate to your Event Grid Viewer web app, and you should see both `ImageDeleted` and `ImagePushed` events.</span><span class="sxs-lookup"><span data-stu-id="86718-152">Navigate to your Event Grid Viewer web app, and you should see both `ImageDeleted` and `ImagePushed` events.</span></span> <span data-ttu-id="86718-153">You might also see a subscription validation event generated by executing the command in the [Subscribe to registry events](#subscribe-to-registry-events) section.</span><span class="sxs-lookup"><span data-stu-id="86718-153">You might also see a subscription validation event generated by executing the command in the [Subscribe to registry events](#subscribe-to-registry-events) section.</span></span>

<span data-ttu-id="86718-154">The following screenshot shows the sample app with the three events, and the `ImageDeleted` event is expanded to show its details.</span><span class="sxs-lookup"><span data-stu-id="86718-154">The following screenshot shows the sample app with the three events, and the `ImageDeleted` event is expanded to show its details.</span></span>

![Web browser showing the sample app with ImagePushed and ImageDeleted events][sample-app-03]

<span data-ttu-id="86718-156">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="86718-156">Congratulations!</span></span> <span data-ttu-id="86718-157">If you see the `ImagePushed` and `ImageDeleted` events, your registry is sending events to Event Grid, and Event Grid is forwarding those events to your web app endpoint.</span><span class="sxs-lookup"><span data-stu-id="86718-157">If you see the `ImagePushed` and `ImageDeleted` events, your registry is sending events to Event Grid, and Event Grid is forwarding those events to your web app endpoint.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="86718-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="86718-158">Clean up resources</span></span>

<span data-ttu-id="86718-159">Once you're done with the resources you created in this quickstart, you can delete them all with the following Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="86718-159">Once you're done with the resources you created in this quickstart, you can delete them all with the following Azure CLI command.</span></span> <span data-ttu-id="86718-160">When you delete a resource group, all of the resources it contains are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="86718-160">When you delete a resource group, all of the resources it contains are permanently deleted.</span></span>

<span data-ttu-id="86718-161">**WARNING**: This operation is irreversible.</span><span class="sxs-lookup"><span data-stu-id="86718-161">**WARNING**: This operation is irreversible.</span></span> <span data-ttu-id="86718-162">Be sure you no longer need any of the resources in the group before running the command.</span><span class="sxs-lookup"><span data-stu-id="86718-162">Be sure you no longer need any of the resources in the group before running the command.</span></span>

```azurecli-interactive
az group delete --name $RESOURCE_GROUP_NAME
```

## <a name="event-grid-event-schema"></a><span data-ttu-id="86718-163">Event Grid event schema</span><span class="sxs-lookup"><span data-stu-id="86718-163">Event Grid event schema</span></span>

<span data-ttu-id="86718-164">You can find the Azure Container Registry event message schema reference in the Event Grid documentation:</span><span class="sxs-lookup"><span data-stu-id="86718-164">You can find the Azure Container Registry event message schema reference in the Event Grid documentation:</span></span>

[<span data-ttu-id="86718-165">Azure Event Grid event schema for Container Registry</span><span class="sxs-lookup"><span data-stu-id="86718-165">Azure Event Grid event schema for Container Registry</span></span>](../event-grid/event-schema-container-registry.md)

## <a name="next-steps"></a><span data-ttu-id="86718-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="86718-166">Next steps</span></span>

<span data-ttu-id="86718-167">In this quickstart, you deployed a container registry, built an image with ACR Build, deleted it, and have consumed your registry's events from Event Grid with a sample application.</span><span class="sxs-lookup"><span data-stu-id="86718-167">In this quickstart, you deployed a container registry, built an image with ACR Build, deleted it, and have consumed your registry's events from Event Grid with a sample application.</span></span> <span data-ttu-id="86718-168">Next, move on to the ACR Build tutorial to learn more about building container images in the cloud, including automated builds on base image update:</span><span class="sxs-lookup"><span data-stu-id="86718-168">Next, move on to the ACR Build tutorial to learn more about building container images in the cloud, including automated builds on base image update:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="86718-169">Build container images in the cloud with ACR Build</span><span class="sxs-lookup"><span data-stu-id="86718-169">Build container images in the cloud with ACR Build</span></span>](container-registry-tutorial-quick-build.md)

<!-- IMAGES -->
[sample-app-01]: ./media/container-registry-event-grid-quickstart/sample-app-01.png
[sample-app-02]: ./media/container-registry-event-grid-quickstart/sample-app-02-no-events.png
[sample-app-03]: ./media/container-registry-event-grid-quickstart/sample-app-03-with-events.png

<!-- LINKS - External -->
[azure-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F
[sample-app]: https://github.com/dbarkol/azure-event-grid-viewer

<!-- LINKS - Internal -->
[az-acr-create]: /cli/azure/acr/repository#az-acr-create
[az-acr-repository-delete]: /cli/azure/acr/repository#az-acr-repository-delete
[az-eventgrid-event-subscription-create]: /cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create
[az-group-create]: /cli/azure/group#az-group-create
